---
title: Просмотр компонентов в ASP.NET Core
author: rick-anderson
description: Узнайте, как компоненты представления используются в ASP.NET Core и как добавить их в приложения.
ms.author: riande
ms.date: 1/30/2019
uid: mvc/views/view-components
ms.openlocfilehash: d979c9480f7bffff993f0ea526bdc231b940baa2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049881"
---
# <a name="view-components-in-aspnet-core"></a><span data-ttu-id="18ad8-103">Просмотр компонентов в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="18ad8-103">View components in ASP.NET Core</span></span>

<span data-ttu-id="18ad8-104">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="18ad8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="18ad8-105">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="18ad8-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="view-components"></a><span data-ttu-id="18ad8-106">Компоненты представлений</span><span class="sxs-lookup"><span data-stu-id="18ad8-106">View components</span></span>

<span data-ttu-id="18ad8-107">Компоненты представлений похожи на частичные представления, но при этом гораздо функциональнее.</span><span class="sxs-lookup"><span data-stu-id="18ad8-107">View components are similar to partial views, but they're much more powerful.</span></span> <span data-ttu-id="18ad8-108">Компоненты представлений не используют привязку модели и зависят только от данных, предоставляемых при их вызове.</span><span class="sxs-lookup"><span data-stu-id="18ad8-108">View components don't use model binding, and only depend on the data provided when calling into it.</span></span> <span data-ttu-id="18ad8-109">Эта статья написана с помощью контроллеров и представлений, но компоненты представлений работают и в Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="18ad8-109">This article was written using controllers and views, but view components also work with Razor Pages.</span></span>

<span data-ttu-id="18ad8-110">Компонент представлений:</span><span class="sxs-lookup"><span data-stu-id="18ad8-110">A view component:</span></span>

* <span data-ttu-id="18ad8-111">Выполняет отрисовку фрагмента, а не всего отклика.</span><span class="sxs-lookup"><span data-stu-id="18ad8-111">Renders a chunk rather than a whole response.</span></span>
* <span data-ttu-id="18ad8-112">Включает те же преимущества разделения функций и тестирования, которые доступны между контроллером и представлением.</span><span class="sxs-lookup"><span data-stu-id="18ad8-112">Includes the same separation-of-concerns and testability benefits found between a controller and view.</span></span>
* <span data-ttu-id="18ad8-113">Может иметь параметры и бизнес-логику.</span><span class="sxs-lookup"><span data-stu-id="18ad8-113">Can have parameters and business logic.</span></span>
* <span data-ttu-id="18ad8-114">Обычно вызывается со страницы макета.</span><span class="sxs-lookup"><span data-stu-id="18ad8-114">Is typically invoked from a layout page.</span></span>

<span data-ttu-id="18ad8-115">Компоненты представлений предназначены для случаев, когда имеется многоразовая логика отрисовки, которая слишком сложна для частичного представления, например:</span><span class="sxs-lookup"><span data-stu-id="18ad8-115">View components are intended anywhere you have reusable rendering logic that's too complex for a partial view, such as:</span></span>

* <span data-ttu-id="18ad8-116">Динамические меню навигации</span><span class="sxs-lookup"><span data-stu-id="18ad8-116">Dynamic navigation menus</span></span>
* <span data-ttu-id="18ad8-117">Облако тегов (где выполняется запрос к базе данных)</span><span class="sxs-lookup"><span data-stu-id="18ad8-117">Tag cloud (where it queries the database)</span></span>
* <span data-ttu-id="18ad8-118">Панель входа</span><span class="sxs-lookup"><span data-stu-id="18ad8-118">Login panel</span></span>
* <span data-ttu-id="18ad8-119">Корзина для покупок</span><span class="sxs-lookup"><span data-stu-id="18ad8-119">Shopping cart</span></span>
* <span data-ttu-id="18ad8-120">Недавно опубликованные статьи</span><span class="sxs-lookup"><span data-stu-id="18ad8-120">Recently published articles</span></span>
* <span data-ttu-id="18ad8-121">Содержимое боковой панели в типичном блоге</span><span class="sxs-lookup"><span data-stu-id="18ad8-121">Sidebar content on a typical blog</span></span>
* <span data-ttu-id="18ad8-122">Панель входа, которая должна отображаться на каждой странице и содержит ссылки для выхода или входа в зависимости от состояния входа пользователя</span><span class="sxs-lookup"><span data-stu-id="18ad8-122">A login panel that would be rendered on every page and show either the links to log out or log in, depending on the log in state of the user</span></span>

<span data-ttu-id="18ad8-123">Компонент представления состоит из двух частей: класса (обычно производного от [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)) и возвращаемого результата (обычно это представление).</span><span class="sxs-lookup"><span data-stu-id="18ad8-123">A view component consists of two parts: the class (typically derived from [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)) and the result it returns (typically a view).</span></span> <span data-ttu-id="18ad8-124">Как и контроллеры, компонент представления может быть объектом POCO, но большинству разработчиков потребуются преимущества методов и свойств, доступные при наследовании от `ViewComponent`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-124">Like controllers, a view component can be a POCO, but most developers will want to take advantage of the methods and properties available by deriving from `ViewComponent`.</span></span>

