---
title: Представления в ASP.NET Core MVC
author: ardalis
description: Узнайте, как представления обеспечивают отображение данных приложения и взаимодействие с пользователем в ASP.NET Core MVC.
ms.author: riande
ms.date: 12/12/2017
uid: mvc/views/overview
ms.openlocfilehash: 6c5b4d7b89ac07a85b5aad626e37855de98064eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036101"
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="4cb1f-103">Представления в ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="4cb1f-103">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="4cb1f-104">Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith) и [Люк Лэтем](https://github.com/guardrex) (Luke Latham)</span><span class="sxs-lookup"><span data-stu-id="4cb1f-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4cb1f-105">В этом документе описываются представления, используемые в приложениях ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-105">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="4cb1f-106">Сведения о Razor Pages см. в статье [Введение в Razor Pages](xref:razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-106">For information on Razor Pages, see [Introduction to Razor Pages](xref:razor-pages/index).</span></span>

<span data-ttu-id="4cb1f-107">В шаблоне MVC (Model-View-Controller, модель — представление — контроллер) *представление* отвечает за отображение данных приложения и взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-107">In the Model-View-Controller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="4cb1f-108">Представление — это шаблон HTML с внедренной [разметкой Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-108">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="4cb1f-109">Разметка Razor — это код, который взаимодействует с разметкой HTML для создания веб-страницы, отправляемой клиенту.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-109">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="4cb1f-110">В ASP.NET Core MVC представления — это файлы *CSHTML*, в которых используется [язык программирования C#](/dotnet/csharp/) в разметке Razor.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-110">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="4cb1f-111">Как правило, файлы представлений объединяются в папки с именами, соответствующими отдельным [контроллерам](xref:mvc/controllers/actions) приложения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-111">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="4cb1f-112">Эти папки находятся в папке *Views* в корне приложения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-112">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Папка Views в обозревателе решений Visual Studio с открытой вложенной папкой Home, содержащей файлы About.cshtml, Contact.cshtml и Index.cshtml](overview/_static/views_solution_explorer.png)

<span data-ttu-id="4cb1f-114">Контроллер *Home* представлен папкой *Home* в папке *Views*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-114">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="4cb1f-115">Папка *Home* (Домашняя страница) содержит представления для веб-страниц *About* (Информация), *Contact* (Контакты) и *Index* (Указатель).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-115">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="4cb1f-116">Когда пользователь запрашивает одну из этих трех веб-страниц, действия контроллера *Home* определяют, какое из трех представлений используется для создания и отправки веб-страницы пользователю.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-116">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="4cb1f-117">[Макеты](xref:mvc/views/layout) позволяют создавать единообразные разделы веб-страниц и сократить повторы в коде.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-117">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="4cb1f-118">Они часто содержат верхний и нижний колонтитулы, а также элементы навигации и меню.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-118">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="4cb1f-119">Колонтитулы обычно содержат стандартную разметку для многих элементов метаданных и ссылки на ресурсы скриптов и стилей.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-119">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="4cb1f-120">Макеты позволяют избежать использования этой стандартной разметки в представлениях.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-120">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="4cb1f-121">[Частичные представления](xref:mvc/views/partial) сокращают дублирование кода, обеспечивая управление многократно используемыми частями представлений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-121">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="4cb1f-122">Например, частичное представление будет полезным для биографии автора, которая присутствует в нескольких представлениях на веб-сайте блога.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-122">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="4cb1f-123">Биография автора — это обычное содержимое представления, которое не требует выполнения кода для формирования содержимого веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-123">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="4cb1f-124">Для доступа к содержимому биографии автора представлению достаточно привязки модели, поэтому частичное представление идеально подходит для такого типа содержимого.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-124">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="4cb1f-125">[Компоненты представления](xref:mvc/views/view-components) похожи на частичные представления тем, что они также позволяют сократить повторы кода, однако они подходят для содержимого представления, которое требует выполнения кода на сервере для преобразования веб-страницы для просмотра.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-125">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="4cb1f-126">Компоненты представления полезны в тех случаях, когда для подготовки содержимого для просмотра требуется взаимодействие с базой данных, например для корзины на веб-сайте электронного магазина.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-126">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="4cb1f-127">При формировании выходных данных веб-страницы компоненты представления не ограничены привязкой модели.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-127">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="4cb1f-128">Преимущества использования представлений</span><span class="sxs-lookup"><span data-stu-id="4cb1f-128">Benefits of using views</span></span>

