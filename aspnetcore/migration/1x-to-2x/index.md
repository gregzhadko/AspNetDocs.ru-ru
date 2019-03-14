---
title: "Миграция с ASP.NET Core\_1.x на 2.0"
author: scottaddie
description: "В этой статье описываются предварительные требования и стандартные этапы миграции проекта ASP.NET Core\_1.x в ASP.NET Core\_2.0."
ms.author: scaddie
ms.custom: mvc
ms.date: 10/24/2018
uid: migration/1x-to-2x/index
---
# <a name="migrate-from-aspnet-core-1x-to-20"></a><span data-ttu-id="a9dba-103">Миграция с ASP.NET Core 1.x на 2.0</span><span class="sxs-lookup"><span data-stu-id="a9dba-103">Migrate from ASP.NET Core 1.x to 2.0</span></span>

<span data-ttu-id="a9dba-104">Автор: [Скотт Адди](https://github.com/scottaddie) (Scott Addie)</span><span class="sxs-lookup"><span data-stu-id="a9dba-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="a9dba-105">В этой статье поэтапно рассматривается обновление существующего проекта ASP.NET Core 1.x до версии ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="a9dba-105">In this article, we walk you through updating an existing ASP.NET Core 1.x project to ASP.NET Core 2.0.</span></span> <span data-ttu-id="a9dba-106">Миграция приложения в ASP.NET Core 2.0 позволяет воспользоваться [множеством новых функций и улучшений производительности](xref:aspnetcore-2.0).</span><span class="sxs-lookup"><span data-stu-id="a9dba-106">Migrating your application to ASP.NET Core 2.0 enables you to take advantage of [many new features and performance improvements](xref:aspnetcore-2.0).</span></span>

<span data-ttu-id="a9dba-107">Существующие приложения ASP.NET Core 1.x основаны на шаблонах проектов для определенной версии.</span><span class="sxs-lookup"><span data-stu-id="a9dba-107">Existing ASP.NET Core 1.x applications are based off of version-specific project templates.</span></span> <span data-ttu-id="a9dba-108">По мере развития платформы ASP.NET Core совершенствуются шаблоны проектов и содержащийся в них начальный код.</span><span class="sxs-lookup"><span data-stu-id="a9dba-108">As the ASP.NET Core framework evolves, so do the project templates and the starter code contained within them.</span></span> <span data-ttu-id="a9dba-109">Помимо обновления платформы ASP.NET Core, необходимо также обновить код приложения.</span><span class="sxs-lookup"><span data-stu-id="a9dba-109">In addition to updating the ASP.NET Core framework, you need to update the code for your application.</span></span>

<a name="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="a9dba-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a9dba-110">Prerequisites</span></span>

<span data-ttu-id="a9dba-111">См. [Начало работы с ASP.NET Core](xref:getting-started).</span><span class="sxs-lookup"><span data-stu-id="a9dba-111">See [Get Started with ASP.NET Core](xref:getting-started).</span></span>

<a name="tfm"></a>

## <a name="update-target-framework-moniker-tfm"></a><span data-ttu-id="a9dba-112">Обновление моникера целевой платформы (TFM)</span><span class="sxs-lookup"><span data-stu-id="a9dba-112">Update Target Framework Moniker (TFM)</span></span>

<span data-ttu-id="a9dba-113">Проекты, предназначенные для .NET Core, должны использовать [моникер целевой платформы](/dotnet/standard/frameworks#referring-to-frameworks) версии не ниже .NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="a9dba-113">Projects targeting .NET Core should use the [TFM](/dotnet/standard/frameworks#referring-to-frameworks) of a version greater than or equal to .NET Core 2.0.</span></span> <span data-ttu-id="a9dba-114">Найдите в файле *CSPROJ* узел `<TargetFramework>` и замените его содержимое на `netcoreapp2.0`:</span><span class="sxs-lookup"><span data-stu-id="a9dba-114">Search for the `<TargetFramework>` node in the *.csproj* file, and replace its inner text with `netcoreapp2.0`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=3)]

<span data-ttu-id="a9dba-115">Проекты, предназначенные для .NET Framework, должны использовать моникер целевой платформы версии не ниже .NET Framework 4.6.1.</span><span class="sxs-lookup"><span data-stu-id="a9dba-115">Projects targeting .NET Framework should use the TFM of a version greater than or equal to .NET Framework 4.6.1.</span></span> <span data-ttu-id="a9dba-116">Найдите в файле *CSPROJ* узел `<TargetFramework>` и замените его содержимое на `net461`:</span><span class="sxs-lookup"><span data-stu-id="a9dba-116">Search for the `<TargetFramework>` node in the *.csproj* file, and replace its inner text with `net461`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=4)]

