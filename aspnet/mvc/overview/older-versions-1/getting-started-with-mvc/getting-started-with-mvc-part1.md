---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: Введение в ASP.NET MVC | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основные сведения по ASP.NET MVC. Создание простого веб-приложения, которое считывает и записывает в базу данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: dcc2e703829cfa0b77575870feff451fd0738f56
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59416497"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="ec0e8-104">Введение в ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ec0e8-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="ec0e8-105">по [(Scott hanselman)](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="ec0e8-106">Обновленную версию, если это руководство доступно [здесь](../../getting-started/introduction/getting-started.md) с помощью [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span><span class="sxs-lookup"><span data-stu-id="ec0e8-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="ec0e8-107">Новое учебное использует ASP.NET MVC 5, который содержит множество улучшений на этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="ec0e8-108">Это руководство для начинающих, в котором представлены основные сведения по ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="ec0e8-109">Вы создадите простое веб-приложение, которое считывает и записывает в базу данных.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="ec0e8-110">Посетите [центр обучения ASP.NET MVC](../../../index.md) для поиска других ASP.NET MVC, учебники и примеры.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="ec0e8-111">Создадим наш первый веб-приложение ASP.NET MVC с помощью [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="ec0e8-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="ec0e8-112">Сделаем небольшое приложение списка фильмов, сообщите нам создать и список фильмов.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="ec0e8-113">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="ec0e8-113">What You'll Build</span></span>

<span data-ttu-id="ec0e8-114">Ниже приведены два снимка экрана приложения, который вам предстоит создать.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="ec0e8-115">Вы получите простую таблицу фильмов с помощью различных столбцов.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="ec0e8-116">[![Список фильмов - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="ec0e8-117">И вы получите Создание формы, поэтому мы можем добавить в список фильмов.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="ec0e8-118">[![Создайте фильм - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="ec0e8-119">Навыки, которые вы узнаете</span><span class="sxs-lookup"><span data-stu-id="ec0e8-119">Skills You'll Learn</span></span>

<span data-ttu-id="ec0e8-120">Этом учебнике описываются основы создания веб-приложение ASP.NET MVC с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="ec0e8-121">Вы узнаете следующее.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-121">You'll learn:</span></span>

- <span data-ttu-id="ec0e8-122">Как создать новый проект ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ec0e8-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="ec0e8-123">Как создать новую базу данных с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="ec0e8-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="ec0e8-124">Как создать ASP.NET MVC контроллеры и представления</span><span class="sxs-lookup"><span data-stu-id="ec0e8-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="ec0e8-125">Получение и отображение данных</span><span class="sxs-lookup"><span data-stu-id="ec0e8-125">How to retrieve and display data</span></span>
- <span data-ttu-id="ec0e8-126">Включение проверки данных и изменения данных</span><span class="sxs-lookup"><span data-stu-id="ec0e8-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="ec0e8-127">Как обновить схему базы данных</span><span class="sxs-lookup"><span data-stu-id="ec0e8-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="ec0e8-128">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="ec0e8-128">Get Started</span></span>

<span data-ttu-id="ec0e8-129">Запустить Visual Web Developer 2010 Express (назовем ее «VWD» теперь) и выберите новый проект из на начальном экране.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="ec0e8-130">Visual Web Developer — это интегрированная среда разработки, или интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="ec0e8-131">Так же, как использовать Microsoft Word для записи документов, вы используете интегрированную среду разработки для создания приложений.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="ec0e8-132">Панель инструментов в верхней, отображаются различные параметры, доступные для вас, а также меню, вы также использовали выберите файл | Новый проект.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="ec0e8-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="ec0e8-134">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="ec0e8-134">Creating Your First Application</span></span>

<span data-ttu-id="ec0e8-135">Можно создавать приложения с помощью Visual Basic или Visual C#.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="ec0e8-136">Теперь выберите Visual C# с левой стороны экрана выберите «Веб-приложение ASP.NET MVC 2».</span><span class="sxs-lookup"><span data-stu-id="ec0e8-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="ec0e8-137">Присвойте проекту имя «Movies» и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="ec0e8-138">[![Новый проект](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="ec0e8-139">В области справа находится обозреватель решений, отображаются все файлы и папки в приложении.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="ec0e8-140">Большие окна в середине — изменения кода и большую часть времени.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="ec0e8-141">Visual Studio используется шаблон по умолчанию для проекта ASP.NET MVC, который вы только что создали, поэтому у вас есть рабочее приложение прямо сейчас не выполняя никаких действий!</span><span class="sxs-lookup"><span data-stu-id="ec0e8-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="ec0e8-142">Это связано с простых «Hello World!</span><span class="sxs-lookup"><span data-stu-id="ec0e8-142">This is a simple "Hello World!</span></span> <span data-ttu-id="ec0e8-143">проект и является хорошей отправной точкой для нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="ec0e8-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="ec0e8-145">Нажмите кнопку «Воспроизвести» на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-145">Select the "play" button to the toolbar.</span></span>

![Начало отладки](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="ec0e8-147">Это зеленая стрелка, указывающая вправо, будет выполняться компиляция программы и запустить приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="ec0e8-148">*ПРИМЕЧАНИЕ. Вместо этого можно нажмите клавишу F5 на клавиатуре или выберите "Отладка" -&gt;запуск отладки из меню «Отладка».*</span><span class="sxs-lookup"><span data-stu-id="ec0e8-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="ec0e8-149">Это приведет к Visual Web Developer для запуска веб сервера разработки и выполнения нашего веб-приложения (не существует конфигурации или ручного действия, необходимые для этого).</span><span class="sxs-lookup"><span data-stu-id="ec0e8-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="ec0e8-150">Затем он запустит браузер и настроить его для просмотра домашней страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="ec0e8-151">Обратите внимание, что ниже говорит что адресной строке браузера «localhost», а не что-то вида example.com.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="ec0e8-152">Том, что localhost всегда указывает на локальном компьютере — в этом случае работающего приложения, которые мы только что создали.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="ec0e8-153">[![Домашняя страница](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="ec0e8-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="ec0e8-154">По умолчанию этот шаблон по умолчанию дает вам две страницы посетить и страницу основное имя для входа.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="ec0e8-155">Давайте изменить работу этого приложения и немного поговорим об ASP.NET MVC в процессе.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="ec0e8-156">Закройте обозреватель и позволяет изменить часть кода.</span><span class="sxs-lookup"><span data-stu-id="ec0e8-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ec0e8-157">Вперед</span><span class="sxs-lookup"><span data-stu-id="ec0e8-157">Next</span></span>](getting-started-with-mvc-part2.md)