<span data-ttu-id="4cb1f-129">Представления помогают реализовать [разделение задач](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) в приложении MVC, изолируя разметку пользовательского интерфейса от других частей приложения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-129">Views help to establish [separation of concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="4cb1f-130">Соблюдение принципа SoC делает приложение модульным, что дает несколько преимуществ.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-130">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="4cb1f-131">Приложение проще обслуживать, так как оно лучше организовано.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-131">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="4cb1f-132">Представления, как правило, группируются по функциональным возможностям приложения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-132">Views are generally grouped by app feature.</span></span> <span data-ttu-id="4cb1f-133">Это упрощает поиск связанных представлений при работе над определенной функцией.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-133">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="4cb1f-134">Части приложения слабо связаны друг с другом.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-134">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="4cb1f-135">Вы можете разрабатывать и обновлять представления приложения отдельно от компонентов бизнес-логики и доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-135">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="4cb1f-136">При обновлении представлений приложения не обязательно обновлять другие его части.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-136">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="4cb1f-137">Части пользовательского интерфейса проще тестировать, так как представления являются отдельными модулями.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-137">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="4cb1f-138">Благодаря более упорядоченной структуре меньше вероятность того, что разделы пользовательского интерфейса будут случайно повторяться.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-138">Due to better organization, it's less likely that you'll accidentally repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="4cb1f-139">Создание представления</span><span class="sxs-lookup"><span data-stu-id="4cb1f-139">Creating a view</span></span>

<span data-ttu-id="4cb1f-140">Представления, относящиеся к определенному контроллеру, создаются в папке *Views/[имя_контроллера]*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-140">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="4cb1f-141">Представления, используемые разными контроллерами, помещаются в папку *Views/Shared*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-141">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="4cb1f-142">Чтобы создать представление, добавьте новый файл и присвойте ему имя связанного действия контроллера с расширением *CSHTML*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-142">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="4cb1f-143">Чтобы создать представление, соответствующее действию *About* контроллера *Home*, создайте файл *About.cshtml* в папке *Views/Home*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-143">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="4cb1f-144">Разметка *Razor* начинается с символа `@`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-144">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="4cb1f-145">Для выполнения операторов C# поместите код C# в [блоки кода Razor](xref:mvc/views/razor#razor-code-blocks), заключенные в фигурные скобки (`{ ... }`).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-145">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="4cb1f-146">Примером может служить приведенный выше оператор присвоения значения "About" свойству `ViewData["Title"]`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-146">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="4cb1f-147">Для отображения значений в коде HTML можно просто ссылаться на них с помощью символа `@`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-147">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="4cb1f-148">См. содержимое элементов `<h2>` и `<h3>` выше.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-148">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="4cb1f-149">Показанное выше содержимое представления — это всего лишь часть веб-страницы, отображаемой для пользователя.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-149">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="4cb1f-150">Остальная часть макета страницы и другие стандартные аспекты представления определяются в других файлах представления.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-150">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="4cb1f-151">Дополнительные сведения см. в статье [Макет](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-151">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="4cb1f-152">Указание представлений в контроллерах</span><span class="sxs-lookup"><span data-stu-id="4cb1f-152">How controllers specify views</span></span>

