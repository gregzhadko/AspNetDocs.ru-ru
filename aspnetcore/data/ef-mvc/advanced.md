---
title: Учебник. Сведения о сложных сценариях для ASP.NET MVC с EF Core
description: В этом учебнике описываются полезные рекомендации по расширенным возможностям разработки веб-приложений ASP.NET Core, использующих платформу Entity Framework Core.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/05/2019
ms.topic: tutorial
uid: data/ef-mvc/advanced
ms.openlocfilehash: f02aa1d6d8e431e7e2613835b3216786aed4ecd4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064671"
---
# <a name="tutorial-learn-about-advanced-scenarios---aspnet-mvc-with-ef-core"></a><span data-ttu-id="d3bcf-103">Учебник. Сведения о сложных сценариях для ASP.NET MVC с EF Core</span><span class="sxs-lookup"><span data-stu-id="d3bcf-103">Tutorial: Learn about advanced scenarios - ASP.NET MVC with EF Core</span></span>

<span data-ttu-id="d3bcf-104">В предыдущем учебнике было реализовано наследование типа "одна таблица на иерархию".</span><span class="sxs-lookup"><span data-stu-id="d3bcf-104">In the previous tutorial, you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="d3bcf-105">В этом учебнике описываются некоторые расширенные возможности, не относящиеся к базовой разработке веб-приложений ASP.NET Core, использующих платформу Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-105">This tutorial introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET Core web applications that use Entity Framework Core.</span></span>

<span data-ttu-id="d3bcf-106">В этом учебнике рассмотрены следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-106">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d3bcf-107">Выполнение прямых SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-107">Perform raw SQL queries</span></span>
> * <span data-ttu-id="d3bcf-108">Вызов запроса для получения сущностей</span><span class="sxs-lookup"><span data-stu-id="d3bcf-108">Call a query to return entities</span></span>
> * <span data-ttu-id="d3bcf-109">Вызов запроса для получения других типов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-109">Call a query to return other types</span></span>
> * <span data-ttu-id="d3bcf-110">Вызов запроса на обновление</span><span class="sxs-lookup"><span data-stu-id="d3bcf-110">Call an update query</span></span>
> * <span data-ttu-id="d3bcf-111">Изучение SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-111">Examine SQL queries</span></span>
> * <span data-ttu-id="d3bcf-112">Создание уровня абстракции</span><span class="sxs-lookup"><span data-stu-id="d3bcf-112">Create an abstraction layer</span></span>
> * <span data-ttu-id="d3bcf-113">Сведения об автоматическом обнаружении изменений</span><span class="sxs-lookup"><span data-stu-id="d3bcf-113">Learn about Automatic change detection</span></span>
> * <span data-ttu-id="d3bcf-114">Сведения об исходном коде EF Core и планах разработки</span><span class="sxs-lookup"><span data-stu-id="d3bcf-114">Learn about EF Core source code and development plans</span></span>
> * <span data-ttu-id="d3bcf-115">Сведения об использовании динамических запросов LINQ для упрощения кода</span><span class="sxs-lookup"><span data-stu-id="d3bcf-115">Learn how to use dynamic LINQ to simplify code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3bcf-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3bcf-116">Prerequisites</span></span>

* <span data-ttu-id="d3bcf-117">Выполните инструкции из руководства [ASP.NET Core MVC с EF Core — наследование — 9 из 10](inheritance.md)</span><span class="sxs-lookup"><span data-stu-id="d3bcf-117">[Implement Inheritance with EF Core in an ASP.NET Core MVC web app](inheritance.md)</span></span>

## <a name="perform-raw-sql-queries"></a><span data-ttu-id="d3bcf-118">Выполнение прямых SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-118">Perform raw SQL queries</span></span>

<span data-ttu-id="d3bcf-119">Одним из преимуществ использования платформы Entity Framework является возможность избежать слишком тесной привязки кода к конкретному способу хранения данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-119">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="d3bcf-120">Это достигается путем автоматического создания запросов и команд SQL, что позволяет упростить написание кода.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-120">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="d3bcf-121">Тем не менее в редких случаях требуется выполнять созданные вручную SQL-запросы.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-121">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created.</span></span> <span data-ttu-id="d3bcf-122">Для таких сценариев в API Entity Framework Code First включены методы, позволяющие передавать команды SQL напрямую в базу данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-122">For these scenarios, the Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="d3bcf-123">В EF Core 1.0 доступны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-123">You have the following options in EF Core 1.0:</span></span>

* <span data-ttu-id="d3bcf-124">Использование метода `DbSet.FromSql` для запросов, которые возвращают типы сущностей.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-124">Use the `DbSet.FromSql` method for queries that return entity types.</span></span> <span data-ttu-id="d3bcf-125">Возвращаемые объекты должны иметь тип, ожидаемый объектом `DbSet`, и автоматически отслеживаются контекстом базы данных, кроме случаев, когда [отслеживание отключено](crud.md#no-tracking-queries).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-125">The returned objects must be of the type expected by the `DbSet` object, and they're automatically tracked by the database context unless you [turn tracking off](crud.md#no-tracking-queries).</span></span>

