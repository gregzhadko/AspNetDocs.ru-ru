---
title: Веб-узел ASP.NET Core
author: guardrex
description: Сведения о веб-узле в ASP.NET Core, который отвечает за запуск приложений и управление временем существования.
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: fundamentals/host/web-host
ms.openlocfilehash: 878fbaa1a61946dadf23ba8fefbf22021e547cc2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044951"
---
# <a name="aspnet-core-web-host"></a>Веб-узел ASP.NET Core

Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)

Приложения ASP.NET Core настраивают и запускают *узел*. Узел отвечает за запуск приложения и управление временем существования. Узел настраивает как минимум сервер и конвейер обработки запросов. Узел также может настроить ведение журнала, внедрение зависимостей и конфигурацию.

::: moniker range="<= aspnetcore-1.1"

Для версии 1.1 этого раздела скачайте статью [Веб-узел ASP.NET Core (версия 1.1, PDF-файл)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Web-Host_1.1.pdf).

::: moniker-end

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

В этой статье рассматривается веб-узел ASP.NET Core (<xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>), который предназначен для размещения веб-приложений. Сведения об универсальном узле .NET ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)) см. в статье <xref:fundamentals/host/generic-host>.

::: moniker-end

::: moniker range="> aspnetcore-2.2"

В этой статье рассматривается веб-узел ASP.NET Core ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)). В ASP.NET Core 3.0 универсальный узел заменяет веб-узел. Дополнительную информацию см. в разделе [Узел](xref:fundamentals/index#host).

::: moniker-end

## <a name="set-up-a-host"></a>Создание узла

Создайте узел с помощью экземпляра [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder). Обычно это делается в точке входа в приложение, то есть в методе `Main`. В шаблонах проектов метод `Main` находится в файле *Program.cs*. Обычно *Program.cs* вызывает [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), чтобы начать настройку узла.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>();
}
```

Метод `CreateDefaultBuilder` выполняет указанные ниже задачи.

* Настраивает сервер [Kestrel](xref:fundamentals/servers/kestrel) в качестве веб-сервера с помощью поставщиков конфигурации размещения приложения. Параметры сервера Kestrel по умолчанию см. в разделе <xref:fundamentals/servers/kestrel#kestrel-options>.
* В качестве корня содержимого задает путь, возвращенный методом [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).
* Загружает [конфигурацию узла](#host-configuration-values) из:
  * Переменные среды с префиксом `ASPNETCORE_` (например, `ASPNETCORE_ENVIRONMENT`).
  * аргументы командной строки.
* Загружает конфигурацию приложения в следующем порядке из:
  * *appsettings.json*;
  * *appsettings.{Environment}.json*;
  * [Менеджера секретов](xref:security/app-secrets), когда приложение выполняется в среде `Development` с использованием начальных сборок.
  * Переменные среды.
  * аргументы командной строки.
* Настраивает [ведение журнала](xref:fundamentals/logging/index) для выходных данных консоли и отладки. Ведение журнала включает в себя правила [фильтрации журналов](xref:fundamentals/logging/index#log-filtering), заданные в разделе конфигурации ведения журнала в файле *appsettings.json* или *appsettings.{Environment}.json*.
* При работе за службами IIS с [модулем ASP.NET Core](xref:host-and-deploy/aspnet-core-module) `CreateDefaultBuilder` обеспечивает [интеграцию со службами IIS](xref:host-and-deploy/iis/index) для настройки базового адреса и порта приложения. Кроме того, интеграция со службами IIS также позволяет настраивать [перехват приложением ошибок запуска](#capture-startup-errors). Параметры IIS по умолчанию см. в разделе <xref:host-and-deploy/iis/index#iis-options>.
* Устанавливает для [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) значение `true`, если приложение находится в среде разработки. Дополнительные сведения см. в разделе [Проверка области](#scope-validation).

Настройки, определенные `CreateDefaultBuilder`, можно переопределить и усилить с помощью [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging) и других методов и методов расширения [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder). Ниже приведены некоторые примеры:

* [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) используется для указания дополнительного объекта `IConfiguration` для приложения. Следующий вызов `ConfigureAppConfiguration` добавляет делегат, чтобы включить конфигурацию приложения в файл *appsettings.xml*. `ConfigureAppConfiguration` можно вызывать несколько раз. Обратите внимание, что эта конфигурация не распространяется на узел (например, URL-адреса серверов или среду). См. раздел [Значения конфигурации узла](#host-configuration-values).

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureAppConfiguration((hostingContext, config) =>
        {
            config.AddXmlFile("appsettings.xml", optional: true, reloadOnChange: true);
        })
        ...
    ```

