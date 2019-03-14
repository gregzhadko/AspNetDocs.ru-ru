---
title: Начало работы с ASP.NET Core и Entity Framework 6
author: rick-anderson
description: В этой статье показано, как использовать платформу Entity Framework 6 в приложении ASP.NET Core.
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/24/2018
uid: data/entity-framework-6
ms.openlocfilehash: b7679afbe4c364386fe8f16d22d7e9797a3e0c27
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059161"
---
# <a name="get-started-with-aspnet-core-and-entity-framework-6"></a><span data-ttu-id="f7e31-103">Начало работы с ASP.NET Core и Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="f7e31-103">Get Started with ASP.NET Core and Entity Framework 6</span></span>

<span data-ttu-id="f7e31-104">Авторы: [Павел Грудзень](https://github.com/pgrudzien12) (Paweł Grudzień), [Дэмиен Понтифекс](https://github.com/DamienPontifex) (Damien Pontifex) и [Том Дайкстра](https://github.com/tdykstra) (Tom Dykstra)</span><span class="sxs-lookup"><span data-stu-id="f7e31-104">By [Paweł Grudzień](https://github.com/pgrudzien12), [Damien Pontifex](https://github.com/DamienPontifex), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f7e31-105">В этой статье показано, как использовать платформу Entity Framework 6 в приложении ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f7e31-105">This article shows how to use Entity Framework 6 in an ASP.NET Core application.</span></span>

## <a name="overview"></a><span data-ttu-id="f7e31-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="f7e31-106">Overview</span></span>

<span data-ttu-id="f7e31-107">Чтобы использовать платформу Entity Framework 6, проект необходимо компилировать на основе .NET Framework, поскольку Entity Framework 6 не поддерживает .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f7e31-107">To use Entity Framework 6, your project has to compile against .NET Framework, as Entity Framework 6 doesn't support .NET Core.</span></span> <span data-ttu-id="f7e31-108">Если вам требуются какие-либо кроссплатформенные функции, необходимо выполнить обновление до [Entity Framework Core](/ef/).</span><span class="sxs-lookup"><span data-stu-id="f7e31-108">If you need cross-platform features you will need to upgrade to [Entity Framework Core](/ef/).</span></span>

<span data-ttu-id="f7e31-109">Рекомендуемый способ использования платформы Entity Framework 6 в приложении ASP.NET Core заключается в помещении контекста и классов модели EF6 в проект библиотеки классов, который предназначен для полной платформы.</span><span class="sxs-lookup"><span data-stu-id="f7e31-109">The recommended way to use Entity Framework 6 in an ASP.NET Core application is to put the EF6 context and model classes in a class library project that targets the full framework.</span></span> <span data-ttu-id="f7e31-110">Добавьте ссылку на библиотеку классов из проекта ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f7e31-110">Add a reference to the class library from the ASP.NET Core project.</span></span> <span data-ttu-id="f7e31-111">См. пример [решения Visual Studio с проектами EF6 и ASP.NET Core](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/).</span><span class="sxs-lookup"><span data-stu-id="f7e31-111">See the sample [Visual Studio solution with EF6 and ASP.NET Core projects](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/).</span></span>

<span data-ttu-id="f7e31-112">Контекст EF6 нельзя поместить в проект ASP.NET Core, поскольку проекты .NET Core поддерживают не все функции, используемые командами EF6, например *Enable-Migrations*.</span><span class="sxs-lookup"><span data-stu-id="f7e31-112">You can't put an EF6 context in an ASP.NET Core project because .NET Core projects don't support all of the functionality that EF6 commands such as *Enable-Migrations* require.</span></span>

<span data-ttu-id="f7e31-113">Независимо от типа проекта, в котором размещается контекст EF6, в этом контексте работают только средства командной строки EF6.</span><span class="sxs-lookup"><span data-stu-id="f7e31-113">Regardless of project type in which you locate your EF6 context, only EF6 command-line tools work with an EF6 context.</span></span> <span data-ttu-id="f7e31-114">Например, команда `Scaffold-DbContext` доступна только в Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="f7e31-114">For example, `Scaffold-DbContext` is only available in Entity Framework Core.</span></span> <span data-ttu-id="f7e31-115">Дополнительные сведения о реконструировании базы данных в модель EF6 см. в разделе [Code First для существующей базы данных](https://msdn.microsoft.com/jj200620).</span><span class="sxs-lookup"><span data-stu-id="f7e31-115">If you need to do reverse engineering of a database into an EF6 model, see [Code First to an Existing Database](https://msdn.microsoft.com/jj200620).</span></span>

## <a name="reference-full-framework-and-ef6-in-the-aspnet-core-project"></a><span data-ttu-id="f7e31-116">Использование ссылок на полную платформу и EF6 в проекте ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f7e31-116">Reference full framework and EF6 in the ASP.NET Core project</span></span>

<span data-ttu-id="f7e31-117">В проекте ASP.NET Core необходимо использовать ссылки на платформу .NET Framework и EF6.</span><span class="sxs-lookup"><span data-stu-id="f7e31-117">Your ASP.NET Core project needs to reference .NET framework and EF6.</span></span> <span data-ttu-id="f7e31-118">Например, файл *CSPROJ* вашего проекта ASP.NET Core будет иметь вид, схожий с показанным в следующем примере (показаны только соответствующие части файла).</span><span class="sxs-lookup"><span data-stu-id="f7e31-118">For example, the *.csproj* file of your ASP.NET Core project will look similar to the following example (only relevant parts of the file are shown).</span></span>

[!code-xml[](entity-framework-6/sample/MVCCore/MVCCore.csproj?range=3-9&highlight=2)]

<span data-ttu-id="f7e31-119">При создании нового проекта используйте шаблон **Веб-приложение ASP.NET Core (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f7e31-119">When creating a new project, use the **ASP.NET Core Web Application (.NET Framework)** template.</span></span>

## <a name="handle-connection-strings"></a><span data-ttu-id="f7e31-120">Обработка строк подключения</span><span class="sxs-lookup"><span data-stu-id="f7e31-120">Handle connection strings</span></span>

<span data-ttu-id="f7e31-121">Средства командной строки EF6, которые используются в проекте библиотеки классов EF6, требуют наличия конструктора по умолчанию, с помощью которого они могут создавать экземпляр контекста.</span><span class="sxs-lookup"><span data-stu-id="f7e31-121">The EF6 command-line tools that you'll use in the EF6 class library project require a default constructor so they can instantiate the context.</span></span> <span data-ttu-id="f7e31-122">Тем не менее, возможно, вам потребуется задать строку подключения для использования в проекте ASP.NET Core. В этом случае конструктор контекста должен иметь параметр, в котором передается строка подключения.</span><span class="sxs-lookup"><span data-stu-id="f7e31-122">But you'll probably want to specify the connection string to use in the ASP.NET Core project, in which case your context constructor must have a parameter that lets you pass in the connection string.</span></span> <span data-ttu-id="f7e31-123">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="f7e31-123">Here's an example.</span></span>

[!code-csharp[](entity-framework-6/sample/EF6/SchoolContext.cs?name=snippet_Constructor)]

<span data-ttu-id="f7e31-124">Поскольку в контексте EF6 отсутствует конструктор без параметров, в проекте EF6 необходимо предоставить реализацию [IDbContextFactory](https://msdn.microsoft.com/library/hh506876).</span><span class="sxs-lookup"><span data-stu-id="f7e31-124">Since your EF6 context doesn't have a parameterless constructor, your EF6 project has to provide an implementation of [IDbContextFactory](https://msdn.microsoft.com/library/hh506876).</span></span> <span data-ttu-id="f7e31-125">Средства командной строки EF6 будут находить и использовать эту реализацию для создания экземпляра контекста.</span><span class="sxs-lookup"><span data-stu-id="f7e31-125">The EF6 command-line tools will find and use that implementation so they can instantiate the context.</span></span> <span data-ttu-id="f7e31-126">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="f7e31-126">Here's an example.</span></span>

[!code-csharp[](entity-framework-6/sample/EF6/SchoolContextFactory.cs?name=snippet_IDbContextFactory)]

<span data-ttu-id="f7e31-127">В этом примере кода реализация `IDbContextFactory` передает жестко запрограммированную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="f7e31-127">In this sample code, the `IDbContextFactory` implementation passes in a hard-coded connection string.</span></span> <span data-ttu-id="f7e31-128">Эта строка подключения будет использоваться средствами командной строки.</span><span class="sxs-lookup"><span data-stu-id="f7e31-128">This is the connection string that the command-line tools will use.</span></span> <span data-ttu-id="f7e31-129">В некоторых случаях требуется реализовать стратегию, в которой библиотека классов использует ту же строку подключения, что и вызывающее приложение.</span><span class="sxs-lookup"><span data-stu-id="f7e31-129">You'll want to implement a strategy to ensure that the class library uses the same connection string that the calling application uses.</span></span> <span data-ttu-id="f7e31-130">Например, вы можете получать значение из переменной среды в обоих проектах.</span><span class="sxs-lookup"><span data-stu-id="f7e31-130">For example, you could get the value from an environment variable in both projects.</span></span>

## <a name="set-up-dependency-injection-in-the-aspnet-core-project"></a><span data-ttu-id="f7e31-131">Настройка внедрения зависимостей в проекте ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f7e31-131">Set up dependency injection in the ASP.NET Core project</span></span>

<span data-ttu-id="f7e31-132">В файле *Startup.cs* проекта Core настройте контекст EF6 для внедрения зависимостей в `ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="f7e31-132">In the Core project's *Startup.cs* file, set up the EF6 context for dependency injection (DI) in `ConfigureServices`.</span></span> <span data-ttu-id="f7e31-133">Объекты контекста EF должны иметь время существования, соответствующее запросу.</span><span class="sxs-lookup"><span data-stu-id="f7e31-133">EF context objects should be scoped for a per-request lifetime.</span></span>

[!code-csharp[](entity-framework-6/sample/MVCCore/Startup.cs?name=snippet_ConfigureServices&highlight=5)]

<span data-ttu-id="f7e31-134">После этого можно получить экземпляр контекста в контроллерах посредством внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="f7e31-134">You can then get an instance of the context in your controllers by using DI.</span></span> <span data-ttu-id="f7e31-135">Этот код похож на тот, который вы написали для контекста EF Core:</span><span class="sxs-lookup"><span data-stu-id="f7e31-135">The code is similar to what you'd write for an EF Core context:</span></span>

[!code-csharp[](entity-framework-6/sample/MVCCore/Controllers/StudentsController.cs?name=snippet_ContextInController)]

## <a name="sample-application"></a><span data-ttu-id="f7e31-136">Пример приложения</span><span class="sxs-lookup"><span data-stu-id="f7e31-136">Sample application</span></span>

<span data-ttu-id="f7e31-137">Рабочий пример приложения см. в разделе [пример решения Visual Studio](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/), который прилагается к этой статье.</span><span class="sxs-lookup"><span data-stu-id="f7e31-137">For a working sample application, see the [sample Visual Studio solution](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/) that accompanies this article.</span></span>

<span data-ttu-id="f7e31-138">Этот пример можно создать с нуля, выполнив следующие действия в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f7e31-138">This sample can be created from scratch by the following steps in Visual Studio:</span></span>

* <span data-ttu-id="f7e31-139">Создайте решение.</span><span class="sxs-lookup"><span data-stu-id="f7e31-139">Create a solution.</span></span>

* <span data-ttu-id="f7e31-140">**Создать** > **Новый проект** > **Веб** > **Веб-приложение ASP.NET Core**</span><span class="sxs-lookup"><span data-stu-id="f7e31-140">**Add** > **New Project** > **Web** > **ASP.NET Core Web Application**</span></span>
  * <span data-ttu-id="f7e31-141">В диалоговом окне для выбора шаблона проекта укажите версию API и .NET Framework в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="f7e31-141">In project template selection dialog, select API and .NET Framework in dropdown</span></span>

* <span data-ttu-id="f7e31-142">**Создать** > **Новый проект** > **Классическое приложение для Windows** > **Библиотека классов (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="f7e31-142">**Add** > **New Project** > **Windows Desktop** > **Class Library (.NET Framework)**</span></span>

* <span data-ttu-id="f7e31-143">В **консоли диспетчера пакетов** для обоих проектов выполните команду `Install-Package Entityframework`.</span><span class="sxs-lookup"><span data-stu-id="f7e31-143">In **Package Manager Console** (PMC) for both projects, run the command `Install-Package Entityframework`.</span></span>

* <span data-ttu-id="f7e31-144">В проекте библиотеки классов создайте классы модели данных и класс контекста, а также реализацию `IDbContextFactory`.</span><span class="sxs-lookup"><span data-stu-id="f7e31-144">In the class library project, create data model classes and a context class, and an implementation of `IDbContextFactory`.</span></span>

* <span data-ttu-id="f7e31-145">В консоли диспетчера пакетов для проекта библиотеки классов выполните команды `Enable-Migrations` и `Add-Migration Initial`.</span><span class="sxs-lookup"><span data-stu-id="f7e31-145">In PMC for the class library project, run the commands `Enable-Migrations` and `Add-Migration Initial`.</span></span> <span data-ttu-id="f7e31-146">Если проект ASP.NET Core настроен как запускаемый, добавьте `-StartupProjectName EF6` в эти команды.</span><span class="sxs-lookup"><span data-stu-id="f7e31-146">If you have set the ASP.NET Core project as the startup project, add `-StartupProjectName EF6` to these commands.</span></span>

* <span data-ttu-id="f7e31-147">В проекте Core добавьте ссылку на проект библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="f7e31-147">In the Core project, add a project reference to the class library project.</span></span>

* <span data-ttu-id="f7e31-148">В проекте Core в файле *Startup.cs* зарегистрируйте контекст для внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="f7e31-148">In the Core project, in *Startup.cs*, register the context for DI.</span></span>

* <span data-ttu-id="f7e31-149">В проекте Core в файле *appsettings.json* добавьте строку подключения.</span><span class="sxs-lookup"><span data-stu-id="f7e31-149">In the Core project, in *appsettings.json*, add the connection string.</span></span>

* <span data-ttu-id="f7e31-150">В проекте Core добавьте контроллер и представление (или представления), чтобы проверить возможность чтения и записи данных.</span><span class="sxs-lookup"><span data-stu-id="f7e31-150">In the Core project, add a controller and view(s) to verify that you can read and write data.</span></span> <span data-ttu-id="f7e31-151">(Обратите внимание, что функция формирования шаблонов ASP.NET Core MVC не будет работать с контекстом EF6, на который указывает ссылка из библиотеки классов.)</span><span class="sxs-lookup"><span data-stu-id="f7e31-151">(Note that ASP.NET Core MVC scaffolding won't work with the EF6 context referenced from the class library.)</span></span>

## <a name="summary"></a><span data-ttu-id="f7e31-152">Сводка</span><span class="sxs-lookup"><span data-stu-id="f7e31-152">Summary</span></span>

<span data-ttu-id="f7e31-153">В этой статье приводятся общие рекомендации по использованию платформы Entity Framework 6 в приложении ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f7e31-153">This article has provided basic guidance for using Entity Framework 6 in an ASP.NET Core application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7e31-154">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f7e31-154">Additional resources</span></span>

* [<span data-ttu-id="f7e31-155">Entity Framework — конфигурация на основе кода</span><span class="sxs-lookup"><span data-stu-id="f7e31-155">Entity Framework - Code-Based Configuration</span></span>](https://msdn.microsoft.com/data/jj680699.aspx)