* <span data-ttu-id="d3bcf-126">Использование `Database.ExecuteSqlCommand` для команд, не относящихся к запросам.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-126">Use the `Database.ExecuteSqlCommand` for non-query commands.</span></span>

<span data-ttu-id="d3bcf-127">Если вам необходимо выполнить запрос, который возвращает типы, не являющиеся сущностями, можно использовать ADO.NET с подключением к базе данных, предоставленным платформой EF.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-127">If you need to run a query that returns types that aren't entities, you can use ADO.NET with the database connection provided by EF.</span></span> <span data-ttu-id="d3bcf-128">Возвращаемые данные не отслеживаются контекстом базы данных, даже если вы используете этот метод для извлечения типов сущностей.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-128">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>

<span data-ttu-id="d3bcf-129">Как и всегда при выполнении команд SQL в веб-приложении, необходимо принимать меры предосторожности для защиты сайта от атак путем внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-129">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="d3bcf-130">Одним из способов защиты является применение параметризованных запросов, которые гарантируют, что строки, отправляемые веб-страницей, не могут быть интерпретированы как команды SQL.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-130">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="d3bcf-131">В рамках этого учебника вы будете использовать параметризованные запросы при интеграции вводимых пользователем данных в запрос.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-131">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

## <a name="call-a-query-to-return-entities"></a><span data-ttu-id="d3bcf-132">Вызов запроса для получения сущностей</span><span class="sxs-lookup"><span data-stu-id="d3bcf-132">Call a query to return entities</span></span>

<span data-ttu-id="d3bcf-133">Класс `DbSet<TEntity>` предоставляет метод, который можно использовать для выполнения запроса, возвращающего сущность типа `TEntity`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-133">The `DbSet<TEntity>` class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="d3bcf-134">Чтобы увидеть, как это работает, измените код в методе `Details` для контроллера Department.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-134">To see how this works you'll change the code in the `Details` method of the Department controller.</span></span>

<span data-ttu-id="d3bcf-135">В файле *DepartmentsController.cs* в методе `Details` замените код, извлекающий кафедру, вызовом метода `FromSql`, как показано ниже в выделенном коде:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-135">In *DepartmentsController.cs*, in the `Details` method, replace the code that retrieves a department with a `FromSql` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_RawSQL&highlight=8,9,10,13)]

<span data-ttu-id="d3bcf-136">Чтобы убедиться, что новый код работает правильно, выберите вкладку **Departments** (Кафедры) и щелкните **Details** (Сведения) для одной из кафедр.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-136">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span>

![Сведения о кафедре](advanced/_static/department-details.png)

## <a name="call-a-query-to-return-other-types"></a><span data-ttu-id="d3bcf-138">Вызов запроса для получения других типов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-138">Call a query to return other types</span></span>

<span data-ttu-id="d3bcf-139">Ранее вы создали таблицу статистики учащихся на странице сведений, в которой было показано число учащихся на каждую дату регистрации.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-139">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="d3bcf-140">Вы получали эти данные из набора сущностей Students (`_context.Students`) и использовали LINQ, чтобы спроецировать результаты в список объектов модели представления `EnrollmentDateGroup`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-140">You got the data from the Students entity set (`_context.Students`) and used LINQ to project the results into a list of `EnrollmentDateGroup` view model objects.</span></span> <span data-ttu-id="d3bcf-141">Предположим, что вы хотите написать код SQL вместо использования LINQ.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-141">Suppose you want to write the SQL itself rather than using LINQ.</span></span> <span data-ttu-id="d3bcf-142">Для этого вам необходимо выполнить SQL-запрос, который возвращает объекты, не являющиеся сущностями.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-142">To do that you need to run a SQL query that returns something other than entity objects.</span></span> <span data-ttu-id="d3bcf-143">В EF Core 1.0 одним из способов сделать это является написание кода ADO.NET и получение подключения к базе данных из EF.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-143">In EF Core 1.0, one way to do that is write ADO.NET code and get the database connection from EF.</span></span>

<span data-ttu-id="d3bcf-144">В файле *HomeController.cs* замените метод `About` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-144">In *HomeController.cs*, replace the `About` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseRawSQL&highlight=3-32)]

<span data-ttu-id="d3bcf-145">Добавьте инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-145">Add a using statement:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings2)]

<span data-ttu-id="d3bcf-146">Запустите приложение и перейдите на страницу About.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-146">Run the app and go to the About page.</span></span> <span data-ttu-id="d3bcf-147">На экран будут выведены те же данные, что и ранее.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-147">It displays the same data it did before.</span></span>

![Страница About](advanced/_static/about.png)