## <a name="creating-a-view-component"></a><span data-ttu-id="18ad8-125">Создание компонента представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-125">Creating a view component</span></span>

<span data-ttu-id="18ad8-126">Этот раздел содержит общие требования к созданию компонента представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-126">This section contains the high-level requirements to create a view component.</span></span> <span data-ttu-id="18ad8-127">Далее в этой статье мы подробно рассмотрим каждый шаг и создадим компонент представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-127">Later in the article, we'll examine each step in detail and create a view component.</span></span>

### <a name="the-view-component-class"></a><span data-ttu-id="18ad8-128">Класс компонентов представлений</span><span class="sxs-lookup"><span data-stu-id="18ad8-128">The view component class</span></span>

<span data-ttu-id="18ad8-129">Класс компонентов представлений можно создать одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="18ad8-129">A view component class can be created by any of the following:</span></span>

* <span data-ttu-id="18ad8-130">Наследование от *ViewComponent*</span><span class="sxs-lookup"><span data-stu-id="18ad8-130">Deriving from *ViewComponent*</span></span>
* <span data-ttu-id="18ad8-131">Декорирование класса с помощью атрибута `[ViewComponent]` или наследование от класса с помощью атрибута `[ViewComponent]`</span><span class="sxs-lookup"><span data-stu-id="18ad8-131">Decorating a class with the `[ViewComponent]` attribute, or deriving from a class with the `[ViewComponent]` attribute</span></span>
* <span data-ttu-id="18ad8-132">Создание класса, где имя заканчивается суффиксом *ViewComponent*</span><span class="sxs-lookup"><span data-stu-id="18ad8-132">Creating a class where the name ends with the suffix *ViewComponent*</span></span>

<span data-ttu-id="18ad8-133">Как и контроллеры, компоненты представлений должны быть открытыми, невложенными и неабстрактными классами.</span><span class="sxs-lookup"><span data-stu-id="18ad8-133">Like controllers, view components must be public, non-nested, and non-abstract classes.</span></span> <span data-ttu-id="18ad8-134">Имя компонента представления — это имя класса с удаленным суффиксом "ViewComponent".</span><span class="sxs-lookup"><span data-stu-id="18ad8-134">The view component name is the class name with the "ViewComponent" suffix removed.</span></span> <span data-ttu-id="18ad8-135">Его можно также можно задать явно с помощью свойства `ViewComponentAttribute.Name`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-135">It can also be explicitly specified using the `ViewComponentAttribute.Name` property.</span></span>

<span data-ttu-id="18ad8-136">Класс компонентов представлений:</span><span class="sxs-lookup"><span data-stu-id="18ad8-136">A view component class:</span></span>

* <span data-ttu-id="18ad8-137">Полностью поддерживает [внедрение зависимостей](../../fundamentals/dependency-injection.md) в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="18ad8-137">Fully supports constructor [dependency injection](../../fundamentals/dependency-injection.md)</span></span>

* <span data-ttu-id="18ad8-138">Не участвует в жизненном цикле контроллера, поэтому в компоненте представления невозможно использовать [фильтры](../controllers/filters.md).</span><span class="sxs-lookup"><span data-stu-id="18ad8-138">Doesn't take part in the controller lifecycle, which means you can't use [filters](../controllers/filters.md) in a view component</span></span>

### <a name="view-component-methods"></a><span data-ttu-id="18ad8-139">Методы компонентов представлений</span><span class="sxs-lookup"><span data-stu-id="18ad8-139">View component methods</span></span>

<span data-ttu-id="18ad8-140">Компонент представления задает свою логику в методе `InvokeAsync`, возвращающем `Task<IViewComponentResult>`, или в синхронном методе `Invoke`, который возвращает `IViewComponentResult`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-140">A view component defines its logic in an `InvokeAsync` method that returns a `Task<IViewComponentResult>` or in a synchronous `Invoke` method that returns an `IViewComponentResult`.</span></span> <span data-ttu-id="18ad8-141">Параметры берутся непосредственно из вызова компонента представления, а не из привязки модели.</span><span class="sxs-lookup"><span data-stu-id="18ad8-141">Parameters come directly from invocation of the view component, not from model binding.</span></span> <span data-ttu-id="18ad8-142">Компонент представления никогда не обрабатывает запрос напрямую.</span><span class="sxs-lookup"><span data-stu-id="18ad8-142">A view component never directly handles a request.</span></span> <span data-ttu-id="18ad8-143">Как правило, компонент представления инициализирует модель и передает ее в представление, вызвав метод `View`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-143">Typically, a view component initializes a model and passes it to a view by calling the `View` method.</span></span> <span data-ttu-id="18ad8-144">Если кратко, методы компонентов представлений:</span><span class="sxs-lookup"><span data-stu-id="18ad8-144">In summary, view component methods:</span></span>

