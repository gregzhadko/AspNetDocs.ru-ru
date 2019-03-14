---
ms.openlocfilehash: 24726fba7f431f701b264a988a8de1b67d41d8a2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048721"
---
# <a name="add-search-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="90df5-101">Добавление поиска в приложение MVC ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="90df5-101">Add search to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="90df5-102">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="90df5-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="90df5-103">В этом разделе вы добавите в метод действия `Index` возможности поиска, которые позволяют выполнять поиск фильмов по *жанру* или *имени*.</span><span class="sxs-lookup"><span data-stu-id="90df5-103">In this section you add search capability to the `Index` action method that lets you search movies by *genre* or *name*.</span></span>

<span data-ttu-id="90df5-104">Обновите метод `Index`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="90df5-104">Update the `Index` method with the following code:</span></span>
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]
-->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

<span data-ttu-id="90df5-105">В первой строке метода действия `Index` создается запрос [LINQ](/dotnet/standard/using-linq) для выбора фильмов:</span><span class="sxs-lookup"><span data-stu-id="90df5-105">The first line of the `Index` action method creates a [LINQ](/dotnet/standard/using-linq) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="90df5-106">Этот запрос *только* определяется в этой точке и **не** выполняется для базы данных.</span><span class="sxs-lookup"><span data-stu-id="90df5-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="90df5-107">Если параметр `searchString` содержит строку, запрос фильмов изменяется для фильтрации по значению в строке поиска:</span><span class="sxs-lookup"><span data-stu-id="90df5-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

<span data-ttu-id="90df5-108">Приведенный выше код `s => s.Title.Contains()` представляет собой [лямбда-выражение](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span><span class="sxs-lookup"><span data-stu-id="90df5-108">The `s => s.Title.Contains()` code above is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="90df5-109">Лямбда-выражения используются в запросах [LINQ](/dotnet/standard/using-linq) на основе методов в качестве аргументов стандартных методов операторов запроса, таких как метод [Where](/dotnet/api/system.linq.enumerable.where) или `Contains` (используется в приведенном выше коде).</span><span class="sxs-lookup"><span data-stu-id="90df5-109">Lambdas are used in method-based [LINQ](/dotnet/standard/using-linq) queries as arguments to standard query operator methods such as the [Where](/dotnet/api/system.linq.enumerable.where) method or `Contains` (used in the code above).</span></span> <span data-ttu-id="90df5-110">Запросы LINQ не выполняются, если они определяются или изменяются путем вызова метода (например, `Where`, `Contains` или `OrderBy`).</span><span class="sxs-lookup"><span data-stu-id="90df5-110">LINQ queries are not executed when they're defined or when they're modified by calling a method such as `Where`, `Contains`  or `OrderBy`.</span></span> <span data-ttu-id="90df5-111">Вместо этого выполнение запроса откладывается.</span><span class="sxs-lookup"><span data-stu-id="90df5-111">Rather, query execution is deferred.</span></span>  <span data-ttu-id="90df5-112">Это означает, что вычисление выражения откладывается до тех пор, пока не будет выполнена итерация его реализованного значения или пока не будет вызван метод `ToListAsync`.</span><span class="sxs-lookup"><span data-stu-id="90df5-112">That means that the evaluation of an expression is delayed until its realized value is actually iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="90df5-113">Дополнительные сведения об отложенном и немедленном выполнении запросов см. в разделе [Выполнение запроса](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span><span class="sxs-lookup"><span data-stu-id="90df5-113">For more information about deferred query execution, see [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span></span>

<span data-ttu-id="90df5-114">Примечание. Метод [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) выполняется в базе данных, а не в коде C#, приведенном выше.</span><span class="sxs-lookup"><span data-stu-id="90df5-114">Note: The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the c# code shown above.</span></span> <span data-ttu-id="90df5-115">Регистр символов запроса учитывается в зависимости от параметров базы данных и сортировки.</span><span class="sxs-lookup"><span data-stu-id="90df5-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="90df5-116">В SQL Server метод[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) сопоставляется с [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), в котором регистр символов не учитывается.</span><span class="sxs-lookup"><span data-stu-id="90df5-116">On SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="90df5-117">В SQLite при параметрах сортировки по умолчанию регистр символов учитывается.</span><span class="sxs-lookup"><span data-stu-id="90df5-117">In SQLlite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="90df5-118">Перейдите к `/Movies/Index`.</span><span class="sxs-lookup"><span data-stu-id="90df5-118">Navigate to `/Movies/Index`.</span></span> <span data-ttu-id="90df5-119">Добавьте в URL-адрес строку запроса, например `?searchString=Ghost`.</span><span class="sxs-lookup"><span data-stu-id="90df5-119">Append a query string such as `?searchString=Ghost` to the URL.</span></span> <span data-ttu-id="90df5-120">Отображаются отфильтрованные фильмы.</span><span class="sxs-lookup"><span data-stu-id="90df5-120">The filtered movies are displayed.</span></span>

![Представление Index](~/tutorials/first-mvc-app/search/_static/ghost.png)

<span data-ttu-id="90df5-122">Если вы изменили сигнатуру метода `Index` и включили в нее параметр с именем `id`, параметр `id` будет соответствовать необязательному заполнителю `{id}` для маршрутов по умолчанию, который задан в файле *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="90df5-122">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the optional `{id}` placeholder for the default routes set in *Startup.cs*.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]