## <a name="call-an-update-query"></a><span data-ttu-id="d3bcf-149">Вызов запроса на обновление</span><span class="sxs-lookup"><span data-stu-id="d3bcf-149">Call an update query</span></span>

<span data-ttu-id="d3bcf-150">Предположим, что администраторам университета Suppose необходимо внести глобальные изменения в базу данных, например изменить число зачетных баллов для каждого курса.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-150">Suppose Contoso University administrators want to perform global changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="d3bcf-151">Поскольку в университете ведется множество курсов, будет неэффективно извлекать их в виде сущностей и изменять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-151">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="d3bcf-152">В этом разделе вы реализуете веб-страницу, на которой пользователь может задать множитель, который будет применен к числу зачетных баллов для каждого курса, после чего изменения будут внесены с помощью инструкции SQL UPDATE.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-152">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL UPDATE statement.</span></span> <span data-ttu-id="d3bcf-153">Веб-страница должна выглядеть так, как показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-153">The web page will look like the following illustration:</span></span>

![Страница обновления числа зачетных баллов для курсов](advanced/_static/update-credits.png)

<span data-ttu-id="d3bcf-155">В файле *CoursesContoller.cs* добавьте методы UpdateCourseCredits для HttpGet и HttpPost:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-155">In *CoursesContoller.cs*, add UpdateCourseCredits methods for HttpGet and HttpPost:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdateGet)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdatePost)]

<span data-ttu-id="d3bcf-156">Когда контроллер обрабатывает запрос HttpGet, в `ViewData["RowsAffected"]` ничего не возвращается, а в представлении отображается пустое текстовое поле и кнопка отправки, как показано на предыдущем рисунке.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-156">When the controller processes an HttpGet request, nothing is returned in `ViewData["RowsAffected"]`, and the view displays an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="d3bcf-157">При нажатии кнопки **Update** (Обновить) вызывается метод HttpPost, а множителю присваивается значение, введенное в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-157">When the **Update** button is clicked, the HttpPost method is called, and multiplier has the value entered in the text box.</span></span> <span data-ttu-id="d3bcf-158">После этого код выполняет SQL-запрос, который обновляет курсы и возвращает число затронутых строк в представление в `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-158">The code then executes the SQL that updates courses and returns the number of affected rows to the view in `ViewData`.</span></span> <span data-ttu-id="d3bcf-159">После того как в представление передано значение `RowsAffected`, оно отображает число обновленных строк.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-159">When the view gets a `RowsAffected` value, it displays the number of rows updated.</span></span>

<span data-ttu-id="d3bcf-160">В **обозревателе решений** щелкните правой кнопкой мыши папку *Views/Courses* и выберите **Добавить > Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-160">In **Solution Explorer**, right-click the *Views/Courses* folder, and then click **Add > New Item**.</span></span>

<span data-ttu-id="d3bcf-161">В диалоговом окне **Добавление нового элемента** щелкните элемент **ASP.NET Core** в разделе **Установленные** в области слева, выберите **Представление Razor** и присвойте новому представлению имя *UpdateCourseCredits.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-161">In the **Add New Item** dialog, click **ASP.NET Core** under **Installed** in the left pane, click **Razor View**, and name the new view *UpdateCourseCredits.cshtml*.</span></span>

<span data-ttu-id="d3bcf-162">В файле *Views/Courses/UpdateCourseCredits.cshtml* замените код шаблона следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-162">In *Views/Courses/UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-html[](intro/samples/cu/Views/Courses/UpdateCourseCredits.cshtml)]

<span data-ttu-id="d3bcf-163">Выполните метод `UpdateCourseCredits`, выбрав вкладку **Courses** (Курсы), а затем добавив "/UpdateCourseCredits" в конец URL-адреса в адресной строке браузера (например, `http://localhost:5813/Courses/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-163">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:5813/Courses/UpdateCourseCredits`).</span></span> <span data-ttu-id="d3bcf-164">Введите число в текстовое поле:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-164">Enter a number in the text box:</span></span>

![Страница обновления числа зачетных баллов для курсов](advanced/_static/update-credits.png)

<span data-ttu-id="d3bcf-166">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-166">Click **Update**.</span></span> <span data-ttu-id="d3bcf-167">Отобразится число обработанных строк:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-167">You see the number of rows affected:</span></span>

![Число затронутых строк на странице обновления числа зачетных баллов для курсов](advanced/_static/update-credits-rows-affected.png)