* <span data-ttu-id="18ad8-145">Определяют метод `InvokeAsync`, который возвращает `Task<IViewComponentResult>`, или синхронный метод `Invoke`, возвращающий `IViewComponentResult`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-145">Define an `InvokeAsync` method that returns a `Task<IViewComponentResult>` or a synchronous `Invoke` method that returns an `IViewComponentResult`.</span></span>
* <span data-ttu-id="18ad8-146">Обычно инициализируют модель и передают ее в представление, вызвав метод `ViewComponent` `View`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-146">Typically initializes a model and passes it to a view by calling the `ViewComponent` `View` method.</span></span>
* <span data-ttu-id="18ad8-147">Получают параметры из вызывающего метода, а не HTTP.</span><span class="sxs-lookup"><span data-stu-id="18ad8-147">Parameters come from the calling method, not HTTP.</span></span> <span data-ttu-id="18ad8-148">Это связано с тем, что привязка модели отсутствует.</span><span class="sxs-lookup"><span data-stu-id="18ad8-148">There's no model binding.</span></span>
* <span data-ttu-id="18ad8-149">Недоступны непосредственно в качестве конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="18ad8-149">Are not reachable directly as an HTTP endpoint.</span></span> <span data-ttu-id="18ad8-150">Вызываются из кода (обычно в представлении).</span><span class="sxs-lookup"><span data-stu-id="18ad8-150">They're invoked from your code (usually in a view).</span></span> <span data-ttu-id="18ad8-151">Компонент представления никогда не обрабатывает запрос.</span><span class="sxs-lookup"><span data-stu-id="18ad8-151">A view component never handles a request.</span></span>
* <span data-ttu-id="18ad8-152">Перегружаются по сигнатуре, а не по сведениям из текущего HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="18ad8-152">Are overloaded on the signature rather than any details from the current HTTP request.</span></span>

### <a name="view-search-path"></a><span data-ttu-id="18ad8-153">Путь поиска представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-153">View search path</span></span>

<span data-ttu-id="18ad8-154">Среда выполнения ищет представление по следующим путям:</span><span class="sxs-lookup"><span data-stu-id="18ad8-154">The runtime searches for the view in the following paths:</span></span>

* <span data-ttu-id="18ad8-155">/Views/{Имя контроллера}/Components/{Имя компонента представления}/{Имя представления}</span><span class="sxs-lookup"><span data-stu-id="18ad8-155">/Views/{Controller Name}/Components/{View Component Name}/{View Name}</span></span>
* <span data-ttu-id="18ad8-156">/Views/Shared/Components/{Имя компонента представления}/{Имя представления}</span><span class="sxs-lookup"><span data-stu-id="18ad8-156">/Views/Shared/Components/{View Component Name}/{View Name}</span></span>
* <span data-ttu-id="18ad8-157">/Pages/Shared/Components/{Имя компонента представления}/{Имя представления}</span><span class="sxs-lookup"><span data-stu-id="18ad8-157">/Pages/Shared/Components/{View Component Name}/{View Name}</span></span>

<span data-ttu-id="18ad8-158">Путь поиска применяется к проектам с помощью контроллеров и представлений, а также Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="18ad8-158">The search path applies to projects using controllers + views and Razor Pages.</span></span>

<span data-ttu-id="18ad8-159">По умолчанию для компонента представления используется имя *Default*, то есть файл представления обычно называется *Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-159">The default view name for a view component is *Default*, which means your view file will typically be named *Default.cshtml*.</span></span> <span data-ttu-id="18ad8-160">При создании результата компонента представления или при вызове метода `View` можно указать другое имя представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-160">You can specify a different view name when creating the view component result or when calling the `View` method.</span></span>

<span data-ttu-id="18ad8-161">Мы рекомендуем назвать файл представления *Default.cshtml* и использовать путь *Views/Shared/Components/{Имя компонента представления}/{Имя представления}*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-161">We recommend you name the view file *Default.cshtml* and use the *Views/Shared/Components/{View Component Name}/{View Name}* path.</span></span> <span data-ttu-id="18ad8-162">Компонент представления `PriorityList` в этом примере использует представление компонента представления *Views/Shared/Components/PriorityList/Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-162">The `PriorityList` view component used in this sample uses *Views/Shared/Components/PriorityList/Default.cshtml* for the view component view.</span></span>

## <a name="invoking-a-view-component"></a><span data-ttu-id="18ad8-163">Вызов компонента представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-163">Invoking a view component</span></span>

<span data-ttu-id="18ad8-164">Чтобы использовать компонент представления, вызовите следующий код внутри представления:</span><span class="sxs-lookup"><span data-stu-id="18ad8-164">To use the view component, call the following inside a view:</span></span>

```cshtml
@await Component.InvokeAsync("Name of view component", {Anonymous Type Containing Parameters})
```