> [!NOTE]
> <span data-ttu-id="a9dba-117">.NET Core 2.0 обеспечивает гораздо большую контактную зону по сравнению с .NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="a9dba-117">.NET Core 2.0 offers a much larger surface area than .NET Core 1.x.</span></span> <span data-ttu-id="a9dba-118">Если вы используете .NET Framework только из-за отсутствия нужных API в .NET Core 1.x, скорее всего, .NET Core 2.0 удовлетворит ваши потребности.</span><span class="sxs-lookup"><span data-stu-id="a9dba-118">If you're targeting .NET Framework solely because of missing APIs in .NET Core 1.x, targeting .NET Core 2.0 is likely to work.</span></span>

<a name="global-json"></a>

## <a name="update-net-core-sdk-version-in-globaljson"></a><span data-ttu-id="a9dba-119">Обновление версии пакета SDK для .NET Core в файле global.json</span><span class="sxs-lookup"><span data-stu-id="a9dba-119">Update .NET Core SDK version in global.json</span></span>

<span data-ttu-id="a9dba-120">Если ваше решение использует файл [*global.json*](/dotnet/core/tools/global-json) для указания целевой версии пакета SDK для .NET Core, измените значение свойства `version` так, чтобы использовалась версия 2.0, установленная на компьютере:</span><span class="sxs-lookup"><span data-stu-id="a9dba-120">If your solution relies upon a [*global.json*](/dotnet/core/tools/global-json) file to target a specific .NET Core SDK version, update its `version` property to use the 2.0 version installed on your machine:</span></span>

[!code-json[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/global.json?highlight=3)]

<a name="package-reference"></a>

## <a name="update-package-references"></a><span data-ttu-id="a9dba-121">Обновление ссылок на пакеты</span><span class="sxs-lookup"><span data-stu-id="a9dba-121">Update package references</span></span>

<span data-ttu-id="a9dba-122">В файле *CSPROJ* в проекте версии 1.x перечислены все проекты NuGet, используемые проектом.</span><span class="sxs-lookup"><span data-stu-id="a9dba-122">The *.csproj* file in a 1.x project lists each NuGet package used by the project.</span></span>

<span data-ttu-id="a9dba-123">В проекте ASP.NET Core 2.0, предназначенном для .NET Core 2.0, коллекция пакетов в файле *CSPROJ* заменяется ссылкой на один [метапакет](xref:fundamentals/metapackage):</span><span class="sxs-lookup"><span data-stu-id="a9dba-123">In an ASP.NET Core 2.0 project targeting .NET Core 2.0, a single [metapackage](xref:fundamentals/metapackage) reference in the *.csproj* file replaces the collection of packages:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=8-10)]

<span data-ttu-id="a9dba-124">В метапакет входят все компоненты ASP.NET Core 2.0 и Entity Framework Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="a9dba-124">All the features of ASP.NET Core 2.0 and Entity Framework Core 2.0 are included in the metapackage.</span></span>