<span data-ttu-id="d3bcf-169">Нажмите кнопку **Back to List** (Вернуться к списку), чтобы просмотреть список курсов с измененным числом зачетных баллов.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-169">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="d3bcf-170">Обратите внимание, что в рабочем коде необходимо всегда проверять допустимость новых данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-170">Note that production code would ensure that updates always result in valid data.</span></span> <span data-ttu-id="d3bcf-171">В приведенном здесь упрощенном коде в результате применения множителя могут получиться значения больше 5.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-171">The simplified code shown here could multiply the number of credits enough to result in numbers greater than 5.</span></span> <span data-ttu-id="d3bcf-172">(Свойство `Credits` имеет атрибут `[Range(0, 5)]`.) Запрос на обновление будет выполнен, однако из-за недопустимых данных в других частях системы, в которых число зачетных баллов должно быть не больше 5, могут возникать неожиданные результаты.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-172">(The `Credits` property has a `[Range(0, 5)]` attribute.) The update query would work but the invalid data could cause unexpected results in other parts of the system that assume the number of credits is 5 or less.</span></span>

<span data-ttu-id="d3bcf-173">Дополнительные сведения о необработанных SQL-запросах см. в разделе [Необработанные SQL-запросы](/ef/core/querying/raw-sql).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-173">For more information about raw SQL queries, see [Raw SQL Queries](/ef/core/querying/raw-sql).</span></span>

## <a name="examine-sql-queries"></a><span data-ttu-id="d3bcf-174">Изучение SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-174">Examine SQL queries</span></span>

<span data-ttu-id="d3bcf-175">В некоторых случаях полезно иметь возможность просмотреть фактические SQL-запросы, отправляемые в базу данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-175">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="d3bcf-176">Платформа EF Core использует встроенные функции ASP.NET Core для автоматического ведения журналов, содержащих код SQL запросов и обновлений.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-176">Built-in logging functionality for ASP.NET Core is automatically used by EF Core to write logs that contain the SQL for queries and updates.</span></span> <span data-ttu-id="d3bcf-177">В этом разделе приводятся некоторые примеры ведения журналов кода SQL.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-177">In this section you'll see some examples of SQL logging.</span></span>

<span data-ttu-id="d3bcf-178">Откройте файл *StudentsController.cs* и установите в методе `Details` точку останова на инструкции `if (student == null)`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-178">Open *StudentsController.cs* and in the `Details` method set a breakpoint on the `if (student == null)` statement.</span></span>

<span data-ttu-id="d3bcf-179">Запустите приложение в режиме отладки и перейдите на страницу Details (Сведения) для учащегося.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-179">Run the app in debug mode, and go to the Details page for a student.</span></span>

<span data-ttu-id="d3bcf-180">Перейдите в **окно вывода**, в котором отображаются результаты отладки. В нем будет показан запрос:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-180">Go to the **Output** window showing debug output, and you see the query:</span></span>

```
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (56ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT TOP(2) [s].[ID], [s].[Discriminator], [s].[FirstName], [s].[LastName], [s].[EnrollmentDate]
FROM [Person] AS [s]
WHERE ([s].[Discriminator] = N'Student') AND ([s].[ID] = @__id_0)
ORDER BY [s].[ID]
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (122ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT [s.Enrollments].[EnrollmentID], [s.Enrollments].[CourseID], [s.Enrollments].[Grade], [s.Enrollments].[StudentID], [e.Course].[CourseID], [e.Course].[Credits], [e.Course].[DepartmentID], [e.Course].[Title]
FROM [Enrollment] AS [s.Enrollments]
INNER JOIN [Course] AS [e.Course] ON [s.Enrollments].[CourseID] = [e.Course].[CourseID]
INNER JOIN (
    SELECT TOP(1) [s0].[ID]
    FROM [Person] AS [s0]
    WHERE ([s0].[Discriminator] = N'Student') AND ([s0].[ID] = @__id_0)
    ORDER BY [s0].[ID]
) AS [t] ON [s.Enrollments].[StudentID] = [t].[ID]
ORDER BY [t].[ID]
```

<span data-ttu-id="d3bcf-181">Вы можете заметить удивительные результаты: код SQL выбирает до 2 строк (`TOP(2)`) из таблицы Person.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-181">You'll notice something here that might surprise you: the SQL selects up to 2 rows (`TOP(2)`) from the Person table.</span></span> <span data-ttu-id="d3bcf-182">Метод `SingleOrDefaultAsync` не разрешается в 1 строку на сервере.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-182">The `SingleOrDefaultAsync` method doesn't resolve to 1 row on the server.</span></span> <span data-ttu-id="d3bcf-183">Далее описывается, почему это происходит:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-183">Here's why:</span></span>

* <span data-ttu-id="d3bcf-184">Если запрос возвращает несколько строк, метод возвращает значение NULL.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-184">If the query would return multiple rows, the method returns null.</span></span>
* <span data-ttu-id="d3bcf-185">Чтобы определить, будет ли запрос возвращать несколько строк, платформа EF проверяет, возвращаются ли как минимум 2 строки.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-185">To determine whether the query would return multiple rows, EF has to check if it returns at least 2.</span></span>