<span data-ttu-id="18ad8-165">Эти параметры передаются в метод `InvokeAsync`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-165">The parameters will be passed to the `InvokeAsync` method.</span></span> <span data-ttu-id="18ad8-166">Компонент представления `PriorityList`, разрабатываемый в рамках этой статьи, вызывается из файла представления *Views/ToDo/Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-166">The `PriorityList` view component developed in the article is invoked from the *Views/ToDo/Index.cshtml* view file.</span></span> <span data-ttu-id="18ad8-167">Следующий код вызывает метод `InvokeAsync` с двумя параметрами:</span><span class="sxs-lookup"><span data-stu-id="18ad8-167">In the following, the `InvokeAsync` method is called with two parameters:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFinal.cshtml?range=35)]

::: moniker range=">= aspnetcore-1.1"

## <a name="invoking-a-view-component-as-a-tag-helper"></a><span data-ttu-id="18ad8-168">Вызов компонента представления в качестве вспомогательной функции тегов</span><span class="sxs-lookup"><span data-stu-id="18ad8-168">Invoking a view component as a Tag Helper</span></span>

<span data-ttu-id="18ad8-169">Для ASP.NET Core 1.1 и более поздних версий можно вызвать компонент представления в качестве [вспомогательной функции тегов](xref:mvc/views/tag-helpers/intro):</span><span class="sxs-lookup"><span data-stu-id="18ad8-169">For ASP.NET Core 1.1 and higher, you can invoke a view component as a [Tag Helper](xref:mvc/views/tag-helpers/intro):</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="18ad8-170">Параметры методов и классов, указанные в стиле Pascal, для вспомогательных функций тегов преобразуются в [кебаб-стиль](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span><span class="sxs-lookup"><span data-stu-id="18ad8-170">Pascal-cased class and method parameters for Tag Helpers are translated into their [kebab case](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span></span> <span data-ttu-id="18ad8-171">Вспомогательная функция тегов для вызова компонента представления использует элемент `<vc></vc>`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-171">The Tag Helper to invoke a view component uses the `<vc></vc>` element.</span></span> <span data-ttu-id="18ad8-172">Компонент представления задан следующим образом:</span><span class="sxs-lookup"><span data-stu-id="18ad8-172">The view component is specified as follows:</span></span>

```cshtml
<vc:[view-component-name]
  parameter1="parameter1 value"
  parameter2="parameter2 value">
</vc:[view-component-name]>
```

<span data-ttu-id="18ad8-173">Чтобы использовать компонент представления в качестве вспомогательного приложения тегов, зарегистрируйте с помощью директивы `@addTagHelper`сборку, содержащую этот компонент представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-173">To use a view component as a Tag Helper, register the assembly containing the view component using the `@addTagHelper` directive.</span></span> <span data-ttu-id="18ad8-174">Если компонент представления находится в сборке с именем `MyWebApp`, добавьте в файл *_ViewImports.cshtml* следующую директиву:</span><span class="sxs-lookup"><span data-stu-id="18ad8-174">If your view component is in an assembly called `MyWebApp`, add the following directive to the *_ViewImports.cshtml* file:</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="18ad8-175">Зарегистрировать компонент представления в качестве вспомогательной функции тегов можно в любом файле, который ссылается на этот компонент представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-175">You can register a view component as a Tag Helper to any file that references the view component.</span></span> <span data-ttu-id="18ad8-176">Раздел [Управление областью вспомогательной функции тегов](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) содержит дополнительные сведения о том, как зарегистрировать вспомогательные функции тегов.</span><span class="sxs-lookup"><span data-stu-id="18ad8-176">See [Managing Tag Helper Scope](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) for more information on how to register Tag Helpers.</span></span>

<span data-ttu-id="18ad8-177">Метод `InvokeAsync`, используемый в этом учебнике:</span><span class="sxs-lookup"><span data-stu-id="18ad8-177">The `InvokeAsync` method used in this tutorial:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="18ad8-178">В разметке вспомогательной функции тегов:</span><span class="sxs-lookup"><span data-stu-id="18ad8-178">In Tag Helper markup:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="18ad8-179">В предыдущем примере компонент представления `PriorityList` становится `priority-list`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-179">In the sample above, the `PriorityList` view component becomes `priority-list`.</span></span> <span data-ttu-id="18ad8-180">Параметры передаются в компонент представления как атрибуты в кебаб-стиле.</span><span class="sxs-lookup"><span data-stu-id="18ad8-180">The parameters to the view component are passed as attributes in kebab case.</span></span>

::: moniker-end

### <a name="invoking-a-view-component-directly-from-a-controller"></a><span data-ttu-id="18ad8-181">Вызов компонента представления непосредственно из контроллера</span><span class="sxs-lookup"><span data-stu-id="18ad8-181">Invoking a view component directly from a controller</span></span>

<span data-ttu-id="18ad8-182">Компоненты представлений обычно вызываются из представления, но их можно вызывать непосредственно из метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="18ad8-182">View components are typically invoked from a view, but you can invoke them directly from a controller method.</span></span> <span data-ttu-id="18ad8-183">Если компоненты представлений не определяют конечные точки, например контроллеры, можно легко реализовать действие контроллера, возвращающее содержимое `ViewComponentResult`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-183">While view components don't define endpoints like controllers, you can easily implement a controller action that returns the content of a `ViewComponentResult`.</span></span>

<span data-ttu-id="18ad8-184">В этом примере компонент представления вызывается непосредственно из контроллера:</span><span class="sxs-lookup"><span data-stu-id="18ad8-184">In this example, the view component is called directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

## <a name="walkthrough-creating-a-simple-view-component"></a><span data-ttu-id="18ad8-185">Пошаговое руководство. Создание простого компонента представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-185">Walkthrough: Creating a simple view component</span></span>

<span data-ttu-id="18ad8-186">[Скачайте](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) начальный код и выполните его сборку и тестирование.</span><span class="sxs-lookup"><span data-stu-id="18ad8-186">[Download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), build and test the starter code.</span></span> <span data-ttu-id="18ad8-187">Это простой проект с контроллером `ToDo`, который отображает список элементов *дел*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-187">It's a simple project with a `ToDo` controller that displays a list of *ToDo* items.</span></span>

![Список дел](view-components/_static/2dos.png)

### <a name="add-a-viewcomponent-class"></a><span data-ttu-id="18ad8-189">Добавление класса ViewComponent</span><span class="sxs-lookup"><span data-stu-id="18ad8-189">Add a ViewComponent class</span></span>

<span data-ttu-id="18ad8-190">Создайте папку *ViewComponents* и добавьте следующий класс `PriorityListViewComponent`:</span><span class="sxs-lookup"><span data-stu-id="18ad8-190">Create a *ViewComponents* folder and add the following `PriorityListViewComponent` class:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponent1.cs?name=snippet1)]