<span data-ttu-id="a9dba-125">В проектах ASP.NET Core 2.0, предназначенных для .NET Framework, по-прежнему должны использоваться ссылки на отдельные пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="a9dba-125">ASP.NET Core 2.0 projects targeting .NET Framework should continue to reference individual NuGet packages.</span></span> <span data-ttu-id="a9dba-126">Измените значение атрибута `Version` каждого узла `<PackageReference />` на 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a9dba-126">Update the `Version` attribute of each `<PackageReference />` node to 2.0.0.</span></span>

<span data-ttu-id="a9dba-127">Например, вот список узлов `<PackageReference />`, используемых в типичном проекте ASP.NET Core 2.0, предназначенном для .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="a9dba-127">For example, here's the list of `<PackageReference />` nodes used in a typical ASP.NET Core 2.0 project targeting .NET Framework:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=9-22)]

<a name="dot-net-cli-tool-reference"></a>

## <a name="update-net-core-cli-tools"></a><span data-ttu-id="a9dba-128">Обновление средств CLI для .NET Core</span><span class="sxs-lookup"><span data-stu-id="a9dba-128">Update .NET Core CLI tools</span></span>

<span data-ttu-id="a9dba-129">Измените значение атрибута *каждого узла* в файле `Version`CSPROJ`<DotNetCliToolReference />` на 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a9dba-129">In the *.csproj* file, update the `Version` attribute of each `<DotNetCliToolReference />` node to 2.0.0.</span></span>

<span data-ttu-id="a9dba-130">Например, вот список средств CLI, используемых в типичном проекте ASP.NET Core 2.0, предназначенном для .NET Core 2.0:</span><span class="sxs-lookup"><span data-stu-id="a9dba-130">For example, here's the list of CLI tools used in a typical ASP.NET Core 2.0 project targeting .NET Core 2.0:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=12-16)]

<a name="package-target-fallback"></a>

## <a name="rename-package-target-fallback-property"></a><span data-ttu-id="a9dba-131">Переименование свойства PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="a9dba-131">Rename Package Target Fallback property</span></span>

<span data-ttu-id="a9dba-132">В проектах версии 1.x в файлах *CSPROJ* использовался узел `PackageTargetFallback` и переменная:</span><span class="sxs-lookup"><span data-stu-id="a9dba-132">The *.csproj* file of a 1.x project used a `PackageTargetFallback` node and variable:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App.csproj?range=5)]

<span data-ttu-id="a9dba-133">Переименуйте этот узел и переменную в `AssetTargetFallback`:</span><span class="sxs-lookup"><span data-stu-id="a9dba-133">Rename both the node and variable to `AssetTargetFallback`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=4)]

<a name="program-cs"></a>

## <a name="update-main-method-in-programcs"></a><span data-ttu-id="a9dba-134">Обновление метода Main в файле Program.cs</span><span class="sxs-lookup"><span data-stu-id="a9dba-134">Update Main method in Program.cs</span></span>

<span data-ttu-id="a9dba-135">В проектах версии 1.x метод `Main` в файле *Program.cs* выглядел так:</span><span class="sxs-lookup"><span data-stu-id="a9dba-135">In 1.x projects, the `Main` method of *Program.cs* looked like this:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Program.cs?name=snippet_ProgramCs&highlight=8-19)]

<span data-ttu-id="a9dba-136">В проектах версии 2.0 метод `Main` в файле *Program.cs* упрощен:</span><span class="sxs-lookup"><span data-stu-id="a9dba-136">In 2.0 projects, the `Main` method of *Program.cs* has been simplified:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Program.cs?highlight=8-11)]

<span data-ttu-id="a9dba-137">Внедрение нового шаблона версии 2.0 настоятельно рекомендуется; оно является обязательным для использования [миграций Entity Framework (EF) Core](xref:data/ef-mvc/migrations) и ряда других функций продукта.</span><span class="sxs-lookup"><span data-stu-id="a9dba-137">The adoption of this new 2.0 pattern is highly recommended and is required for product features like [Entity Framework (EF) Core Migrations](xref:data/ef-mvc/migrations) to work.</span></span> <span data-ttu-id="a9dba-138">Например, при выполнении команды `Update-Database` из консоли диспетчера пакетов или команды `dotnet ef database update` в командной строке (для проектов, преобразованных в ASP.NET Core 2.0) возникает следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="a9dba-138">For example, running `Update-Database` from the Package Manager Console window or `dotnet ef database update` from the command line (on projects converted to ASP.NET Core 2.0) generates the following error:</span></span>