<span data-ttu-id="d3bcf-186">Обратите внимание, что вам необязательно использовать режим отладки и доходить до точки останова, чтобы просмотреть содержимое журнала в **окне вывода**.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-186">Note that you don't have to use debug mode and stop at a breakpoint to get logging output in the **Output** window.</span></span> <span data-ttu-id="d3bcf-187">Это просто удобный способ остановить ведение журнала в тот момент, когда вам нужно просмотреть выходные данные.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-187">It's just a convenient way to stop the logging at the point you want to look at the output.</span></span> <span data-ttu-id="d3bcf-188">Если не сделать этого, ведение журнала продолжится и вам придется прокручивать окно до нужного места.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-188">If you don't do that, logging continues and you have to scroll back to find the parts you're interested in.</span></span>

## <a name="create-an-abstraction-layer"></a><span data-ttu-id="d3bcf-189">Создание уровня абстракции</span><span class="sxs-lookup"><span data-stu-id="d3bcf-189">Create an abstraction layer</span></span>

<span data-ttu-id="d3bcf-190">Многие разработчики пишут код, реализующий шаблоны репозитория и единиц работы, в качестве оболочки для кода, работающего с платформой Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-190">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="d3bcf-191">Эти шаблоны позволяют создать уровень абстракции между уровнями доступа к данным и бизнес-логики приложения.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-191">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="d3bcf-192">Реализация таких шаблонов позволяет изолировать приложение от изменений в хранилище данных и упрощает автоматическое модульное тестирование или разработку на основе тестирования.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-192">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="d3bcf-193">Тем не менее написание дополнительного кода для реализации этих шаблонов не всегда подходит для приложений, которые используют платформу EF. Этому есть несколько причин:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-193">However, writing additional code to implement these patterns isn't always the best choice for applications that use EF, for several reasons:</span></span>

* <span data-ttu-id="d3bcf-194">Класс контекста EF сам по себе изолирует код от кода хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-194">The EF context class itself insulates your code from data-store-specific code.</span></span>

* <span data-ttu-id="d3bcf-195">Класс контекста EF может выступать в качестве класса единиц работы для обновления базы данных, которые выполняются с помощью EF.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-195">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>

* <span data-ttu-id="d3bcf-196">Платформа EF предусматривает функции для реализации разработки на основе тестирования, не требующие написания кода репозитория.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-196">EF includes features for implementing TDD without writing repository code.</span></span>