<span data-ttu-id="4cb1f-153">Представления, как правило, возвращаются из действий в виде объекта [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult), который является разновидностью объекта [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-153">Views are typically returned from actions as a [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="4cb1f-154">Метод действия может создавать и возвращать объект `ViewResult` напрямую, однако обычно так не делается.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-154">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="4cb1f-155">Так как большинство контроллеров наследуются от класса [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller), для возврата объекта `ViewResult` можно просто использовать вспомогательный метод `View`:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-155">Since most controllers inherit from [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="4cb1f-156">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="4cb1f-156">*HomeController.cs*</span></span>

[!code-csharp[](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="4cb1f-157">Когда это действие возвращает управление, представление *About.cshtml*, приведенное в предыдущем разделе, отрисовывается в виде следующей веб-страницы:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-157">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![Страница About в браузере Microsoft Edge](overview/_static/about-page.png)

<span data-ttu-id="4cb1f-159">Вспомогательный метод `View` имеет несколько перегрузок.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-159">The `View` helper method has several overloads.</span></span> <span data-ttu-id="4cb1f-160">Вы можете дополнительно указать:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-160">You can optionally specify:</span></span>

* <span data-ttu-id="4cb1f-161">Представление, которое нужно вернуть, явным образом:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-161">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="4cb1f-162">[Модель](xref:mvc/models/model-binding), которую нужно передать в представление:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-162">A [model](xref:mvc/models/model-binding) to pass to the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="4cb1f-163">Представление и модель:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-163">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="4cb1f-164">Обнаружение представления</span><span class="sxs-lookup"><span data-stu-id="4cb1f-164">View discovery</span></span>

<span data-ttu-id="4cb1f-165">Когда действие возвращает представление, происходит процесс, который называется *обнаружением представления*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-165">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="4cb1f-166">Он служит для определения используемого файла представления на основе имени представления.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-166">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="4cb1f-167">Метод `View` (`return View();`) по умолчанию возвращает представление с тем же именем, что и у метода действия, из которого он был вызван.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-167">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="4cb1f-168">Например, имя метода `ActionResult` действия *About* контроллера служит для поиска файла представления с именем *About.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-168">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="4cb1f-169">Сначала среда выполнения ищет представление в папке *Views/[имя_контроллера]*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-169">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="4cb1f-170">Если подходящее представление в ней не найдено, поиск производится в папке *Shared*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-170">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="4cb1f-171">Не имеет значения, возвращается ли объект `ViewResult` неявно с помощью метода `return View();` или имя представления явно передается в метод `View` с помощью `return View("<ViewName>");`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-171">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="4cb1f-172">В обоих случаях обнаружение подходящего файла представления происходит в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-172">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="4cb1f-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="4cb1f-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="4cb1f-174">*Views/Shared/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="4cb1f-174">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="4cb1f-175">Вместо имени файла можно предоставить путь к файлу представления.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-175">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="4cb1f-176">При использовании абсолютного пути, начинающегося с корня приложения (может начинаться с символов "/" или "~/"), необходимо указывать расширение *CSHTML*:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-176">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="4cb1f-177">Для указания представлений в разных каталогах можно также использовать относительный путь без расширения *CSHTML*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-177">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="4cb1f-178">Внутри `HomeController` можно вернуть представление *Index* из папки *Manage* с помощью следующего относительного пути:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-178">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="4cb1f-179">Аналогичным образом, можно указать каталог текущего контроллера с помощью префикса "./":</span><span class="sxs-lookup"><span data-stu-id="4cb1f-179">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="4cb1f-180">[Частичные представления](xref:mvc/views/partial) и [компоненты представлений](xref:mvc/views/view-components) используют похожие (но не одинаковые) механизмы обнаружения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-180">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="4cb1f-181">Настроить соглашение по умолчанию, определяющее способ поиска представлений в приложении, можно с помощью пользовательской реализации [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-181">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="4cb1f-182">Обнаружение представлений предусматривает поиск файлов представлений по имени.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-182">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="4cb1f-183">Если в базовой файловой системе учитывается регистр символов, то он, скорее всего, будет учитываться и в именах представлений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-183">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="4cb1f-184">В целях совместимости в разных операционных системах следует соблюдать одинаковый реестр символов в именах контроллеров и действий с одной стороны и в соответствующих именах файлов и папок представлений с другой.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-184">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="4cb1f-185">Если при работе в файловой системе, в которой учитывается регистр символов, возникает ошибка, связанная с тем, что не удается найти файл представления, проверьте, совпадает ли регистр символов в запрошенном и фактическом именах файлов представлений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-185">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="4cb1f-186">Для удобства и простоты работы следуйте рекомендациям по организации структуры файлов представлений, которая должна отражать взаимосвязи между контроллерами, действиями и представлениями.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-186">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="4cb1f-187">Передача данных в представления</span><span class="sxs-lookup"><span data-stu-id="4cb1f-187">Passing data to views</span></span>

<span data-ttu-id="4cb1f-188">Существует несколько подходов к передаче данных в представления:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-188">Pass data to views using several approaches:</span></span>

* <span data-ttu-id="4cb1f-189">Строго типизированные данные: viewmodel</span><span class="sxs-lookup"><span data-stu-id="4cb1f-189">Strongly typed data: viewmodel</span></span>
* <span data-ttu-id="4cb1f-190">Слабо типизированные данные</span><span class="sxs-lookup"><span data-stu-id="4cb1f-190">Weakly typed data</span></span>
  * <span data-ttu-id="4cb1f-191">`ViewData` (`ViewDataAttribute`)</span><span class="sxs-lookup"><span data-stu-id="4cb1f-191">`ViewData` (`ViewDataAttribute`)</span></span>
  * `ViewBag`

### <a name="strongly-typed-data-viewmodel"></a><span data-ttu-id="4cb1f-192">Строго типизированные данные (viewmodel)</span><span class="sxs-lookup"><span data-stu-id="4cb1f-192">Strongly typed data (viewmodel)</span></span>

<span data-ttu-id="4cb1f-193">Наиболее надежный подход — указание типа [модели](xref:mvc/models/model-binding) в представлении.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-193">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="4cb1f-194">Такая модель называется *viewmodel*.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-194">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="4cb1f-195">Экземпляр типа viewmodel передается в представление из действия.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-195">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="4cb1f-196">Использование viewmodel для передачи данных в представление позволяет ему применять *строгую* проверку типов.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-196">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="4cb1f-197">Термин *строгая типизация* (или *строго типизированный*) означает, что каждая переменная и константа имеет явным образом определенный тип (например, `string`, `int` или `DateTime`).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-197">*Strong typing* (or *strongly typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="4cb1f-198">Допустимость типов, используемых в представлении, проверяется во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-198">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="4cb1f-199">В [Visual Studio](https://www.visualstudio.com/vs/) и [Visual Studio Code](https://code.visualstudio.com/) строго типизированные члены классов перечисляются с помощью функции [IntelliSense](/visualstudio/ide/using-intellisense).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-199">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="4cb1f-200">Чтобы просмотреть свойства viewmodel, введите имя переменной viewmodel с точкой (`.`) после него.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-200">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="4cb1f-201">Это позволяет писать код быстрее, допуская меньше ошибок.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-201">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="4cb1f-202">Укажите модель с помощью директивы `@model`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-202">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="4cb1f-203">Используйте модель с `@Model`:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-203">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="4cb1f-204">Чтобы предоставить модель для представления, контроллер передает ее в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-204">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="4cb1f-205">В отношении типов моделей, которые можно предоставлять для представления, ограничений нет.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-205">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="4cb1f-206">Мы рекомендуем использовать модели представлений POCO, которые позволяют определять минимум методов или не определять их вовсе.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-206">We recommend using Plain Old CLR Object (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="4cb1f-207">Как правило, классы viewmodel хранятся либо в папке *Models*, либо в отдельной папке *ViewModels* в корне приложения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-207">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="4cb1f-208">Модель представления *Address*, используемая в приведенном выше примере, — это модель POCO, хранящаяся в файле с именем *Address.cs*:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-208">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

<span data-ttu-id="4cb1f-209">Ничто не мешает вам использовать одни и те же классы как для типов viewmodel, так и для типов бизнес-модели.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-209">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="4cb1f-210">Однако применение отдельных моделей позволяет изменять представления независимо от компонентов бизнес-логики и доступа к данным в приложении.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-210">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="4cb1f-211">Разделение моделей и моделей представлений также предоставляет преимущества в плане безопасности, когда модели используют [привязку модели](xref:mvc/models/model-binding) и [проверку](xref:mvc/models/validation) для данных, отправляемых в приложение пользователем.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-211">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>

<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-viewdata-attribute-and-viewbag"></a><span data-ttu-id="4cb1f-212">Нестрого типизированные данные (ViewData, атрибут ViewData и ViewBag)</span><span class="sxs-lookup"><span data-stu-id="4cb1f-212">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>

<span data-ttu-id="4cb1f-213">`ViewBag`Свойство  *недоступно в Razor Pages.*</span><span class="sxs-lookup"><span data-stu-id="4cb1f-213">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="4cb1f-214">Помимо строго типизированных представлений, представления имеют доступ к *нестрого типизированной* (*слабо типизированной*) коллекции данных.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-214">In addition to strongly typed views, views have access to a *weakly typed* (also called *loosely typed*) collection of data.</span></span> <span data-ttu-id="4cb1f-215">В отличие от строгих типов, *нестрогие типы* (или *слабые типы*) предполагают, что тип используемых данных не объявляется явным образом.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-215">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="4cb1f-216">Коллекцию нестрого типизированных данных можно использовать для передачи небольших объемов данных в контроллеры и представления или из них.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-216">You can use the collection of weakly typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="4cb1f-217">Передача данных между...</span><span class="sxs-lookup"><span data-stu-id="4cb1f-217">Passing data between a ...</span></span>                        | <span data-ttu-id="4cb1f-218">Пример</span><span class="sxs-lookup"><span data-stu-id="4cb1f-218">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="4cb1f-219">Контроллером и представлением</span><span class="sxs-lookup"><span data-stu-id="4cb1f-219">Controller and a view</span></span>                             | <span data-ttu-id="4cb1f-220">Заполнение раскрывающегося списка данными.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-220">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="4cb1f-221">Представлением и [представлением макета](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="4cb1f-221">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="4cb1f-222">Задание содержимого элемента **\<title>** в представлении макета из файла представления.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-222">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="4cb1f-223">[Частичным представлением](xref:mvc/views/partial) и представлением</span><span class="sxs-lookup"><span data-stu-id="4cb1f-223">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="4cb1f-224">Мини-приложение, в котором данные выводятся на основе запрошенной пользователем веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-224">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="4cb1f-225">На эту коллекцию можно ссылаться в контроллерах и представлениях посредством свойства `ViewData` или `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-225">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="4cb1f-226">Свойство `ViewData` представляет собой словарь нестрого типизированных объектов.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-226">The `ViewData` property is a dictionary of weakly typed objects.</span></span> <span data-ttu-id="4cb1f-227">Свойство `ViewBag` представляет собой оболочку для свойства `ViewData`, которая предоставляет динамические свойства для базовой коллекции `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-227">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="4cb1f-228">Свойства `ViewData` и `ViewBag` разрешаются динамически во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-228">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="4cb1f-229">Так как они не обеспечивают проверку во время компиляции, их использование обычно приводит к большему числу ошибок, чем использование viewmodel.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-229">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="4cb1f-230">По этой причине некоторые разработчики предпочитают как можно реже использовать свойства `ViewData` и `ViewBag` или не использовать их вовсе.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-230">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>

<a name="VD"></a>

<span data-ttu-id="4cb1f-231">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="4cb1f-231">**ViewData**</span></span>

<span data-ttu-id="4cb1f-232">`ViewData` — это объект [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), доступ к которому осуществляется посредством ключей `string`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-232">`ViewData` is a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="4cb1f-233">Строковые данные можно сохранять и использовать напрямую без приведения, однако при извлечении других значений объекта `ViewData` их необходимо приводить к соответствующим типам.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-233">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="4cb1f-234">С помощью свойства `ViewData` можно передавать данные, включая [частичные представления](xref:mvc/views/partial) и [макеты](xref:mvc/views/layout), из контроллеров в представления и внутри представлений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-234">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="4cb1f-235">Ниже приведен пример, в котором с помощью свойства `ViewData` в действии задаются значения для приветствия и адреса.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-235">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="4cb1f-236">Работа с данными в представлении:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-236">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="4cb1f-237">**Атрибут ViewData**</span><span class="sxs-lookup"><span data-stu-id="4cb1f-237">**ViewData attribute**</span></span>

<span data-ttu-id="4cb1f-238">Другой подход, который использует [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), — [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-238">Another approach that uses the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) is [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="4cb1f-239">Свойства на контроллерах или моделях страниц Razor, отмеченные атрибутом `[ViewData]`, обладают своими собственными значениями, загружаемыми из словаря.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-239">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the dictionary.</span></span>

<span data-ttu-id="4cb1f-240">В следующем примере контроллер Home содержит свойство `Title`, отмеченное атрибутом `[ViewData]`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-240">In the following example, the Home controller contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="4cb1f-241">Метод `About` задает заголовок для представления About:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-241">The `About` method sets the title for the About view:</span></span>

```csharp
public class HomeController : Controller
{
    [ViewData]
    public string Title { get; set; }

    public IActionResult About()
    {
        Title = "About Us";
        ViewData["Message"] = "Your application description page.";

        return View();
    }
}
```

<span data-ttu-id="4cb1f-242">В представлении About доступ к свойству `Title` осуществляется как доступ к свойству модели:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-242">In the About view, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="4cb1f-243">В макете заголовок считывается из словаря ViewData.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-243">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

<span data-ttu-id="4cb1f-244">**ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4cb1f-244">**ViewBag**</span></span>

<span data-ttu-id="4cb1f-245">`ViewBag`Свойство  *недоступно в Razor Pages.*</span><span class="sxs-lookup"><span data-stu-id="4cb1f-245">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="4cb1f-246">`ViewBag` — это объект [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), который обеспечивает динамический доступ к объектам, хранящимся в `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-246">`ViewBag` is a [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="4cb1f-247">Работать со свойством `ViewBag` может быть удобнее, так как оно не требует приведения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-247">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="4cb1f-248">В приведенном ниже примере демонстрируется использование свойства `ViewBag` с тем же результатом, что и свойства `ViewData` ранее.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-248">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="4cb1f-249">**Одновременное использование ViewData и ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4cb1f-249">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="4cb1f-250">`ViewBag`Свойство  *недоступно в Razor Pages.*</span><span class="sxs-lookup"><span data-stu-id="4cb1f-250">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="4cb1f-251">Так как свойства `ViewData` и `ViewBag` ссылаются на одну и ту же базовую коллекцию `ViewData`, вы можете использовать `ViewData` и `ViewBag` вместе в различных сочетаниях при чтении и записи значений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-251">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="4cb1f-252">Например, задайте заголовок с помощью свойства `ViewBag`, а описание с помощью свойства `ViewData` в начале представления *About.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-252">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="4cb1f-253">В этом примере свойства считываются, причем очередность использования свойств `ViewData` и `ViewBag` обратная.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-253">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="4cb1f-254">В файле *_Layout.cshtml* получите заголовок с помощью свойства `ViewData`, а описание с помощью свойства `ViewBag`:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-254">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="4cb1f-255">Помните, что строки не требуют приведения значения `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-255">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="4cb1f-256">`@ViewData["Title"]` можно использовать без приведения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-256">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="4cb1f-257">Свойства `ViewData` и `ViewBag` можно использовать одновременно в различных сочетаниях для считывания и записи значений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-257">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="4cb1f-258">Следующая разметка будет обработана:</span><span class="sxs-lookup"><span data-stu-id="4cb1f-258">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="4cb1f-259">**Сводка различий между ViewData и ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4cb1f-259">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="4cb1f-260">Свойство `ViewBag` недоступно в Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-260">`ViewBag` isn't available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="4cb1f-261">Является производным от [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), поэтому имеет свойства словаря, которые могут быть полезны, например `ContainsKey`, `Add`, `Remove` и `Clear`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-261">Derives from [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="4cb1f-262">Ключи в словаре представляют собой строки, поэтому пробел допустим.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-262">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="4cb1f-263">Пример: `ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="4cb1f-263">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="4cb1f-264">Любой тип, кроме `string`, должен быть приведен в представлении так, чтобы он мог использоваться в `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-264">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="4cb1f-265">Является производным от [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), поэтому позволяет создавать динамические свойства с помощью точечной нотации (`@ViewBag.SomeKey = <value or object>`); приведение не требуется.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-265">Derives from [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="4cb1f-266">Синтаксис свойства `ViewBag` позволяет быстрее добавлять его в контроллеры и представления.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-266">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="4cb1f-267">Проще проверять значение NULL.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-267">Simpler to check for null values.</span></span> <span data-ttu-id="4cb1f-268">Пример: `@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="4cb1f-268">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="4cb1f-269">**Выбор между ViewData и ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4cb1f-269">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="4cb1f-270">Свойства `ViewData` и `ViewBag` в равной степени подходят для передачи небольших объемов данных между контроллерами и представлениями.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-270">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="4cb1f-271">Выбор одного из них зависит от предпочтений.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-271">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="4cb1f-272">Вы можете сочетать объекты `ViewData` и `ViewBag`, однако код будет проще для восприятия и обслуживания при последовательном применении одного подхода.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-272">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="4cb1f-273">Оба свойства разрешаются динамически во время выполнения и поэтому могут приводить к ошибкам во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-273">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="4cb1f-274">Некоторые команды разработчиков избегают их использования.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-274">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="4cb1f-275">Динамические представления</span><span class="sxs-lookup"><span data-stu-id="4cb1f-275">Dynamic views</span></span>

<span data-ttu-id="4cb1f-276">Представления, в которых тип модели не объявляется с помощью `@model`, но в которые вместо этого передается экземпляр модели (например, `return View(Address);`), могут ссылаться на свойства экземпляра динамически.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-276">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="4cb1f-277">Эта возможность повышает гибкость, но не обеспечивает защиту компиляции или функцию IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-277">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="4cb1f-278">Если свойство не существует, создание веб-страницы завершается сбоем во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-278">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="4cb1f-279">Дополнительные возможности представлений</span><span class="sxs-lookup"><span data-stu-id="4cb1f-279">More view features</span></span>

<span data-ttu-id="4cb1f-280">[Вспомогательные функции тегов](xref:mvc/views/tag-helpers/intro) упрощают реализацию поведения на стороне сервера в существующих HTML-тегах.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-280">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="4cb1f-281">Их применение избавляет от необходимости писать пользовательский код или вспомогательные функции в представлениях.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-281">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="4cb1f-282">Вспомогательные функции тегов применяются к элементам HTML как атрибуты и игнорируются редакторами, которые не поддерживают их.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-282">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="4cb1f-283">Это позволяет редактировать и подготавливать разметку представлений для просмотра в различных средствах.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-283">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="4cb1f-284">Пользовательская HTML-разметка может формироваться с помощью множества встроенных вспомогательных функций HTML.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-284">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="4cb1f-285">Более сложная логика пользовательского интерфейса может обрабатываться [компонентами представлений](xref:mvc/views/view-components).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-285">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="4cb1f-286">Компоненты представлений предоставляют те же возможности SoC, что и контроллеры и представления.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-286">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="4cb1f-287">Они могут устранить необходимость в действиях и представлениях, предназначенных для работы с данными, которые используются общими элементами пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="4cb1f-287">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="4cb1f-288">Как и многие другие аспекты ASP.NET Core, представления поддерживают [внедрение зависимостей](xref:fundamentals/dependency-injection), которое позволяет [внедрять службы в представления](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="4cb1f-288">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>