```
Unable to create an object of type '<Context>'. Add an implementation of 'IDesignTimeDbContextFactory<Context>' to the project, or see https://go.microsoft.com/fwlink/?linkid=851728 for additional patterns supported at design time.
```

<a name="add-modify-configuration"></a>

## <a name="add-configuration-providers"></a><span data-ttu-id="a9dba-139">Все поставщики конфигурации</span><span class="sxs-lookup"><span data-stu-id="a9dba-139">Add configuration providers</span></span>

<span data-ttu-id="a9dba-140">В проектах 1.x поставщики конфигурации добавлялись в приложение с помощью конструктора `Startup`.</span><span class="sxs-lookup"><span data-stu-id="a9dba-140">In 1.x projects, adding configuration providers to an app was accomplished via the `Startup` constructor.</span></span> <span data-ttu-id="a9dba-141">Для этого нужно было создать экземпляр `ConfigurationBuilder`, загрузить применимые поставщики (переменные сред, параметры приложений и т. д.) и инициализировать член `IConfigurationRoot`.</span><span class="sxs-lookup"><span data-stu-id="a9dba-141">The steps involved creating an instance of `ConfigurationBuilder`, loading applicable providers (environment variables, app settings, etc.), and initializing a member of `IConfigurationRoot`.</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Startup.cs?name=snippet_1xStartup)]

<span data-ttu-id="a9dba-142">В примере выше происходит загрузка члена `Configuration` с параметрами конфигурации из *appsettings.json* и любого файла *appsettings.\<Имя_среды\>.json*, соответствующего свойству `IHostingEnvironment.EnvironmentName`.</span><span class="sxs-lookup"><span data-stu-id="a9dba-142">The preceding example loads the `Configuration` member with configuration settings from *appsettings.json* as well as any *appsettings.\<EnvironmentName\>.json* file matching the `IHostingEnvironment.EnvironmentName` property.</span></span> <span data-ttu-id="a9dba-143">Эти файлы располагаются по тому же пути, что и *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="a9dba-143">The location of these files is at the same path as *Startup.cs*.</span></span>

<span data-ttu-id="a9dba-144">В проектах 2.0 стереотипный код конфигурации из проектов 1.x запускается "за кулисами".</span><span class="sxs-lookup"><span data-stu-id="a9dba-144">In 2.0 projects, the boilerplate configuration code inherent to 1.x projects runs behind-the-scenes.</span></span> <span data-ttu-id="a9dba-145">Например, переменные сред и параметры приложений загружаются при запуске.</span><span class="sxs-lookup"><span data-stu-id="a9dba-145">For example, environment variables and app settings are loaded at startup.</span></span> <span data-ttu-id="a9dba-146">Эквивалентный код *Startup.cs* сокращается до инициализации `IConfiguration` с внедрением экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a9dba-146">The equivalent *Startup.cs* code is reduced to `IConfiguration` initialization with the injected instance:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/Startup.cs?name=snippet_2xStartup)]