<span data-ttu-id="18ad8-191">Примечания к коду:</span><span class="sxs-lookup"><span data-stu-id="18ad8-191">Notes on the code:</span></span>

* <span data-ttu-id="18ad8-192">Классы компонентов представлений могут находиться в **любой** папке проекта.</span><span class="sxs-lookup"><span data-stu-id="18ad8-192">View component classes can be contained in **any** folder in the project.</span></span>
* <span data-ttu-id="18ad8-193">Так как имя класса PriorityList**ViewComponent** заканчивается суффиксом **ViewComponent**, среда выполнения использует строку "PriorityList" при ссылке на компонент класса из представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-193">Because the class name PriorityList**ViewComponent** ends with the suffix **ViewComponent**, the runtime will use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="18ad8-194">Я подробнее расскажу об этом чуть позже.</span><span class="sxs-lookup"><span data-stu-id="18ad8-194">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="18ad8-195">Атрибут `[ViewComponent]` может изменить имя, используемое для ссылки на компонент представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-195">The `[ViewComponent]` attribute can change the name used to reference a view component.</span></span> <span data-ttu-id="18ad8-196">Например, мы могли назвать класс `XYZ` и применить атрибут `ViewComponent`:</span><span class="sxs-lookup"><span data-stu-id="18ad8-196">For example, we could've named the class `XYZ` and applied the `ViewComponent` attribute:</span></span>

  ```csharp
  [ViewComponent(Name = "PriorityList")]
     public class XYZ : ViewComponent
     ```

* <span data-ttu-id="18ad8-197">Приведенный выше атрибут `[ViewComponent]` предписывает средству выбора компонентов представлений использовать имя `PriorityList` при поиске представлений, связанных с данным компонентом, и строку "PriorityList" при ссылке на компонент класса из представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-197">The `[ViewComponent]` attribute above tells the view component selector to use the name `PriorityList` when looking for the views associated with the component, and to use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="18ad8-198">Я подробнее расскажу об этом чуть позже.</span><span class="sxs-lookup"><span data-stu-id="18ad8-198">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="18ad8-199">Компонент использует [внедрение зависимостей](../../fundamentals/dependency-injection.md) для предоставления контекста данных.</span><span class="sxs-lookup"><span data-stu-id="18ad8-199">The component uses [dependency injection](../../fundamentals/dependency-injection.md) to make the data context available.</span></span>
* <span data-ttu-id="18ad8-200">`InvokeAsync` предоставляет метод, который возможно вызывать из представления и который может принять произвольное число аргументов.</span><span class="sxs-lookup"><span data-stu-id="18ad8-200">`InvokeAsync` exposes a method which can be called from a view, and it can take an arbitrary number of arguments.</span></span>
* <span data-ttu-id="18ad8-201">Метод `InvokeAsync` возвращает набор элементов `ToDo`, удовлетворяющих параметрам `isDone` и `maxPriority`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-201">The `InvokeAsync` method returns the set of `ToDo` items that satisfy the `isDone` and `maxPriority` parameters.</span></span>

### <a name="create-the-view-component-razor-view"></a><span data-ttu-id="18ad8-202">Создание представления Razor для компонента представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-202">Create the view component Razor view</span></span>

* <span data-ttu-id="18ad8-203">Создайте папку *Views/Shared/Components*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-203">Create the *Views/Shared/Components* folder.</span></span> <span data-ttu-id="18ad8-204">Она **должна**  называться *Components*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-204">This folder **must** be named *Components*.</span></span>

