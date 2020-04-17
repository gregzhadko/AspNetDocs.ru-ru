---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Создание нового проекта MVC ASP.NET (ru) Документы Майкрософт
author: rick-anderson
description: Шаг 1 показывает, как поставить основную структуру приложения NerdDinner на месте.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541485"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="f6035-103">Создание проекта ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f6035-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="f6035-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f6035-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f6035-105">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="f6035-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f6035-106">Это шаг 1 [бесплатного "NerdDinner" приложение учебник,](introducing-the-nerddinner-tutorial.md) который ходит через как построить небольшой, но полный, веб-приложение с помощью ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="f6035-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f6035-107">Шаг 1 показывает, как поставить основную структуру приложения NerdDinner на месте.</span><span class="sxs-lookup"><span data-stu-id="f6035-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="f6035-108">Если вы используете ASP.NET MVC 3, мы рекомендуем вам следовать [начиная с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.</span><span class="sxs-lookup"><span data-stu-id="f6035-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="f6035-109">NerdУжин Шаг 1:&gt;Файл-Новый проект</span><span class="sxs-lookup"><span data-stu-id="f6035-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="f6035-110">Мы начнем наше приложение NerdDinner, выбрав **файл-новый&gt;** пункт меню проекта в рамках либо Visual Studio 2008 или бесплатный визуальный веб-разработчик 2008 Express.</span><span class="sxs-lookup"><span data-stu-id="f6035-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="f6035-111">Это позволит поднять диалог "Новый проект".</span><span class="sxs-lookup"><span data-stu-id="f6035-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="f6035-112">Для создания нового приложения mVC ASP.NET мы выберем узел "Web" на левой стороне диалога, а затем выберем шаблон проекта "ASP.NET MVC Web Application" справа:</span><span class="sxs-lookup"><span data-stu-id="f6035-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="f6035-113">*Важно: Убедитесь, что вы скачали и установили ASP.NET MVC - в противном случае он не будет отображаться в диалоге нового проекта. Вы можете использовать V2 [установки веб-платформы Microsoft,](https://www.microsoft.com/web/downloads/platform.aspx) если вы еще не установили его&gt;(ASP.NET MVC доступен в разделе "Веб-платформа- и Runtimes").*</span><span class="sxs-lookup"><span data-stu-id="f6035-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="f6035-114">Мы назовем новый проект, который мы собираемся создать "NerdDinner", а затем нажмите кнопку "ОК", чтобы создать его.</span><span class="sxs-lookup"><span data-stu-id="f6035-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="f6035-115">При нажатии кнопки "ОК" Visual Studio будет воспитывать дополнительный диалог, который побуждает нас дополнительно создать модульный проект тестирования для нового приложения, а также.</span><span class="sxs-lookup"><span data-stu-id="f6035-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="f6035-116">Этот модульный проект тестирования позволяет нам создавать автоматизированные тесты, которые проверяют функциональность и поведение нашего приложения (что-то, что мы рассмотрим, как сделать позже в этом учебнике).</span><span class="sxs-lookup"><span data-stu-id="f6035-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="f6035-117">Выпадение "Тестовой рамки" в вышеуказанном диалоге наполнено всеми доступными ASP.NET шаблонами тестового проекта MVC, установленными на машине.</span><span class="sxs-lookup"><span data-stu-id="f6035-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="f6035-118">Версии можно загрузить для NUnit, MBUnit и XUnit.</span><span class="sxs-lookup"><span data-stu-id="f6035-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="f6035-119">Также поддерживается встроенная платформа Visual Studio Unit Test.</span><span class="sxs-lookup"><span data-stu-id="f6035-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="f6035-120">*Примечание: Visual Studio Unit Test Framework доступна только с Visual Studio 2008 Профессиональные и более высокие версии. Если вы используете VS 2008 Standard Edition или Visual Web Developer 2008 Express, вам нужно будет загрузить и установить расширения NUnit, MBUnit или XUnit для ASP.NET MVC для того, чтобы этот диалог был показан. Диалог не будет отображаться, если нет установленных тестовых рамок.*</span><span class="sxs-lookup"><span data-stu-id="f6035-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="f6035-121">Мы будем использовать значение "NerdDinner.Tests" для тестового проекта, который мы создаем, и используем опцию "Visual Studio Unit Test".</span><span class="sxs-lookup"><span data-stu-id="f6035-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="f6035-122">При нажатии кнопки "ОК" Visual Studio создадим для нас решение с двумя проектами - один для нашего веб-приложения и один для наших модульных тестов:</span><span class="sxs-lookup"><span data-stu-id="f6035-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="f6035-123">Изучение структуры каталога NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f6035-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="f6035-124">При создании нового приложения mVC ASP.NET с помощью Visual Studio он автоматически добавляет в проект ряд файлов и каталогов:</span><span class="sxs-lookup"><span data-stu-id="f6035-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="f6035-125">ASP.NET проектов MVC по умолчанию имеют шесть каталогов верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="f6035-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="f6035-126">**Каталог**</span><span class="sxs-lookup"><span data-stu-id="f6035-126">**Directory**</span></span> | <span data-ttu-id="f6035-127">**Цель**</span><span class="sxs-lookup"><span data-stu-id="f6035-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="f6035-128">**/Контролеры**</span><span class="sxs-lookup"><span data-stu-id="f6035-128">**/Controllers**</span></span> | <span data-ttu-id="f6035-129">Где размещаться классы контроллера, обрабатывающие запросы URL</span><span class="sxs-lookup"><span data-stu-id="f6035-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="f6035-130">**/Модели**</span><span class="sxs-lookup"><span data-stu-id="f6035-130">**/Models**</span></span> | <span data-ttu-id="f6035-131">Где вы размещаете классы, представляющие и манипулируют данными</span><span class="sxs-lookup"><span data-stu-id="f6035-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="f6035-132">**/Виды**</span><span class="sxs-lookup"><span data-stu-id="f6035-132">**/Views**</span></span> | <span data-ttu-id="f6035-133">Где размещаются файлы шаблонов uI, ответственные за визуализацию вывода</span><span class="sxs-lookup"><span data-stu-id="f6035-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="f6035-134">**/Сценарии**</span><span class="sxs-lookup"><span data-stu-id="f6035-134">**/Scripts**</span></span> | <span data-ttu-id="f6035-135">Где вы размещаете файлы библиотеки JavaScript и скрипты (.js)</span><span class="sxs-lookup"><span data-stu-id="f6035-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="f6035-136">**/Содержание**</span><span class="sxs-lookup"><span data-stu-id="f6035-136">**/Content**</span></span> | <span data-ttu-id="f6035-137">Где вы размещаете CSS и файлы изображений, а также другое нединамическое/не-JavaScript-содержимое</span><span class="sxs-lookup"><span data-stu-id="f6035-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="f6035-138">**/Данные приложения\_**</span><span class="sxs-lookup"><span data-stu-id="f6035-138">**/App\_Data**</span></span> | <span data-ttu-id="f6035-139">Где вы храните файлы данных, которые вы хотите читать/писать.</span><span class="sxs-lookup"><span data-stu-id="f6035-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="f6035-140">ASP.NET MVC не требует такой структуры.</span><span class="sxs-lookup"><span data-stu-id="f6035-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="f6035-141">На самом деле, разработчики, работающие над большими приложениями, обычно разбирают приложение на несколько проектов, чтобы сделать его более управляемым (например: классы моделей данных часто идут в отдельный проект библиотеки класса из веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="f6035-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="f6035-142">Структура проекта по умолчанию, однако, обеспечивает хорошую конвенцию каталога по умолчанию, которую мы можем использовать, чтобы держать наши проблемы приложений в чистоте.</span><span class="sxs-lookup"><span data-stu-id="f6035-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="f6035-143">Когда мы расширим каталог /Controllers, мы обнаружим, что Visual Studio добавила два класса контроллера - HomeController и AccountController - по умолчанию к проекту:</span><span class="sxs-lookup"><span data-stu-id="f6035-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="f6035-144">Когда мы расширим каталог /Views, мы найдем три подкаталога - /Home, /Account и /Shared - а также несколько файлов шаблонов внутри них также были добавлены в проект по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="f6035-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="f6035-145">Расширяя каталоги /Content и /Scripts, мы найдем файл Site.css, который используется для стиля всех HTML на сайте, а также библиотеки JavaScript, которые могут включить ASP.NET поддержку AJAX и j'ery в приложении:</span><span class="sxs-lookup"><span data-stu-id="f6035-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="f6035-146">Когда мы расширим проект NerdDinner.Tests, мы найдем два класса, которые содержат модульные тесты для наших классов контроллеров:</span><span class="sxs-lookup"><span data-stu-id="f6035-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="f6035-147">Эти файлы по умолчанию, добавленные Visual Studio, предоставляют нам базовую структуру для рабочего приложения - в комплекте с домашней страницей, страницой о странице, страницей входа в учетную запись/регистрацией и страницей ошибки без обработки (все проводные и работающие из коробки).</span><span class="sxs-lookup"><span data-stu-id="f6035-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="f6035-148">Запуск приложения NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f6035-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="f6035-149">Мы можем запустить проект, выбрав либо **Debug-&gt;Start Debugging,** либо **debug-&gt;Start без отладки** элементов меню:</span><span class="sxs-lookup"><span data-stu-id="f6035-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="f6035-150">Это позволит запустить встроенный ASP.NET веб-сервер, который поставляется с Visual Studio, и запустить наше приложение:</span><span class="sxs-lookup"><span data-stu-id="f6035-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="f6035-151">Ниже приводится главная страница для нашего нового проекта (URL: "/"), когда он работает:</span><span class="sxs-lookup"><span data-stu-id="f6035-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="f6035-152">На жапке "О" отображается страница (URL: "/Home/About"):</span><span class="sxs-lookup"><span data-stu-id="f6035-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="f6035-153">Нажав на ссылку "Войти в прямой справа" нас на страницу входа (URL: "/Account/LogOn")</span><span class="sxs-lookup"><span data-stu-id="f6035-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="f6035-154">Если у нас нет учетной записи входа, мы можем нажать на ссылку регистра (URL: "/Account/Register"), чтобы создать ее:</span><span class="sxs-lookup"><span data-stu-id="f6035-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="f6035-155">Код для реализации вышеупомянутого домашнего, о, и выхода / регистрации функциональность была добавлена по умолчанию, когда мы создали наш новый проект.</span><span class="sxs-lookup"><span data-stu-id="f6035-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="f6035-156">Мы будем использовать его в качестве отправной точки нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f6035-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="f6035-157">Тестирование приложения NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f6035-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="f6035-158">Если мы используем Профессиональное издание или более высокую версию Visual Studio 2008, мы можем использовать встроенную поддержку IDE-тестирования подразделения для тестирования проекта:</span><span class="sxs-lookup"><span data-stu-id="f6035-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="f6035-159">Выбор одного из вышеперечисленных вариантов откроет панель "Результаты испытаний" в рамках IDE и предоставит нам статус прохода/неудачи на 27 модульных тестах, включенных в наш новый проект, охватывающий встроенную функциональность:</span><span class="sxs-lookup"><span data-stu-id="f6035-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="f6035-160">Позже в этом учебнике мы поговорим больше об автоматизированном тестировании и добавим дополнительные модульные тесты, которые охватывают функциональность приложения, которую мы реализуем.</span><span class="sxs-lookup"><span data-stu-id="f6035-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="f6035-161">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="f6035-161">Next Step</span></span>

<span data-ttu-id="f6035-162">Теперь у нас есть базовая структура приложения на месте.</span><span class="sxs-lookup"><span data-stu-id="f6035-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="f6035-163">Давайте [создадим базу данных для хранения данных приложения.](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="f6035-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f6035-164">[Назад](introducing-the-nerddinner-tutorial.md)
> [Вперед](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="f6035-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
