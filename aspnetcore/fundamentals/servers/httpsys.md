---
title: Реализация веб-сервера HTTP.sys в ASP.NET Core
author: guardrex
description: Общие сведения о веб-сервере HTTP.sys для ASP.NET Core в Windows. Веб-сервер HTTP.sys на основе работающего в режиме ядра драйвера Http.Sys — это альтернатива Kestrel, которую можно использовать для прямого подключения к Интернету без служб IIS.
monikerRange: '>= aspnetcore-2.0'
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/21/2019
uid: fundamentals/servers/httpsys
ms.openlocfilehash: abb426b1a41226e52d9b9b5c00c41ff816890d36
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038071"
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a>Реализация веб-сервера HTTP.sys в ASP.NET Core

Авторы: [Том Дикстра](https://github.com/tdykstra) (Tom Dykstra), [Крис Росс](https://github.com/Tratcher) (Chris Ross) и [Люк Латам](https://github.com/guardrex) (Luke Latham)

[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys) — это [веб-сервер для ASP.NET Core](xref:fundamentals/servers/index), который запускается только в Windows. HTTP.sys является альтернативой серверу [Kestrel](xref:fundamentals/servers/kestrel), предлагая некоторые функции, отсутствующие в Kestrel.

> [!IMPORTANT]
> HTTP.sys не подходит для использования с IIS или IIS Express из-за несовместимости с [модулем ASP.NET Core](xref:host-and-deploy/aspnet-core-module).

HTTP.sys поддерживает следующие функции:

* [Аутентификация Windows](xref:security/authentication/windowsauth)
* Совместное использование портов
* Использование HTTPS с SNI
* Использование HTTP/2 через TLS (Windows 10 и более поздние версии)
* Прямая передача файлов
* Кэширование откликов
* Использование WebSockets (Windows 8 и более поздние версии)

Поддерживаемые версии Windows:

* Windows 7 и более поздние версии
* Windows Server 2008 R2 и более поздние версии

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="when-to-use-httpsys"></a>Условия для применения HTTP.sys

HTTP.sys удобно использовать с развертываниями в таких случаях:

* когда нужно подключить сервер к Интернету напрямую без использования служб IIS;

  ![HTTP.sys взаимодействует с Интернетом напрямую](httpsys/_static/httpsys-to-internet.png)

* когда для внутренних развертываний нужна функция, отсутствующая в Kestrel, например [аутентификация Windows](xref:security/authentication/windowsauth).

  ![HTTP.sys взаимодействует с внутренней сетью напрямую](httpsys/_static/httpsys-to-internal.png)

HTTP.sys — это проверенная технология, которая защищает от многих типов атак, а также обеспечивает надежность, безопасность и масштабируемость полнофункционального веб-сервера. Сами службы IIS выполняются в качестве HTTP-прослушивателя поверх HTTP.sys.

## <a name="http2-support"></a>Поддержка HTTP/2

Протокол [HTTP/2](https://httpwg.org/specs/rfc7540.html) включен для приложений ASP.NET Core, если выполнены следующие базовые требования:

* установлена ОС Windows Server 2016 либо Windows 10 или более поздних версий;
* установлено подключение с поддержкой [согласования протокола уровня приложений (ALPN)](https://tools.ietf.org/html/rfc7301#section-3);
* установлено подключение TLS 1.2 или более поздней версии.

::: moniker range=">= aspnetcore-2.2"

Если установлено подключение HTTP/2, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) возвращает `HTTP/2`.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Если установлено подключение HTTP/2, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) возвращает `HTTP/1.1`.

::: moniker-end

Протокол HTTP/2 включен по умолчанию. Если не удается установить подключение HTTP/2, применяется резервный вариант HTTP/1.1. В будущих версиях Windows будут доступны флаги конфигурации HTTP/2, в том числе возможность отключения HTTP/2 с использованием HTTP.sys.

## <a name="kernel-mode-authentication-with-kerberos"></a>Проверка подлинности в режиме ядра с помощью Kerberos

HTTP.sys делегирует задачи в проверку подлинности в режиме ядра с помощью протокола проверки подлинности Kerberos. Проверка подлинности в режиме пользователя не поддерживается с Kerberos и HTTP.sys. Необходимо использовать учетную запись компьютера для расшифровки маркера/билета Kerberos, полученного из Active Directory и переадресованного клиентом на сервер для проверки подлинности пользователя. Зарегистрируйте имя субъекта-службы (SPN) для узла, а не пользователя приложения.

## <a name="how-to-use-httpsys"></a>Способы применения HTTP.sys

### <a name="configure-the-aspnet-core-app-to-use-httpsys"></a>Настройка приложения ASP.NET Core для использования HTTP.sys

1. Ссылка на пакет в файле проекта не требуется при использовании [метапакета Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) ([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)) (ASP.NET Core 2.1 или более поздней версии). Если метапакет `Microsoft.AspNetCore.App` не используется, добавьте ссылку на пакет в файл [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/).

2. Вызовите метод расширения <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderHttpSysExtensions.UseHttpSys*> при создании веб-узла, указав все необходимые параметры <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions>:

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=4-12)]

   Дополнительная настройка HTTP.sys выполняется с помощью [параметров реестра](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows).

   **Параметры HTTP.sys**

   | Свойство | Описание | Значение по умолчанию |
   | -------- | ----------- | :-----: |
   | [AllowSynchronousIO](xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.AllowSynchronousIO) | Указывает, разрешен ли синхронные операции ввода-вывода для `HttpContext.Request.Body` и `HttpContext.Response.Body`. | `true` |
   | [Authentication.AllowAnonymous](xref:Microsoft.AspNetCore.Server.HttpSys.AuthenticationManager.AllowAnonymous) | Разрешает анонимные запросы. | `true` |
   | [Authentication.Schemes](xref:Microsoft.AspNetCore.Server.HttpSys.AuthenticationManager.Schemes) | Указывает разрешенные схемы аутентификации. Может быть изменен в любое время до удаления прослушивателя. Предоставляет значения, полученные при [перечислении AuthenticationSchemes](xref:Microsoft.AspNetCore.Server.HttpSys.AuthenticationSchemes): `Basic`, `Kerberos`, `Negotiate`, `None` и `NTLM`. | `None` |
   | [EnableResponseCaching](xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.EnableResponseCaching) | Выполняет попытку кэшировать [режим ядра](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) для ответов с допустимыми заголовками. Ответ не может включать заголовки `Set-Cookie`, `Vary` или `Pragma`. Он должен включать заголовок `Cache-Control` со значением `public`, а также значение `shared-max-age` или `max-age` заголовок `Expires`. | `true` |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxAccepts> | Максимальное число одновременных попыток. | 5 &times; [Environment.<br>ProcessorCount](xref:System.Environment.ProcessorCount) |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxConnections> | Максимальное число попыток установить одновременное подключение. Использует `-1` для бесконечных циклов. Использует `null` для работы с параметром реестра на уровне компьютера. | `null`<br>Без ограничений. |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxRequestBodySize> | См. раздел <a href="#maxrequestbodysize">MaxRequestBodySize</a>. | 30 000 000 байт.<br>(~28,6 МБ). |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.RequestQueueLimit> | Максимально допустимое число запросов в очереди. | 1000. |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.ThrowWriteExceptions> | Указывает, следует ли вызывать исключение или завершать работу нормально, когда запись текста ответа завершается ошибкой из-за отключения клиента. | `false`<br>Нормальное завершение. |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.Timeouts> | Предоставляет конфигурацию <xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager> HTTP.sys, которую также можно настроить в реестре. Дополнительные сведения о каждом параметре, включая значения по умолчанию, см. здесь:<ul><li>[TimeoutManager.DrainEntityBody](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.DrainEntityBody) &ndash; время, выделенное для API сервера HTTP для очистки текста сущности при активном подключении.</li><li>[TimeoutManager.EntityBody](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.EntityBody) &ndash; время, выделенное на получение текста сущности запроса.</li><li>[TimeoutManager.HeaderWait](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.HeaderWait) &ndash; время, выделенное для API сервера HTTP для выполнения синтаксического анализа заголовка запроса.</li><li>[TimeoutManager.IdleConnection](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.IdleConnection) &ndash; время, выделенное для неактивного подключения.</li><li>[TimeoutManager.MinSendBytesPerSecond](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.MinSendBytesPerSecond) &ndash; минимальная скорость отправки ответа.</li><li>[TimeoutManager.RequestQueue](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.RequestQueue) &ndash; время, выделенное для пребывания запроса в очереди до его получения приложением.</li></ul> |  |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.UrlPrefixes> | Указывает <xref:Microsoft.AspNetCore.Server.HttpSys.UrlPrefixCollection> для регистрации с использованием HTTP.sys. Удобнее всего использовать параметр [UrlPrefixCollection.Add](xref:Microsoft.AspNetCore.Server.HttpSys.UrlPrefixCollection.Add*), который добавляет префикс к коллекции. Могут быть изменены в любое время до удаления прослушивателя. |  |

   <a name="maxrequestbodysize"></a>

   **MaxRequestBodySize**

   Максимально допустимый размер текста запроса в байтах. Если задано значение `null`, размер максимального запроса не ограничен. Это ограничение не оказывает влияния на обновленные подключения, которые не имеют ограничений.

   Чтобы переопределить это ограничение в приложении ASP.NET Core MVC для `IActionResult`, рекомендуется использовать атрибут <xref:Microsoft.AspNetCore.Mvc.RequestSizeLimitAttribute> в методе действия:

   ```csharp
   [RequestSizeLimit(100000000)]
   public IActionResult MyActionMethod()
   ```

   При попытке приложения настроить ограничение для запроса после того, как приложение начало считывать запрос, возникает исключение. Свойство `IsReadOnly` указывает на то, что свойство `MaxRequestBodySize` находится в состоянии только для чтения и настраивать ограничение слишком поздно.

   Если приложение должно переопределять <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxRequestBodySize> по запросу, используйте <xref:Microsoft.AspNetCore.Http.Features.IHttpMaxRequestBodySizeFeature>:

   [!code-csharp[](httpsys/sample/Startup.cs?name=snippet1&highlight=6-7)]

