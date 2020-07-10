---
uid: mvc/overview/getting-started/introduction/adding-search
title: Поиск | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211469"
---
# <a name="search"></a><span data-ttu-id="2db96-102">Поиск</span><span class="sxs-lookup"><span data-stu-id="2db96-102">Search</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="2db96-103">Добавление метода поиска и представления поиска</span><span class="sxs-lookup"><span data-stu-id="2db96-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="2db96-104">В этом разделе вы добавите функцию поиска в `Index` метод действия, который позволяет искать фильмы по жанру или названию.</span><span class="sxs-lookup"><span data-stu-id="2db96-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2db96-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2db96-105">Prerequisites</span></span>

<span data-ttu-id="2db96-106">Чтобы сопоставить снимки экрана этого раздела, необходимо запустить приложение (F5) и добавить в базу данных следующие фильмы.</span><span class="sxs-lookup"><span data-stu-id="2db96-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="2db96-107">Название</span><span class="sxs-lookup"><span data-stu-id="2db96-107">Title</span></span> | <span data-ttu-id="2db96-108">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="2db96-108">Release Date</span></span> | <span data-ttu-id="2db96-109">Genre</span><span class="sxs-lookup"><span data-stu-id="2db96-109">Genre</span></span> | <span data-ttu-id="2db96-110">Цена</span><span class="sxs-lookup"><span data-stu-id="2db96-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="2db96-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="2db96-111">Ghostbusters</span></span> | <span data-ttu-id="2db96-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="2db96-112">6/8/1984</span></span> | <span data-ttu-id="2db96-113">Комедия</span><span class="sxs-lookup"><span data-stu-id="2db96-113">Comedy</span></span> | <span data-ttu-id="2db96-114">6,99</span><span class="sxs-lookup"><span data-stu-id="2db96-114">6.99</span></span> |
| <span data-ttu-id="2db96-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="2db96-115">Ghostbusters II</span></span> | <span data-ttu-id="2db96-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="2db96-116">6/16/1989</span></span> | <span data-ttu-id="2db96-117">Комедия</span><span class="sxs-lookup"><span data-stu-id="2db96-117">Comedy</span></span> | <span data-ttu-id="2db96-118">6,99</span><span class="sxs-lookup"><span data-stu-id="2db96-118">6.99</span></span> |
| <span data-ttu-id="2db96-119">Планета АПЕС</span><span class="sxs-lookup"><span data-stu-id="2db96-119">Planet of the Apes</span></span> | <span data-ttu-id="2db96-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="2db96-120">3/27/1986</span></span> | <span data-ttu-id="2db96-121">Действие</span><span class="sxs-lookup"><span data-stu-id="2db96-121">Action</span></span> | <span data-ttu-id="2db96-122">5,99</span><span class="sxs-lookup"><span data-stu-id="2db96-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="2db96-123">Обновление формы индекса</span><span class="sxs-lookup"><span data-stu-id="2db96-123">Updating the Index Form</span></span>

