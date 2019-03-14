---
title: Размещение ASP.NET Core в службе Windows
author: guardrex
description: Узнайте, как разместить приложение ASP.NET Core в службе Windows.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/windows-service
ms.openlocfilehash: 081a631c9c3e74c01e15f4b0b272d650c162bd20
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031291"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="9cf81-103">Размещение ASP.NET Core в службе Windows</span><span class="sxs-lookup"><span data-stu-id="9cf81-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="9cf81-104">Авторы: [Люк Латэм](https://github.com/guardrex) (Luke Latham) и [Tom Dykstra](https://github.com/tdykstra) (Том Дайкстра)</span><span class="sxs-lookup"><span data-stu-id="9cf81-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="9cf81-105">Приложение ASP.NET Core можно разместить в Windows в качестве [службы Windows](/dotnet/framework/windows-services/introduction-to-windows-service-applications) без использования IIS.</span><span class="sxs-lookup"><span data-stu-id="9cf81-105">An ASP.NET Core app can be hosted on Windows as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications) without using IIS.</span></span> <span data-ttu-id="9cf81-106">При размещении в качестве службы Windows приложение автоматически запускается после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="9cf81-106">When hosted as a Windows Service, the app automatically starts after reboots.</span></span>

<span data-ttu-id="9cf81-107">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9cf81-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="deployment-type"></a><span data-ttu-id="9cf81-108">Тип развертывания</span><span class="sxs-lookup"><span data-stu-id="9cf81-108">Deployment type</span></span>

<span data-ttu-id="9cf81-109">Вы можете создать зависящее от платформы или автономное развертывание службы Windows.</span><span class="sxs-lookup"><span data-stu-id="9cf81-109">You can create either a framework-dependent or self-contained Windows Service deployment.</span></span> <span data-ttu-id="9cf81-110">Дополнительные сведения и рекомендации по сценариям развертывания см. в статье [Развертывание приложений .NET Core](/dotnet/core/deploying/).</span><span class="sxs-lookup"><span data-stu-id="9cf81-110">For information and advice on deployment scenarios, see [.NET Core application deployment](/dotnet/core/deploying/).</span></span>

### <a name="framework-dependent-deployment"></a><span data-ttu-id="9cf81-111">развертывание, зависящее от платформы;</span><span class="sxs-lookup"><span data-stu-id="9cf81-111">Framework-dependent deployment</span></span>

<span data-ttu-id="9cf81-112">Зависящее от платформы развертывание (FDD) требует наличия в целевой системе общей для всей системы версии .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9cf81-112">Framework-dependent deployment (FDD) relies on the presence of a shared system-wide version of .NET Core on the target system.</span></span> <span data-ttu-id="9cf81-113">При использовании сценария с FDD с приложением ASP.NET Core (службой Windows) с помощью пакета SDK создается исполняемый файл (*\*.exe*), который называется *исполняемым файлом, зависящим от платформы*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-113">When the FDD scenario is used with an ASP.NET Core Windows Service app, the SDK produces an executable (*\*.exe*), called a *framework-dependent executable*.</span></span>

### <a name="self-contained-deployment"></a><span data-ttu-id="9cf81-114">автономное развертывание;</span><span class="sxs-lookup"><span data-stu-id="9cf81-114">Self-contained deployment</span></span>

<span data-ttu-id="9cf81-115">Для автономного развертывания (SCD) общие компоненты в целевой системе не требуются.</span><span class="sxs-lookup"><span data-stu-id="9cf81-115">Self-contained deployment (SCD) doesn't rely on the presence of shared components on the target system.</span></span> <span data-ttu-id="9cf81-116">Среда выполнения и зависимости приложения развертываются с приложением в системе для размещения.</span><span class="sxs-lookup"><span data-stu-id="9cf81-116">The runtime and the app's dependencies are deployed with the app to the hosting system.</span></span>

## <a name="convert-a-project-into-a-windows-service"></a><span data-ttu-id="9cf81-117">Преобразование проекта в службу Windows</span><span class="sxs-lookup"><span data-stu-id="9cf81-117">Convert a project into a Windows Service</span></span>

<span data-ttu-id="9cf81-118">Внесите следующие изменения в существующий проект ASP.NET Core, чтобы запустить приложение в качестве службы:</span><span class="sxs-lookup"><span data-stu-id="9cf81-118">Make the following changes to an existing ASP.NET Core project to run the app as a service:</span></span>

### <a name="project-file-updates"></a><span data-ttu-id="9cf81-119">Обновления файла проекта</span><span class="sxs-lookup"><span data-stu-id="9cf81-119">Project file updates</span></span>

<span data-ttu-id="9cf81-120">Измените файл проекта с учетом выбранного [типа развертывания](#deployment-type).</span><span class="sxs-lookup"><span data-stu-id="9cf81-120">Based on your choice of [deployment type](#deployment-type), update the project file:</span></span>

#### <a name="framework-dependent-deployment-fdd"></a><span data-ttu-id="9cf81-121">Зависящее от платформы развертывание</span><span class="sxs-lookup"><span data-stu-id="9cf81-121">Framework-dependent Deployment (FDD)</span></span>

<span data-ttu-id="9cf81-122">Добавьте [идентификатор среды выполнения](/dotnet/core/rid-catalog) Windows в `<PropertyGroup>`, где содержится требуемая версия платформы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-122">Add a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) to the `<PropertyGroup>` that contains the target framework.</span></span> <span data-ttu-id="9cf81-123">В следующем примере для RID задано значение `win7-x64`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-123">In the following example, the RID is set to `win7-x64`.</span></span> <span data-ttu-id="9cf81-124">Добавьте свойство `<SelfContained>` со значением `false`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-124">Add the `<SelfContained>` property set to `false`.</span></span> <span data-ttu-id="9cf81-125">Эти свойства дают пакету SDK инструкцию создать исполняемый файл (*EXE*) для Windows.</span><span class="sxs-lookup"><span data-stu-id="9cf81-125">These properties instruct the SDK to generate an executable (*.exe*) file for Windows.</span></span>

<span data-ttu-id="9cf81-126">Файл *web.config*, который обычно создается при публикации приложения ASP.NET Core, не требуется для приложения служб Windows.</span><span class="sxs-lookup"><span data-stu-id="9cf81-126">A *web.config* file, which is normally produced when publishing an ASP.NET Core app, is unnecessary for a Windows Services app.</span></span> <span data-ttu-id="9cf81-127">Отмените создание файла *web.config*, добавив свойство `<IsTransformWebConfigDisabled>` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-127">To disable the creation of the *web.config* file, add the `<IsTransformWebConfigDisabled>` property set to `true`.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="9cf81-128">Добавьте свойство `<UseAppHost>` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-128">Add the `<UseAppHost>` property set to `true`.</span></span> <span data-ttu-id="9cf81-129">Это свойство предоставляет службу с путем активации (исполняемый файл, *EXE*) для FDD.</span><span class="sxs-lookup"><span data-stu-id="9cf81-129">This property provides the service with an activation path (an executable, *.exe*) for an FDD.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.1</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <UseAppHost>true</UseAppHost>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

#### <a name="self-contained-deployment-scd"></a><span data-ttu-id="9cf81-130">Автономное развертывание</span><span class="sxs-lookup"><span data-stu-id="9cf81-130">Self-contained Deployment (SCD)</span></span>

<span data-ttu-id="9cf81-131">Подтвердите наличие [идентификатора среды выполнения](/dotnet/core/rid-catalog) Windows или добавьте его в `<PropertyGroup>`, где содержится требуемая версия платформы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-131">Confirm the presence of a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) or add a RID to the `<PropertyGroup>` that contains the target framework.</span></span> <span data-ttu-id="9cf81-132">Отмените создание файла *web.config*, добавив свойство `<IsTransformWebConfigDisabled>` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-132">Disable the creation of a *web.config* file by adding the `<IsTransformWebConfigDisabled>` property set to `true`.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="9cf81-133">Чтобы выполнить публикацию для нескольких идентификаторов RID, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="9cf81-133">To publish for multiple RIDs:</span></span>

* <span data-ttu-id="9cf81-134">Укажите список идентификаторов RID, разделив их точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="9cf81-134">Provide the RIDs in a semicolon-delimited list.</span></span>
* <span data-ttu-id="9cf81-135">Укажите имя свойства `<RuntimeIdentifiers>` (множественное число).</span><span class="sxs-lookup"><span data-stu-id="9cf81-135">Use the property name `<RuntimeIdentifiers>` (plural).</span></span>

  <span data-ttu-id="9cf81-136">Дополнительные сведения см. в [каталоге RID для .NET Core](/dotnet/core/rid-catalog).</span><span class="sxs-lookup"><span data-stu-id="9cf81-136">For more information, see [.NET Core RID Catalog](/dotnet/core/rid-catalog).</span></span>

<span data-ttu-id="9cf81-137">Добавьте ссылку на пакет для [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span><span class="sxs-lookup"><span data-stu-id="9cf81-137">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span></span>

<span data-ttu-id="9cf81-138">Чтобы включить ведение журнала событий Windows, добавьте ссылку на пакет для [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog).</span><span class="sxs-lookup"><span data-stu-id="9cf81-138">To enable Windows Event Log logging, add a package reference for [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog).</span></span>

<span data-ttu-id="9cf81-139">Дополнительные сведения см. в разделе [Обработка событий запуска и остановки](#handle-starting-and-stopping-events).</span><span class="sxs-lookup"><span data-stu-id="9cf81-139">For more information, see the [Handle starting and stopping events](#handle-starting-and-stopping-events) section.</span></span>

### <a name="programmain-updates"></a><span data-ttu-id="9cf81-140">Обновления Program.Main</span><span class="sxs-lookup"><span data-stu-id="9cf81-140">Program.Main updates</span></span>

<span data-ttu-id="9cf81-141">Внесите следующие изменения в `Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="9cf81-141">Make the following changes in `Program.Main`:</span></span>

* <span data-ttu-id="9cf81-142">Для тестирования и отладки при работе вне службы добавьте код, чтобы определить, как выполняется приложение: в качестве службы или консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf81-142">To test and debug when running outside of a service, add code to determine if the app is running as a service or a console app.</span></span> <span data-ttu-id="9cf81-143">Проверьте, присоединен ли отладчик или присутствует ли аргумент командной строки `--console`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-143">Inspect if the debugger is attached or a `--console` command-line argument is present.</span></span>

  <span data-ttu-id="9cf81-144">Если одно из условий имеет значение true (приложение выполняется не в качестве службы), вызовите <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> на веб-узле.</span><span class="sxs-lookup"><span data-stu-id="9cf81-144">If either condition is true (the app isn't run as a service), call <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> on the Web Host.</span></span>

  <span data-ttu-id="9cf81-145">Если условия имеют значение false (приложение выполняется в качестве службы), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9cf81-145">If the conditions are false (the app is run as a service):</span></span>

  * <span data-ttu-id="9cf81-146">Вызовите <xref:System.IO.Directory.SetCurrentDirectory*> и используйте путь к расположению для публикации приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf81-146">Call <xref:System.IO.Directory.SetCurrentDirectory*> and use a path to the app's published location.</span></span> <span data-ttu-id="9cf81-147">Не вызывайте <xref:System.IO.Directory.GetCurrentDirectory*> для получения пути, так как при вызове <xref:System.IO.Directory.GetCurrentDirectory*> приложение службы Windows возвращает папку *C:\\WINDOWS\\system32*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-147">Don't call <xref:System.IO.Directory.GetCurrentDirectory*> to obtain the path because a Windows Service app returns the *C:\\WINDOWS\\system32* folder when <xref:System.IO.Directory.GetCurrentDirectory*> is called.</span></span> <span data-ttu-id="9cf81-148">Дополнительные сведения см. в разделе [Текущий каталог и корневой каталог содержимого](#current-directory-and-content-root).</span><span class="sxs-lookup"><span data-stu-id="9cf81-148">For more information, see the [Current directory and content root](#current-directory-and-content-root) section.</span></span>
  * <span data-ttu-id="9cf81-149">Вызовите <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>, чтобы запустить приложение в качестве службы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-149">Call <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> to run the app as a service.</span></span>

  <span data-ttu-id="9cf81-150">Так как для [поставщика конфигурации командной строки](xref:fundamentals/configuration/index#command-line-configuration-provider) требуется пара имя-значение для аргументов командной строки, параметр `--console` удаляется из аргументов, прежде чем <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> получит его.</span><span class="sxs-lookup"><span data-stu-id="9cf81-150">Because the [Command-line Configuration Provider](xref:fundamentals/configuration/index#command-line-configuration-provider) requires name-value pairs for command-line arguments, the `--console` switch is removed from the arguments before <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> receives them.</span></span>

* <span data-ttu-id="9cf81-151">Для записи данных в журнал событий Windows добавьте поставщик EventLog в <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>.</span><span class="sxs-lookup"><span data-stu-id="9cf81-151">To write to the Windows Event Log, add the EventLog provider to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>.</span></span> <span data-ttu-id="9cf81-152">Задайте уровень ведения журнала с помощью ключа `Logging:LogLevel:Default` в файле *appsettings.Production.json*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-152">Set the logging level with the `Logging:LogLevel:Default` key in the *appsettings.Production.json* file.</span></span> <span data-ttu-id="9cf81-153">Для демонстрации и тестирования в файле параметров примера приложения для рабочей среды мы укажем такой уровень ведения журнала: `Information`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-153">For demonstration and testing purposes, the sample app's Production settings file sets the logging level to `Information`.</span></span> <span data-ttu-id="9cf81-154">В рабочей среде обычно присваивается значение `Error`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-154">In production, the value is typically set to `Error`.</span></span> <span data-ttu-id="9cf81-155">Дополнительные сведения см. в разделе <xref:fundamentals/logging/index#windows-eventlog-provider>.</span><span class="sxs-lookup"><span data-stu-id="9cf81-155">For more information, see <xref:fundamentals/logging/index#windows-eventlog-provider>.</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=snippet_Program)]

### <a name="publish-the-app"></a><span data-ttu-id="9cf81-156">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="9cf81-156">Publish the app</span></span>

<span data-ttu-id="9cf81-157">Опубликуйте приложение с помощью команды [dotnet publish](/dotnet/articles/core/tools/dotnet-publish), [профиля публикации Visual Studio](xref:host-and-deploy/visual-studio-publish-profiles) или Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9cf81-157">Publish the app using [dotnet publish](/dotnet/articles/core/tools/dotnet-publish), a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles), or Visual Studio Code.</span></span> <span data-ttu-id="9cf81-158">Если вы используете Visual Studio, выберите **FolderProfile** и настройте **целевое расположение**, прежде чем нажимать кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="9cf81-158">When using Visual Studio, select the **FolderProfile** and configure the **Target Location** before selecting the **Publish** button.</span></span>

<span data-ttu-id="9cf81-159">Чтобы опубликовать пример приложения с помощью интерфейса командной строки (CLI), выполните в командной строке команду [dotnet publish](/dotnet/core/tools/dotnet-publish) в папке проекта с конфигурацией выпуска, передаваемой параметру [-c|--configuration](/dotnet/core/tools/dotnet-publish#options).</span><span class="sxs-lookup"><span data-stu-id="9cf81-159">To publish the sample app using command-line interface (CLI) tools, run the [dotnet publish](/dotnet/core/tools/dotnet-publish) command at a command prompt from the project folder with a Release configuration passed to the [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) option.</span></span> <span data-ttu-id="9cf81-160">Чтобы опубликовать этот пример в папке за пределами приложения, задайте параметр [-o|--output](/dotnet/core/tools/dotnet-publish#options) и укажите путь.</span><span class="sxs-lookup"><span data-stu-id="9cf81-160">Use the [-o|--output](/dotnet/core/tools/dotnet-publish#options) option with a path to publish to a folder outside of the app.</span></span>

#### <a name="publish-a-framework-dependent-deployment-fdd"></a><span data-ttu-id="9cf81-161">Публикация зависящего от платформы развертывания</span><span class="sxs-lookup"><span data-stu-id="9cf81-161">Publish a Framework-dependent Deployment (FDD)</span></span>

<span data-ttu-id="9cf81-162">В следующем примере приложение публикуется в папке *c:\\svc*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-162">In the following example, the app is published to the *c:\\svc* folder:</span></span>

```console
dotnet publish --configuration Release --output c:\svc
```

#### <a name="publish-a-self-contained-deployment-scd"></a><span data-ttu-id="9cf81-163">Публикация автономного развертывания</span><span class="sxs-lookup"><span data-stu-id="9cf81-163">Publish a Self-contained Deployment (SCD)</span></span>

<span data-ttu-id="9cf81-164">Идентификатор RID следует указать в свойстве `<RuntimeIdenfifier>` (или `<RuntimeIdentifiers>`) в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="9cf81-164">The RID must be specified in the `<RuntimeIdenfifier>` (or `<RuntimeIdentifiers>`) property of the project file.</span></span> <span data-ttu-id="9cf81-165">Укажите среду выполнения в параметре [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) команды `dotnet publish`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-165">Supply the runtime to the [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) option of the `dotnet publish` command.</span></span>

<span data-ttu-id="9cf81-166">В следующем примере приложение публикуется для среды выполнения `win7-x64` в папке *c:\\svc*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-166">In the following example, the app is published for the `win7-x64` runtime to the *c:\\svc* folder:</span></span>

```console
dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
```

### <a name="create-a-user-account"></a><span data-ttu-id="9cf81-167">Создание учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="9cf81-167">Create a user account</span></span>

<span data-ttu-id="9cf81-168">Создайте для службы учетную запись пользователя с помощью команды `net user` из административной командной оболочки:</span><span class="sxs-lookup"><span data-stu-id="9cf81-168">Create a user account for the service using the `net user` command from an administrative command shell:</span></span>

```console
net user {USER ACCOUNT} {PASSWORD} /add
```

<span data-ttu-id="9cf81-169">Срок действия пароля по умолчанию составляет шесть недель.</span><span class="sxs-lookup"><span data-stu-id="9cf81-169">The default password expiration is six weeks.</span></span>

<span data-ttu-id="9cf81-170">Для примера приложения создайте учетную запись пользователя с именем `ServiceUser` и пароль.</span><span class="sxs-lookup"><span data-stu-id="9cf81-170">For the sample app, create a user account with the name `ServiceUser` and a password.</span></span> <span data-ttu-id="9cf81-171">В следующей команде замените `{PASSWORD}` на [надежный пароль](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).</span><span class="sxs-lookup"><span data-stu-id="9cf81-171">In the following command, replace `{PASSWORD}` with a [strong password](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).</span></span>

```console
net user ServiceUser {PASSWORD} /add
```

<span data-ttu-id="9cf81-172">Если вам нужно добавить пользователя в группу, используйте команду `net localgroup`, где `{GROUP}` — это имя группы:</span><span class="sxs-lookup"><span data-stu-id="9cf81-172">If you need to add the user to a group, use the `net localgroup` command, where `{GROUP}` is the name of the group:</span></span>

```console
net localgroup {GROUP} {USER ACCOUNT} /add
```

<span data-ttu-id="9cf81-173">Дополнительные сведения см. в статье [Service User Accounts](/windows/desktop/services/service-user-accounts) (Учетные записи пользователей службы).</span><span class="sxs-lookup"><span data-stu-id="9cf81-173">For more information, see [Service User Accounts](/windows/desktop/services/service-user-accounts).</span></span>

<span data-ttu-id="9cf81-174">Альтернативный подход к управлению пользователями при работе с Active Directory заключается в применении управляемых учетных записей служб.</span><span class="sxs-lookup"><span data-stu-id="9cf81-174">An alternative approach to managing users when using Active Directory is to use Managed Service Accounts.</span></span> <span data-ttu-id="9cf81-175">Дополнительные сведения см. в [обзоре групповых управляемых учетных записей службы](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).</span><span class="sxs-lookup"><span data-stu-id="9cf81-175">For more information, see [Group Managed Service Accounts Overview](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).</span></span>

### <a name="set-permissions"></a><span data-ttu-id="9cf81-176">Настройка разрешений</span><span class="sxs-lookup"><span data-stu-id="9cf81-176">Set permissions</span></span>

#### <a name="access-to-the-app-folder"></a><span data-ttu-id="9cf81-177">Доступ к папке приложения</span><span class="sxs-lookup"><span data-stu-id="9cf81-177">Access to the app folder</span></span>

<span data-ttu-id="9cf81-178">Предоставьте доступ на запись, чтение и выполнение к папке приложения с помощью команды [icacls](/windows-server/administration/windows-commands/icacls) из административной командной оболочки:</span><span class="sxs-lookup"><span data-stu-id="9cf81-178">Grant write/read/execute access to the app's folder using the [icacls](/windows-server/administration/windows-commands/icacls) command from an administrative command shell:</span></span>

```console
icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
```

* <span data-ttu-id="9cf81-179">`{PATH}` &ndash; путь к папке приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf81-179">`{PATH}` &ndash; Path to the app's folder.</span></span>
* <span data-ttu-id="9cf81-180">`{USER ACCOUNT}` &ndash; учетная запись пользователя (SID).</span><span class="sxs-lookup"><span data-stu-id="9cf81-180">`{USER ACCOUNT}` &ndash; The user account (SID).</span></span>
* <span data-ttu-id="9cf81-181">`(OI)` &ndash; флаг наследования объекта, который распространяет разрешения на вложенные файлы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-181">`(OI)` &ndash; The Object Inherit flag propagates permissions to subordinate files.</span></span>
* <span data-ttu-id="9cf81-182">`(CI)` &ndash; флаг наследования контейнера, который распространяет разрешения на вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="9cf81-182">`(CI)` &ndash; The Container Inherit flag propagates permissions to subordinate folders.</span></span>
* <span data-ttu-id="9cf81-183">`{PERMISSION FLAGS}` &ndash; устанавливает разрешения для доступа к приложениям.</span><span class="sxs-lookup"><span data-stu-id="9cf81-183">`{PERMISSION FLAGS}` &ndash; Sets the app's access permissions.</span></span>
  * <span data-ttu-id="9cf81-184">Запись (`W`)</span><span class="sxs-lookup"><span data-stu-id="9cf81-184">Write (`W`)</span></span>
  * <span data-ttu-id="9cf81-185">Чтение (`R`)</span><span class="sxs-lookup"><span data-stu-id="9cf81-185">Read (`R`)</span></span>
  * <span data-ttu-id="9cf81-186">Выполнение (`X`)</span><span class="sxs-lookup"><span data-stu-id="9cf81-186">Execute (`X`)</span></span>
  * <span data-ttu-id="9cf81-187">Полное (`F`)</span><span class="sxs-lookup"><span data-stu-id="9cf81-187">Full (`F`)</span></span>
  * <span data-ttu-id="9cf81-188">Изменение (`M`)</span><span class="sxs-lookup"><span data-stu-id="9cf81-188">Modify (`M`)</span></span>
* <span data-ttu-id="9cf81-189">`/t` &ndash; применяется рекурсивно к имеющимся вложенным папкам и файлам.</span><span class="sxs-lookup"><span data-stu-id="9cf81-189">`/t` &ndash; Apply recursively to existing subordinate folders and files.</span></span>

<span data-ttu-id="9cf81-190">Для примера приложения, опубликованного в папке *c:\\svc*, и учетной записи `ServiceUser` с разрешениями на запись, чтение и выполнение используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9cf81-190">For the sample app published to the *c:\\svc* folder and the `ServiceUser` account with write/read/execute permissions, use the following command:</span></span>

```console
icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
```

<span data-ttu-id="9cf81-191">Дополнительные сведения см. в статье об [icacls](/windows-server/administration/windows-commands/icacls).</span><span class="sxs-lookup"><span data-stu-id="9cf81-191">For more information, see [icacls](/windows-server/administration/windows-commands/icacls).</span></span>

#### <a name="log-on-as-a-service"></a><span data-ttu-id="9cf81-192">вход в систему в качестве службы;</span><span class="sxs-lookup"><span data-stu-id="9cf81-192">Log on as a service</span></span>

<span data-ttu-id="9cf81-193">Чтобы предоставить учетной записи пользователя разрешение на [вход в качестве службы](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9cf81-193">To grant the [Log on as a service](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) privilege to the user account:</span></span>

1. <span data-ttu-id="9cf81-194">Найдите политики **назначения прав пользователя** в консоли локальной политики безопасности или в консоли редактора локальных групповых политик.</span><span class="sxs-lookup"><span data-stu-id="9cf81-194">Locate the **User Rights Assignment** policies in either the Local Security Policy console or Local Group Policy Editor console.</span></span> <span data-ttu-id="9cf81-195">Инструкции см. в разделе: [Настройка параметров политики безопасности](/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).</span><span class="sxs-lookup"><span data-stu-id="9cf81-195">For instructions, see: [Configure security policy settings](/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).</span></span>
1. <span data-ttu-id="9cf81-196">Найдите политику `Log on as a service`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-196">Locate the `Log on as a service` policy.</span></span> <span data-ttu-id="9cf81-197">Дважды щелкните имя политики, чтобы открыть ее.</span><span class="sxs-lookup"><span data-stu-id="9cf81-197">Double-click the policy to open it.</span></span>
1. <span data-ttu-id="9cf81-198">Щелкните **Добавить пользователя или группу**.</span><span class="sxs-lookup"><span data-stu-id="9cf81-198">Select **Add User or Group**.</span></span>
1. <span data-ttu-id="9cf81-199">Выберите **Дополнительно**, а затем **Найти**.</span><span class="sxs-lookup"><span data-stu-id="9cf81-199">Select **Advanced** and select **Find Now**.</span></span>
1. <span data-ttu-id="9cf81-200">Выберите учетную запись пользователя, которую вы создали при работе с разделом [Создание учетной записи пользователя](#create-a-user-account).</span><span class="sxs-lookup"><span data-stu-id="9cf81-200">Select the user account created in the [Create a user account](#create-a-user-account) section earlier.</span></span> <span data-ttu-id="9cf81-201">Щелкните **ОК**, чтобы подтвердить выбор.</span><span class="sxs-lookup"><span data-stu-id="9cf81-201">Select **OK** to accept the selection.</span></span>
1. <span data-ttu-id="9cf81-202">Убедитесь, что имя объекта указано правильно, и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9cf81-202">Select **OK** after confirming that the object name is correct.</span></span>
1. <span data-ttu-id="9cf81-203">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="9cf81-203">Select **Apply**.</span></span> <span data-ttu-id="9cf81-204">Щелкните **ОК**, чтобы закрыть окно политики.</span><span class="sxs-lookup"><span data-stu-id="9cf81-204">Select **OK** to close the policy window.</span></span>

## <a name="manage-the-service"></a><span data-ttu-id="9cf81-205">Управление службой</span><span class="sxs-lookup"><span data-stu-id="9cf81-205">Manage the service</span></span>

### <a name="create-the-service"></a><span data-ttu-id="9cf81-206">Создание службы</span><span class="sxs-lookup"><span data-stu-id="9cf81-206">Create the service</span></span>

<span data-ttu-id="9cf81-207">Используйте программу командной строки [sc.exe](https://technet.microsoft.com/library/bb490995), чтобы создать службу из административной командной оболочки.</span><span class="sxs-lookup"><span data-stu-id="9cf81-207">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service from an administrative command shell.</span></span> <span data-ttu-id="9cf81-208">Значение `binPath` обозначает путь к исполняемому файлу приложения, включая имя самого файла.</span><span class="sxs-lookup"><span data-stu-id="9cf81-208">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="9cf81-209">**Требуется пробел между знаком равенства и кавычками для каждого обязательного параметра и значения.**</span><span class="sxs-lookup"><span data-stu-id="9cf81-209">**The space between the equal sign and the quote character of each parameter and value is required.**</span></span>

```console
sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
```

* <span data-ttu-id="9cf81-210">`{SERVICE NAME}` &ndash; имя, присваиваемое службе в [диспетчере служб](/windows/desktop/services/service-control-manager).</span><span class="sxs-lookup"><span data-stu-id="9cf81-210">`{SERVICE NAME}` &ndash; The name to assign to the service in [Service Control Manager](/windows/desktop/services/service-control-manager).</span></span>
* <span data-ttu-id="9cf81-211">`{PATH}` &ndash; путь к исполняемому файлу.</span><span class="sxs-lookup"><span data-stu-id="9cf81-211">`{PATH}` &ndash; The path to the service executable.</span></span>
* <span data-ttu-id="9cf81-212">`{DOMAIN}` &ndash; домен, к которому присоединен компьютер.</span><span class="sxs-lookup"><span data-stu-id="9cf81-212">`{DOMAIN}` &ndash; The domain of a domain-joined machine.</span></span> <span data-ttu-id="9cf81-213">Если компьютер не присоединен к домену, используйте имя локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="9cf81-213">If the machine isn't domain-joined, use the local machine name.</span></span>
* <span data-ttu-id="9cf81-214">`{USER ACCOUNT}` &ndash; учетная запись пользователя, которая используется для запуска службы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-214">`{USER ACCOUNT}` &ndash; The user account under which the service runs.</span></span>
* <span data-ttu-id="9cf81-215">`{PASSWORD}` &ndash; пароль учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="9cf81-215">`{PASSWORD}` &ndash; The user account password.</span></span>

> [!WARNING]
> <span data-ttu-id="9cf81-216">**Не** пропускайте параметр `obj`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-216">Do **not** omit the `obj` parameter.</span></span> <span data-ttu-id="9cf81-217">Значение по умолчанию параметра `obj` — это [учетная запись LocalSystem](/windows/desktop/services/localsystem-account).</span><span class="sxs-lookup"><span data-stu-id="9cf81-217">The default value for `obj` is the [LocalSystem account](/windows/desktop/services/localsystem-account) account.</span></span> <span data-ttu-id="9cf81-218">Выполнение службы под учетной записью `LocalSystem` представляет собой серьезную угрозу безопасности.</span><span class="sxs-lookup"><span data-stu-id="9cf81-218">Running a service under the `LocalSystem` account presents a significant security risk.</span></span> <span data-ttu-id="9cf81-219">Всегда запускайте службу, используя учетную запись пользователя с ограниченными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="9cf81-219">Always run a service with a user account that has restricted privileges.</span></span>

<span data-ttu-id="9cf81-220">В примере ниже для примера приложения указано следующее:</span><span class="sxs-lookup"><span data-stu-id="9cf81-220">In the following example for the sample app:</span></span>

* <span data-ttu-id="9cf81-221">Служба называется **MyService**.</span><span class="sxs-lookup"><span data-stu-id="9cf81-221">The service is named **MyService**.</span></span>
* <span data-ttu-id="9cf81-222">Опубликованная служба размещается в папке *c:\\svc*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-222">The published service resides in the *c:\\svc* folder.</span></span> <span data-ttu-id="9cf81-223">Исполняемый файл приложения с именем *SampleApp.exe*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-223">The app executable is named *SampleApp.exe*.</span></span> <span data-ttu-id="9cf81-224">Значение `binPath` заключается в двойные кавычки (").</span><span class="sxs-lookup"><span data-stu-id="9cf81-224">Enclose the `binPath` value in double quotation marks (").</span></span>
* <span data-ttu-id="9cf81-225">Служба работает под учетной записью `ServiceUser`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-225">The service runs under the `ServiceUser` account.</span></span> <span data-ttu-id="9cf81-226">Замените `{DOMAIN}` на домен учетной записи пользователя или имя локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="9cf81-226">Replace `{DOMAIN}` with the user account's domain or local machine name.</span></span> <span data-ttu-id="9cf81-227">Значение `obj` заключается в двойные кавычки (").</span><span class="sxs-lookup"><span data-stu-id="9cf81-227">Enclose the `obj` value in double quotation marks (").</span></span> <span data-ttu-id="9cf81-228">Пример Если система размещения — это локальный компьютер с именем `MairaPC`, задайте для параметра `obj` значение `"MairaPC\ServiceUser"`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-228">Example: If the hosting system is a local machine named `MairaPC`, set `obj` to `"MairaPC\ServiceUser"`.</span></span>
* <span data-ttu-id="9cf81-229">Замените `{PASSWORD}` на пароль учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="9cf81-229">Replace `{PASSWORD}` with the user account's password.</span></span> <span data-ttu-id="9cf81-230">Значение `password` заключается в двойные кавычки (").</span><span class="sxs-lookup"><span data-stu-id="9cf81-230">Enclose the `password` value in double quotation marks (").</span></span>

```console
sc create MyService binPath= "c:\svc\sampleapp.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
```

> [!IMPORTANT]
> <span data-ttu-id="9cf81-231">Убедитесь, что между знаками равенства и значениями параметров есть пробелы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-231">Make sure that the spaces between the parameters' equal signs and the parameters' values are present.</span></span>

### <a name="start-the-service"></a><span data-ttu-id="9cf81-232">Запуск службы</span><span class="sxs-lookup"><span data-stu-id="9cf81-232">Start the service</span></span>

<span data-ttu-id="9cf81-233">Запустите службу с помощью команды `sc start {SERVICE NAME}`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-233">Start the service with the `sc start {SERVICE NAME}` command.</span></span>

<span data-ttu-id="9cf81-234">Чтобы запустить пример службы приложения, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9cf81-234">To start the sample app service, use the following command:</span></span>

```console
sc start MyService
```

<span data-ttu-id="9cf81-235">Команде потребуется несколько секунд, чтобы запустить службу.</span><span class="sxs-lookup"><span data-stu-id="9cf81-235">The command takes a few seconds to start the service.</span></span>

### <a name="determine-the-service-status"></a><span data-ttu-id="9cf81-236">Определение состояния службы</span><span class="sxs-lookup"><span data-stu-id="9cf81-236">Determine the service status</span></span>

<span data-ttu-id="9cf81-237">Чтобы проверить состояние службы, используйте команду `sc query {SERVICE NAME}`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-237">To check the status of the service, use the `sc query {SERVICE NAME}` command.</span></span> <span data-ttu-id="9cf81-238">Состояние отображается одним из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="9cf81-238">The status is reported as one of the following values:</span></span>

* `START_PENDING`
* `RUNNING`
* `STOP_PENDING`
* `STOPPED`

<span data-ttu-id="9cf81-239">Чтобы проверить состояние примера службы приложения, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9cf81-239">Use the following command to check the status of the sample app service:</span></span>

```console
sc query MyService
```

### <a name="browse-a-web-app-service"></a><span data-ttu-id="9cf81-240">Обзор службы веб-приложений</span><span class="sxs-lookup"><span data-stu-id="9cf81-240">Browse a web app service</span></span>

<span data-ttu-id="9cf81-241">Если служба находится в состоянии `RUNNING` и является веб-приложением, найдите приложение по его пути (по умолчанию `http://localhost:5000`, который перенаправляет на `https://localhost:5001` при использовании [ПО промежуточного слоя перенаправления на HTTPS](xref:security/enforcing-ssl)).</span><span class="sxs-lookup"><span data-stu-id="9cf81-241">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

<span data-ttu-id="9cf81-242">Чтобы получить пример службы приложений, найдите приложение по адресу `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-242">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

### <a name="stop-the-service"></a><span data-ttu-id="9cf81-243">Остановите службу</span><span class="sxs-lookup"><span data-stu-id="9cf81-243">Stop the service</span></span>

<span data-ttu-id="9cf81-244">Остановите службу с помощью команды `sc stop {SERVICE NAME}`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-244">Stop the service with the `sc stop {SERVICE NAME}` command.</span></span>

<span data-ttu-id="9cf81-245">Чтобы остановить пример службы приложения, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9cf81-245">The following command stops the sample app service:</span></span>

```console
sc stop MyService
```

### <a name="delete-the-service"></a><span data-ttu-id="9cf81-246">Удаление службы</span><span class="sxs-lookup"><span data-stu-id="9cf81-246">Delete the service</span></span>

<span data-ttu-id="9cf81-247">После небольшой задержки для остановки службы удалите службу с помощью команды `sc delete {SERVICE NAME}`.</span><span class="sxs-lookup"><span data-stu-id="9cf81-247">After a short delay to stop a service, uninstall the service with the `sc delete {SERVICE NAME}` command.</span></span>

<span data-ttu-id="9cf81-248">Проверьте состояние примера службы приложений:</span><span class="sxs-lookup"><span data-stu-id="9cf81-248">Check the status of the sample app service:</span></span>

```console
sc query MyService
```

<span data-ttu-id="9cf81-249">Когда пример службы приложений находится в состоянии `STOPPED`, используйте следующую команду для удаления примера службы приложений:</span><span class="sxs-lookup"><span data-stu-id="9cf81-249">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

```console
sc delete MyService
```

## <a name="handle-starting-and-stopping-events"></a><span data-ttu-id="9cf81-250">Обработка событий запуска и остановки</span><span class="sxs-lookup"><span data-stu-id="9cf81-250">Handle starting and stopping events</span></span>

<span data-ttu-id="9cf81-251">Чтобы правильно обрабатывать события <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*> и <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*>, внесите дополнительные изменения:</span><span class="sxs-lookup"><span data-stu-id="9cf81-251">To handle <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*>, and <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> events, perform the following additional changes:</span></span>

1. <span data-ttu-id="9cf81-252">Создайте класс, производный от <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService>, с методами `OnStarting`, `OnStarted` и `OnStopping`:</span><span class="sxs-lookup"><span data-stu-id="9cf81-252">Create a class that derives from <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService> with the `OnStarting`, `OnStarted`, and `OnStopping` methods:</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=snippet_CustomWebHostService)]

2. <span data-ttu-id="9cf81-253">Создайте метод расширения для <xref:Microsoft.AspNetCore.Hosting.IWebHost>, который передает `CustomWebHostService` в <xref:System.ServiceProcess.ServiceBase.Run*>:</span><span class="sxs-lookup"><span data-stu-id="9cf81-253">Create an extension method for <xref:Microsoft.AspNetCore.Hosting.IWebHost> that passes the `CustomWebHostService` to <xref:System.ServiceProcess.ServiceBase.Run*>:</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="9cf81-254">В `Program.Main` вызовите метод расширения `RunAsCustomService` вместо <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>:</span><span class="sxs-lookup"><span data-stu-id="9cf81-254">In `Program.Main`, call the `RunAsCustomService` extension method instead of <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>:</span></span>

   ```csharp
   host.RunAsCustomService();
   ```

   <span data-ttu-id="9cf81-255">Чтобы узнать расположение <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> в `Program.Main`, см. пример кода, приведенный в разделе [Преобразование проекта в службу Windows](#convert-a-project-into-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="9cf81-255">To see the location of <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> in `Program.Main`, refer to the code sample shown in the [Convert a project into a Windows Service](#convert-a-project-into-a-windows-service) section.</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="9cf81-256">Сценарии использования прокси-сервера и подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="9cf81-256">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="9cf81-257">Для служб, которые взаимодействуют с запросами из Интернета или корпоративной сети и размещаются за прокси-сервером или подсистемой балансировки нагрузки, может потребоваться дополнительная настройка.</span><span class="sxs-lookup"><span data-stu-id="9cf81-257">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="9cf81-258">Дополнительные сведения см. в разделе <xref:host-and-deploy/proxy-load-balancer>.</span><span class="sxs-lookup"><span data-stu-id="9cf81-258">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="configure-https"></a><span data-ttu-id="9cf81-259">Настройка HTTPS</span><span class="sxs-lookup"><span data-stu-id="9cf81-259">Configure HTTPS</span></span>

<span data-ttu-id="9cf81-260">Чтобы настроить службу с защищенной конечной точкой, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9cf81-260">To configure the service with a secure endpoint:</span></span>

1. <span data-ttu-id="9cf81-261">Создайте сертификат X.509 для системы размещения с помощью механизмов получения и развертывания сертификата вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-261">Create an X.509 certificate for the hosting system using your platform's certificate acquisition and deployment mechanisms.</span></span>

1. <span data-ttu-id="9cf81-262">Укажите [конфигурацию конечной точки HTTPS для сервера Kestrel](xref:fundamentals/servers/kestrel#endpoint-configuration), чтобы использовать сертификат.</span><span class="sxs-lookup"><span data-stu-id="9cf81-262">Specify a [Kestrel server HTTPS endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) to use the certificate.</span></span>

<span data-ttu-id="9cf81-263">Использование сертификата разработки ASP.NET Core HTTPS для защиты конечной точки службы не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9cf81-263">Use of the ASP.NET Core HTTPS development certificate to secure a service endpoint isn't supported.</span></span>

## <a name="current-directory-and-content-root"></a><span data-ttu-id="9cf81-264">Текущий каталог и корневой каталог содержимого</span><span class="sxs-lookup"><span data-stu-id="9cf81-264">Current directory and content root</span></span>

<span data-ttu-id="9cf81-265">Для службы Windows <xref:System.IO.Directory.GetCurrentDirectory*> возвращает текущий рабочий каталог *C:\\WINDOWS\\system32*.</span><span class="sxs-lookup"><span data-stu-id="9cf81-265">The current working directory returned by calling <xref:System.IO.Directory.GetCurrentDirectory*> for a Windows Service is the *C:\\WINDOWS\\system32* folder.</span></span> <span data-ttu-id="9cf81-266">Папка *system32* не подходит для хранения файлов службы (например, файлов параметров).</span><span class="sxs-lookup"><span data-stu-id="9cf81-266">The *system32* folder isn't a suitable location to store a service's files (for example, settings files).</span></span> <span data-ttu-id="9cf81-267">Используйте один из следующих методов для сохранения ресурсов и файлов параметров службы и доступа к ним.</span><span class="sxs-lookup"><span data-stu-id="9cf81-267">Use one of the following approaches to maintain and access a service's assets and settings files.</span></span>

### <a name="set-the-content-root-path-to-the-apps-folder"></a><span data-ttu-id="9cf81-268">Указание папки приложения в качестве пути корневого каталога содержимого</span><span class="sxs-lookup"><span data-stu-id="9cf81-268">Set the content root path to the app's folder</span></span>

<span data-ttu-id="9cf81-269"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*> — это тот же путь, предоставленный аргументом `binPath` при создании службы.</span><span class="sxs-lookup"><span data-stu-id="9cf81-269">The <xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*> is the same path provided to the `binPath` argument when the service is created.</span></span> <span data-ttu-id="9cf81-270">Чтобы не вызывать метод `GetCurrentDirectory` для создания путей к файлам параметров, вызовите <xref:System.IO.Directory.SetCurrentDirectory*> с указанным путем к корневому каталогу содержимого приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf81-270">Instead of calling `GetCurrentDirectory` to create paths to settings files, call <xref:System.IO.Directory.SetCurrentDirectory*> with the path to the app's content root.</span></span>

<span data-ttu-id="9cf81-271">В `Program.Main` определите путь к папке с исполняемым файлом службы и используйте этот путь, чтобы создать корневой каталог содержимого приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf81-271">In `Program.Main`, determine the path to the folder of the service's executable and use the path to establish the app's content root:</span></span>

```csharp
var pathToExe = Process.GetCurrentProcess().MainModule.FileName;
var pathToContentRoot = Path.GetDirectoryName(pathToExe);
Directory.SetCurrentDirectory(pathToContentRoot);

CreateWebHostBuilder(args)
    .Build()
    .RunAsService();
```

### <a name="store-the-services-files-in-a-suitable-location-on-disk"></a><span data-ttu-id="9cf81-272">Хранение файлов службы в подходящем месте на диске</span><span class="sxs-lookup"><span data-stu-id="9cf81-272">Store the service's files in a suitable location on disk</span></span>

<span data-ttu-id="9cf81-273">Укажите абсолютный путь к папке, содержащей файлы, с помощью <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> при использовании <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>.</span><span class="sxs-lookup"><span data-stu-id="9cf81-273">Specify an absolute path with <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> when using an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to the folder containing the files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cf81-274">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9cf81-274">Additional resources</span></span>

* <span data-ttu-id="9cf81-275">[Конфигурация конечных точек Kestrel](xref:fundamentals/servers/kestrel#endpoint-configuration) (включает конфигурацию HTTPS и поддержку SNI)</span><span class="sxs-lookup"><span data-stu-id="9cf81-275">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
* <xref:test/troubleshoot>
