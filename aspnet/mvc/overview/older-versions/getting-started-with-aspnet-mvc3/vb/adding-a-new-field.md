---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: Добавление нового поля в модель Movie и таблицу базы данных (Visual Basic) | Документация Майкрософт
author: Rick-Anderson
description: Этом учебнике описываются основы создания MVC веб-приложения ASP.NET с помощью Microsoft Visual Web Developer 2010 Express пакетом обновления 1, который является...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 8fb0fb5c1db24f1961bba08f7b1c2182caca39ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063541"
---
<a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a><span data-ttu-id="3be13-103">Добавление нового поля в модель Movie и таблицу базы данных (VB)</span><span class="sxs-lookup"><span data-stu-id="3be13-103">Adding a New Field to the Movie Model and Database Table (VB)</span></span>
====================
<span data-ttu-id="3be13-104">по [Рик Андерсон]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="3be13-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="3be13-105">Этом учебнике описываются основы создания MVC веб-приложения ASP.NET с помощью Microsoft Visual Web Developer 2010 Express пакетом обновления 1, которой является бесплатной версии Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3be13-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3be13-106">Перед началом работы убедитесь, что вы установили необходимые компоненты, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="3be13-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3be13-107">Все из них можно установить, щелкнув следующую ссылку: [Установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="3be13-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3be13-108">Кроме того можно установить по отдельности необходимых компонентов, с помощью следующих ссылок:</span><span class="sxs-lookup"><span data-stu-id="3be13-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3be13-109">Необходимые компоненты для Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="3be13-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3be13-110">Обновление средств ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="3be13-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3be13-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(среды выполнения и средства поддержки)</span><span class="sxs-lookup"><span data-stu-id="3be13-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3be13-112">Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Необходимые компоненты для Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="3be13-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3be13-113">Проект Visual Web Developer с VB.NET исходный код доступен на следующей странице в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="3be13-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="3be13-114">[Загрузить версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="3be13-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3be13-115">Если вы предпочитаете C#, переключитесь в [C# версии](../cs/adding-a-new-field.md) работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="3be13-115">If you prefer C#, switch to the [C# version](../cs/adding-a-new-field.md) of this tutorial.</span></span>


<span data-ttu-id="3be13-116">В этом разделе будет внести некоторые изменения в классы моделей и узнайте, как обновить схему базы данных в соответствии с изменениями модели.</span><span class="sxs-lookup"><span data-stu-id="3be13-116">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="3be13-117">Добавление свойства Rating в модель Movie</span><span class="sxs-lookup"><span data-stu-id="3be13-117">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="3be13-118">Начните с добавления нового `Rating` к существующему полю `Movie` класса.</span><span class="sxs-lookup"><span data-stu-id="3be13-118">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="3be13-119">Откройте *Movie.cs* файл и добавьте `Rating` свойство следующего вида:</span><span class="sxs-lookup"><span data-stu-id="3be13-119">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

<span data-ttu-id="3be13-120">Полный `Movie` класса сейчас выглядит аналогично следующему коду:</span><span class="sxs-lookup"><span data-stu-id="3be13-120">The complete `Movie` class now looks like the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

<span data-ttu-id="3be13-121">Перекомпилировать приложение с помощью **Отладка** &gt; **построения фильма** команды меню.</span><span class="sxs-lookup"><span data-stu-id="3be13-121">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="3be13-122">Теперь, когда вы обновили `Model` класса, необходимо также обновить *\Views\Movies\Index.vbhtml* и *\Views\Movies\Create.vbhtml* просмотра шаблонов для поддержки новых `Rating`свойство.</span><span class="sxs-lookup"><span data-stu-id="3be13-122">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.vbhtml* and *\Views\Movies\Create.vbhtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="3be13-123">Откройте<em>\Views\Movies\Index.vbhtml</em> файл и добавьте `<th>Rating</th>` сразу после заголовка столбца <strong>цена</strong> столбца.</span><span class="sxs-lookup"><span data-stu-id="3be13-123">Open the<em>\Views\Movies\Index.vbhtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="3be13-124">Затем добавьте `<td>` столбца в конце шаблона для отображения `@item.Rating` значение.</span><span class="sxs-lookup"><span data-stu-id="3be13-124">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="3be13-125">Ниже приведен какие обновленный <em>Index.vbhtml</em> Просмотр шаблона выглядит как:</span><span class="sxs-lookup"><span data-stu-id="3be13-125">Below is what the updated <em>Index.vbhtml</em> view template looks like:</span></span>

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

<span data-ttu-id="3be13-126">Затем откройте *\Views\Movies\Create.vbhtml* файл и добавьте следующую разметку в конце формы.</span><span class="sxs-lookup"><span data-stu-id="3be13-126">Next, open the *\Views\Movies\Create.vbhtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="3be13-127">Это отрисовывает текстовое поле, можно указать оценку, если создается новый фильм.</span><span class="sxs-lookup"><span data-stu-id="3be13-127">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="3be13-128">Управление модели и различия в схемах базы данных</span><span class="sxs-lookup"><span data-stu-id="3be13-128">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="3be13-129">Теперь вы обновили код приложения, поддерживающие новое `Rating` свойство.</span><span class="sxs-lookup"><span data-stu-id="3be13-129">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="3be13-130">Теперь запустите приложение и перейдите к */Movies* URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3be13-130">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="3be13-131">При этом, однако вы увидите следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="3be13-131">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="3be13-132">Вы видите эту ошибку, так как обновленный `Movie` класс модели в приложение теперь отличается от схемы `Movie` таблицы в существующей базе данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-132">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="3be13-133">(В таблице базы данных отсутствует столбец `Rating`.)</span><span class="sxs-lookup"><span data-stu-id="3be13-133">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="3be13-134">По умолчанию при использовании Entity Framework Code First для автоматического создания базы данных, как это делалось ранее в этом учебнике, Code First добавляет таблицу в базу данных, которая позволяет отслеживать синхронизацию с классами модели, в которой она была создана из схемы базы данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-134">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="3be13-135">Если синхронизация нарушена, Entity Framework завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3be13-135">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="3be13-136">Это упрощает для выявления проблем во время разработки, в противном случае только выявленных (по непонятные ошибки) во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="3be13-136">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="3be13-137">Средство проверки синхронизации, что вызывает сообщение об ошибке для отображения, который вы только что увидели.</span><span class="sxs-lookup"><span data-stu-id="3be13-137">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="3be13-138">Существует два подхода, устранить эту ошибку:</span><span class="sxs-lookup"><span data-stu-id="3be13-138">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="3be13-139">Можно с помощью Entity Framework автоматически удалить и повторно создать базу данных на основе новой схемы класса модели.</span><span class="sxs-lookup"><span data-stu-id="3be13-139">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="3be13-140">Этот подход очень удобен при выполнении активное развертывание в тестовой базы данных, так как он позволяет быстро развитие модели и схемы базы данных осуществляется одновременно.</span><span class="sxs-lookup"><span data-stu-id="3be13-140">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="3be13-141">Недостатком, однако является потеря существующих данных в базе данных, поэтому вы *не* хотите использовать этот подход на производственной базы данных!</span><span class="sxs-lookup"><span data-stu-id="3be13-141">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="3be13-142">Можно явно изменить схему существующей базы данных в соответствии с новыми классами модели.</span><span class="sxs-lookup"><span data-stu-id="3be13-142">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="3be13-143">Преимущество такого подхода состоит в том, что сохраняются все данные.</span><span class="sxs-lookup"><span data-stu-id="3be13-143">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="3be13-144">Это изменение можно выполнить как вручную, так и с помощью соответствующего скрипта базы данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-144">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="3be13-145">В этом учебнике мы будем использовать первый подход — вы Entity Framework Code First автоматически повторно создать базу данных каждый раз, когда модель изменяется.</span><span class="sxs-lookup"><span data-stu-id="3be13-145">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="3be13-146">Автоматическое повторное создание базы данных об изменениях модели</span><span class="sxs-lookup"><span data-stu-id="3be13-146">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="3be13-147">Давайте обновим приложение, чтобы Code First автоматически удаляет и повторно создает базу данных в любое время изменить модель для приложения.</span><span class="sxs-lookup"><span data-stu-id="3be13-147">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3be13-148">**Предупреждение** следует включить этот подход для автоматического удаления и повторного создания базы данных только в том случае, если вы используете базу данных разработки или тестирования, и *никогда не* рабочей базы данных, которая содержит реальные данные.</span><span class="sxs-lookup"><span data-stu-id="3be13-148">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="3be13-149">С его помощью на производственном сервере может привести к потере данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-149">Using it on a production server can lead to data loss.</span></span>


<span data-ttu-id="3be13-150">В **обозревателе решений**, щелкните правой кнопкой мыши *моделей* папку, выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="3be13-150">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="3be13-151">Назовите класс &quot;MovieInitializer&quot;.</span><span class="sxs-lookup"><span data-stu-id="3be13-151">Name the class &quot;MovieInitializer&quot;.</span></span> <span data-ttu-id="3be13-152">Обновление `MovieInitializer` класс, содержащий следующий код:</span><span class="sxs-lookup"><span data-stu-id="3be13-152">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

<span data-ttu-id="3be13-153">`MovieInitializer` Класс указывает, что удален базы данных, используемым в модели и они будут автоматически создан повторно, если все-таки измените классы моделей.</span><span class="sxs-lookup"><span data-stu-id="3be13-153">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="3be13-154">Включает в себя код `Seed` метод, чтобы задать время, некоторые данные по умолчанию, чтобы автоматически добавить в базу данных любой создании (или повторном создании).</span><span class="sxs-lookup"><span data-stu-id="3be13-154">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="3be13-155">Это обеспечивает удобный способ заполнения базы данных с демонстрационными данными, без необходимости вручную заполнить его каждый раз при внесении изменения модели.</span><span class="sxs-lookup"><span data-stu-id="3be13-155">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="3be13-156">Теперь, когда вы определили `MovieInitializer` класса, необходимо подключить его, чтобы при каждом запуске приложения, он проверяет, различаются ли классы моделей из схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-156">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="3be13-157">Если это так, можно запустить инициализатор для повторного создания базы данных совпадает с моделью, а затем заполнить базу данных с использованием образца данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-157">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="3be13-158">Откройте *Global.asax* файл, который находится в корне `MvcMovies` проекта:</span><span class="sxs-lookup"><span data-stu-id="3be13-158">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

<span data-ttu-id="3be13-159">*Global.asax* файл содержит класс, который определяет все приложение для проекта и содержит `Application_Start` обработчик событий, который выполняется при первом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="3be13-159">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="3be13-160">Найти `Application_Start` метод и добавьте вызов `Database.SetInitializer` в начале метода, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3be13-160">Find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

<span data-ttu-id="3be13-161">`Database.SetInitializer` Только что добавленного оператора указывает, что базы данных используется `MovieDBContext` экземпляр должен автоматически удаляется и создается повторно, если схемы и базы данных не совпадают.</span><span class="sxs-lookup"><span data-stu-id="3be13-161">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="3be13-162">И как можно было увидеть, он также заполняет базы данных с демонстрационными данными, который указан в `MovieInitializer` класса.</span><span class="sxs-lookup"><span data-stu-id="3be13-162">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="3be13-163">Закрыть *Global.asax* файл.</span><span class="sxs-lookup"><span data-stu-id="3be13-163">Close the *Global.asax* file.</span></span>

<span data-ttu-id="3be13-164">Повторно запустите приложение и перейдите к */Movies* URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3be13-164">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="3be13-165">При запуске приложения, он обнаруживает, что структура модели больше не соответствует схеме базы данных.</span><span class="sxs-lookup"><span data-stu-id="3be13-165">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="3be13-166">Автоматически повторно создает базу данных в соответствии с новой структуры модели и заполняет базу данных, с помощью Образец фильмов:</span><span class="sxs-lookup"><span data-stu-id="3be13-166">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

<span data-ttu-id="3be13-168">Нажмите кнопку **Create New** ссылку, чтобы добавить новый фильм.</span><span class="sxs-lookup"><span data-stu-id="3be13-168">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="3be13-169">Обратите внимание на то, что вы можете добавить оценку.</span><span class="sxs-lookup"><span data-stu-id="3be13-169">Note that you can add a rating.</span></span>

<span data-ttu-id="3be13-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3be13-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span></span>

<span data-ttu-id="3be13-171">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3be13-171">Click **Create**.</span></span> <span data-ttu-id="3be13-172">Этот новый фильм, включая оценку, отображается в окне списка фильмов:</span><span class="sxs-lookup"><span data-stu-id="3be13-172">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

<span data-ttu-id="3be13-174">В этом разделе вы узнали, как можно изменять объекты модели и синхронизации базы данных с изменениями.</span><span class="sxs-lookup"><span data-stu-id="3be13-174">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="3be13-175">Вы также узнали способ заполнения вновь созданную базу данных с демонстрационными данными, можно опробовать сценарии.</span><span class="sxs-lookup"><span data-stu-id="3be13-175">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="3be13-176">Теперь давайте взглянем на как можно добавить более широкие логику проверки в классы модели и включить некоторые бизнес-правила, которые будут применяться.</span><span class="sxs-lookup"><span data-stu-id="3be13-176">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3be13-177">[Назад](examining-the-edit-methods-and-edit-view.md)
> [Вперед](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="3be13-177">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>