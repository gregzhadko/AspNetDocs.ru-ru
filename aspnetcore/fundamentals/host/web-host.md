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
# <a name="aspnet-core-web-host"></a><span data-ttu-id="d0948-103">Веб-узел ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d0948-103">ASP.NET Core Web Host</span></span>

<span data-ttu-id="d0948-104">Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)</span><span class="sxs-lookup"><span data-stu-id="d0948-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d0948-105">Приложения ASP.NET Core настраивают и запускают *узел*.</span><span class="sxs-lookup"><span data-stu-id="d0948-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="d0948-106">Узел отвечает за запуск приложения и управление временем существования.</span><span class="sxs-lookup"><span data-stu-id="d0948-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="d0948-107">Узел настраивает как минимум сервер и конвейер обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="d0948-107">At a minimum, the host configures a server and a request processing pipeline.</span></span> <span data-ttu-id="d0948-108">Узел также может настроить ведение журнала, внедрение зависимостей и конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="d0948-108">The host can also set up logging, dependency injection, and configuration.</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="d0948-109">Для версии 1.1 этого раздела скачайте статью [Веб-узел ASP.NET Core (версия 1.1, PDF-файл)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Web-Host_1.1.pdf).</span><span class="sxs-lookup"><span data-stu-id="d0948-109">For the 1.1 version of this topic, download [ASP.NET Core Web Host (version 1.1, PDF)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Web-Host_1.1.pdf).</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

<span data-ttu-id="d0948-110">В этой статье рассматривается веб-узел ASP.NET Core (<xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>), который предназначен для размещения веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d0948-110">This article covers the ASP.NET Core Web Host (<xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>), which is for hosting web apps.</span></span> <span data-ttu-id="d0948-111">Сведения об универсальном узле .NET ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)) см. в статье <xref:fundamentals/host/generic-host>.</span><span class="sxs-lookup"><span data-stu-id="d0948-111">For information about the .NET Generic Host ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)), see <xref:fundamentals/host/generic-host>.</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.2"

