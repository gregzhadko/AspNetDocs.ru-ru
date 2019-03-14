---
title: Размещение ASP.NET Core в Windows со службами IIS
author: guardrex
description: Сведения о размещении приложений ASP.NET Core в службах Windows Server Internet Information Services (IIS).
ms.author: riande
ms.custom: mvc
ms.date: 02/19/2019
uid: host-and-deploy/iis/index
---
# <a name="host-aspnet-core-on-windows-with-iis"></a>Размещение ASP.NET Core в Windows со службами IIS

Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)

[Установка пакета размещения .NET Core](#install-the-net-core-hosting-bundle)

## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы

Поддерживаются следующие операционные системы:

* Windows 7 и более поздние версии
* Windows Server 2008 R2 и более поздние версии

[Сервер HTTP.sys](xref:fundamentals/servers/httpsys) (ранее назывался WebListener) не работает в конфигурации обратного прокси-сервера со службами IIS. Используйте [сервер Kestrel](xref:fundamentals/servers/kestrel).

Сведения о размещении в Azure см. в статье <xref:host-and-deploy/azure-apps/index>.

## <a name="supported-platforms"></a>Поддерживаемые платформы

Поддерживаются приложения, опубликованные для развертывания в 32-разрядных (x86) и 64-разрядный (x64) системах. Разверните 32-разрядную версию приложения, кроме следующих случаев:

* Приложению требуется более широкое адресное пространство виртуальной памяти, доступное в 64-разрядной версии приложения.
* Приложению требуется стек IIS большего размера.
* В коде присутствуют зависимости 64-разрядной версии.

## <a name="application-configuration"></a>Настройка приложения

### <a name="enable-the-iisintegration-components"></a>Включение компонентов IISIntegration

::: moniker range=">= aspnetcore-2.1"

Обычно *Program.cs* вызывает <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>, чтобы начать настройку узла:

```csharp
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

Обычно *Program.cs* вызывает <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>, чтобы начать настройку узла:

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

**Модель внутрипроцессного размещения**

`CreateDefaultBuilder` вызывает метод `UseIIS` для загрузки [CoreCLR](/dotnet/standard/glossary#coreclr) и размещения приложения внутри рабочего процесса IIS (*w3wp.exe* или *iisexpress.exe*). Тесты производительности показывают, что размещение приложения .NET Core внутри процесса позволяет обрабатывать значительно больше запросов, чем при размещении приложения вне процесса с перенаправлением запросов к серверу [Kestrel](xref:fundamentals/servers/kestrel).

Модель внутрипроцессного размещения не поддерживается для приложений ASP.NET Core, предназначенных для .NET Framework.

**Модель размещения вне процесса**

Для внепроцессного размещения в IIS метод `CreateDefaultBuilder` настраивает сервер [Kestrel](xref:fundamentals/servers/kestrel) в качестве веб-сервера и активирует интеграцию с IIS, задавая базовый путь и порт для [модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module).

Модуль ASP.NET Core создает динамический порт для назначения серверному процессу. `CreateDefaultBuilder` вызывает метод <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>. `UseIISIntegration` настраивает Kestrel для прослушивания динамического порта по IP-адресу localhost (`127.0.0.1`). Если динамический порт — 1234, Kestrel прослушивает `127.0.0.1:1234`. Эта конфигурация заменяет другие конфигурации URL-адресов, предоставляемые:

* `UseUrls`
* [API прослушивания Kestrel](xref:fundamentals/servers/kestrel#endpoint-configuration);
* [Конфигурацией](xref:fundamentals/configuration/index) (или [параметром командной строки--urls](xref:fundamentals/host/web-host#override-configuration)).

Вызовы `UseUrls` или API `Listen` Kestrel при работе с этим модулем не требуются. При вызове `UseUrls` или `Listen` Kestrel ожидает передачи данных на порты, указанные только при выполнении приложения без IIS.

Дополнительные сведения о моделях внутри- и внепроцессного размещения см. в разделах [Модуль ASP.NET Core](xref:host-and-deploy/aspnet-core-module) и [Справочник по конфигурации модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module).

::: moniker-end

::: moniker range="= aspnetcore-2.1"

`CreateDefaultBuilder` настраивает сервер [Kestrel](xref:fundamentals/servers/kestrel) в качестве веб-сервера и активирует интеграцию IIS, задавая базовый путь и порт для [модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module).

Модуль ASP.NET Core создает динамический порт для назначения серверному процессу. `CreateDefaultBuilder` вызывает метод <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>. `UseIISIntegration` настраивает Kestrel для прослушивания динамического порта по IP-адресу localhost (`127.0.0.1`). Если динамический порт — 1234, Kestrel прослушивает `127.0.0.1:1234`. Эта конфигурация заменяет другие конфигурации URL-адресов, предоставляемые:

* `UseUrls`
* [API прослушивания Kestrel](xref:fundamentals/servers/kestrel#endpoint-configuration);
* [Конфигурацией](xref:fundamentals/configuration/index) (или [параметром командной строки--urls](xref:fundamentals/host/web-host#override-configuration)).

Вызовы `UseUrls` или API `Listen` Kestrel при работе с этим модулем не требуются. При вызове `UseUrls` или `Listen` Kestrel ожидает передачи данных на порт, указанный только при выполнении приложения без IIS.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

`CreateDefaultBuilder` настраивает сервер [Kestrel](xref:fundamentals/servers/kestrel) в качестве веб-сервера и активирует интеграцию IIS, задавая базовый путь и порт для [модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module).

Модуль ASP.NET Core создает динамический порт для назначения серверному процессу. `CreateDefaultBuilder` вызывает метод <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>. `UseIISIntegration` настраивает Kestrel для прослушивания динамического порта по IP-адресу localhost (`localhost`). Если динамический порт — 1234, Kestrel прослушивает `localhost:1234`. Эта конфигурация заменяет другие конфигурации URL-адресов, предоставляемые:

* `UseUrls`
* [API прослушивания Kestrel](xref:fundamentals/servers/kestrel#endpoint-configuration);
* [Конфигурацией](xref:fundamentals/configuration/index) (или [параметром командной строки--urls](xref:fundamentals/host/web-host#override-configuration)).

Вызовы `UseUrls` или API `Listen` Kestrel при работе с этим модулем не требуются. При вызове `UseUrls` или `Listen` Kestrel ожидает передачи данных на порт, указанный только при выполнении приложения без IIS.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Включите в зависимости приложения зависимость от пакета [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/). Используйте ПО промежуточного слоя для интеграции IIS, добавив метод расширения <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> в <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>:

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*> и <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> являются обязательными элементами. Код, вызывающий `UseIISIntegration`, не влияет на переносимость кода. Если приложение запускается не в IIS (например, запускается непосредственно в Kestrel), `UseIISIntegration` не работает.

Модуль ASP.NET Core создает динамический порт для назначения серверному процессу. `UseIISIntegration` настраивает Kestrel для прослушивания динамического порта по IP-адресу localhost (`localhost`). Если динамический порт — 1234, Kestrel прослушивает `localhost:1234`. Эта конфигурация заменяет другие конфигурации URL-адресов, предоставляемые:

* `UseUrls`
* [Конфигурацией](xref:fundamentals/configuration/index) (или [параметром командной строки--urls](xref:fundamentals/host/web-host#override-configuration)).

При использовании этого модуля вызов `UseUrls` не требуется. При вызове `UseUrls` Kestrel ожидает передачи данных на порт, указанный только при выполнении приложения без IIS.

При вызове `UseUrls` в приложении ASP.NET Core 1.0 следует выполнять вызов **до** вызова `UseIISIntegration`, чтобы исключить перезапись порта, настроенного в модуле. В ASP.NET Core 1.1 соблюдать этот порядок вызовов не требуется, так как параметр модуля переопределяет `UseUrls`.

::: moniker-end

Дополнительные сведения о размещении см. в разделе [Размещение в ASP.NET Core](xref:fundamentals/index#host).

### <a name="iis-options"></a>Параметры служб IIS

::: moniker range=">= aspnetcore-2.2"

**Модель внутрипроцессного размещения**

Чтобы настроить параметры сервера IIS, включите конфигурацию служб для <xref:Microsoft.AspNetCore.Builder.IISServerOptions> в <xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*>. В следующем примере показано, как отключить AutomaticAuthentication:

```csharp
services.Configure<IISServerOptions>(options => 
{
    options.AutomaticAuthentication = false;
});
```

| Параметр                         | Значение по умолчанию | Параметр |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | Если значение — `true`, сервер IIS задает свойство `HttpContext.User`, использующее [проверку подлинности Windows](xref:security/authentication/windowsauth). Если значение — `false`, сервер только предоставляет идентификатор для `HttpContext.User` и отвечает на явные запросы защиты от `AuthenticationScheme`. Для работы `AutomaticAuthentication` необходимо включить в службах IIS проверку подлинности Windows. Дополнительные сведения: [Проверка подлинности Windows](xref:security/authentication/windowsauth). |
| `AuthenticationDisplayName`    | `null`  | Задает отображаемое имя для пользователей на страницах входа. |

**Модель размещения вне процесса**

::: moniker-end

Чтобы настроить параметры IIS, включите конфигурацию служб для <xref:Microsoft.AspNetCore.Builder.IISOptions> в <xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*>. В следующем примере приложению запрещается заполнение `HttpContext.Connection.ClientCertificate`:

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| Параметр                         | Значение по умолчанию | Параметр |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | Если значение — `true`, ПО промежуточного слоя для интеграции IIS задает свойство `HttpContext.User`, которое прошло [проверку подлинности Windows](xref:security/authentication/windowsauth). Если значение — `false`, ПО промежуточного слоя только предоставляет идентификатор для `HttpContext.User` и отвечает на явные запросы защиты от `AuthenticationScheme`. Для работы `AutomaticAuthentication` необходимо включить в службах IIS проверку подлинности Windows. Дополнительные сведения см. в статье о [проверке подлинности Windows](xref:security/authentication/windowsauth). |
| `AuthenticationDisplayName`    | `null`  | Задает отображаемое имя для пользователей на страницах входа. |
| `ForwardClientCertificate`     | `true`  | Если значение — `true` и если присутствует заголовок запроса `MS-ASPNETCORE-CLIENTCERT`, происходит заполнение `HttpContext.Connection.ClientCertificate`. |

### <a name="proxy-server-and-load-balancer-scenarios"></a>Сценарии использования прокси-сервера и подсистемы балансировки нагрузки

ПО промежуточного слоя для интеграции IIS, которое настраивает ПО промежуточного слоя переадресации заголовков, и модуль ASP.NET Core настраиваются на пересылку схемы (HTTP/HTTPS) и удаленного IP-адреса расположения, где был сформирован запрос. Для приложений, размещенных за дополнительными прокси-серверами и подсистемами балансировки нагрузки, может потребоваться дополнительная настройка. Дополнительные сведения см. в разделе [Настройка ASP.NET Core для работы с прокси-серверами и подсистемами балансировки нагрузки](xref:host-and-deploy/proxy-load-balancer).

### <a name="webconfig-file"></a>Файл web.config

В файле *web.config* содержится конфигурация [модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module). Создание, преобразование и публикация файла *web.config* обрабатываются целевым объектом MSBuild (`_TransformWebConfig`) при публикации проекта. Этот целевой объект присутствует в целевых веб-пакетах SDK (`Microsoft.NET.Sdk.Web`). Пакет SDK задается в начале файла проекта:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

Если в проекте нет файла *web.config*, он создается с соответствующими аргументами *processPath* и *arguments* для настройки [модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module) и переносится в [опубликованные выходные данные](xref:host-and-deploy/directory-structure).

Если в проекте есть файл *web.config*, он преобразуется с соответствующими аргументами *processPath* и *arguments* для настройки модуля ASP.NET Core и переносится в опубликованные выходные данные. Преобразование не изменяет параметры конфигурации служб IIS, включенные в файл.

Файл *web.config* может содержать дополнительные параметры конфигурации IIS, управляющие активными модулями IIS. Сведения о модулях IIS, которые могут обрабатывать запросы к приложениям ASP.NET Core, см. в статье [Модули IIS](xref:host-and-deploy/iis/modules).

Чтобы пакет SDK не преобразовывал файл *web.config*, добавьте в файл проекта свойство **\<IsTransformWebConfigDisabled>**.

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

Если пакет SDK не преобразует файл, аргументы *processPath* и *arguments* нужно задать вручную. Дополнительные сведения см. в разделе [Справочник по конфигурации модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module).

### <a name="webconfig-file-location"></a>Расположение файла web.config

Для корректной настройки [модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module) необходимо наличие файла *web.config* в корневой папке контента развертываемого приложения (как правило, это основной путь приложения). Это расположение соответствует физическому пути веб-сайта, указанному в службах IIS. Файл *web.config* требуется в корне приложения, чтобы разрешить публикацию нескольких приложений с помощью веб-развертывания.

По физическому пути приложения находятся файлы с конфиденциальной информацией: *\<имя_сборки>.runtimeconfig.json*, *\<имя_сборки>.xml* (комментарии к XML-документации) и *\<имя_сборки>.deps.json*. Когда файл *web.config* присутствует и сайт запускается нормально, службы IIS не обрабатывают запросы к этим файлам. Если файл *web.config* отсутствует, неправильно именован или не может настроить нормальный запуск сайта, службы IIS могут свободно передавать содержимое этих конфиденциальных файлов.

**Файл *web.config* должен постоянно находиться в развертывании, у этого файла должно быть правильное имя, и файл должен быть в состоянии настроить нормальный запуск сайта. Никогда не удаляйте файл *web.config* из развертывания в рабочей среде.**

### <a name="transform-webconfig"></a>Преобразование web.config

Если вам нужно преобразовать *web.config* при публикации (например, задать переменные среды на основе конфигурации, профиля или среды), см. раздел <xref:host-and-deploy/iis/transform-webconfig>.

## <a name="iis-configuration"></a>Конфигурация IIS

**Операционные системы семейства Windows Server**

Включите роль сервера **Веб-сервер (IIS)** и настройте службы роли.

1. В меню **Управление** запустите мастер **Добавить роли и компоненты** или в окне **Диспетчер серверов** щелкните соответствующую ссылку. На этапе **Роли сервера** установите флажок **Веб-сервер (IIS)**.

   ![Роль "Веб-сервер (IIS)" выбрана на странице "Выбор ролей сервера".](index/_static/server-roles-ws2016.png)

1. После этапа выбора **компонентов** запускается этап выбора **служб роли** для веб-сервера (IIS). Выберите нужные службы роли IIS или оставьте службы по умолчанию.

   ![Службы роли по умолчанию, выбранные на странице "Выбор служб ролей".](index/_static/role-services-ws2016.png)

   **Проверка подлинности Windows (необязательный компонент)**  
   Чтобы включить проверку подлинности Windows, разверните такие узлы: **Веб-сервер** > **Безопасность**. Выберите компонент **Проверка подлинности Windows**. Дополнительные сведения см. в статьях [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) (Проверка подлинности Windows <windowsAuthentication>) и [Configure Windows authentication in an ASP.NET Core app](xref:security/authentication/windowsauth) (Настройка проверки подлинности Windows в приложении ASP.NET Core).

   **Протокол WebSocket (необязательный компонент)**  
   Протокол WebSocket поддерживается в ASP.NET Core начиная с версии 1.1. Чтобы включить протокол WebSocket, разверните такие узлы: **Веб-сервер** > **Разработка приложений**. Выберите компонент **Протокол WebSocket**. Дополнительные сведения см. в разделе [Протокол WebSocket](xref:fundamentals/websockets).

1. Пройдите этап **Подтверждение**, чтобы установить роль и службы веб-сервера. После установки роли **Веб-сервер (IIS)** перезагружать сервер или службы IIS не требуется.

**Операционные системы Windows для настольных компьютеров**

Включите компоненты **Консоль управления IIS** и **Службы Интернета**.

1. Последовательно выберите **Панель управления** > **Программы** > **Программы и компоненты** > **Включение или отключение компонентов Windows** (в левой части экрана).

1. Разверните узел **Службы IIS**. Разверните узел **Средства управления веб-сайтом**.

1. Установите флажок **Консоль управления IIS**.

1. Установите флажок **Службы Интернета**.

1. В группе **Службы Интернета** оставьте компоненты по умолчанию или настройте компоненты IIS.

   **Проверка подлинности Windows (необязательный компонент)**  
   Чтобы включить проверку подлинности Windows, разверните такие узлы: **Службы Интернета** > **Безопасность**. Выберите компонент **Проверка подлинности Windows**. Дополнительные сведения см. в статьях [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) (Проверка подлинности Windows <windowsAuthentication>) и [Configure Windows authentication in an ASP.NET Core app](xref:security/authentication/windowsauth) (Настройка проверки подлинности Windows в приложении ASP.NET Core).

   **Протокол WebSocket (необязательный компонент)**  
   Протокол WebSocket поддерживается в ASP.NET Core начиная с версии 1.1. Чтобы включить протокол WebSocket, разверните такие узлы: **Службы Интернета** > **Компоненты разработки приложений**. Выберите компонент **Протокол WebSocket**. Дополнительные сведения см. в разделе [Протокол WebSocket](xref:fundamentals/websockets).

1. Если во время установки IIS потребуется перезагрузка, перезагрузите систему.

![Группы "Консоль управления IIS" и "Службы Интернета" выбраны в окне "Компоненты Windows".](index/_static/windows-features-win10.png)

## <a name="install-the-net-core-hosting-bundle"></a>Установка пакета размещения .NET Core

Установите *пакет размещения .NET Core* в размещающей системе. В составе пакета устанавливаются среда выполнения .NET Core, библиотека .NET Core и [модуль ASP.NET Core](xref:host-and-deploy/aspnet-core-module). Модуль позволяет запускать приложения ASP.NET Core под управлением IIS. Если система не подключена к Интернету, перед установкой пакета размещения .NET Core получите и установите [Распространяемый компонент Microsoft Visual C++ 2015](https://www.microsoft.com/download/details.aspx?id=53840).

> [!IMPORTANT]
> Если пакет размещения устанавливается до установки служб IIS, его нужно восстановить. После установки служб IIS запустите установщик пакета размещения еще раз.

### <a name="direct-download-current-version"></a>Прямая загрузка (текущая версия)

Скачайте установщик по следующей ссылке:

[Текущий установщик пакета размещения .NET Core (прямая загрузка)](https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer)

### <a name="earlier-versions-of-the-installer"></a>Более ранние версии установщика

Получение более ранней версии установщика:

1. Перейдите в [архивы загрузок .NET](https://www.microsoft.com/net/download/archives).
1. В разделе **.NET Core** выберите версию .NET Core.
1. В столбце **Запуск приложений — среда выполнения** найдите строку, содержащую нужную версию среды выполнения .NET Core.
1. Скачайте установщик по ссылке **Среда выполнения и пакет размещения**.

> [!WARNING]
> Некоторые установщики содержат версии выпусков, которые достигли конца своего жизненного цикла и больше не поддерживаются корпорацией Майкрософт. Дополнительные сведения см. в разделе [Политика поддержки](https://www.microsoft.com/net/download/dotnet-core/2.0).

### <a name="install-the-hosting-bundle"></a>Установка пакета размещения .NET Core

1. Запустите установщик на сервере. При запуске установщика из командной оболочки администратора доступны следующие параметры:

   * `OPT_NO_ANCM=1` — пропуск установки модуля ASP.NET Core;
   * `OPT_NO_RUNTIME=1` — пропуск установки среды выполнения .NET Core;
   * `OPT_NO_SHAREDFX=1` — пропуск установки общей платформы ASP.NET (среды выполнения ASP.NET);
   * `OPT_NO_X86=1` — пропуск установки 32-разрядных сред выполнения. Этот параметр следует использовать, если вы наверняка не будете размещать 32-разрядные приложения. Если есть хоть малейшая возможность, что в будущем придется размещать и 32-разрядные, и 64-разрядные приложения, не указывайте этот параметр и установите обе среды выполнения.
   * `OPT_NO_SHARED_CONFIG_CHECK=1` &ndash; — отключение проверки использования общей конфигурации IIS, если файл общей конфигурации (*applicationHost.config*) находится на том же компьютере, что и установка IIS. *Доступен только для пакетных установщиков размещения ASP.NET Core 2.2 или более поздней версии.* Дополнительные сведения см. в разделе <xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration>.
1. Перезагрузите систему или в командой оболочке выполните команду **net stop was /y**, а затем — команду **net start w3svc**. Перезапуск служб IIS позволит обнаружить внесенные установщиком изменения в системном пути, который является переменной среды.

Если установщик пакета размещения Windows обнаруживает, что для завершения установки требуется сброс IIS, установщик выполняет этот сброс. Если установщик применяет сброс IIS, перезапускаются все пулы приложений и веб-сайты IIS.

> [!NOTE]
> Сведения об общей конфигурации IIS см. в разделе [Модуль ASP.NET Core с общей конфигурацией IIS](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration).

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a>Установка веб-развертывания при публикации с помощью Visual Studio

При развертывании приложений на серверах с помощью [веб-развертывания](/iis/publish/using-web-deploy/introduction-to-web-deploy) установите на сервере последнюю версию веб-развертывания. Чтобы установить веб-развертывание, можно использовать [установщик веб-платформы (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) или получить установщик непосредственно в [Центре загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=43717). Предпочтительный метод — использовать WebPI. WebPI обеспечивает автономную установку и настройку поставщиков размещения.

## <a name="create-the-iis-site"></a>Создание сайта IIS

1. В размещающей системе создайте папку, в которой будут храниться файлы и папки опубликованного приложения. Макет развертывания приложения описан в статье [Directory structure of published ASP.NET Core apps](xref:host-and-deploy/directory-structure) (Структура каталогов опубликованных приложений ASP.NET Core).

1. В окне диспетчера IIS на панели **Подключения** разверните узел сервера. Щелкните правой кнопкой мыши папку **Сайты**. В контекстном меню выберите пункт **Добавить веб-сайт**.

1. Укажите имя в поле **Имя сайта** и задайте значение в поле **Физический путь** для созданной папки развертывания приложения. Укажите конфигурацию **привязки** и нажмите кнопку **ОК**, чтобы создать веб-сайт.

   ![В окне "Добавить веб-сайт" укажите имя сайта, физический путь и имя узла.](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > **Не используйте** привязки с подстановочными знаками (`http://*:80/` и `http://+:80`) на верхнем уровне. Это может создать уязвимость и поставить ваше приложение под угрозу. Сюда относятся и строгие, и нестрогие подстановочные знаки. Вместо этого используйте имена узлов в явном виде. Привязки с подстановочными знаками на уровне дочерних доменов (например `*.mysub.com`) не создают таких угроз безопасности, если вы полностью контролируете родительский домен (в отличие от варианта `*.com`, создающего уязвимость). Дополнительные сведения см. в документе [rfc7230, раздел 5.4](https://tools.ietf.org/html/rfc7230#section-5.4).

1. Разверните узел сервера и выберите **Пулы приложений**.

1. Щелкните правой кнопкой мыши пул приложений сайта и в контекстном меню выберите пункт **Основные параметры**.

1. В окне **Изменение пула приложений** задайте для параметра **Версия среды CLR .NET** значение **Без управляемого кода**.

   ![Выбор значения "Без управляемого кода" для параметра "Версия среды CLR .NET".](index/_static/edit-apppool-ws2016.png)

    ASP.NET Core выполняется в отдельном процессе и управляет средой выполнения. Для ASP.NET Core не требуется загрузка классической среды CLR. Задавать для параметра **Версия среды CLR .NET** значение **Без управляемого кода** необязательно.

1. *ASP.NET Core 2.2 или более поздней версии*: для 64-разрядного (x64) [автономного развертывания](/dotnet/core/deploying/#self-contained-deployments-scd), в котором используется [модель размещения в процессе](xref:fundamentals/servers/index#in-process-hosting-model), отключите пул приложений для 32-разрядных (x86) процессов.

   На боковой панели **Действия** в разделе **Пулы приложений** диспетчера IIS выберите **Задать значения по умолчанию для пула приложений** или **Дополнительные параметры**. Найдите пункт **Включить 32-разрядные приложения** и задайте значение `False`. Этот параметр не влияет на приложения, развернутые для [размещения вне процесса](xref:host-and-deploy/aspnet-core-module#out-of-process-hosting-model).

1. Убедитесь в том, что удостоверение модели процесса имеет соответствующие разрешения.

   При изменении удостоверения по умолчанию для пула приложений (**Модель процесса** > **Удостоверение**) с **ApplicationPoolIdentity** на другое, убедитесь, что у нового удостоверения есть соответствующие разрешения для доступа к папке приложения, базе данных и другим необходимым ресурсам. Например, пулу приложений требуются права на чтение и запись в папках, в которых приложение считывает и записывает файлы.

**Настройка проверки подлинности Windows (необязательный этап)**  
См. статью [Configure Windows authentication in an ASP.NET Core app](xref:security/authentication/windowsauth) (Настройка проверки подлинности Windows в приложении ASP.NET Core).

## <a name="deploy-the-app"></a>Развертывание приложения

Разверните приложение в папке, созданной в размещающей системе. Рекомендуемый механизм развертывания — [веб-развертывание](/iis/publish/using-web-deploy/introduction-to-web-deploy).

### <a name="web-deploy-with-visual-studio"></a>Веб-развертывание с помощью Visual Studio

Сведения о создании профиля публикации для веб-развертывания см. в статье [Профили публикации Visual Studio для развертывания приложений ASP.NET Core](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles). Если поставщик услуг размещения предоставляет профиль публикации или позволяет его создать, скачайте этот профиль и импортируйте его с помощью диалогового окна **Публикация** в Visual Studio.

![Диалоговое окно "Публикация"](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a>Веб-развертывание вне Visual Studio

[Веб-развертывание](/iis/publish/using-web-deploy/introduction-to-web-deploy) можно также использовать вне Visual Studio с помощью командной строки. Дополнительные сведения см. в статье [Средство веб-развертывания](/iis/publish/using-web-deploy/use-the-web-deployment-tool).

### <a name="alternatives-to-web-deploy"></a>Альтернативы веб-развертыванию

Переместить приложение в размещающую систему можно несколькими способами: с помощью копирования вручную, Xcopy, Robocopy или PowerShell.

Дополнительные сведения о развертывании ASP.NET Core в службах IIS см. в разделе [Ресурсы развертывания для администраторов IIS](#deployment-resources-for-iis-administrators).

## <a name="browse-the-website"></a>Обзор веб-сайта

![Начальная страница IIS, загруженная в браузере Microsoft Edge.](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a>Заблокированные файлы развертывания

Во время выполнения приложения файлы в папке развертывания блокируются. Заблокированные файлы невозможно перезаписать во время развертывания. Чтобы снять блокировку с файлов в развертывании, остановите пул приложений с помощью **одного** из следующих методов:

* Запустите веб-развертывание и добавьте ссылку на `Microsoft.NET.Sdk.Web` в файл проекта. Файл *app_offline.htm* помещается в корень каталога веб-приложения. Если файл присутствует, модуль ASP.NET Core корректно завершает работу приложения и обслуживает файл *app_offline.htm* во время развертывания. Дополнительные сведения см. в разделе [Справочник по конфигурации модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module#app_offlinehtm).
* Вручную остановите пул приложений в диспетчере служб IIS на сервере.
* С помощью PowerShell удалите *app_offline.html* (требуется PowerShell 5 или более поздняя версия):

  ```PowerShell
  $pathToApp = 'PATH_TO_APP'

  # Stop the AppPool
  New-Item -Path $pathToApp app_offline.htm

  # Provide script commands here to deploy the app

  # Restart the AppPool
  Remove-Item -Path $pathToApp app_offline.htm

  ```

## <a name="data-protection"></a>Защита данных

[Стек защиты данных ASP.NET Core](xref:security/data-protection/introduction) используют несколько [ПО промежуточного слоя](xref:fundamentals/middleware/index) ASP.NET Core, включая ПО, которое применяется для аутентификации. Даже если API-интерфейсы защиты данных не вызываются из пользовательского кода, защиту данных следует настроить для создания постоянного [хранилища криптографических ключей](xref:security/data-protection/implementation/key-management). Это можно сделать с помощью скрипта развертывания или в пользовательском коде. Если защита данных не настроена, ключи хранятся в памяти и удаляются при перезапуске приложения.

Если набор ключей хранится в памяти, при перезапуске приложения происходит следующее:

* Все токены аутентификации, использующие файлы cookie, становятся недействительными. 
* При выполнении следующего запроса пользователю требуется выполнить вход снова. 
* Все данные, защищенные с помощью набора ключей, больше не могут быть расшифрованы. Это могут быть [токены CSRF](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) и [файлы cookie временных данных ASP.NET Core MVC](xref:fundamentals/app-state#tempdata).

Чтобы настроить защиту данных в службах IIS для хранения набора ключей, воспользуйтесь **одним** из следующих методов:

* **Создание раздела реестра для защиты данных**.

  Ключи защиты данных, используемые приложениями ASP.NET Core, хранятся во внешнем для приложений реестре. Чтобы хранить эти ключи для определенного приложения, нужно создать разделы реестра для пула приложений.

  При автономной установке служб IIS, не поддерживающей веб-ферму, можно выполнить [скрипт PowerShell Provision-AutoGenKeys.ps1 для защиты данных](https://github.com/aspnet/AspNetCore/blob/master/src/DataProtection/Provision-AutoGenKeys.ps1) применительно к каждому пулу приложений, в который входит приложение ASP.NET Core. Этот скрипт создает раздел в реестре HKLM, который будет доступен только для учетной записи рабочего процесса пула приложений, к которому относится соответствующее приложение. Неактивные ключи шифруются с помощью API защиты данных с ключом компьютера.

  В случаях, когда используется веб-ферма, в приложении можно настроить UNC-путь, по которому это приложение будет хранить набор ключей для защиты данных. По умолчанию ключи защиты данных не шифруются. Разрешения на доступ к файлам в сетевой папке должны быть предоставлены только учетной записи Windows, с помощью которой выполняется приложение. Для защиты неактивных ключей можно использовать сертификат X509. Рассмотрите возможность реализации механизма, позволяющего пользователям отправлять сертификаты: поместите сертификаты в хранилище доверенных сертификатов пользователя и обеспечьте их доступность на всех компьютерах, где выполняется приложение. Дополнительные сведения см. в разделе [Настройка защиты данных в ASP.NET Core](xref:security/data-protection/configuration/overview).

* **Настройка пула приложений IIS для загрузки профиля пользователя**.

  Этот параметр находится на странице **Дополнительные параметры** пула приложений в разделе **Модель процесса**. Задайте для параметра **Загрузить профиль пользователя** значение `True`. Если задать значение `True`, ключи будут храниться в каталоге профиля пользователя и защищаться с помощью API защиты данных и ключа на уровне учетной записи пользователя. Ключи хранятся в папке *%LOCALAPPDATA%/ASP.NET/DataProtection-Keys*.

  Также необходимо включить атрибут [setProfileEnvironment](/iis/configuration/system.applicationhost/applicationpools/add/processmodel#configuration) пула приложений. Значением свойства `setProfileEnvironment` по умолчанию является `true`. В некоторых сценариях (например, в ОС Windows) для параметра `setProfileEnvironment` установлено значение `false`. Если ключи не хранятся в каталоге профиля пользователя:

  1. Перейдите к папке *%windir%/system32/inetsrv/config*.
  1. Откройте файл *applicationHost.config*.
  1. Найдите элемент `<system.applicationHost><applicationPools><applicationPoolDefaults><processModel>` .
  1. Убедитесь, что атрибут `setProfileEnvironment` отсутствует и установлено значение по умолчанию `true`, или же явно задайте для атрибута значение `true`.

* **Использование файловой системы в качестве хранилища набора ключей**.

  Измените код приложения так, чтобы [в качестве хранилища набора ключей использовалась файловая система](xref:security/data-protection/configuration/overview). Для защиты набора ключей используйте доверенный сертификат X509. Если сертификат — самозаверяющий, поместите его в доверенное корневое хранилище.

  При использовании служб IIS в веб-ферме:

  * используйте общую папку, которая доступна всем компьютерам;
  * разверните сертификат X509 на каждом компьютере; настройте [защиту данных в коде](xref:security/data-protection/configuration/overview).

* **Настройка политики защиты данных на уровне компьютера**.

  Система защиты данных обеспечивает ограниченную поддержку задания [политики по умолчанию на уровне компьютера](xref:security/data-protection/configuration/machine-wide-policy) для всех приложений, использующих интерфейсы API защиты данных. Дополнительные сведения см. в разделе <xref:security/data-protection/introduction>.

## <a name="virtual-directories"></a>Виртуальные каталоги

[Виртуальные каталоги IIS](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#virtual-directories) не поддерживаются в приложениях ASP.NET Core. Приложение может размещаться как [вложенное](#sub-applications).

## <a name="sub-applications"></a>Вложенные приложения

Приложение ASP.NET Core можно разместить как [вложенное приложение IIS](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#applications). Путь к вложенному приложению становится частью URL-адреса главного приложения.

::: moniker range="< aspnetcore-2.2"

Вложенное приложение не должно включать модуль ASP.NET Core в качестве обработчика. Если модуль добавляется в качестве обработчика в файл *web.config* дочернего приложения, при попытке работы с этим приложением выводится ошибка *500.19* (внутренняя ошибка сервера) с указанием некорректного файла конфигурации.

Вот пример опубликованного файла *web.config* для дочернего приложения ASP.NET Core:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

Размещая вложенное приложение не на основе ASP.NET Core в приложении ASP.NET Core, явным образом удалите унаследованный обработчик из файла *web.config* вложенного приложения.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

В ссылках на статический ресурс во вложенном приложении следует использовать нотацию `~/`. Такая нотация активирует [вспомогательную функцию тега](xref:mvc/views/tag-helpers/intro) для добавления свойства pathbase вложенного приложения в начало отображаемой относительной ссылки. Для вложенного приложения с путем `/subapp_path` ссылка на изображение `src="~/image.png"` отображается как `src="/subapp_path/image.png"`. ПО промежуточного слоя для обработки статических файлов в главном приложении не обрабатывает такой запрос статического файла. Запрос обрабатывается соответствующим ПО вложенного приложения.

Если атрибуту `src` статического ресурса присваивается абсолютный путь (например, `src="/image.png"`), ссылка отображается без свойства pathbase вложенного приложения. ПО промежуточного слоя для обработки статических файлов в главном приложении пытается найти ресурс в [корневом веб-каталоге](xref:fundamentals/index#web-root) главного приложения, что приводит к ошибке *404 — Not Found* (не найдено), кроме случаев, когда статический ресурс доступен из главного приложения.

Для размещения приложения ASP.NET Core в качестве приложения, вложенного в другое приложение ASP.NET Core, сделайте следующее:

1. Создайте пул приложений для вложенного приложения. Для параметра **Версия среды CLR .NET** выберите значение **Без управляемого кода**.

1. Добавьте корневой веб-сайт в диспетчере служб IIS с вложенным приложением в папке внутри корневого веб-сайта.

1. Щелкните правой кнопкой мыши папку вложенного приложения в диспетчере служб IIS и выберите **Convert to Application** (Преобразовать в приложение).

1. В диалоговом окне **Add Application** (Добавление приложения) нажмите кнопку **Select** (Выбрать), чтобы назначить созданный **пул приложений** вложенному приложению. Нажмите кнопку **ОК**.

Назначение отдельного пула приложений вложенному приложению является обязательным при использовании модели внутрипроцессного размещения.

Дополнительные сведения о внутрипроцессной модели размещения и настройке модуля ASP.NET Core см. в статьях <xref:host-and-deploy/aspnet-core-module> и <xref:host-and-deploy/aspnet-core-module>.

## <a name="configuration-of-iis-with-webconfig"></a>Настройка служб IIS с помощью файла web.config

Конфигурация IIS зависит от `<system.webServer>` раздела *web.config* для сценариев IIS, предназначенных для работы приложений ASP.NET Core с помощью модуля ASP.NET Core. Например, конфигурация IIS работает для динамического сжатия. Если в службах IIS на уровне сервера настроено динамическое сжатие, элемент `<urlCompression>` в файле *web.config* приложения может отключить это сжатие для приложения ASP.NET Core.

Дополнительные сведения см. в [справочнике по настройке \<system.webServer>](/iis/configuration/system.webServer/), [справочнике по настройке модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module) и статье [Модули IIS с ASP.NET Core](xref:host-and-deploy/iis/modules). Сведения о настройке переменных среды для отдельных приложений, выполняющихся в изолированных пулах приложений (такая возможность поддерживается в службах IIS начиная с версии 10.0), см. в справочной документации по службам IIS, в частности в разделе *AppCmd.exe* статьи [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) (Переменные среды <environmentVariables>).

## <a name="configuration-sections-of-webconfig"></a>Разделы конфигурации файла web.config

Разделы конфигурации приложений ASP.NET 4.x в файле *web.config* не используются для конфигурации приложений ASP.NET Core.

* `<system.web>`
* `<appSettings>`
* `<connectionStrings>`
* `<location>`

Для настройки приложений ASP.NET Core используются другие поставщики конфигураций. Дополнительные сведения см. в разделе [Конфигурация](xref:fundamentals/configuration/index).

## <a name="application-pools"></a>Пулы приложений

::: moniker range=">= aspnetcore-2.2"

Модель размещения определяет изоляцию пула приложений:

* Внутрипроцессное размещение &ndash; Приложения должны работать в отдельных пулах.
* Внепроцессное размещение &ndash; Рекомендуем изолировать приложения друг от друга, запуская каждое из них в собственном пуле.

В диалоговом окне **Добавление веб-сайта** IIS на каждое приложение по умолчанию задан один пул приложений. Если указано **Имя сайта**, оно автоматически переносится в текстовое поле **Пул приложений**. При добавлении веб-сайта создается пул приложений с именем сайта.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

При размещении на сервере множества веб-сайтов рекомендуем изолировать приложения друг от друга, запуская каждое из них в собственном пуле. В диалоговом окне **Добавить веб-сайт** служб IIS такая конфигурация задана по умолчанию. Если указано **Имя сайта**, оно автоматически переносится в текстовое поле **Пул приложений**. При добавлении веб-сайта создается пул приложений с именем сайта.

::: moniker-end

## <a name="application-pool-identity"></a>Удостоверение пула приложений

Учетная запись удостоверения пула приложений позволяет запускать приложение от имени уникальной учетной записи, не создавая домены или локальные учетные записи и не управляя ими. В службах IIS начиная с версии 8.0 рабочий процесс администратора IIS (WAS) создает виртуальную учетную запись с именем нового пула приложений и по умолчанию выполняет рабочие процессы пула приложений с помощью этой учетной записи. В консоли управления IIS в окне **Дополнительные параметры** для пула приложений должно быть выбрано **Удостоверение** **ApplicationPoolIdentity**.

![Диалоговое окно дополнительных параметров для пула приложений](index/_static/apppool-identity.png)

Процесс управления IIS создает в системе безопасности Windows безопасный идентификатор с именем пула приложений. С помощью этого идентификатора можно защищать ресурсы, но он не является реальной учетной записью и не отображается в консоли управления пользователями Windows.

Если рабочему процессу IIS требуется предоставить доступ к приложению с повышенными правами, измените список управления доступом (ACL) для каталога, содержащего приложение.

1. Откройте проводник и перейдите к каталогу.

1. Щелкните каталог правой кнопкой мыши и выберите пункт **Свойства**.

1. На вкладке **Безопасность** нажмите кнопку **Изменить**, а затем — кнопку **Добавить**.

1. Нажмите кнопку **Размещение** и выберите систему.

1. В поле **Введите имена выбираемых объектов** введите **IIS AppPool\\<имя_пула_приложений>**. Нажмите кнопку **Проверить имена**. В случае с *DefaultAppPool* проверьте имена с помощью **IIS AppPool\DefaultAppPool**. После нажатия кнопки **Проверить имена** в области имен объектов отобразится значение **DefaultAppPool**. Вручную ввести имя пула приложений в области имен объектов нельзя. При поиске имени объекта используйте формат **IIS AppPool\\<имя_пула_приложений>**.

   ![Диалоговое окно "Выбор пользователей или групп" для папки приложения. До нажатия кнопки "Проверить имена" в области имен объектов к строке IIS AppPool\" добавилось имя пула приложений, DefaultAppPool.](index/_static/select-users-or-groups-1.png)

1. Нажмите кнопку **ОК**.

   ![Диалоговое окно "Выбор пользователей или групп" для папки приложения. После нажатия кнопки "Проверить имена" в области имен объектов отображается имя пула приложений, DefaultAppPool.](index/_static/select-users-or-groups-2.png)

1. Разрешения на чтение и выполнение предоставляются по умолчанию. При необходимости предоставьте дополнительные разрешения.

Кроме того, доступ можно предоставить через командную строку, используя средство **ICACLS**. В случае с *DefaultAppPool* выполняется такая команда:

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

Дополнительные сведения об ICACLS см. [здесь](/windows-server/administration/windows-commands/icacls).

## <a name="http2-support"></a>Поддержка HTTP/2

::: moniker range=">= aspnetcore-2.2"

[HTTP/2](https://httpwg.org/specs/rfc7540.html) поддерживается в ASP.NET Core для следующих сценариев развертывания IIS:

* Внутрипроцессно
  * Windows Server 2016 / Windows 10 или более поздних версий; IIS 10 или более поздней версии
  * Подключение TLS 1.2 или более поздней версии.
* Внепроцессно
  * Windows Server 2016 / Windows 10 или более поздних версий; IIS 10 или более поздней версии
  * Подключения к пограничным серверам, открытых для общего доступа, выполняются по протоколу HTTP/2, а подключения к [серверу Kestrel](xref:fundamentals/servers/kestrel) через обратный прокси-сервер — по HTTP/1.1.
  * Подключение TLS 1.2 или более поздней версии.

При внутрипроцессном развертывании и установленном подключении HTTP/2 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) возвращает `HTTP/2`. При внепроцессном развертывании и установленном подключении HTTP/2 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) возвращает `HTTP/1.1`.

Дополнительные сведения о моделях размещения внутри и вне процесса см. в статьях <xref:host-and-deploy/aspnet-core-module> и <xref:host-and-deploy/aspnet-core-module>.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

[HTTP/2](https://httpwg.org/specs/rfc7540.html) поддерживается для внепроцессных развертываний, которые удовлетворяют следующим базовым требованиям:

* Windows Server 2016 / Windows 10 или более поздних версий; IIS 10 или более поздней версии
* Подключения к пограничным серверам, открытых для общего доступа, выполняются по протоколу HTTP/2, а подключения к [серверу Kestrel](xref:fundamentals/servers/kestrel) через обратный прокси-сервер — по HTTP/1.1.
* Целевая платформа: неприменимо к развертываниям вне процесса, так как IIS полностью обрабатывает подключение HTTP/2.
* Подключение TLS 1.2 или более поздней версии.

Если установлено подключение HTTP/2, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) возвращает `HTTP/1.1`.

::: moniker-end

Протокол HTTP/2 по умолчанию включен. Если не удается установить подключение HTTP/2, применяется резервный вариант HTTP/1.1. Дополнительные сведения о настройке HTTP/2 для развертываний IIS см. в статье [об HTTP/2 в IIS](/iis/get-started/whats-new-in-iis-10/http2-on-iis).

## <a name="cors-preflight-requests"></a>Предварительные запросы CORS

*Этот раздел относится только к приложениям ASP.NET Core, предназначенным для .NET Framework.*

Для приложения ASP.NET Core, предназначенного для .NET Framework, параметры OPTIONS не передаются в приложение по умолчанию в службах IIS. Чтобы узнать, как настроить обработчики приложения IIS в файле *web.config* для передачи запросов OPTIONS, см. раздел [Enable cross-origin requests in ASP.NET Web API 2. How CORS Works](/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api#how-cors-works) (Включение запросов CORS в ASP.NET Web API 2. Принцип работы CORS).

## <a name="deployment-resources-for-iis-administrators"></a>Ресурсы развертывания для администраторов IIS

Дополнительные сведения о службах IIS см. в документации по ним.  
[Документация по службам IIS](/iis)

Дополнительные сведения о моделях развертывания приложения .NET Core.  
[Развертывание приложений .NET Core](/dotnet/core/deploying/)

Сведения о том, как модуль ASP.NET Core позволяет веб-серверу Kestrel использовать IIS или IIS Express в качестве обратного прокси-сервера.  
[Модуль ASP.NET Core](xref:host-and-deploy/aspnet-core-module)

Сведения о настройке модуля ASP.NET Core для размещения приложений ASP.NET Core.  
[Справочник по конфигурации модуля ASP.NET Core](xref:host-and-deploy/aspnet-core-module)

Сведения о структуре каталогов опубликованных приложений ASP.NET Core.  
[Структура каталогов](xref:host-and-deploy/directory-structure)

Сведения об обнаружении активных и неактивных модулей IIS для приложения ASP.NET Core и управлении модулями IIS.  
[Модули IIS](xref:host-and-deploy/iis/troubleshoot)

Сведения о диагностике проблем с развертываниями IIS приложений ASP.NET Core.  
[Устранение неполадок](xref:host-and-deploy/iis/troubleshoot)

Распознавание распространенных ошибок при размещении приложений ASP.NET Core в IIS.  
[Справочник по общим ошибкам для службы приложений Azure и служб IIS](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a>Дополнительные ресурсы

* <xref:test/troubleshoot>
* [Введение в ASP.NET Core](xref:index)
* [Официальный веб-сайт Microsoft IIS](https://www.iis.net/)
* [Библиотека технического содержимого по Windows Server](/windows-server/windows-server)
* [HTTP/2 в IIS](/iis/get-started/whats-new-in-iis-10/http2-on-iis)
* <xref:host-and-deploy/iis/transform-webconfig>