<span data-ttu-id="2db96-124">Начните с обновления `Index` метода действия до существующего `MoviesController` класса.</span><span class="sxs-lookup"><span data-stu-id="2db96-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="2db96-125">Вот этот код:</span><span class="sxs-lookup"><span data-stu-id="2db96-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="2db96-126">Первая строка `Index` метода создает следующий запрос [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) для выбора фильмов:</span><span class="sxs-lookup"><span data-stu-id="2db96-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="2db96-127">Запрос определен на этом этапе, но еще не выполнялся для базы данных.</span><span class="sxs-lookup"><span data-stu-id="2db96-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="2db96-128">Если `searchString` параметр содержит строку, запрос фильмов изменяется для фильтрации по значению строки поиска с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="2db96-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="2db96-129">Приведенный выше код `s => s.Title` представляет собой [лямбда-выражение](https://msdn.microsoft.com/library/bb397687.aspx).</span><span class="sxs-lookup"><span data-stu-id="2db96-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="2db96-130">Лямбда-выражения используются в запросах [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) на основе методов в качестве аргументов методов стандартных операторов запросов, таких как метод [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) , используемый в приведенном выше коде.</span><span class="sxs-lookup"><span data-stu-id="2db96-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="2db96-131">Запросы LINQ не выполняются, если они определены или изменяются путем вызова метода, такого как `Where` или `OrderBy` .</span><span class="sxs-lookup"><span data-stu-id="2db96-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="2db96-132">Вместо этого выполнение запроса откладывается, что означает, что вычисление выражения откладывается до тех пор, пока его реализованное значение фактически не будет перебираться или [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) метод не будет вызван.</span><span class="sxs-lookup"><span data-stu-id="2db96-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="2db96-133">В этом `Search` примере запрос выполняется в представлении *index. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="2db96-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="2db96-134">Дополнительные сведения об отложенном и немедленном выполнении запросов см. в разделе [Выполнение запроса](https://msdn.microsoft.com/library/bb738633.aspx).</span><span class="sxs-lookup"><span data-stu-id="2db96-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2db96-135">Метод [Contains](https://msdn.microsoft.com/library/bb155125.aspx) выполняется в базе данных, а не в коде c#, приведенном выше.</span><span class="sxs-lookup"><span data-stu-id="2db96-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="2db96-136">В базе данных [содержит](https://msdn.microsoft.com/library/bb155125.aspx) сопоставление с [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), в котором регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="2db96-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="2db96-137">Теперь можно обновить `Index` представление, которое будет отображать форму пользователю.</span><span class="sxs-lookup"><span data-stu-id="2db96-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="2db96-138">Запустите приложение и перейдите по адресу */мовиес/индекс*.</span><span class="sxs-lookup"><span data-stu-id="2db96-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="2db96-139">Добавьте в URL-адрес строку запроса, например `?searchString=ghost`.</span><span class="sxs-lookup"><span data-stu-id="2db96-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="2db96-140">Отображаются отфильтрованные фильмы.</span><span class="sxs-lookup"><span data-stu-id="2db96-140">The filtered movies are displayed.</span></span>

![сеарчкристр](adding-search/_static/image1.png)

<span data-ttu-id="2db96-142">Если изменить сигнатуру `Index` метода для параметра с именем `id` , `id` параметр будет соответствовать `{id}` заполнительу для маршрутов по умолчанию, заданных в файле \* \_ старт\раутеконфиг.КС приложения\* .</span><span class="sxs-lookup"><span data-stu-id="2db96-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="2db96-143">Исходный `Index` метод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2db96-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="2db96-144">Измененный `Index` метод будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2db96-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="2db96-145">Теперь можно передать заголовок поиска в качестве данных маршрута (сегмент URL-адреса) вместо значения строки запроса.</span><span class="sxs-lookup"><span data-stu-id="2db96-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="2db96-146">Тем не менее пользователи вряд ли будут каждый раз изменять URL-адрес для поиска фильмов.</span><span class="sxs-lookup"><span data-stu-id="2db96-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="2db96-147">Итак, теперь вам необходимо добавить пользовательский интерфейс для удобства фильтрации фильмов.</span><span class="sxs-lookup"><span data-stu-id="2db96-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="2db96-148">Если вы изменили сигнатуру `Index` метода, чтобы проверить, как передать параметр идентификатора, привязанного к маршруту, измените его обратно, чтобы метод задавал `Index` строковый параметр с именем `searchString` :</span><span class="sxs-lookup"><span data-stu-id="2db96-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="2db96-149">Откройте файл *виевс\мовиес\индекс.кштмл* и сразу после `@Html.ActionLink("Create New", "Create")` добавьте разметку формы, выделенную ниже:</span><span class="sxs-lookup"><span data-stu-id="2db96-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="2db96-150">`Html.BeginForm`Вспомогательный объект создает открывающий `<form>` тег.</span><span class="sxs-lookup"><span data-stu-id="2db96-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="2db96-151">`Html.BeginForm`Вспомогательная функция заставляет форму опубликовать себя, когда пользователь отправит форму, нажав кнопку **Фильтр** .</span><span class="sxs-lookup"><span data-stu-id="2db96-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="2db96-152">Visual Studio 2013 имеет хорошее улучшение при отображении и изменении файлов представления.</span><span class="sxs-lookup"><span data-stu-id="2db96-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="2db96-153">При запуске приложения с открытым файлом представления Visual Studio 2013 вызывает правильный метод действия контроллера для отображения представления.</span><span class="sxs-lookup"><span data-stu-id="2db96-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="2db96-154">Откройте представление индекса в Visual Studio (как показано на рисунке выше), нажмите клавишу CTRL F5 или F5, чтобы запустить приложение, а затем попробуйте найти фильм.</span><span class="sxs-lookup"><span data-stu-id="2db96-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="2db96-155">`HttpPost`Перегрузка `Index` метода отсутствует.</span><span class="sxs-lookup"><span data-stu-id="2db96-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="2db96-156">Это не требуется, так как метод не изменяет состояние приложения, просто отфильтровывая данные.</span><span class="sxs-lookup"><span data-stu-id="2db96-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="2db96-157">Можно добавить следующий метод `HttpPost Index`.</span><span class="sxs-lookup"><span data-stu-id="2db96-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="2db96-158">В этом случае вызывающий элемент действия будет соответствовать `HttpPost Index` методу, и `HttpPost Index` метод будет выполняться, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="2db96-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![сеарчпостгхост](adding-search/_static/image5.png)

<span data-ttu-id="2db96-160">Тем не менее при добавлении этой версии `HttpPost` метода `Index` существует ограничение на общую реализацию.</span><span class="sxs-lookup"><span data-stu-id="2db96-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="2db96-161">Допустим, вам необходимо добавить в закладки конкретный поиск или отправить друзьям ссылку, по которой они могут просмотреть аналогичный отфильтрованный список фильмов.</span><span class="sxs-lookup"><span data-stu-id="2db96-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="2db96-162">Обратите внимание на то, что URL-адрес запроса HTTP POST совпадает с URL-адресом для запроса GET (localhost: XXXXX/Movies/index) — в самом URL-адресе отсутствует информация для поиска.</span><span class="sxs-lookup"><span data-stu-id="2db96-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="2db96-163">Сейчас данные строки поиска отправляются на сервер в виде значения поля формы.</span><span class="sxs-lookup"><span data-stu-id="2db96-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="2db96-164">Это означает, что вы не сможете записать эту информацию для поиска в закладки или отправить друзьям по URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="2db96-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="2db96-165">Решение заключается в использовании перегрузки `BeginForm` , указывающей, что запрос POST должен добавить сведения для поиска в URL-адрес и направлять его в `HttpGet` версию `Index` метода.</span><span class="sxs-lookup"><span data-stu-id="2db96-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="2db96-166">Замените существующий `BeginForm` метод без параметров на следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="2db96-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="2db96-168">Теперь при отправке поиска URL-адрес содержит строку запроса поиска.</span><span class="sxs-lookup"><span data-stu-id="2db96-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="2db96-169">Поиск также переносится в метод `HttpGet Index`, даже если у вас определен метод `HttpPost Index`.</span><span class="sxs-lookup"><span data-stu-id="2db96-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![индексвисжетурл](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="2db96-171">Добавление поиска по жанру</span><span class="sxs-lookup"><span data-stu-id="2db96-171">Adding Search by Genre</span></span>

<span data-ttu-id="2db96-172">Если вы добавили `HttpPost` версию `Index` метода, удалите ее сейчас.</span><span class="sxs-lookup"><span data-stu-id="2db96-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="2db96-173">Далее предстоит добавить функцию, позволяющую пользователям искать фильмы по жанрам.</span><span class="sxs-lookup"><span data-stu-id="2db96-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="2db96-174">Замените метод `Index` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2db96-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="2db96-175">Эта версия `Index` метода принимает дополнительный параметр, а именно `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="2db96-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="2db96-176">Первые несколько строк кода создают `List` объект для хранения жанров фильмов из базы данных.</span><span class="sxs-lookup"><span data-stu-id="2db96-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="2db96-177">Следующий код определяет запрос LINQ, который извлекает все жанры из базы данных.</span><span class="sxs-lookup"><span data-stu-id="2db96-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="2db96-178">Код использует `AddRange` метод универсальной `List` коллекции, чтобы добавить в список все отдельные жанры.</span><span class="sxs-lookup"><span data-stu-id="2db96-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="2db96-179">(Без `Distinct` модификатора добавляются дубликаты жанров, например, в нашем примере комедия будет добавляться дважды).</span><span class="sxs-lookup"><span data-stu-id="2db96-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="2db96-180">Затем в коде сохраняется список жанров в `ViewBag.MovieGenre` объекте.</span><span class="sxs-lookup"><span data-stu-id="2db96-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="2db96-181">Хранение данных категорий (таких как жанры фильмов) в виде объекта [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) в `ViewBag` , а доступ к данным категории в раскрывающемся списке является типичным подходом для приложений MVC.</span><span class="sxs-lookup"><span data-stu-id="2db96-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="2db96-182">В следующем коде показано, как проверить `movieGenre` параметр.</span><span class="sxs-lookup"><span data-stu-id="2db96-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="2db96-183">Если он не пуст, код дополнительно ограничивает запрос фильмов, чтобы ограничить выбранные фильмы указанным жанром.</span><span class="sxs-lookup"><span data-stu-id="2db96-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="2db96-184">Как уже отмечалось ранее, запрос не выполняется в базе данных до тех пор, пока список фильмов не будет перебираться (что происходит в представлении после `Index` возврата метода действия).</span><span class="sxs-lookup"><span data-stu-id="2db96-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="2db96-185">Добавление разметки в представление индекса для поддержки поиска по жанру</span><span class="sxs-lookup"><span data-stu-id="2db96-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="2db96-186">Добавьте `Html.DropDownList` вспомогательную функцию в файл *виевс\мовиес\индекс.кштмл* непосредственно перед `TextBox` вспомогательным модулем.</span><span class="sxs-lookup"><span data-stu-id="2db96-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="2db96-187">Готовая разметка показана ниже:</span><span class="sxs-lookup"><span data-stu-id="2db96-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="2db96-188">В приведенном ниже коде выполняется следующее:</span><span class="sxs-lookup"><span data-stu-id="2db96-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="2db96-189">Параметр "Мовиеженре" предоставляет ключ для `DropDownList` вспомогательного метода для поиска `IEnumerable<SelectListItem>` в `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="2db96-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="2db96-190">`ViewBag`Заполняется в методе действия:</span><span class="sxs-lookup"><span data-stu-id="2db96-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="2db96-191">Параметр «ALL» предоставляет метку параметра.</span><span class="sxs-lookup"><span data-stu-id="2db96-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="2db96-192">Если вы проверите этот вариант в браузере, вы увидите, что его атрибут "value" пуст.</span><span class="sxs-lookup"><span data-stu-id="2db96-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="2db96-193">Так как наш контроллер фильтрует только `if` строку или не является `null` пустой, при отправке пустого значения для `movieGenre` отображаются все жанры.</span><span class="sxs-lookup"><span data-stu-id="2db96-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="2db96-194">Можно также задать параметр, который будет выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2db96-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="2db96-195">Если вы хотите «комедия» в качестве параметра по умолчанию, измените код в контроллере следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2db96-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="2db96-196">Запустите приложение и перейдите по */мовиес/индекс*.</span><span class="sxs-lookup"><span data-stu-id="2db96-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="2db96-197">Попробуйте поиск по жанру, по имени фильма и по обоим критериям.</span><span class="sxs-lookup"><span data-stu-id="2db96-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="2db96-198">В этом разделе вы создали метод действия поиска и представление, которые позволяют пользователям выполнять поиск по названию и жанру фильма.</span><span class="sxs-lookup"><span data-stu-id="2db96-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="2db96-199">В следующем разделе вы узнаете, как добавить свойство в `Movie` модель и как добавить инициализатор, который будет автоматически создавать тестовую базу данных.</span><span class="sxs-lookup"><span data-stu-id="2db96-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2db96-200">[Назад](examining-the-edit-methods-and-edit-view.md)
> [Вперед](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