<span data-ttu-id="d0948-112">В этой статье рассматривается веб-узел ASP.NET Core ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)).</span><span class="sxs-lookup"><span data-stu-id="d0948-112">This article covers the ASP.NET Core Web Host ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)).</span></span> <span data-ttu-id="d0948-113">В ASP.NET Core 3.0 универсальный узел заменяет веб-узел.</span><span class="sxs-lookup"><span data-stu-id="d0948-113">In ASP.NET Core 3.0, Generic Host replaces Web Host.</span></span> <span data-ttu-id="d0948-114">Дополнительную информацию см. в разделе [Узел](xref:fundamentals/index#host).</span><span class="sxs-lookup"><span data-stu-id="d0948-114">For more information, see [The host](xref:fundamentals/index#host).</span></span>

::: moniker-end

## <a name="set-up-a-host"></a><span data-ttu-id="d0948-115">Создание узла</span><span class="sxs-lookup"><span data-stu-id="d0948-115">Set up a host</span></span>

<span data-ttu-id="d0948-116">Создайте узел с помощью экземпляра [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span><span class="sxs-lookup"><span data-stu-id="d0948-116">Create a host using an instance of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="d0948-117">Обычно это делается в точке входа в приложение, то есть в методе `Main`.</span><span class="sxs-lookup"><span data-stu-id="d0948-117">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="d0948-118">В шаблонах проектов метод `Main` находится в файле *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="d0948-118">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="d0948-119">Обычно *Program.cs* вызывает [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), чтобы начать настройку узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-119">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

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

<span data-ttu-id="d0948-120">Метод `CreateDefaultBuilder` выполняет указанные ниже задачи.</span><span class="sxs-lookup"><span data-stu-id="d0948-120">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="d0948-121">Настраивает сервер [Kestrel](xref:fundamentals/servers/kestrel) в качестве веб-сервера с помощью поставщиков конфигурации размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-121">Configures [Kestrel](xref:fundamentals/servers/kestrel) server as the web server using the app's hosting configuration providers.</span></span> <span data-ttu-id="d0948-122">Параметры сервера Kestrel по умолчанию см. в разделе <xref:fundamentals/servers/kestrel#kestrel-options>.</span><span class="sxs-lookup"><span data-stu-id="d0948-122">For the Kestrel server's default options, see <xref:fundamentals/servers/kestrel#kestrel-options>.</span></span>
* <span data-ttu-id="d0948-123">В качестве корня содержимого задает путь, возвращенный методом [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span><span class="sxs-lookup"><span data-stu-id="d0948-123">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="d0948-124">Загружает [конфигурацию узла](#host-configuration-values) из:</span><span class="sxs-lookup"><span data-stu-id="d0948-124">Loads [host configuration](#host-configuration-values) from:</span></span>
  * <span data-ttu-id="d0948-125">Переменные среды с префиксом `ASPNETCORE_` (например, `ASPNETCORE_ENVIRONMENT`).</span><span class="sxs-lookup"><span data-stu-id="d0948-125">Environment variables prefixed with `ASPNETCORE_` (for example, `ASPNETCORE_ENVIRONMENT`).</span></span>
  * <span data-ttu-id="d0948-126">аргументы командной строки.</span><span class="sxs-lookup"><span data-stu-id="d0948-126">Command-line arguments.</span></span>
* <span data-ttu-id="d0948-127">Загружает конфигурацию приложения в следующем порядке из:</span><span class="sxs-lookup"><span data-stu-id="d0948-127">Loads app configuration in the following order from:</span></span>
  * <span data-ttu-id="d0948-128">*appsettings.json*;</span><span class="sxs-lookup"><span data-stu-id="d0948-128">*appsettings.json*.</span></span>
  * <span data-ttu-id="d0948-129">*appsettings.{Environment}.json*;</span><span class="sxs-lookup"><span data-stu-id="d0948-129">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="d0948-130">[Менеджера секретов](xref:security/app-secrets), когда приложение выполняется в среде `Development` с использованием начальных сборок.</span><span class="sxs-lookup"><span data-stu-id="d0948-130">[Secret Manager](xref:security/app-secrets) when the app runs in the `Development` environment using the entry assembly.</span></span>
  * <span data-ttu-id="d0948-131">Переменные среды.</span><span class="sxs-lookup"><span data-stu-id="d0948-131">Environment variables.</span></span>
  * <span data-ttu-id="d0948-132">аргументы командной строки.</span><span class="sxs-lookup"><span data-stu-id="d0948-132">Command-line arguments.</span></span>
* <span data-ttu-id="d0948-133">Настраивает [ведение журнала](xref:fundamentals/logging/index) для выходных данных консоли и отладки.</span><span class="sxs-lookup"><span data-stu-id="d0948-133">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="d0948-134">Ведение журнала включает в себя правила [фильтрации журналов](xref:fundamentals/logging/index#log-filtering), заданные в разделе конфигурации ведения журнала в файле *appsettings.json* или *appsettings.{Environment}.json*.</span><span class="sxs-lookup"><span data-stu-id="d0948-134">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="d0948-135">При работе за службами IIS с [модулем ASP.NET Core](xref:host-and-deploy/aspnet-core-module) `CreateDefaultBuilder` обеспечивает [интеграцию со службами IIS](xref:host-and-deploy/iis/index) для настройки базового адреса и порта приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-135">When running behind IIS with the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module), `CreateDefaultBuilder` enables [IIS Integration](xref:host-and-deploy/iis/index), which configures the app's base address and port.</span></span> <span data-ttu-id="d0948-136">Кроме того, интеграция со службами IIS также позволяет настраивать [перехват приложением ошибок запуска](#capture-startup-errors).</span><span class="sxs-lookup"><span data-stu-id="d0948-136">IIS Integration also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="d0948-137">Параметры IIS по умолчанию см. в разделе <xref:host-and-deploy/iis/index#iis-options>.</span><span class="sxs-lookup"><span data-stu-id="d0948-137">For the IIS default options, see <xref:host-and-deploy/iis/index#iis-options>.</span></span>
* <span data-ttu-id="d0948-138">Устанавливает для [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) значение `true`, если приложение находится в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="d0948-138">Sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span> <span data-ttu-id="d0948-139">Дополнительные сведения см. в разделе [Проверка области](#scope-validation).</span><span class="sxs-lookup"><span data-stu-id="d0948-139">For more information, see [Scope validation](#scope-validation).</span></span>

<span data-ttu-id="d0948-140">Настройки, определенные `CreateDefaultBuilder`, можно переопределить и усилить с помощью [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging) и других методов и методов расширения [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span><span class="sxs-lookup"><span data-stu-id="d0948-140">The configuration defined by `CreateDefaultBuilder` can be overridden and augmented by [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging), and other methods and extension methods of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="d0948-141">Ниже приведены некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="d0948-141">A few examples follow:</span></span>

* <span data-ttu-id="d0948-142">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) используется для указания дополнительного объекта `IConfiguration` для приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-142">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) is used to specify additional `IConfiguration` for the app.</span></span> <span data-ttu-id="d0948-143">Следующий вызов `ConfigureAppConfiguration` добавляет делегат, чтобы включить конфигурацию приложения в файл *appsettings.xml*.</span><span class="sxs-lookup"><span data-stu-id="d0948-143">The following `ConfigureAppConfiguration` call adds a delegate to include app configuration in the *appsettings.xml* file.</span></span> <span data-ttu-id="d0948-144">`ConfigureAppConfiguration` можно вызывать несколько раз.</span><span class="sxs-lookup"><span data-stu-id="d0948-144">`ConfigureAppConfiguration` may be called multiple times.</span></span> <span data-ttu-id="d0948-145">Обратите внимание, что эта конфигурация не распространяется на узел (например, URL-адреса серверов или среду).</span><span class="sxs-lookup"><span data-stu-id="d0948-145">Note that this configuration doesn't apply to the host (for example, server URLs or environment).</span></span> <span data-ttu-id="d0948-146">См. раздел [Значения конфигурации узла](#host-configuration-values).</span><span class="sxs-lookup"><span data-stu-id="d0948-146">See the [Host configuration values](#host-configuration-values) section.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureAppConfiguration((hostingContext, config) =>
        {
            config.AddXmlFile("appsettings.xml", optional: true, reloadOnChange: true);
        })
        ...
    ```

* <span data-ttu-id="d0948-147">Следующий вызов `ConfigureLogging` добавляет делегата, чтобы настроить минимальный уровень ведения журнала ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) для [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel).</span><span class="sxs-lookup"><span data-stu-id="d0948-147">The following `ConfigureLogging` call adds a delegate to configure the minimum logging level ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) to [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="d0948-148">Этот параметр переопределяет параметры в *appsettings.Development.json* (`LogLevel.Debug`) и *appsettings.Production.json* (`LogLevel.Error`), заданные `CreateDefaultBuilder`.</span><span class="sxs-lookup"><span data-stu-id="d0948-148">This setting overrides the settings in *appsettings.Development.json* (`LogLevel.Debug`) and *appsettings.Production.json* (`LogLevel.Error`) configured by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="d0948-149">`ConfigureLogging` можно вызывать несколько раз.</span><span class="sxs-lookup"><span data-stu-id="d0948-149">`ConfigureLogging` may be called multiple times.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureLogging(logging => 
        {
            logging.SetMinimumLevel(LogLevel.Warning);
        })
        ...
    ```

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d0948-150">При следующем вызове к `ConfigureKestrel` переопределяется значение по умолчанию [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize), равное 30 000 000 байтов, установленное при настройке Kestrel методом `CreateDefaultBuilder`:</span><span class="sxs-lookup"><span data-stu-id="d0948-150">The following call to `ConfigureKestrel` overrides the default [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize) of 30,000,000 bytes established when Kestrel was configured by `CreateDefaultBuilder`:</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureKestrel((context, options) =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
    ```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="d0948-151">Следующий вызов [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) переопределяет значение по умолчанию [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize), равное 30 000 000 байтов, установленное при настройке Kestrel методом `CreateDefaultBuilder`:</span><span class="sxs-lookup"><span data-stu-id="d0948-151">The following call to [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) overrides the default [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize) of 30,000,000 bytes established when Kestrel was configured by `CreateDefaultBuilder`:</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .UseKestrel(options =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
    ```

::: moniker-end

<span data-ttu-id="d0948-152">*Корень содержимого* определяет, где узел ищет файлы содержимого, например файлы представлений MVC.</span><span class="sxs-lookup"><span data-stu-id="d0948-152">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="d0948-153">При запуске приложения из корневой папки проекта эта папка используется в качестве корня содержимого.</span><span class="sxs-lookup"><span data-stu-id="d0948-153">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="d0948-154">Такое поведение по умолчанию принято в [Visual Studio](https://www.visualstudio.com/) и [шаблонах dotnet new](/dotnet/core/tools/dotnet-new).</span><span class="sxs-lookup"><span data-stu-id="d0948-154">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="d0948-155">Дополнительные сведения о конфигурации приложения см. в разделе <xref:fundamentals/configuration/index>.</span><span class="sxs-lookup"><span data-stu-id="d0948-155">For more information on app configuration, see <xref:fundamentals/configuration/index>.</span></span>

> [!NOTE]
> <span data-ttu-id="d0948-156">Помимо использования статического метода `CreateDefaultBuilder`, в ASP.NET Core 2.x поддерживается создание узла на основе [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span><span class="sxs-lookup"><span data-stu-id="d0948-156">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="d0948-157">Дополнительные сведения см. на вкладке со сведениями об ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="d0948-157">For more information, see the ASP.NET Core 1.x tab.</span></span>

<span data-ttu-id="d0948-158">При настройке узла можно предоставить методы [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) и [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1).</span><span class="sxs-lookup"><span data-stu-id="d0948-158">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="d0948-159">Если используется класс `Startup`, в нем должен быть определен метод `Configure`.</span><span class="sxs-lookup"><span data-stu-id="d0948-159">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="d0948-160">Дополнительные сведения см. в разделе <xref:fundamentals/startup>.</span><span class="sxs-lookup"><span data-stu-id="d0948-160">For more information, see <xref:fundamentals/startup>.</span></span> <span data-ttu-id="d0948-161">Несколько вызовов `ConfigureServices` добавляются друг к другу.</span><span class="sxs-lookup"><span data-stu-id="d0948-161">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="d0948-162">При нескольких вызовах `Configure` или `UseStartup` в `WebHostBuilder` предыдущие параметры заменяются.</span><span class="sxs-lookup"><span data-stu-id="d0948-162">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="d0948-163">Значения конфигурации узла</span><span class="sxs-lookup"><span data-stu-id="d0948-163">Host configuration values</span></span>

<span data-ttu-id="d0948-164">Для задания значений конфигурации узла класс [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) поддерживает следующие подходы:</span><span class="sxs-lookup"><span data-stu-id="d0948-164">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="d0948-165">конфигурация построителя узла, которая включает в себя переменные среды в формате `ASPNETCORE_{configurationKey}`,</span><span class="sxs-lookup"><span data-stu-id="d0948-165">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="d0948-166">Например, `ASPNETCORE_ENVIRONMENT`.</span><span class="sxs-lookup"><span data-stu-id="d0948-166">For example, `ASPNETCORE_ENVIRONMENT`.</span></span>
* <span data-ttu-id="d0948-167">Расширения, такие как [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) и [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) (см. раздел [Переопределение конфигурации](#override-configuration)).</span><span class="sxs-lookup"><span data-stu-id="d0948-167">Extensions such as [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) and [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) (see the [Override configuration](#override-configuration) section).</span></span>
* <span data-ttu-id="d0948-168">метод [UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) и связанный ключ.</span><span class="sxs-lookup"><span data-stu-id="d0948-168">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="d0948-169">Значение, задаваемое с помощью `UseSetting`, всегда является строкой независимо от типа.</span><span class="sxs-lookup"><span data-stu-id="d0948-169">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="d0948-170">Хост использует значение, заданное последним.</span><span class="sxs-lookup"><span data-stu-id="d0948-170">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="d0948-171">Дополнительные сведения см. в подразделе [Переопределение конфигурации](#override-configuration) следующего раздела.</span><span class="sxs-lookup"><span data-stu-id="d0948-171">For more information, see [Override configuration](#override-configuration) in the next section.</span></span>

### <a name="application-key-name"></a><span data-ttu-id="d0948-172">Ключ приложения (имя)</span><span class="sxs-lookup"><span data-stu-id="d0948-172">Application Key (Name)</span></span>

<span data-ttu-id="d0948-173">Свойство [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) задается автоматически при вызове [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) или [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) во время создания узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-173">The [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) property is automatically set when [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) or [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) is called during host construction.</span></span> <span data-ttu-id="d0948-174">Значение присваивается имени сборки, содержащей точку входа приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-174">The value is set to the name of the assembly containing the app's entry point.</span></span> <span data-ttu-id="d0948-175">Чтобы явно задать значение, используйте [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey).</span><span class="sxs-lookup"><span data-stu-id="d0948-175">To set the value explicitly, use the [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey):</span></span>

<span data-ttu-id="d0948-176">**Ключ**: applicationName</span><span class="sxs-lookup"><span data-stu-id="d0948-176">**Key**: applicationName</span></span>  
<span data-ttu-id="d0948-177">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-177">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-178">**По умолчанию**: имя сборки, содержащей точку входа приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-178">**Default**: The name of the assembly containing the app's entry point.</span></span>  
<span data-ttu-id="d0948-179">**Задается с помощью**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="d0948-179">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="d0948-180">**Переменная среды**: `ASPNETCORE_APPLICATIONNAME`</span><span class="sxs-lookup"><span data-stu-id="d0948-180">**Environment variable**: `ASPNETCORE_APPLICATIONNAME`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.ApplicationKey, "CustomApplicationName")
```

### <a name="capture-startup-errors"></a><span data-ttu-id="d0948-181">Перехват ошибок при загрузке</span><span class="sxs-lookup"><span data-stu-id="d0948-181">Capture Startup Errors</span></span>

<span data-ttu-id="d0948-182">Этот параметр управляет перехватом ошибок при загрузке.</span><span class="sxs-lookup"><span data-stu-id="d0948-182">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="d0948-183">**Ключ**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="d0948-183">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="d0948-184">**Тип**: *bool* (`true` или `1`)</span><span class="sxs-lookup"><span data-stu-id="d0948-184">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="d0948-185">**По умолчанию**: `false`, если только приложение не работает с сервером Kestrel за службами IIS; в этом случае значение по умолчанию — `true`.</span><span class="sxs-lookup"><span data-stu-id="d0948-185">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="d0948-186">**Задается с помощью**: `CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="d0948-186">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="d0948-187">**Переменная среды**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="d0948-187">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="d0948-188">Если задано значение `false`, ошибки во время запуска приводят к завершению работы узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-188">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="d0948-189">Если задано значение `true`, узел перехватывает исключения во время запуска и пытается запустить сервер.</span><span class="sxs-lookup"><span data-stu-id="d0948-189">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
```

### <a name="content-root"></a><span data-ttu-id="d0948-190">Корень содержимого</span><span class="sxs-lookup"><span data-stu-id="d0948-190">Content Root</span></span>

<span data-ttu-id="d0948-191">Этот параметр определяет то, где ASP.NET Core начинает искать файлы содержимого, например представления MVC.</span><span class="sxs-lookup"><span data-stu-id="d0948-191">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="d0948-192">**Ключ**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="d0948-192">**Key**: contentRoot</span></span>  
<span data-ttu-id="d0948-193">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-193">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-194">**По умолчанию**: папка, в которой находится сборка приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-194">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="d0948-195">**Задается с помощью**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="d0948-195">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="d0948-196">**Переменная среды**: `ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="d0948-196">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="d0948-197">Корень содержимого также используется в качестве базового пути для [корневого каталога документов](#web-root).</span><span class="sxs-lookup"><span data-stu-id="d0948-197">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="d0948-198">Если путь не существует, узел не запускается.</span><span class="sxs-lookup"><span data-stu-id="d0948-198">If the path doesn't exist, the host fails to start.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\<content-root>")
```

### <a name="detailed-errors"></a><span data-ttu-id="d0948-199">Подробные сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="d0948-199">Detailed Errors</span></span>

<span data-ttu-id="d0948-200">Определяет, следует ли перехватывать подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="d0948-200">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="d0948-201">**Ключ**: detailedErrors</span><span class="sxs-lookup"><span data-stu-id="d0948-201">**Key**: detailedErrors</span></span>  
<span data-ttu-id="d0948-202">**Тип**: *bool* (`true` или `1`)</span><span class="sxs-lookup"><span data-stu-id="d0948-202">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="d0948-203">**Значение по умолчанию**: false</span><span class="sxs-lookup"><span data-stu-id="d0948-203">**Default**: false</span></span>  
<span data-ttu-id="d0948-204">**Задается с помощью**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="d0948-204">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="d0948-205">**Переменная среды**: `ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="d0948-205">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="d0948-206">Если этот параметр включен (или если параметр <a href="#environment">Среда</a> имеет значение `Development`), приложение перехватывает подробные исключения.</span><span class="sxs-lookup"><span data-stu-id="d0948-206">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

### <a name="environment"></a><span data-ttu-id="d0948-207">Среда</span><span class="sxs-lookup"><span data-stu-id="d0948-207">Environment</span></span>

<span data-ttu-id="d0948-208">Задает среду приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-208">Sets the app's environment.</span></span>

<span data-ttu-id="d0948-209">**Ключ**: environment</span><span class="sxs-lookup"><span data-stu-id="d0948-209">**Key**: environment</span></span>  
<span data-ttu-id="d0948-210">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-210">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-211">**По умолчанию**: Рабочие</span><span class="sxs-lookup"><span data-stu-id="d0948-211">**Default**: Production</span></span>  
<span data-ttu-id="d0948-212">**Задается с помощью**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="d0948-212">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="d0948-213">**Переменная среды**: `ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="d0948-213">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="d0948-214">В качестве среды можно указать любое значение.</span><span class="sxs-lookup"><span data-stu-id="d0948-214">The environment can be set to any value.</span></span> <span data-ttu-id="d0948-215">В платформе определены значения `Development`, `Staging` и `Production`.</span><span class="sxs-lookup"><span data-stu-id="d0948-215">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="d0948-216">Регистр символов в значениях не учитывается.</span><span class="sxs-lookup"><span data-stu-id="d0948-216">Values aren't case sensitive.</span></span> <span data-ttu-id="d0948-217">По умолчанию значение параметра *Среда* считывается из переменной среды `ASPNETCORE_ENVIRONMENT`.</span><span class="sxs-lookup"><span data-stu-id="d0948-217">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="d0948-218">При использовании [Visual Studio](https://www.visualstudio.com/) переменные среды можно задавать в файле *launchSettings.json*.</span><span class="sxs-lookup"><span data-stu-id="d0948-218">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="d0948-219">Дополнительные сведения см. в разделе <xref:fundamentals/environments>.</span><span class="sxs-lookup"><span data-stu-id="d0948-219">For more information, see <xref:fundamentals/environments>.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment(EnvironmentName.Development)
```

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="d0948-220">Начальные сборки размещения</span><span class="sxs-lookup"><span data-stu-id="d0948-220">Hosting Startup Assemblies</span></span>

<span data-ttu-id="d0948-221">Задает начальные сборки размещения для приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-221">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="d0948-222">**Ключ**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="d0948-222">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="d0948-223">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-223">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-224">**По умолчанию**: Пустая строка</span><span class="sxs-lookup"><span data-stu-id="d0948-224">**Default**: Empty string</span></span>  
<span data-ttu-id="d0948-225">**Задается с помощью**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="d0948-225">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="d0948-226">**Переменная среды**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="d0948-226">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="d0948-227">Разделенная точками с запятой строка начальных сборок размещения, загружаемых при запуске.</span><span class="sxs-lookup"><span data-stu-id="d0948-227">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span>

<span data-ttu-id="d0948-228">Хотя значением по умолчанию этого параметра конфигурации является пустая строка, начальные сборки размещения всегда включают в себя сборку приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-228">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="d0948-229">Если начальные сборки размещения указаны, они добавляются к сборке приложения для загрузки во время построения приложением общих служб при запуске.</span><span class="sxs-lookup"><span data-stu-id="d0948-229">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
```

### <a name="https-port"></a><span data-ttu-id="d0948-230">HTTPS-порт</span><span class="sxs-lookup"><span data-stu-id="d0948-230">HTTPS Port</span></span>

<span data-ttu-id="d0948-231">Задайте порт перенаправления HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0948-231">Set the HTTPS redirect port.</span></span> <span data-ttu-id="d0948-232">Используется при [принудительном применении HTTPS](xref:security/enforcing-ssl).</span><span class="sxs-lookup"><span data-stu-id="d0948-232">Used in [enforcing HTTPS](xref:security/enforcing-ssl).</span></span>

<span data-ttu-id="d0948-233">**Ключ**: https_port **Тип**: *string*
**По умолчанию**: значение по умолчанию не задано.</span><span class="sxs-lookup"><span data-stu-id="d0948-233">**Key**: https_port **Type**: *string*
**Default**: A default value isn't set.</span></span>
<span data-ttu-id="d0948-234">**Задается с помощью**: `UseSetting`
**переменной среды**: `ASPNETCORE_HTTPS_PORT`</span><span class="sxs-lookup"><span data-stu-id="d0948-234">**Set using**: `UseSetting`
**Environment variable**: `ASPNETCORE_HTTPS_PORT`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

### <a name="hosting-startup-exclude-assemblies"></a><span data-ttu-id="d0948-235">Исключаемые начальные сборки размещения</span><span class="sxs-lookup"><span data-stu-id="d0948-235">Hosting Startup Exclude Assemblies</span></span>

<span data-ttu-id="d0948-236">Разделенная точками с запятой строка начальных сборок размещения, которые необходимо исключить при запуске.</span><span class="sxs-lookup"><span data-stu-id="d0948-236">A semicolon-delimited string of hosting startup assemblies to exclude on startup.</span></span>

<span data-ttu-id="d0948-237">**Ключ**: hostingStartupExcludeAssemblies</span><span class="sxs-lookup"><span data-stu-id="d0948-237">**Key**: hostingStartupExcludeAssemblies</span></span>  
<span data-ttu-id="d0948-238">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-238">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-239">**По умолчанию**: Пустая строка</span><span class="sxs-lookup"><span data-stu-id="d0948-239">**Default**: Empty string</span></span>  
<span data-ttu-id="d0948-240">**Задается с помощью**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="d0948-240">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="d0948-241">**Переменная среды**: `ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="d0948-241">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupExcludeAssembliesKey, "assembly1;assembly2")
```

### <a name="prefer-hosting-urls"></a><span data-ttu-id="d0948-242">Предпочитать URL-адреса размещения</span><span class="sxs-lookup"><span data-stu-id="d0948-242">Prefer Hosting URLs</span></span>

<span data-ttu-id="d0948-243">Указывает, должен ли узел ожидать передачи данных по URL-адресам, настроенным с помощью `WebHostBuilder`, вместо настроенных с помощью реализации `IServer`.</span><span class="sxs-lookup"><span data-stu-id="d0948-243">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="d0948-244">**Ключ**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="d0948-244">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="d0948-245">**Тип**: *bool* (`true` или `1`)</span><span class="sxs-lookup"><span data-stu-id="d0948-245">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="d0948-246">**Значение по умолчанию**: true</span><span class="sxs-lookup"><span data-stu-id="d0948-246">**Default**: true</span></span>  
<span data-ttu-id="d0948-247">**Задается с помощью**: `PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="d0948-247">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="d0948-248">**Переменная среды**: `ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="d0948-248">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
```

### <a name="prevent-hosting-startup"></a><span data-ttu-id="d0948-249">Запретить запуск размещения</span><span class="sxs-lookup"><span data-stu-id="d0948-249">Prevent Hosting Startup</span></span>

<span data-ttu-id="d0948-250">Запрещает автоматическую загрузку начальных сборок размещения, включая начальные сборки размещения, настроенные сборкой приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-250">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="d0948-251">Дополнительные сведения см. в разделе <xref:fundamentals/configuration/platform-specific-configuration>.</span><span class="sxs-lookup"><span data-stu-id="d0948-251">For more information, see <xref:fundamentals/configuration/platform-specific-configuration>.</span></span>

<span data-ttu-id="d0948-252">**Ключ**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="d0948-252">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="d0948-253">**Тип**: *bool* (`true` или `1`)</span><span class="sxs-lookup"><span data-stu-id="d0948-253">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="d0948-254">**Значение по умолчанию**: false</span><span class="sxs-lookup"><span data-stu-id="d0948-254">**Default**: false</span></span>  
<span data-ttu-id="d0948-255">**Задается с помощью**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="d0948-255">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="d0948-256">**Переменная среды**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="d0948-256">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
```

### <a name="server-urls"></a><span data-ttu-id="d0948-257">URL-адреса сервера</span><span class="sxs-lookup"><span data-stu-id="d0948-257">Server URLs</span></span>

<span data-ttu-id="d0948-258">Задает IP-адреса или адреса узлов с портами и протоколами, по которым сервер должен ожидать получения запросов.</span><span class="sxs-lookup"><span data-stu-id="d0948-258">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="d0948-259">**Ключ**: urls</span><span class="sxs-lookup"><span data-stu-id="d0948-259">**Key**: urls</span></span>  
<span data-ttu-id="d0948-260">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-260">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-261">**По умолчанию**: http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="d0948-261">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="d0948-262">**Задается с помощью**: `UseUrls`</span><span class="sxs-lookup"><span data-stu-id="d0948-262">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="d0948-263">**Переменная среды**: `ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="d0948-263">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="d0948-264">Укажите разделенный точками с запятой (;) список префиксов URL-адресов, на которые сервер должен отвечать.</span><span class="sxs-lookup"><span data-stu-id="d0948-264">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="d0948-265">Например, `http://localhost:123`.</span><span class="sxs-lookup"><span data-stu-id="d0948-265">For example, `http://localhost:123`.</span></span> <span data-ttu-id="d0948-266">Используйте символ "\*", чтобы указать, что сервер должен ожидать получения запросов через определенный порт и по определенному протоколу по любому IP-адресу или имени узла (например, `http://*:5000`).</span><span class="sxs-lookup"><span data-stu-id="d0948-266">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="d0948-267">Протокол (`http://` или `https://`) должен указываться для каждого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d0948-267">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="d0948-268">Поддерживаемые форматы зависят от сервера.</span><span class="sxs-lookup"><span data-stu-id="d0948-268">Supported formats vary among servers.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

<span data-ttu-id="d0948-269">Kestrel имеет собственный интерфейс API настройки конечных точек.</span><span class="sxs-lookup"><span data-stu-id="d0948-269">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="d0948-270">Дополнительные сведения см. в разделе <xref:fundamentals/servers/kestrel#endpoint-configuration>.</span><span class="sxs-lookup"><span data-stu-id="d0948-270">For more information, see <xref:fundamentals/servers/kestrel#endpoint-configuration>.</span></span>

### <a name="shutdown-timeout"></a><span data-ttu-id="d0948-271">Время ожидания завершения работы</span><span class="sxs-lookup"><span data-stu-id="d0948-271">Shutdown Timeout</span></span>

<span data-ttu-id="d0948-272">Определяет, как долго необходимо ожидать завершения работы веб-узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-272">Specifies the amount of time to wait for Web Host to shut down.</span></span>

<span data-ttu-id="d0948-273">**Ключ**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="d0948-273">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="d0948-274">**Тип**: *int*</span><span class="sxs-lookup"><span data-stu-id="d0948-274">**Type**: *int*</span></span>  
<span data-ttu-id="d0948-275">**По умолчанию**: 5</span><span class="sxs-lookup"><span data-stu-id="d0948-275">**Default**: 5</span></span>  
<span data-ttu-id="d0948-276">**Задается с помощью**: `UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="d0948-276">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="d0948-277">**Переменная среды**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="d0948-277">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="d0948-278">Хотя ключ принимает значение *int* с `UseSetting` (например, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), метод расширения [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) принимает [TimeSpan](/dotnet/api/system.timespan).</span><span class="sxs-lookup"><span data-stu-id="d0948-278">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) extension method takes a [TimeSpan](/dotnet/api/system.timespan).</span></span>

<span data-ttu-id="d0948-279">Во время ожидания размещение:</span><span class="sxs-lookup"><span data-stu-id="d0948-279">During the timeout period, hosting:</span></span>

* <span data-ttu-id="d0948-280">Активирует [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span><span class="sxs-lookup"><span data-stu-id="d0948-280">Triggers [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span></span>
* <span data-ttu-id="d0948-281">Пытается остановить размещенные службы, записывая в журнал все ошибки для служб, которые не удалось остановить.</span><span class="sxs-lookup"><span data-stu-id="d0948-281">Attempts to stop hosted services, logging any errors for services that fail to stop.</span></span>

<span data-ttu-id="d0948-282">Если время ожидания истекает до остановки всех размещенных служб, активные службы останавливаются при завершении работы приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-282">If the timeout period expires before all of the hosted services stop, any remaining active services are stopped when the app shuts down.</span></span> <span data-ttu-id="d0948-283">Службы останавливаются даже в том случае, если еще не завершили обработку.</span><span class="sxs-lookup"><span data-stu-id="d0948-283">The services stop even if they haven't finished processing.</span></span> <span data-ttu-id="d0948-284">Если службе требуется дополнительное время для остановки, увеличьте время ожидания.</span><span class="sxs-lookup"><span data-stu-id="d0948-284">If services require additional time to stop, increase the timeout.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
```

### <a name="startup-assembly"></a><span data-ttu-id="d0948-285">Стартовая сборка</span><span class="sxs-lookup"><span data-stu-id="d0948-285">Startup Assembly</span></span>

<span data-ttu-id="d0948-286">Определяет сборку, в которой необходимо искать класс `Startup`.</span><span class="sxs-lookup"><span data-stu-id="d0948-286">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="d0948-287">**Ключ**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="d0948-287">**Key**: startupAssembly</span></span>  
<span data-ttu-id="d0948-288">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-288">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-289">**По умолчанию**: сборка приложения</span><span class="sxs-lookup"><span data-stu-id="d0948-289">**Default**: The app's assembly</span></span>  
<span data-ttu-id="d0948-290">**Задается с помощью**: `UseStartup`</span><span class="sxs-lookup"><span data-stu-id="d0948-290">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="d0948-291">**Переменная среды**: `ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="d0948-291">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="d0948-292">На сборку можно ссылаться по имени (`string`) или типу (`TStartup`).</span><span class="sxs-lookup"><span data-stu-id="d0948-292">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="d0948-293">При вызове нескольких методов `UseStartup` приоритет имеет последний.</span><span class="sxs-lookup"><span data-stu-id="d0948-293">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
```

### <a name="web-root"></a><span data-ttu-id="d0948-294">Корневой каталог документов</span><span class="sxs-lookup"><span data-stu-id="d0948-294">Web Root</span></span>

<span data-ttu-id="d0948-295">Задает относительный путь к статическим ресурсам приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-295">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="d0948-296">**Ключ**: webroot</span><span class="sxs-lookup"><span data-stu-id="d0948-296">**Key**: webroot</span></span>  
<span data-ttu-id="d0948-297">**Тип**: *string*</span><span class="sxs-lookup"><span data-stu-id="d0948-297">**Type**: *string*</span></span>  
<span data-ttu-id="d0948-298">**По умолчанию**: если значение не задано, по умолчанию используется путь "(Корень содержимого)/wwwroot" при его наличии.</span><span class="sxs-lookup"><span data-stu-id="d0948-298">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="d0948-299">Если этот путь не существует, используется фиктивный поставщик файлов.</span><span class="sxs-lookup"><span data-stu-id="d0948-299">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="d0948-300">**Задается с помощью**: `UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="d0948-300">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="d0948-301">**Переменная среды**: `ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="d0948-301">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
```

## <a name="override-configuration"></a><span data-ttu-id="d0948-302">Переопределение конфигурации</span><span class="sxs-lookup"><span data-stu-id="d0948-302">Override configuration</span></span>

<span data-ttu-id="d0948-303">Используйте [конфигурацию](xref:fundamentals/configuration/index) для настройки веб-узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-303">Use [Configuration](xref:fundamentals/configuration/index) to configure Web Host.</span></span> <span data-ttu-id="d0948-304">В приведенном ниже примере необязательная конфигурация узла задается в файле *hostsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="d0948-304">In the following example, host configuration is optionally specified in a *hostsettings.json* file.</span></span> <span data-ttu-id="d0948-305">Любую конфигурацию, загружаемую из файла *hostsettings.json*, можно переопределить с помощью аргументов командной строки.</span><span class="sxs-lookup"><span data-stu-id="d0948-305">Any configuration loaded from the *hostsettings.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="d0948-306">Встроенная конфигурация (в `config`) используется для настройки узла с помощью [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration).</span><span class="sxs-lookup"><span data-stu-id="d0948-306">The built configuration (in `config`) is used to configure the host with [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration).</span></span> <span data-ttu-id="d0948-307">Конфигурация `IWebHostBuilder` добавляется в конфигурацию приложения, но не наоборот &mdash; `ConfigureAppConfiguration` не влияет на конфигурацию `IWebHostBuilder`.</span><span class="sxs-lookup"><span data-stu-id="d0948-307">`IWebHostBuilder` configuration is added to the app's configuration, but the converse isn't true&mdash;`ConfigureAppConfiguration` doesn't affect the `IWebHostBuilder` configuration.</span></span>

<span data-ttu-id="d0948-308">Конфигурация, предоставленная методом `UseUrls`, сначала переопределяется конфигурацией из файла *hostsettings.json*, а затем с помощью аргументов командной строки:</span><span class="sxs-lookup"><span data-stu-id="d0948-308">Overriding the configuration provided by `UseUrls` with *hostsettings.json* config first, command-line argument config second:</span></span>

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

<span data-ttu-id="d0948-309">*hostsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="d0948-309">*hostsettings.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

> [!NOTE]
> <span data-ttu-id="d0948-310">Метод расширения [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) в настоящее время не может анализировать раздел конфигурации, возвращаемый методом `GetSection` (например, `.UseConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="d0948-310">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="d0948-311">Метод `GetSection` фильтрует ключи конфигурации до запрошенного раздела, но оставляет имя раздела в ключах (например, `section:urls`, `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="d0948-311">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="d0948-312">Метод `UseConfiguration` ожидает, что ключи соответствуют ключам `WebHostBuilder` (например, `urls`, `environment`).</span><span class="sxs-lookup"><span data-stu-id="d0948-312">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="d0948-313">Наличие имени раздела в ключах предотвращает настройку узла с помощью значений этого раздела.</span><span class="sxs-lookup"><span data-stu-id="d0948-313">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="d0948-314">Эта проблема будет устранена в следующем выпуске.</span><span class="sxs-lookup"><span data-stu-id="d0948-314">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="d0948-315">Дополнительные сведения и способы решения см. в описании проблемы [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839) (При передаче раздела конфигурации в WebHostBuilder.UseConfiguration используются полные ключи).</span><span class="sxs-lookup"><span data-stu-id="d0948-315">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>
>
> <span data-ttu-id="d0948-316">`UseConfiguration` копирует ключи только из предоставленного объекта `IConfiguration` для конфигурации конструктора узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-316">`UseConfiguration` only copies keys from the provided `IConfiguration` to the host builder configuration.</span></span> <span data-ttu-id="d0948-317">Поэтому указание `reloadOnChange: true` для файлов JSON, XML и INI ни на что не влияет.</span><span class="sxs-lookup"><span data-stu-id="d0948-317">Therefore, setting `reloadOnChange: true` for JSON, INI, and XML settings files has no effect.</span></span>

<span data-ttu-id="d0948-318">Чтобы указать узел, выполняющийся по определенному URL-адресу, можно передать нужное значение из командной строки при выполнении команды [dotnet run](/dotnet/core/tools/dotnet-run).</span><span class="sxs-lookup"><span data-stu-id="d0948-318">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing [dotnet run](/dotnet/core/tools/dotnet-run).</span></span> <span data-ttu-id="d0948-319">Аргумент командной строки переопределяет значение `urls` из файла *hostsettings.json*, и сервер будет ожидать передачи данных через порт 8080:</span><span class="sxs-lookup"><span data-stu-id="d0948-319">The command-line argument overrides the `urls` value from the *hostsettings.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="manage-the-host"></a><span data-ttu-id="d0948-320">Управление узлом</span><span class="sxs-lookup"><span data-stu-id="d0948-320">Manage the host</span></span>

<span data-ttu-id="d0948-321">**Выполнить**</span><span class="sxs-lookup"><span data-stu-id="d0948-321">**Run**</span></span>

<span data-ttu-id="d0948-322">Метод `Run` запускает веб-приложение и блокирует вызывающий поток до тех пор, пока работа узла не будет завершена.</span><span class="sxs-lookup"><span data-stu-id="d0948-322">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="d0948-323">**Запуск**</span><span class="sxs-lookup"><span data-stu-id="d0948-323">**Start**</span></span>

<span data-ttu-id="d0948-324">Чтобы запустить узел без блокировки, вызовите метод `Start`.</span><span class="sxs-lookup"><span data-stu-id="d0948-324">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="d0948-325">Если в метод `Start` передается список URL-адресов, он будет ожидать передачи данных по указанным URL-адресам.</span><span class="sxs-lookup"><span data-stu-id="d0948-325">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="d0948-326">Приложение может инициализировать и запустить новый узел с использованием предварительно настроенных значений по умолчанию `CreateDefaultBuilder` с помощью статического удобного метода.</span><span class="sxs-lookup"><span data-stu-id="d0948-326">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="d0948-327">Эти методы запускают сервер без вывода данных в консоль и со временем ожидания прерывания, равным [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) (Ctrl-C/SIGINT или SIGTERM):</span><span class="sxs-lookup"><span data-stu-id="d0948-327">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="d0948-328">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="d0948-328">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="d0948-329">Выполните запуск с помощью `RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="d0948-329">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="d0948-330">В браузере выполните запрос по адресу `http://localhost:5000`, чтобы получить ответ "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="d0948-330">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="d0948-331">`WaitForShutdown` блокируется, пока не будет создано прерывание (Ctrl-C/SIGINT или SIGTERM).</span><span class="sxs-lookup"><span data-stu-id="d0948-331">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="d0948-332">Приложение выводит сообщение `Console.WriteLine` и ожидает нажатия клавиши, после чего завершает работу.</span><span class="sxs-lookup"><span data-stu-id="d0948-332">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="d0948-333">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="d0948-333">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="d0948-334">Выполните запуск с помощью URL-адреса и `RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="d0948-334">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="d0948-335">Результат будет тем же, что и при использовании **Start(RequestDelegate app)**, но приложение отвечает по адресу `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="d0948-335">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="d0948-336">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="d0948-336">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="d0948-337">Используйте экземпляр `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) для применения ПО промежуточного слоя маршрутизации:</span><span class="sxs-lookup"><span data-stu-id="d0948-337">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="d0948-338">В этом примере используйте следующие запросы в браузере:</span><span class="sxs-lookup"><span data-stu-id="d0948-338">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="d0948-339">Запрос</span><span class="sxs-lookup"><span data-stu-id="d0948-339">Request</span></span>                                    | <span data-ttu-id="d0948-340">Ответ</span><span class="sxs-lookup"><span data-stu-id="d0948-340">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="d0948-341">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="d0948-341">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="d0948-342">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="d0948-342">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="d0948-343">Вызывает исключение со строкой "ooops!"</span><span class="sxs-lookup"><span data-stu-id="d0948-343">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="d0948-344">Вызывает исключение со строкой "Uh oh!"</span><span class="sxs-lookup"><span data-stu-id="d0948-344">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="d0948-345">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="d0948-345">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="d0948-346">Пример "Здравствуй,</span><span class="sxs-lookup"><span data-stu-id="d0948-346">Hello World!</span></span>                             |

<span data-ttu-id="d0948-347">`WaitForShutdown` блокируется, пока не будет создано прерывание (Ctrl-C/SIGINT или SIGTERM).</span><span class="sxs-lookup"><span data-stu-id="d0948-347">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="d0948-348">Приложение выводит сообщение `Console.WriteLine` и ожидает нажатия клавиши, после чего завершает работу.</span><span class="sxs-lookup"><span data-stu-id="d0948-348">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="d0948-349">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="d0948-349">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="d0948-350">Используйте URL-адрес и экземпляр `IRouteBuilder`:</span><span class="sxs-lookup"><span data-stu-id="d0948-350">Use a URL and an instance of `IRouteBuilder`:</span></span>

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

<span data-ttu-id="d0948-351">Результат будет тем же, что и при использовании **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, но приложение будет отвечать по адресу `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="d0948-351">Produces the same result as **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="d0948-352">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="d0948-352">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="d0948-353">Предоставьте делегат для настройки `IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="d0948-353">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="d0948-354">В браузере выполните запрос по адресу `http://localhost:5000`, чтобы получить ответ "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="d0948-354">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="d0948-355">`WaitForShutdown` блокируется, пока не будет создано прерывание (Ctrl-C/SIGINT или SIGTERM).</span><span class="sxs-lookup"><span data-stu-id="d0948-355">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="d0948-356">Приложение выводит сообщение `Console.WriteLine` и ожидает нажатия клавиши, после чего завершает работу.</span><span class="sxs-lookup"><span data-stu-id="d0948-356">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="d0948-357">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="d0948-357">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="d0948-358">Предоставьте URL-адрес и делегат для настройки `IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="d0948-358">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="d0948-359">Результат будет тем же, что и при использовании **StartWith(Action&lt;IApplicationBuilder&gt; app)**, но приложение будет отвечать по адресу `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="d0948-359">Produces the same result as **StartWith(Action&lt;IApplicationBuilder&gt; app)**, except the app responds on `http://localhost:8080`.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="d0948-360">Интерфейс IHostingEnvironment</span><span class="sxs-lookup"><span data-stu-id="d0948-360">IHostingEnvironment interface</span></span>

<span data-ttu-id="d0948-361">[Интерфейс IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) предоставляет сведения о среде веб-размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-361">The [IHostingEnvironment interface](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="d0948-362">Чтобы получить интерфейс `IHostingEnvironment` для использования его свойств и методов расширения, воспользуйтесь [внедрением конструктора](xref:fundamentals/dependency-injection):</span><span class="sxs-lookup"><span data-stu-id="d0948-362">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="d0948-363">Для настройки приложения при запуске в соответствии со средой можно применять [подход на основе соглашения](xref:fundamentals/environments#environment-based-startup-class-and-methods).</span><span class="sxs-lookup"><span data-stu-id="d0948-363">A [convention-based approach](xref:fundamentals/environments#environment-based-startup-class-and-methods) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="d0948-364">Кроме того, можно внедрить интерфейс `IHostingEnvironment` в конструктор `Startup` для использования в `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="d0948-364">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="d0948-365">Помимо метода расширения `IsDevelopment`, интерфейс `IHostingEnvironment` предоставляет методы `IsStaging`, `IsProduction` и `IsEnvironment(string environmentName)`.</span><span class="sxs-lookup"><span data-stu-id="d0948-365">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="d0948-366">Дополнительные сведения см. в разделе <xref:fundamentals/environments>.</span><span class="sxs-lookup"><span data-stu-id="d0948-366">For more information, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="d0948-367">Службу `IHostingEnvironment` также можно внедрять непосредственно в метод `Configure` для настройки конвейера обработки:</span><span class="sxs-lookup"><span data-stu-id="d0948-367">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="d0948-368">`IHostingEnvironment` можно внедрить в метод `Invoke` при создании пользовательского [ПО промежуточного слоя](xref:fundamentals/middleware/write):</span><span class="sxs-lookup"><span data-stu-id="d0948-368">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/write):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="d0948-369">Интерфейс IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="d0948-369">IApplicationLifetime interface</span></span>

<span data-ttu-id="d0948-370">[Интерфейс IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) позволяет выполнять действия после запуска и завершения работы.</span><span class="sxs-lookup"><span data-stu-id="d0948-370">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="d0948-371">Три свойства этого интерфейса представляют собой токены отмены, которые служат для регистрации методов `Action`, определяющих события запуска и завершения работы.</span><span class="sxs-lookup"><span data-stu-id="d0948-371">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="d0948-372">Токен отмены</span><span class="sxs-lookup"><span data-stu-id="d0948-372">Cancellation Token</span></span>    | <span data-ttu-id="d0948-373">Условие инициации&#8230;</span><span class="sxs-lookup"><span data-stu-id="d0948-373">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| [<span data-ttu-id="d0948-374">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="d0948-374">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="d0948-375">Узел полностью запущен.</span><span class="sxs-lookup"><span data-stu-id="d0948-375">The host has fully started.</span></span> |
| [<span data-ttu-id="d0948-376">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="d0948-376">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="d0948-377">Заканчивается нормальное завершение работы узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-377">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="d0948-378">Все запросы должны быть обработаны.</span><span class="sxs-lookup"><span data-stu-id="d0948-378">All requests should be processed.</span></span> <span data-ttu-id="d0948-379">Завершение работы блокируется до тех пор, пока это событие не завершится.</span><span class="sxs-lookup"><span data-stu-id="d0948-379">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="d0948-380">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="d0948-380">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="d0948-381">Происходит нормальное завершение работы узла.</span><span class="sxs-lookup"><span data-stu-id="d0948-381">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="d0948-382">Запросы могут все еще обрабатываться.</span><span class="sxs-lookup"><span data-stu-id="d0948-382">Requests may still be processing.</span></span> <span data-ttu-id="d0948-383">Завершение работы блокируется до тех пор, пока это событие не завершится.</span><span class="sxs-lookup"><span data-stu-id="d0948-383">Shutdown blocks until this event completes.</span></span> |

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

<span data-ttu-id="d0948-384">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) запрашивает остановку приложения.</span><span class="sxs-lookup"><span data-stu-id="d0948-384">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="d0948-385">Следующий класс использует `StopApplication` для корректного завершения работы приложения при вызове метода класса `Shutdown`:</span><span class="sxs-lookup"><span data-stu-id="d0948-385">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="scope-validation"></a><span data-ttu-id="d0948-386">Проверка области</span><span class="sxs-lookup"><span data-stu-id="d0948-386">Scope validation</span></span>

<span data-ttu-id="d0948-387">[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) устанавливает для [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) значение `true`, если приложение находится в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="d0948-387">[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span>

<span data-ttu-id="d0948-388">Если для `ValidateScopes` установлено значение `true`, поставщик службы по умолчанию проверяет, что:</span><span class="sxs-lookup"><span data-stu-id="d0948-388">When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="d0948-389">Службы с заданной областью не разрешаются из корневого поставщика службы, прямо или косвенно.</span><span class="sxs-lookup"><span data-stu-id="d0948-389">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="d0948-390">Службы с заданной областью не вводятся в одноэлементные объекты, прямо или косвенно.</span><span class="sxs-lookup"><span data-stu-id="d0948-390">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="d0948-391">Корневой поставщик службы создается при вызове [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider).</span><span class="sxs-lookup"><span data-stu-id="d0948-391">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="d0948-392">Время существования корневого поставщика службы соответствует времени существования приложения или сервера — поставщик запускается с приложением и удаляется, когда приложение завершает работу.</span><span class="sxs-lookup"><span data-stu-id="d0948-392">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="d0948-393">Службы с заданной областью удаляются создавшим их контейнером.</span><span class="sxs-lookup"><span data-stu-id="d0948-393">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="d0948-394">Если служба с заданной областью создается в корневом контейнере, время существования службы повышается до уровня одноэлементного объекта, поскольку она удаляется только корневым контейнером при завершении работы приложения или сервера.</span><span class="sxs-lookup"><span data-stu-id="d0948-394">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="d0948-395">Проверка областей службы перехватывает эти ситуации при вызове `BuildServiceProvider`.</span><span class="sxs-lookup"><span data-stu-id="d0948-395">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="d0948-396">Чтобы всегда проверять области, в том числе в рабочей среде, настройте [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) с [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) в конструкторе узлов:</span><span class="sxs-lookup"><span data-stu-id="d0948-396">To always validate scopes, including in the Production environment, configure the [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) with [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) on the host builder:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="additional-resources"></a><span data-ttu-id="d0948-397">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d0948-397">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <xref:host-and-deploy/windows-service>
