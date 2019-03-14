---
ms.openlocfilehash: e098ad497b13b4add583de017885cdbed952a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036761"
---
<!-- This include not used by windows version -->
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="a2bd2-101">Добавление нового поля в приложение MVC ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a2bd2-101">Add a new field to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="a2bd2-102">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="a2bd2-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a2bd2-103">В этом руководстве в таблицу `Movies` добавляется новое поле.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-103">This tutorial will add a new field to the `Movies` table.</span></span> <span data-ttu-id="a2bd2-104">После изменения схемы (и добавления нового поля) мы удалим старую базу данных и создадим новую.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-104">We'll drop the database and create a new one when we change the schema (add a new field).</span></span> <span data-ttu-id="a2bd2-105">Этот подход применяется на ранней стадии разработки, когда в базе отсутствуют важные рабочие данные.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-105">This workflow works well early in development when we don't have any production data to perserve.</span></span>

<span data-ttu-id="a2bd2-106">После того, как приложение развернуто и содержит нужные данные, при изменении схемы нельзя удалять существующую базу данных.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-106">Once your app is deployed and you have data that you need to perserve, you can't drop your DB when you need to change the schema.</span></span> <span data-ttu-id="a2bd2-107">Платформа Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) позволяет обновлять схему и переносить базу данных без потери данных.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-107">Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) allows you to update your schema and migrate the database without losing data.</span></span> <span data-ttu-id="a2bd2-108">При работе с SQL Server миграция выполняется достаточно часто, но в SQLlite набор операций, связанных со схемой миграции, крайне ограничен.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-108">Migrations is a popular feature when using SQL Server, but SQLlite doesn't support many migration schema operations, so only very simply migrations are possible.</span></span> <span data-ttu-id="a2bd2-109">Дополнительные сведения см. в разделе [Ограничения в SQLite](/ef/core/providers/sqlite/limitations).</span><span class="sxs-lookup"><span data-stu-id="a2bd2-109">See [SQLite Limitations](/ef/core/providers/sqlite/limitations) for more information.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="a2bd2-110">Добавление свойства Rating в модель Movie</span><span class="sxs-lookup"><span data-stu-id="a2bd2-110">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="a2bd2-111">Откройте файл *Models/Movie.cs* и добавьте свойство `Rating`:</span><span class="sxs-lookup"><span data-stu-id="a2bd2-111">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Models/MovieDateRating.cs?highlight=12&name=snippet)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

::: moniker-end

<span data-ttu-id="a2bd2-112">Поскольку в класс `Movie` было добавлено новое поле, необходимо также обновить белый список привязки, включив в него новое свойство.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-112">Because you've added a new field to the `Movie` class, you also need to update the binding whitelist so this new property will be included.</span></span> <span data-ttu-id="a2bd2-113">В файле *MoviesController.cs* обновите атрибут `[Bind]` для методов действия `Create` и `Edit`, включив свойство `Rating`:</span><span class="sxs-lookup"><span data-stu-id="a2bd2-113">In *MoviesController.cs*, update the `[Bind]` attribute for both the `Create` and `Edit` action methods to include the `Rating` property:</span></span>

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

<span data-ttu-id="a2bd2-114">Также необходимо обновить шаблоны представлений, чтобы реализовать отображение, создание и редактирование нового свойства `Rating` в представлении браузера.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-114">You also need to update the view templates in order to display, create, and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="a2bd2-115">Измените файл */Views/Movies/Index.cshtml* и добавьте поле `Rating`:</span><span class="sxs-lookup"><span data-stu-id="a2bd2-115">Edit the */Views/Movies/Index.cshtml* file and add a `Rating` field:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexGenreRating.cshtml?highlight=17,39&range=24-64)]

<span data-ttu-id="a2bd2-116">Обновите файл */Views/Movies/Create.cshtml*, указав поле `Rating`.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-116">Update the */Views/Movies/Create.cshtml* with a `Rating` field.</span></span>

<span data-ttu-id="a2bd2-117">Для работы приложения необходимо обновить базу данных, включив в нее новое поле.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-117">The app won't work until we update the DB to include the new field.</span></span> <span data-ttu-id="a2bd2-118">Если запустить приложение сейчас, появится следующее исключение `SqliteException`:</span><span class="sxs-lookup"><span data-stu-id="a2bd2-118">If you run it now, you'll get the following `SqliteException`:</span></span>

```
SqliteException: SQLite Error 1: 'no such column: m.Rating'.
```

<span data-ttu-id="a2bd2-119">Эта ошибка связана с тем, что обновленный класс модели Movie отличается от схемы таблицы Movie в существующей базе данных.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-119">You're seeing this error because the updated Movie model class is different than the schema of the Movie table of the existing database.</span></span> <span data-ttu-id="a2bd2-120">(В таблице базы данных отсутствует столбец `Rating`.)</span><span class="sxs-lookup"><span data-stu-id="a2bd2-120">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="a2bd2-121">Устранить эту ошибку можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="a2bd2-121">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="a2bd2-122">Можно удалить базу данных и затем с помощью Entity Framework автоматически повторно создать ее на основе новой схемы класса модели.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-122">Drop the database and have the Entity Framework automatically re-create the database based on the new model class schema.</span></span> <span data-ttu-id="a2bd2-123">При таком подходе теряются существующие данные в базе, поэтому он не применяется для рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-123">With this approach, you lose existing data in the database — so you can't do this with a production database!</span></span> <span data-ttu-id="a2bd2-124">При разработке приложения часто используется инициализатор для автоматического заполнения базы тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-124">Using an initializer to automatically seed a database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="a2bd2-125">Можно вручную изменить схему существующей базы данных в соответствии с новыми классами модели.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-125">Manually modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="a2bd2-126">Преимущество такого подхода состоит в том, что сохраняются все данные.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-126">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="a2bd2-127">Это изменение можно выполнить как вручную, так и с помощью соответствующего скрипта базы данных.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-127">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="a2bd2-128">Можно обновить схему базы данных с помощью Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-128">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="a2bd2-129">В рамках этого руководства мы удалим и повторно создадим базу данных при изменении схемы.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-129">For this tutorial, we'll drop and re-create the database when the schema changes.</span></span> <span data-ttu-id="a2bd2-130">Для удаления базы данных выполните следующую команду из терминала:</span><span class="sxs-lookup"><span data-stu-id="a2bd2-130">Run the following command from a terminal to drop the db:</span></span>

`dotnet ef database drop`

<span data-ttu-id="a2bd2-131">Обновите класс `SeedData` так, чтобы он предоставлял значение нового столбца.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-131">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="a2bd2-132">Ниже показан пример изменения, которое необходимо выполнить для каждого `new Movie`.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-132">A sample change is shown below, but you'll want to make this change for each `new Movie`.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

<span data-ttu-id="a2bd2-133">Добавьте поле `Rating` в представления `Edit`, `Details` и `Delete`.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-133">Add the `Rating` field to the `Edit`, `Details`, and `Delete` view.</span></span>

<span data-ttu-id="a2bd2-134">Запустите приложение и проверьте возможность создания, редактирования и отображения фильмов с использованием поля `Rating`.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-134">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="a2bd2-135">шаблоны.</span><span class="sxs-lookup"><span data-stu-id="a2bd2-135">templates.</span></span>
