---
title: Внедрение зависимостей в представления в ASP.NET Core
author: ardalis
description: Узнайте, как ASP.NET Core поддерживает внедрение зависимостей в представления MVC.
ms.author: riande
ms.date: 10/14/2016
uid: mvc/views/dependency-injection
ms.openlocfilehash: dfadafe9ebb5799b45ef68653f20c5fc1a2506b5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025461"
---
# <a name="dependency-injection-into-views-in-aspnet-core"></a><span data-ttu-id="bd375-103">Внедрение зависимостей в представления в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bd375-103">Dependency injection into views in ASP.NET Core</span></span>

<span data-ttu-id="bd375-104">Автор: [Стив Смит](https://ardalis.com/) (Steve Smith)</span><span class="sxs-lookup"><span data-stu-id="bd375-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="bd375-105">ASP.NET Core поддерживает [внедрение зависимостей](xref:fundamentals/dependency-injection) в представления.</span><span class="sxs-lookup"><span data-stu-id="bd375-105">ASP.NET Core supports [dependency injection](xref:fundamentals/dependency-injection) into views.</span></span> <span data-ttu-id="bd375-106">Это может быть полезно для связанных с представлениями служб (например, локализации) или данных, необходимых только для заполнения элементов представления.</span><span class="sxs-lookup"><span data-stu-id="bd375-106">This can be useful for view-specific services, such as localization or data required only for populating view elements.</span></span> <span data-ttu-id="bd375-107">Старайтесь поддерживать [разделение ответственности](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) между контроллерами и представлениями.</span><span class="sxs-lookup"><span data-stu-id="bd375-107">You should try to maintain [separation of concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) between your controllers and views.</span></span> <span data-ttu-id="bd375-108">Большая часть данных, отображаемых представлениями, должна передаваться от контроллера.</span><span class="sxs-lookup"><span data-stu-id="bd375-108">Most of the data your views display should be passed in from the controller.</span></span>

<span data-ttu-id="bd375-109">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/dependency-injection/sample) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="bd375-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/dependency-injection/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="a-simple-example"></a><span data-ttu-id="bd375-110">Простой пример</span><span class="sxs-lookup"><span data-stu-id="bd375-110">A Simple Example</span></span>

<span data-ttu-id="bd375-111">Вы можете внедрить в представление службу с помощью директивы `@inject`.</span><span class="sxs-lookup"><span data-stu-id="bd375-111">You can inject a service into a view using the `@inject` directive.</span></span> <span data-ttu-id="bd375-112">По сути, `@inject` добавляет в представление свойство и заполняет это свойство с помощью внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="bd375-112">You can think of `@inject` as adding a property to your view, and populating the property using DI.</span></span>

<span data-ttu-id="bd375-113">Синтаксис для `@inject`: `@inject <type> <name>`</span><span class="sxs-lookup"><span data-stu-id="bd375-113">The syntax for `@inject`: `@inject <type> <name>`</span></span>

<span data-ttu-id="bd375-114">Пример `@inject` в действии:</span><span class="sxs-lookup"><span data-stu-id="bd375-114">An example of `@inject` in action:</span></span>

[!code-csharp[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Views/ToDo/Index.cshtml?highlight=4,5,15,16,17)]

<span data-ttu-id="bd375-115">Это представление отображает список экземпляров `ToDoItem`, а также сводку по общей статистике.</span><span class="sxs-lookup"><span data-stu-id="bd375-115">This view displays a list of `ToDoItem` instances, along with a summary showing overall statistics.</span></span> <span data-ttu-id="bd375-116">Сводка заполняется из внедренного `StatisticsService`.</span><span class="sxs-lookup"><span data-stu-id="bd375-116">The summary is populated from the injected `StatisticsService`.</span></span> <span data-ttu-id="bd375-117">Эта служба регистрируется для внедрения зависимости в `ConfigureServices` в файле *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="bd375-117">This service is registered for dependency injection in `ConfigureServices` in *Startup.cs*:</span></span>

[!code-csharp[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Startup.cs?highlight=6,7&range=15-22)]

