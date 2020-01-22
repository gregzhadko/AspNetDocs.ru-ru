---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: e01953dcfb2abf2db53a8aa869aa75b40485daca
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519093"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="71323-102">Доступ к данным модели из контроллера</span><span class="sxs-lookup"><span data-stu-id="71323-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="71323-103">по [Рик Андерсон (]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="71323-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="71323-104">В этом разделе вы создадите новый класс `MoviesController` и запишете код, который извлекает данные фильмов и отображает их в браузере с помощью шаблона представления.</span><span class="sxs-lookup"><span data-stu-id="71323-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="71323-105">**Создайте приложение,** прежде чем переходить к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="71323-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="71323-106">Если вы не создаете приложение, вы получите сообщение об ошибке при добавлении контроллера.</span><span class="sxs-lookup"><span data-stu-id="71323-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="71323-107">В обозреватель решений щелкните правой кнопкой мыши папку *Controllers* и выберите команду **Добавить**, а затем — **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="71323-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="71323-108">В диалоговом окне **Добавление шаблона** выберите **контроллер MVC 5 с представлениями с помощью Entity Framework**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="71323-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="71323-109">Выберите **фильм (MvcMovie. Models)** для класса Model.</span><span class="sxs-lookup"><span data-stu-id="71323-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="71323-110">Выберите **мовиедбконтекст (MvcMovie. Models)** для класса контекста данных.</span><span class="sxs-lookup"><span data-stu-id="71323-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="71323-111">В качестве имени контроллера введите **MoviesController**.</span><span class="sxs-lookup"><span data-stu-id="71323-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="71323-112">На рисунке ниже показано диалоговое окно завершено.</span><span class="sxs-lookup"><span data-stu-id="71323-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="71323-113">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="71323-113">Click **Add**.</span></span> <span data-ttu-id="71323-114">(Если появляется сообщение об ошибке, то, возможно, приложение не было собрано до начала добавления контроллера.) Visual Studio создает следующие файлы и папки:</span><span class="sxs-lookup"><span data-stu-id="71323-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="71323-115">Файл *MoviesController.CS* в папке *Controllers* .</span><span class="sxs-lookup"><span data-stu-id="71323-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="71323-116">Папка *виевс\мовиес* .</span><span class="sxs-lookup"><span data-stu-id="71323-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="71323-117">В новой папке *Виевс\мовиес* *создаются. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml*и *index. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="71323-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="71323-118">Visual Studio автоматически создавала методы и представления действия [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (создание, чтение, обновление и удаление) для вас (автоматическое создание методов и ПРЕДСТАВЛЕНИЙ действий CRUD называется формированием шаблонов).</span><span class="sxs-lookup"><span data-stu-id="71323-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="71323-119">Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.</span><span class="sxs-lookup"><span data-stu-id="71323-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="71323-120">Запустите приложение и щелкните ссылку на **ролик MVC** (или перейдите к контроллеру `Movies`, добавив */Movies* к URL-адресу в адресной строке браузера).</span><span class="sxs-lookup"><span data-stu-id="71323-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="71323-121">Поскольку приложение полагается на маршрутизацию по умолчанию (определенную в файле *приложения\_старт\раутеконфиг.КС* ), запрос браузера `http://localhost:xxxxx/Movies` перенаправляется в метод действия `Index` по умолчанию контроллера `Movies`.</span><span class="sxs-lookup"><span data-stu-id="71323-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="71323-122">Иными словами, `http://localhost:xxxxx/Movies` запроса браузера фактически аналогичен `http://localhost:xxxxx/Movies/Index`запроса браузера.</span><span class="sxs-lookup"><span data-stu-id="71323-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="71323-123">Результатом является пустой список фильмов, так как вы еще не добавили их.</span><span class="sxs-lookup"><span data-stu-id="71323-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="71323-124">Создание фильма</span><span class="sxs-lookup"><span data-stu-id="71323-124">Creating a Movie</span></span>

<span data-ttu-id="71323-125">Щелкните ссылку **Create New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="71323-125">Select the **Create New** link.</span></span> <span data-ttu-id="71323-126">Введите некоторые сведения о фильме и нажмите кнопку **создать** .</span><span class="sxs-lookup"><span data-stu-id="71323-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="71323-127">Возможно, вы не сможете вводить десятичные или запятые в поле Price.</span><span class="sxs-lookup"><span data-stu-id="71323-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="71323-128">для поддержки проверки jQuery для национальных стандартов, отличных от английского, которые используют запятую (&quot;,&quot;) для десятичной запятой и форматы даты, отличные от US-English, необходимо включить *глобализацию. js* и определенные *языки и региональные параметры/глобализации. js* (из [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) и JavaScript для использования `Globalize.parseFloat`.</span><span class="sxs-lookup"><span data-stu-id="71323-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="71323-129">Я покажу, как это сделать в следующем руководстве.</span><span class="sxs-lookup"><span data-stu-id="71323-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="71323-130">А пока вводите целые числа, такие как 10.</span><span class="sxs-lookup"><span data-stu-id="71323-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="71323-131">Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных.</span><span class="sxs-lookup"><span data-stu-id="71323-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="71323-132">Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.</span><span class="sxs-lookup"><span data-stu-id="71323-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="71323-133">Создайте еще несколько записей фильмов.</span><span class="sxs-lookup"><span data-stu-id="71323-133">Create a couple more movie entries.</span></span> <span data-ttu-id="71323-134">Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.</span><span class="sxs-lookup"><span data-stu-id="71323-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="71323-135">Проверка созданного кода</span><span class="sxs-lookup"><span data-stu-id="71323-135">Examining the Generated Code</span></span>

<span data-ttu-id="71323-136">Откройте файл *контроллерс\мовиесконтроллер.КС* и изучите созданный метод `Index`.</span><span class="sxs-lookup"><span data-stu-id="71323-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="71323-137">Ниже показана часть контроллера фильмов с методом `Index`.</span><span class="sxs-lookup"><span data-stu-id="71323-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="71323-138">Запрос к контроллеру `Movies` возвращает все записи в таблице `Movies`, а затем передает результаты в представление `Index`.</span><span class="sxs-lookup"><span data-stu-id="71323-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="71323-139">Следующая строка из класса `MoviesController` создает экземпляр контекста базы данных Movie, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="71323-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="71323-140">Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.</span><span class="sxs-lookup"><span data-stu-id="71323-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="71323-141">Строго типизированные модели и ключевое слово @model</span><span class="sxs-lookup"><span data-stu-id="71323-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="71323-142">Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью объекта `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="71323-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="71323-143">`ViewBag` — это динамический объект, предоставляющий удобный способ для передачи сведений в представление.</span><span class="sxs-lookup"><span data-stu-id="71323-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="71323-144">MVC также предоставляет возможность передачи *строго* типизированных объектов в шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="71323-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="71323-145">Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71323-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="71323-146">Механизм формирования шаблонов в Visual Studio использовал такой подход (то есть передает *строго* типизированную модель) с классом `MoviesController` и шаблонами представления при создании методов и представлений.</span><span class="sxs-lookup"><span data-stu-id="71323-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="71323-147">В файле *контроллерс\мовиесконтроллер.КС* изучите созданный метод `Details`.</span><span class="sxs-lookup"><span data-stu-id="71323-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="71323-148">Ниже показан метод `Details`.</span><span class="sxs-lookup"><span data-stu-id="71323-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="71323-149">Параметр `id` обычно передается как данные маршрута, например `http://localhost:1234/movies/details/1` установит контроллер в качестве контроллера ролика, действие для `details`, а `id` — 1.</span><span class="sxs-lookup"><span data-stu-id="71323-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="71323-150">Идентификатор можно также передать в строку запроса следующим образом:</span><span class="sxs-lookup"><span data-stu-id="71323-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="71323-151">При обнаружении `Movie` экземпляр модели `Movie` передается в представление `Details`.</span><span class="sxs-lookup"><span data-stu-id="71323-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="71323-152">Изучите содержимое файла *виевс\мовиес\детаилс.кштмл* :</span><span class="sxs-lookup"><span data-stu-id="71323-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="71323-153">Включив инструкцию `@model` в верхней части файла шаблона представления, можно указать тип объекта, который предполагается отобразить в представлении.</span><span class="sxs-lookup"><span data-stu-id="71323-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="71323-154">При создании контроллера movie Visual Studio автоматически включает следующий оператор `@model` в начало файла *Details.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="71323-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="71323-155">Эта директива `@model` обеспечивает доступ к фильму, который контроллер передал в представление с использованием строго типизированного объекта `Model`.</span><span class="sxs-lookup"><span data-stu-id="71323-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="71323-156">Например, в шаблоне *Details. cshtml* код передает каждое поле movie в `DisplayNameFor` и [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) вспомогательные методы HTML с помощью строго типизированного объекта `Model`.</span><span class="sxs-lookup"><span data-stu-id="71323-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="71323-157">Методы `Create` и `Edit` и шаблоны представлений также передают объект модели фильма.</span><span class="sxs-lookup"><span data-stu-id="71323-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="71323-158">Изучите шаблон представления *index. cshtml* и метод `Index` в файле *MoviesController.CS* .</span><span class="sxs-lookup"><span data-stu-id="71323-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="71323-159">Обратите внимание, что код создает объект [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) при вызове вспомогательного метода `View` в методе `Index` действия.</span><span class="sxs-lookup"><span data-stu-id="71323-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="71323-160">Затем код передает этот список `Movies` из метода действия `Index` в представление:</span><span class="sxs-lookup"><span data-stu-id="71323-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="71323-161">При создании контроллера фильмов Visual Studio автоматически включил в начало файла *index. cshtml* следующую инструкцию `@model`:</span><span class="sxs-lookup"><span data-stu-id="71323-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="71323-162">Эта директива `@model` позволяет получить доступ к списку фильмов, переданных контроллером в представление, используя строго типизированный объект `Model`.</span><span class="sxs-lookup"><span data-stu-id="71323-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="71323-163">Например, в шаблоне *index. cshtml* код проходит через фильмы, выполняя инструкцию `foreach` для строго типизированного объекта `Model`:</span><span class="sxs-lookup"><span data-stu-id="71323-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="71323-164">Так как объект `Model` является строго типизированным (в виде объекта `IEnumerable<Movie>`), каждый объект `item` в цикле вводится как `Movie`.</span><span class="sxs-lookup"><span data-stu-id="71323-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="71323-165">Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.</span><span class="sxs-lookup"><span data-stu-id="71323-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![моделинтеллисенсе](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="71323-167">Работа с SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="71323-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="71323-168">Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на базу данных `Movies`, которая еще не существовала, поэтому Code First автоматически создавала базу данных.</span><span class="sxs-lookup"><span data-stu-id="71323-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="71323-169">Чтобы убедиться, что он создан, найдите в папке *приложение\_данные* .</span><span class="sxs-lookup"><span data-stu-id="71323-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="71323-170">Если файл *movies. mdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " *приложение\_данные* ".</span><span class="sxs-lookup"><span data-stu-id="71323-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="71323-171">Дважды щелкните *movies. mdf* , чтобы открыть **Обозреватель сервера**, а затем разверните папку **таблицы** , чтобы просмотреть таблицу фильмов.</span><span class="sxs-lookup"><span data-stu-id="71323-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="71323-172">Обратите внимание на значок ключа рядом с ИДЕНТИФИКАТОРом.</span><span class="sxs-lookup"><span data-stu-id="71323-172">Note the key icon next to ID.</span></span> <span data-ttu-id="71323-173">По умолчанию EF сделает свойство с именем ID первичным ключом.</span><span class="sxs-lookup"><span data-stu-id="71323-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="71323-174">Дополнительные сведения о EF и MVC см. в разделе о отличном руководстве Tom Dykstra) по [MVC и EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="71323-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="71323-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="71323-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="71323-176">Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Показать данные таблицы** , чтобы просмотреть созданные данные.</span><span class="sxs-lookup"><span data-stu-id="71323-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="71323-177">Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Open Table Definition (Открыть определение таблицы** ), чтобы увидеть структуру таблицы, которая Entity Framework Code First создана.</span><span class="sxs-lookup"><span data-stu-id="71323-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="71323-178">Обратите внимание, что схема `Movies` таблицы сопоставляется с созданным ранее классом `Movie`.</span><span class="sxs-lookup"><span data-stu-id="71323-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="71323-179">Entity Framework Code First автоматически создали эту схему на основе класса `Movie`.</span><span class="sxs-lookup"><span data-stu-id="71323-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="71323-180">По завершении закройте подключение, щелкнув правой кнопкой мыши *мовиедбконтекст* и выбрав **закрыть подключение**.</span><span class="sxs-lookup"><span data-stu-id="71323-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="71323-181">(Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).</span><span class="sxs-lookup"><span data-stu-id="71323-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="71323-182">Теперь у вас есть база данных и страницы для отображения, редактирования, обновления и удаления данных.</span><span class="sxs-lookup"><span data-stu-id="71323-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="71323-183">В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим метод `SearchIndex` и представление `SearchIndex`, которое позволяет выполнять поиск фильмов в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="71323-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="71323-184">Дополнительные сведения об использовании Entity Framework с MVC см. в разделе [Создание модели данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="71323-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="71323-185">[Назад](creating-a-connection-string.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="71323-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