* <span data-ttu-id="18ad8-205">Создайте папку *Views/Shared/Components/PriorityList*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-205">Create the *Views/Shared/Components/PriorityList* folder.</span></span> <span data-ttu-id="18ad8-206">Ее имя должно соответствовать имени класса представлений компонентов или имени класса без суффикса (если мы следовали соглашению и использовали суффикс *ViewComponent* в имени класса).</span><span class="sxs-lookup"><span data-stu-id="18ad8-206">This folder name must match the name of the view component class, or the name of the class minus the suffix (if we followed convention and used the *ViewComponent* suffix in the class name).</span></span> <span data-ttu-id="18ad8-207">Если вы использовали атрибут `ViewComponent`, имя класса должно соответствовать его обозначению.</span><span class="sxs-lookup"><span data-stu-id="18ad8-207">If you used the `ViewComponent` attribute, the class name would need to match the attribute designation.</span></span>

* <span data-ttu-id="18ad8-208">Создайте представление Razor *Views/Shared/Components/PriorityList/Default.cshtml*: [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="18ad8-208">Create a *Views/Shared/Components/PriorityList/Default.cshtml* Razor view: [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span></span>

   <span data-ttu-id="18ad8-209">Представление Razor принимает список `TodoItem` и отображает их.</span><span class="sxs-lookup"><span data-stu-id="18ad8-209">The Razor view takes a list of `TodoItem` and displays them.</span></span> <span data-ttu-id="18ad8-210">Если метод `InvokeAsync` компонента представления не передает имя представления (как в нашем примере), по соглашению используется имя *Default*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-210">If the view component `InvokeAsync` method doesn't pass the name of the view (as in our sample), *Default* is used for the view name by convention.</span></span> <span data-ttu-id="18ad8-211">Далее в этом учебнике я покажу, как передать имя представления.</span><span class="sxs-lookup"><span data-stu-id="18ad8-211">Later in the tutorial, I'll show you how to pass the name of the view.</span></span> <span data-ttu-id="18ad8-212">Чтобы переопределить стиль по умолчанию для определенного контроллера, добавьте представление в папку соответствующего контроллера (например, *Views/ToDo/Components/PriorityList/Default.cshtml)*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-212">To override the default styling for a specific controller, add a view to the controller-specific view folder (for example *Views/ToDo/Components/PriorityList/Default.cshtml)*.</span></span>

    <span data-ttu-id="18ad8-213">Если компонент представления связан с конкретным контроллером, его можно добавить в папку этого контроллера (*Views/ToDo/Components/PriorityList/Default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="18ad8-213">If the view component is controller-specific, you can add it to the controller-specific folder (*Views/ToDo/Components/PriorityList/Default.cshtml*).</span></span>

* <span data-ttu-id="18ad8-214">Добавьте `div`, содержащий вызов компонента списка приоритетов, в конец файла *Views/ToDo/index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="18ad8-214">Add a `div` containing a call to the priority list component to the bottom of the *Views/ToDo/index.cshtml* file:</span></span>

    [!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFirst.cshtml?range=34-38)]

<span data-ttu-id="18ad8-215">`@await Component.InvokeAsync` в разметке показывает синтаксис для вызова компонентов представлений.</span><span class="sxs-lookup"><span data-stu-id="18ad8-215">The markup `@await Component.InvokeAsync` shows the syntax for calling view components.</span></span> <span data-ttu-id="18ad8-216">Первым аргументом является имя компонента, который требуется вызвать.</span><span class="sxs-lookup"><span data-stu-id="18ad8-216">The first argument is the name of the component we want to invoke or call.</span></span> <span data-ttu-id="18ad8-217">Последующие параметры передаются в компонент.</span><span class="sxs-lookup"><span data-stu-id="18ad8-217">Subsequent parameters are passed to the component.</span></span> <span data-ttu-id="18ad8-218">`InvokeAsync` может занять произвольное число аргументов.</span><span class="sxs-lookup"><span data-stu-id="18ad8-218">`InvokeAsync` can take an arbitrary number of arguments.</span></span>

<span data-ttu-id="18ad8-219">Проверьте работу приложения.</span><span class="sxs-lookup"><span data-stu-id="18ad8-219">Test the app.</span></span> <span data-ttu-id="18ad8-220">Следующий рисунок показывает список дел и элементы с приоритетом:</span><span class="sxs-lookup"><span data-stu-id="18ad8-220">The following image shows the ToDo list and the priority items:</span></span>

![список дел и элементы с приоритетом](view-components/_static/pi.png)

<span data-ttu-id="18ad8-222">Кроме того, компонент представления можно вызвать непосредственно из контроллера:</span><span class="sxs-lookup"><span data-stu-id="18ad8-222">You can also call the view component directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

![элементы с приоритетом из действия IndexVC](view-components/_static/indexvc.png)

### <a name="specifying-a-view-name"></a><span data-ttu-id="18ad8-224">Указание имени представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-224">Specifying a view name</span></span>

<span data-ttu-id="18ad8-225">Сложному представлению компонента в некоторых условиях может потребоваться указать нестандартное представление.</span><span class="sxs-lookup"><span data-stu-id="18ad8-225">A complex view component might need to specify a non-default view under some conditions.</span></span> <span data-ttu-id="18ad8-226">Ниже показано, как указать представление "PVC" из метода `InvokeAsync`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-226">The following code shows how to specify the "PVC" view  from the `InvokeAsync` method.</span></span> <span data-ttu-id="18ad8-227">Обновите метод `InvokeAsync` в классе `PriorityListViewComponent`.</span><span class="sxs-lookup"><span data-stu-id="18ad8-227">Update the `InvokeAsync` method in the `PriorityListViewComponent` class.</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponentFinal.cs?highlight=4,5,6,7,8,9&range=28-39)]

<span data-ttu-id="18ad8-228">Скопируйте файл *Views/Shared/Components/PriorityList/Default.cshtml* в представление *Views/Shared/Components/PriorityList/PVC.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-228">Copy the *Views/Shared/Components/PriorityList/Default.cshtml* file to a view named *Views/Shared/Components/PriorityList/PVC.cshtml*.</span></span> <span data-ttu-id="18ad8-229">Добавьте заголовок, чтобы указать используемое представление PVC.</span><span class="sxs-lookup"><span data-stu-id="18ad8-229">Add a heading to indicate the PVC view is being used.</span></span>

[!code-cshtml[](../../mvc/views/view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/PVC.cshtml?highlight=3)]

<span data-ttu-id="18ad8-230">Измените *Views/ToDo/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="18ad8-230">Update *Views/ToDo/Index.cshtml*:</span></span>

<!-- Views/ToDo/Index.cshtml is never imported, so change to test tutorial -->

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="18ad8-231">Запустите приложение и проверьте представление PVC.</span><span class="sxs-lookup"><span data-stu-id="18ad8-231">Run the app and verify PVC view.</span></span>

![Компонент представления с приоритетом](view-components/_static/pvc.png)

<span data-ttu-id="18ad8-233">Если представление PVC не отображается, убедитесь, что вы вызываете компонент представления с приоритетом 4 или выше.</span><span class="sxs-lookup"><span data-stu-id="18ad8-233">If the PVC view isn't rendered, verify you are calling the view component with a priority of 4 or higher.</span></span>

### <a name="examine-the-view-path"></a><span data-ttu-id="18ad8-234">Проверка пути к представлению</span><span class="sxs-lookup"><span data-stu-id="18ad8-234">Examine the view path</span></span>

* <span data-ttu-id="18ad8-235">Задайте для параметра приоритета значение 3 или меньше, чтобы представление с приоритетом не возвращалось.</span><span class="sxs-lookup"><span data-stu-id="18ad8-235">Change the priority parameter to three or less so the priority view isn't returned.</span></span>
* <span data-ttu-id="18ad8-236">Временно переименуйте *Views/ToDo/Components/PriorityList/Default.cshtml* в *1Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-236">Temporarily rename the *Views/ToDo/Components/PriorityList/Default.cshtml* to *1Default.cshtml*.</span></span>
* <span data-ttu-id="18ad8-237">Проверьте приложение, при этом происходит следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="18ad8-237">Test the app, you'll get the following error:</span></span>

   ```
   An unhandled exception occurred while processing the request.
   InvalidOperationException: The view 'Components/PriorityList/Default' wasn't found. The following locations were searched:
   /Views/ToDo/Components/PriorityList/Default.cshtml
   /Views/Shared/Components/PriorityList/Default.cshtml
   EnsureSuccessful
   ```

* <span data-ttu-id="18ad8-238">Скопируйте *Views/ToDo/Components/PriorityList/1Default.cshtml* в *Views/Shared/Components/PriorityList/Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-238">Copy *Views/ToDo/Components/PriorityList/1Default.cshtml* to *Views/Shared/Components/PriorityList/Default.cshtml*.</span></span>
* <span data-ttu-id="18ad8-239">Добавьте разметку в представление компонента представления дел *Shared*, чтобы указать, что это представление из папки *Shared*.</span><span class="sxs-lookup"><span data-stu-id="18ad8-239">Add some markup to the *Shared* ToDo view component view to indicate the view is from the *Shared* folder.</span></span>
* <span data-ttu-id="18ad8-240">Протестируйте представление компонента **Shared**.</span><span class="sxs-lookup"><span data-stu-id="18ad8-240">Test the **Shared** component view.</span></span>

![Выходные данные дел с представлением компонента Shared](view-components/_static/shared.png)

### <a name="avoiding-hard-coded-strings"></a><span data-ttu-id="18ad8-242">Как избежать жестко запрограммированных строк</span><span class="sxs-lookup"><span data-stu-id="18ad8-242">Avoiding hard-coded strings</span></span>

<span data-ttu-id="18ad8-243">Чтобы обеспечить безопасность во время компиляции, можно заменить жестко заданное имя компонента представления на имя класса.</span><span class="sxs-lookup"><span data-stu-id="18ad8-243">If you want compile time safety, you can replace the hard-coded view component name with the class name.</span></span> <span data-ttu-id="18ad8-244">Создайте компонент представления без суффикса "ViewComponent":</span><span class="sxs-lookup"><span data-stu-id="18ad8-244">Create the view component without the "ViewComponent" suffix:</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityList.cs?highlight=10&range=5-35)]

