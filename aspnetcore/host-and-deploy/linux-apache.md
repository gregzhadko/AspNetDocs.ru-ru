---
title: Размещение ASP.NET Core в операционной системе Linux с Apache
description: Процедура настройки Apache в качестве обратного прокси-сервера в CentOS для перенаправления трафика HTTP в веб-приложение ASP.NET Core, выполняемое в Kestrel.
author: spboyer
ms.author: spboyer
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 0dec9c657134bba3224a1fbb69aaefaaba753404
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026491"
---
# <a name="host-aspnet-core-on-linux-with-apache"></a>Размещение ASP.NET Core в операционной системе Linux с Apache

Автор: [Шейн Бойер (Shayne Boyer)](https://github.com/spboyer)

Из этого руководства вы узнаете, как настроить [Apache](https://httpd.apache.org/) в качестве обратного прокси-сервера в [CentOS 7](https://www.centos.org/) для перенаправления трафика HTTP в веб-приложение ASP.NET Core, выполняемое на сервере [Kestrel](xref:fundamentals/servers/kestrel). [Расширение mod_proxy](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) и связанные с ним модули создают обратный прокси-сервер.

## <a name="prerequisites"></a>Предварительные требования

* Сервер под управлением CentOS 7 и учетная запись обычного пользователя с правами sudo.
* Установите среду выполнения .NET Core на сервере.
   1. Перейдите на [страницу всех загрузок .NET Core](https://www.microsoft.com/net/download/all).
   1. Выберите последнюю не предварительную версию среды выполнения из списка под заголовком **Среда выполнения**.
   1. Сделайте выбор и следуйте инструкциям для CentOS/Oracle.
* Существующее приложение ASP.NET Core.

## <a name="publish-and-copy-over-the-app"></a>Публикация и копирование приложения

Настройте приложение, чтобы [его развертывание зависело от платформы](/dotnet/core/deploying/#framework-dependent-deployments-fdd).

Запустите [dotnet publish](/dotnet/core/tools/dotnet-publish) в среде разработки, чтобы упаковать приложение в каталог (например, *bin/Release/&lt;target_framework_moniker&gt;/publish*), который может выполняться на сервере:

```console
dotnet publish --configuration Release
```

Приложение может быть опубликовано как [автономное развертывание](/dotnet/core/deploying/#self-contained-deployments-scd), если вы предпочитаете не сохранять среду выполнения .NET Core на сервере.

Скопируйте приложение ASP.NET Core на сервер с помощью инструмента, интегрированного в ваш рабочий процесс (например, SCP или SFTP). Обычно веб-приложения находятся в каталоге *var* (например, *var/www/helloapp*).

> [!NOTE]
> Если развертывание выполняется в рабочей среде, рабочий процесс непрерывной интеграции автоматически опубликует приложение и скопирует его ресурсы на сервер.

## <a name="configure-a-proxy-server"></a>Настройка прокси-сервера

Обратный прокси-сервер — это стандартный вариант настройки для обслуживания динамических веб-приложений. Обратный прокси-сервер завершает HTTP-запрос и перенаправляет его в приложение ASP.NET.

Прокси-сервер перенаправляет запросы клиента на другой сервер, а не обрабатывает их самостоятельно. Обратный прокси-сервер перенаправляет запросы в фиксированное назначение обычно от имени клиентов. При работе с этим руководством мы настроим Apache в качестве обратного прокси-сервера, который работает на том же сервере, где Kestrel предоставляет приложение ASP.NET Core.

Так как запросы перенаправляются обратным прокси-сервером, используйте [ПО промежуточного слоя перенаправления заголовков](xref:host-and-deploy/proxy-load-balancer), которое входит в пакет [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/). Это ПО обновляет `Request.Scheme`, используя заголовок `X-Forwarded-Proto`, что обеспечивает правильную работу URI перенаправления и других политик безопасности.

Любой компонент, который зависит от схемы, например проверка подлинности, генерация ссылок, перенаправление и геолокация, должен находиться после вызова ПО промежуточного слоя перенаправления заголовков. Как правило, ПО промежуточного слоя перенаправления заголовков должно выполняться до остального ПО промежуточного слоя, за исключением ПО промежуточного слоя для диагностики и обработки ошибок. Такой порядок гарантирует, что ПО промежуточного слоя, полагающееся на сведения о перенаправленных заголовках, может использовать значения заголовков для обработки.

::: moniker range=">= aspnetcore-2.0"

Вызовите метод <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> в методе `Startup.Configure` перед вызовом <xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*> или другого ПО промежуточного слоя, предназначенного для проверки подлинности. В ПО промежуточного слоя настройте перенаправление заголовков `X-Forwarded-For` и `X-Forwarded-Proto`:

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Вызовите метод <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> в методе `Startup.Configure` перед вызовом <xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*> и <xref:Microsoft.AspNetCore.Builder.FacebookAppBuilderExtensions.UseFacebookAuthentication*> или другого ПО промежуточного слоя, предназначенного для проверки подлинности. В ПО промежуточного слоя настройте перенаправление заголовков `X-Forwarded-For` и `X-Forwarded-Proto`:

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

::: moniker-end

Если параметр <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions> не задан для ПО промежуточного слоя, по умолчанию перенаправляются заголовки `None`.

По умолчанию доверенными считаются только прокси-серверы, работающие на localhost (127.0.0.1, [:: 1]). Если запросы между Интернетом и веб-сервером обрабатывают другие прокси-серверы или сети организации, добавьте их в список <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> или <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> с помощью <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions>. Следующий пример добавляет доверенный прокси-сервер с IP-адресом 10.0.0.100 в ПО промежуточного слоя для перенаправления заголовков `KnownProxies` в `Startup.ConfigureServices`:

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.KnownProxies.Add(IPAddress.Parse("10.0.0.100"));
});
```

Дополнительные сведения см. в разделе <xref:host-and-deploy/proxy-load-balancer>.

### <a name="install-apache"></a>Установка Apache

Обновите пакеты CentOS до последних стабильных версий:

```bash
sudo yum update -y
```

Установите веб-сервер Apache на CentOS, выполнив одну команду `yum`:

```bash
sudo yum -y install httpd mod_ssl
```

Пример выходных данных этой команды:

```bash
Downloading packages:
httpd-2.4.6-40.el7.centos.4.x86_64.rpm               | 2.7 MB  00:00:01
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Installing : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 
Verifying  : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 

Installed:
httpd.x86_64 0:2.4.6-40.el7.centos.4

Complete!
```

> [!NOTE]
> В нашем примере выходные данные содержат строку httpd.86_64, так как используется 64-разрядная версия CentOS 7. Чтобы проверить, где установлен Apache, выполните `whereis httpd` из командной строки.

### <a name="configure-apache"></a>Настройка Apache

Файлы конфигурации для Apache находятся в каталоге `/etc/httpd/conf.d/`. В алфавитном порядке обрабатываются все файлы с расширением *.conf*, а также файлы конфигурации модуля из папки `/etc/httpd/conf.modules.d/`, где содержатся файлы конфигурации, необходимые для загрузки модулей.

Создайте для приложения файл конфигурации с именем *helloapp.conf*:

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ServerName www.example.com
    ServerAlias *.example.com
    ErrorLog ${APACHE_LOG_DIR}helloapp-error.log
    CustomLog ${APACHE_LOG_DIR}helloapp-access.log common
</VirtualHost>
```

Блок `VirtualHost` может встречаться несколько раз в одном или нескольких файлах на сервере. С представленным выше файлом конфигурации Apache принимает трафик от любого источника через порт 80. Он обслуживает домен `www.example.com`, а псевдоним `*.example.com` указывает на тот же веб-сайт. Дополнительные сведения см. в статье [о поддержке виртуальных узлов на основе имен](https://httpd.apache.org/docs/current/vhosts/name-based.html). Запросы к корневому каталогу перенаправляются на порт 5000 того же сервера по адресу 127.0.0.1. Для двусторонней связи требуются `ProxyPass` и `ProxyPassReverse`. Сведения о том, как изменить IP-адрес/порт Kestrel, см. в разделе [Kestrel: конфигурация конечной точки](xref:fundamentals/servers/kestrel#endpoint-configuration).

> [!WARNING]
> Если не удастся указать правильную [директиву ServerName](https://httpd.apache.org/docs/current/mod/core.html#servername) в блоке **VirtualHost**, приложение будет иметь значительные уязвимости. Привязки с подстановочными знаками на уровне дочерних доменов (например, `*.example.com`) не создают таких угроз безопасности, если вы полностью контролируете родительский домен (в отличие от варианта `*.com`, создающего уязвимость). Дополнительные сведения см. в документе [rfc7230, раздел 5.4](https://tools.ietf.org/html/rfc7230#section-5.4).

Ведение журнала можно настроить отдельно для каждого `VirtualHost` с помощью директив `ErrorLog` и `CustomLog`. Журналы ошибок сохраняются в расположение `ErrorLog`, а параметр `CustomLog` задает имя и формат для файла журнала. В нашем примере здесь фиксируются сведения о запросах. Для каждого запроса создается одна строка.

Сохраните файл и протестируйте конфигурацию. Если проверка выполнена успешно, ответ должен быть `Syntax [OK]`.

```bash
sudo service httpd configtest
```

Перезапустите Apache.

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitor-the-app"></a>Мониторинг приложения

Теперь Apache настроен на перенаправление запросов к `http://localhost:80` в приложение ASP.NET Core, выполняемое в Kestrel по адресу `http://127.0.0.1:5000`. Но Apache не настроен для управления процессом Kestrel. Для запуска и мониторинга базового веб-приложения используйте *systemd* и создайте файл службы. *systemd* — это система инициализации, предоставляющая различные функции для запуска и остановки процессов, а также управления ими.

### <a name="create-the-service-file"></a>Создание файла службы

Создайте файл определения службы.

```bash
sudo nano /etc/systemd/system/kestrel-helloapp.service
```

Пример файла службы для приложения:

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/www/helloapp
ExecStart=/usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

Если пользователь *apache* в вашей конфигурации еще не используется, его необходимо создать и правильно предоставить ему права владения для соответствующих файлов.

Используйте `TimeoutStopSec`, чтобы настроить время ожидания до завершения работы приложения после начального сигнала прерывания. Если приложение не завершит работу в течение этого периода, оно прерывается сигналом SIGKILL. Укажите значение в секундах без единиц измерения (например, `150`), значение интервала (например, `2min 30s`) или значение `infinity`, которое отключает время ожидания. По умолчанию `TimeoutStopSec` принимает значение `DefaultTimeoutStopSec` в файле конфигурации диспетчера (*systemd-system.conf*, *system.conf.d*, *systemd-user.conf*, *user.conf.d*). В большинстве дистрибутивов по умолчанию устанавливается время ожидания 90 секунд.

```
# The default value is 90 seconds for most distributions.
TimeoutStopSec=90
```

Некоторые значения (например, строки подключения SQL) необходимо экранировать, чтобы поставщики конфигурации могли считать переменные среды. Используйте следующую команду, чтобы создать правильно экранированное значение для файла конфигурации:

```console
systemd-escape "<value-to-escape>"
```

Сохраните файл и включите службу.

```bash
sudo systemctl enable kestrel-helloapp.service
```

Запустите службу и убедитесь, что она работает.

```bash
sudo systemctl start kestrel-helloapp.service
sudo systemctl status kestrel-helloapp.service

● kestrel-helloapp.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-helloapp.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-helloapp.service
            └─9021 /usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
```

Теперь, когда обратный прокси-сервер настроен и *systemd* управляет процессом Kestrel, веб-приложение можно считать полностью настроенным и вы можете обратиться к нему по адресу `http://localhost` из браузера на локальном компьютере. Заголовок **Server** в ответе подтверждает, что приложение ASP.NET Core обслуживается Kestrel.

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="view-logs"></a>Просмотр журналов

Так как веб-приложением, использующим Kestrel, управляет *systemd*, все события и процессы регистрируются в централизованном журнале. Но этот журнал содержит все записи обо всех службах и процессах, управляемых *systemd*. Чтобы просмотреть элементы, связанные с `kestrel-helloapp.service`, используйте следующую команду.

```bash
sudo journalctl -fu kestrel-helloapp.service
```

Чтобы отфильтровать элементы по времени, укажите в команде параметры времени. Например, `--since today` позволяет отфильтровать данные за текущий день, а `--until 1 hour ago` — просмотреть записи за предыдущий час. Дополнительные сведения см. на странице руководства о команде [journalctl](https://www.unix.com/man-page/centos/1/journalctl/).

```bash
sudo journalctl -fu kestrel-helloapp.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="data-protection"></a>Защита данных

[Стек защиты данных в ASP.NET Core](xref:security/data-protection/introduction) используется определенным [ПО промежуточного слоя](xref:fundamentals/middleware/index) ASP.NET Core, включая промежуточное ПО для проверки подлинности (например, промежуточное ПО файлов cookie) и средствами защиты от подделки межсайтовых запросов. Даже если API-интерфейсы защиты данных не вызываются из пользовательского кода, необходимо настроить защиту данных для создания постоянного [хранилища криптографических ключей](xref:security/data-protection/implementation/key-management). Если защита данных не настроена, ключи хранятся в памяти и удаляются при перезапуске приложения.

Если набор ключей хранится в памяти, при перезапуске приложения происходит следующее:

* Все токены аутентификации, использующие файлы cookie, становятся недействительными.
* При выполнении следующего запроса пользователю требуется выполнить вход снова.
* Все данные, защищенные с помощью набора ключей, больше не могут быть расшифрованы. Это могут быть [токены CSRF](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) и [файлы cookie временных данных ASP.NET Core MVC](xref:fundamentals/app-state#tempdata).

Сведения о настройке защиты данных для хранения и шифрования набора ключей см. в приведенных ниже статьях.

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>

## <a name="secure-the-app"></a>Защита приложения

### <a name="configure-firewall"></a>Настройка брандмауэра

*Firewalld* — это динамическая управляющая программа брандмауэра, которая поддерживает зоны сети. Фильтрацию портов и пакетов можно по-прежнему осуществлять через iptables. *Firewalld* обычно устанавливается в системе по умолчанию. `yum` позволяет установить этот пакет или убедиться, что он установлен.

```bash
sudo yum install firewalld -y
```

С помощью `firewalld` вы можете открыть только те порты, которые необходимые для работы приложения. В этом случае используются порты 80 и 443. Следующие команды назначают порты 80 и 443 постоянно открытыми.

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

Обновите параметры брандмауэра. Проверьте, что доступные службы и порты находятся в зоне по умолчанию. Эти параметры можно просмотреть с помощью `firewall-cmd -h`.

```bash
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

```bash
public (default, active)
interfaces: eth0
sources: 
services: dhcpv6-client
ports: 443/tcp 80/tcp
masquerade: no
forward-ports: 
icmp-blocks: 
rich rules: 
```

### <a name="https-configuration"></a>Конфигурация HTTPS

Apache для HTTPS настраивается с помощью модуля *mod_ssl*. При установке модуля *httpd* автоматически добавляется и модуль *mod_ssl*. Если он по каким-то причинам отсутствует, добавьте его в систему с помощью `yum`.

```bash
sudo yum install mod_ssl
```

Чтобы принудительно использовать HTTPS, установите модуль `mod_rewrite` для перезаписи URL-адресов:

```bash
sudo yum install mod_rewrite
```

Измените файл *helloapp.conf*, чтобы разрешить перезапись URL-адресов и безопасный обмен данными через порт 443:

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/helloapp-error.log
    CustomLog /var/log/httpd/helloapp-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

> [!NOTE]
> В этом примере используется локально созданный сертификат. В **SSLCertificateFile** должен быть указан основной файл сертификата для доменного имени. В **SSLCertificateKeyFile** должен быть указан файл ключа, сформированный при создании CSR. В **SSLCertificateChainFile** должен быть указан файл промежуточного сертификата (если он существует), предоставленный центром сертификации.

Сохраните файл и протестируйте конфигурацию.

```bash
sudo service httpd configtest
```

Перезапустите Apache.

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a>Дополнительные предложения Apache

### <a name="additional-headers"></a>Дополнительные заголовки

Для защиты от вредоносных атак следует изменить или добавить несколько заголовков. Убедитесь, что модуль `mod_headers` установлен.

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a>Защита Apache от атак кликджекинга

[Кликджекинг](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger) (или *атака с подменой пользовательского интерфейса*) является вредоносной атакой, при которой посетителя сайта обманным путем вынуждают щелкнуть ссылку или нажать кнопку не той страницы, на которой он находится. Используйте `X-FRAME-OPTIONS` для защиты сайта.

Чтобы уменьшить риск атак кликджекинга, выполните указанные ниже действия.

1. Измените файл *httpd.conf*.

   ```bash
   sudo nano /etc/httpd/conf/httpd.conf
   ```

   Добавьте строку `Header append X-FRAME-OPTIONS "SAMEORIGIN"`.
1. Сохраните файл.
1. Перезапустите Apache.

#### <a name="mime-type-sniffing"></a>Сканирование типа MIME

Заголовок `X-Content-Type-Options` защищает Internet Explorer от *сканирования MIME* (определения `Content-Type` для файла по его содержимому). Если сервер задает заголовок `Content-Type` со значением `text/html`, и при этом установлен параметр `nosniff`, Internet Explorer отображает содержимое как `text/html` независимо от содержимого файла.

Измените файл *httpd.conf*.

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

Добавьте строку `Header set X-Content-Type-Options "nosniff"`. Сохраните файл. Перезапустите Apache.

### <a name="load-balancing"></a>Балансировка нагрузки

В этом примере показано, как установить и настроить Apache в CentOS 7 и Kestrel на том же компьютере. Чтобы устранить единую точку отказа, воспользуйтесь *mod_proxy_balancer* и измените значение **VirtualHost** для управления несколькими экземплярами веб-приложений за прокси-сервером Apache.

```bash
sudo yum install mod_proxy_balancer
```

В представленном ниже файле конфигурации настроен дополнительный экземпляр `helloapp`, работающий на порте 5001. В разделе *Proxy* настраивается конфигурация подсистемы балансировки нагрузки с двумя членами для распределения нагрузки методом *byrequests*.

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPass / balancer://mycluster/ 

    ProxyPassReverse / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5001/

    <Proxy balancer://mycluster>
        BalancerMember http://127.0.0.1:5000
        BalancerMember http://127.0.0.1:5001 
        ProxySet lbmethod=byrequests
    </Proxy>

    <Location />
        SetHandler balancer
    </Location>
    ErrorLog /var/log/httpd/helloapp-error.log
    CustomLog /var/log/httpd/helloapp-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

### <a name="rate-limits"></a>Ограничения скорости

С помощью элемента *mod_ratelimit*, который входит в модуль *httpd*, можно ограничить пропускную способность для клиентов:

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```

В примере файла пропускная способность составляет 600 Кбит/с в корневой папке.

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```

### <a name="long-request-header-fields"></a>Длинные поля заголовка запроса

Если приложение требует поля заголовка запроса длиннее, чем разрешено параметром по умолчанию прокси-сервера (обычно 8190 байт). измените значение директивы [LimitRequestFieldSize](https://httpd.apache.org/docs/2.4/mod/core.html#LimitRequestFieldSize). Применяемое значение зависит от условий. Дополнительные сведения см. в документации сервера.

> [!WARNING]
> Не увеличивайте значение `LimitRequestFieldSize` по умолчанию, если это не требуется. Увеличение значения повышает риск переполнения буфера и атак типа "отказ в обслуживании" (DoS) со стороны злоумышленников.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Необходимые компоненты для .NET Core в Linux](/dotnet/core/linux-prerequisites)
* <xref:test/troubleshoot>
* <xref:host-and-deploy/proxy-load-balancer>
