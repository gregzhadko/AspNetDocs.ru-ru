---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Общие сведения о фильтрах действий (C#) | Документация Майкрософт
author: microsoft
description: Цель данного руководства — объяснить фильтров действий. Фильтр операции — атрибут, который можно применить к действию контроллера--или всего контроллера...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 8264b48388ee4a6b51515aa2b897ece3b2f3972a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59380877"
---
# <a name="understanding-action-filters-c"></a><span data-ttu-id="2924d-104">Общие сведения о фильтрах действий (C#)</span><span class="sxs-lookup"><span data-stu-id="2924d-104">Understanding Action Filters (C#)</span></span>

<span data-ttu-id="2924d-105">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2924d-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2924d-106">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="2924d-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="2924d-107">Цель данного руководства — объяснить фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="2924d-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="2924d-108">Фильтр операции — атрибут, который можно применить к действию контроллера--или всего контроллера--, изменяет способ, в котором выполняется действие.</span><span class="sxs-lookup"><span data-stu-id="2924d-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="2924d-109">Общие сведения о фильтрах действий</span><span class="sxs-lookup"><span data-stu-id="2924d-109">Understanding Action Filters</span></span>

<span data-ttu-id="2924d-110">Цель данного руководства — объяснить фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="2924d-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="2924d-111">Фильтр операции — атрибут, который можно применить к действию контроллера--или всего контроллера--, изменяет способ, в котором выполняется действие.</span><span class="sxs-lookup"><span data-stu-id="2924d-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="2924d-112">Платформа ASP.NET MVC включает в себя несколько фильтров действий:</span><span class="sxs-lookup"><span data-stu-id="2924d-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="2924d-113">OutputCache-этот фильтр действий кэширует выходные данные действия контроллера, в течение определенного времени.</span><span class="sxs-lookup"><span data-stu-id="2924d-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="2924d-114">HandleError — это фильтр действий обрабатывает ошибки, возникшие при выполнении действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="2924d-115">Авторизация — этот фильтр действий позволяет ограничить доступ к определенному пользователю или роли.</span><span class="sxs-lookup"><span data-stu-id="2924d-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="2924d-116">Также можно создать собственные фильтры настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="2924d-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="2924d-117">Например может потребоваться создание пользовательского фильтра действий, чтобы реализовать пользовательскую систему аутентификации.</span><span class="sxs-lookup"><span data-stu-id="2924d-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="2924d-118">Или, может потребоваться создание фильтра действий, изменяющих данные представления, возвращаемое в результате действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="2924d-119">В этом руководстве вы узнаете, как для создания фильтра действий с нуля.</span><span class="sxs-lookup"><span data-stu-id="2924d-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="2924d-120">Мы создадим фильтр действий журнала, который записывает различные этапы обработки действия в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2924d-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="2924d-121">С помощью фильтра действий</span><span class="sxs-lookup"><span data-stu-id="2924d-121">Using an Action Filter</span></span>

<span data-ttu-id="2924d-122">Фильтр операции — атрибут.</span><span class="sxs-lookup"><span data-stu-id="2924d-122">An action filter is an attribute.</span></span> <span data-ttu-id="2924d-123">Большинство фильтров действий можно применить к действию отдельного контроллера или всего контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="2924d-124">Например, контроллер данных в листинге 1 предоставляет действие с именем `Index()` , возвращает текущее время.</span><span class="sxs-lookup"><span data-stu-id="2924d-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="2924d-125">Это действие снабжен `OutputCache` фильтра действий.</span><span class="sxs-lookup"><span data-stu-id="2924d-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="2924d-126">Этот фильтр вызывает значение, возвращаемое в результате действия должен быть помещен в кэш на 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="2924d-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

**<span data-ttu-id="2924d-127">Листинг 1.</span><span class="sxs-lookup"><span data-stu-id="2924d-127">Listing 1 –</span></span> `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="2924d-128">При многократном запуске `Index()` действие, введя URL-адрес/Data/индекса в адресную строку браузера и обновление кнопку несколько раз, вы увидите то же время на 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="2924d-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="2924d-129">Выходные данные `Index()` действие кэшируется на 10 секунд (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="2924d-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


[![C<span data-ttu-id="2924d-130">пострадавший time]</span><span class="sxs-lookup"><span data-stu-id="2924d-130">ached time]</span></span>(understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

<span data-ttu-id="2924d-131">**Рис 01**: Время ([Просмотр полноразмерного изображения](understanding-action-filters-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2924d-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>


<span data-ttu-id="2924d-132">В листинге 1 фильтр одно действие — `OutputCache` фильтр действий — применяется к `Index()` метод.</span><span class="sxs-lookup"><span data-stu-id="2924d-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="2924d-133">Если требуется, можно применить несколько фильтров действий к одному действию.</span><span class="sxs-lookup"><span data-stu-id="2924d-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="2924d-134">Например, может потребоваться применить оба `OutputCache` и `HandleError` фильтров действий к одному действию.</span><span class="sxs-lookup"><span data-stu-id="2924d-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="2924d-135">В листинге 1 `OutputCache` фильтр действий применяется к `Index()` действие.</span><span class="sxs-lookup"><span data-stu-id="2924d-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="2924d-136">Вы также можете применить этот атрибут, чтобы `DataController` сам по себе класс.</span><span class="sxs-lookup"><span data-stu-id="2924d-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="2924d-137">В этом случае результат, возвращаемый никаких действий, предоставляемых контроллер будет кэшироваться на 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="2924d-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="2924d-138">Различные типы фильтров</span><span class="sxs-lookup"><span data-stu-id="2924d-138">The Different Types of Filters</span></span>

<span data-ttu-id="2924d-139">Платформа ASP.NET MVC поддерживает четыре различных типа фильтров:</span><span class="sxs-lookup"><span data-stu-id="2924d-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="2924d-140">Фильтры авторизации — реализует `IAuthorizationFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="2924d-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="2924d-141">Фильтры действий — реализует `IActionFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="2924d-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="2924d-142">Фильтры — реализует результатов `IResultFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="2924d-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="2924d-143">Фильтры исключений — реализует `IExceptionFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="2924d-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="2924d-144">Фильтры выполняются в порядке, указанном выше.</span><span class="sxs-lookup"><span data-stu-id="2924d-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="2924d-145">Например фильтры авторизации всегда выполняются перед фильтров действий и фильтров исключений, всегда выполняются после любого другого типа фильтра.</span><span class="sxs-lookup"><span data-stu-id="2924d-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="2924d-146">Фильтры авторизации используются для реализации проверки подлинности и авторизации для действий контроллеров.</span><span class="sxs-lookup"><span data-stu-id="2924d-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="2924d-147">Например фильтра Authorize является примером фильтра авторизации.</span><span class="sxs-lookup"><span data-stu-id="2924d-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="2924d-148">Фильтры действий содержат логику, выполняемую перед и после выполнения действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="2924d-149">Можно использовать фильтр действий, например, для изменения представления данных, возвращающий действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="2924d-150">Фильтры результатов содержат логику, выполняемую перед и после выполнения результат представления.</span><span class="sxs-lookup"><span data-stu-id="2924d-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="2924d-151">Например, может потребоваться изменить результат представления непосредственно перед визуализации представления в браузер.</span><span class="sxs-lookup"><span data-stu-id="2924d-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="2924d-152">Фильтры исключений — это последний тип фильтра для выполнения.</span><span class="sxs-lookup"><span data-stu-id="2924d-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="2924d-153">Фильтр исключений можно использовать для обработки ошибок, вызванных результатов действий контроллера или действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="2924d-154">Также можно использовать фильтры исключений для ведения журнала ошибок.</span><span class="sxs-lookup"><span data-stu-id="2924d-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="2924d-155">У каждого типа фильтра выполняется в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="2924d-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="2924d-156">Если вы хотите управлять порядком, в котором выполняются фильтры одного типа можно задать свойство порядок фильтра.</span><span class="sxs-lookup"><span data-stu-id="2924d-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="2924d-157">Является базовым классом для всех фильтров действий `System.Web.Mvc.FilterAttribute` класса.</span><span class="sxs-lookup"><span data-stu-id="2924d-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="2924d-158">Если вы хотите реализовать определенный тип фильтра, то необходимо создать класс, наследующий от базового класса фильтра и реализует один или несколько `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, или `IExceptionFilter` интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="2924d-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="2924d-159">Базовый класс ActionFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="2924d-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="2924d-160">Для повышения его читаемости для реализации пользовательского фильтра действий, платформа ASP.NET MVC включает в себя базовый `ActionFilterAttribute` класса.</span><span class="sxs-lookup"><span data-stu-id="2924d-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="2924d-161">Этот класс реализует оба `IActionFilter` и `IResultFilter` интерфейсы и наследует от `Filter` класса.</span><span class="sxs-lookup"><span data-stu-id="2924d-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="2924d-162">Терминология здесь не полностью согласована.</span><span class="sxs-lookup"><span data-stu-id="2924d-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="2924d-163">С технической точки зрения класс, наследуемый от класса ActionFilterAttribute является фильтром действий и фильтра результатов.</span><span class="sxs-lookup"><span data-stu-id="2924d-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="2924d-164">Тем не менее в том смысле, свободные, фильтр действий word используется для ссылки на любой тип фильтра в платформе ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2924d-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="2924d-165">Базовый `ActionFilterAttribute` класс содержит следующие методы, которые можно переопределить:</span><span class="sxs-lookup"><span data-stu-id="2924d-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="2924d-166">OnActionExecuting — этот метод вызывается перед выполнением действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="2924d-167">OnActionExecuted — этот метод вызывается после выполнения действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="2924d-168">OnResultExecuting — этот метод вызывается до выполнения результата действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="2924d-169">OnResultExecuted — этот метод вызывается после выполнения результата действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="2924d-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="2924d-170">В следующем разделе мы рассмотрим, как можно реализовать каждый из этих различных методов.</span><span class="sxs-lookup"><span data-stu-id="2924d-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="2924d-171">Создание фильтра журнала действий</span><span class="sxs-lookup"><span data-stu-id="2924d-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="2924d-172">Чтобы проиллюстрировать, как создать настраиваемого фильтра действий, мы создадим пользовательского фильтра действий, заносящий в журнал на этапах обработки действия контроллера, в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2924d-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="2924d-173">Наши `LogActionFilter` содержится в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="2924d-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

**<span data-ttu-id="2924d-174">Листинг 2.</span><span class="sxs-lookup"><span data-stu-id="2924d-174">Listing 2 –</span></span> `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="2924d-175">В листинге 2 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, и `OnResultExecuted()` вызывать все методы `Log()` метод.</span><span class="sxs-lookup"><span data-stu-id="2924d-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="2924d-176">Имя метода и текущих данных маршрута передается `Log()` метод.</span><span class="sxs-lookup"><span data-stu-id="2924d-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="2924d-177">`Log()` Метод записывает сообщение в окне вывода Visual Studio (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="2924d-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


[![W<span data-ttu-id="2924d-178">riting в окне вывода Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="2924d-178">riting to the Visual Studio Output window]</span></span>(understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

<span data-ttu-id="2924d-179">**Рис. 02**: Запись в окно вывода Visual Studio ([Просмотр полноразмерного изображения](understanding-action-filters-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2924d-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>


<span data-ttu-id="2924d-180">Контроллер Home в листинге 3 показано, как можно применить фильтр журнала действий в класс контроллера целиком.</span><span class="sxs-lookup"><span data-stu-id="2924d-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="2924d-181">Каждый раз, когда любое из действий, предоставляемых контроллера Home вызываются — либо `Index()` метод или `About()` метод — этапы обработки, действия записываются в окно вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2924d-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

**<span data-ttu-id="2924d-182">Листинг 3.</span><span class="sxs-lookup"><span data-stu-id="2924d-182">Listing 3 –</span></span> `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="2924d-183">Сводка</span><span class="sxs-lookup"><span data-stu-id="2924d-183">Summary</span></span>

<span data-ttu-id="2924d-184">В этом руководстве вы ознакомились с фильтров операций ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2924d-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="2924d-185">Вы узнали о четыре различных типа фильтров: фильтры авторизации, фильтров действий, фильтров результатов и фильтры исключений.</span><span class="sxs-lookup"><span data-stu-id="2924d-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="2924d-186">Вы также узнали о базовый `ActionFilterAttribute` класса.</span><span class="sxs-lookup"><span data-stu-id="2924d-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="2924d-187">Наконец вы узнали, как выполнить простой фильтр действий.</span><span class="sxs-lookup"><span data-stu-id="2924d-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="2924d-188">Мы создали фильтр действий журнала, который записывает журнал на этапах обработки действия контроллера, в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2924d-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2924d-189">[Назад](asp-net-mvc-routing-overview-cs.md)
> [Вперед](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2924d-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
