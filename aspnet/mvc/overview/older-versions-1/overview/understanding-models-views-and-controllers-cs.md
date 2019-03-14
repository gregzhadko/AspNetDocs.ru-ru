---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: Общие сведения о моделях, представлениях и контроллерах (C#) | Документация Майкрософт
author: StephenWalther
description: Не понимаете, о моделях, представлениях и контроллерах? В этом руководстве Стивен Вальтер рассказывается о различных частях приложения ASP.NET MVC.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 5e9186a6c261266de8f1a1509a49b84b359bd920
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040581"
---
<a name="understanding-models-views-and-controllers-c"></a><span data-ttu-id="f93f2-104">Общие сведения о моделях, представлениях и контроллерах (C#)</span><span class="sxs-lookup"><span data-stu-id="f93f2-104">Understanding Models, Views, and Controllers (C#)</span></span>
====================
<span data-ttu-id="f93f2-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="f93f2-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="f93f2-106">Не понимаете, о моделях, представлениях и контроллерах?</span><span class="sxs-lookup"><span data-stu-id="f93f2-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="f93f2-107">В этом руководстве Стивен Вальтер рассказывается о различных частях приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>


<span data-ttu-id="f93f2-108">Этот учебник дает общий обзор ASP.NET MVC моделях, представлениях и контроллерах.</span><span class="sxs-lookup"><span data-stu-id="f93f2-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="f93f2-109">Другими словами, он объясняет M ", V" и C "в ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="f93f2-110">После изучения этого учебника, необходимо понимать, как взаимодействуют различные части приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="f93f2-111">Необходимо также понимать, как архитектура приложения ASP.NET MVC отличается от приложения веб-форм ASP.NET или приложения ASP-страницы.</span><span class="sxs-lookup"><span data-stu-id="f93f2-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="f93f2-112">Пример приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f93f2-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="f93f2-113">Шаблон Visual Studio по умолчанию для создания веб-приложений ASP.NET MVC включает в себя пример очень простого приложения, которое можно использовать для понимания различные части приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="f93f2-114">Мы используем это простое приложение, в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f93f2-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="f93f2-115">Создание нового приложения ASP.NET MVC с помощью шаблона MVC, запустив Visual Studio 2008 и выбрав пункт меню файл, создать проект (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="f93f2-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="f93f2-116">В диалоговом окне нового проекта выберите вашем любимом языке программирования, в списке типов проектов (Visual Basic или C#) и выберите **веб-приложение ASP.NET MVC** в группе шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f93f2-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="f93f2-117">Нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="f93f2-117">Click the OK button.</span></span>


<span data-ttu-id="f93f2-118">[![Диалоговое окно нового проекта](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f93f2-118">[![New Project Dialog](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span></span>

<span data-ttu-id="f93f2-119">**Рис 01**: Диалоговое окно нового проекта ([Просмотр полноразмерного изображения](understanding-models-views-and-controllers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="f93f2-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image2.png))</span></span>


<span data-ttu-id="f93f2-120">При создании нового приложения ASP.NET MVC, **Создание проекта модульных тестов** откроется диалоговое окно (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="f93f2-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="f93f2-121">Это диалоговое окно позволяет создать отдельный проект в решении для тестирования приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="f93f2-122">Выберите параметр **нет, не создавать проект модульного теста** и нажмите кнопку **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f93f2-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>


<span data-ttu-id="f93f2-123">[![Создание диалогового окна модульного теста](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f93f2-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span></span>

<span data-ttu-id="f93f2-124">**Рис. 02**: Создание диалогового окна модульных тестов ([Просмотр полноразмерного изображения](understanding-models-views-and-controllers-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="f93f2-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image4.png))</span></span>


<span data-ttu-id="f93f2-125">После нового ASP.NET MVC будет создано приложение.</span><span class="sxs-lookup"><span data-stu-id="f93f2-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="f93f2-126">Вы увидите несколько папок и файлов в окне обозревателя решений.</span><span class="sxs-lookup"><span data-stu-id="f93f2-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="f93f2-127">В частности вы увидите три папки с именем модели, представления и контроллеры.</span><span class="sxs-lookup"><span data-stu-id="f93f2-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="f93f2-128">Как можно догадаться из имен папок, эти папки содержат файлы для реализации модели, представления и контроллеры.</span><span class="sxs-lookup"><span data-stu-id="f93f2-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="f93f2-129">Если развернуть папку Controllers, вы увидите файл с именем AccountController.cs и файл с именем HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="f93f2-129">If you expand the Controllers folder, you should see a file named AccountController.cs and a file named HomeController.cs.</span></span> <span data-ttu-id="f93f2-130">Если развернуть папку Views, вы увидите три вложенные папки с именем учетной записи, Главная и Shared.</span><span class="sxs-lookup"><span data-stu-id="f93f2-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="f93f2-131">Если развернуть корневой папки, вы увидите два дополнительных файла с именем About.aspx и Index.aspx (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="f93f2-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="f93f2-132">Эти файлы, составляющие пример приложения, в состав шаблона ASP.NET MVC по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f93f2-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>


<span data-ttu-id="f93f2-133">[![Окно обозревателя решений](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f93f2-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span></span>

<span data-ttu-id="f93f2-134">**Рис 03**: Окно обозревателя решений ([Просмотр полноразмерного изображения](understanding-models-views-and-controllers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f93f2-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image6.png))</span></span>


<span data-ttu-id="f93f2-135">Можно запустить его, выбрав параметр меню **отладка, начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="f93f2-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="f93f2-136">Кроме того можно нажать клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="f93f2-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="f93f2-137">При первом запуске приложения ASP.NET, откроется диалоговое окно, на рис. 4, в которое рекомендует включить режим отладки.</span><span class="sxs-lookup"><span data-stu-id="f93f2-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="f93f2-138">Нажмите кнопку "ОК", и приложение будет запущено.</span><span class="sxs-lookup"><span data-stu-id="f93f2-138">Click the OK button and the application will run.</span></span>


<span data-ttu-id="f93f2-139">[![Диалоговое окно отладки не включена](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f93f2-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span></span>

<span data-ttu-id="f93f2-140">**Рис. 04**: Отладка не включена диалоговое окно ([Просмотр полноразмерного изображения](understanding-models-views-and-controllers-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="f93f2-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image8.png))</span></span>


<span data-ttu-id="f93f2-141">При запуске приложения ASP.NET MVC, Visual Studio запускает приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="f93f2-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="f93f2-142">Пример приложения состоит из только двух страниц: страницу индекса и страницы About.</span><span class="sxs-lookup"><span data-stu-id="f93f2-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="f93f2-143">При первом запуске приложения, открытии страницы индекса (см. рис. 5).</span><span class="sxs-lookup"><span data-stu-id="f93f2-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="f93f2-144">Можно перейти на страницу About, щелкнув ссылку меню в верхней правой части приложения.</span><span class="sxs-lookup"><span data-stu-id="f93f2-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>


<span data-ttu-id="f93f2-145">[![Страница индекса](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="f93f2-145">[![The Index Page](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span></span>

<span data-ttu-id="f93f2-146">**05 рис**: Страница индекса ([Просмотр полноразмерного изображения](understanding-models-views-and-controllers-cs/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="f93f2-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image11.png))</span></span>


<span data-ttu-id="f93f2-147">Обратите внимание, что URL-адреса в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="f93f2-148">Например, при щелчке ссылки меню About URL-адрес в адресной строке браузера изменяется **/Home/About**.</span><span class="sxs-lookup"><span data-stu-id="f93f2-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="f93f2-149">Если закрыть окно браузера и вернитесь в Visual Studio, нельзя будет найти файл с домом путь/о программе.</span><span class="sxs-lookup"><span data-stu-id="f93f2-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="f93f2-150">Эти файлы не существуют.</span><span class="sxs-lookup"><span data-stu-id="f93f2-150">The files don't exist.</span></span> <span data-ttu-id="f93f2-151">Как такое возможно?</span><span class="sxs-lookup"><span data-stu-id="f93f2-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="f93f2-152">URL-адрес не является страницей</span><span class="sxs-lookup"><span data-stu-id="f93f2-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="f93f2-153">При создании традиционного приложения веб-форм ASP.NET или приложение Active Server Pages, имеется однозначное соответствие между URL-адреса и страницы.</span><span class="sxs-lookup"><span data-stu-id="f93f2-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="f93f2-154">При запросе страницы с именем SomePage.aspx с сервера, то лучше быть страницы на диск с именем SomePage.aspx.</span><span class="sxs-lookup"><span data-stu-id="f93f2-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="f93f2-155">Если файл SomePage.aspx не существует, вы получаете ужасно **404 — страница не найдена** ошибки.</span><span class="sxs-lookup"><span data-stu-id="f93f2-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="f93f2-156">При создании приложения ASP.NET MVC, напротив, нет соответствия между URL-адрес, введите в адресную строку браузера и файлы, которые можно найти в приложении.</span><span class="sxs-lookup"><span data-stu-id="f93f2-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="f93f2-157">В приложении ASP.NET MVC URL-адрес соответствует действия контроллера, а не страницу на диске.</span><span class="sxs-lookup"><span data-stu-id="f93f2-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="f93f2-158">В традиционном приложении ASP.NET и ASP запросы браузера сопоставляются страниц.</span><span class="sxs-lookup"><span data-stu-id="f93f2-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="f93f2-159">В приложении ASP.NET MVC напротив, запросы браузера сопоставляются действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="f93f2-160">Приложение веб-форм ASP.NET — ориентированных на содержимое.</span><span class="sxs-lookup"><span data-stu-id="f93f2-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="f93f2-161">Приложения ASP.NET MVC, напротив, — на логику приложения.</span><span class="sxs-lookup"><span data-stu-id="f93f2-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="f93f2-162">Сведения о маршрутизации ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f93f2-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="f93f2-163">Запрос браузера с регистрационными действие контроллера посредством компонента платформы ASP.NET, который называется *маршрутизация ASP.NET*.</span><span class="sxs-lookup"><span data-stu-id="f93f2-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="f93f2-164">Используется маршрутизация ASP.NET, платформой ASP.NET MVC для *маршрута* входящие запросы к действиям контроллера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="f93f2-165">Маршрутизация ASP.NET использует таблицу маршрутизации для обработки входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="f93f2-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="f93f2-166">Эта таблица маршрутов создается при первом запуске веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f93f2-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="f93f2-167">Таблица маршрутов — Настройка в файле Global.asax.</span><span class="sxs-lookup"><span data-stu-id="f93f2-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="f93f2-168">Файл MVC Global.asax по умолчанию содержится в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="f93f2-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="f93f2-169">**В листинге 1 - Global.asax**</span><span class="sxs-lookup"><span data-stu-id="f93f2-169">**Listing 1 - Global.asax**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

<span data-ttu-id="f93f2-170">Когда приложение ASP.NET первом запуске приложения\_вызывается метод Start().</span><span class="sxs-lookup"><span data-stu-id="f93f2-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="f93f2-171">В листинге 1 Этот метод вызывает метод RegisterRoutes() и метод RegisterRoutes() создает таблицы маршрутов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f93f2-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="f93f2-172">Таблица маршрутов по умолчанию состоит из одного маршрута.</span><span class="sxs-lookup"><span data-stu-id="f93f2-172">The default route table consists of one route.</span></span> <span data-ttu-id="f93f2-173">Этот маршрут по умолчанию разбивает все входящие запросы на три сегмента (сегмент URL-адрес — это что-то между косыми чертами).</span><span class="sxs-lookup"><span data-stu-id="f93f2-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="f93f2-174">Первый сегмент сопоставляется имя контроллера, второй сегмент сопоставляется имени действия и последний сегмент сопоставляется с параметром, который передается в действие с именем Id.</span><span class="sxs-lookup"><span data-stu-id="f93f2-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="f93f2-175">Например, рассмотрим следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="f93f2-175">For example, consider the following URL:</span></span>

<span data-ttu-id="f93f2-176">/ Продукта/сведения/3</span><span class="sxs-lookup"><span data-stu-id="f93f2-176">/Product/Details/3</span></span>

<span data-ttu-id="f93f2-177">Этот URL-адрес преобразуется в три параметра следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f93f2-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="f93f2-178">Контроллер = продукт</span><span class="sxs-lookup"><span data-stu-id="f93f2-178">Controller = Product</span></span>

<span data-ttu-id="f93f2-179">Действие — подробности</span><span class="sxs-lookup"><span data-stu-id="f93f2-179">Action = Details</span></span>

<span data-ttu-id="f93f2-180">идентификатор = 3</span><span class="sxs-lookup"><span data-stu-id="f93f2-180">Id = 3</span></span>

<span data-ttu-id="f93f2-181">Маршрут по умолчанию, определенные в файле Global.asax содержит значения по умолчанию для всех трех параметров.</span><span class="sxs-lookup"><span data-stu-id="f93f2-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="f93f2-182">По умолчанию контроллера Home, действие по умолчанию используется индекс, а идентификатор по умолчанию является пустой строкой.</span><span class="sxs-lookup"><span data-stu-id="f93f2-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="f93f2-183">Эти значения по умолчанию в виду рассмотрите как следующий URL-адрес анализируется:</span><span class="sxs-lookup"><span data-stu-id="f93f2-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="f93f2-184">Сотрудник —</span><span class="sxs-lookup"><span data-stu-id="f93f2-184">/Employee</span></span>

<span data-ttu-id="f93f2-185">Этот URL-адрес преобразуется в три параметра следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f93f2-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="f93f2-186">Контроллер = сотрудника</span><span class="sxs-lookup"><span data-stu-id="f93f2-186">Controller = Employee</span></span>

<span data-ttu-id="f93f2-187">Действие = индекс</span><span class="sxs-lookup"><span data-stu-id="f93f2-187">Action = Index</span></span>

<span data-ttu-id="f93f2-188">Id = </span><span class="sxs-lookup"><span data-stu-id="f93f2-188">Id = ��</span></span>

<span data-ttu-id="f93f2-189">Наконец Если открыть приложения ASP.NET MVC, не указав любой URL-адрес (например, `http://localhost`) URL-адрес разбивается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f93f2-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="f93f2-190">контроллер = Home</span><span class="sxs-lookup"><span data-stu-id="f93f2-190">Controller = Home</span></span>

<span data-ttu-id="f93f2-191">Действие = индекс</span><span class="sxs-lookup"><span data-stu-id="f93f2-191">Action = Index</span></span>

<span data-ttu-id="f93f2-192">Id = </span><span class="sxs-lookup"><span data-stu-id="f93f2-192">Id = ��</span></span>

<span data-ttu-id="f93f2-193">Запрос перенаправляется к действию Index() класса HomeController.</span><span class="sxs-lookup"><span data-stu-id="f93f2-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="f93f2-194">Общее представление о контроллерах</span><span class="sxs-lookup"><span data-stu-id="f93f2-194">Understanding Controllers</span></span>

<span data-ttu-id="f93f2-195">Контроллер отвечает за управление способ, которым пользователь взаимодействует с MVC-приложениях.</span><span class="sxs-lookup"><span data-stu-id="f93f2-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="f93f2-196">Контроллер содержит логику управления потоком для приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="f93f2-197">Контроллер определяет, какой ответ для отправки обратно пользователю, когда пользователь делает запрос браузера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="f93f2-198">Контроллер — это класс (например, класс Visual Basic или C#).</span><span class="sxs-lookup"><span data-stu-id="f93f2-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="f93f2-199">Пример приложения ASP.NET MVC включает контроллер с именем HomeController.cs, расположенный в папке Controllers.</span><span class="sxs-lookup"><span data-stu-id="f93f2-199">The sample ASP.NET MVC application includes a controller named HomeController.cs located in the Controllers folder.</span></span> <span data-ttu-id="f93f2-200">Содержимое файла HomeController.cs будет воспроизведено в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="f93f2-200">The content of the HomeController.cs file is reproduced in Listing 2.</span></span>

<span data-ttu-id="f93f2-201">**В листинге 2 - HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="f93f2-201">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

<span data-ttu-id="f93f2-202">Обратите внимание на то, что HomeController имеет два метода с именем Index() и About().</span><span class="sxs-lookup"><span data-stu-id="f93f2-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="f93f2-203">Эти два метода соответствуют два действия, предоставляемые контроллером.</span><span class="sxs-lookup"><span data-stu-id="f93f2-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="f93f2-204">URL-адрес/Home/Index вызывает метод HomeController.Index() и URL-адрес/Home/About вызывает метод HomeController.About().</span><span class="sxs-lookup"><span data-stu-id="f93f2-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="f93f2-205">Любой открытый метод в контроллере указывается в виде действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="f93f2-206">Необходимо соблюдать осторожность, об этом.</span><span class="sxs-lookup"><span data-stu-id="f93f2-206">You need to be careful about this.</span></span> <span data-ttu-id="f93f2-207">Это означает, что любой открытый метод, содержащихся в контроллере может быть вызван любым пользователем, имеющим доступ к Интернету, введя правой URL-адрес в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="f93f2-208">Общие сведения о представлениях</span><span class="sxs-lookup"><span data-stu-id="f93f2-208">Understanding Views</span></span>

<span data-ttu-id="f93f2-209">Два контроллера действия, предоставляемые классом HomeController, Index() и About(), как вернуть представление.</span><span class="sxs-lookup"><span data-stu-id="f93f2-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="f93f2-210">Представление содержит HTML-разметка и содержимое, отправляемое в браузер.</span><span class="sxs-lookup"><span data-stu-id="f93f2-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="f93f2-211">Представление является эквивалентом страницы, при работе с приложением ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f93f2-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="f93f2-212">Необходимо создать свои представления в нужных местах.</span><span class="sxs-lookup"><span data-stu-id="f93f2-212">You must create your views in the right location.</span></span> <span data-ttu-id="f93f2-213">HomeController.Index() действие возвращает представление, расположенный по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="f93f2-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="f93f2-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="f93f2-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="f93f2-215">HomeController.About() действие возвращает представление, расположенный по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="f93f2-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="f93f2-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="f93f2-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="f93f2-217">Как правило если вы хотите вернуть представление для действия контроллера, затем необходимо создать вложенную папку в папке Views с тем же именем, что и контроллер.</span><span class="sxs-lookup"><span data-stu-id="f93f2-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="f93f2-218">В папке необходимо создать ASPX-файл с тем же именем, что действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="f93f2-219">Этот файл в листинге 3 содержит представление About.aspx.</span><span class="sxs-lookup"><span data-stu-id="f93f2-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="f93f2-220">**Листинг 3 - About.aspx**</span><span class="sxs-lookup"><span data-stu-id="f93f2-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

<span data-ttu-id="f93f2-221">Если сейчас пропустить первой строки в листинге 3, большая часть rest представления состоит из стандартный HTML.</span><span class="sxs-lookup"><span data-stu-id="f93f2-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="f93f2-222">Содержимое представления можно изменить, указав любой код HTML, который здесь.</span><span class="sxs-lookup"><span data-stu-id="f93f2-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="f93f2-223">Представление — очень похожа на страницу в ASP-страницы или веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f93f2-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="f93f2-224">Представление может содержать HTML-содержимого и скрипты.</span><span class="sxs-lookup"><span data-stu-id="f93f2-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="f93f2-225">Можно создавать скрипты в своего любимого .NET язык (например, C# или Visual Basic .NET).</span><span class="sxs-lookup"><span data-stu-id="f93f2-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="f93f2-226">Использовать сценарии для отображения динамического содержимого, таких как базы данных.</span><span class="sxs-lookup"><span data-stu-id="f93f2-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="f93f2-227">Общие сведения о моделях</span><span class="sxs-lookup"><span data-stu-id="f93f2-227">Understanding Models</span></span>

<span data-ttu-id="f93f2-228">Было рассмотрено, контроллеры и представления было рассмотрено.</span><span class="sxs-lookup"><span data-stu-id="f93f2-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="f93f2-229">Последний вопрос, мы должны говорить о составляют модели.</span><span class="sxs-lookup"><span data-stu-id="f93f2-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="f93f2-230">Что такое модель MVC?</span><span class="sxs-lookup"><span data-stu-id="f93f2-230">What is an MVC model?</span></span>

<span data-ttu-id="f93f2-231">Модель MVC содержит все логики приложения, не содержится в контроллере или представления.</span><span class="sxs-lookup"><span data-stu-id="f93f2-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="f93f2-232">Модели должен содержать все ваши бизнес-логики приложения, логику проверки и логики доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="f93f2-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="f93f2-233">Например если вы используете Microsoft Entity Framework для доступа к базе данных, бы создать классы платформы Entity Framework (EDMX-файл) в папке Models.</span><span class="sxs-lookup"><span data-stu-id="f93f2-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="f93f2-234">Представления должен содержать только логику, связанные с созданием пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f93f2-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="f93f2-235">Контроллер должен содержать только минимальные логику, необходимую для возвращения правильное представление или перенаправить пользователя в другое действие (Управление потоком).</span><span class="sxs-lookup"><span data-stu-id="f93f2-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="f93f2-236">Все остальное должно содержаться в модели.</span><span class="sxs-lookup"><span data-stu-id="f93f2-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="f93f2-237">В общем случае следует стремиться fat моделей и небольшой контроллеров.</span><span class="sxs-lookup"><span data-stu-id="f93f2-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="f93f2-238">Методы контроллера должны содержать всего несколько строк кода.</span><span class="sxs-lookup"><span data-stu-id="f93f2-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="f93f2-239">Если действие контроллера получает слишком fat, затем следует перемещать логику в новый класс в папке Models.</span><span class="sxs-lookup"><span data-stu-id="f93f2-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="f93f2-240">Сводка</span><span class="sxs-lookup"><span data-stu-id="f93f2-240">Summary</span></span>

<span data-ttu-id="f93f2-241">Это руководство предоставляет вам общий обзор различных частей ASP.NET MVC веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f93f2-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="f93f2-242">Вы узнали, как маршрутизация ASP.NET сопоставляет входящий запрос браузера к действиям конкретного контроллера.</span><span class="sxs-lookup"><span data-stu-id="f93f2-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="f93f2-243">Вы узнали, как контроллеры координировать как представления возвращаются в браузер.</span><span class="sxs-lookup"><span data-stu-id="f93f2-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="f93f2-244">Наконец вы узнали, как модели содержат application business, проверки и логики доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="f93f2-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>