<span data-ttu-id="18ad8-245">Добавьте инструкцию `using` в файл представления Razor и используйте оператор `nameof`:</span><span class="sxs-lookup"><span data-stu-id="18ad8-245">Add a `using` statement to your Razor view file, and use the `nameof` operator:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexNameof.cshtml?range=1-6,35-)]

## <a name="perform-synchronous-work"></a><span data-ttu-id="18ad8-246">Выполнение синхронных задач</span><span class="sxs-lookup"><span data-stu-id="18ad8-246">Perform synchronous work</span></span>

<span data-ttu-id="18ad8-247">Платформа обрабатывает вызов синхронного метода `Invoke`, если не требуется асинхронное выполнение работы.</span><span class="sxs-lookup"><span data-stu-id="18ad8-247">The framework handles invoking a synchronous `Invoke` method if you don't need to perform asynchronous work.</span></span> <span data-ttu-id="18ad8-248">Следующий метод создает синхронный компонент представления `Invoke`:</span><span class="sxs-lookup"><span data-stu-id="18ad8-248">The following method creates a synchronous `Invoke` view component:</span></span>

```csharp
public class PriorityList : ViewComponent
{
    public IViewComponentResult Invoke(int maxPriority, bool isDone)
    {
        var items = new List<string> { $"maxPriority: {maxPriority}", $"isDone: {isDone}" };
        return View(items);
    }
}
```

