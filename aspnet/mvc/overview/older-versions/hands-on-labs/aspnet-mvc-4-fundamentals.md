---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: Основы ASP.NET MVC 4 | Документация Майкрософт
author: rick-anderson
description: Эта практическая лабораторная работа основана на музыкальном магазине MVC (контроллер представления модели), в котором представлено пошаговое руководство, в котором описывается, как использовать ASP.NET MV...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484572"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="b648e-103">Основы ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b648e-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="b648e-104">по [веб-Camp командам](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b648e-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b648e-105">Скачать обучающий комплект Web Camp</span><span class="sxs-lookup"><span data-stu-id="b648e-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="b648e-106">Эта практическая лабораторная работа основана на музыкальном магазине MVC (контроллер представления модели), в котором представлено пошаговое руководство, в котором описывается, как использовать ASP.NET MVC и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="b648e-107">В ходе лабораторной работы вы узнаете простоту, а также возможности использования этих технологий вместе.</span><span class="sxs-lookup"><span data-stu-id="b648e-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="b648e-108">Вы начнете с простого приложения и начнете его сборку, пока не будет полностью функциональным веб-приложением ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b648e-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="b648e-109">Эта лабораторная работа работает с ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b648e-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="b648e-110">Если вы хотите изучить версию учебного приложения ASP.NET MVC 3, ее можно найти в [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="b648e-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="b648e-111">В этой практической лабораторной работе предполагается, что у разработчика есть опыт работы с веб-разработками, например HTML и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b648e-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="b648e-112">Все примеры кода и фрагментов включены в набор средств для обучения Web Camp, доступный в [выпусках Microsoft-Web/вебкамптраинингкит](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="b648e-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="b648e-113">Проект, относящийся к этой лабораторной работе, доступен по [принципу ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span><span class="sxs-lookup"><span data-stu-id="b648e-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="b648e-114">Приложение музыкального магазина</span><span class="sxs-lookup"><span data-stu-id="b648e-114">The Music Store application</span></span>

<span data-ttu-id="b648e-115">Веб-приложение музыкального магазина, которое будет построено в рамках этой лабораторной работы, состоит из трех основных частей: покупки, извлечения и администрирования.</span><span class="sxs-lookup"><span data-stu-id="b648e-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="b648e-116">Посетители смогут просматривать альбомы по жанрам, добавлять в них альбомы, просматривать их выбор и, наконец, продолжить их извлечение для входа и выполнить заказ.</span><span class="sxs-lookup"><span data-stu-id="b648e-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="b648e-117">Кроме того, Администраторы хранилища смогут управлять доступными альбомами, а также их основными свойствами.</span><span class="sxs-lookup"><span data-stu-id="b648e-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="b648e-118">![Экраны музыкального хранилища](aspnet-mvc-4-fundamentals/_static/image1.png "Экраны музыкального хранилища")</span><span class="sxs-lookup"><span data-stu-id="b648e-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="b648e-119">*Экраны музыкального хранилища*</span><span class="sxs-lookup"><span data-stu-id="b648e-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="b648e-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="b648e-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="b648e-121">Приложение музыкального магазина будет создано с использованием **контроллера представления модели (MVC)** , шаблон архитектуры, который разделяет приложение на три основных компонента:</span><span class="sxs-lookup"><span data-stu-id="b648e-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="b648e-122">**Модели**: объекты модели — это части приложения, которые реализуют логику предметной области.</span><span class="sxs-lookup"><span data-stu-id="b648e-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="b648e-123">Часто объекты модели также извлекают и хранят состояние модели в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b648e-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="b648e-124">**Представления:** Представления — это компоненты, отображающие пользовательский интерфейс приложения.</span><span class="sxs-lookup"><span data-stu-id="b648e-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="b648e-125">Пользовательский интерфейс обычно создается на основе данных модели.</span><span class="sxs-lookup"><span data-stu-id="b648e-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="b648e-126">В качестве примера можно привести представление для редактирования альбомов, в котором отображаются текстовые поля и раскрывающийся список, основанный на текущем состоянии объекта альбома.</span><span class="sxs-lookup"><span data-stu-id="b648e-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="b648e-127">**Контроллеры:** Контроллеры — это компоненты, которые управляют взаимодействием с пользователем, используют модель и в конечном итоге выбирают представление для отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b648e-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="b648e-128">В приложении MVC представление служит только для отображения информации. Обработку введенных данных, формирование ответа и взаимодействие с пользователем обеспечивает контроллер.</span><span class="sxs-lookup"><span data-stu-id="b648e-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="b648e-129">Шаблон MVC помогает создавать приложения, которые отделяют различные аспекты приложения (логику ввода, бизнес-логику и логику пользовательского интерфейса), обеспечивая слабую связь между этими элементами.</span><span class="sxs-lookup"><span data-stu-id="b648e-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="b648e-130">Это разделение помогает управлять сложностью при создании приложения, так как оно позволяет сосредоточиться на одном аспекте реализации за раз.</span><span class="sxs-lookup"><span data-stu-id="b648e-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="b648e-131">Кроме того, шаблон MVC упрощает тестирование приложений, а также позволяет использовать разработку на основе тестирования (TDD) для создания приложений.</span><span class="sxs-lookup"><span data-stu-id="b648e-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="b648e-132">Платформа **ASP.NET MVC** предоставляет альтернативу шаблону веб-форм ASP.NET для создания веб-приложений на основе MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b648e-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="b648e-133">**ASP.NET MVC** Framework — это упрощенная, хорошо тестируемая платформа для презентаций, которая (как и в приложениях на основе веб-форм) интегрирована с существующими функциями ASP.NET, такими как главные страницы и аутентификация на основе членства, чтобы вы могли получить всю мощь основной платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b648e-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="b648e-134">Это полезно, если вы уже знакомы с ASP.NET Web Forms, так как все уже используемые библиотеки доступны в ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b648e-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="b648e-135">Кроме того, слабая связь между тремя основными компонентами приложения MVC также способствует параллельной разработке.</span><span class="sxs-lookup"><span data-stu-id="b648e-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="b648e-136">Например, один разработчик может работать с представлением, второй разработчик может работать с логикой контроллера, а третий разработчик может сосредоточиться на бизнес-логике в модели.</span><span class="sxs-lookup"><span data-stu-id="b648e-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b648e-137">Цели</span><span class="sxs-lookup"><span data-stu-id="b648e-137">Objectives</span></span>

<span data-ttu-id="b648e-138">В этой практической лабораторной работе вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b648e-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="b648e-139">Создание приложения ASP.NET MVC с нуля на основе учебника по приложениям музыкального магазина</span><span class="sxs-lookup"><span data-stu-id="b648e-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="b648e-140">Добавление контроллеров для обработки URL-адресов на домашней странице сайта и для обзора основных функций</span><span class="sxs-lookup"><span data-stu-id="b648e-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="b648e-141">Добавление представления для настройки отображаемого содержимого вместе с его стилем</span><span class="sxs-lookup"><span data-stu-id="b648e-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="b648e-142">Добавление классов модели для хранения и управления данными и логикой предметной области</span><span class="sxs-lookup"><span data-stu-id="b648e-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="b648e-143">Использование шаблона представления модели для передачи сведений из действий контроллера в шаблоны представлений</span><span class="sxs-lookup"><span data-stu-id="b648e-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="b648e-144">Изучите новый шаблон ASP.NET MVC 4 для Интернет приложений</span><span class="sxs-lookup"><span data-stu-id="b648e-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b648e-145">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b648e-145">Prerequisites</span></span>

<span data-ttu-id="b648e-146">Для выполнения этой лабораторной работы необходимо иметь следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="b648e-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="b648e-147">[Visual Studio 2012 Express для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (Дополнительные сведения об установке см. в [приложении A](#AppendixA) )</span><span class="sxs-lookup"><span data-stu-id="b648e-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b648e-148">Настройка</span><span class="sxs-lookup"><span data-stu-id="b648e-148">Setup</span></span>

<span data-ttu-id="b648e-149">**Установка фрагментов кода**</span><span class="sxs-lookup"><span data-stu-id="b648e-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="b648e-150">Для удобства большая часть кода, который вы будете управлять в этой лаборатории, доступна в виде фрагментов кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="b648e-151">Чтобы установить фрагменты кода, запустите файл **.\саурце\сетуп\кодесниппетс.ВСИ** .</span><span class="sxs-lookup"><span data-stu-id="b648e-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="b648e-152">Если вы не знакомы с фрагментами кода Visual Studio Code и хотите узнать, как их использовать, см. приложение в этом документе &quot;[приложении C: использование фрагментов кода](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="b648e-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b648e-153">Полнят</span><span class="sxs-lookup"><span data-stu-id="b648e-153">Exercises</span></span>

<span data-ttu-id="b648e-154">Эта практическая лабораторная работа состоит из следующих упражнений:</span><span class="sxs-lookup"><span data-stu-id="b648e-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="b648e-155">Упражнение 1. Создание проекта веб-приложения Мусиксторе ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b648e-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="b648e-156">Упражнение 2. Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="b648e-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="b648e-157">Упражнение 3. Передача параметров в контроллер</span><span class="sxs-lookup"><span data-stu-id="b648e-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="b648e-158">Упражнение 4. Создание представления</span><span class="sxs-lookup"><span data-stu-id="b648e-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="b648e-159">Упражнение 5. Создание модели представления</span><span class="sxs-lookup"><span data-stu-id="b648e-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="b648e-160">Упражнение 6. Использование параметров в представлении</span><span class="sxs-lookup"><span data-stu-id="b648e-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="b648e-161">Упражнение 7. Создание шаблона на основе ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b648e-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="b648e-162">Каждое упражнение сопровождается **конечной** папкой, содержащей итоговое решение, которое следует получить после завершения упражнений.</span><span class="sxs-lookup"><span data-stu-id="b648e-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="b648e-163">Это решение можно использовать в качестве инструкции, если вам нужна дополнительная помощь по работе с упражнениями.</span><span class="sxs-lookup"><span data-stu-id="b648e-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="b648e-164">Предполагаемое время выполнения этой лабораторной работы: **60 минут**.</span><span class="sxs-lookup"><span data-stu-id="b648e-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="b648e-165">Упражнение 1. Создание проекта веб-приложения Мусиксторе ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b648e-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="b648e-166">В этом упражнении вы узнаете, как создать приложение ASP.NET MVC в Visual Studio 2012 Express для Web, а также в основной организации папок.</span><span class="sxs-lookup"><span data-stu-id="b648e-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="b648e-167">Кроме того, вы узнаете, как добавить новый контроллер и сделать так, чтобы на домашней странице приложения отображалась простая строка.</span><span class="sxs-lookup"><span data-stu-id="b648e-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="b648e-168">Задача 1. Создание проекта веб-приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b648e-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="b648e-169">В этой задаче будет создан пустой проект приложения ASP.NET MVC с помощью шаблона MVC Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="b648e-170">Запустите **VS Express для Web**.</span><span class="sxs-lookup"><span data-stu-id="b648e-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="b648e-171">В меню **Файл** выберите пункт **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="b648e-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="b648e-172">В диалоговом окне **Новый проект** выберите тип проекта **веб-приложение ASP.NET MVC 4** , расположенный в **разделе C#Visual,** список **веб-** шаблонов.</span><span class="sxs-lookup"><span data-stu-id="b648e-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="b648e-173">Измените **имя** на *мвкмусиксторе*.</span><span class="sxs-lookup"><span data-stu-id="b648e-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="b648e-174">Задайте расположение решения в новой **начальной** папке в исходной папке этого упражнения, например **[The-Холь-path] \Source\Ex01-CreatingMusicStoreProject\Begin**.</span><span class="sxs-lookup"><span data-stu-id="b648e-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="b648e-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b648e-175">Click **OK**.</span></span>

    <span data-ttu-id="b648e-176">![Диалоговое окно «Создание нового проекта»](aspnet-mvc-4-fundamentals/_static/image2.png "Диалоговое окно «Создание нового проекта»")</span><span class="sxs-lookup"><span data-stu-id="b648e-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="b648e-177">*Диалоговое окно «Создание нового проекта»*</span><span class="sxs-lookup"><span data-stu-id="b648e-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="b648e-178">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **базовый** шаблон и убедитесь, что для **обработчика представлений** выбрано значение **Razor**.</span><span class="sxs-lookup"><span data-stu-id="b648e-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="b648e-179">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b648e-179">Click **OK**.</span></span>

    <span data-ttu-id="b648e-180">![Диалоговое окно "Создание проекта ASP.NET MVC 4"](aspnet-mvc-4-fundamentals/_static/image3.png "Диалоговое окно "Создание проекта ASP.NET MVC 4"")</span><span class="sxs-lookup"><span data-stu-id="b648e-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="b648e-181">*Диалоговое окно "Создание проекта ASP.NET MVC 4"*</span><span class="sxs-lookup"><span data-stu-id="b648e-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="b648e-182">Задача 2. изучение структуры решения</span><span class="sxs-lookup"><span data-stu-id="b648e-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="b648e-183">Платформа ASP.NET MVC включает шаблон проекта Visual Studio, который помогает создавать веб-приложения, поддерживающие шаблон MVC.</span><span class="sxs-lookup"><span data-stu-id="b648e-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="b648e-184">Этот шаблон создает новое веб-приложение ASP.NET MVC с необходимыми папками, шаблонами элементов и записями файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b648e-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="b648e-185">В этой задаче будет рассмотрена структура решения, чтобы понять, какие элементы участвуют в работе, и их связи.</span><span class="sxs-lookup"><span data-stu-id="b648e-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="b648e-186">Следующие папки включены во все приложение ASP.NET MVC, так как платформа ASP.NET MVC по умолчанию использует &quot;ное соглашение по сравнению с конфигурацией&quot; и делает некоторые предположения по умолчанию на основе соглашений об именовании папок.</span><span class="sxs-lookup"><span data-stu-id="b648e-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="b648e-187">После создания проекта проверьте структуру папок, созданную в обозреватель решений с правой стороны:</span><span class="sxs-lookup"><span data-stu-id="b648e-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="b648e-188">![Структура папок ASP.NET MVC в обозреватель решений](aspnet-mvc-4-fundamentals/_static/image4.png "Структура папок ASP.NET MVC в обозреватель решений")</span><span class="sxs-lookup"><span data-stu-id="b648e-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="b648e-189">*Структура папок ASP.NET MVC в обозреватель решений*</span><span class="sxs-lookup"><span data-stu-id="b648e-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="b648e-190">**Контроллеры**.</span><span class="sxs-lookup"><span data-stu-id="b648e-190">**Controllers**.</span></span> <span data-ttu-id="b648e-191">В этой папке будут содержаться классы контроллеров.</span><span class="sxs-lookup"><span data-stu-id="b648e-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="b648e-192">В приложении на основе MVC контроллеры отвечают за обработку взаимодействия с конечным пользователем, управление моделью и в конечном итоге выбор представления для отрисовки пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b648e-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="b648e-193">Платформа MVC требует, чтобы имена всех контроллеров завершались с &quot;контроллером&quot;— например, HomeController, Логинконтроллер или Продуктконтроллер.</span><span class="sxs-lookup"><span data-stu-id="b648e-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="b648e-194">**Модели**.</span><span class="sxs-lookup"><span data-stu-id="b648e-194">**Models**.</span></span> <span data-ttu-id="b648e-195">Эта папка предоставляется для классов, представляющих модель приложения для веб-приложения MVC.</span><span class="sxs-lookup"><span data-stu-id="b648e-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="b648e-196">Обычно это включает код, определяющий объекты и логику для взаимодействия с хранилищем данных.</span><span class="sxs-lookup"><span data-stu-id="b648e-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="b648e-197">Сами объекты модели обычно располагаются в отдельных библиотеках классов.</span><span class="sxs-lookup"><span data-stu-id="b648e-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="b648e-198">Однако при создании нового приложения можно включить классы, а затем переместить их в отдельные библиотеки классов на более поздней стадии цикла разработки.</span><span class="sxs-lookup"><span data-stu-id="b648e-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="b648e-199">**Представления**.</span><span class="sxs-lookup"><span data-stu-id="b648e-199">**Views**.</span></span> <span data-ttu-id="b648e-200">Эта папка является рекомендуемым расположением для представлений, компонентов, ответственных за отображение пользовательского интерфейса приложения.</span><span class="sxs-lookup"><span data-stu-id="b648e-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="b648e-201">В представлениях используются файлы. aspx,. ascx,. cshtml и. master, а также любые другие файлы, связанные с представлениями подготовки отчетов.</span><span class="sxs-lookup"><span data-stu-id="b648e-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="b648e-202">Папка Views содержит папку для каждого контроллера; папка называется префиксом имени контроллера.</span><span class="sxs-lookup"><span data-stu-id="b648e-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="b648e-203">Например, если у вас есть контроллер с именем **HomeController**, в папке Views будет содержаться папка с именем Home.</span><span class="sxs-lookup"><span data-stu-id="b648e-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="b648e-204">По умолчанию, когда платформа MVC ASP.NET загружает представление, она ищет ASPX-файл с запрошенным именем представления в папке Виевс\контроллернаме (**views [controllerName] [Action]. aspx**) или (**views [ControllerName] [Action]. cshtml**) для представлений Razor.</span><span class="sxs-lookup"><span data-stu-id="b648e-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b648e-205">В дополнение к папкам, перечисленным ранее, веб-приложение MVC использует файл **Global. asax** для установки глобальных URL-адресов по умолчанию и использует файл **Web. config** для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b648e-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="b648e-206">Задача 3. Добавление HomeController</span><span class="sxs-lookup"><span data-stu-id="b648e-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="b648e-207">В приложениях ASP.NET, не использующих платформу MVC, взаимодействие с пользователем организовано по страницам, а вокруг этих страниц создается и обрабатывается событие.</span><span class="sxs-lookup"><span data-stu-id="b648e-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="b648e-208">В отличие от этого, взаимодействие пользователей с приложениями ASP.NET MVC организовано вокруг контроллеров и методов действий.</span><span class="sxs-lookup"><span data-stu-id="b648e-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="b648e-209">С другой стороны, ASP.NET платформа MVC сопоставляет URL-адреса классам, которые называются контроллерами.</span><span class="sxs-lookup"><span data-stu-id="b648e-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="b648e-210">Контроллеры обрабатывают входящие запросы, управляют вводом и взаимодействием пользователя, выполняют соответствующую логику приложения и определяют ответ для отправки клиенту (отображение HTML, скачивание файла, перенаправление на другой URL-адрес и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b648e-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="b648e-211">В случае отображения HTML класс контроллера обычно вызывает отдельный компонент представления для создания разметки HTML для запроса.</span><span class="sxs-lookup"><span data-stu-id="b648e-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="b648e-212">В приложении MVC представление служит только для отображения информации. Обработку введенных данных, формирование ответа и взаимодействие с пользователем обеспечивает контроллер.</span><span class="sxs-lookup"><span data-stu-id="b648e-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="b648e-213">В этой задаче вы добавите класс контроллера, который будет выполнять обработку URL-адресов на домашней странице сайта музыкального магазина.</span><span class="sxs-lookup"><span data-stu-id="b648e-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="b648e-214">Щелкните правой кнопкой мыши папку **Controllers** в Обозреватель решений, выберите **Добавить** , а затем — команду **контроллера** :</span><span class="sxs-lookup"><span data-stu-id="b648e-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="b648e-215">![Команда "добавить контроллер"](aspnet-mvc-4-fundamentals/_static/image5.png "Команда "добавить контроллер"")</span><span class="sxs-lookup"><span data-stu-id="b648e-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="b648e-216">*Команда добавления контроллера*</span><span class="sxs-lookup"><span data-stu-id="b648e-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="b648e-217">Откроется диалоговое окно **Добавление контроллера** .</span><span class="sxs-lookup"><span data-stu-id="b648e-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="b648e-218">Присвойте контроллеру имя *HomeController* и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="b648e-219">![Диалоговое окно добавления контроллера](aspnet-mvc-4-fundamentals/_static/image6.png "Диалоговое окно добавления контроллера")</span><span class="sxs-lookup"><span data-stu-id="b648e-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="b648e-220">*Диалоговое окно добавления контроллера*</span><span class="sxs-lookup"><span data-stu-id="b648e-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="b648e-221">Файл **HomeController.CS** создается в папке **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="b648e-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="b648e-222">Чтобы **HomeController** возвращал строку в своем действии индекса, замените метод **index** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="b648e-223">(Фрагмент кода — *основы ASP.NET MVC 4 — EX1 HomeController index*)</span><span class="sxs-lookup"><span data-stu-id="b648e-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="b648e-224">Задача 4. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="b648e-225">В этой задаче вы попробуете выполнить приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="b648e-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="b648e-226">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="b648e-227">Проект компилируется, и запускается локальный веб-сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="b648e-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="b648e-228">Локальный веб-сервер IIS автоматически откроет веб-браузер, указывающий на URL веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="b648e-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="b648e-229">![Приложение, работающее в веб-браузере](aspnet-mvc-4-fundamentals/_static/image7.png "Приложение, работающее в веб-браузере")</span><span class="sxs-lookup"><span data-stu-id="b648e-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="b648e-230">*Приложение, работающее в веб-браузере*</span><span class="sxs-lookup"><span data-stu-id="b648e-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-231">Локальный веб-сервер IIS запустит веб-сайт на случайный номер порта с произвольным номером.</span><span class="sxs-lookup"><span data-stu-id="b648e-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="b648e-232">На рисунке выше сайт работает на `http://localhost:50103/`, поэтому он использует порт 50103.</span><span class="sxs-lookup"><span data-stu-id="b648e-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="b648e-233">Номер порта может отличаться.</span><span class="sxs-lookup"><span data-stu-id="b648e-233">Your port number may vary.</span></span>
2. <span data-ttu-id="b648e-234">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="b648e-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="b648e-235">Упражнение 2. Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="b648e-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="b648e-236">В этом упражнении вы узнаете, как обновить контроллер, чтобы реализовать простую функциональность приложения музыкального магазина.</span><span class="sxs-lookup"><span data-stu-id="b648e-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="b648e-237">Этот контроллер будет определять методы действий для обработки каждого из следующих запросов:</span><span class="sxs-lookup"><span data-stu-id="b648e-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="b648e-238">Страница со списком жанров музыки в музыкальном магазине</span><span class="sxs-lookup"><span data-stu-id="b648e-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="b648e-239">Страница обзора, на которой перечислены все альбомы музыки для определенного жанра</span><span class="sxs-lookup"><span data-stu-id="b648e-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="b648e-240">Страница сведений, на которой отображаются сведения о конкретном музыкальном альбоме</span><span class="sxs-lookup"><span data-stu-id="b648e-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="b648e-241">В рамках этого упражнения эти действия будут просто возвращать строку.</span><span class="sxs-lookup"><span data-stu-id="b648e-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="b648e-242">Задача 1. Добавление нового класса Стореконтроллер</span><span class="sxs-lookup"><span data-stu-id="b648e-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="b648e-243">В этой задаче будет добавлен новый контроллер.</span><span class="sxs-lookup"><span data-stu-id="b648e-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="b648e-244">Если он еще не открыт, запустите **VS Express для Web 2012**.</span><span class="sxs-lookup"><span data-stu-id="b648e-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="b648e-245">В меню **файл** выберите команду **Открыть проект**.</span><span class="sxs-lookup"><span data-stu-id="b648e-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="b648e-246">В диалоговом окне Открытие проекта перейдите к **Source\Ex02-CreatingAController\Begin**, выберите **Begin. sln** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="b648e-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="b648e-247">Кроме того, вы можете продолжить работу с решением, полученным после завершения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="b648e-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="b648e-248">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="b648e-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b648e-249">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b648e-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b648e-250">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="b648e-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b648e-251">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="b648e-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b648e-252">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b648e-253">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b648e-254">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="b648e-255">Добавьте новый контроллер.</span><span class="sxs-lookup"><span data-stu-id="b648e-255">Add the new controller.</span></span> <span data-ttu-id="b648e-256">Для этого щелкните правой кнопкой мыши папку **Controllers** в Обозреватель решений, выберите **Добавить** , а затем — команду **контроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="b648e-257">Измените **имя контроллера** на *стореконтроллер*и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="b648e-258">![Диалоговое окно добавления контроллера](aspnet-mvc-4-fundamentals/_static/image8.png "Диалоговое окно добавления контроллера")</span><span class="sxs-lookup"><span data-stu-id="b648e-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="b648e-259">*Диалоговое окно добавления контроллера*</span><span class="sxs-lookup"><span data-stu-id="b648e-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="b648e-260">Задача 2. изменение действий Стореконтроллер</span><span class="sxs-lookup"><span data-stu-id="b648e-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="b648e-261">В этой задаче будут изменены методы контроллера, которые называются **действиями**.</span><span class="sxs-lookup"><span data-stu-id="b648e-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="b648e-262">Действия отвечают за обработку запросов URL-адресов и определение содержимого, которое должно быть отправлено обратно браузеру или пользователю, вызвавшему этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b648e-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="b648e-263">Класс **стореконтроллер** уже имеет метод **индекса** .</span><span class="sxs-lookup"><span data-stu-id="b648e-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="b648e-264">Он будет использоваться позже в этой лабораторной работе для реализации страницы со списком всех жанров музыкального магазина.</span><span class="sxs-lookup"><span data-stu-id="b648e-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="b648e-265">Сейчас просто замените метод **index** следующим кодом, который возвращает строку &quot;Hello из Store. index ()&quot;:</span><span class="sxs-lookup"><span data-stu-id="b648e-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="b648e-266">(Фрагмент кода — *основы ASP.NET MVC 4 — EX2 Стореконтроллер index*)</span><span class="sxs-lookup"><span data-stu-id="b648e-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="b648e-267">Добавьте методы **обзора** и **подробностей** .</span><span class="sxs-lookup"><span data-stu-id="b648e-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="b648e-268">Для этого добавьте в **стореконтроллер**следующий код:</span><span class="sxs-lookup"><span data-stu-id="b648e-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="b648e-269">(Фрагмент кода — *ASP.NET MVC 4 основы — EX2 Стореконтроллер бровсеанддетаилс*)</span><span class="sxs-lookup"><span data-stu-id="b648e-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="b648e-270">Задача 3. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="b648e-271">В этой задаче вы попробуете выполнить приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="b648e-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="b648e-272">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-273">Проект начинается на **домашней** странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="b648e-274">Измените URL-адрес, чтобы проверить реализацию каждого действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="b648e-275">**/Store**.</span><span class="sxs-lookup"><span data-stu-id="b648e-275">**/Store**.</span></span> <span data-ttu-id="b648e-276">Вы увидите **&quot;Hello из Store. index ()&quot;** .</span><span class="sxs-lookup"><span data-stu-id="b648e-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="b648e-277">**/Сторе/бровсе**.</span><span class="sxs-lookup"><span data-stu-id="b648e-277">**/Store/Browse**.</span></span> <span data-ttu-id="b648e-278">Вы увидите **&quot;Hello из Store. Browse ()&quot;** .</span><span class="sxs-lookup"><span data-stu-id="b648e-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="b648e-279">**/Сторе/детаилс**.</span><span class="sxs-lookup"><span data-stu-id="b648e-279">**/Store/Details**.</span></span> <span data-ttu-id="b648e-280">Вы увидите **&quot;Hello from Store. Details ()&quot;** .</span><span class="sxs-lookup"><span data-stu-id="b648e-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="b648e-281">![Просмотр Сторебровсе](aspnet-mvc-4-fundamentals/_static/image9.png "Просмотр Сторебровсе")</span><span class="sxs-lookup"><span data-stu-id="b648e-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="b648e-282">*Просмотр/Сторе/бровсе*</span><span class="sxs-lookup"><span data-stu-id="b648e-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="b648e-283">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="b648e-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="b648e-284">Упражнение 3. Передача параметров в контроллер</span><span class="sxs-lookup"><span data-stu-id="b648e-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="b648e-285">До настоящего момента вы возвращали постоянные строки из контроллеров.</span><span class="sxs-lookup"><span data-stu-id="b648e-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="b648e-286">В этом упражнении вы узнаете, как передавать параметры в контроллер с помощью URL-адреса и строки запроса, а затем сделать так, чтобы действия метода реагировали на текст в браузере.</span><span class="sxs-lookup"><span data-stu-id="b648e-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="b648e-287">Задача 1. Добавление параметра жанра в Стореконтроллер</span><span class="sxs-lookup"><span data-stu-id="b648e-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="b648e-288">В этой задаче вы будете использовать **строку запроса** для отправки параметров в метод действия **Browse** в **стореконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="b648e-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="b648e-289">Если он еще не открыт, запустите **VS Express для Web**.</span><span class="sxs-lookup"><span data-stu-id="b648e-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="b648e-290">В меню **файл** выберите команду **Открыть проект**.</span><span class="sxs-lookup"><span data-stu-id="b648e-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="b648e-291">В диалоговом окне Открытие проекта перейдите к **Source\Ex03-PassingParametersToAController\Begin**, выберите **Begin. sln** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="b648e-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="b648e-292">Кроме того, вы можете продолжить работу с решением, полученным после завершения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="b648e-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="b648e-293">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="b648e-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b648e-294">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b648e-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b648e-295">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="b648e-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b648e-296">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="b648e-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b648e-297">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b648e-298">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b648e-299">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="b648e-300">Откройте класс **стореконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-300">Open **StoreController** class.</span></span> <span data-ttu-id="b648e-301">Для этого в **Обозреватель решений**разверните папку **Controllers** и дважды щелкните **StoreController.CS**.</span><span class="sxs-lookup"><span data-stu-id="b648e-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="b648e-302">Измените метод **Browse** , добавив строковый параметр для запроса определенного жанра.</span><span class="sxs-lookup"><span data-stu-id="b648e-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="b648e-303">ASP.NET MVC автоматически передает любые параметры QueryString или формы POST с именем **жанра** в этот метод действия при вызове.</span><span class="sxs-lookup"><span data-stu-id="b648e-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="b648e-304">Для этого замените метод **Browse** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="b648e-305">(Фрагмент кода — *ASP.NET MVC 4 основы — EX3 Стореконтроллер бровсемесод*)</span><span class="sxs-lookup"><span data-stu-id="b648e-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="b648e-306">Вы используете служебный метод **HttpUtility. HtmlEncode** , чтобы запретить пользователям внедрять JavaScript в представление со ссылкой, например **/Сторе/бровсе? Жанр =&lt;скрипт&gt;Window. location = '[http://hackersite.com](http://hackersite.com)'&lt;/Script&gt;** .</span><span class="sxs-lookup"><span data-stu-id="b648e-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="b648e-307">Дополнительные объяснения см. в [этой статье MSDN](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span><span class="sxs-lookup"><span data-stu-id="b648e-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="b648e-308">Задача 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="b648e-309">В этой задаче вы попробуете использовать приложение в веб-браузере и запустите параметр **Жанр** .</span><span class="sxs-lookup"><span data-stu-id="b648e-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="b648e-310">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-311">Проект начинается на **домашней** странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="b648e-312">Изменить URL-адрес на */Сторе/бровсе? Жанр = Disco* , чтобы убедиться, что действие получает параметр жанра.</span><span class="sxs-lookup"><span data-stu-id="b648e-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="b648e-313">![Просмотр Сторебровсеженре = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Просмотр Сторебровсеженре = Disco")</span><span class="sxs-lookup"><span data-stu-id="b648e-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="b648e-314">*Обзор/Сторе/бровсе? Жанр = Disco*</span><span class="sxs-lookup"><span data-stu-id="b648e-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="b648e-315">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="b648e-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="b648e-316">Задача 3. Добавление параметра идентификатора, внедренного в URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b648e-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="b648e-317">В этой задаче вы будете использовать **URL-адрес** для передачи **параметра ID** методу действия **Details** объекта **стореконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="b648e-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="b648e-318">Соглашение о маршрутизации по умолчанию для ASP.NET MVC состоит в том, чтобы обрабатывать сегмент URL-адреса после имени метода действия в качестве параметра с именем **ID**. Если у метода действия есть параметр с именем ID, ASP.NET MVC автоматически передаст сегмент URL-адреса в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="b648e-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="b648e-319">В хранилище URL-адресов/ **Details/5** **идентификатор** будет интерпретирован как **5**.</span><span class="sxs-lookup"><span data-stu-id="b648e-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="b648e-320">Измените метод **Details** объекта **стореконтроллер**, добавив параметр **int** с именем **ID**. Для этого замените метод **Details** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="b648e-321">(Фрагмент кода — *ASP.NET MVC 4 основы — EX3 Стореконтроллер детаилсмесод*)</span><span class="sxs-lookup"><span data-stu-id="b648e-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="b648e-322">Задача 4. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="b648e-323">В этой задаче вы попробуете выполнить приложение в веб-браузере и будете использовать параметр **ID** .</span><span class="sxs-lookup"><span data-stu-id="b648e-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="b648e-324">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-325">Проект начинается на **домашней** странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="b648e-326">Измените URL-адрес на */Store/Details/5* , чтобы убедиться, что действие получает параметр ID.</span><span class="sxs-lookup"><span data-stu-id="b648e-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="b648e-327">![Просмотр StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Просмотр StoreDetails5")</span><span class="sxs-lookup"><span data-stu-id="b648e-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="b648e-328">*Просмотр/Store/Details/5*</span><span class="sxs-lookup"><span data-stu-id="b648e-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="b648e-329">Упражнение 4. Создание представления</span><span class="sxs-lookup"><span data-stu-id="b648e-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="b648e-330">До сих пор вы вернули строки из действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="b648e-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="b648e-331">Хотя это полезный способ понять, как работают контроллеры, это не то, как создаются реальные веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b648e-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="b648e-332">Представления — это компоненты, обеспечивающие лучший подход к созданию HTML обратно в браузере с использованием файлов шаблонов.</span><span class="sxs-lookup"><span data-stu-id="b648e-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="b648e-333">В этом упражнении вы узнаете, как добавить главную страницу макета, чтобы настроить шаблон для общего содержимого HTML, таблицу стилей для улучшения внешнего вида веб-узла и, наконец, шаблон представления, позволяющий HomeController вернуть HTML.</span><span class="sxs-lookup"><span data-stu-id="b648e-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="b648e-334">Задача 1. изменение файла \_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="b648e-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="b648e-335">Файл **~/виевс/шаред/\_Layout. cshtml** позволяет настроить шаблон для общего HTML-кода, который будет использоваться во всем веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="b648e-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="b648e-336">В этой задаче будет добавлена эталонная страница макета со стандартным заголовком со ссылками на домашнюю страницу и область хранения.</span><span class="sxs-lookup"><span data-stu-id="b648e-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="b648e-337">Если он еще не открыт, запустите **VS Express для Web**.</span><span class="sxs-lookup"><span data-stu-id="b648e-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="b648e-338">В меню **файл** выберите команду **Открыть проект**.</span><span class="sxs-lookup"><span data-stu-id="b648e-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="b648e-339">В диалоговом окне Открытие проекта перейдите к **Source\Ex04-CreatingAView\Begin**, выберите **Begin. sln** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="b648e-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="b648e-340">Кроме того, вы можете продолжить работу с решением, полученным после завершения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="b648e-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="b648e-341">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="b648e-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b648e-342">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b648e-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b648e-343">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="b648e-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b648e-344">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="b648e-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b648e-345">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b648e-346">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b648e-347">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="b648e-348">Файл <strong>\_Layout. cshtml</strong> содержит макет контейнера HTML для всех страниц сайта.</span><span class="sxs-lookup"><span data-stu-id="b648e-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="b648e-349">Он включает элемент <strong>&lt;html&gt;</strong> для ответа HTML, а также элементы <strong>&lt;head&gt;</strong> и <strong>&lt;Body&gt;</strong> .</span><span class="sxs-lookup"><span data-stu-id="b648e-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="b648e-350"><strong>@RenderBody()</strong> в тексте HTML определяет регионы, в которых шаблоны просмотра могут заполняться динамическим содержимым.</span><span class="sxs-lookup"><span data-stu-id="b648e-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="b648e-351">C#</span><span class="sxs-lookup"><span data-stu-id="b648e-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="b648e-352">Добавьте общий заголовок со ссылками на домашнюю страницу и область хранения на всех страницах сайта.</span><span class="sxs-lookup"><span data-stu-id="b648e-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="b648e-353">Для этого добавьте следующий код, приведенный ниже &lt;текстовой инструкции&gt;.</span><span class="sxs-lookup"><span data-stu-id="b648e-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="b648e-354">C#</span><span class="sxs-lookup"><span data-stu-id="b648e-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="b648e-355">Включите тег div, чтобы отобразить раздел текста на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="b648e-356">Замените <strong>@RenderBody()</strong> следующим выделенным кодом: (C#)</span><span class="sxs-lookup"><span data-stu-id="b648e-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="b648e-357">Знаете ли вы?</span><span class="sxs-lookup"><span data-stu-id="b648e-357">Did you know?</span></span> <span data-ttu-id="b648e-358">В Visual Studio 2012 есть фрагменты кода, которые упрощают добавление часто используемых кодов в HTML, файлы кода и многое другое.</span><span class="sxs-lookup"><span data-stu-id="b648e-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="b648e-359">Попробуйте ввести **&lt;div&gt;** и дважды нажмите клавишу **Tab** , чтобы вставить полный тег **div** .</span><span class="sxs-lookup"><span data-stu-id="b648e-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="b648e-360">Задача 2. Добавление таблицы стилей CSS</span><span class="sxs-lookup"><span data-stu-id="b648e-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="b648e-361">Шаблон пустого проекта содержит очень упрощенный файл CSS, который содержит только стили, используемые для вывода базовых форм и сообщений о проверке.</span><span class="sxs-lookup"><span data-stu-id="b648e-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="b648e-362">Для улучшения внешнего вида веб-узла будут использоваться дополнительные CSS и изображения (потенциально предоставляемые конструктором).</span><span class="sxs-lookup"><span data-stu-id="b648e-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="b648e-363">В этой задаче будет добавлена таблица стилей CSS для определения стилей сайта.</span><span class="sxs-lookup"><span data-stu-id="b648e-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="b648e-364">Файл CSS и изображения включаются в папку **саурце\ассетс\контент** этой лабораторной работы.</span><span class="sxs-lookup"><span data-stu-id="b648e-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="b648e-365">Чтобы добавить их в приложение, перетащите его содержимое из окна **проводника Windows** в **Обозреватель решений** в Visual Studio Express для Web, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b648e-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="b648e-366">![Перетаскивание содержимого стиля](aspnet-mvc-4-fundamentals/_static/image12.png "Перетаскивание содержимого стиля")</span><span class="sxs-lookup"><span data-stu-id="b648e-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="b648e-367">*Перетаскивание содержимого стиля*</span><span class="sxs-lookup"><span data-stu-id="b648e-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="b648e-368">Появится диалоговое окно с предупреждением, в котором запрашивается подтверждение замены файла **site. CSS** и некоторых существующих образов.</span><span class="sxs-lookup"><span data-stu-id="b648e-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="b648e-369">Установите флажок **Применить ко всем элементам** и нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="b648e-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="b648e-370">Задача 3. Добавление шаблона представления</span><span class="sxs-lookup"><span data-stu-id="b648e-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="b648e-371">В этой задаче будет добавлен шаблон представления для создания ответа HTML, который будет использовать главную страницу макета и CSS, добавленные в этом упражнении.</span><span class="sxs-lookup"><span data-stu-id="b648e-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="b648e-372">Чтобы использовать шаблон представления при просмотре домашней страницы сайта, необходимо сначала указать, что вместо возврата строки метод **HomeController index** вернет **представление**.</span><span class="sxs-lookup"><span data-stu-id="b648e-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="b648e-373">Откройте класс **HomeController** и измените его метод **index** , чтобы он возвращал объект **ActionResult**и возвращал **представление ()** .</span><span class="sxs-lookup"><span data-stu-id="b648e-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="b648e-374">(Фрагмент кода — *основы ASP.NET MVC 4 — EX4 HomeController index*)</span><span class="sxs-lookup"><span data-stu-id="b648e-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="b648e-375">Теперь необходимо добавить соответствующий шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="b648e-376">Для этого **щелкните правой кнопкой мыши** внутри метода действия **индекса** и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="b648e-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="b648e-377">Откроется диалоговое окно **Добавление представления** .</span><span class="sxs-lookup"><span data-stu-id="b648e-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="b648e-378">![Добавление представления из метода index](aspnet-mvc-4-fundamentals/_static/image13.png "Добавление представления из метода index")</span><span class="sxs-lookup"><span data-stu-id="b648e-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="b648e-379">*Добавление представления из метода index*</span><span class="sxs-lookup"><span data-stu-id="b648e-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="b648e-380">Появится диалоговое окно **Добавление представления** для создания файла шаблона представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="b648e-381">По умолчанию это диалоговое окно предварительно заполняет имя шаблона представления, чтобы оно соответствовало методу действия, который будет его использовать.</span><span class="sxs-lookup"><span data-stu-id="b648e-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="b648e-382">Поскольку вы использовали контекстное меню **Добавить представление** в методе действия **индекса** в HomeController, в диалоговом окне **Добавление представления** в качестве имени представления по умолчанию используется индекс.</span><span class="sxs-lookup"><span data-stu-id="b648e-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="b648e-383">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-383">Click **Add**.</span></span>

    <span data-ttu-id="b648e-384">![Диалоговое окно добавления представления](aspnet-mvc-4-fundamentals/_static/image14.png "Диалоговое окно добавления представления")</span><span class="sxs-lookup"><span data-stu-id="b648e-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="b648e-385">*Диалоговое окно добавления представления*</span><span class="sxs-lookup"><span data-stu-id="b648e-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="b648e-386">Visual Studio создаст шаблон представления **index. cshtml** в папке **Views\Home** , а затем откроет его.</span><span class="sxs-lookup"><span data-stu-id="b648e-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="b648e-387">![Создано представление домашнего индекса](aspnet-mvc-4-fundamentals/_static/image15.png "Создано представление домашнего индекса")</span><span class="sxs-lookup"><span data-stu-id="b648e-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="b648e-388">*Создано представление домашнего индекса*</span><span class="sxs-lookup"><span data-stu-id="b648e-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-389">имя и расположение файла **index. cshtml** являются релевантными и следуют соглашениям об именовании ASP.NET MVC по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b648e-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="b648e-390">Папка \Виевс\**Home*\* соответствует имени контроллера (**домашний** контроллер).</span><span class="sxs-lookup"><span data-stu-id="b648e-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="b648e-391">Имя шаблона представления (**индекс**) соответствует методу действия контроллера, который будет отображать представление.</span><span class="sxs-lookup"><span data-stu-id="b648e-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="b648e-392">Таким образом, ASP.NET MVC позволяет избежать необходимости явно указывать имя или расположение шаблона представления при использовании этого соглашения об именовании для возвращения представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="b648e-393">Созданный шаблон представления основан на ранее определенном шаблоне **\_Layout. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="b648e-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="b648e-394">Измените свойство ViewBag. Title на **Home**, а основное содержимое **— на домашнюю страницу**, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="b648e-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="b648e-395">Выберите проект **мвкмусиксторе** в Обозреватель решений и нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="b648e-396">Задача 4. Проверка</span><span class="sxs-lookup"><span data-stu-id="b648e-396">Task 4: Verification</span></span>

<span data-ttu-id="b648e-397">Чтобы убедиться в правильности выполнения всех действий, описанных в предыдущем упражнении, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="b648e-398">Если приложение открыто в браузере, следует отметить следующее:</span><span class="sxs-lookup"><span data-stu-id="b648e-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="b648e-399">Метод действия индекса HomeController находит и отображает шаблон представления **\виевс\хоме\индекс.кштмл** , несмотря на то, что в коде, именуемом, **возвращается View ()** , так как шаблон представления, за которым следует стандартное соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="b648e-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="b648e-400">На домашней странице отображается приветственное сообщение, определенное в шаблоне представления **\виевс\хоме\индекс.кштмл** .</span><span class="sxs-lookup"><span data-stu-id="b648e-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="b648e-401">Домашняя страница использует шаблон **\_Layout. cshtml** , поэтому приветственное сообщение содержится в макете HTML для стандартного сайта.</span><span class="sxs-lookup"><span data-stu-id="b648e-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="b648e-402">![Представление домашнего индекса с использованием определенного Лайаутпаже и стиля](aspnet-mvc-4-fundamentals/_static/image16.png "Представление домашнего индекса с использованием определенного Лайаутпаже и стиля")</span><span class="sxs-lookup"><span data-stu-id="b648e-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="b648e-403">*Представление домашнего индекса с использованием определенного Лайаутпаже и стиля*</span><span class="sxs-lookup"><span data-stu-id="b648e-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="b648e-404">Упражнение 5. Создание модели представления</span><span class="sxs-lookup"><span data-stu-id="b648e-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="b648e-405">Пока вы сделали так, чтобы в представлениях отображался жестко закодированный HTML, но для создания динамических веб-приложений шаблон представления должен получить сведения от контроллера.</span><span class="sxs-lookup"><span data-stu-id="b648e-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="b648e-406">Одним из распространенных способов использования этой цели является шаблон **ViewModel** , который позволяет контроллеру упаковать всю информацию, необходимую для создания соответствующего HTML-ответа.</span><span class="sxs-lookup"><span data-stu-id="b648e-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="b648e-407">В этом упражнении вы узнаете, как создать класс ViewModel и добавить необходимые свойства: количество жанров в магазине и список этих жанров.</span><span class="sxs-lookup"><span data-stu-id="b648e-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="b648e-408">Вы также обновите Стореконтроллер для использования созданного ViewModel и, наконец, создадите новый шаблон представления, который будет отображать указанные свойства на странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="b648e-409">Задача 1. Создание класса ViewModel</span><span class="sxs-lookup"><span data-stu-id="b648e-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="b648e-410">В этой задаче будет создан класс ViewModel, который будет реализовывать сценарий Store со списком жанров.</span><span class="sxs-lookup"><span data-stu-id="b648e-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="b648e-411">Если он еще не открыт, запустите **VS Express для Web**.</span><span class="sxs-lookup"><span data-stu-id="b648e-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="b648e-412">В меню **файл** выберите команду **Открыть проект**.</span><span class="sxs-lookup"><span data-stu-id="b648e-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="b648e-413">В диалоговом окне Открытие проекта перейдите к **Source\Ex05-CreatingAViewModel\Begin**, выберите **Begin. sln** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="b648e-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="b648e-414">Кроме того, вы можете продолжить работу с решением, полученным после завершения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="b648e-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="b648e-415">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="b648e-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b648e-416">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b648e-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b648e-417">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="b648e-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b648e-418">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="b648e-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b648e-419">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b648e-420">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b648e-421">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="b648e-422">Создайте папку **ViewModels** для хранения ViewModel.</span><span class="sxs-lookup"><span data-stu-id="b648e-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="b648e-423">Для этого щелкните правой кнопкой мыши проект **мвкмусиксторе** верхнего уровня, выберите **Добавить** , а затем — **создать папку**.</span><span class="sxs-lookup"><span data-stu-id="b648e-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="b648e-424">![Добавление новой папки](aspnet-mvc-4-fundamentals/_static/image17.png "Добавление новой папки")</span><span class="sxs-lookup"><span data-stu-id="b648e-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="b648e-425">*Добавление новой папки*</span><span class="sxs-lookup"><span data-stu-id="b648e-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="b648e-426">Присвойте папке имя *ViewModel*.</span><span class="sxs-lookup"><span data-stu-id="b648e-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="b648e-427">![Папка ViewModels в обозреватель решений](aspnet-mvc-4-fundamentals/_static/image18.png "Папка ViewModels в обозреватель решений")</span><span class="sxs-lookup"><span data-stu-id="b648e-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="b648e-428">*Папка ViewModels в обозреватель решений*</span><span class="sxs-lookup"><span data-stu-id="b648e-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="b648e-429">Создайте класс **ViewModel** .</span><span class="sxs-lookup"><span data-stu-id="b648e-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="b648e-430">Для этого щелкните правой кнопкой мыши папку **ViewModels** , созданную недавно, и выберите **Добавить** , а затем **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="b648e-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="b648e-431">В разделе **код**выберите элемент **класса** и назовите файл *StoreIndexViewModel.CS*, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="b648e-432">![Добавление нового класса](aspnet-mvc-4-fundamentals/_static/image19.png "Добавление нового класса")</span><span class="sxs-lookup"><span data-stu-id="b648e-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="b648e-433">*Добавление нового класса*</span><span class="sxs-lookup"><span data-stu-id="b648e-433">*Adding a new Class*</span></span>

    <span data-ttu-id="b648e-434">![Создание класса Стореиндексвиевмодел](aspnet-mvc-4-fundamentals/_static/image20.png "Создание класса Стореиндексвиевмодел")</span><span class="sxs-lookup"><span data-stu-id="b648e-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="b648e-435">*Создание класса Стореиндексвиевмодел*</span><span class="sxs-lookup"><span data-stu-id="b648e-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="b648e-436">Задача 2. Добавление свойств в класс ViewModel</span><span class="sxs-lookup"><span data-stu-id="b648e-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="b648e-437">Существует два параметра, которые необходимо передать из Стореконтроллер в шаблон представления, чтобы создать ожидаемый ответ HTML: количество жанров в магазине и список этих жанров.</span><span class="sxs-lookup"><span data-stu-id="b648e-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="b648e-438">В этой задаче вы добавите эти 2 свойства в класс **стореиндексвиевмодел** : **нумберофженрес** (целое число) и **жанры** (список строк).</span><span class="sxs-lookup"><span data-stu-id="b648e-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="b648e-439">Добавьте свойства **нумберофженрес** и **жанры** в класс **стореиндексвиевмодел** .</span><span class="sxs-lookup"><span data-stu-id="b648e-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="b648e-440">Для этого добавьте следующие 2 строки в определение класса:</span><span class="sxs-lookup"><span data-stu-id="b648e-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="b648e-441">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex5 стореиндексвиевмодел Properties*)</span><span class="sxs-lookup"><span data-stu-id="b648e-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="b648e-442">В нотации **{Get; Set;}** используется C#функция автоматического внедрения свойств.</span><span class="sxs-lookup"><span data-stu-id="b648e-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="b648e-443">Он предоставляет преимущества свойства, не требуя объявления резервного поля.</span><span class="sxs-lookup"><span data-stu-id="b648e-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="b648e-444">Задача 3. обновление Стореконтроллер для использования Стореиндексвиевмодел</span><span class="sxs-lookup"><span data-stu-id="b648e-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="b648e-445">Класс **стореиндексвиевмодел** инкапсулирует сведения, необходимые для передачи из метода индекса **Стореконтроллер**в шаблон представления, чтобы создать ответ.</span><span class="sxs-lookup"><span data-stu-id="b648e-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="b648e-446">В этой задаче будет обновлен **стореконтроллер** для использования **стореиндексвиевмодел**.</span><span class="sxs-lookup"><span data-stu-id="b648e-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="b648e-447">Откройте класс **стореконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="b648e-448">![Открытие класса Стореконтроллер](aspnet-mvc-4-fundamentals/_static/image21.png "Открытие класса Стореконтроллер")</span><span class="sxs-lookup"><span data-stu-id="b648e-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="b648e-449">*Открытие класса Стореконтроллер*</span><span class="sxs-lookup"><span data-stu-id="b648e-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="b648e-450">Чтобы использовать класс **стореиндексвиевмодел** из **стореконтроллер**, добавьте следующее пространство имен в начало кода **стореконтроллер** :</span><span class="sxs-lookup"><span data-stu-id="b648e-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="b648e-451">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex5 стореиндексвиевмодел с использованием ViewModels*)</span><span class="sxs-lookup"><span data-stu-id="b648e-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="b648e-452">Измените метод действия **индекса** **стореконтроллер**таким образом, чтобы он создавал и заполнил объект **стореиндексвиевмодел** , а затем передавал его в шаблон представления, чтобы создать HTML-ответ с ним.</span><span class="sxs-lookup"><span data-stu-id="b648e-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-453">В лабораториях &quot;ASP.NET модели MVC и доступ к данным&quot; будет написан код, который извлекает список жанров магазина из базы данных.</span><span class="sxs-lookup"><span data-stu-id="b648e-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="b648e-454">В следующем коде будет создан **список** фиктивных жанров данных, которые будут заполнять **стореиндексвиевмодел**.</span><span class="sxs-lookup"><span data-stu-id="b648e-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="b648e-455">После создания и настройки объекта **стореиндексвиевмодел** он будет передан в качестве аргумента в метод **View** .</span><span class="sxs-lookup"><span data-stu-id="b648e-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="b648e-456">Это означает, что шаблон представления будет использовать этот объект для создания в нем ответа HTML.</span><span class="sxs-lookup"><span data-stu-id="b648e-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="b648e-457">Замените метод **index** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="b648e-458">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex5 Стореконтроллер index*)</span><span class="sxs-lookup"><span data-stu-id="b648e-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="b648e-459">Если вы не знакомы с C#, можно предположить, что использование **var** означает, что переменная **viewModel** имеет позднюю привязку.</span><span class="sxs-lookup"><span data-stu-id="b648e-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="b648e-460">Это неверно. C# компилятор использует определение типа, основанное на назначении переменной, чтобы определить, что **ViewModel** имеет тип **стореиндексвиевмодел**.</span><span class="sxs-lookup"><span data-stu-id="b648e-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="b648e-461">Кроме того, путем компиляции локальной переменной **viewModel** в качестве типа **стореиндексвиевмодел** вы получаете проверку во время компиляции и поддержку редактора кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="b648e-462">Задача 4. Создание шаблона представления, использующего Стореиндексвиевмодел</span><span class="sxs-lookup"><span data-stu-id="b648e-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="b648e-463">В этой задаче будет создан шаблон представления, который будет использовать объект Стореиндексвиевмодел, переданный контроллером, для отображения списка жанров.</span><span class="sxs-lookup"><span data-stu-id="b648e-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="b648e-464">Перед созданием нового шаблона представления выполним сборку проекта, чтобы **диалоговое окно добавления представления** знало о классе **стореиндексвиевмодел** .</span><span class="sxs-lookup"><span data-stu-id="b648e-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="b648e-465">Выполните сборку проекта, выбрав пункт меню **Сборка** , а затем — **сборку мвкмусиксторе**.</span><span class="sxs-lookup"><span data-stu-id="b648e-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="b648e-466">![Сборка проекта](aspnet-mvc-4-fundamentals/_static/image22.png "Сборка проекта")</span><span class="sxs-lookup"><span data-stu-id="b648e-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="b648e-467">*Сборка проекта*</span><span class="sxs-lookup"><span data-stu-id="b648e-467">*Building the project*</span></span>
2. <span data-ttu-id="b648e-468">Создайте новый шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-468">Create a new View template.</span></span> <span data-ttu-id="b648e-469">Для этого щелкните правой кнопкой мыши внутри метода **index** и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="b648e-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="b648e-470">![Добавление представления](aspnet-mvc-4-fundamentals/_static/image23.png "Добавление представления")</span><span class="sxs-lookup"><span data-stu-id="b648e-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="b648e-471">*Добавление представления*</span><span class="sxs-lookup"><span data-stu-id="b648e-471">*Adding a View*</span></span>
3. <span data-ttu-id="b648e-472">Так как **диалоговое окно добавления представления** было вызвано из **Стореконтроллер**, шаблон представления по умолчанию будет добавлен в файл **\виевс\сторе\индекс.кштмл** .</span><span class="sxs-lookup"><span data-stu-id="b648e-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="b648e-473">Установите флажок **создать строго типизированное представление** и выберите **стореиндексвиевмодел** в качестве **класса модели**.</span><span class="sxs-lookup"><span data-stu-id="b648e-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="b648e-474">Кроме того, убедитесь, что для обработчика представлений выбрано значение **Razor**.</span><span class="sxs-lookup"><span data-stu-id="b648e-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="b648e-475">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-475">Click **Add**.</span></span>

    <span data-ttu-id="b648e-476">![Диалоговое окно добавления представления](aspnet-mvc-4-fundamentals/_static/image24.png "Диалоговое окно добавления представления")</span><span class="sxs-lookup"><span data-stu-id="b648e-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="b648e-477">*Диалоговое окно добавления представления*</span><span class="sxs-lookup"><span data-stu-id="b648e-477">*Add View Dialog*</span></span>

    <span data-ttu-id="b648e-478">Будет создан и открыт файл шаблона представления **\виевс\сторе\индекс.кштмл** .</span><span class="sxs-lookup"><span data-stu-id="b648e-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="b648e-479">В зависимости от сведений, предоставленных в диалоговом окне **Добавление представления** на последнем шаге, шаблон представления будет предполагать, что экземпляр **стореиндексвиевмодел** используется в качестве данных для создания ответа HTML.</span><span class="sxs-lookup"><span data-stu-id="b648e-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="b648e-480">Вы увидите, что шаблон наследует `ViewPage<musicstore.viewmodels.storeindexviewmodel>` в C#.</span><span class="sxs-lookup"><span data-stu-id="b648e-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="b648e-481">Задача 5. обновление шаблона представления</span><span class="sxs-lookup"><span data-stu-id="b648e-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="b648e-482">В этой задаче будет обновлен шаблон представления, созданный в последней задаче, чтобы получить количество жанров и их имен на странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="b648e-483">Для выполнения кода в шаблоне представления будет использоваться @ Syntax (часто это называется &quot;Code кусочки&quot;).</span><span class="sxs-lookup"><span data-stu-id="b648e-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="b648e-484">В файле **index. cshtml** в папке **Store** замените его код следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="b648e-485">Проведите перебор списка жанров в **стореиндексвиевмодел** и создайте список **&gt;HTML&lt;UL** с помощью цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="b648e-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="b648e-486">C#</span><span class="sxs-lookup"><span data-stu-id="b648e-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="b648e-487">Нажмите клавишу **F5** , чтобы запустить приложение и просмотреть **/Store**.</span><span class="sxs-lookup"><span data-stu-id="b648e-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="b648e-488">Вы увидите список жанров, переданных в объект **стореиндексвиевмодел** из **Стореконтроллер** в шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="b648e-489">![Просмотр списка жанров](aspnet-mvc-4-fundamentals/_static/image26.png "Просмотр списка жанров")</span><span class="sxs-lookup"><span data-stu-id="b648e-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="b648e-490">*Просмотр списка жанров*</span><span class="sxs-lookup"><span data-stu-id="b648e-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="b648e-491">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="b648e-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="b648e-492">Упражнение 6. Использование параметров в представлении</span><span class="sxs-lookup"><span data-stu-id="b648e-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="b648e-493">В упражнении 3 вы узнали, как передавать параметры в контроллер.</span><span class="sxs-lookup"><span data-stu-id="b648e-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="b648e-494">В этом упражнении вы узнаете, как использовать эти параметры в шаблоне представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="b648e-495">Для этой цели вы сначала предоставили классы модели, которые помогут вам управлять данными и логикой предметной области.</span><span class="sxs-lookup"><span data-stu-id="b648e-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="b648e-496">Кроме того, вы узнаете, как создавать ссылки на страницы в приложении MVC ASP.NET, не беспокоясь о том, как кодировать URL-пути.</span><span class="sxs-lookup"><span data-stu-id="b648e-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="b648e-497">Задача 1. Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="b648e-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="b648e-498">В отличие от ViewModel, которые создаются для передачи информации из контроллера в представление, классы модели создаются для хранения и управления данными и логикой предметной области.</span><span class="sxs-lookup"><span data-stu-id="b648e-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="b648e-499">В этой задаче предстоит добавить два класса модели для представления этих концепций: **Жанр** и **альбом**.</span><span class="sxs-lookup"><span data-stu-id="b648e-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="b648e-500">Если он еще не открыт, запустите **VS Express для Web**</span><span class="sxs-lookup"><span data-stu-id="b648e-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="b648e-501">В меню **файл** выберите команду **Открыть проект**.</span><span class="sxs-lookup"><span data-stu-id="b648e-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="b648e-502">В диалоговом окне Открытие проекта перейдите к **Source\Ex06-UsingParametersInView\Begin**, выберите **Begin. sln** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="b648e-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="b648e-503">Кроме того, вы можете продолжить работу с решением, полученным после завершения предыдущего упражнения.</span><span class="sxs-lookup"><span data-stu-id="b648e-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="b648e-504">Если вы открыли предоставленное **Начальное** решение, перед продолжением потребуется загрузить некоторые недостающие пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="b648e-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b648e-505">Для этого в меню **проект** выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b648e-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b648e-506">В диалоговом окне **Управление пакетами NuGet** нажмите кнопку **восстановить** , чтобы скачать недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="b648e-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b648e-507">Наконец, создайте решение, щелкнув **build** | **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="b648e-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b648e-508">Одним из преимуществ использования NuGet является то, что вам не нужно поставлять все библиотеки в проекте, уменьшая размер проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b648e-509">С помощью средств управления питанием NuGet, указав версии пакетов в файле Packages. config, вы сможете скачать все необходимые библиотеки при первом запуске проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b648e-510">Именно поэтому после открытия существующего решения из этой лабораторной работы потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b648e-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="b648e-511">Добавьте класс модели **жанра** .</span><span class="sxs-lookup"><span data-stu-id="b648e-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="b648e-512">Для этого щелкните правой кнопкой мыши папку **модели** в **Обозреватель решений**, выберите **Добавить** , а затем — **новый элемент** .</span><span class="sxs-lookup"><span data-stu-id="b648e-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="b648e-513">В разделе **код**выберите элемент **класса** и назовите файл *genre.CS*, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="b648e-514">![Добавление класса](aspnet-mvc-4-fundamentals/_static/image27.png "Добавление класса")</span><span class="sxs-lookup"><span data-stu-id="b648e-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="b648e-515">*Добавление нового элемента*</span><span class="sxs-lookup"><span data-stu-id="b648e-515">*Adding a new item*</span></span>

    <span data-ttu-id="b648e-516">![Добавление класса модели жанра](aspnet-mvc-4-fundamentals/_static/image28.png "Добавление класса модели жанра")</span><span class="sxs-lookup"><span data-stu-id="b648e-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="b648e-517">*Добавление класса модели жанра*</span><span class="sxs-lookup"><span data-stu-id="b648e-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="b648e-518">Добавьте свойство **Name** в класс жанра.</span><span class="sxs-lookup"><span data-stu-id="b648e-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="b648e-519">Для этого добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b648e-519">To do this, add the following code:</span></span>

    <span data-ttu-id="b648e-520">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex6-жанр*)</span><span class="sxs-lookup"><span data-stu-id="b648e-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="b648e-521">Следуя той же процедуре, что и ранее, добавьте класс **альбома** .</span><span class="sxs-lookup"><span data-stu-id="b648e-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="b648e-522">Для этого щелкните правой кнопкой мыши папку **модели** в **Обозреватель решений**, выберите **Добавить** , а затем — **новый элемент** .</span><span class="sxs-lookup"><span data-stu-id="b648e-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="b648e-523">В разделе **код**выберите элемент **класса** и назовите файл *Album.CS*, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="b648e-524">Добавьте два свойства в класс альбома: **Жанр** и **Title**.</span><span class="sxs-lookup"><span data-stu-id="b648e-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="b648e-525">Для этого добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b648e-525">To do this, add the following code:</span></span>

    <span data-ttu-id="b648e-526">(Фрагмент кода — *ASP.NET MVC 4 основы — альбом Ex6*)</span><span class="sxs-lookup"><span data-stu-id="b648e-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="b648e-527">Задача 2. Добавление Сторебровсевиевмодел</span><span class="sxs-lookup"><span data-stu-id="b648e-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="b648e-528">В этой задаче будет использоваться **сторебровсевиевмодел** для отображения альбомов, соответствующих выбранному жанру.</span><span class="sxs-lookup"><span data-stu-id="b648e-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="b648e-529">В этой задаче вы создадите этот класс, а затем добавите два свойства для обработка **жанра** и его списка **альбома**.</span><span class="sxs-lookup"><span data-stu-id="b648e-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="b648e-530">Добавьте класс **сторебровсевиевмодел** .</span><span class="sxs-lookup"><span data-stu-id="b648e-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="b648e-531">Для этого щелкните правой кнопкой мыши папку **ViewModels** в **Обозреватель решений**, выберите **Добавить** , а затем — **новый элемент** .</span><span class="sxs-lookup"><span data-stu-id="b648e-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="b648e-532">В разделе **код**выберите элемент **класса** и назовите файл *StoreBrowseViewModel.CS*, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="b648e-533">Добавьте ссылку на модели в классе **сторебровсевиевмодел** .</span><span class="sxs-lookup"><span data-stu-id="b648e-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="b648e-534">Для этого добавьте следующее с помощью пространства имен:</span><span class="sxs-lookup"><span data-stu-id="b648e-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="b648e-535">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex6 усингмодел*)</span><span class="sxs-lookup"><span data-stu-id="b648e-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="b648e-536">Добавьте два свойства в класс **сторебровсевиевмодел** : **Жанр** и **альбомы**.</span><span class="sxs-lookup"><span data-stu-id="b648e-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="b648e-537">Для этого добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b648e-537">To do this, add the following code:</span></span>

    <span data-ttu-id="b648e-538">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex6 моделпропертиес*)</span><span class="sxs-lookup"><span data-stu-id="b648e-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="b648e-539">Что такое **список&lt;альбом&gt;** ?. это определение использует тип **списка&lt;t&gt;** , где **t** ограничивает тип, к которому принадлежат элементы этого **списка** , в данном случае это **альбом** (или любой из его потомков).</span><span class="sxs-lookup"><span data-stu-id="b648e-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="b648e-540">Эта возможность разрабатывать классы и методы, которые откладывают спецификацию одного или нескольких типов до тех пор, пока класс или метод не будет объявлен и не будет создан с помощью C# клиентского кода, — является функцией языка, именуемого **универсальными**классами.</span><span class="sxs-lookup"><span data-stu-id="b648e-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="b648e-541">**List&lt;t&gt;** является универсальным эквивалентом типа **ArrayList** и доступен в пространстве имен **System. Collections. Generic** .</span><span class="sxs-lookup"><span data-stu-id="b648e-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="b648e-542">Одним из преимуществ использования **универсальных шаблонов** является то, что, поскольку тип задан, вам не нужно предпринимать такие операции проверки типов, как приведение элементов к **альбому** , как и в случае с **ArrayList**.</span><span class="sxs-lookup"><span data-stu-id="b648e-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="b648e-543">Задача 3. Использование нового ViewModel в Стореконтроллер</span><span class="sxs-lookup"><span data-stu-id="b648e-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="b648e-544">В этой задаче вы измените методы действия " **Обзор** " и **"подробности** " **Стореконтроллер**, чтобы использовать новый **сторебровсевиевмодел**.</span><span class="sxs-lookup"><span data-stu-id="b648e-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="b648e-545">Добавьте ссылку на папку Models в классе **стореконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="b648e-546">Для этого разверните папку **Controllers** в **Обозреватель решений** и откройте класс **стореконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="b648e-547">Затем добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b648e-547">Then add the following code:</span></span>

    <span data-ttu-id="b648e-548">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex6 усингмоделинконтроллер*)</span><span class="sxs-lookup"><span data-stu-id="b648e-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="b648e-549">Замените метод действия **Browse** для использования класса **сторевиевбровсеконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="b648e-550">Вы создадите жанр и два новых объекта альбомов с фиктивными данными (в следующей практической лабораторной работе вы будете использовать реальные данные из базы данных).</span><span class="sxs-lookup"><span data-stu-id="b648e-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="b648e-551">Для этого замените метод **Browse** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="b648e-552">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex6 бровсемесод*)</span><span class="sxs-lookup"><span data-stu-id="b648e-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="b648e-553">Замените метод действия **Details** , чтобы использовался класс **сторевиевбровсеконтроллер** .</span><span class="sxs-lookup"><span data-stu-id="b648e-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="b648e-554">Вы создадите новый объект **альбома** , который будет возвращен в **представление**.</span><span class="sxs-lookup"><span data-stu-id="b648e-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="b648e-555">Для этого замените метод **Details** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b648e-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="b648e-556">(Фрагмент кода — *основы ASP.NET MVC 4 — Ex6 детаилсмесод*)</span><span class="sxs-lookup"><span data-stu-id="b648e-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="b648e-557">Задача 4. Добавление шаблона представления обзора</span><span class="sxs-lookup"><span data-stu-id="b648e-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="b648e-558">В этой задаче будет добавлено представление **обзора** для отображения альбомов, найденных для определенного жанра.</span><span class="sxs-lookup"><span data-stu-id="b648e-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="b648e-559">Перед созданием нового шаблона представления необходимо выполнить сборку проекта, чтобы диалоговое окно **добавления представления** знало о том, какой класс **ViewModel** будет использовать.</span><span class="sxs-lookup"><span data-stu-id="b648e-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="b648e-560">Выполните сборку проекта, выбрав пункт меню **Сборка** , а затем — **сборку мвкмусиксторе**.</span><span class="sxs-lookup"><span data-stu-id="b648e-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="b648e-561">Добавьте представление **обзора** .</span><span class="sxs-lookup"><span data-stu-id="b648e-561">Add a **Browse** View.</span></span> <span data-ttu-id="b648e-562">Для этого щелкните правой кнопкой мыши метод действия **обзора** **стореконтроллер** и выберите команду **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="b648e-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="b648e-563">В диалоговом окне **Добавление представления** убедитесь, что имя представления является **обзором**.</span><span class="sxs-lookup"><span data-stu-id="b648e-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="b648e-564">Установите флажок **создать строго типизированное представление** и выберите **сторебровсевиевмодел** в раскрывающемся списке **класс модели** .</span><span class="sxs-lookup"><span data-stu-id="b648e-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="b648e-565">Оставьте в других полях значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b648e-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="b648e-566">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-566">Then click **Add**.</span></span>

    <span data-ttu-id="b648e-567">![Добавление представления обзора](aspnet-mvc-4-fundamentals/_static/image29.png "Добавление представления обзора")</span><span class="sxs-lookup"><span data-stu-id="b648e-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="b648e-568">*Добавление представления обзора*</span><span class="sxs-lookup"><span data-stu-id="b648e-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="b648e-569">Измените значение свойства **Browse. cshtml** , чтобы отобразить сведения о жанре и получить доступ к объекту **сторебровсевиевмодел** , который передается в шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="b648e-570">Для этого замените содержимое следующим: (C#).</span><span class="sxs-lookup"><span data-stu-id="b648e-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="b648e-571">Задача 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="b648e-572">В этой задаче вы проверите, что метод **Browse** извлекает альбомы из действия метода **Browse** .</span><span class="sxs-lookup"><span data-stu-id="b648e-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="b648e-573">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-574">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-574">The project starts in the Home page.</span></span> <span data-ttu-id="b648e-575">Изменить URL-адрес на **/Сторе/бровсе? Жанр = Disco** , чтобы убедиться, что действие возвращает два альбома.</span><span class="sxs-lookup"><span data-stu-id="b648e-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="b648e-576">![Обзор хранилищ альбомов Disco](aspnet-mvc-4-fundamentals/_static/image30.png "Обзор хранилищ альбомов Disco")</span><span class="sxs-lookup"><span data-stu-id="b648e-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="b648e-577">*Обзор хранилищ альбомов Disco*</span><span class="sxs-lookup"><span data-stu-id="b648e-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="b648e-578">Задача 6. Отображение сведений о конкретном альбоме</span><span class="sxs-lookup"><span data-stu-id="b648e-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="b648e-579">В этой задаче будет реализовано представление **Store/Details** для отображения сведений о конкретном альбоме.</span><span class="sxs-lookup"><span data-stu-id="b648e-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="b648e-580">В этой практической лабораторной работе все отображаемые сведения о альбоме уже содержатся в шаблоне **представления** .</span><span class="sxs-lookup"><span data-stu-id="b648e-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="b648e-581">Таким образом, вместо создания класса **сторедетаилсвиевмодел** будет использоваться текущий шаблон **сторебровсевиевмодел** , передающий в него альбом.</span><span class="sxs-lookup"><span data-stu-id="b648e-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="b648e-582">При необходимости закройте браузер, чтобы вернуться в окно Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="b648e-583">Добавьте новое представление **сведений** для метода действия **Details** **стореконтроллер**.</span><span class="sxs-lookup"><span data-stu-id="b648e-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="b648e-584">Для этого щелкните правой кнопкой мыши метод **Details** в классе **Стореконтроллер** и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="b648e-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="b648e-585">В диалоговом окне **Добавление представления** убедитесь, что **имя представления** содержит **сведения**.</span><span class="sxs-lookup"><span data-stu-id="b648e-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="b648e-586">Установите флажок **создать строго типизированное представление** и выберите **альбом** в раскрывающемся списке **класс модели** .</span><span class="sxs-lookup"><span data-stu-id="b648e-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="b648e-587">Оставьте в других полях значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b648e-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="b648e-588">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b648e-588">Then click **Add**.</span></span> <span data-ttu-id="b648e-589">Будет создан и открыт файл **\виевс\сторе\детаилс.кштмл** .</span><span class="sxs-lookup"><span data-stu-id="b648e-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="b648e-590">![Добавление подробного представления](aspnet-mvc-4-fundamentals/_static/image31.png "Добавление подробного представления")</span><span class="sxs-lookup"><span data-stu-id="b648e-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="b648e-591">*Добавление подробного представления*</span><span class="sxs-lookup"><span data-stu-id="b648e-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="b648e-592">Измените файл **Details. cshtml** , чтобы отобразить сведения об альбоме, доступ к объекту **альбома** , который передается в шаблон представления.</span><span class="sxs-lookup"><span data-stu-id="b648e-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="b648e-593">Для этого замените содержимое следующим: (C#).</span><span class="sxs-lookup"><span data-stu-id="b648e-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="b648e-594">Задача 7. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="b648e-595">В этой задаче вы проверите, что представление **Details** извлекает сведения о альбоме из метода **действия Details** .</span><span class="sxs-lookup"><span data-stu-id="b648e-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="b648e-596">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-597">Проект начинается на **домашней** странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="b648e-598">Измените URL-адрес на **/Store/Details/5** , чтобы проверить сведения об альбоме.</span><span class="sxs-lookup"><span data-stu-id="b648e-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="b648e-599">![Просмотр сведений о альбомах](aspnet-mvc-4-fundamentals/_static/image32.png "Просмотр сведений о альбомах")</span><span class="sxs-lookup"><span data-stu-id="b648e-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="b648e-600">*Просмотр сведений о альбоме*</span><span class="sxs-lookup"><span data-stu-id="b648e-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="b648e-601">Задача 8. Добавление ссылок между страницами</span><span class="sxs-lookup"><span data-stu-id="b648e-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="b648e-602">В этой задаче вы добавите ссылку в представление хранилища, чтобы ссылка в каждом имени жанра соответствовала соответствующему URL-адресу **/Сторе/бровсе** .</span><span class="sxs-lookup"><span data-stu-id="b648e-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="b648e-603">Таким образом, если щелкнуть жанр, например **Disco**, он будет переходить к URL-адресу **/Сторе/бровсе? жанр = Disco** .</span><span class="sxs-lookup"><span data-stu-id="b648e-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="b648e-604">При необходимости закройте браузер, чтобы вернуться в окно Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="b648e-605">Обновите страницу **индекса** , чтобы добавить ссылку на страницу **обзора** .</span><span class="sxs-lookup"><span data-stu-id="b648e-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="b648e-606">Для этого в **Обозреватель решений** разверните папку **представления** , а затем папку **Store** и дважды щелкните страницу **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="b648e-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="b648e-607">Добавьте ссылку на представление "Обзор", указывающее на выбранный жанр.</span><span class="sxs-lookup"><span data-stu-id="b648e-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="b648e-608">Для этого замените следующий выделенный код в **&lt;li&gt;** тегов: (C#)</span><span class="sxs-lookup"><span data-stu-id="b648e-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="b648e-609">другой подход будет напрямую связываться со страницей с кодом, подобным следующему:</span><span class="sxs-lookup"><span data-stu-id="b648e-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="b648e-610">&lt;a href =&quot;/Сторе/бровсе? жанр =@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="b648e-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="b648e-611">Хотя этот подход работает, он зависит от жестко закодированной строки.</span><span class="sxs-lookup"><span data-stu-id="b648e-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="b648e-612">Если впоследствии вы переименуете контроллер, вам придется изменить эту инструкцию вручную.</span><span class="sxs-lookup"><span data-stu-id="b648e-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="b648e-613">Лучшим вариантом является использование **вспомогательного метода HTML** .</span><span class="sxs-lookup"><span data-stu-id="b648e-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="b648e-614">ASP.NET MVC включает вспомогательный метод HTML, доступный для таких задач.</span><span class="sxs-lookup"><span data-stu-id="b648e-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="b648e-615">Вспомогательный метод **HTML. ActionLink ()** упрощает создание Html- **&lt;&gt;** ссылок, обеспечивая правильность кодирования URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="b648e-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="b648e-616">В HTML. ActionLink имеется несколько перегрузок.</span><span class="sxs-lookup"><span data-stu-id="b648e-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="b648e-617">В этом упражнении вы будете использовать его, который принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="b648e-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="b648e-618">Текст ссылки, в котором отображается название жанра</span><span class="sxs-lookup"><span data-stu-id="b648e-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="b648e-619">Имя действия контроллера (**Обзор**)</span><span class="sxs-lookup"><span data-stu-id="b648e-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="b648e-620">Значения параметров маршрута, в которых указывается как имя (**Жанр**), так и значение (**Название жанра**).</span><span class="sxs-lookup"><span data-stu-id="b648e-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="b648e-621">Задача 9. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="b648e-622">В этой задаче вы проверите, что каждый жанр отображается со ссылкой на соответствующий URL-адрес **/Сторе/бровсе** .</span><span class="sxs-lookup"><span data-stu-id="b648e-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="b648e-623">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-624">Проект начинается на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-624">The project starts in the Home page.</span></span> <span data-ttu-id="b648e-625">Измените URL-адрес на **/Store** , чтобы убедиться, что каждый жанр ссылается на соответствующий URL-адрес **/Сторе/бровсе** .</span><span class="sxs-lookup"><span data-stu-id="b648e-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="b648e-626">![Просмотр жанров со ссылками на страницу обзора](aspnet-mvc-4-fundamentals/_static/image33.png "Просмотр жанров со ссылками на страницу обзора")</span><span class="sxs-lookup"><span data-stu-id="b648e-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="b648e-627">*Просмотр жанров со ссылками на страницу обзора*</span><span class="sxs-lookup"><span data-stu-id="b648e-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="b648e-628">Задача 10. Использование динамической коллекции ViewModel для передачи значений</span><span class="sxs-lookup"><span data-stu-id="b648e-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="b648e-629">В этой задаче вы узнаете простой и мощный метод передачи значений между контроллером и представлением без внесения каких-либо изменений в модель.</span><span class="sxs-lookup"><span data-stu-id="b648e-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="b648e-630">ASP.NET MVC 4 предоставляет коллекцию &quot;ViewModel&quot;, которая может быть назначена любому динамическому значению и доступна также в контроллерах и представлениях.</span><span class="sxs-lookup"><span data-stu-id="b648e-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="b648e-631">Теперь вы будете использовать динамическую коллекцию ViewBag для передачи списка&quot;ных **жанров &quot;звездочками** из контроллера в представление.</span><span class="sxs-lookup"><span data-stu-id="b648e-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="b648e-632">Представление индекса магазина будет иметь доступ к **ViewModel** и отображать сведения.</span><span class="sxs-lookup"><span data-stu-id="b648e-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="b648e-633">При необходимости закройте браузер, чтобы вернуться в окно Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="b648e-634">Откройте **StoreController.CS** и измените метод **index** , чтобы создать список жанров звездочками в коллекции ViewModel:</span><span class="sxs-lookup"><span data-stu-id="b648e-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="b648e-635">Для доступа к свойствам можно также использовать синтаксис **ViewBag [&quot;звездочками&quot;]** .</span><span class="sxs-lookup"><span data-stu-id="b648e-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="b648e-636">Значок звездочки **&quot;звездочками. png&quot;** включен в папку **саурце\ассетс\имажес** этой лабораторной работы.</span><span class="sxs-lookup"><span data-stu-id="b648e-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="b648e-637">Чтобы добавить его в приложение, перетащите его содержимое из окна **проводника Windows** в **Обозреватель решений** в Visual Web Developer Express, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b648e-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="b648e-638">![Добавление изображения Star в решение](aspnet-mvc-4-fundamentals/_static/image34.png "Добавление изображения Star в решение")</span><span class="sxs-lookup"><span data-stu-id="b648e-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="b648e-639">*Добавление изображения Star в решение*</span><span class="sxs-lookup"><span data-stu-id="b648e-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="b648e-640">Откройте представление **store/index. cshtml** и измените содержимое.</span><span class="sxs-lookup"><span data-stu-id="b648e-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="b648e-641">Вы прочитаете свойство &quot;звездочками&quot; в коллекции **ViewBag** и спросите, есть ли имя текущего жанра в списке.</span><span class="sxs-lookup"><span data-stu-id="b648e-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="b648e-642">В этом случае вы увидите значок звездочки справа по ссылке на жанр.</span><span class="sxs-lookup"><span data-stu-id="b648e-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="b648e-643">C#</span><span class="sxs-lookup"><span data-stu-id="b648e-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="b648e-644">Задача 11. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b648e-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="b648e-645">В этой задаче вы проверите, что жанры звездочками отображают значок звездочки.</span><span class="sxs-lookup"><span data-stu-id="b648e-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="b648e-646">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b648e-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="b648e-647">Проект начинается на **домашней** странице.</span><span class="sxs-lookup"><span data-stu-id="b648e-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="b648e-648">Измените URL-адрес на **/Store** , чтобы убедиться, что каждый рекомендуемый жанр имеет метку соответствия:</span><span class="sxs-lookup"><span data-stu-id="b648e-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="b648e-649">![Просмотр жанров с помощью элементов звездочками](aspnet-mvc-4-fundamentals/_static/image35.png "Просмотр жанров с помощью элементов звездочками")</span><span class="sxs-lookup"><span data-stu-id="b648e-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="b648e-650">*Просмотр жанров с помощью элементов звездочками*</span><span class="sxs-lookup"><span data-stu-id="b648e-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="b648e-651">Упражнение 7. Создание шаблона на основе ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b648e-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="b648e-652">В этом упражнении вы изучите усовершенствования в шаблонах проектов ASP.NET MVC 4, используя наиболее важные возможности нового шаблона.</span><span class="sxs-lookup"><span data-stu-id="b648e-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="b648e-653">Задача 1. изучение шаблона Интернет приложения ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b648e-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="b648e-654">Если он еще не открыт, запустите **VS Express для Web**</span><span class="sxs-lookup"><span data-stu-id="b648e-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="b648e-655">Выберите **файл | Создать |** Команда меню "проект".</span><span class="sxs-lookup"><span data-stu-id="b648e-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="b648e-656">В диалоговом окне **Новый проект** выберите **визуальный C#элемент |** В дереве слева щелкните веб-шаблон и выберите **веб-приложение ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="b648e-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="b648e-657">**Назовите** проект *мусиксторе* и обновите **имя решения** , чтобы *начать*, затем выберите расположение (или оставьте значение по умолчанию) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b648e-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="b648e-658">![Создание нового проекта ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image36.png "Создание нового проекта ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="b648e-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="b648e-659">*Создание нового проекта ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="b648e-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="b648e-660">В диалоговом окне **Новый проект ASP.NET MVC 4** выберите шаблон проекта **Интернет приложение** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b648e-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="b648e-661">Обратите внимание, что в качестве обработчика представлений можно выбрать Razor или ASPX.</span><span class="sxs-lookup"><span data-stu-id="b648e-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="b648e-662">![Создание нового Интернет-приложения ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image37.png "Создание нового Интернет-приложения ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="b648e-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="b648e-663">*Создание нового Интернет-приложения ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="b648e-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-664">Синтаксис Razor представлен в ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="b648e-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="b648e-665">Его целью является сокращение количества символов и нажатий клавиш, необходимых в файле, что позволяет быстро и гибко создавать рабочие процессы кодирования.</span><span class="sxs-lookup"><span data-stu-id="b648e-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="b648e-666">Razor использует существующие C#навыки языка/VB (или другие) и предоставляет синтаксис разметки шаблона, который позволяет создавать восходящий рабочий процесс создания HTML-кода.</span><span class="sxs-lookup"><span data-stu-id="b648e-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="b648e-667">Нажмите клавишу **F5** , чтобы запустить решение и просмотреть обновленный шаблон.</span><span class="sxs-lookup"><span data-stu-id="b648e-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="b648e-668">Вы можете узнать о следующих функциях:</span><span class="sxs-lookup"><span data-stu-id="b648e-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="b648e-669">**Шаблоны современных стилей**</span><span class="sxs-lookup"><span data-stu-id="b648e-669">**Modern-style templates**</span></span>

        <span data-ttu-id="b648e-670">Шаблоны были обновлены, предоставляя более современные стили.</span><span class="sxs-lookup"><span data-stu-id="b648e-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="b648e-671">![Шаблоны с ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image38.png "Шаблоны с ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="b648e-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="b648e-672">*Шаблоны с ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="b648e-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="b648e-673">**Адаптивная визуализация**</span><span class="sxs-lookup"><span data-stu-id="b648e-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="b648e-674">Изучите изменение размера окна браузера и обратите внимание, что макет страницы динамически адаптируется к новому размеру окна.</span><span class="sxs-lookup"><span data-stu-id="b648e-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="b648e-675">Эти шаблоны используют метод адаптивной отрисовки для правильной отрисовки на настольных и мобильных платформах без каких бы то ни было настроек.</span><span class="sxs-lookup"><span data-stu-id="b648e-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="b648e-676">![Шаблон проекта ASP.NET MVC 4 в разных размерах браузера](aspnet-mvc-4-fundamentals/_static/image39.png "Шаблон проекта ASP.NET MVC 4 в разных размерах браузера")</span><span class="sxs-lookup"><span data-stu-id="b648e-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="b648e-677">*Шаблон проекта ASP.NET MVC 4 в разных размерах браузера*</span><span class="sxs-lookup"><span data-stu-id="b648e-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="b648e-678">Закройте браузер, чтобы завершить работу отладчика и вернуться в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="b648e-679">Теперь вы можете исследовать решение и ознакомиться с новыми функциями, появившимися в ASP.NET MVC 4 в шаблоне проекта.</span><span class="sxs-lookup"><span data-stu-id="b648e-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="b648e-680">![ASP.NET MVC4-Internet-Application-Project-Template](aspnet-mvc-4-fundamentals/_static/image40.png "Шаблон проекта Интернет приложения ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="b648e-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="b648e-681">*Шаблон проекта Интернет приложения ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="b648e-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="b648e-682">**Разметка HTML5**</span><span class="sxs-lookup"><span data-stu-id="b648e-682">**HTML5 markup**</span></span>

       <span data-ttu-id="b648e-683">Просмотрите представления шаблонов, чтобы узнать новую разметку темы, например открыть представление **About. cshtml** в **домашней** папке.</span><span class="sxs-lookup"><span data-stu-id="b648e-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="b648e-684">![Новый шаблон с использованием разметки Razor и HTML5](aspnet-mvc-4-fundamentals/_static/image41.png "Новый шаблон с использованием разметки Razor и HTML5")</span><span class="sxs-lookup"><span data-stu-id="b648e-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="b648e-685">*Новый шаблон с использованием разметки Razor и HTML5*</span><span class="sxs-lookup"><span data-stu-id="b648e-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="b648e-686">**Включаемые библиотеки JavaScript**</span><span class="sxs-lookup"><span data-stu-id="b648e-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="b648e-687">**jQuery**: jQuery упрощает обход документов HTML, обработку событий, анимацию и взаимодействие AJAX.</span><span class="sxs-lookup"><span data-stu-id="b648e-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="b648e-688">**Пользовательский интерфейс jQuery**. Эта библиотека предоставляет абстракции для низкоуровневого взаимодействия и анимации, расширенные эффекты и тематические мини-приложения, созданные на основе библиотеки jQuery JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b648e-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="b648e-689">Сведения о jQuery и пользовательском интерфейсе jQuery можно узнать в [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="b648e-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="b648e-690">**KnockoutJS**. шаблон ASP.NET MVC 4 по умолчанию теперь включает **KnockoutJS**, платформу JavaScript MVVM, которая позволяет создавать многофункциональные и высокоэффективные веб-приложения с помощью JavaScript и HTML.</span><span class="sxs-lookup"><span data-stu-id="b648e-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="b648e-691">Как и в ASP.NET MVC 3, библиотеки пользовательского интерфейса jQuery и jQuery также включены в ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b648e-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="b648e-692">Дополнительные сведения о библиотеке KnockOutJS можно получить по этой ссылке: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="b648e-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="b648e-693">**Modernizr**: Эта библиотека запускается автоматически, делая сайт совместимым с более старыми браузерами при использовании технологий HTML5 и CSS3.</span><span class="sxs-lookup"><span data-stu-id="b648e-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="b648e-694">Дополнительные сведения о библиотеке Modernizr можно получить по этой ссылке: [http://www.modernizr.com/](http://www.modernizr.com/).</span><span class="sxs-lookup"><span data-stu-id="b648e-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="b648e-695">**Симплемембершип, включаемые в решение**</span><span class="sxs-lookup"><span data-stu-id="b648e-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="b648e-696">Симплемембершип был разработан в качестве замены для предыдущей ASP.NET роли и системы поставщика членства.</span><span class="sxs-lookup"><span data-stu-id="b648e-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="b648e-697">В нем реализовано множество новых функций, упрощающих защиту веб-страниц разработчиками более гибким способом.</span><span class="sxs-lookup"><span data-stu-id="b648e-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="b648e-698">В шаблоне Интернета уже настроено несколько вещей для интеграции Симплемембершип, например, AccountController подготовлена к использованию Оаусвебсекурити (для регистрации учетной записи OAuth, входа, управления и т. д.) и веб-безопасности.</span><span class="sxs-lookup"><span data-stu-id="b648e-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="b648e-699">![Симплемембершип, включаемые в решение](aspnet-mvc-4-fundamentals/_static/image42.png "Симплемембершип, включаемые в решение")</span><span class="sxs-lookup"><span data-stu-id="b648e-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="b648e-700">*Симплемембершип, включаемые в решение*</span><span class="sxs-lookup"><span data-stu-id="b648e-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="b648e-701">Дополнительные сведения о [оаусвебсекурити](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) см. на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="b648e-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="b648e-702">Кроме того, это приложение можно развернуть на веб-сайтах Windows Azure в [приложении б: Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="b648e-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b648e-703">Сводка</span><span class="sxs-lookup"><span data-stu-id="b648e-703">Summary</span></span>

<span data-ttu-id="b648e-704">Выполняя эту практическую лабораторию, вы узнали об основах ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="b648e-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="b648e-705">Основные элементы приложения MVC и их взаимодействие</span><span class="sxs-lookup"><span data-stu-id="b648e-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="b648e-706">Создание приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b648e-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="b648e-707">Добавление и настройка контроллеров для управления параметрами, передаваемыми по URL-адресу и строке запроса</span><span class="sxs-lookup"><span data-stu-id="b648e-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="b648e-708">Добавление главной страницы макета для настройки шаблона для общего содержимого HTML, таблицы стилей для улучшения внешнего вида и шаблона представления для отображения HTML-содержимого</span><span class="sxs-lookup"><span data-stu-id="b648e-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="b648e-709">Как использовать шаблон ViewModel для передачи свойств в шаблон представления для отображения динамической информации</span><span class="sxs-lookup"><span data-stu-id="b648e-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="b648e-710">Использование параметров, передаваемых контроллерам в шаблоне представления</span><span class="sxs-lookup"><span data-stu-id="b648e-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="b648e-711">Добавление ссылок на страницы в приложении MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b648e-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="b648e-712">Добавление и использование динамических свойств в представлении</span><span class="sxs-lookup"><span data-stu-id="b648e-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="b648e-713">Улучшения в шаблонах проектов ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b648e-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="b648e-714">Приложение а. Установка Visual Studio Express 2012 для Web</span><span class="sxs-lookup"><span data-stu-id="b648e-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="b648e-715">Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версии с помощью **[установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="b648e-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="b648e-716">Следующие инструкции помогут вам выполнить действия, необходимые для установки *Visual Studio Express 2012 для Web* с помощью *установщик веб-платформы Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="b648e-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="b648e-717">Перейдите в [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="b648e-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="b648e-718">Кроме того, если у вас уже установлен установщик веб-платформы, вы можете открыть его и найти продукт &quot;<em>Visual Studio Express 2012 для Web с Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="b648e-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="b648e-719">Щелкните **Install Now (установить сейчас**).</span><span class="sxs-lookup"><span data-stu-id="b648e-719">Click on **Install Now**.</span></span> <span data-ttu-id="b648e-720">Если у вас нет **установщика веб-платформы** , вы будете сначала перенаправлены на загрузку и установку.</span><span class="sxs-lookup"><span data-stu-id="b648e-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="b648e-721">После открытия **установщика веб-платформы** нажмите кнопку **установить** , чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="b648e-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="b648e-722">![Установка Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Установка Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="b648e-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="b648e-723">*Установка Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="b648e-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="b648e-724">Прочитайте все лицензии и условия продуктов и нажмите кнопку " **принять** ", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="b648e-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Принятие условий лицензии](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="b648e-726">*Принятие условий лицензии*</span><span class="sxs-lookup"><span data-stu-id="b648e-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="b648e-727">Дождитесь завершения процесса загрузки и установки.</span><span class="sxs-lookup"><span data-stu-id="b648e-727">Wait until the downloading and installation process completes.</span></span>

    ![Ход установки](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="b648e-729">*Ход установки*</span><span class="sxs-lookup"><span data-stu-id="b648e-729">*Installation progress*</span></span>
6. <span data-ttu-id="b648e-730">После завершения установки нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b648e-730">When the installation completes, click **Finish**.</span></span>

    ![Установка завершена](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="b648e-732">*Установка завершена*</span><span class="sxs-lookup"><span data-stu-id="b648e-732">*Installation completed*</span></span>
7. <span data-ttu-id="b648e-733">Нажмите кнопку **выход** , чтобы закрыть установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="b648e-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="b648e-734">Чтобы открыть Visual Studio Express для Интернета, перейдите на **начальный** экран и начните запись &quot;**VS Express**&quot;, а затем щелкните плитку **VS Express для Web** .</span><span class="sxs-lookup"><span data-stu-id="b648e-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Плитка VS Express для Web](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="b648e-736">*Плитка VS Express для Web*</span><span class="sxs-lookup"><span data-stu-id="b648e-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="b648e-737">Приложение б. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="b648e-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="b648e-738">В этом приложении показано, как создать новый веб-сайт из портал управления Windows Azure и опубликовать полученное приложение, выполнив следующие лабораторные занятия, используя возможности публикации веб-развертывание, предоставляемые Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b648e-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="b648e-739">Задача 1. Создание нового веб-сайта на портале Windows Azure</span><span class="sxs-lookup"><span data-stu-id="b648e-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="b648e-740">Перейдите в [портал управления Windows Azure](https://manage.windowsazure.com/) и выполните вход с использованием учетных данных Майкрософт, связанных с подпиской.</span><span class="sxs-lookup"><span data-stu-id="b648e-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-741">С помощью Windows Azure можно бесплатно разместить 10 веб-сайтов ASP.NET, а затем масштабировать их по мере роста объема трафика.</span><span class="sxs-lookup"><span data-stu-id="b648e-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="b648e-742">Вы можете зарегистрироваться [здесь](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="b648e-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="b648e-743">![Вход в Windows портал Azure](aspnet-mvc-4-fundamentals/_static/image48.png "Вход в Windows портал Azure")</span><span class="sxs-lookup"><span data-stu-id="b648e-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="b648e-744">*Вход в Windows Azure портал управления*</span><span class="sxs-lookup"><span data-stu-id="b648e-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="b648e-745">На панели команд щелкните **создать** .</span><span class="sxs-lookup"><span data-stu-id="b648e-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="b648e-746">![Создание нового веб-сайта](aspnet-mvc-4-fundamentals/_static/image49.png "Создание нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="b648e-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="b648e-747">*Создание нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="b648e-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="b648e-748">Щелкните **Compute** | **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="b648e-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="b648e-749">Затем выберите пункт **Быстрое создание** .</span><span class="sxs-lookup"><span data-stu-id="b648e-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="b648e-750">Предоставьте доступный URL-адрес для нового веб-сайта и щелкните **создать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="b648e-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-751">Веб-сайт Windows Azure — это узел для веб-приложения, работающего в облаке, которыми можно управлять и которыми вы управляете.</span><span class="sxs-lookup"><span data-stu-id="b648e-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="b648e-752">Параметр Быстрое создание позволяет развернуть завершенное веб-приложение на веб-сайте Windows Azure извне портала.</span><span class="sxs-lookup"><span data-stu-id="b648e-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="b648e-753">Он не включает шаги по настройке базы данных.</span><span class="sxs-lookup"><span data-stu-id="b648e-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="b648e-754">![Создание нового веб-сайта с помощью быстрого создания](aspnet-mvc-4-fundamentals/_static/image50.png "Создание нового веб-сайта с помощью быстрого создания")</span><span class="sxs-lookup"><span data-stu-id="b648e-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="b648e-755">*Создание нового веб-сайта с помощью быстрого создания*</span><span class="sxs-lookup"><span data-stu-id="b648e-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="b648e-756">Дождитесь создания нового **веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="b648e-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="b648e-757">После создания веб-сайта щелкните ссылку в столбце **URL-адрес** .</span><span class="sxs-lookup"><span data-stu-id="b648e-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="b648e-758">Убедитесь, что новый веб-сайт работает.</span><span class="sxs-lookup"><span data-stu-id="b648e-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="b648e-759">![Обзор нового веб-сайта](aspnet-mvc-4-fundamentals/_static/image51.png "Обзор нового веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="b648e-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="b648e-760">*Обзор нового веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="b648e-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="b648e-761">![Веб-сайт работает](aspnet-mvc-4-fundamentals/_static/image52.png "Веб-сайт работает")</span><span class="sxs-lookup"><span data-stu-id="b648e-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="b648e-762">*Веб-сайт работает*</span><span class="sxs-lookup"><span data-stu-id="b648e-762">*Web site running*</span></span>
6. <span data-ttu-id="b648e-763">Вернитесь на портал и щелкните имя веб-сайта в столбце **имя** , чтобы отобразить страницы управления.</span><span class="sxs-lookup"><span data-stu-id="b648e-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="b648e-764">![Открытие страниц управления веб-сайтом](aspnet-mvc-4-fundamentals/_static/image53.png "Открытие страниц управления веб-сайтом")</span><span class="sxs-lookup"><span data-stu-id="b648e-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="b648e-765">*Открытие страниц управления веб-сайтом*</span><span class="sxs-lookup"><span data-stu-id="b648e-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="b648e-766">На странице **панель мониторинга** в разделе **краткий обзор** щелкните ссылку **скачать профиль публикации** .</span><span class="sxs-lookup"><span data-stu-id="b648e-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-767">*Профиль публикации* содержит все сведения, необходимые для публикации веб-приложения на веб-сайте Windows Azure для каждого включенного метода публикации.</span><span class="sxs-lookup"><span data-stu-id="b648e-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="b648e-768">Профиль публикации содержит URL-адреса, учетные данные пользователей и строки для открытия базы данных, которые необходимы для проверки подлинности и подключения к каждой из конечных точек, соответствующей разрешенному методу публикации.</span><span class="sxs-lookup"><span data-stu-id="b648e-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="b648e-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express для Web** и **Microsoft Visual Studio 2012** поддерживают чтение профилей публикации для автоматизации настройки этих программ для публикации веб-приложений на веб-сайтах Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b648e-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="b648e-770">![Скачивание профиля публикации веб-сайта](aspnet-mvc-4-fundamentals/_static/image54.png "Скачивание профиля публикации веб-сайта")</span><span class="sxs-lookup"><span data-stu-id="b648e-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="b648e-771">*Скачивание профиля публикации веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="b648e-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="b648e-772">Скачайте файл профиля публикации в известное расположение.</span><span class="sxs-lookup"><span data-stu-id="b648e-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="b648e-773">Далее в этом упражнении вы узнаете, как использовать этот файл для публикации веб-приложения на веб-сайтах Windows Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b648e-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="b648e-774">![Сохранение файла профиля публикации](aspnet-mvc-4-fundamentals/_static/image55.png "Сохранение профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="b648e-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="b648e-775">*Сохранение файла профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="b648e-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="b648e-776">Задача 2. Настройка сервера базы данных</span><span class="sxs-lookup"><span data-stu-id="b648e-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="b648e-777">Если приложение использует SQL Server базы данных, потребуется создать сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b648e-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="b648e-778">Если вы хотите развернуть простое приложение, которое не использует SQL Server вы можете пропустить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="b648e-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="b648e-779">Для хранения базы данных приложения необходим сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b648e-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="b648e-780">Серверы базы данных SQL можно просмотреть в подписке на портале управления Windows Azure в **базах данных sql** | **серверы** | **панели мониторинга сервера**.</span><span class="sxs-lookup"><span data-stu-id="b648e-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="b648e-781">Если сервер не создан, можно создать его с помощью кнопки **Добавить** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="b648e-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="b648e-782">Запишите **имя сервера и URL-адрес, имя для входа администратора и пароль**, так как они будут использоваться в следующих задачах.</span><span class="sxs-lookup"><span data-stu-id="b648e-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="b648e-783">Пока не создавайте базу данных, так как она будет создана на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="b648e-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="b648e-784">![Панель мониторинга сервера базы данных SQL](aspnet-mvc-4-fundamentals/_static/image56.png "Панель мониторинга сервера базы данных SQL")</span><span class="sxs-lookup"><span data-stu-id="b648e-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="b648e-785">*Панель мониторинга сервера базы данных SQL*</span><span class="sxs-lookup"><span data-stu-id="b648e-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="b648e-786">В следующей задаче вы проверите подключение к базе данных из Visual Studio. по этой причине необходимо включить локальный IP-адрес в список **разрешенных IP-адресов**сервера.</span><span class="sxs-lookup"><span data-stu-id="b648e-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="b648e-787">Для этого нажмите кнопку **настроить**, выберите IP-адрес из **текущего IP-адреса клиента** и вставьте его в текстовые поля **начальный IP-адрес** и **конечный IP** -адрес и нажмите кнопку ![добавить-клиент-IP – адрес-OK-кнопка](aspnet-mvc-4-fundamentals/_static/image57.png).</span><span class="sxs-lookup"><span data-stu-id="b648e-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![Добавление IP-адреса клиента](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="b648e-789">*Добавление IP-адреса клиента*</span><span class="sxs-lookup"><span data-stu-id="b648e-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="b648e-790">После добавления **IP-адреса клиента** в список Разрешенные IP-адреса нажмите кнопку **сохранить** , чтобы подтвердить изменения.</span><span class="sxs-lookup"><span data-stu-id="b648e-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Подтверждение изменений](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="b648e-792">*Подтверждение изменений*</span><span class="sxs-lookup"><span data-stu-id="b648e-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="b648e-793">Задача 3. Публикация приложения ASP.NET MVC 4 с помощью веб-развертывание</span><span class="sxs-lookup"><span data-stu-id="b648e-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="b648e-794">Вернитесь к решению ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b648e-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="b648e-795">В **Обозреватель решений**щелкните правой кнопкой мыши проект веб-сайта и выберите **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b648e-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="b648e-796">![Публикация приложения](aspnet-mvc-4-fundamentals/_static/image60.png "Публикация приложения")</span><span class="sxs-lookup"><span data-stu-id="b648e-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="b648e-797">*Публикация веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="b648e-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="b648e-798">Импортируйте профиль публикации, сохраненный в первой задаче.</span><span class="sxs-lookup"><span data-stu-id="b648e-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="b648e-799">![Импорт профиля публикации](aspnet-mvc-4-fundamentals/_static/image61.png "Импорт профиля публикации")</span><span class="sxs-lookup"><span data-stu-id="b648e-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="b648e-800">*Импорт профиля публикации*</span><span class="sxs-lookup"><span data-stu-id="b648e-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="b648e-801">Щелкните **проверить подключение**.</span><span class="sxs-lookup"><span data-stu-id="b648e-801">Click **Validate Connection**.</span></span> <span data-ttu-id="b648e-802">После завершения проверки нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b648e-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b648e-803">Проверка завершится, когда появится зеленая галочка рядом с кнопкой проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="b648e-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="b648e-804">![Проверка подключения](aspnet-mvc-4-fundamentals/_static/image62.png "Проверка подключения")</span><span class="sxs-lookup"><span data-stu-id="b648e-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="b648e-805">*Проверка подключения*</span><span class="sxs-lookup"><span data-stu-id="b648e-805">*Validating connection*</span></span>
4. <span data-ttu-id="b648e-806">На странице **Параметры** в разделе **базы данных** нажмите кнопку рядом с текстовым полем подключения к базе данных (т. е. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="b648e-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="b648e-807">![Конфигурация веб-развертывания](aspnet-mvc-4-fundamentals/_static/image63.png "Конфигурация веб-развертывания")</span><span class="sxs-lookup"><span data-stu-id="b648e-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="b648e-808">*Конфигурация веб-развертывания*</span><span class="sxs-lookup"><span data-stu-id="b648e-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="b648e-809">Настройте подключение к базе данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b648e-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="b648e-810">В поле **имя сервера** введите URL-адрес сервера базы данных SQL с помощью префикса *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="b648e-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="b648e-811">В окне **имя пользователя** введите имя для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="b648e-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="b648e-812">В окне **пароль** введите пароль для входа администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="b648e-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="b648e-813">Введите имя новой базы данных, например: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="b648e-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="b648e-814">![Настройка строки подключения к целевому объекту](aspnet-mvc-4-fundamentals/_static/image64.png "Настройка строки подключения к целевому объекту")</span><span class="sxs-lookup"><span data-stu-id="b648e-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="b648e-815">*Настройка строки подключения к целевому объекту*</span><span class="sxs-lookup"><span data-stu-id="b648e-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="b648e-816">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b648e-816">Then click **OK**.</span></span> <span data-ttu-id="b648e-817">При появлении запроса на создание базы данных нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="b648e-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="b648e-818">![Создание базы данных](aspnet-mvc-4-fundamentals/_static/image65.png "Создание строки базы данных")</span><span class="sxs-lookup"><span data-stu-id="b648e-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="b648e-819">*Создание базы данных*</span><span class="sxs-lookup"><span data-stu-id="b648e-819">*Creating the database*</span></span>
7. <span data-ttu-id="b648e-820">Строка подключения, которая будет использоваться для подключения к базе данных SQL в Windows Azure, отображается в текстовом поле подключения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b648e-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="b648e-821">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b648e-821">Then click **Next**.</span></span>

    <span data-ttu-id="b648e-822">![Строка подключения, указывающая на базу данных SQL](aspnet-mvc-4-fundamentals/_static/image66.png "Строка подключения, указывающая на базу данных SQL")</span><span class="sxs-lookup"><span data-stu-id="b648e-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="b648e-823">*Строка подключения, указывающая на базу данных SQL*</span><span class="sxs-lookup"><span data-stu-id="b648e-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="b648e-824">На странице **Предварительный просмотр** нажмите кнопку **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b648e-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="b648e-825">![Публикация веб-приложения](aspnet-mvc-4-fundamentals/_static/image67.png "Публикация веб-приложения")</span><span class="sxs-lookup"><span data-stu-id="b648e-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="b648e-826">*Публикация веб-приложения*</span><span class="sxs-lookup"><span data-stu-id="b648e-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="b648e-827">По завершении процесса публикации браузер по умолчанию будет открывать опубликованный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="b648e-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="b648e-828">![Приложение, опубликованное в Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Приложение, опубликованное в Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="b648e-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="b648e-829">*Приложение, опубликованное в Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="b648e-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="b648e-830">Приложение в. Использование фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="b648e-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="b648e-831">С помощью фрагментов кода вы можете получить все необходимые вам коды.</span><span class="sxs-lookup"><span data-stu-id="b648e-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="b648e-832">В лабораторном документе вы узнаете, когда можно использовать их, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="b648e-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="b648e-833">![Использование фрагментов кода Visual Studio для вставки кода в проект](aspnet-mvc-4-fundamentals/_static/image69.png "Использование фрагментов кода Visual Studio для вставки кода в проект")</span><span class="sxs-lookup"><span data-stu-id="b648e-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="b648e-834">*Использование фрагментов кода Visual Studio для вставки кода в проект*</span><span class="sxs-lookup"><span data-stu-id="b648e-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="b648e-835">***Добавление фрагмента кода с помощью клавиатуры (C# только)***</span><span class="sxs-lookup"><span data-stu-id="b648e-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="b648e-836">Поместите курсор в то место, куда вы хотите вставить код.</span><span class="sxs-lookup"><span data-stu-id="b648e-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="b648e-837">Начните вводить имя фрагмента (без пробелов или дефисов).</span><span class="sxs-lookup"><span data-stu-id="b648e-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="b648e-838">Посмотрите, как IntelliSense отображает соответствующие имена фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="b648e-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="b648e-839">Выберите правильный фрагмент кода (или вводите его, пока не будет выбрано имя всего фрагмента).</span><span class="sxs-lookup"><span data-stu-id="b648e-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="b648e-840">Дважды нажмите клавишу TAB, чтобы вставить фрагмент в позицию курсора.</span><span class="sxs-lookup"><span data-stu-id="b648e-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="b648e-841">![Начните вводить имя фрагмента](aspnet-mvc-4-fundamentals/_static/image70.png "Начните вводить имя фрагмента")</span><span class="sxs-lookup"><span data-stu-id="b648e-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="b648e-842">*Начните вводить имя фрагмента*</span><span class="sxs-lookup"><span data-stu-id="b648e-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="b648e-843">![Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.](aspnet-mvc-4-fundamentals/_static/image71.png "Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="b648e-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="b648e-844">*Нажмите клавишу TAB, чтобы выбрать выделенный фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="b648e-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="b648e-845">![Снова нажмите клавишу TAB, и фрагмент развернется](aspnet-mvc-4-fundamentals/_static/image72.png "Снова нажмите клавишу TAB, и фрагмент развернется")</span><span class="sxs-lookup"><span data-stu-id="b648e-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="b648e-846">*Снова нажмите клавишу TAB, и фрагмент развернется*</span><span class="sxs-lookup"><span data-stu-id="b648e-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="b648e-847">***Добавление фрагмента кода с помощью мыши (C#, Visual Basic и XML)*** одного.</span><span class="sxs-lookup"><span data-stu-id="b648e-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="b648e-848">Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="b648e-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="b648e-849">Выберите **Вставить фрагмент** , за которым следуют **фрагменты кода**.</span><span class="sxs-lookup"><span data-stu-id="b648e-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="b648e-850">Выберите соответствующий фрагмент из списка, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="b648e-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="b648e-851">![Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.](aspnet-mvc-4-fundamentals/_static/image73.png "Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.")</span><span class="sxs-lookup"><span data-stu-id="b648e-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="b648e-852">*Щелкните правой кнопкой мыши место, куда нужно вставить фрагмент кода, и выберите пункт Вставить фрагмент.*</span><span class="sxs-lookup"><span data-stu-id="b648e-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="b648e-853">![Выберите соответствующий фрагмент из списка, щелкнув его.](aspnet-mvc-4-fundamentals/_static/image74.png "Выберите соответствующий фрагмент из списка, щелкнув его.")</span><span class="sxs-lookup"><span data-stu-id="b648e-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="b648e-854">*Выберите соответствующий фрагмент из списка, щелкнув его.*</span><span class="sxs-lookup"><span data-stu-id="b648e-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