<span data-ttu-id="bd375-118">Функция `StatisticsService` выполняет ряд вычислений с набором экземпляров `ToDoItem`, к которым она обращается через репозиторий:</span><span class="sxs-lookup"><span data-stu-id="bd375-118">The `StatisticsService` performs some calculations on the set of `ToDoItem` instances, which it accesses via a repository:</span></span>

[!code-csharp[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Model/Services/StatisticsService.cs?highlight=15,20,25)]

<span data-ttu-id="bd375-119">Пример репозитория использует коллекцию в памяти.</span><span class="sxs-lookup"><span data-stu-id="bd375-119">The sample repository uses an in-memory collection.</span></span> <span data-ttu-id="bd375-120">Представленная выше реализация (работающая со всеми данными в памяти) не рекомендуется для больших наборов данных с удаленным доступом.</span><span class="sxs-lookup"><span data-stu-id="bd375-120">The implementation shown above (which operates on all of the data in memory) isn't recommended for large, remotely accessed data sets.</span></span>

<span data-ttu-id="bd375-121">Пример показывает данные из модели, привязанной к представлению, и из внедренной в представление службы:</span><span class="sxs-lookup"><span data-stu-id="bd375-121">The sample displays data from the model bound to the view and the service injected into the view:</span></span>

![Список дел к выполнению, показывающий общее количество пунктов, число выполненных пунктов, средний показатель приоритета, а также список задач с их уровнями приоритета и логическими значениями, характеризующими выполнение.](dependency-injection/_static/screenshot.png)

## <a name="populating-lookup-data"></a><span data-ttu-id="bd375-123">Заполнение данных подстановки</span><span class="sxs-lookup"><span data-stu-id="bd375-123">Populating Lookup Data</span></span>

<span data-ttu-id="bd375-124">Внедрение в представление можно использовать для заполнения параметров в элементах пользовательского интерфейса, например в раскрывающихся списках.</span><span class="sxs-lookup"><span data-stu-id="bd375-124">View injection can be useful to populate options in UI elements, such as dropdown lists.</span></span> <span data-ttu-id="bd375-125">Рассмотрим форму профиля пользователя, содержащую параметры для указания пола, штата и другие свойства.</span><span class="sxs-lookup"><span data-stu-id="bd375-125">Consider a user profile form that includes options for specifying gender, state, and other preferences.</span></span> <span data-ttu-id="bd375-126">Для отрисовки такой формы в стандартном подходе MVC контроллеру нужно будет запрашивать каждый из этих наборов параметров в службах доступа к данным, а затем заполнять привязываемыми наборами модель или `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="bd375-126">Rendering such a form using a standard MVC approach would require the controller to request data access services for each of these sets of options, and then populate a model or `ViewBag` with each set of options to be bound.</span></span>

<span data-ttu-id="bd375-127">Альтернативный вариант получения параметров заключается во внедрении служб непосредственно в представление.</span><span class="sxs-lookup"><span data-stu-id="bd375-127">An alternative approach injects services directly into the view to obtain the options.</span></span> <span data-ttu-id="bd375-128">В этом случае необходимый контроллеру код сводится к минимуму, так как логика создания элемента представления помещается в само представление.</span><span class="sxs-lookup"><span data-stu-id="bd375-128">This minimizes the amount of code required by the controller, moving this view element construction logic into the view itself.</span></span> <span data-ttu-id="bd375-129">Действие контроллера по отображению формы редактирования профиля должно только передать форму экземпляру профиля:</span><span class="sxs-lookup"><span data-stu-id="bd375-129">The controller action to display a profile editing form only needs to pass the form the profile instance:</span></span>

[!code-csharp[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Controllers/ProfileController.cs?highlight=9,19)]

<span data-ttu-id="bd375-130">HTML-форма, используемая для изменения этих свойств, содержит для трех свойств раскрывающиеся списки:</span><span class="sxs-lookup"><span data-stu-id="bd375-130">The HTML form used to update these preferences includes dropdown lists for three of the properties:</span></span>

![Представление редактирования профиля с формой для ввода имени, пола, штата и любимого цвета.](dependency-injection/_static/updateprofile.png)

<span data-ttu-id="bd375-132">Эти списки заполняются службой, которая внедрена в представление:</span><span class="sxs-lookup"><span data-stu-id="bd375-132">These lists are populated by a service that has been injected into the view:</span></span>

[!code-cshtml[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Views/Profile/Index.cshtml?highlight=4,16,17,21,22,26,27)]

<span data-ttu-id="bd375-133">`ProfileOptionsService` — это работающая на уровне пользовательского интерфейса служба, которая предоставляет именно те данные, которые нужны в этой форме:</span><span class="sxs-lookup"><span data-stu-id="bd375-133">The `ProfileOptionsService` is a UI-level service designed to provide just the data needed for this form:</span></span>

[!code-csharp[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Model/Services/ProfileOptionsService.cs?highlight=7,13,24)]

> [!IMPORTANT]
> <span data-ttu-id="bd375-134">Не забудьте зарегистрировать типы, которые вы будете запрашивать через внедрение зависимостей в методе `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="bd375-134">Don't forget to register types you request through dependency injection in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="bd375-135">Незарегистрированный тип создает исключение в среде выполнения, так как поставщик услуг получает внутренние запросы через [GetRequiredService](/dotnet/api/microsoft.extensions.dependencyinjection.serviceproviderserviceextensions.getrequiredservice).</span><span class="sxs-lookup"><span data-stu-id="bd375-135">An unregistered type throws an exception at runtime because the service provider is internally queried via [GetRequiredService](/dotnet/api/microsoft.extensions.dependencyinjection.serviceproviderserviceextensions.getrequiredservice).</span></span>