* Следующий вызов `ConfigureLogging` добавляет делегата, чтобы настроить минимальный уровень ведения журнала ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) для [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel). Этот параметр переопределяет параметры в *appsettings.Development.json* (`LogLevel.Debug`) и *appsettings.Production.json* (`LogLevel.Error`), заданные `CreateDefaultBuilder`. `ConfigureLogging` можно вызывать несколько раз.

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureLogging(logging => 
        {
            logging.SetMinimumLevel(LogLevel.Warning);
        })
        ...
    ```

::: moniker range=">= aspnetcore-2.2"

* При следующем вызове к `ConfigureKestrel` переопределяется значение по умолчанию [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize), равное 30 000 000 байтов, установленное при настройке Kestrel методом `CreateDefaultBuilder`:

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureKestrel((context, options) =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
    ```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* Следующий вызов [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) переопределяет значение по умолчанию [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize), равное 30 000 000 байтов, установленное при настройке Kestrel методом `CreateDefaultBuilder`:

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .UseKestrel(options =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
    ```

::: moniker-end

*Корень содержимого* определяет, где узел ищет файлы содержимого, например файлы представлений MVC. При запуске приложения из корневой папки проекта эта папка используется в качестве корня содержимого. Такое поведение по умолчанию принято в [Visual Studio](https://www.visualstudio.com/) и [шаблонах dotnet new](/dotnet/core/tools/dotnet-new).

Дополнительные сведения о конфигурации приложения см. в разделе <xref:fundamentals/configuration/index>.

> [!NOTE]
> Помимо использования статического метода `CreateDefaultBuilder`, в ASP.NET Core 2.x поддерживается создание узла на основе [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder). Дополнительные сведения см. на вкладке со сведениями об ASP.NET Core 1.x.

При настройке узла можно предоставить методы [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) и [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1). Если используется класс `Startup`, в нем должен быть определен метод `Configure`. Дополнительные сведения см. в разделе <xref:fundamentals/startup>. Несколько вызовов `ConfigureServices` добавляются друг к другу. При нескольких вызовах `Configure` или `UseStartup` в `WebHostBuilder` предыдущие параметры заменяются.

## <a name="host-configuration-values"></a>Значения конфигурации узла

Для задания значений конфигурации узла класс [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) поддерживает следующие подходы:

* конфигурация построителя узла, которая включает в себя переменные среды в формате `ASPNETCORE_{configurationKey}`, Например, `ASPNETCORE_ENVIRONMENT`.
* Расширения, такие как [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) и [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) (см. раздел [Переопределение конфигурации](#override-configuration)).
* метод [UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) и связанный ключ. Значение, задаваемое с помощью `UseSetting`, всегда является строкой независимо от типа.

Хост использует значение, заданное последним. Дополнительные сведения см. в подразделе [Переопределение конфигурации](#override-configuration) следующего раздела.

### <a name="application-key-name"></a>Ключ приложения (имя)

Свойство [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) задается автоматически при вызове [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) или [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) во время создания узла. Значение присваивается имени сборки, содержащей точку входа приложения. Чтобы явно задать значение, используйте [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey).

**Ключ**: applicationName  
**Тип**: *string*  
**По умолчанию**: имя сборки, содержащей точку входа приложения.  
**Задается с помощью**: `UseSetting`  
**Переменная среды**: `ASPNETCORE_APPLICATIONNAME`

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.ApplicationKey, "CustomApplicationName")
```

### <a name="capture-startup-errors"></a>Перехват ошибок при загрузке

Этот параметр управляет перехватом ошибок при загрузке.

**Ключ**: captureStartupErrors  
**Тип**: *bool* (`true` или `1`)  
**По умолчанию**: `false`, если только приложение не работает с сервером Kestrel за службами IIS; в этом случае значение по умолчанию — `true`.  
**Задается с помощью**: `CaptureStartupErrors`  
**Переменная среды**: `ASPNETCORE_CAPTURESTARTUPERRORS`

Если задано значение `false`, ошибки во время запуска приводят к завершению работы узла. Если задано значение `true`, узел перехватывает исключения во время запуска и пытается запустить сервер.

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
```

### <a name="content-root"></a>Корень содержимого

Этот параметр определяет то, где ASP.NET Core начинает искать файлы содержимого, например представления MVC. 

**Ключ**: contentRoot  
**Тип**: *string*  
**По умолчанию**: папка, в которой находится сборка приложения.  
**Задается с помощью**: `UseContentRoot`  
**Переменная среды**: `ASPNETCORE_CONTENTROOT`

Корень содержимого также используется в качестве базового пути для [корневого каталога документов](#web-root). Если путь не существует, узел не запускается.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\<content-root>")
```

### <a name="detailed-errors"></a>Подробные сообщения об ошибках

Определяет, следует ли перехватывать подробные сообщения об ошибках.

**Ключ**: detailedErrors  
**Тип**: *bool* (`true` или `1`)  
**Значение по умолчанию**: false  
**Задается с помощью**: `UseSetting`  
**Переменная среды**: `ASPNETCORE_DETAILEDERRORS`

Если этот параметр включен (или если параметр <a href="#environment">Среда</a> имеет значение `Development`), приложение перехватывает подробные исключения.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

### <a name="environment"></a>Среда

Задает среду приложения.

**Ключ**: environment  
**Тип**: *string*  
**По умолчанию**: Рабочие  
**Задается с помощью**: `UseEnvironment`  
**Переменная среды**: `ASPNETCORE_ENVIRONMENT`

В качестве среды можно указать любое значение. В платформе определены значения `Development`, `Staging` и `Production`. Регистр символов в значениях не учитывается. По умолчанию значение параметра *Среда* считывается из переменной среды `ASPNETCORE_ENVIRONMENT`. При использовании [Visual Studio](https://www.visualstudio.com/) переменные среды можно задавать в файле *launchSettings.json*. Дополнительные сведения см. в разделе <xref:fundamentals/environments>.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment(EnvironmentName.Development)
```

### <a name="hosting-startup-assemblies"></a>Начальные сборки размещения

Задает начальные сборки размещения для приложения.

**Ключ**: hostingStartupAssemblies  
**Тип**: *string*  
**По умолчанию**: Пустая строка  
**Задается с помощью**: `UseSetting`  
**Переменная среды**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`

Разделенная точками с запятой строка начальных сборок размещения, загружаемых при запуске.

Хотя значением по умолчанию этого параметра конфигурации является пустая строка, начальные сборки размещения всегда включают в себя сборку приложения. Если начальные сборки размещения указаны, они добавляются к сборке приложения для загрузки во время построения приложением общих служб при запуске.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
```

### <a name="https-port"></a>HTTPS-порт

Задайте порт перенаправления HTTPS. Используется при [принудительном применении HTTPS](xref:security/enforcing-ssl).

**Ключ**: https_port **Тип**: *string*
**По умолчанию**: значение по умолчанию не задано.
**Задается с помощью**: `UseSetting`
**переменной среды**: `ASPNETCORE_HTTPS_PORT`

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

### <a name="hosting-startup-exclude-assemblies"></a>Исключаемые начальные сборки размещения

Разделенная точками с запятой строка начальных сборок размещения, которые необходимо исключить при запуске.

**Ключ**: hostingStartupExcludeAssemblies  
**Тип**: *string*  
**По умолчанию**: Пустая строка  
**Задается с помощью**: `UseSetting`  
**Переменная среды**: `ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES`

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupExcludeAssembliesKey, "assembly1;assembly2")
```

### <a name="prefer-hosting-urls"></a>Предпочитать URL-адреса размещения

Указывает, должен ли узел ожидать передачи данных по URL-адресам, настроенным с помощью `WebHostBuilder`, вместо настроенных с помощью реализации `IServer`.

**Ключ**: preferHostingUrls  
**Тип**: *bool* (`true` или `1`)  
**Значение по умолчанию**: true  
**Задается с помощью**: `PreferHostingUrls`  
**Переменная среды**: `ASPNETCORE_PREFERHOSTINGURLS`

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
```

### <a name="prevent-hosting-startup"></a>Запретить запуск размещения

Запрещает автоматическую загрузку начальных сборок размещения, включая начальные сборки размещения, настроенные сборкой приложения. Дополнительные сведения см. в разделе <xref:fundamentals/configuration/platform-specific-configuration>.

**Ключ**: preventHostingStartup  
**Тип**: *bool* (`true` или `1`)  
**Значение по умолчанию**: false  
**Задается с помощью**: `UseSetting`  
**Переменная среды**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
```

### <a name="server-urls"></a>URL-адреса сервера

Задает IP-адреса или адреса узлов с портами и протоколами, по которым сервер должен ожидать получения запросов.

**Ключ**: urls  
**Тип**: *string*  
**По умолчанию**: http://localhost:5000  
**Задается с помощью**: `UseUrls`  
**Переменная среды**: `ASPNETCORE_URLS`

Укажите разделенный точками с запятой (;) список префиксов URL-адресов, на которые сервер должен отвечать. Например, `http://localhost:123`. Используйте символ "\*", чтобы указать, что сервер должен ожидать получения запросов через определенный порт и по определенному протоколу по любому IP-адресу или имени узла (например, `http://*:5000`). Протокол (`http://` или `https://`) должен указываться для каждого URL-адреса. Поддерживаемые форматы зависят от сервера.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

Kestrel имеет собственный интерфейс API настройки конечных точек. Дополнительные сведения см. в разделе <xref:fundamentals/servers/kestrel#endpoint-configuration>.

### <a name="shutdown-timeout"></a>Время ожидания завершения работы

Определяет, как долго необходимо ожидать завершения работы веб-узла.

**Ключ**: shutdownTimeoutSeconds  
**Тип**: *int*  
**По умолчанию**: 5  
**Задается с помощью**: `UseShutdownTimeout`  
**Переменная среды**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`

Хотя ключ принимает значение *int* с `UseSetting` (например, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), метод расширения [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) принимает [TimeSpan](/dotnet/api/system.timespan).

Во время ожидания размещение:

* Активирует [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).
* Пытается остановить размещенные службы, записывая в журнал все ошибки для служб, которые не удалось остановить.

Если время ожидания истекает до остановки всех размещенных служб, активные службы останавливаются при завершении работы приложения. Службы останавливаются даже в том случае, если еще не завершили обработку. Если службе требуется дополнительное время для остановки, увеличьте время ожидания.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
```

### <a name="startup-assembly"></a>Стартовая сборка

Определяет сборку, в которой необходимо искать класс `Startup`.

**Ключ**: startupAssembly  
**Тип**: *string*  
**По умолчанию**: сборка приложения  
**Задается с помощью**: `UseStartup`  
**Переменная среды**: `ASPNETCORE_STARTUPASSEMBLY`

На сборку можно ссылаться по имени (`string`) или типу (`TStartup`). При вызове нескольких методов `UseStartup` приоритет имеет последний.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
```

### <a name="web-root"></a>Корневой каталог документов

Задает относительный путь к статическим ресурсам приложения.

**Ключ**: webroot  
**Тип**: *string*  
**По умолчанию**: если значение не задано, по умолчанию используется путь "(Корень содержимого)/wwwroot" при его наличии. Если этот путь не существует, используется фиктивный поставщик файлов.  
**Задается с помощью**: `UseWebRoot`  
**Переменная среды**: `ASPNETCORE_WEBROOT`

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
```

## <a name="override-configuration"></a>Переопределение конфигурации

Используйте [конфигурацию](xref:fundamentals/configuration/index) для настройки веб-узла. В приведенном ниже примере необязательная конфигурация узла задается в файле *hostsettings.json*. Любую конфигурацию, загружаемую из файла *hostsettings.json*, можно переопределить с помощью аргументов командной строки. Встроенная конфигурация (в `config`) используется для настройки узла с помощью [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration). Конфигурация `IWebHostBuilder` добавляется в конфигурацию приложения, но не наоборот &mdash; `ConfigureAppConfiguration` не влияет на конфигурацию `IWebHostBuilder`.

Конфигурация, предоставленная методом `UseUrls`, сначала переопределяется конфигурацией из файла *hostsettings.json*, а затем с помощью аргументов командной строки:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hostsettings.json", optional: true)
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            });
    }
}
```

*hostsettings.json*:

```json
{
    urls: "http://*:5005"
}
```

> [!NOTE]
> Метод расширения [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) в настоящее время не может анализировать раздел конфигурации, возвращаемый методом `GetSection` (например, `.UseConfiguration(Configuration.GetSection("section"))`). Метод `GetSection` фильтрует ключи конфигурации до запрошенного раздела, но оставляет имя раздела в ключах (например, `section:urls`, `section:environment`). Метод `UseConfiguration` ожидает, что ключи соответствуют ключам `WebHostBuilder` (например, `urls`, `environment`). Наличие имени раздела в ключах предотвращает настройку узла с помощью значений этого раздела. Эта проблема будет устранена в следующем выпуске. Дополнительные сведения и способы решения см. в описании проблемы [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839) (При передаче раздела конфигурации в WebHostBuilder.UseConfiguration используются полные ключи).
>
> `UseConfiguration` копирует ключи только из предоставленного объекта `IConfiguration` для конфигурации конструктора узла. Поэтому указание `reloadOnChange: true` для файлов JSON, XML и INI ни на что не влияет.

Чтобы указать узел, выполняющийся по определенному URL-адресу, можно передать нужное значение из командной строки при выполнении команды [dotnet run](/dotnet/core/tools/dotnet-run). Аргумент командной строки переопределяет значение `urls` из файла *hostsettings.json*, и сервер будет ожидать передачи данных через порт 8080:

```console
dotnet run --urls "http://*:8080"
```

## <a name="manage-the-host"></a>Управление узлом

**Выполнить**

Метод `Run` запускает веб-приложение и блокирует вызывающий поток до тех пор, пока работа узла не будет завершена.

```csharp
host.Run();
```

**Запуск**

Чтобы запустить узел без блокировки, вызовите метод `Start`.

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

Если в метод `Start` передается список URL-адресов, он будет ожидать передачи данных по указанным URL-адресам.

```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