<span data-ttu-id="a9dba-147">Чтобы удалить добавляемых `WebHostBuilder.CreateDefaultBuilder` поставщиков по умолчанию, вызовите метод `Clear` для свойства `IConfigurationBuilder.Sources` внутри `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="a9dba-147">To remove the default providers added by `WebHostBuilder.CreateDefaultBuilder`, invoke the `Clear` method on the `IConfigurationBuilder.Sources` property inside of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="a9dba-148">Чтобы снова добавить поставщиков, используйте метод `ConfigureAppConfiguration` в *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="a9dba-148">To add providers back, utilize the `ConfigureAppConfiguration` method in *Program.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/Program.cs?name=snippet_ProgramMainConfigProviders&highlight=9-14)]

<span data-ttu-id="a9dba-149">Конфигурацию, используемую в предыдущем фрагменте кода методом `CreateDefaultBuilder`, можно посмотреть [здесь](https://github.com/aspnet/MetaPackages/blob/rel/2.0.0/src/Microsoft.AspNetCore/WebHost.cs#L152).</span><span class="sxs-lookup"><span data-stu-id="a9dba-149">The configuration used by the `CreateDefaultBuilder` method in the preceding code snippet can be seen [here](https://github.com/aspnet/MetaPackages/blob/rel/2.0.0/src/Microsoft.AspNetCore/WebHost.cs#L152).</span></span>

<span data-ttu-id="a9dba-150">Дополнительные сведения см. в разделе [Конфигурация в ASP.NET Core](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="a9dba-150">For more information, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

<a name="db-init-code"></a>

## <a name="move-database-initialization-code"></a><span data-ttu-id="a9dba-151">Перенос кода инициализации базы данных</span><span class="sxs-lookup"><span data-stu-id="a9dba-151">Move database initialization code</span></span>

<span data-ttu-id="a9dba-152">В проектах 1.x, где используется EF Core 1.x, такая команда, как `dotnet ef migrations add`, делает следующее.</span><span class="sxs-lookup"><span data-stu-id="a9dba-152">In 1.x projects using EF Core 1.x, a command such as `dotnet ef migrations add` does the following:</span></span>

1. <span data-ttu-id="a9dba-153">Создает экземпляр `Startup`.</span><span class="sxs-lookup"><span data-stu-id="a9dba-153">Instantiates a `Startup` instance</span></span>
1. <span data-ttu-id="a9dba-154">Вызывает метод `ConfigureServices`, чтобы зарегистрировать все службы с использованием вставки зависимостей (включая типы `DbContext`).</span><span class="sxs-lookup"><span data-stu-id="a9dba-154">Invokes the `ConfigureServices` method to register all services with dependency injection (including `DbContext` types)</span></span>
1. <span data-ttu-id="a9dba-155">Выполняет свои требуемые задачи.</span><span class="sxs-lookup"><span data-stu-id="a9dba-155">Performs its requisite tasks</span></span>

<span data-ttu-id="a9dba-156">В проектах 2.0, где используется EF Core 2.0, вызывается `Program.BuildWebHost`, чтобы получить службы приложений.</span><span class="sxs-lookup"><span data-stu-id="a9dba-156">In 2.0 projects using EF Core 2.0, `Program.BuildWebHost` is invoked to obtain the application services.</span></span> <span data-ttu-id="a9dba-157">В отличие от 1.x, это также приводит к вызову `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="a9dba-157">Unlike 1.x, this has the additional side effect of invoking `Startup.Configure`.</span></span> <span data-ttu-id="a9dba-158">Если ваше приложение 1.x вызвало код инициализации базы данных в своем методе `Configure`, могут возникнуть непредвиденные проблемы.</span><span class="sxs-lookup"><span data-stu-id="a9dba-158">If your 1.x app invoked database initialization code in its `Configure` method, unexpected problems can occur.</span></span> <span data-ttu-id="a9dba-159">Например, если база данных еще не существует, код заполнения запускается до выполнения команды миграции EF Core.</span><span class="sxs-lookup"><span data-stu-id="a9dba-159">For example, if the database doesn't yet exist, the seeding code runs before the EF Core Migrations command execution.</span></span> <span data-ttu-id="a9dba-160">Из-за этой проблемы, если база данных еще не существует, команда `dotnet ef migrations list` не срабатывает.</span><span class="sxs-lookup"><span data-stu-id="a9dba-160">This problem causes a `dotnet ef migrations list` command to fail if the database doesn't yet exist.</span></span>

