---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
title: Создание приложения базы данных Movie за 15 минут с помощью ASP.NET MVC (C#) | Документация Майкрософт
author: StephenWalther
description: Стивен Вальтер строит всей базы данных приложения ASP.NET MVC от начала до конца. Это руководство является отличным введением для тех, кто новый t....
ms.author: riande
ms.date: 01/27/2009
ms.assetid: dd1be137-91c5-47a8-8137-fecf0789c7f5
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
msc.type: authoredcontent
ms.openlocfilehash: 51cc38989fb204a3d14e04fb280fdd81bfd38a4d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415171"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-c"></a><span data-ttu-id="e93f3-104">Создание приложения для базы данных Movie за 15 минут с помощью ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="e93f3-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (C#)</span></span>

<span data-ttu-id="e93f3-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e93f3-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="e93f3-106">Скачать код</span><span class="sxs-lookup"><span data-stu-id="e93f3-106">Download Code</span></span>](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_CS.zip)

> <span data-ttu-id="e93f3-107">Стивен Вальтер строит всей базы данных приложения ASP.NET MVC от начала до конца.</span><span class="sxs-lookup"><span data-stu-id="e93f3-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="e93f3-108">Это руководство предназначено для вас отличным введением для тех, кто не знаком с ASP.NET MVC Framework и хотят получить представление о процессе создания приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>


<span data-ttu-id="e93f3-109">Цель этого руководства является дать вам представление о «что это как» для создания приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="e93f3-110">В этом учебнике я смоделируйте рассматривается создание всего приложения ASP.NET MVC от начала до конца.</span><span class="sxs-lookup"><span data-stu-id="e93f3-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="e93f3-111">Я покажу, как создать простое приложение на основе базы данных, показано, как список, создания и редактирования записей базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="e93f3-112">Чтобы упростить процесс создания приложения, мы рассмотрим преимущества возможностей формирования шаблонов Visual Studio 2008.</span><span class="sxs-lookup"><span data-stu-id="e93f3-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="e93f3-113">Мы сообщим Visual Studio создать исходный код и содержимое для нашей контроллеры, модели и представления.</span><span class="sxs-lookup"><span data-stu-id="e93f3-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="e93f3-114">Если вы работали с страниц ASP или ASP.NET, затем следует найти ASP.NET MVC очень знакомым.</span><span class="sxs-lookup"><span data-stu-id="e93f3-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="e93f3-115">Представления ASP.NET MVC — это почти так, как и страницы в приложение Active Server Pages.</span><span class="sxs-lookup"><span data-stu-id="e93f3-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="e93f3-116">И так же, как и традиционные приложения ASP.NET Web Forms, ASP.NET MVC предоставляет полный доступ к широкому набору языков и классов, предоставляемых платформой .NET framework.</span><span class="sxs-lookup"><span data-stu-id="e93f3-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="e93f3-117">Я надеюсь является то, что этот учебник позволит получить представление о том, как работу с приложением ASP.NET MVC, аналогичные и отличается от работу с приложение Active Server Pages или веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e93f3-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="e93f3-118">Обзор приложения базы данных Movie</span><span class="sxs-lookup"><span data-stu-id="e93f3-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="e93f3-119">Так как наша цель — не усложнять, мы создадим очень простое приложение базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="e93f3-120">Наши простое приложение базы данных Movie позволит нам выполнить три действия:</span><span class="sxs-lookup"><span data-stu-id="e93f3-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="e93f3-121">Список набора записей базы данных movie</span><span class="sxs-lookup"><span data-stu-id="e93f3-121">List a set of movie database records</span></span>
2. <span data-ttu-id="e93f3-122">Создать новую запись базы данных movie</span><span class="sxs-lookup"><span data-stu-id="e93f3-122">Create a new movie database record</span></span>
3. <span data-ttu-id="e93f3-123">Изменить существующую запись базы данных movie</span><span class="sxs-lookup"><span data-stu-id="e93f3-123">Edit an existing movie database record</span></span>

<span data-ttu-id="e93f3-124">Опять же так как нам нужно, чтобы не усложнять, мы рассмотрим преимущества минимальное количество функций платформы ASP.NET MVC, необходимые для построения нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e93f3-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="e93f3-125">Например мы не используют преимущества разработки, направляемой тестированием.</span><span class="sxs-lookup"><span data-stu-id="e93f3-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="e93f3-126">Чтобы создать наше приложение, нам нужно выполнить каждое из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="e93f3-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="e93f3-127">Создание проекта веб-приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e93f3-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="e93f3-128">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-128">Create the database</span></span>
3. <span data-ttu-id="e93f3-129">Создание модели базы данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-129">Create the database model</span></span>
4. <span data-ttu-id="e93f3-130">Создание контроллера ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e93f3-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="e93f3-131">Создание представления ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e93f3-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="e93f3-132">Предварительные действия</span><span class="sxs-lookup"><span data-stu-id="e93f3-132">Preliminaries</span></span>

<span data-ttu-id="e93f3-133">Вам потребуется Visual Studio 2008 или Visual Web Developer 2008 Express, чтобы создать приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="e93f3-134">Вам также потребуется платформа ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="e93f3-135">Если вы не являетесь владельцем Visual Studio 2008, можно загрузить 90-дневную пробную версию Visual Studio 2008 с этого веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="e93f3-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="e93f3-136">Кроме того создаются ASP.NET MVC приложений с помощью Visual Web Developer Express 2008.</span><span class="sxs-lookup"><span data-stu-id="e93f3-136">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="e93f3-137">Если вы решили использовать Visual Web Developer Express, то вы должны иметь установленным пакетом обновления 1.</span><span class="sxs-lookup"><span data-stu-id="e93f3-137">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="e93f3-138">Visual Web Developer 2008 Express с пакетом обновления 1 можно загрузить с этого веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="e93f3-138">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="e93f3-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp; displaylang = en</span><span class="sxs-lookup"><span data-stu-id="e93f3-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="e93f3-140">После установки Visual Studio 2008 или Visual Web Developer 2008, необходимо установить ASP.NET MVC framework.</span><span class="sxs-lookup"><span data-stu-id="e93f3-140">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="e93f3-141">Платформа ASP.NET MVC можно загрузить на следующих веб-сайте:</span><span class="sxs-lookup"><span data-stu-id="e93f3-141">You can download the ASP.NET MVC framework from the following website:</span></span>

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="e93f3-142">Вместо скачивания платформы ASP.NET и ASP.NET MVC framework по отдельности, можно воспользоваться преимуществами установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="e93f3-142">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="e93f3-143">Установщик веб-платформы является приложение, которое позволяет легко управлять установленных приложений на компьютере:</span><span class="sxs-lookup"><span data-stu-id="e93f3-143">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="e93f3-144">Создание проекта веб-приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e93f3-144">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="e93f3-145">Давайте начнем с создания проекта веб-приложения ASP.NET MVC в Visual Studio 2008.</span><span class="sxs-lookup"><span data-stu-id="e93f3-145">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="e93f3-146">Выберите пункт меню **файл, создать проект** и вы увидите диалоговое окно нового проекта на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="e93f3-146">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="e93f3-147">Выберите в качестве языка программирования C# и выберите шаблон проекта веб-приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-147">Select C# as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="e93f3-148">Присвойте проекту имя MovieApp и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="e93f3-148">Give your project the name MovieApp and click the OK button.</span></span>


[![T<span data-ttu-id="e93f3-149">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-149">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)

<span data-ttu-id="e93f3-150">**Рис 01**: В диалоговом окне нового проекта ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-150">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))</span></span>


<span data-ttu-id="e93f3-151">Убедитесь, что выбран .NET Framework 3.5 из раскрывающегося списка в верхней части диалогового окна нового проекта или шаблона проекта веб-приложения ASP.NET MVC не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="e93f3-151">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>


<span data-ttu-id="e93f3-152">Каждый раз при создании проекта веб-приложение MVC, Visual Studio появится запрос на создание проекта модульного теста.</span><span class="sxs-lookup"><span data-stu-id="e93f3-152">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="e93f3-153">Откроется диалоговое окно, на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="e93f3-153">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="e93f3-154">Так как мы не будете создавать тесты в этом руководстве из-за ограничений по времени (и, Да, мы должны будете чувствовать себя немного виновны об этом) выберите **нет** и нажмите кнопку **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e93f3-154">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e93f3-155">Visual Web Developer не поддерживает проекты тестов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-155">Visual Web Developer does not support test projects.</span></span>


[![T<span data-ttu-id="e93f3-156">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-156">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)

<span data-ttu-id="e93f3-157">**Рис. 02**: Диалоговое окно создания проекта модульного теста ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-157">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))</span></span>


<span data-ttu-id="e93f3-158">Приложение ASP.NET MVC имеет стандартный набор папок: в моделях, представлениях и контроллерах папку.</span><span class="sxs-lookup"><span data-stu-id="e93f3-158">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="e93f3-159">Вы увидите этот стандартный набор папок в окне обозревателя решений.</span><span class="sxs-lookup"><span data-stu-id="e93f3-159">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="e93f3-160">Необходимо добавить файлы в каждую папку моделях, представлениях и контроллерах для построения нашего приложения базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-160">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="e93f3-161">При создании нового приложения MVC с помощью Visual Studio, вы получите пример приложения.</span><span class="sxs-lookup"><span data-stu-id="e93f3-161">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="e93f3-162">Поскольку мы хотим начать с нуля, нам нужно удалить содержимое для этого примера приложения.</span><span class="sxs-lookup"><span data-stu-id="e93f3-162">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="e93f3-163">Вам потребуется удалить следующий файл, а также в следующую папку:</span><span class="sxs-lookup"><span data-stu-id="e93f3-163">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="e93f3-164">Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="e93f3-164">Controllers\HomeController.cs</span></span>
- <span data-ttu-id="e93f3-165">Views\Home</span><span class="sxs-lookup"><span data-stu-id="e93f3-165">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="e93f3-166">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-166">Creating the Database</span></span>

<span data-ttu-id="e93f3-167">Нам нужно создать базу данных для хранения наших записей базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-167">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="e93f3-168">К счастью Visual Studio включает бесплатную базу данных с именем SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="e93f3-168">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="e93f3-169">Выполните следующие действия для создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-169">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="e93f3-170">Щелкните правой кнопкой мыши приложение\_папка данных в окно обозревателя решений и выберите пункт меню **добавить, новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-170">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="e93f3-171">Выберите **данных** категорию и выберите **базы данных SQL Server** шаблона (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="e93f3-171">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="e93f3-172">Присвойте имя новой базы данных *MoviesDB.mdf* и нажмите кнопку **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e93f3-172">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="e93f3-173">После создания базы данных, вы может соединиться с базой данных, дважды щелкнув файл MoviesDB.mdf, расположенный в приложении\_папку данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-173">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="e93f3-174">Дважды щелкните файл MoviesDB.mdf открыть окно обозревателя сервера.</span><span class="sxs-lookup"><span data-stu-id="e93f3-174">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e93f3-175">Окно обозревателя сервера с именем окна обозревателя базы данных в случае Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="e93f3-175">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>


[![T<span data-ttu-id="e93f3-176">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-176">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)

<span data-ttu-id="e93f3-177">**Рис 03**: Создание базы данных Microsoft SQL Server ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-177">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))</span></span>


<span data-ttu-id="e93f3-178">Далее нам нужно создать новую таблицу базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-178">Next, we need to create a new database table.</span></span> <span data-ttu-id="e93f3-179">Из окна обозревателя сервера, щелкните правой кнопкой мыши папку «таблицы» и выберите пункт меню **добавить новую таблицу**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-179">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="e93f3-180">Если выбрать этот пункт меню откроется конструктор таблиц базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-180">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="e93f3-181">Создайте следующие столбцы базы данных:</span><span class="sxs-lookup"><span data-stu-id="e93f3-181">Create the following database columns:</span></span>

<a id="0.1_table01"></a>


| **<span data-ttu-id="e93f3-182">Имя столбца</span><span class="sxs-lookup"><span data-stu-id="e93f3-182">Column Name</span></span>** | **<span data-ttu-id="e93f3-183">Тип данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-183">Data Type</span></span>** | **<span data-ttu-id="e93f3-184">Разрешить значения null</span><span class="sxs-lookup"><span data-stu-id="e93f3-184">Allow Nulls</span></span>** |
| --- | --- | --- |
| <span data-ttu-id="e93f3-185">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="e93f3-185">Id</span></span> | <span data-ttu-id="e93f3-186">Int</span><span class="sxs-lookup"><span data-stu-id="e93f3-186">Int</span></span> | <span data-ttu-id="e93f3-187">False</span><span class="sxs-lookup"><span data-stu-id="e93f3-187">False</span></span> |
| <span data-ttu-id="e93f3-188">Заголовок</span><span class="sxs-lookup"><span data-stu-id="e93f3-188">Title</span></span> | <span data-ttu-id="e93f3-189">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="e93f3-189">Nvarchar(100)</span></span> | <span data-ttu-id="e93f3-190">False</span><span class="sxs-lookup"><span data-stu-id="e93f3-190">False</span></span> |
| <span data-ttu-id="e93f3-191">Директор</span><span class="sxs-lookup"><span data-stu-id="e93f3-191">Director</span></span> | <span data-ttu-id="e93f3-192">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="e93f3-192">Nvarchar(100)</span></span> | <span data-ttu-id="e93f3-193">False</span><span class="sxs-lookup"><span data-stu-id="e93f3-193">False</span></span> |
| <span data-ttu-id="e93f3-194">DateReleased</span><span class="sxs-lookup"><span data-stu-id="e93f3-194">DateReleased</span></span> | <span data-ttu-id="e93f3-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="e93f3-195">DateTime</span></span> | <span data-ttu-id="e93f3-196">False</span><span class="sxs-lookup"><span data-stu-id="e93f3-196">False</span></span> |


<span data-ttu-id="e93f3-197">Первый столбец, столбец идентификатора, имеет два специальных свойства.</span><span class="sxs-lookup"><span data-stu-id="e93f3-197">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="e93f3-198">Во-первых необходимо пометить идентификатор столбца, как столбец первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="e93f3-198">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="e93f3-199">После выбора столбца идентификатора, нажмите кнопку **задать первичный ключ** (это значок, который выглядит как ключ).</span><span class="sxs-lookup"><span data-stu-id="e93f3-199">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="e93f3-200">Во-вторых необходимо пометить идентификатор столбца, как столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-200">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="e93f3-201">В окне «Свойства столбца» перейдите к разделу Спецификация идентификатора и разверните его.</span><span class="sxs-lookup"><span data-stu-id="e93f3-201">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="e93f3-202">Изменение **Is Identity** в соответствии с значением **Да**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-202">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="e93f3-203">Когда вы закончите, таблица должна выглядеть как на рис. 4.</span><span class="sxs-lookup"><span data-stu-id="e93f3-203">When you are finished, the table should look like Figure 4.</span></span>


[![T<span data-ttu-id="e93f3-204">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-204">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)

<span data-ttu-id="e93f3-205">**Рис. 04**: В таблице базы данных фильмов ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-205">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))</span></span>


<span data-ttu-id="e93f3-206">Последним шагом является сохранение новой таблицы.</span><span class="sxs-lookup"><span data-stu-id="e93f3-206">The final step is to save the new table.</span></span> <span data-ttu-id="e93f3-207">Нажмите кнопку "Сохранить" (значок дискеты) и присвойте новой таблицы фильмы имя.</span><span class="sxs-lookup"><span data-stu-id="e93f3-207">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="e93f3-208">После создания таблицы, добавьте некоторые записи фильма в таблицу.</span><span class="sxs-lookup"><span data-stu-id="e93f3-208">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="e93f3-209">Щелкните правой кнопкой мыши в таблице фильмов в окно обозревателя сервера и выберите пункт меню **Показать таблицу данных**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-209">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="e93f3-210">Введите список ваших любимых фильмов (см. рис. 5).</span><span class="sxs-lookup"><span data-stu-id="e93f3-210">Enter a list of your favorite movies (see Figure 5).</span></span>


[![T<span data-ttu-id="e93f3-211">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-211">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)

<span data-ttu-id="e93f3-212">**05 рис**: Введя записей фильмов ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-212">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))</span></span>


## <a name="creating-the-model"></a><span data-ttu-id="e93f3-213">Создание модели</span><span class="sxs-lookup"><span data-stu-id="e93f3-213">Creating the Model</span></span>

<span data-ttu-id="e93f3-214">Далее нам нужно создать набор классов для представления нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-214">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="e93f3-215">Нам нужно создать модель базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-215">We need to create a database model.</span></span> <span data-ttu-id="e93f3-216">Мы рассмотрим преимущества Microsoft Entity Framework, чтобы автоматически создать классы для нашей модели базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-216">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e93f3-217">Платформа ASP.NET MVC не привязан к Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="e93f3-217">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="e93f3-218">Базы данных можно создавать классы модели за счет использования различных реляционное сопоставление объекта (или / M) средства, включая LINQ to SQL, Subsonic и NHibernate.</span><span class="sxs-lookup"><span data-stu-id="e93f3-218">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>


<span data-ttu-id="e93f3-219">Выполните следующие действия, чтобы запустить мастер моделей EDM.</span><span class="sxs-lookup"><span data-stu-id="e93f3-219">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="e93f3-220">Щелкните правой кнопкой мыши папку Models в окне обозревателя решений и выберите пункт меню **добавить, новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-220">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="e93f3-221">Выберите **данных** категорию и выберите **ADO.NET Entity Data Model** шаблона.</span><span class="sxs-lookup"><span data-stu-id="e93f3-221">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="e93f3-222">Назовите модель данных *MoviesDBModel.edmx* и нажмите кнопку **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e93f3-222">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="e93f3-223">После нажатия кнопки Добавить появится мастер модели EDM (см. рис. 6).</span><span class="sxs-lookup"><span data-stu-id="e93f3-223">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="e93f3-224">Выполните следующие действия, чтобы завершить работу мастера.</span><span class="sxs-lookup"><span data-stu-id="e93f3-224">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="e93f3-225">В **Выбор содержимого модели** выберите **создать из базы данных** параметр.</span><span class="sxs-lookup"><span data-stu-id="e93f3-225">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="e93f3-226">В **Выбор подключения к данным** шаг, используйте *MoviesDB.mdf* подключение к данным и имя *MoviesDBEntities* параметры подключения.</span><span class="sxs-lookup"><span data-stu-id="e93f3-226">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="e93f3-227">Нажмите кнопку **Далее** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e93f3-227">Click the **Next** button.</span></span>
3. <span data-ttu-id="e93f3-228">В **Choose Your Database Objects** шаг, разверните узел таблицы, выберите таблицу фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-228">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="e93f3-229">Введите пространство имен *MovieApp.Models* и нажмите кнопку **Готово** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e93f3-229">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>


[![T<span data-ttu-id="e93f3-230">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-230">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)

<span data-ttu-id="e93f3-231">**Рис 06**: Создание модели базы данных с помощью мастера моделей EDM ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-231">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))</span></span>


<span data-ttu-id="e93f3-232">После завершения мастера модели EDM, откроется в конструкторе моделей EDM.</span><span class="sxs-lookup"><span data-stu-id="e93f3-232">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="e93f3-233">Конструктор должен отображать в таблице базы данных фильмов (см. рис. 7).</span><span class="sxs-lookup"><span data-stu-id="e93f3-233">The Designer should display the Movies database table (see Figure 7).</span></span>


[![T<span data-ttu-id="e93f3-234">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-234">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)

<span data-ttu-id="e93f3-235">**07 рис**: В конструкторе моделей EDM ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-235">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))</span></span>


<span data-ttu-id="e93f3-236">Нам нужно внести одно изменение, перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="e93f3-236">We need to make one change before we continue.</span></span> <span data-ttu-id="e93f3-237">Мастер EDM создает класс с именем модели *фильмы* , представляющий таблицу базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-237">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="e93f3-238">Так как мы будем использовать класс фильмов для представления определенного фильма, нам нужно изменить имя класса, чтобы быть *фильма* вместо *фильмы* (единственного числа, а не во множественном числе).</span><span class="sxs-lookup"><span data-stu-id="e93f3-238">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="e93f3-239">Дважды щелкните имя класса в области конструктора и измените имя класса из фильмов на фильм.</span><span class="sxs-lookup"><span data-stu-id="e93f3-239">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="e93f3-240">После внесения этого изменения, нажмите кнопку **Сохранить** кнопку для создания класса Movie (значок дискеты).</span><span class="sxs-lookup"><span data-stu-id="e93f3-240">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="e93f3-241">Создание контроллера ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e93f3-241">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="e93f3-242">Следующим шагом является создание контроллера ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-242">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="e93f3-243">Контроллер отвечает за управление как пользователь взаимодействует с приложением ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-243">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="e93f3-244">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e93f3-244">Follow these steps:</span></span>

1. <span data-ttu-id="e93f3-245">В окне обозревателя решений щелкните правой кнопкой мыши папку Controllers и выберите пункт меню **Add, контроллера**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-245">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="e93f3-246">В диалоговом окне "Добавление контроллера", введите имя *HomeController* и установите флажок "с меткой" **добавить методы действий для сценариев создания, обновления и сведения о** (см. рис. 8).</span><span class="sxs-lookup"><span data-stu-id="e93f3-246">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="e93f3-247">Нажмите кнопку **добавить** кнопку, чтобы добавить новый контроллер в проект.</span><span class="sxs-lookup"><span data-stu-id="e93f3-247">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="e93f3-248">После выполнения этих действий создается контроллер в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="e93f3-248">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="e93f3-249">Обратите внимание на то, что он содержит методы, с именем индекса, сведения, создать и изменить.</span><span class="sxs-lookup"><span data-stu-id="e93f3-249">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="e93f3-250">В следующих разделах мы добавим необходимый код для получения этих методов для работы.</span><span class="sxs-lookup"><span data-stu-id="e93f3-250">In the following sections, we'll add the necessary code to get these methods to work.</span></span>


[![T<span data-ttu-id="e93f3-251">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-251">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)

<span data-ttu-id="e93f3-252">**Рис 08**: Добавление нового контроллера MVC ASP.NET ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-252">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))</span></span>


**<span data-ttu-id="e93f3-253">В листинге 1 — Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="e93f3-253">Listing 1 – Controllers\HomeController.cs</span></span>**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample1.cs)]

## <a name="listing-database-records"></a><span data-ttu-id="e93f3-254">Список записей базы данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-254">Listing Database Records</span></span>

<span data-ttu-id="e93f3-255">Метод Index() контроллера Home способ по умолчанию для приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-255">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="e93f3-256">При запуске приложения ASP.NET MVC, метод Index() — первый вызываемый метод контроллера.</span><span class="sxs-lookup"><span data-stu-id="e93f3-256">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="e93f3-257">Мы будем использовать метод Index() для отображения списка записей из таблицы базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-257">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="e93f3-258">Мы рассмотрим преимущества базы данных классов модели, которые мы создали ранее для получения записей базы данных фильмов с помощью метода Index().</span><span class="sxs-lookup"><span data-stu-id="e93f3-258">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="e93f3-259">Я изменил в класс HomeController в листинге 2, чтобы он содержал новый закрытое поле, именуемое \_db.</span><span class="sxs-lookup"><span data-stu-id="e93f3-259">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="e93f3-260">Представляет класс MoviesDBEntities нашей базы данных модели, и мы будем использовать этот класс для взаимодействия с нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-260">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="e93f3-261">Я также изменил метод Index() в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="e93f3-261">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="e93f3-262">Метод Index() используется класс MoviesDBEntities для получения всех записей фильмов из таблицы базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-262">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="e93f3-263">Выражение  *\_db. MovieSet.ToList()* возвращает список всех записей фильмов из таблицы базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-263">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="e93f3-264">Список фильмов передается в представление.</span><span class="sxs-lookup"><span data-stu-id="e93f3-264">The list of movies is passed to the view.</span></span> <span data-ttu-id="e93f3-265">Все, что передается в метод View() передается в представление как представление данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-265">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

**<span data-ttu-id="e93f3-266">В листинге 2 — Controllers/HomeController.cs (измененный метод Index)</span><span class="sxs-lookup"><span data-stu-id="e93f3-266">Listing 2 – Controllers/HomeController.cs (modified Index method)</span></span>**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample2.cs)]

<span data-ttu-id="e93f3-267">Метод Index() возвращает представление с именем Index.</span><span class="sxs-lookup"><span data-stu-id="e93f3-267">The Index() method returns a view named Index.</span></span> <span data-ttu-id="e93f3-268">Нам нужно создать это представление для отображения списка записей базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-268">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="e93f3-269">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e93f3-269">Follow these steps:</span></span>


<span data-ttu-id="e93f3-270">Нужно построить проект (выберите пункт меню **создать, собрать решение**) перед открытием **Добавление представления** dialog» или «нет классов будет отображаться в **просмотреть класс данных** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="e93f3-270">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>


1. <span data-ttu-id="e93f3-271">Щелкните правой кнопкой мыши метод Index() в редакторе кода и выберите пункт меню **Добавление представления** (см. рис. 9).</span><span class="sxs-lookup"><span data-stu-id="e93f3-271">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="e93f3-272">В диалоговом окне «Добавление представления» убедитесь, что флажок с меткой **создать строго типизированное представление** проверяется.</span><span class="sxs-lookup"><span data-stu-id="e93f3-272">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="e93f3-273">Из **просматривать содержимое** раскрывающемся списке выберите значение *списка*.</span><span class="sxs-lookup"><span data-stu-id="e93f3-273">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="e93f3-274">Из **просмотреть класс данных** раскрывающемся списке выберите значение *MovieApp.Models.Movie*.</span><span class="sxs-lookup"><span data-stu-id="e93f3-274">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="e93f3-275">Нажмите кнопку "Добавить" для создания нового представления (см. рис. 10).</span><span class="sxs-lookup"><span data-stu-id="e93f3-275">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="e93f3-276">После выполнения этих действий, новое представление с именем Index.aspx добавляется к папке Views\Home.</span><span class="sxs-lookup"><span data-stu-id="e93f3-276">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="e93f3-277">Содержимое представления индекса включаются в листинге 3.</span><span class="sxs-lookup"><span data-stu-id="e93f3-277">The contents of the Index view are included in Listing 3.</span></span>


[![T<span data-ttu-id="e93f3-278">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-278">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)

<span data-ttu-id="e93f3-279">**Рис 09**: Добавление представления из действия контроллера ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-279">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))</span></span>


[![T<span data-ttu-id="e93f3-280">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-280">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)

<span data-ttu-id="e93f3-281">**Рис. 10**: Создать новое представление с диалоговым окном Добавление представления ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-281">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))</span></span>


**<span data-ttu-id="e93f3-282">Листинг 3 – Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="e93f3-282">Listing 3 – Views\Home\Index.aspx</span></span>**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample3.aspx)]

<span data-ttu-id="e93f3-283">В представлении индекса отображаются все записи фильма из таблицы базы данных фильмов в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="e93f3-283">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="e93f3-284">Представление содержит цикл по каждому элементу, который выполняет итерацию каждого фильма, представленный свойством ViewData.Model.</span><span class="sxs-lookup"><span data-stu-id="e93f3-284">The view contains a foreach loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="e93f3-285">Если вы запустите приложение, нажав клавишу F5, вы увидите веб-страницы на рис. 11.</span><span class="sxs-lookup"><span data-stu-id="e93f3-285">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>


[![T<span data-ttu-id="e93f3-286">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-286">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)

<span data-ttu-id="e93f3-287">**Рис. 11**: Представление Index ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-287">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))</span></span>


## <a name="creating-new-database-records"></a><span data-ttu-id="e93f3-288">Создание новых записей базы данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-288">Creating New Database Records</span></span>

<span data-ttu-id="e93f3-289">Представление Index, созданную в предыдущем разделе со ссылкой для создания новых записей базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-289">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="e93f3-290">Давайте продолжим и реализовать логику и создать представление, необходимое для создания новых записей базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-290">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="e93f3-291">Контроллер Home содержит два метода с именем Create().</span><span class="sxs-lookup"><span data-stu-id="e93f3-291">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="e93f3-292">Первый метод Create() не имеет параметров.</span><span class="sxs-lookup"><span data-stu-id="e93f3-292">The first Create() method has no parameters.</span></span> <span data-ttu-id="e93f3-293">Эта перегрузка метода Create() используется для отображения HTML-формы для создания новой записи базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-293">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="e93f3-294">Второй метод Create() имеет параметр FormCollection.</span><span class="sxs-lookup"><span data-stu-id="e93f3-294">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="e93f3-295">Эта перегрузка метода Create() вызывается в том случае, когда HTML для создания новый фильм отправкой формы на сервер.</span><span class="sxs-lookup"><span data-stu-id="e93f3-295">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="e93f3-296">Обратите внимание, что этот второй метод Create() AcceptVerbs атрибут, который запрещает метода вызывается, пока не будет выполнена операция HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e93f3-296">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP POST operation is performed.</span></span>

<span data-ttu-id="e93f3-297">Этот второй метод Create() был изменен в класс HomeController, обновленные в листинге 4.</span><span class="sxs-lookup"><span data-stu-id="e93f3-297">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="e93f3-298">Новая версия Create() метод принимает параметр фильма и содержит логику для вставки новый фильм в таблице базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-298">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e93f3-299">Обратите внимание на атрибут привязки.</span><span class="sxs-lookup"><span data-stu-id="e93f3-299">Notice the Bind attribute.</span></span> <span data-ttu-id="e93f3-300">Так как мы не хотим обновить свойство идентификатор фильма из формы HTML, необходимо явно исключить это свойство.</span><span class="sxs-lookup"><span data-stu-id="e93f3-300">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>


**<span data-ttu-id="e93f3-301">Листинг 4 — Controllers\HomeController.cs (измененный метод Create)</span><span class="sxs-lookup"><span data-stu-id="e93f3-301">Listing 4 – Controllers\HomeController.cs (modified Create method)</span></span>**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample4.cs)]

<span data-ttu-id="e93f3-302">Visual Studio упрощает создание формы для создания новой базы данных movie записи (см. рис. 12).</span><span class="sxs-lookup"><span data-stu-id="e93f3-302">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="e93f3-303">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e93f3-303">Follow these steps:</span></span>

1. <span data-ttu-id="e93f3-304">Щелкните правой кнопкой мыши метод Create() в редакторе кода и выберите пункт меню **Добавление представления**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-304">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="e93f3-305">Убедитесь, что флажок с меткой **создать строго типизированное представление** проверяется.</span><span class="sxs-lookup"><span data-stu-id="e93f3-305">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="e93f3-306">Из **просматривать содержимое** раскрывающемся списке выберите значение *создать*.</span><span class="sxs-lookup"><span data-stu-id="e93f3-306">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="e93f3-307">Из **просмотреть класс данных** раскрывающемся списке выберите значение *MovieApp.Models.Movie*.</span><span class="sxs-lookup"><span data-stu-id="e93f3-307">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="e93f3-308">Нажмите кнопку **добавить** кнопку, чтобы создать новое представление.</span><span class="sxs-lookup"><span data-stu-id="e93f3-308">Click the **Add** button to create the new view.</span></span>


[![T<span data-ttu-id="e93f3-309">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-309">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)

<span data-ttu-id="e93f3-310">**Рис. 12**: Добавление представления создания ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-310">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))</span></span>


<span data-ttu-id="e93f3-311">Visual Studio автоматически создает представление в листинге 5.</span><span class="sxs-lookup"><span data-stu-id="e93f3-311">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="e93f3-312">Это представление содержит HTML-форму, включающий поля, которые соответствуют каждому из свойств класса фильма.</span><span class="sxs-lookup"><span data-stu-id="e93f3-312">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

**<span data-ttu-id="e93f3-313">Listing 5 – Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="e93f3-313">Listing 5 – Views\Home\Create.aspx</span></span>**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="e93f3-314">HTML-формы, созданные в диалоговом окне Add View создает поле идентификатора формы.</span><span class="sxs-lookup"><span data-stu-id="e93f3-314">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="e93f3-315">Так как столбец идентификатора является столбцом идентификаторов, нам не нужен этот поля формы и ее можно безопасно удалить.</span><span class="sxs-lookup"><span data-stu-id="e93f3-315">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>


<span data-ttu-id="e93f3-316">После добавления представления создания, можно добавить новые записи фильма к базе данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-316">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="e93f3-317">Запустите приложение, нажав клавишу F5 и нажмите кнопку Создать ссылку, чтобы просмотреть форму на рис. 13.</span><span class="sxs-lookup"><span data-stu-id="e93f3-317">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="e93f3-318">Если заполнения и отправки формы, создается запись новый фильм в базе данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-318">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="e93f3-319">Обратите внимание, что вы получаете проверку формы автоматически.</span><span class="sxs-lookup"><span data-stu-id="e93f3-319">Notice that you get form validation automatically.</span></span> <span data-ttu-id="e93f3-320">Если не ввести дату выпуска фильма, или введите дату недействительный выпуск, отобразится форма, и выделяется поле даты выхода.</span><span class="sxs-lookup"><span data-stu-id="e93f3-320">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>


[![T<span data-ttu-id="e93f3-321">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-321">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)

<span data-ttu-id="e93f3-322">**Рис. 13**: Создание новой записи базы данных movie ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-322">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))</span></span>


## <a name="editing-existing-database-records"></a><span data-ttu-id="e93f3-323">Изменение существующих записей базы данных</span><span class="sxs-lookup"><span data-stu-id="e93f3-323">Editing Existing Database Records</span></span>

<span data-ttu-id="e93f3-324">В предыдущих разделах мы рассмотрели, как список и создания новых записей базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-324">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="e93f3-325">В этом заключительном разделе мы рассмотрим, как можно изменить существующие записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-325">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="e93f3-326">Во-первых необходимо создать форму редактирования.</span><span class="sxs-lookup"><span data-stu-id="e93f3-326">First, we need to generate the Edit form.</span></span> <span data-ttu-id="e93f3-327">Этот шаг является простой, так как Visual Studio создаст форму редактирования для нас автоматически.</span><span class="sxs-lookup"><span data-stu-id="e93f3-327">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="e93f3-328">Откройте класс HomeController.cs в редакторе кода Visual Studio и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e93f3-328">Open the HomeController.cs class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="e93f3-329">Щелкните правой кнопкой мыши метод Edit() в редакторе кода и выберите пункт меню **Добавление представления** (см. рис. 14).</span><span class="sxs-lookup"><span data-stu-id="e93f3-329">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="e93f3-330">Установите флажок "с меткой" **создать строго типизированное представление**.</span><span class="sxs-lookup"><span data-stu-id="e93f3-330">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="e93f3-331">Из **просматривать содержимое** раскрывающемся списке выберите значение *изменить*.</span><span class="sxs-lookup"><span data-stu-id="e93f3-331">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="e93f3-332">Из **просмотреть класс данных** раскрывающемся списке выберите значение *MovieApp.Models.Movie*.</span><span class="sxs-lookup"><span data-stu-id="e93f3-332">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="e93f3-333">Нажмите кнопку **добавить** кнопку, чтобы создать новое представление.</span><span class="sxs-lookup"><span data-stu-id="e93f3-333">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="e93f3-334">Выполнение этих действий добавляет новое представление с именем Edit.aspx в папку Views\Home.</span><span class="sxs-lookup"><span data-stu-id="e93f3-334">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="e93f3-335">Это представление содержит HTML-формы для редактирования и фильмов.</span><span class="sxs-lookup"><span data-stu-id="e93f3-335">This view contains an HTML form for editing a movie record.</span></span>


[![T<span data-ttu-id="e93f3-336">диалоговое окно нового проекта он]</span><span class="sxs-lookup"><span data-stu-id="e93f3-336">he New Project dialog box]</span></span>(create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)

<span data-ttu-id="e93f3-337">**Рис. 14**: Добавление представления изменения ([Просмотр полноразмерного изображения](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="e93f3-337">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="e93f3-338">Изменить представление содержит поля формы HTML, соответствующее свойству, идентификатор фильма.</span><span class="sxs-lookup"><span data-stu-id="e93f3-338">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="e93f3-339">Так как вы не хотите людей, изменив значение свойства Id, следует удалить это поле формы.</span><span class="sxs-lookup"><span data-stu-id="e93f3-339">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>


<span data-ttu-id="e93f3-340">Наконец нам нужно изменить контроллера Home, таким образом, чтобы он поддерживает редактирование записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-340">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="e93f3-341">Обновленный класс HomeController содержится в листинге 6.</span><span class="sxs-lookup"><span data-stu-id="e93f3-341">The updated HomeController class is contained in Listing 6.</span></span>

**<span data-ttu-id="e93f3-342">В листинге 6 – Controllers\HomeController.cs (методов Edit)</span><span class="sxs-lookup"><span data-stu-id="e93f3-342">Listing 6 – Controllers\HomeController.cs (Edit methods)</span></span>**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample6.cs)]

<span data-ttu-id="e93f3-343">В листинге 6 я добавил дополнительную логику для обеих перегрузок метода Edit().</span><span class="sxs-lookup"><span data-stu-id="e93f3-343">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="e93f3-344">Первый метод Edit() возвращает запись базы данных фильмов, соответствующий параметру Id, передаваемый в метод.</span><span class="sxs-lookup"><span data-stu-id="e93f3-344">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="e93f3-345">Вторая перегрузка выполняет обновления записи фильм в базе данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-345">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="e93f3-346">Обратите внимание на то, что необходимо получить исходного фильма, а затем вызовите ApplyPropertyChanges(), чтобы обновить существующий фильм в базе данных.</span><span class="sxs-lookup"><span data-stu-id="e93f3-346">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="e93f3-347">Сводка</span><span class="sxs-lookup"><span data-stu-id="e93f3-347">Summary</span></span>

<span data-ttu-id="e93f3-348">Цель этого руководства было дать вам представление о работу с приложением ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-348">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="e93f3-349">Я надеюсь, что обнаружение, что создание веб-приложения ASP.NET MVC является очень похожа на работу с приложение Active Server Pages или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e93f3-349">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="e93f3-350">В этом учебнике мы рассмотрели только самые основные функции платформы ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e93f3-350">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="e93f3-351">В последующих учебных курсах мы подробнее рассмотрим таким темам, как контроллеры, действия контроллера, представления, просмотр данных и вспомогательных методов HTML.</span><span class="sxs-lookup"><span data-stu-id="e93f3-351">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e93f3-352">Далее</span><span class="sxs-lookup"><span data-stu-id="e93f3-352">Next</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb.md)