Приложение может инициализировать и запустить новый узел с использованием предварительно настроенных значений по умолчанию `CreateDefaultBuilder` с помощью статического удобного метода. Эти методы запускают сервер без вывода данных в консоль и со временем ожидания прерывания, равным [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) (Ctrl-C/SIGINT или SIGTERM):

**Start(RequestDelegate app)**

Выполните запуск с помощью `RequestDelegate`:

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

В браузере выполните запрос по адресу `http://localhost:5000`, чтобы получить ответ "Hello World!" `WaitForShutdown` блокируется, пока не будет создано прерывание (Ctrl-C/SIGINT или SIGTERM). Приложение выводит сообщение `Console.WriteLine` и ожидает нажатия клавиши, после чего завершает работу.

**Start(string url, RequestDelegate app)**

Выполните запуск с помощью URL-адреса и `RequestDelegate`:

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

Результат будет тем же, что и при использовании **Start(RequestDelegate app)**, но приложение отвечает по адресу `http://localhost:8080`.

**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**

Используйте экземпляр `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) для применения ПО промежуточного слоя маршрутизации:

```csharp
using (var host = WebHost.Start(router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

В этом примере используйте следующие запросы в браузере:

| Запрос                                    | Ответ                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | Hello, Martin!                           |
| `http://localhost:5000/buenosdias/Catrina` | Buenos dias, Catrina!                    |
| `http://localhost:5000/throw/ooops!`       | Вызывает исключение со строкой "ooops!" |
| `http://localhost:5000/throw`              | Вызывает исключение со строкой "Uh oh!" |
| `http://localhost:5000/Sante/Kevin`        | Sante, Kevin!                            |
| `http://localhost:5000`                    | Пример "Здравствуй,                             |

`WaitForShutdown` блокируется, пока не будет создано прерывание (Ctrl-C/SIGINT или SIGTERM). Приложение выводит сообщение `Console.WriteLine` и ожидает нажатия клавиши, после чего завершает работу.

**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**

Используйте URL-адрес и экземпляр `IRouteBuilder`:

```csharp
using (var host = WebHost.Start("http://localhost:8080", router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

Результат будет тем же, что и при использовании **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, но приложение будет отвечать по адресу `http://localhost:8080`.

**StartWith(Action&lt;IApplicationBuilder&gt; app)**

Предоставьте делегат для настройки `IApplicationBuilder`:

```csharp
using (var host = WebHost.StartWith(app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

В браузере выполните запрос по адресу `http://localhost:5000`, чтобы получить ответ "Hello World!" `WaitForShutdown` блокируется, пока не будет создано прерывание (Ctrl-C/SIGINT или SIGTERM). Приложение выводит сообщение `Console.WriteLine` и ожидает нажатия клавиши, после чего завершает работу.

**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**

Предоставьте URL-адрес и делегат для настройки `IApplicationBuilder`:

```csharp
using (var host = WebHost.StartWith("http://localhost:8080", app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

Результат будет тем же, что и при использовании **StartWith(Action&lt;IApplicationBuilder&gt; app)**, но приложение будет отвечать по адресу `http://localhost:8080`.

## <a name="ihostingenvironment-interface"></a>Интерфейс IHostingEnvironment

[Интерфейс IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) предоставляет сведения о среде веб-размещения приложения. Чтобы получить интерфейс `IHostingEnvironment` для использования его свойств и методов расширения, воспользуйтесь [внедрением конструктора](xref:fundamentals/dependency-injection):

```csharp
public class CustomFileReader
{
    private readonly IHostingEnvironment _env;

    public CustomFileReader(IHostingEnvironment env)
    {
        _env = env;
    }

    public string ReadFile(string filePath)
    {
        var fileProvider = _env.WebRootFileProvider;
        // Process the file here
    }
}
```

Для настройки приложения при запуске в соответствии со средой можно применять [подход на основе соглашения](xref:fundamentals/environments#environment-based-startup-class-and-methods). Кроме того, можно внедрить интерфейс `IHostingEnvironment` в конструктор `Startup` для использования в `ConfigureServices`:

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        HostingEnvironment = env;
    }

    public IHostingEnvironment HostingEnvironment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        if (HostingEnvironment.IsDevelopment())
        {
            // Development configuration
        }
        else
        {
            // Staging/Production configuration
        }

        var contentRootPath = HostingEnvironment.ContentRootPath;
    }
}
```

> [!NOTE]
> Помимо метода расширения `IsDevelopment`, интерфейс `IHostingEnvironment` предоставляет методы `IsStaging`, `IsProduction` и `IsEnvironment(string environmentName)`. Дополнительные сведения см. в разделе <xref:fundamentals/environments>.

Службу `IHostingEnvironment` также можно внедрять непосредственно в метод `Configure` для настройки конвейера обработки:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // In Development, use the developer exception page
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // In Staging/Production, route exceptions to /error
        app.UseExceptionHandler("/error");
    }

    var contentRootPath = env.ContentRootPath;
}
```

