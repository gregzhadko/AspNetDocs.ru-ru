---
title: "Миграция с ASP.NET на ASP.NET\_Core"
author: isaac2004
description: "Здесь вы найдете указания по миграции существующих приложений MVC\_ASP.NET или веб-API на ASP.NET\_Core.web"
ms.author: scaddie
ms.date: 12/11/2018
uid: migration/proper-to-2x/index
---
# <a name="migrate-from-aspnet-to-aspnet-core"></a><span data-ttu-id="98b52-103">Миграция с ASP.NET на ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="98b52-103">Migrate from ASP.NET to ASP.NET Core</span></span>

<span data-ttu-id="98b52-104">Автор [Айзек Левин](https://isaaclevin.com) (Isaac Levin)</span><span class="sxs-lookup"><span data-stu-id="98b52-104">By [Isaac Levin](https://isaaclevin.com)</span></span>

<span data-ttu-id="98b52-105">Данная статья служит руководством по миграции приложений ASP.NET на ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="98b52-105">This article serves as a reference guide for migrating ASP.NET apps to ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98b52-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98b52-106">Prerequisites</span></span>

[<span data-ttu-id="98b52-107">Пакет SDK для .NET Core 2.2 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="98b52-107">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download)

## <a name="target-frameworks"></a><span data-ttu-id="98b52-108">Требуемые версии .NET Framework</span><span class="sxs-lookup"><span data-stu-id="98b52-108">Target frameworks</span></span>

<span data-ttu-id="98b52-109">Проекты ASP.NET Core предлагают разработчикам гибкость работы с .NET Core и .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="98b52-109">ASP.NET Core projects offer developers the flexibility of targeting .NET Core, .NET Framework, or both.</span></span> <span data-ttu-id="98b52-110">Определить наиболее подходящую платформу поможет статья [Выбор между .NET Core и .NET Framework для серверных приложений](/dotnet/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="98b52-110">See [Choosing between .NET Core and .NET Framework for server apps](/dotnet/standard/choosing-core-framework-server) to determine which target framework is most appropriate.</span></span>

<span data-ttu-id="98b52-111">При разработке для .NET Framework проекты должны ссылаться на отдельные пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="98b52-111">When targeting .NET Framework, projects need to reference individual NuGet packages.</span></span>

<span data-ttu-id="98b52-112">Работа с .NET Core позволяет избавиться от многочисленных явных ссылок на пакеты благодаря [метапакету](xref:fundamentals/metapackage-app) ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="98b52-112">Targeting .NET Core allows you to eliminate numerous explicit package references, thanks to the ASP.NET Core [metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="98b52-113">Установите метапакет `Microsoft.AspNetCore.App` в свой проект.</span><span class="sxs-lookup"><span data-stu-id="98b52-113">Install the `Microsoft.AspNetCore.App` metapackage in your project:</span></span>

```xml
<ItemGroup>
   <PackageReference Include="Microsoft.AspNetCore.App" />
</ItemGroup>
```

<span data-ttu-id="98b52-114">При использовании метапакета никакие указанные по ссылкам пакеты с приложением не развертываются.</span><span class="sxs-lookup"><span data-stu-id="98b52-114">When the metapackage is used, no packages referenced in the metapackage are deployed with the app.</span></span> <span data-ttu-id="98b52-115">Все эти ресурсы входят в хранилище среды выполнения .NET Core и предварительно компилируются для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="98b52-115">The .NET Core Runtime Store includes these assets, and they're precompiled to improve performance.</span></span> <span data-ttu-id="98b52-116">Дополнительные сведения см. в статье [Метапакет Microsoft.AspNetCore.App для ASP.NET Core 2.1](xref:fundamentals/metapackage-app).</span><span class="sxs-lookup"><span data-stu-id="98b52-116">See [Microsoft.AspNetCore.App metapackage for ASP.NET Core](xref:fundamentals/metapackage-app) for more detail.</span></span>

## <a name="project-structure-differences"></a><span data-ttu-id="98b52-117">Различия в структуре пакетов</span><span class="sxs-lookup"><span data-stu-id="98b52-117">Project structure differences</span></span>

<span data-ttu-id="98b52-118">В ASP.NET Core упрощен формат файла *.csproj*.</span><span class="sxs-lookup"><span data-stu-id="98b52-118">The *.csproj* file format has been simplified in ASP.NET Core.</span></span> <span data-ttu-id="98b52-119">Вот некоторые основные изменения.</span><span class="sxs-lookup"><span data-stu-id="98b52-119">Some notable changes include:</span></span>

- <span data-ttu-id="98b52-120">Чтобы файлы считались частью проекта, включать их явно теперь не требуется.</span><span class="sxs-lookup"><span data-stu-id="98b52-120">Explicit inclusion of files isn't necessary for them to be considered part of the project.</span></span> <span data-ttu-id="98b52-121">Это уменьшает вероятность конфликтов слияния XML при работе в больших командах.</span><span class="sxs-lookup"><span data-stu-id="98b52-121">This reduces the risk of XML merge conflicts when working on large teams.</span></span>
- <span data-ttu-id="98b52-122">GUID-ссылки на другие проекты не используются, что повышает удобочитаемость файла.</span><span class="sxs-lookup"><span data-stu-id="98b52-122">There are no GUID-based references to other projects, which improves file readability.</span></span>
- <span data-ttu-id="98b52-123">Файл можно редактировать, не выгружая его в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98b52-123">The file can be edited without unloading it in Visual Studio:</span></span>

    ![Параметр изменения файла CSPROJ в контекстном меню в Visual Studio 2017](_static/EditProjectVs2017.png)

## <a name="globalasax-file-replacement"></a><span data-ttu-id="98b52-125">Замена файла Global.asax</span><span class="sxs-lookup"><span data-stu-id="98b52-125">Global.asax file replacement</span></span>

<span data-ttu-id="98b52-126">В ASP.NET Core появился новый механизм для начальной загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="98b52-126">ASP.NET Core introduced a new mechanism for bootstrapping an app.</span></span> <span data-ttu-id="98b52-127">Точкой входа для приложений ASP.NET стал файл *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="98b52-127">The entry point for ASP.NET applications is the *Global.asax* file.</span></span> <span data-ttu-id="98b52-128">Такие задачи, как конфигурация маршрута, а также регистрации фильтров и областей, теперь выполняются в файле *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="98b52-128">Tasks such as route configuration and filter and area registrations are handled in the *Global.asax* file.</span></span>

[!code-csharp[](samples/globalasax-sample.cs)]

<span data-ttu-id="98b52-129">При этом подходе приложение сопоставляется с сервером, на котором оно развертывается, таким образом, чтобы это не мешало реализации.</span><span class="sxs-lookup"><span data-stu-id="98b52-129">This approach couples the application and the server to which it's deployed in a way that interferes with the implementation.</span></span> <span data-ttu-id="98b52-130">Чтобы отделить приложение от сервера, был введен [OWIN](http://owin.org/), который обеспечивает более точный способ совместного использования нескольких платформ.</span><span class="sxs-lookup"><span data-stu-id="98b52-130">In an effort to decouple, [OWIN](http://owin.org/) was introduced to provide a cleaner way to use multiple frameworks together.</span></span> <span data-ttu-id="98b52-131">OWIN предоставляет конвейер для добавления только необходимых модулей.</span><span class="sxs-lookup"><span data-stu-id="98b52-131">OWIN provides a pipeline to add only the modules needed.</span></span> <span data-ttu-id="98b52-132">Среда внешнего размещения принимает функцию [Startup](xref:fundamentals/startup) для настройки служб и конвейера обработки запросов приложения.</span><span class="sxs-lookup"><span data-stu-id="98b52-132">The hosting environment takes a [Startup](xref:fundamentals/startup) function to configure services and the app's request pipeline.</span></span> <span data-ttu-id="98b52-133">`Startup` регистрирует набор ПО промежуточного слоя в приложении.</span><span class="sxs-lookup"><span data-stu-id="98b52-133">`Startup` registers a set of middleware with the application.</span></span> <span data-ttu-id="98b52-134">Для каждого запроса приложение вызывает каждый из компонентов ПО промежуточного слоя по заглавному указателю связанного списка на существующий набор обработчиков.</span><span class="sxs-lookup"><span data-stu-id="98b52-134">For each request, the application calls each of the middleware components with the head pointer of a linked list to an existing set of handlers.</span></span> <span data-ttu-id="98b52-135">Каждый компонент ПО промежуточного слоя может добавлять в конвейер обработки запросов один обработчик или несколько.</span><span class="sxs-lookup"><span data-stu-id="98b52-135">Each middleware component can add one or more handlers to the request handling pipeline.</span></span> <span data-ttu-id="98b52-136">Это достигается путем возвращения ссылки на обработчик, который представляет собой новый заголовок списка.</span><span class="sxs-lookup"><span data-stu-id="98b52-136">This is accomplished by returning a reference to the handler that's the new head of the list.</span></span> <span data-ttu-id="98b52-137">Каждый обработчик отвечает за запоминание и вызов следующего обработчика в списке.</span><span class="sxs-lookup"><span data-stu-id="98b52-137">Each handler is responsible for remembering and invoking the next handler in the list.</span></span> <span data-ttu-id="98b52-138">При работе с ASP.NET Core точкой входа в приложения становится `Startup`, и зависимость от файла *Global.asax* исчезает.</span><span class="sxs-lookup"><span data-stu-id="98b52-138">With ASP.NET Core, the entry point to an application is `Startup`, and you no longer have a dependency on *Global.asax*.</span></span> <span data-ttu-id="98b52-139">Используя OWIN с .NET Framework, применяйте для конвейера код следующего вида:</span><span class="sxs-lookup"><span data-stu-id="98b52-139">When using OWIN with .NET Framework, use something like the following as a pipeline:</span></span>

[!code-csharp[](samples/webapi-owin.cs)]

<span data-ttu-id="98b52-140">Он определяет ваши маршруты по умолчанию и изначально предусматривает XmlSerialization по Json.</span><span class="sxs-lookup"><span data-stu-id="98b52-140">This configures your default routes, and defaults to XmlSerialization over Json.</span></span> <span data-ttu-id="98b52-141">При необходимости добавьте другое ПО промежуточного слоя для этого конвейера (загрузка служб, параметры конфигурации, статические файлы и т. д.).</span><span class="sxs-lookup"><span data-stu-id="98b52-141">Add other Middleware to this pipeline as needed (loading services, configuration settings, static files, etc.).</span></span>

<span data-ttu-id="98b52-142">ASP.NET Core использует аналогичный подход, но не требует OWIN для обработки запроса.</span><span class="sxs-lookup"><span data-stu-id="98b52-142">ASP.NET Core uses a similar approach, but doesn't rely on OWIN to handle the entry.</span></span> <span data-ttu-id="98b52-143">Вместо этого применяется метод *Program.cs* `Main` (как в консольных приложениях) и `Startup` загружается через него.</span><span class="sxs-lookup"><span data-stu-id="98b52-143">Instead, that's done through the *Program.cs* `Main` method (similar to console applications) and `Startup` is loaded through there.</span></span>

[!code-csharp[](samples/program.cs)]

<span data-ttu-id="98b52-144">`Startup` должен включать метод `Configure`.</span><span class="sxs-lookup"><span data-stu-id="98b52-144">`Startup` must include a `Configure` method.</span></span> <span data-ttu-id="98b52-145">В `Configure` добавьте в конвейер необходимое ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="98b52-145">In `Configure`, add the necessary middleware to the pipeline.</span></span> <span data-ttu-id="98b52-146">В примере ниже (на основе шаблона веб-сайта по умолчанию) используются методы расширения для настройки конвейера с поддержкой следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="98b52-146">In the following example (from the default web site template), extension methods configure the pipeline with support for:</span></span>

* <span data-ttu-id="98b52-147">Страницы ошибок</span><span class="sxs-lookup"><span data-stu-id="98b52-147">Error pages</span></span>
* <span data-ttu-id="98b52-148">HTTP Strict Transport Security;</span><span class="sxs-lookup"><span data-stu-id="98b52-148">HTTP Strict Transport Security</span></span>
* <span data-ttu-id="98b52-149">перенаправление с HTTP на HTTPS;</span><span class="sxs-lookup"><span data-stu-id="98b52-149">HTTP redirection to HTTPS</span></span>
* <span data-ttu-id="98b52-150">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="98b52-150">ASP.NET Core MVC</span></span>

[!code-csharp[](samples/startup.cs)]

<span data-ttu-id="98b52-151">Сервер и приложение разделены, что позволит вам в будущем легко перейти на другую платформу.</span><span class="sxs-lookup"><span data-stu-id="98b52-151">The host and application have been decoupled, which provides the flexibility of moving to a different platform in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="98b52-152">Более подробный справочник по запуску ASP.NET Core и ПО промежуточного слоя см. в статье [Запуск в ASP.NET Core](xref:fundamentals/startup).</span><span class="sxs-lookup"><span data-stu-id="98b52-152">For a more in-depth reference to ASP.NET Core Startup and Middleware, see [Startup in ASP.NET Core](xref:fundamentals/startup)</span></span>

## <a name="store-configurations"></a><span data-ttu-id="98b52-153">Конфигурации хранения</span><span class="sxs-lookup"><span data-stu-id="98b52-153">Store configurations</span></span>

<span data-ttu-id="98b52-154">ASP.NET поддерживает параметры хранения.</span><span class="sxs-lookup"><span data-stu-id="98b52-154">ASP.NET supports storing settings.</span></span> <span data-ttu-id="98b52-155">Эти параметры используются, например, для поддержки среды, в которой развертываются приложения.</span><span class="sxs-lookup"><span data-stu-id="98b52-155">These setting are used, for example, to support the environment to which the applications were deployed.</span></span> <span data-ttu-id="98b52-156">Как правило, все пользовательские пары ключей и значений хранятся в разделе `<appSettings>` файла *Web.config*:</span><span class="sxs-lookup"><span data-stu-id="98b52-156">A common practice was to store all custom key-value pairs in the `<appSettings>` section of the *Web.config* file:</span></span>

[!code-xml[](samples/webconfig-sample.xml)]

<span data-ttu-id="98b52-157">Приложения считывают эти параметры с помощью коллекции `ConfigurationManager.AppSettings` в пространстве имен `System.Configuration`:</span><span class="sxs-lookup"><span data-stu-id="98b52-157">Applications read these settings using the `ConfigurationManager.AppSettings` collection in the `System.Configuration` namespace:</span></span>

[!code-csharp[](samples/read-webconfig.cs)]

<span data-ttu-id="98b52-158">ASP.NET Core может сохранять данные конфигурации для приложения из любого файла и загружать их в процессе начальной загрузки ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="98b52-158">ASP.NET Core can store configuration data for the application in any file and load them as part of middleware bootstrapping.</span></span> <span data-ttu-id="98b52-159">По умолчанию в шаблонах проектов используется файл *appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="98b52-159">The default file used in the project templates is *appsettings.json*:</span></span>

[!code-json[](samples/appsettings-sample.json)]

<span data-ttu-id="98b52-160">Загрузка этого файла в экземпляр `IConfiguration` в вашем приложении выполняется в файле *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="98b52-160">Loading this file into an instance of `IConfiguration` inside your application is done in *Startup.cs*:</span></span>

[!code-csharp[](samples/startup-builder.cs)]

<span data-ttu-id="98b52-161">Для получения этих параметров приложение считывает данные из `Configuration`:</span><span class="sxs-lookup"><span data-stu-id="98b52-161">The app reads from `Configuration` to get the settings:</span></span>

[!code-csharp[](samples/read-appsettings.cs)]

<span data-ttu-id="98b52-162">Существуют расширения, повышающие надежность этого подхода, например, [внедрение зависимостей](xref:fundamentals/dependency-injection) позволяет загружать эти значения в службу.</span><span class="sxs-lookup"><span data-stu-id="98b52-162">There are extensions to this approach to make the process more robust, such as using [Dependency Injection](xref:fundamentals/dependency-injection) (DI) to load a service with these values.</span></span> <span data-ttu-id="98b52-163">Метод внедрения зависимостей предоставляет строго типизированный набор объектов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98b52-163">The DI approach provides a strongly-typed set of configuration objects.</span></span>

````csharp
// Assume AppConfiguration is a class representing a strongly-typed version of AppConfiguration section
services.Configure<AppConfiguration>(Configuration.GetSection("AppConfiguration"));
````

> [!NOTE]
> <span data-ttu-id="98b52-164">Более подробное руководство по конфигурации ASP.NET Core см. в статье [Конфигурация в ASP.NET Core](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="98b52-164">For a more in-depth reference to ASP.NET Core configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

## <a name="native-dependency-injection"></a><span data-ttu-id="98b52-165">Собственные функции внедрения зависимостей</span><span class="sxs-lookup"><span data-stu-id="98b52-165">Native dependency injection</span></span>

<span data-ttu-id="98b52-166">При сборке больших, масштабируемых приложений важно обеспечить слабые взаимозависимости между компонентами и службами.</span><span class="sxs-lookup"><span data-stu-id="98b52-166">An important goal when building large, scalable applications is the loose coupling of components and services.</span></span> <span data-ttu-id="98b52-167">[Внедрение зависимостей](xref:fundamentals/dependency-injection) — популярный способ решения этой задачи и собственный компонент ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="98b52-167">[Dependency Injection](xref:fundamentals/dependency-injection) is a popular technique for achieving this, and it's a native component of ASP.NET Core.</span></span>

<span data-ttu-id="98b52-168">В приложениях ASP.NET разработчики используют для внедрения зависимостей стороннюю библиотеку.</span><span class="sxs-lookup"><span data-stu-id="98b52-168">In ASP.NET apps, developers rely on a third-party library to implement Dependency Injection.</span></span> <span data-ttu-id="98b52-169">Одна из таких библиотек, [Unity](https://github.com/unitycontainer/unity), входит в шаблоны и рекомендации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="98b52-169">One such library is [Unity](https://github.com/unitycontainer/unity), provided by Microsoft Patterns & Practices.</span></span>

<span data-ttu-id="98b52-170">Пример внедрения зависимостей с использованием библиотеки Unity — это реализация `IDependencyResolver` как оболочки для `UnityContainer`:</span><span class="sxs-lookup"><span data-stu-id="98b52-170">An example of setting up Dependency Injection with Unity is implementing `IDependencyResolver` that wraps a `UnityContainer`:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample8.cs)]

<span data-ttu-id="98b52-171">Создайте экземпляр `UnityContainer`, зарегистрируйте свою службу и установите средство разрешения зависимостей `HttpConfiguration` в новый экземпляр `UnityResolver` для вашего контейнера:</span><span class="sxs-lookup"><span data-stu-id="98b52-171">Create an instance of your `UnityContainer`, register your service, and set the dependency resolver of `HttpConfiguration` to the new instance of `UnityResolver` for your container:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample9.cs)]

<span data-ttu-id="98b52-172">Там, где необходимо, вставьте `IProductRepository`:</span><span class="sxs-lookup"><span data-stu-id="98b52-172">Inject `IProductRepository` where needed:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample5.cs)]