3. При использовании Visual Studio убедитесь, что приложение не настроено для запуска IIS или IIS Express.

   В Visual Studio профиль запуска по умолчанию использует IIS Express. Чтобы запустить проект как консольное приложение, измените выбранный профиль вручную, как показано на следующем снимке экрана.

   ![Выбор профиля консольного приложения](httpsys/_static/vs-choose-profile.png)

### <a name="configure-windows-server"></a>Настройка Windows Server

1. Определите, какие порты нужно открыть для приложения, и используйте [брандмауэр Windows](/windows/security/threat-protection/windows-firewall/create-an-inbound-port-rule) или командлет PowerShell [New-NetFirewallRule](/powershell/module/netsecurity/new-netfirewallrule), чтобы открыть порты брандмауэра для доступа трафика к HTTP.sys. В следующих командах и конфигурации приложения используется порт 443.

1. При развертывании на виртуальных машинах Azure откройте эти порты в [группе безопасности сети](/azure/virtual-machines/windows/nsg-quickstart-portal). В следующих командах и конфигурации приложения используется порт 443.

1. При необходимости получите и установите сертификаты X.509.

   В Windows создайте самозаверяющие сертификаты с помощью [командлета PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate). Примеры, которые не поддерживаются, см. в разделе [UpdateIISExpressSSLForChrome.ps1](https://github.com/aspnet/Docs/tree/master/aspnetcore/includes/make-x509-cert/UpdateIISExpressSSLForChrome.ps1).

   Установите самозаверяющие или подписанные центром сертификации сертификаты в хранилище сервера, выбрав **Локальный компьютер** > **Личный**.

1. Если приложение является [развертыванием, не зависящим от платформы](/dotnet/core/deploying/#framework-dependent-deployments-fdd), установите NET Core или .NET Framework (или обе платформы, если это приложение .NET Core, предназначенное для .NET Framework).

   * **.NET Core** — если приложению требуется .NET Core, скачайте установщик **среды выполнения .NET Core** на странице [скачивания .NET Core](https://dotnet.microsoft.com/download) и запустите его. Не устанавливайте полный пакет SDK на сервере.
   * **.NET Framework** — если приложению требуется .NET Framework, см. [руководство по установке](/dotnet/framework/install/). Установите требуемую платформу .NET Framework. Установщик последней версии .NET Framework доступен на странице [скачивания .NET](https://dotnet.microsoft.com/download).

   Если приложение [развертывается автономно](/dotnet/core/deploying/#framework-dependent-deployments-scd), в его развертывание включена среда выполнения. Устанавливать .NET Framework на сервере не нужно.

1. Настройте URL-адреса и порты в приложении.

   По умолчанию платформа ASP.NET Core привязана к `http://localhost:5000`. Чтобы настроить префиксы URL-адресов и порты, используйте следующие параметры:

   * <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseUrls*>
   * Аргументы командной строки `urls`.
   * Переменная среды `ASPNETCORE_URLS`.
   * <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.UrlPrefixes>

   В следующем примере кода показано, как использовать <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.UrlPrefixes> с локальным IP-адресом сервера `10.0.0.4` через порт 443.

   [!code-csharp[](httpsys/sample_snapshot/Program.cs?name=snippet1&highlight=11)]

   Преимущество `UrlPrefixes` заключается в том, что при неправильном формате префиксов сразу же создается сообщение об ошибке.

   Этот параметр в `UrlPrefixes` переопределяет параметры `UseUrls`/`urls`/`ASPNETCORE_URLS`. Таким образом, преимущество переменных среды`UseUrls`, `urls`и `ASPNETCORE_URLS` заключается в возможности быстрого переключения между Kestrel и HTTP.sys. Дополнительные сведения см. в разделе <xref:fundamentals/host/web-host>.

   HTTP.sys использует [форматы строк UrlPrefix API сервера HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).

   > [!WARNING]
   > **Не используйте** привязки с подстановочными знаками (`http://*:80/` и `http://+:80`) на верхнем уровне. Они создают уязвимости и ставят под угрозу безопасность приложения. Сюда относятся и строгие, и нестрогие подстановочные знаки. Вместо подстановочных знаков используйте имена узлов или IP-адреса в явном виде. Привязки с подстановочными знаками на уровне дочерних доменов (например, `*.mysub.com`) не создают таких угроз безопасности, если вы полностью контролируете родительский домен (в отличие от варианта `*.com`, создающего уязвимость). Дополнительные сведения см. в стандарте [RFC 7230, раздел 5.4, Host](https://tools.ietf.org/html/rfc7230#section-5.4).

1. Предварительно зарегистрируйте префиксы URL-адресов на сервере.

   Встроенным средством для настройки сервера HTTP.sys является *netsh.exe*. С помощью*netsh.exe* можно зарезервировать префиксы URL-адресов и назначить сертификаты X.509. Для использования этого средства требуются права администратора.

   Используйте средство *netsh.exe* для регистрации URL-адреса приложения.

   ```console
   netsh http add urlacl url=<URL> user=<USER>
   ```

   * `<URL>` — полное имя URL-адреса. Не используйте привязки с подстановочными знаками. Используйте допустимое имя узла или локальный IP-адрес. *URL-адрес должен включать косую черту в конце.*
   * `<USER>` — определяет имя пользователя или группы пользователей.

   В следующем примере сервер имеет локальный IP-адрес `10.0.0.4`.

   ```console
   netsh http add urlacl url=https://10.0.0.4:443/ user=Users
   ```

   При регистрации URL-адреса средство возвращает ответ `URL reservation successfully added`.

   Чтобы удалить зарегистрированный URL-адрес, используйте команду `delete urlacl`.

   ```console
   netsh http delete urlacl url=<URL>
   ```

1. Зарегистрируйте сертификаты X.509 на сервере.

   Используйте средство *netsh.exe* для регистрации сертификатов приложения.

   ```console
   netsh http add sslcert ipport=<IP>:<PORT> certhash=<THUMBPRINT> appid="{<GUID>}"
   ```

   * `<IP>` — задает локальный IP-адрес для привязки. Не используйте привязки с подстановочными знаками. Используйте допустимый IP-адрес.
   * `<PORT>` — указывает порт для прокси-сервера.
   * `<THUMBPRINT>` — отпечаток сертификата X.509.
   * `<GUID>` — глобальный уникальный идентификатор приложения, задаваемый разработчиком в информационных целях.

   В справочных целях храните GUID в приложении в виде тега пакета.

   * В Visual Studio сделайте следующее:
     * Откройте свойства проекта приложения, щелкнув приложение правой кнопкой мыши в **обозревателе решений** и выбрав **Properties** (Свойства).
     * Перейдите на вкладку **Package** (Пакет).
     * Введите GUID, который вы указали в поле **Tags** (Теги).
   * Если Visual Studio не используется:
     * Откройте файл проекта приложения.
     * Добавьте свойство `<PackageTags>` в новую или существующую группу `<PropertyGroup>` с GUID, который вы создали.

       ```xml
       <PropertyGroup>
         <PackageTags>9412ee86-c21b-4eb8-bd89-f650fbf44931</PackageTags>
       </PropertyGroup>
       ```

   В следующем примере:

   * Локальный IP-адрес сервера — `10.0.0.4`.
   * Сетевой генератор случайных GUID задает значение `appid`.

   ```console
   netsh http add sslcert 
       ipport=10.0.0.4:443 
       certhash=b66ee04419d4ee37464ab8785ff02449980eae10 
       appid="{9412ee86-c21b-4eb8-bd89-f650fbf44931}"
   ```

   При регистрации сертификата средство возвращает ответ `SSL Certificate successfully added`.

   Чтобы удалить регистрацию сертификата, используйте команду `delete sslcert`.

   ```console
   netsh http delete sslcert ipport=<IP>:<PORT>
   ```

   Дополнительные сведения см. в справочной документации по *netsh.exe*:

   * [Команды netsh для протокола HTTP](https://technet.microsoft.com/library/cc725882.aspx)
   * [Строки UrlPrefix](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

1. Запустите приложение.

   Если выполнена привязка к localhost через HTTP (не HTTPS) с номером порта больше 1024, для запуска приложения права администратора не требуются. При других конфигурациях (например, при использовании локального IP-адреса или привязки к порту 443) для запуска приложения требуются права администратора.

   Приложение отвечает по общедоступному IP-адресу сервера. В этом примере подключение к серверу происходит через Интернет по общедоступному IP-адресу `104.214.79.47` сервера.

   В этом примере используется сертификат разработки. После обхода предупреждения о ненадежном сертификате браузера происходит безопасная загрузка страницы.

   ![Окно браузера с отображаемой страницей индекса приложения](httpsys/_static/browser.png)

## <a name="proxy-server-and-load-balancer-scenarios"></a>Сценарии использования прокси-сервера и подсистемы балансировки нагрузки

Для приложений, размещенных с помощью файла HTTP.sys, которые взаимодействуют с запросами из Интернета или корпоративной сети, может потребоваться дополнительная настройка при размещении за прокси-серверами и подсистемами балансировки нагрузки. Дополнительные сведения см. в разделе [Настройка ASP.NET Core для работы с прокси-серверами и подсистемами балансировки нагрузки](xref:host-and-deploy/proxy-load-balancer).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Включить проверку подлинности Windows с использованием HTTP.sys](xref:security/authentication/windowsauth#enable-windows-authentication-with-httpsys)
* [API сервера HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)
* [Репозиторий GitHub ASPNET/HttpSysServer (исходный код)](https://github.com/aspnet/HttpSysServer/)
* [Узел](xref:fundamentals/index#host)
* <xref:test/troubleshoot>