<span data-ttu-id="a9dba-161">В качестве примера из версии 1.x возьмем следующий код инициализации заполнения в методе `Configure` из *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="a9dba-161">Consider the following 1.x seed initialization code in the `Configure` method of *Startup.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Startup.cs?name=snippet_ConfigureSeedData&highlight=8)]

<span data-ttu-id="a9dba-162">В проектах 2.0 поместите вызов `SeedData.Initialize` в метод `Main` из *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="a9dba-162">In 2.0 projects, move the `SeedData.Initialize` call to the `Main` method of *Program.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Program2.cs?name=snippet_Main2Code&highlight=10)]

<span data-ttu-id="a9dba-163">Начиная с версии 2.0, делать в `BuildWebHost` что-либо помимо сборки и настройки веб-узла не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="a9dba-163">As of 2.0, it's bad practice to do anything in `BuildWebHost` except build and configure the web host.</span></span> <span data-ttu-id="a9dba-164">Все, что касается работы приложения, должно обрабатываться вне `BuildWebHost` &mdash; обычно в методе `Main` из *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="a9dba-164">Anything that's about running the application should be handled outside of `BuildWebHost` &mdash; typically in the `Main` method of *Program.cs*.</span></span>

<a name="view-compilation"></a>

## <a name="review-razor-view-compilation-setting"></a><span data-ttu-id="a9dba-165">Проверка параметра компиляции представлений Razor</span><span class="sxs-lookup"><span data-stu-id="a9dba-165">Review Razor view compilation setting</span></span>

<span data-ttu-id="a9dba-166">Сокращение времени запуска приложений и уменьшение размеров публикуемых пакетов крайне важны.</span><span class="sxs-lookup"><span data-stu-id="a9dba-166">Faster application startup time and smaller published bundles are of utmost importance to you.</span></span> <span data-ttu-id="a9dba-167">По этой причине в ASP.NET Core 2.0 по умолчанию включена [компиляция представлений Razor](xref:mvc/views/view-compilation).</span><span class="sxs-lookup"><span data-stu-id="a9dba-167">For these reasons, [Razor view compilation](xref:mvc/views/view-compilation) is enabled by default in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="a9dba-168">Присваивать свойству `MvcRazorCompileOnPublish` значение true больше не нужно.</span><span class="sxs-lookup"><span data-stu-id="a9dba-168">Setting the `MvcRazorCompileOnPublish` property to true is no longer required.</span></span> <span data-ttu-id="a9dba-169">Если вы не собираетесь отключать компиляцию представлений, это свойство можно удалить из файла *CSPROJ*.</span><span class="sxs-lookup"><span data-stu-id="a9dba-169">Unless you're disabling view compilation, the property may be removed from the *.csproj* file.</span></span>

<span data-ttu-id="a9dba-170">Если проект предназначен для .NET Framework, необходимо по-прежнему явно указывать ссылку на пакет NuGet [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) в файле *CSPROJ*:</span><span class="sxs-lookup"><span data-stu-id="a9dba-170">When targeting .NET Framework, you still need to explicitly reference the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) NuGet package in your *.csproj* file:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=15)]

<a name="app-insights"></a>

## <a name="rely-on-application-insights-light-up-features"></a><span data-ttu-id="a9dba-171">Использование подсветки функций Application Insights</span><span class="sxs-lookup"><span data-stu-id="a9dba-171">Rely on Application Insights "light-up" features</span></span>

<span data-ttu-id="a9dba-172">Простота настройки инструментария для обеспечения производительности приложений имеет большое значение.</span><span class="sxs-lookup"><span data-stu-id="a9dba-172">Effortless setup of application performance instrumentation is important.</span></span> <span data-ttu-id="a9dba-173">Теперь вам доступны новые функции подготовки [Application Insights](/azure/application-insights/app-insights-overview) в составе средств Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a9dba-173">You can now rely on the new [Application Insights](/azure/application-insights/app-insights-overview) "light-up" features available in the Visual Studio 2017 tooling.</span></span>