<span data-ttu-id="18ad8-249">В файле Razor для этого компонента представления содержится список строк, передаваемых в метод `Invoke` (*Views/Home/Components/PriorityList/Default.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="18ad8-249">The view component's Razor file lists the strings passed to the `Invoke` method (*Views/Home/Components/PriorityList/Default.cshtml*):</span></span>

```cshtml
@model List<string>

<h3>Priority Items</h3>
<ul>
    @foreach (var item in Model)
    {
        <li>@item</li>
    }
</ul>
```

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="18ad8-250">Компонент представления вызывается в файле Razor (например, *Views/Home/Index.cshtml*) с помощью одного из следующих подходов:</span><span class="sxs-lookup"><span data-stu-id="18ad8-250">The view component is invoked in a Razor file (for example, *Views/Home/Index.cshtml*) using one of the following approaches:</span></span>

* <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper>
* [<span data-ttu-id="18ad8-251">Вспомогательное приложение тегов</span><span class="sxs-lookup"><span data-stu-id="18ad8-251">Tag Helper</span></span>](xref:mvc/views/tag-helpers/intro)

<span data-ttu-id="18ad8-252">Чтобы использовать подход <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper>, вызовите `Component.InvokeAsync`:</span><span class="sxs-lookup"><span data-stu-id="18ad8-252">To use the <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper> approach, call `Component.InvokeAsync`:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-1.1"

<span data-ttu-id="18ad8-253">Компонент представления вызывается в файле Razor (например, *Views/Home/Index.cshtml*) с помощью <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper>:</span><span class="sxs-lookup"><span data-stu-id="18ad8-253">The view component is invoked in a Razor file (for example, *Views/Home/Index.cshtml*) with <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper>.</span></span>

<span data-ttu-id="18ad8-254">Вызов `Component.InvokeAsync`:</span><span class="sxs-lookup"><span data-stu-id="18ad8-254">Call `Component.InvokeAsync`:</span></span>

::: moniker-end

```cshtml
@await Component.InvokeAsync(nameof(PriorityList), new { maxPriority = 4, isDone = true })
```

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="18ad8-255">Чтобы использовать вспомогательное приложение тэгов зарегистрируйте с помощью директивы `@addTagHelper`сборку, содержащую этот компонент представления (он находится в сборке с именем `MyWebApp`):</span><span class="sxs-lookup"><span data-stu-id="18ad8-255">To use the Tag Helper, register the assembly containing the View Component using the `@addTagHelper` directive (the view component is in an assembly called `MyWebApp`):</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="18ad8-256">Примените вспомогательное приложение тэгов из компонента представления в файле разметки Razor:</span><span class="sxs-lookup"><span data-stu-id="18ad8-256">Use the view component Tag Helper in the Razor markup file:</span></span>

```cshtml
<vc:priority-list max-priority="999" is-done="false">
</vc:priority-list>
```
::: moniker-end

<span data-ttu-id="18ad8-257">Метод `PriorityList.Invoke` имеет синхронную подпись, но Razor обнаруживает и вызывает метод с помощью `Component.InvokeAsync` в файле разметки.</span><span class="sxs-lookup"><span data-stu-id="18ad8-257">The method signature of `PriorityList.Invoke` is synchronous, but Razor finds and calls the method with `Component.InvokeAsync` in the markup file.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18ad8-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="18ad8-258">Additional resources</span></span>

* [<span data-ttu-id="18ad8-259">Внедрение зависимостей в представления</span><span class="sxs-lookup"><span data-stu-id="18ad8-259">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