`IHostingEnvironment` можно внедрить в метод `Invoke` при создании пользовательского [ПО промежуточного слоя](xref:fundamentals/middleware/write):

```csharp
public async Task Invoke(HttpContext context, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // Configure middleware for Development
    }
    else
    {
        // Configure middleware for Staging/Production
    }

    var contentRootPath = env.ContentRootPath;
}
```

## <a name="iapplicationlifetime-interface"></a>Интерфейс IApplicationLifetime

[Интерфейс IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) позволяет выполнять действия после запуска и завершения работы. Три свойства этого интерфейса представляют собой токены отмены, которые служат для регистрации методов `Action`, определяющих события запуска и завершения работы.

| Токен отмены    | Условие инициации&#8230; |
| --------------------- | --------------------- |
| [ApplicationStarted](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | Узел полностью запущен. |
| [ApplicationStopped](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | Заканчивается нормальное завершение работы узла. Все запросы должны быть обработаны. Завершение работы блокируется до тех пор, пока это событие не завершится. |
| [ApplicationStopping](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | Происходит нормальное завершение работы узла. Запросы могут все еще обрабатываться. Завершение работы блокируется до тех пор, пока это событие не завершится. |

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app, IApplicationLifetime appLifetime)
    {
        appLifetime.ApplicationStarted.Register(OnStarted);
        appLifetime.ApplicationStopping.Register(OnStopping);
        appLifetime.ApplicationStopped.Register(OnStopped);

        Console.CancelKeyPress += (sender, eventArgs) =>
        {
            appLifetime.StopApplication();
            // Don't terminate the process immediately, wait for the Main thread to exit gracefully.
            eventArgs.Cancel = true;
        };
    }

    private void OnStarted()
    {
        // Perform post-startup activities here
    }

    private void OnStopping()
    {
        // Perform on-stopping activities here
    }

    private void OnStopped()
    {
        // Perform post-stopped activities here
    }
}
```

[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) запрашивает остановку приложения. Следующий класс использует `StopApplication` для корректного завершения работы приложения при вызове метода класса `Shutdown`:

```csharp
public class MyClass
{
    private readonly IApplicationLifetime _appLifetime;

    public MyClass(IApplicationLifetime appLifetime)
    {
        _appLifetime = appLifetime;
    }

    public void Shutdown()
    {
        _appLifetime.StopApplication();
    }
}
```

## <a name="scope-validation"></a>Проверка области

[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) устанавливает для [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) значение `true`, если приложение находится в среде разработки.

Если для `ValidateScopes` установлено значение `true`, поставщик службы по умолчанию проверяет, что:

* Службы с заданной областью не разрешаются из корневого поставщика службы, прямо или косвенно.
* Службы с заданной областью не вводятся в одноэлементные объекты, прямо или косвенно.

Корневой поставщик службы создается при вызове [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider). Время существования корневого поставщика службы соответствует времени существования приложения или сервера — поставщик запускается с приложением и удаляется, когда приложение завершает работу.

Службы с заданной областью удаляются создавшим их контейнером. Если служба с заданной областью создается в корневом контейнере, время существования службы повышается до уровня одноэлементного объекта, поскольку она удаляется только корневым контейнером при завершении работы приложения или сервера. Проверка областей службы перехватывает эти ситуации при вызове `BuildServiceProvider`.

Чтобы всегда проверять области, в том числе в рабочей среде, настройте [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) с [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) в конструкторе узлов:

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="additional-resources"></a>Дополнительные ресурсы

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <xref:host-and-deploy/windows-service>