<span data-ttu-id="d3bcf-197">Дополнительные сведения о реализации шаблонов репозитория и единиц работы см. в [версии этой серии учебников для платформы Entity Framework 5](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-197">For information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span></span>

<span data-ttu-id="d3bcf-198">Платформа Entity Framework Core реализует выполняющийся в памяти поставщик базы данных, который может использоваться для тестирования.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-198">Entity Framework Core implements an in-memory database provider that can be used for testing.</span></span> <span data-ttu-id="d3bcf-199">Дополнительные сведения см. в разделе [Тестирование с помощью InMemory](/ef/core/miscellaneous/testing/in-memory).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-199">For more information, see [Test with InMemory](/ef/core/miscellaneous/testing/in-memory).</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="d3bcf-200">Автоматическое обнаружение изменений</span><span class="sxs-lookup"><span data-stu-id="d3bcf-200">Automatic change detection</span></span>

<span data-ttu-id="d3bcf-201">Платформа Entity Framework определяет, как была изменена сущность (и, соответственно, какие обновления требуется отправить в базу данных), сравнивая текущие значения сущности с исходными.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-201">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="d3bcf-202">Исходные значения сохраняются при запросе или присоединении сущности.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-202">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="d3bcf-203">Ниже перечислены некоторые из методов, которые приводят к автоматическому обнаружению изменений:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-203">Some of the methods that cause automatic change detection are the following:</span></span>

* <span data-ttu-id="d3bcf-204">DbContext.SaveChanges</span><span class="sxs-lookup"><span data-stu-id="d3bcf-204">DbContext.SaveChanges</span></span>

* <span data-ttu-id="d3bcf-205">DbContext.Entry</span><span class="sxs-lookup"><span data-stu-id="d3bcf-205">DbContext.Entry</span></span>

* <span data-ttu-id="d3bcf-206">ChangeTracker.Entries</span><span class="sxs-lookup"><span data-stu-id="d3bcf-206">ChangeTracker.Entries</span></span>

<span data-ttu-id="d3bcf-207">Если вы отслеживаете большое число сущностей и многократно вызываете один из этих методов в цикле, вы сможете добиться заметного повышения производительности, отключив автоматическое обнаружение изменений с помощью свойства `ChangeTracker.AutoDetectChangesEnabled`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-207">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the `ChangeTracker.AutoDetectChangesEnabled` property.</span></span> <span data-ttu-id="d3bcf-208">Пример:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-208">For example:</span></span>

```csharp
_context.ChangeTracker.AutoDetectChangesEnabled = false;
```

## <a name="ef-core-source-code-and-development-plans"></a><span data-ttu-id="d3bcf-209">Исходный код EF Core и планы разработки</span><span class="sxs-lookup"><span data-stu-id="d3bcf-209">EF Core source code and development plans</span></span>

<span data-ttu-id="d3bcf-210">Источник Entity Framework Core расположен на странице [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-210">The Entity Framework Core source is at [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span></span> <span data-ttu-id="d3bcf-211">Репозиторий EF Core содержит ночные сборки, результаты отслеживания проблем, спецификации функций, протоколы совещаний по проекту, а также [стратегию дальнейшей разработки](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-211">The EF Core repository contains nightly builds, issue tracking, feature specs, design meeting notes, and [the roadmap for future development](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap).</span></span> <span data-ttu-id="d3bcf-212">Вы также можете сообщать об ошибках, находить сведения об обнаруженных проблемах и участвовать в работе сообщества.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-212">You can file or find bugs, and contribute.</span></span>

<span data-ttu-id="d3bcf-213">Несмотря на открытый исходный код, платформа Entity Framework Core полностью поддерживается как продукт корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-213">Although the source code is open, Entity Framework Core is fully supported as a Microsoft product.</span></span> <span data-ttu-id="d3bcf-214">Команда Microsoft Entity Framework контролирует предложения участников, принимает их и тестирует любые изменения кода, чтобы обеспечить максимальное качество каждого выпуска.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-214">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="reverse-engineer-from-existing-database"></a><span data-ttu-id="d3bcf-215">Реконструирование из существующей базы данных</span><span class="sxs-lookup"><span data-stu-id="d3bcf-215">Reverse engineer from existing database</span></span>

<span data-ttu-id="d3bcf-216">Чтобы реконструировать модель данных, включая классы сущностей, из существующей базы данных, используйте команду [scaffold-dbcontext](/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-216">To reverse engineer a data model including entity classes from an existing database, use the [scaffold-dbcontext](/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext) command.</span></span> <span data-ttu-id="d3bcf-217">Ознакомьтесь с [учебником по началу работы](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-217">See the [getting-started tutorial](/ef/core/get-started/aspnetcore/existing-db).</span></span>

<a id="dynamic-linq"></a>

## <a name="use-dynamic-linq-to-simplify-code"></a><span data-ttu-id="d3bcf-218">Использование динамических запросов LINQ для упрощения кода</span><span class="sxs-lookup"><span data-stu-id="d3bcf-218">Use dynamic LINQ to simplify code</span></span>

<span data-ttu-id="d3bcf-219">В [третьем учебнике этой серии](sort-filter-page.md) демонстрируется написание кода LINQ с жестко запрограммированными именами столбцов в инструкции `switch`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-219">The [third tutorial in this series](sort-filter-page.md) shows how to write LINQ code by hard-coding column names in a `switch` statement.</span></span> <span data-ttu-id="d3bcf-220">При наличии всего двух столбцов такой подход эффективен, однако если столбцов много, код может стать слишком громоздким.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-220">With two columns to choose from, this works fine, but if you have many columns the code could get verbose.</span></span> <span data-ttu-id="d3bcf-221">Чтобы устранить эту проблему, можно использовать метод `EF.Property` для указания имени свойства в виде строки.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-221">To solve that problem, you can use the `EF.Property` method to specify the name of the property as a string.</span></span> <span data-ttu-id="d3bcf-222">Чтобы попробовать этот подход, замените метод `Index` в `StudentsController` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-222">To try out this approach, replace the `Index` method in the `StudentsController` with the following code.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DynamicLinq)]

## <a name="acknowledgments"></a><span data-ttu-id="d3bcf-223">Благодарности</span><span class="sxs-lookup"><span data-stu-id="d3bcf-223">Acknowledgments</span></span>

<span data-ttu-id="d3bcf-224">Этот учебник написан Томом Дайкстра (Tom Dykstra) и Риком Андерсоном (Rick Anderson) (twitter @RickAndMSFT).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-224">Tom Dykstra and Rick Anderson (twitter @RickAndMSFT) wrote this tutorial.</span></span> <span data-ttu-id="d3bcf-225">Помощь в проверке кода для учебника и отладке проблем, возникавших при его написании, оказывали Роуэн Миллер (Rowan Miller), Диего Вега (Diego Vega) и другие участники команды Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-225">Rowan Miller, Diego Vega, and other members of the Entity Framework team assisted with code reviews and helped debug issues that arose while we were writing code for the tutorials.</span></span> <span data-ttu-id="d3bcf-226">Джон Парент (John Parente) и Пол Голдмен (Paul Goldman) обновили это руководство для версии ASP.NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-226">John Parente and Paul Goldman worked on updating the tutorial for ASP.NET Core 2.2.</span></span>

<a id="common-errors"></a>
## <a name="troubleshoot-common-errors"></a><span data-ttu-id="d3bcf-227">Устранение неполадок при распространенных ошибках</span><span class="sxs-lookup"><span data-stu-id="d3bcf-227">Troubleshoot common errors</span></span>

### <a name="contosouniversitydll-used-by-another-process"></a><span data-ttu-id="d3bcf-228">Библиотека ContosoUniversity.dll используется другим процессом</span><span class="sxs-lookup"><span data-stu-id="d3bcf-228">ContosoUniversity.dll used by another process</span></span>

<span data-ttu-id="d3bcf-229">Сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-229">Error message:</span></span>

> <span data-ttu-id="d3bcf-230">Не удается открыть файл "...bin\Debug\netcoreapp1.0\ContosoUniversity.dll" для записи — "Процесс не может получить доступ к файлу "...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll", так как этот файл занят другим процессом.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-230">Cannot open '...bin\Debug\netcoreapp1.0\ContosoUniversity.dll' for writing -- 'The process cannot access the file '...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll' because it is being used by another process.</span></span>

<span data-ttu-id="d3bcf-231">Решение:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-231">Solution:</span></span>

<span data-ttu-id="d3bcf-232">Остановите сайт в IIS Express.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-232">Stop the site in IIS Express.</span></span> <span data-ttu-id="d3bcf-233">Найдите значок IIS Express в панели задач Windows, щелкните его правой кнопкой мыши, выберите сайт университета Contoso и затем выберите **Остановить сайт**.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-233">Go to the Windows System Tray, find IIS Express and right-click its icon, select the Contoso University site, and then click **Stop Site**.</span></span>

### <a name="migration-scaffolded-with-no-code-in-up-and-down-methods"></a><span data-ttu-id="d3bcf-234">Формирование шаблонов миграции без кода в методах Up и Down</span><span class="sxs-lookup"><span data-stu-id="d3bcf-234">Migration scaffolded with no code in Up and Down methods</span></span>

<span data-ttu-id="d3bcf-235">Возможная причина:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-235">Possible cause:</span></span>

<span data-ttu-id="d3bcf-236">Команды интерфейса командной строки EF не выполняют автоматическое закрытие и сохранение файлов кода.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-236">The EF CLI commands don't automatically close and save code files.</span></span> <span data-ttu-id="d3bcf-237">Если при выполнении команды `migrations add` у вас есть несохраненные изменения, платформа EF не сможет обнаружить их.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-237">If you have unsaved changes when you run the `migrations add` command, EF won't find your changes.</span></span>

<span data-ttu-id="d3bcf-238">Решение:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-238">Solution:</span></span>

<span data-ttu-id="d3bcf-239">Выполните команду `migrations remove`, сохраните изменения в коде и повторно выполните команду `migrations add`.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-239">Run the `migrations remove` command, save your code changes and rerun the `migrations add` command.</span></span>

### <a name="errors-while-running-database-update"></a><span data-ttu-id="d3bcf-240">Ошибки во время обновления базы данных</span><span class="sxs-lookup"><span data-stu-id="d3bcf-240">Errors while running database update</span></span>

<span data-ttu-id="d3bcf-241">При изменении схемы в базе, содержащей существующие данные, возможны другие ошибки.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-241">It's possible to get other errors when making schema changes in a database that has existing data.</span></span> <span data-ttu-id="d3bcf-242">Если вы получаете ошибки миграции, которые не удается устранить, измените имя базы данных в строке подключения или удалите базу данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-242">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="d3bcf-243">В новой базе не будет данных, которые требуется перенести, в результате чего команда обновления базы данных с большей долей вероятности завершится без ошибок.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-243">With a new database, there's no data to migrate, and the update-database command is much more likely to complete without errors.</span></span>

<span data-ttu-id="d3bcf-244">Проще всего в этом случае переименовать базу данных в файле *appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-244">The simplest approach is to rename the database in *appsettings.json*.</span></span> <span data-ttu-id="d3bcf-245">В следующий раз при выполнении команды `database update` будет создана новая база данных.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-245">The next time you run `database update`, a new database will be created.</span></span>

<span data-ttu-id="d3bcf-246">Чтобы удалить базу данных в средстве SSOX, щелкните ее правой кнопкой мыши, выберите **Удалить**, а затем в диалоговом окне **Удаление базы данных** выберите **Закрыть существующие соединения** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-246">To delete a database in SSOX, right-click the database, click **Delete**, and then in the **Delete Database** dialog box select **Close existing connections** and click **OK**.</span></span>

<span data-ttu-id="d3bcf-247">Чтобы удалить базу данных с помощью интерфейса командной строки, выполните команду `database drop`:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-247">To delete a database by using the CLI, run the `database drop` CLI command:</span></span>

```console
dotnet ef database drop
```

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="d3bcf-248">Ошибка при обнаружении экземпляра SQL Server</span><span class="sxs-lookup"><span data-stu-id="d3bcf-248">Error locating SQL Server instance</span></span>

<span data-ttu-id="d3bcf-249">Сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-249">Error Message:</span></span>

> <span data-ttu-id="d3bcf-250">При установлении подключения к SQL Server произошла ошибка сети или ошибка экземпляра.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-250">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="d3bcf-251">Сервер не найден или недоступен.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-251">The server was not found or was not accessible.</span></span> <span data-ttu-id="d3bcf-252">Проверьте правильность имени экземпляра и настройку сервера SQL Server для удаленных подключений.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-252">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="d3bcf-253">(поставщик: сетевые интерфейсы SQL, ошибка: 26 — ошибка при обнаружении указанного сервера или экземпляра)</span><span class="sxs-lookup"><span data-stu-id="d3bcf-253">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="d3bcf-254">Решение:</span><span class="sxs-lookup"><span data-stu-id="d3bcf-254">Solution:</span></span>

<span data-ttu-id="d3bcf-255">Проверьте строку подключения.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-255">Check the connection string.</span></span> <span data-ttu-id="d3bcf-256">Если вы вручную удалили файл базы данных, измените имя базы данных в строке подключения, чтобы начать работу с новой базой.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-256">If you have manually deleted the database file, change the name of the database in the construction string to start over with a new database.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="d3bcf-257">Получение кода</span><span class="sxs-lookup"><span data-stu-id="d3bcf-257">Get the code</span></span>

[<span data-ttu-id="d3bcf-258">Скачайте или ознакомьтесь с готовым приложением.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-258">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="additional-resources"></a><span data-ttu-id="d3bcf-259">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3bcf-259">Additional resources</span></span>

<span data-ttu-id="d3bcf-260">Дополнительные сведения о EF Core см. в [документации по платформе Entity Framework Core](/ef/core).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-260">For more information about EF Core, see the [Entity Framework Core documentation](/ef/core).</span></span> <span data-ttu-id="d3bcf-261">Можно также прочесть книгу [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action).</span><span class="sxs-lookup"><span data-stu-id="d3bcf-261">A book is also available: [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action).</span></span>

<span data-ttu-id="d3bcf-262">Сведения о развертывании веб-приложения см. в <xref:host-and-deploy/index>.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-262">For information on how to deploy a web app, see <xref:host-and-deploy/index>.</span></span>

<span data-ttu-id="d3bcf-263">Дополнительные сведения по другим вопросам, связанным с использованием ASP.NET Core MVC, включая способы проверки подлинности и авторизации, см. в <xref:index>.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-263">For information about other topics related to ASP.NET Core MVC, such as authentication and authorization, see <xref:index>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3bcf-264">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="d3bcf-264">Next steps</span></span>

<span data-ttu-id="d3bcf-265">В этом учебнике рассмотрены следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-265">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d3bcf-266">Выполнение прямых SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-266">Performed raw SQL queries</span></span>
> * <span data-ttu-id="d3bcf-267">Вызов запроса для получения сущностей</span><span class="sxs-lookup"><span data-stu-id="d3bcf-267">Called a query to return entities</span></span>
> * <span data-ttu-id="d3bcf-268">Вызов запроса для получения других типов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-268">Called a query to return other types</span></span>
> * <span data-ttu-id="d3bcf-269">Вызов запроса на обновление</span><span class="sxs-lookup"><span data-stu-id="d3bcf-269">Called an update query</span></span>
> * <span data-ttu-id="d3bcf-270">Изучение SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="d3bcf-270">Examined SQL queries</span></span>
> * <span data-ttu-id="d3bcf-271">Создание уровня абстракции</span><span class="sxs-lookup"><span data-stu-id="d3bcf-271">Created an abstraction layer</span></span>
> * <span data-ttu-id="d3bcf-272">Сведения об автоматическом обнаружении изменений</span><span class="sxs-lookup"><span data-stu-id="d3bcf-272">Learned about Automatic change detection</span></span>
> * <span data-ttu-id="d3bcf-273">Сведения об исходном коде EF Core и планах разработки</span><span class="sxs-lookup"><span data-stu-id="d3bcf-273">Learned about EF Core source code and development plans</span></span>
> * <span data-ttu-id="d3bcf-274">Сведения об использовании динамических запросов LINQ для упрощения кода</span><span class="sxs-lookup"><span data-stu-id="d3bcf-274">Learned how to use dynamic LINQ to simplify code</span></span>

<span data-ttu-id="d3bcf-275">На этом серия учебников, посвященных использованию платформы Entity Framework Core в приложении ASP.NET Core MVC, завершена.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-275">This completes this series of tutorials on using the Entity Framework Core in an ASP.NET Core MVC application.</span></span> <span data-ttu-id="d3bcf-276">Если вам нужны сведения об использовании EF 6 с ASP.NET Core, изучите следующую статью.</span><span class="sxs-lookup"><span data-stu-id="d3bcf-276">If you want to learn about using EF 6 with ASP.NET Core, see the next article.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d3bcf-277">EF 6 с ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d3bcf-277">EF 6 with ASP.NET Core</span></span>](../entity-framework-6.md)