<span data-ttu-id="a9dba-174">При создании проектов ASP.NET Core 1.1 в Visual Studio 2017 служба Application Insights добавлялась по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9dba-174">ASP.NET Core 1.1 projects created in Visual Studio 2017 added Application Insights by default.</span></span> <span data-ttu-id="a9dba-175">Если вы не используете пакет SDK для Application Insights напрямую вне файлов *Program.cs* и *Startup.cs*, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="a9dba-175">If you're not using the Application Insights SDK directly, outside of *Program.cs* and *Startup.cs*, follow these steps:</span></span>

1. <span data-ttu-id="a9dba-176">Для работы с .NET Core удалите из файла *CSPROJ* следующий узел `<PackageReference />`:</span><span class="sxs-lookup"><span data-stu-id="a9dba-176">If targeting .NET Core, remove the following `<PackageReference />` node from the *.csproj* file:</span></span>

    [!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App.csproj?range=10)]

2. <span data-ttu-id="a9dba-177">Для работы с .NET Core удалите вызов метода расширения `UseApplicationInsights` из файла *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="a9dba-177">If targeting .NET Core, remove the `UseApplicationInsights` extension method invocation from *Program.cs*:</span></span>

    [!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Program.cs?name=snippet_ProgramCsMain&highlight=8)]

3. <span data-ttu-id="a9dba-178">Удалите вызов API на стороне клиента Application Insights из файла *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="a9dba-178">Remove the Application Insights client-side API call from *_Layout.cshtml*.</span></span> <span data-ttu-id="a9dba-179">Этот вызов включает две строки кода:</span><span class="sxs-lookup"><span data-stu-id="a9dba-179">It comprises the following two lines of code:</span></span>

    [!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Views/Shared/_Layout.cshtml?range=1,19&dedent=4)]

<span data-ttu-id="a9dba-180">Если вы используете пакет SDK для Application Insights напрямую, продолжайте делать это.</span><span class="sxs-lookup"><span data-stu-id="a9dba-180">If you are using the Application Insights SDK directly, continue to do so.</span></span> <span data-ttu-id="a9dba-181">[Метапакет](xref:fundamentals/metapackage) версии 2.0 включает в себя последнюю версию Application Insights, поэтому при попытке сослаться на более старую версию возникает ошибка понижения уровня пакета.</span><span class="sxs-lookup"><span data-stu-id="a9dba-181">The 2.0 [metapackage](xref:fundamentals/metapackage) includes the latest version of Application Insights, so a package downgrade error appears if you're referencing an older version.</span></span>

<a name="auth-and-identity"></a>

## <a name="adopt-authenticationidentity-improvements"></a><span data-ttu-id="a9dba-182">Усовершенствования проверки подлинности и службы идентификации</span><span class="sxs-lookup"><span data-stu-id="a9dba-182">Adopt authentication/Identity improvements</span></span>

<span data-ttu-id="a9dba-183">В ASP.NET Core 2.0 реализована новая модель проверки подлинности и внесен ряд важных изменений в удостоверение ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a9dba-183">ASP.NET Core 2.0 has a new authentication model and a number of significant changes to ASP.NET Core Identity.</span></span> <span data-ttu-id="a9dba-184">Если при создании проекта вы включили отдельные учетные записи пользователей либо вручную добавили проверку подлинности или удостоверение, см. статью [Миграция на другой метод проверки подлинности и другие удостоверения в ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x).</span><span class="sxs-lookup"><span data-stu-id="a9dba-184">If you created your project with Individual User Accounts enabled, or if you have manually added authentication or Identity, see [Migrate Authentication and Identity to ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9dba-185">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a9dba-185">Additional resources</span></span>

* [<span data-ttu-id="a9dba-186">Критические изменения в ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="a9dba-186">Breaking Changes in ASP.NET Core 2.0</span></span>](https://github.com/aspnet/announcements/issues?page=1&q=is%3Aissue+is%3Aopen+label%3A2.0.0+label%3A%22Breaking+change%22&utf8=%E2%9C%93)