## <a name="overriding-services"></a><span data-ttu-id="bd375-136">Переопределение служб</span><span class="sxs-lookup"><span data-stu-id="bd375-136">Overriding Services</span></span>

<span data-ttu-id="bd375-137">Помимо добавления новых служб, этот метод также позволяет переопределять ранее добавленные службы на странице.</span><span class="sxs-lookup"><span data-stu-id="bd375-137">In addition to injecting new services, this technique can also be used to override previously injected services on a page.</span></span> <span data-ttu-id="bd375-138">На следующем рисунке показаны все доступные поля на странице, используемой в первом примере:</span><span class="sxs-lookup"><span data-stu-id="bd375-138">The figure below shows all of the fields available on the page used in the first example:</span></span>

![Контекстное меню IntelliSense к введенному символу @ с полями Html, Component, StatsService и Url](dependency-injection/_static/razor-fields.png)

<span data-ttu-id="bd375-140">Как видно, полями по умолчанию являются `Html`, `Component` и `Url` (а также внедренное нами поле `StatsService`).</span><span class="sxs-lookup"><span data-stu-id="bd375-140">As you can see, the default fields include `Html`, `Component`, and `Url` (as well as the `StatsService` that we injected).</span></span> <span data-ttu-id="bd375-141">Если, например, нужно заменить вспомогательные методы HTML на собственные, вы можете легко сделать это с помощью `@inject`:</span><span class="sxs-lookup"><span data-stu-id="bd375-141">If for instance you wanted to replace the default HTML Helpers with your own, you could easily do so using `@inject`:</span></span>

[!code-cshtml[](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Views/Helper/Index.cshtml?highlight=3,11)]

<span data-ttu-id="bd375-142">При необходимости расширить существующие службы вы можете просто применять этот метод при наследовании от существующей реализации или использовании ее внутри вашей собственной.</span><span class="sxs-lookup"><span data-stu-id="bd375-142">If you want to extend existing services, you can simply use this technique while inheriting from or wrapping the existing implementation with your own.</span></span>

## <a name="see-also"></a><span data-ttu-id="bd375-143">См. также</span><span class="sxs-lookup"><span data-stu-id="bd375-143">See Also</span></span>

* <span data-ttu-id="bd375-144">Блог Саймона Тиммса (Simon Timms): [Getting Lookup Data Into Your View](http://blog.simontimms.com/2015/06/09/getting-lookup-data-into-you-view/) (Внедрение данных подстановки в ваше представление)</span><span class="sxs-lookup"><span data-stu-id="bd375-144">Simon Timms Blog: [Getting Lookup Data Into Your View](http://blog.simontimms.com/2015/06/09/getting-lookup-data-into-you-view/)</span></span>