<span data-ttu-id="98b52-173">Так как внедрение зависимостей является частью ASP.NET Core, вы можете добавить свою службу в метод `ConfigureServices` файла *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="98b52-173">Because Dependency Injection is part of ASP.NET Core, you can add your service in the `ConfigureServices` method of *Startup.cs*:</span></span>

[!code-csharp[](samples/configure-services.cs)]

<span data-ttu-id="98b52-174">Репозиторий, как и в Unity, можно внедрять где угодно.</span><span class="sxs-lookup"><span data-stu-id="98b52-174">The repository can be injected anywhere, as was true with Unity.</span></span>

> [!NOTE]
> <span data-ttu-id="98b52-175">Дополнительные сведения о внедрении зависимостей см. [здесь](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="98b52-175">For more information on dependency injection, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="serve-static-files"></a><span data-ttu-id="98b52-176">Обслуживание статических файлов</span><span class="sxs-lookup"><span data-stu-id="98b52-176">Serve static files</span></span>

<span data-ttu-id="98b52-177">Важной частью разработки веб-приложений является возможность обслуживания статических ресурсов на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="98b52-177">An important part of web development is the ability to serve static, client-side assets.</span></span> <span data-ttu-id="98b52-178">Наиболее распространенные примеры статических файлов — это HTML, каскадные таблицы стилей, Javascript и изображения.</span><span class="sxs-lookup"><span data-stu-id="98b52-178">The most common examples of static files are HTML, CSS, Javascript, and images.</span></span> <span data-ttu-id="98b52-179">Эти файлы необходимо сохранять в место публикации приложения (или CDN) и указывать по ссылкам, чтобы они могли загружаться по запросу.</span><span class="sxs-lookup"><span data-stu-id="98b52-179">These files need to be saved in the published location of the app (or CDN) and referenced so they can be loaded by a request.</span></span> <span data-ttu-id="98b52-180">В ASP.NET Core ситуация изменилась.</span><span class="sxs-lookup"><span data-stu-id="98b52-180">This process has changed in ASP.NET Core.</span></span>

<span data-ttu-id="98b52-181">В ASP.NET статические файлы хранятся в разных папках со ссылками в представлениях.</span><span class="sxs-lookup"><span data-stu-id="98b52-181">In ASP.NET, static files are stored in various directories and referenced in the views.</span></span>

<span data-ttu-id="98b52-182">В ASP.NET Core, если не заданы другие настройки, статические файлы хранятся на корневом веб-узле (*&lt;содержимое корневой папки&gt;/wwwroot*).</span><span class="sxs-lookup"><span data-stu-id="98b52-182">In ASP.NET Core, static files are stored in the "web root" (*&lt;content root&gt;/wwwroot*), unless configured otherwise.</span></span> <span data-ttu-id="98b52-183">Файлы загружаются в конвейер запросов путем вызова метода расширения `UseStaticFiles` из `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="98b52-183">The files are loaded into the request pipeline by invoking the `UseStaticFiles` extension method from `Startup.Configure`:</span></span>

[!code-csharp[](../../fundamentals/static-files/samples/1x/StartupStaticFiles.cs?highlight=3&name=snippet_ConfigureMethod)]

> [!NOTE]
> <span data-ttu-id="98b52-184">Для работы с .NET Framework установите пакет NuGet `Microsoft.AspNetCore.StaticFiles`.</span><span class="sxs-lookup"><span data-stu-id="98b52-184">If targeting .NET Framework, install the NuGet package `Microsoft.AspNetCore.StaticFiles`.</span></span>

<span data-ttu-id="98b52-185">Например, ресурс изображения в папке *wwwroot/images* доступен для браузера в расположении `http://<app>/images/<imageFileName>`.</span><span class="sxs-lookup"><span data-stu-id="98b52-185">For example, an image asset in the *wwwroot/images* folder is accessible to the browser at a location such as `http://<app>/images/<imageFileName>`.</span></span>

> [!NOTE]
> <span data-ttu-id="98b52-186">Более подробное руководство по обработке статических файлов в ASP.NET Core см. в статье [Статические файлы](xref:fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="98b52-186">For a more in-depth reference to serving static files in ASP.NET Core, see [Static files](xref:fundamentals/static-files).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98b52-187">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="98b52-187">Additional resources</span></span>

- [<span data-ttu-id="98b52-188">Перенос библиотек в .NET Core</span><span class="sxs-lookup"><span data-stu-id="98b52-188">Porting Libraries to .NET Core</span></span>](/dotnet/core/porting/libraries)
