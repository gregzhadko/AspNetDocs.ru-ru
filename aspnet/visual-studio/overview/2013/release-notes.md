---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET и веб-инструменты для визуальной студии 2013 Примечания к выпуску (ru) Документы Майкрософт
author: rick-anderson
description: В этом документе описывается выпуск ASP.NET и web Tools for Visual Studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543500"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="52685-103">Заметки о выпуске ASP.NET and Web Tools для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="52685-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="52685-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="52685-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="52685-105">В этом документе описывается выпуск ASP.NET и web Tools for Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="52685-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="52685-106">Содержимое</span><span class="sxs-lookup"><span data-stu-id="52685-106">Contents</span></span>

- [<span data-ttu-id="52685-107">Примечания к установке</span><span class="sxs-lookup"><span data-stu-id="52685-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="52685-108">Документация</span><span class="sxs-lookup"><span data-stu-id="52685-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="52685-109">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="52685-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="52685-110">Новые возможности в ASP.NET и веб-инструменты для визуальной студии 2013</span><span class="sxs-lookup"><span data-stu-id="52685-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="52685-111">Один ASP.NET</span><span class="sxs-lookup"><span data-stu-id="52685-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="52685-112">Новый опыт веб-проектов</span><span class="sxs-lookup"><span data-stu-id="52685-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="52685-113">ASP.NET Леса</span><span class="sxs-lookup"><span data-stu-id="52685-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="52685-114">Привязывание к браузеру</span><span class="sxs-lookup"><span data-stu-id="52685-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="52685-115">Улучшения веб-редактора визуальной студии</span><span class="sxs-lookup"><span data-stu-id="52685-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="52685-116">Поддержка веб-приложений службы приложений Azure в визуальной студии</span><span class="sxs-lookup"><span data-stu-id="52685-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="52685-117">Веб-публикации Улучшения</span><span class="sxs-lookup"><span data-stu-id="52685-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="52685-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="52685-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="52685-119">ASP.NET веб-формы</span><span class="sxs-lookup"><span data-stu-id="52685-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="52685-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="52685-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="52685-121">Веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="52685-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="52685-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="52685-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="52685-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="52685-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="52685-124">Компоненты Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="52685-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="52685-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="52685-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="52685-126">ASP.NET бритва 3</span><span class="sxs-lookup"><span data-stu-id="52685-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="52685-127">ASP.NET приложение Приостановить</span><span class="sxs-lookup"><span data-stu-id="52685-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="52685-128">Известные проблемы и ломая изменения</span><span class="sxs-lookup"><span data-stu-id="52685-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="52685-129">Замечания по установке</span><span class="sxs-lookup"><span data-stu-id="52685-129">Installation Notes</span></span>

<span data-ttu-id="52685-130">ASP.NET и веб-инструменты для визуальной студии 2013 в комплекте в основной установщик и могут быть загружены [здесь](https://www.asp.net/downloads).</span><span class="sxs-lookup"><span data-stu-id="52685-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="52685-131">Документация</span><span class="sxs-lookup"><span data-stu-id="52685-131">Documentation</span></span>

<span data-ttu-id="52685-132">Учебники и другая информация о ASP.NET и веб-инструменты для визуальной студии 2013 доступны на [веб-сайте ASP.NET](https://www.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="52685-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="52685-133">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="52685-133">Software Requirements</span></span>

<span data-ttu-id="52685-134">ASP.NET и веб-инструменты требует Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="52685-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="52685-135">Новые возможности в ASP.NET и веб-инструменты для визуальной студии 2013</span><span class="sxs-lookup"><span data-stu-id="52685-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="52685-136">В следующих разделах описаны функции, которые были введены в релизе.</span><span class="sxs-lookup"><span data-stu-id="52685-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="52685-137">Один ASP.NET</span><span class="sxs-lookup"><span data-stu-id="52685-137">One ASP.NET</span></span>

<span data-ttu-id="52685-138">С выпуском Visual Studio 2013 мы сделали шаг к объединению опыта использования ASP.NET технологий, так что вы можете легко смешивать и сочетать те, которые вы хотите.</span><span class="sxs-lookup"><span data-stu-id="52685-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="52685-139">Например, можно начать проект с помощью MVC и легко добавить страницы web Forms в проект позже или эшафот Web AIS в проекте Web Forms.</span><span class="sxs-lookup"><span data-stu-id="52685-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="52685-140">Один ASP.NET это все о том, чтобы сделать его проще для вас, как разработчика, чтобы делать то, что вы любите в ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52685-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="52685-141">Независимо от того, какую технологию вы выберете, вы можете быть уверены в том, что вы строите на доверенных базовых рамках One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52685-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="52685-142">Новый опыт веб-проектов</span><span class="sxs-lookup"><span data-stu-id="52685-142">New Web Project Experience</span></span>

<span data-ttu-id="52685-143">Мы расширили опыт создания новых веб-проектов в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="52685-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="52685-144">В диалоге **New ASP.NET Web Project** вы можете выбрать нужный тип проекта, настроить любую комбинацию технологий (Web Forms, MVC, Web API), настроить параметры аутентификации и добавить модульный проект тестирования.</span><span class="sxs-lookup"><span data-stu-id="52685-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![Проект «Новый ASP.NET»](release-notes/_static/image1.png)

<span data-ttu-id="52685-146">Новый диалог позволяет изменять параметры аутентификации по умолчанию для многих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="52685-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="52685-147">Например, при создании проекта ASP.NET Web-форм можно выбрать любой из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="52685-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="52685-148">Без аутентификации</span><span class="sxs-lookup"><span data-stu-id="52685-148">No Authentication</span></span>
- <span data-ttu-id="52685-149">Индивидуальные учетные записи пользователей (ASP.NET членство или в систему социального провайдера)</span><span class="sxs-lookup"><span data-stu-id="52685-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="52685-150">Организационные учетные записи (Активный каталог в интернет-приложении)</span><span class="sxs-lookup"><span data-stu-id="52685-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="52685-151">Аутентификация Windows (Активный каталог в интранет-приложении)</span><span class="sxs-lookup"><span data-stu-id="52685-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![Параметры проверки подлинности](release-notes/_static/image2.png)

<span data-ttu-id="52685-153">Для получения дополнительной информации о новом процессе создания веб-проектов, см [ASP.NET.](creating-web-projects-in-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="52685-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="52685-154">Более подробную информацию о новых вариантах проверки подлинности можно узнать ASP.NET [identity](#TOC8) позже в этом документе.</span><span class="sxs-lookup"><span data-stu-id="52685-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="52685-155">ASP.NET Леса</span><span class="sxs-lookup"><span data-stu-id="52685-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="52685-156">ASP.NET Scaffolding — это платформа для генерации кода для ASP.NET веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="52685-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="52685-157">Это упрощает добавление шаблонного кода в проект, который взаимодействует с моделью данных.</span><span class="sxs-lookup"><span data-stu-id="52685-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="52685-158">В предыдущих версиях Visual Studio строительные леса ограничивались ASP.NET проектами MVC.</span><span class="sxs-lookup"><span data-stu-id="52685-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="52685-159">С Visual Studio 2013 теперь вы можете использовать строительные леса для любого ASP.NET проекта, включая веб-формы.</span><span class="sxs-lookup"><span data-stu-id="52685-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="52685-160">Visual Studio 2013 в настоящее время не поддерживает генерацию страниц для проекта Web Forms, но вы все еще можете использовать строительные леса с веб-формами, добавляя mVC зависимостей в проект.</span><span class="sxs-lookup"><span data-stu-id="52685-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="52685-161">Поддержка создания страниц для веб-форм будет добавлена в будущем обновлении.</span><span class="sxs-lookup"><span data-stu-id="52685-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="52685-162">При использовании строительных лесов мы гарантируем, что все необходимые зависимости установлены в проекте.</span><span class="sxs-lookup"><span data-stu-id="52685-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="52685-163">Например, если вы начинаете с проекта ASP.NET web Forms, а затем используете строительные леса для добавления контроллера Web API, необходимые пакеты и ссылки NuGet добавляются в ваш проект автоматически.</span><span class="sxs-lookup"><span data-stu-id="52685-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="52685-164">Чтобы добавить строительные леса MVC в проект Web Forms, добавьте **новый элемент Scaffolded** и выберите **MVC 5 Зависимости** в окне диалога.</span><span class="sxs-lookup"><span data-stu-id="52685-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="52685-165">Есть два варианта для строительных лесов MVC; Минимальный и полный.</span><span class="sxs-lookup"><span data-stu-id="52685-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="52685-166">Если вы выберете Minimal, в проект добавляются только пакеты и ссылки NuGet для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="52685-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="52685-167">При выборе опции Full добавлены минимальные зависимости, а также необходимые файлы содержимого для проекта MVC.</span><span class="sxs-lookup"><span data-stu-id="52685-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="52685-168">Поддержка контроллеров асин для строительных лесов использует новые функции async из Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="52685-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="52685-169">Для получения дополнительной информации и учебников, см [ASP.NET Scaffolding Обзор](aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52685-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="52685-170">Ссылка на браузер - канал SignalR между браузером и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52685-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="52685-171">Новая функция [Browser Link](using-browser-link.md) позволяет подключить несколько браузеров к Visual Studio и обновить их все, нажав кнопку в панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="52685-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="52685-172">Вы можете подключить несколько браузеров к сайту разработки, включая мобильные эмуляторы, и нажмите обновление, чтобы обновить все браузеры одновременно.</span><span class="sxs-lookup"><span data-stu-id="52685-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="52685-173">Browser Link также предоставляет API, позволяющий разработчикам писать расширения Браузерной ссылки.</span><span class="sxs-lookup"><span data-stu-id="52685-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="52685-174">Позволяя разработчикам воспользоваться API Link Browser, становится возможным создавать очень продвинутые сценарии, которые пересекают границы между Visual Studio и любым подключенным браузером.</span><span class="sxs-lookup"><span data-stu-id="52685-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="52685-175">Web Essentials использует API для создания интегрированного интерфейса между Visual Studio и инструментами разработчика браузера, удаленного управления мобильными эмуляторами и многое другое.</span><span class="sxs-lookup"><span data-stu-id="52685-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="52685-176">Улучшения веб-редактора визуальной студии</span><span class="sxs-lookup"><span data-stu-id="52685-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="52685-177">Visual Studio 2013 включает в себя новый HTML-редактор для файлов Razor и HTML файлов в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="52685-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="52685-178">Новый HTML-редактор предоставляет единую единую схему на основе HTML5.</span><span class="sxs-lookup"><span data-stu-id="52685-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="52685-179">Он имеет автоматическое завершение скобки, J'ury UI и AngularJS атрибут IntelliSense, атрибут IntelliSense группирования, ID и название класса Intellisense, и другие улучшения, включая лучшую производительность, форматирование и SmartTags.</span><span class="sxs-lookup"><span data-stu-id="52685-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="52685-180">Следующий скриншот демонстрирует использование атрибута Bootstrap IntelliSense в html-редакторе.</span><span class="sxs-lookup"><span data-stu-id="52685-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![Интеллект в HTML-редакторе](release-notes/_static/image4.png)

<span data-ttu-id="52685-182">Visual Studio 2013 также поставляется с как CoffeeScript и LESS редакторов встроенных дюйма</span><span class="sxs-lookup"><span data-stu-id="52685-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="52685-183">Редактор LESS поставляется со всеми классными функциями от редактора CSS и имеет специфический Intellisense для переменных и миксинов во всех документах LESS в цепочке. @import</span><span class="sxs-lookup"><span data-stu-id="52685-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="52685-184">Поддержка веб-приложений службы приложений Azure в визуальной студии</span><span class="sxs-lookup"><span data-stu-id="52685-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="52685-185">В Visual Studio 2013 с Azure SDK для .NET 2.2 вы можете использовать **Server Explorer** для непосредственного взаимодействия с удаленными веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="52685-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="52685-186">Вы можете войти в свою учетную запись Azure, создать новые веб-приложения, настроить приложения, просматривать журналы в реальном времени и многое другое.</span><span class="sxs-lookup"><span data-stu-id="52685-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="52685-187">Вскоре после выхода SDK 2.2 вы сможете работать в режиме отладки удаленно в Azure.</span><span class="sxs-lookup"><span data-stu-id="52685-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="52685-188">Большинство новых функций для Web Apps Azure App Service также работают в Visual Studio 2012 при установке текущего выпуска SDK Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="52685-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="52685-189">Дополнительные сведения см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="52685-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="52685-190">Создайте ASP.NET веб-приложение в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="52685-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="52685-191">Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52685-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="52685-192">Веб-публикации Улучшения</span><span class="sxs-lookup"><span data-stu-id="52685-192">Web Publish Enhancements</span></span>

<span data-ttu-id="52685-193">Visual Studio 2013 включает в себя новые и расширенные функции Web Publish.</span><span class="sxs-lookup"><span data-stu-id="52685-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="52685-194">Вот некоторые из них:</span><span class="sxs-lookup"><span data-stu-id="52685-194">Here are a few of them:</span></span>

- <span data-ttu-id="52685-195">Легко [автоматизировать шифрование файлов Web.config.](https://go.microsoft.com/fwlink/?LinkId=325529)</span><span class="sxs-lookup"><span data-stu-id="52685-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="52685-196">(Эта ссылка и следующие два пункта к документации по MSDN, которые могут быть доступны не до конца дня 10/17.)</span><span class="sxs-lookup"><span data-stu-id="52685-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="52685-197">Легко [автоматизировать принятие приложения в автономном режиме во время развертывания.](https://go.microsoft.com/fwlink/?LinkId=325530)</span><span class="sxs-lookup"><span data-stu-id="52685-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="52685-198">Нанастройка Web Deploy для [использования проверки файлов вместо последней измененной даты](https://go.microsoft.com/fwlink/?LinkId=325531) для определения того, какие файлы следует скопировать на сервер.</span><span class="sxs-lookup"><span data-stu-id="52685-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="52685-199">Быстро публикуйте отдельные выбранные файлы (включая Web.config) при использовании методов публикации FTP или файловой системы, а также web Deploy.</span><span class="sxs-lookup"><span data-stu-id="52685-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="52685-200">Для получения дополнительной информации о ASP.NET веб-развертывание, см [ASP.NET сайте](https://go.microsoft.com/fwlink/?LinkId=322027).</span><span class="sxs-lookup"><span data-stu-id="52685-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="52685-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="52685-201">NuGet 2.7</span></span>

<span data-ttu-id="52685-202">NuGet 2.7 включает в себя богатый набор новых функций, которые подробно описаны на [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="52685-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="52685-203">Эта версия NuGet также устраняет необходимость предоставления явного согласия на функцию восстановления пакета NuGet для загрузки пакетов.</span><span class="sxs-lookup"><span data-stu-id="52685-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="52685-204">Согласие (и связанный с ним флажок в диалоге предпочтений NuGet) теперь предоставляется путем установки NuGet.</span><span class="sxs-lookup"><span data-stu-id="52685-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="52685-205">Теперь восстановление пакета просто работает по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="52685-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="52685-206">Веб-формы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="52685-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="52685-207">Один ASP.NET</span><span class="sxs-lookup"><span data-stu-id="52685-207">One ASP.NET</span></span>

<span data-ttu-id="52685-208">Шаблоны проекта Web Forms легко интегрируются с новым опытом One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52685-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="52685-209">Вы можете добавить поддержку MVC и Web API в проект Web Forms, а также настроить аутентификацию с помощью мастера создания проекта One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52685-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="52685-210">Для получения дополнительной информации, смотрите [Создание ASP.NET веб-проектов в Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="52685-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="52685-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="52685-211">ASP.NET Identity</span></span>

<span data-ttu-id="52685-212">Шаблоны проекта Web Forms поддерживают новую платформу ASP.NET identity.</span><span class="sxs-lookup"><span data-stu-id="52685-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="52685-213">Кроме того, шаблоны теперь поддерживают создание проекта интрасети web Forms.</span><span class="sxs-lookup"><span data-stu-id="52685-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="52685-214">Для получения дополнительной [информации, см. Методы аутентификации](creating-web-projects-in-visual-studio.md#auth) в **создании ASP.NET веб-проектов в Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="52685-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="52685-215">Начальная загрузка</span><span class="sxs-lookup"><span data-stu-id="52685-215">Bootstrap</span></span>

<span data-ttu-id="52685-216">Шаблоны Web Forms используют [Bootstrap,](http://twitter.github.io/bootstrap/) чтобы обеспечить гладкий и отзывчивый внешний вид, который можно легко настроить.</span><span class="sxs-lookup"><span data-stu-id="52685-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="52685-217">Для получения дополнительной информации, [см. Bootstrap в Visual Studio 2013 веб-шаблоны проекта](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="52685-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="52685-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="52685-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="52685-219">Один ASP.NET</span><span class="sxs-lookup"><span data-stu-id="52685-219">One ASP.NET</span></span>

<span data-ttu-id="52685-220">Шаблоны проекта Web MVC легко интегрируются с новым опытом One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52685-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="52685-221">Вы можете настроить проект MVC и настроить аутентификацию с помощью мастера создания проекта One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52685-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="52685-222">Вступительный учебник для ASP.NET MVC 5 можно найти на [начало работы с ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="52685-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="52685-223">Для получения информации о модернизации проектов MVC 4 до MVC 5, [см. Как обновить ASP.NET MVC 4 и Web API проекта ASP.NET MVC 5 и Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="52685-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="52685-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="52685-224">ASP.NET Identity</span></span>

<span data-ttu-id="52685-225">Шаблоны проекта MVC были обновлены для использования ASP.NET Identity для проверки подлинности и управления идентификацией.</span><span class="sxs-lookup"><span data-stu-id="52685-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="52685-226">Учебник с участием Facebook и Google аутентификации и нового aPI членства можно найти в [Создать ASP.NET MVC 5 App с Facebook и Google OAuth2 и OpenID Войти и](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) создать ASP.NET [MVC приложение с auth и S'L DB и развернуть](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)в Azure App Service .</span><span class="sxs-lookup"><span data-stu-id="52685-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="52685-227">Начальная загрузка</span><span class="sxs-lookup"><span data-stu-id="52685-227">Bootstrap</span></span>

<span data-ttu-id="52685-228">Шаблон проекта MVC был обновлен, чтобы использовать [Bootstrap,](http://getbootstrap.com/) чтобы обеспечить гладкий и отзывчивый внешний вид, что вы можете легко настроить.</span><span class="sxs-lookup"><span data-stu-id="52685-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="52685-229">Для получения дополнительной информации, [см. Bootstrap в Visual Studio 2013 веб-шаблоны проекта](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="52685-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="52685-230">Фильтры аутентификации</span><span class="sxs-lookup"><span data-stu-id="52685-230">Authentication filters</span></span>

<span data-ttu-id="52685-231">Фильтры аутентификации — это новый вид фильтра в ASP.NET MVC, который работает до фильтрации авторизации в конвейере ASP.NET MVC и позволяет указывать логику аутентификации за действие, контроллер или глобально для всех контроллеров.</span><span class="sxs-lookup"><span data-stu-id="52685-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="52685-232">Фильтры аутентификации обрабатывают учетные данные в запросе и предоставляют соответствующий принцип.</span><span class="sxs-lookup"><span data-stu-id="52685-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="52685-233">Фильтры аутентификации могут также добавлять проблемы аутентификации в ответ на несанкционированные запросы.</span><span class="sxs-lookup"><span data-stu-id="52685-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="52685-234">Фильтр переопределения</span><span class="sxs-lookup"><span data-stu-id="52685-234">Filter overrides</span></span>

<span data-ttu-id="52685-235">Теперь можно переопределить, какие фильтры применяются к данному методу действия или контроллеру, указав фильтр переопределения.</span><span class="sxs-lookup"><span data-stu-id="52685-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="52685-236">Фильтры переопределения указывают набор типов фильтров, которые не должны быть запущены для заданной области (действия или контроллера).</span><span class="sxs-lookup"><span data-stu-id="52685-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="52685-237">Это позволяет настроить фильтры, которые применяются глобально, но затем исключить некоторые глобальные фильтры от применения к конкретным действиям или контроллерам.</span><span class="sxs-lookup"><span data-stu-id="52685-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="52685-238">Маршрутизация с помощью атрибутов</span><span class="sxs-lookup"><span data-stu-id="52685-238">Attribute routing</span></span>

<span data-ttu-id="52685-239">ASP.NET MVC теперь поддерживает атрибут разгрома, благодаря вкладу Тим [http://attributerouting.net](http://attributerouting.net)Ак колл, автор .</span><span class="sxs-lookup"><span data-stu-id="52685-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="52685-240">При маршрутизации атрибутов вы можете указать свои маршруты, аннотируя свои действия и контроллеры.</span><span class="sxs-lookup"><span data-stu-id="52685-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="52685-241">Веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="52685-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="52685-242">Маршрутизация с помощью атрибутов</span><span class="sxs-lookup"><span data-stu-id="52685-242">Attribute routing</span></span>

<span data-ttu-id="52685-243">ASP.NET Web API теперь поддерживает атрибут ывалии, благодаря вкладу [http://attributerouting.net](http://attributerouting.net)Тима Макколла, автора .</span><span class="sxs-lookup"><span data-stu-id="52685-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="52685-244">При маршрутизации атрибутов можно указать маршруты Web API, аннотируя свои действия и контроллеры следующим образом:</span><span class="sxs-lookup"><span data-stu-id="52685-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="52685-245">Трассировка атрибутов дает вам больше контроля над URIs в вашем веб-API.</span><span class="sxs-lookup"><span data-stu-id="52685-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="52685-246">Например, можно легко определить иерархию ресурсов с помощью одного контроллера API:</span><span class="sxs-lookup"><span data-stu-id="52685-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="52685-247">Маршрутирование атрибутов также обеспечивает удобный синтаксис для определения дополнительных параметров, значений по умолчанию и ограничений маршрута:</span><span class="sxs-lookup"><span data-stu-id="52685-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="52685-248">Для получения дополнительной информации о [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)разгроме атрибутов см.</span><span class="sxs-lookup"><span data-stu-id="52685-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="52685-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="52685-249">OAuth 2.0</span></span>

<span data-ttu-id="52685-250">Шаблоны проекта Web API и одностраничного приложения теперь поддерживают авторизацию с помощью OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="52685-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="52685-251">OAuth 2.0 является основой для авторизации доступа клиентов к защищенным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="52685-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="52685-252">Он работает для различных клиентов, включая браузеры и мобильные устройства.</span><span class="sxs-lookup"><span data-stu-id="52685-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="52685-253">Поддержка OAuth 2.0 основана на новых средствах обеспечения безопасности, предоставляемых компонентами Microsoft OWIN для проверки подлинности предъявителя и реализации роли сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="52685-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="52685-254">Кроме того, клиенты могут быть авторизованы с помощью сервера авторизации организации, например Azure Active Directory или ADFS в Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="52685-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="52685-255">Улучшения OData</span><span class="sxs-lookup"><span data-stu-id="52685-255">OData Improvements</span></span>

<span data-ttu-id="52685-256">**Поддержка $select, $expand, $batch и $value**</span><span class="sxs-lookup"><span data-stu-id="52685-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="52685-257">ASP.NET Web API OData теперь имеет полную поддержку $select, $expand и $value.</span><span class="sxs-lookup"><span data-stu-id="52685-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="52685-258">Вы также можете использовать $batch для пакетирования запросов и обработки наборов изменений.</span><span class="sxs-lookup"><span data-stu-id="52685-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="52685-259">Варианты $select и $expand позволяют изменить форму данных, которые возвращаются из конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="52685-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="52685-260">Для получения дополнительной информаци [$expand $selectи см.](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)</span><span class="sxs-lookup"><span data-stu-id="52685-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="52685-261">**Улучшенная расширяемость**</span><span class="sxs-lookup"><span data-stu-id="52685-261">**Improved extensibility**</span></span>

<span data-ttu-id="52685-262">Formatters OData теперь расширяются.</span><span class="sxs-lookup"><span data-stu-id="52685-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="52685-263">Можно добавить метаданные о вводе Atom, поддержку именованных потоков и записей ссылок на мультимедиа, добавить аннотации экземпляров и настроить способы создания ссылок.</span><span class="sxs-lookup"><span data-stu-id="52685-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="52685-264">**Поддержка без шрифта**</span><span class="sxs-lookup"><span data-stu-id="52685-264">**Type-less support**</span></span>

<span data-ttu-id="52685-265">Теперь можно создавать службы OData без необходимости определения типов CLR для типов сущностей.</span><span class="sxs-lookup"><span data-stu-id="52685-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="52685-266">Вместо этого контроллеры OData могут принимать или возвращать экземпляры **IEdmObject,** которые являются фактами OData, сериализуются/десериализируются.</span><span class="sxs-lookup"><span data-stu-id="52685-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="52685-267">**Повторное использование существующей модели**</span><span class="sxs-lookup"><span data-stu-id="52685-267">**Reuse an existing model**</span></span>

<span data-ttu-id="52685-268">Если у вас уже есть существующая модель данных сущности (EDM), теперь ее можно использовать напрямую, вместо того, чтобы строить новую.</span><span class="sxs-lookup"><span data-stu-id="52685-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="52685-269">Например, если вы используете рамки сущности, вы можете использовать EDM, который создает ДЛЯ вас EF.</span><span class="sxs-lookup"><span data-stu-id="52685-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="52685-270">Запрос пакетирования</span><span class="sxs-lookup"><span data-stu-id="52685-270">Request Batching</span></span>

<span data-ttu-id="52685-271">Пакетирование запроса объединяет несколько операций в один запрос HTTP POST, чтобы уменьшить сетевой трафик и обеспечить более плавный и менее болтливый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="52685-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="52685-272">ASP.NET Web API теперь поддерживает несколько стратегий пакетирования запросов:</span><span class="sxs-lookup"><span data-stu-id="52685-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="52685-273">Используйте $batch конечную точку службы OData.</span><span class="sxs-lookup"><span data-stu-id="52685-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="52685-274">Упакуйте несколько запросов в один многокомпонентный запрос MIME.</span><span class="sxs-lookup"><span data-stu-id="52685-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="52685-275">Используйте пользовательский формат пакетирования.</span><span class="sxs-lookup"><span data-stu-id="52685-275">Use a custom batching format.</span></span>

<span data-ttu-id="52685-276">Для включения пакета запросов просто добавьте маршрут с обработчиком пакетирования в конфигурацию Web API:</span><span class="sxs-lookup"><span data-stu-id="52685-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="52685-277">Вы также можете контролировать, выполняются ли запросы или выполняются последовательно или в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="52685-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="52685-278">Портативный клиент ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="52685-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="52685-279">Теперь вы можете использовать ASP.NET веб-клиент API для создания портативных библиотек классов, которые работают в windows Store и Windows Phone 8 приложений.</span><span class="sxs-lookup"><span data-stu-id="52685-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="52685-280">Вы также можете создать портативные предки, которые могут быть общими для всех клиентов и серверов.</span><span class="sxs-lookup"><span data-stu-id="52685-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="52685-281">Улучшенная тестируемость</span><span class="sxs-lookup"><span data-stu-id="52685-281">Improved Testability</span></span>

<span data-ttu-id="52685-282">Web API 2 значительно упрощает модульное тестирование контроллеров API.</span><span class="sxs-lookup"><span data-stu-id="52685-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="52685-283">Просто мгновенно ваш контроллер API с сообщением запроса и конфигурации, а затем вызвать метод действия, который вы хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="52685-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="52685-284">Также легко издеваться над классом **UrlHelper** для методов действий, выполняющие генерацию ссылок.</span><span class="sxs-lookup"><span data-stu-id="52685-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="52685-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="52685-285">IHttpActionResult</span></span>

<span data-ttu-id="52685-286">Теперь вы можете реализовать IHttpActionResult для инкапсулировать результат ваших методов действий Web API.</span><span class="sxs-lookup"><span data-stu-id="52685-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="52685-287">IHttpActionResult, возвращенный из метода действий Web API, выполняется ASP.NET время выполнения Web API для получения полученного сообщения ответа.</span><span class="sxs-lookup"><span data-stu-id="52685-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="52685-288">IHttpActionResult может быть возвращен из любого действия Web API для упрощения модульного тестирования реализации Web API.</span><span class="sxs-lookup"><span data-stu-id="52685-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="52685-289">Для удобства ряд реализаций IHttpActionResult предоставляется из коробки, включая результаты для возвращения определенных кодов статуса, отформатированного контента или ответов, согласованных с содержанием.</span><span class="sxs-lookup"><span data-stu-id="52685-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="52685-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="52685-290">HttpRequestContext</span></span>

<span data-ttu-id="52685-291">Новый **HttpRequestContext** отслеживает любое состояние, которое привязано к запросу, но не сразу доступно из запроса.</span><span class="sxs-lookup"><span data-stu-id="52685-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="52685-292">Например, можно использовать **HttpRequestContext** для получения данных маршрута, основного, связанного с запросом, сертификата клиента, **UrlHelper** и корня виртуального пути.</span><span class="sxs-lookup"><span data-stu-id="52685-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="52685-293">Вы можете легко создать **HttpRequestContext** для целей модульного тестирования.</span><span class="sxs-lookup"><span data-stu-id="52685-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="52685-294">Поскольку основной для запроса вытекает с запросом вместо того, чтобы полагаться на **Thread.CurrentPrincipal,** основной теперь доступен в течение всего срока действия запроса, пока он находится в конвейере Web API.</span><span class="sxs-lookup"><span data-stu-id="52685-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="52685-295">CORS</span><span class="sxs-lookup"><span data-stu-id="52685-295">CORS</span></span>

<span data-ttu-id="52685-296">Благодаря еще одному большому вкладу Брока Аллена, ASP.NET теперь полностью поддерживает совместное использование запросов Cross Origin (CORS).</span><span class="sxs-lookup"><span data-stu-id="52685-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="52685-297">Параметры безопасности веб-браузера предотвращают отправку запросов AJAX с веб-страницы к другому домену.</span><span class="sxs-lookup"><span data-stu-id="52685-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="52685-298">[CORS](http://www.w3.org/TR/cors/) является стандартом W3C, который позволяет серверу ослабить политику того же происхождения.</span><span class="sxs-lookup"><span data-stu-id="52685-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="52685-299">С помощью CORS сервер может явным образом разрешить некоторые запросы независимо от источника, а другие — отклонить.</span><span class="sxs-lookup"><span data-stu-id="52685-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="52685-300">Web API 2 теперь поддерживает CORS, включая автоматическое обращение с предполетным запросом.</span><span class="sxs-lookup"><span data-stu-id="52685-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="52685-301">Для получения дополнительной информации смотрите [включение запросов Cross-Origin в ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="52685-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="52685-302">Фильтры аутентификации</span><span class="sxs-lookup"><span data-stu-id="52685-302">Authentication Filters</span></span>

<span data-ttu-id="52685-303">Фильтры аутентификации — это новый вид фильтра в ASP.NET Web API, который работает до фильтрации авторизации в ASP.NET конвейера Web API и позволяет указывать логику проверки подлинности за действие, контроллер или глобально для всех контроллеров.</span><span class="sxs-lookup"><span data-stu-id="52685-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="52685-304">Фильтры аутентификации обрабатывают учетные данные в запросе и предоставляют соответствующий принцип.</span><span class="sxs-lookup"><span data-stu-id="52685-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="52685-305">Фильтры аутентификации могут также добавлять проблемы аутентификации в ответ на несанкционированные запросы.</span><span class="sxs-lookup"><span data-stu-id="52685-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="52685-306">Переопределения фильтра</span><span class="sxs-lookup"><span data-stu-id="52685-306">Filter Overrides</span></span>

<span data-ttu-id="52685-307">Теперь можно переопределить, какие фильтры применяются к данному методу действия или контроллеру, указав фильтр переопределения.</span><span class="sxs-lookup"><span data-stu-id="52685-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="52685-308">Фильтры переопределения указывают набор типов фильтров, которые не должны работать для заданной области (действия или контроллера).</span><span class="sxs-lookup"><span data-stu-id="52685-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="52685-309">Это позволяет добавлять глобальные фильтры, но затем исключить некоторые из конкретных действий или контроллеров.</span><span class="sxs-lookup"><span data-stu-id="52685-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="52685-310">Интеграция OWIN</span><span class="sxs-lookup"><span data-stu-id="52685-310">OWIN Integration</span></span>

<span data-ttu-id="52685-311">ASP.NET Web API теперь полностью поддерживает OWIN и может работать на любом хосте OWIN.</span><span class="sxs-lookup"><span data-stu-id="52685-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="52685-312">Также включен **HostAuthenticationFilter,** который обеспечивает интеграцию с системой аутентификации OWIN.</span><span class="sxs-lookup"><span data-stu-id="52685-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="52685-313">С интеграцией OWIN вы можете самостоятельно размещать Web API в собственном процессе наряду с другими программами-посредниками OWIN, такими как SignalR.</span><span class="sxs-lookup"><span data-stu-id="52685-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="52685-314">Для получения дополнительной информации см [ASP.NET.](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)</span><span class="sxs-lookup"><span data-stu-id="52685-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="52685-315">ASP.NET СигналР 2.0</span><span class="sxs-lookup"><span data-stu-id="52685-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="52685-316">В следующих разделах описаны особенности SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="52685-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="52685-317">Построен на OWIN</span><span class="sxs-lookup"><span data-stu-id="52685-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="52685-318">MapHubs и MapConnection теперь MapSignalR</span><span class="sxs-lookup"><span data-stu-id="52685-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="52685-319">Поддержка кросс-домена</span><span class="sxs-lookup"><span data-stu-id="52685-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="52685-320">Поддержка iOS и Android через MonoTouch и MonoDroid</span><span class="sxs-lookup"><span data-stu-id="52685-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="52685-321">Портативный клиент .NET</span><span class="sxs-lookup"><span data-stu-id="52685-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="52685-322">Новый пакет self-host</span><span class="sxs-lookup"><span data-stu-id="52685-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="52685-323">Обратная поддержка сервера, совместимая с обратной памятью</span><span class="sxs-lookup"><span data-stu-id="52685-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="52685-324">Удалена поддержка сервера для .NET 4.0</span><span class="sxs-lookup"><span data-stu-id="52685-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="52685-325">Отправка сообщения в список клиентов и групп</span><span class="sxs-lookup"><span data-stu-id="52685-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="52685-326">Отправка сообщения конкретному пользователю</span><span class="sxs-lookup"><span data-stu-id="52685-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="52685-327">Улучшенная поддержка обработки ошибок</span><span class="sxs-lookup"><span data-stu-id="52685-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="52685-328">Упрощенное модульное тестирование концентраторов</span><span class="sxs-lookup"><span data-stu-id="52685-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="52685-329">Обработка ошибок JavaScript</span><span class="sxs-lookup"><span data-stu-id="52685-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="52685-330">Например, как обновить существующий проект 1.x до SignalR 2.0, [см.](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)</span><span class="sxs-lookup"><span data-stu-id="52685-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="52685-331">Построен на OWIN</span><span class="sxs-lookup"><span data-stu-id="52685-331">Built on OWIN</span></span>

<span data-ttu-id="52685-332">SignalR 2.0 построен полностью на [OWIN (Открытый веб-интерфейс для .NET)](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="52685-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="52685-333">Это изменение делает процесс настройки SignalR гораздо более последовательным между веб-хостинга и самостоятельнох приложений SignalR, но также требует ряда изменений API.</span><span class="sxs-lookup"><span data-stu-id="52685-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="52685-334">MapHubs и MapConnection теперь MapSignalR</span><span class="sxs-lookup"><span data-stu-id="52685-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="52685-335">Для совместимости со стандартами OWIN эти методы `MapSignalR`были переименованы в .</span><span class="sxs-lookup"><span data-stu-id="52685-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="52685-336">`MapSignalR`вызов без параметров будет отображать `MapHubs` все концентраторы (как это делает в версии 1.x); для отображения отдельных объектов **PersistentConnection,** укажите тип соединения как параметр типа и расширение URL для соединения в качестве первого аргумента.</span><span class="sxs-lookup"><span data-stu-id="52685-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="52685-337">Метод `MapSignalR` называется в классе стартапов Owin.</span><span class="sxs-lookup"><span data-stu-id="52685-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="52685-338">Visual Studio 2013 содержит новый шаблон для стартап-класса Owin; использовать этот шаблон, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="52685-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="52685-339">Нажмите на проект правой кнопкой мыши</span><span class="sxs-lookup"><span data-stu-id="52685-339">Right-click on the project</span></span>
2. <span data-ttu-id="52685-340">Выберите **Добавить,** **Новый пункт...**</span><span class="sxs-lookup"><span data-stu-id="52685-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="52685-341">Выберите **класс стартапа Owin.**</span><span class="sxs-lookup"><span data-stu-id="52685-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="52685-342">Назовите новый класс **Startup.cs**.</span><span class="sxs-lookup"><span data-stu-id="52685-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="52685-343">В **web-приложении** класс запуска Owin, содержащий `MapSignalR` метод, затем добавляется в процесс запуска Owin с помощью записи в настройках приложения в файле Web.Config, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="52685-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="52685-344">В **самохознятом приложении**класс Startup передается `WebApp.Start` как параметр типа метода.</span><span class="sxs-lookup"><span data-stu-id="52685-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="52685-345">**Картирование концентраторов и соединений в SignalR 1.x (из глобального файла приложения в веб-приложении):**</span><span class="sxs-lookup"><span data-stu-id="52685-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="52685-346">**Картирование концентраторов и соединений в SignalR 2.0 (из файла класса Owin Startup):**</span><span class="sxs-lookup"><span data-stu-id="52685-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="52685-347">В **самохознящемся приложении**класс Startup передается как параметр типа для метода, `WebApp.Start` как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="52685-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="52685-348">Поддержка кросс-домена</span><span class="sxs-lookup"><span data-stu-id="52685-348">Cross-Domain Support</span></span>

<span data-ttu-id="52685-349">В SignalR 1.x запросы на перекрестный домен контролировались одним флагом EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="52685-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="52685-350">Этот флаг контролировал запросы JSONP и CORS.</span><span class="sxs-lookup"><span data-stu-id="52685-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="52685-351">Для большей гибкости вся поддержка CORS была удалена из серверного компонента SignalR (клиенты JavaScript по-прежнему используют CORS обычно, если обнаруживается, что браузер поддерживает его), и для поддержки этих сценариев было предоставлено новое промежуточное программное обеспечение OWIN.</span><span class="sxs-lookup"><span data-stu-id="52685-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="52685-352">В SignalR 2.0, если JSONP требуется для клиента (для поддержки запросов кросс-домена в `EnableJSONP` старых браузерах), он должен быть включен явно, установив на `HubConfiguration` объекте, как `true`показано ниже.</span><span class="sxs-lookup"><span data-stu-id="52685-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="52685-353">JSONP отключен по умолчанию, так как он менее безопасен, чем CORS.</span><span class="sxs-lookup"><span data-stu-id="52685-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="52685-354">Чтобы добавить новое промежуточное программное обеспечение `Microsoft.Owin.Cors` CORS в SignalR `UseCors` 2.0, добавьте библиотеку в свой проект и позвоните перед программой SignalR, как показано в разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="52685-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="52685-355">**Добавление в проект Microsoft.Owin.Cors:** Для установки этой библиотеки запустите следующую команду в консоли менеджера пакетов:</span><span class="sxs-lookup"><span data-stu-id="52685-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="52685-356">Эта команда добавит версию пакета 2.0.0 в проект.</span><span class="sxs-lookup"><span data-stu-id="52685-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="52685-357">**Вызов UseCors**</span><span class="sxs-lookup"><span data-stu-id="52685-357">**Calling UseCors**</span></span>

<span data-ttu-id="52685-358">Следующие фрагменты кода демонстрируют, как реализовать соединения кросс-домена в SignalR 1.x и 2.0.</span><span class="sxs-lookup"><span data-stu-id="52685-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="52685-359">**Реализация запросов кросс-домена в SignalR 1.x (из глобального файла приложения)**</span><span class="sxs-lookup"><span data-stu-id="52685-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="52685-360">**Реализация запросов кросс-домена в SignalR 2.0 (из файла кода C')**</span><span class="sxs-lookup"><span data-stu-id="52685-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="52685-361">Следующий код показывает, как включить CORS или JSONP в проекте SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="52685-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="52685-362">Этот образец `Map` `RunSignalR` кода `MapSignalR`использует и вместо , так что CORS промежуточное программное обеспечение работает только для `MapSignalR`запросов SignalR, которые требуют поддержки CORS (а не для всего трафика на пути, указанном в .) `Map` также может быть использован для любого другого промежуточного программного обеспечения, которое должно работать для конкретного приставки URL, а не для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="52685-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="52685-363">Поддержка iOS и Android через MonoTouch и MonoDroid</span><span class="sxs-lookup"><span data-stu-id="52685-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="52685-364">Поддержка была добавлена для клиентов iOS и Android с использованием компонентов MonoTouch и MonoDroid из [библиотеки Xamarin.](https://xamarin.com/)</span><span class="sxs-lookup"><span data-stu-id="52685-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="52685-365">Для получения дополнительной информации о том, как их использовать, [см.](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)</span><span class="sxs-lookup"><span data-stu-id="52685-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="52685-366">Эти компоненты будут доступны в [магазине Xamarin,](https://store.xamarin.com/) когда будет выпущен релиз SignalR RTW.</span><span class="sxs-lookup"><span data-stu-id="52685-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="52685-367">Портативный клиент .NET</span><span class="sxs-lookup"><span data-stu-id="52685-367">### Portable .NET client</span></span>

<span data-ttu-id="52685-368">Чтобы лучше облегчить развитие кросс-платформы, клиенты Silverlight, WinRT и Windows Phone были заменены одним портативным клиентом .NET, который поддерживает следующие платформы:</span><span class="sxs-lookup"><span data-stu-id="52685-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="52685-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="52685-369">NET 4.5</span></span>
- <span data-ttu-id="52685-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="52685-370">Silverlight 5</span></span>
- <span data-ttu-id="52685-371">WinRT (.NET для приложений магазина Windows)</span><span class="sxs-lookup"><span data-stu-id="52685-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="52685-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="52685-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="52685-373">Новый пакет self-host</span><span class="sxs-lookup"><span data-stu-id="52685-373">New Self-Host Package</span></span>

<span data-ttu-id="52685-374">В настоящее время существует пакет NuGet, чтобы было легче начать работу с SignalR Self-Host (приложения SignalR, которые размещаются в процессе или другом приложении, а не размещаются на веб-сервере).</span><span class="sxs-lookup"><span data-stu-id="52685-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="52685-375">Чтобы обновить проект самостоятельного размещения, построенный с помощью SignalR 1.x, удалите пакет Microsoft.AspNet.SignalR.Owin и добавьте пакет Microsoft.AspNet.SignalR.SelfHost.</span><span class="sxs-lookup"><span data-stu-id="52685-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="52685-376">Для получения дополнительной информации о начале работы с пакетом самостоятельного хозяина, [см.](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)</span><span class="sxs-lookup"><span data-stu-id="52685-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="52685-377">Обратная поддержка сервера, совместимая с обратной памятью</span><span class="sxs-lookup"><span data-stu-id="52685-377">Backward-compatible server support</span></span>

<span data-ttu-id="52685-378">В предыдущих версиях SignalR версии пакета SignalR, используемые в клиенте и сервере, должны быть идентичными.</span><span class="sxs-lookup"><span data-stu-id="52685-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="52685-379">Для поддержки приложений с толстыми клиентами, которые будет трудно обновить, SignalR 2.0 теперь поддерживает использование более новой версии сервера со старым клиентом.</span><span class="sxs-lookup"><span data-stu-id="52685-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="52685-380">**Примечание: SignalR 2.0 не поддерживает серверы, построенные со старыми версиями с новыми клиентами.**</span><span class="sxs-lookup"><span data-stu-id="52685-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="52685-381">Удалена поддержка сервера для .NET 4.0</span><span class="sxs-lookup"><span data-stu-id="52685-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="52685-382">SignalR 2.0 отказался от поддержки совместимости сервера с .NET 4.0.</span><span class="sxs-lookup"><span data-stu-id="52685-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="52685-383">.NET 4.5 должен использоваться с серверами SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="52685-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="52685-384">Существует еще .NET 4.0 клиент для SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="52685-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="52685-385">Отправка сообщения в список клиентов и групп</span><span class="sxs-lookup"><span data-stu-id="52685-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="52685-386">В SignalR 2.0 можно отправить сообщение, используя список идентирок клиента и группы.</span><span class="sxs-lookup"><span data-stu-id="52685-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="52685-387">Следующие фрагменты кода демонстрируют, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="52685-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="52685-388">**Отправка сообщения в список клиентов и групп с помощью PersistentConnection**</span><span class="sxs-lookup"><span data-stu-id="52685-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="52685-389">**Отправка сообщения в список клиентов и групп, использующих концентраторы**</span><span class="sxs-lookup"><span data-stu-id="52685-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="52685-390">Отправка сообщения конкретному пользователю</span><span class="sxs-lookup"><span data-stu-id="52685-390">Sending a message to a specific user</span></span>

<span data-ttu-id="52685-391">Эта функция позволяет пользователям указать, что userId основан на IRequest через новый интерфейс IUserIdProvider:</span><span class="sxs-lookup"><span data-stu-id="52685-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="52685-392">**Интерфейс IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="52685-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="52685-393">По умолчанию будет осуществляться реализация, которая использует IPrincipal.Identity.Name пользователя в качестве имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="52685-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="52685-394">В концентратах вы сможете отправлять сообщения этим пользователям через новый API:</span><span class="sxs-lookup"><span data-stu-id="52685-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="52685-395">**Использование API клиента.Пользователя**</span><span class="sxs-lookup"><span data-stu-id="52685-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="52685-396">Улучшенная поддержка обработки ошибок</span><span class="sxs-lookup"><span data-stu-id="52685-396">Better Error Handling Support</span></span>

<span data-ttu-id="52685-397">Теперь пользователи могут выбрасывать **HubException** из любого вызова концентратора.</span><span class="sxs-lookup"><span data-stu-id="52685-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="52685-398">Конструктор **HubException** может принимать строку сообщения и объект дополнительных данных об ошибке.</span><span class="sxs-lookup"><span data-stu-id="52685-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="52685-399">SignalR автоматически заследует исключение и отправляет его клиенту, где он будет использоваться для отклонения/отказа вызова метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="52685-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="52685-400">Настройка **исключениях концентратора показывает** подробное отношение к **HubException,** отправляемого обратно клиенту или нет; он всегда отправляется.</span><span class="sxs-lookup"><span data-stu-id="52685-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="52685-401">**Код на стороне сервера, демонстрирующий отправку HubException клиенту**</span><span class="sxs-lookup"><span data-stu-id="52685-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="52685-402">**Клиентский код JavaScript, демонстрирующий ответ на HubException, отправленный с сервера**</span><span class="sxs-lookup"><span data-stu-id="52685-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="52685-403">**клиентский код .NET, демонстрирующий ответ на HubException, отправленный с сервера**</span><span class="sxs-lookup"><span data-stu-id="52685-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="52685-404">Упрощенное модульное тестирование концентраторов</span><span class="sxs-lookup"><span data-stu-id="52685-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="52685-405">SignalR 2.0 включает `IHubCallerConnectionContext` в себя интерфейс, вызванный на концентраторы, что делает его легче создавать макет вызова стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="52685-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="52685-406">Следующие фрагменты кода демонстрируют, используя этот интерфейс с популярными тестовыми ремнями [xUnit.net](https://github.com/xunit/xunit) и [moq.](https://code.google.com/p/moq/)</span><span class="sxs-lookup"><span data-stu-id="52685-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="52685-407">**Модульное тестирование SignalR с xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="52685-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="52685-408">**Модульное тестирование SignalR с moq**</span><span class="sxs-lookup"><span data-stu-id="52685-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="52685-409">Обработка ошибок JavaScript</span><span class="sxs-lookup"><span data-stu-id="52685-409">JavaScript error handling</span></span>

<span data-ttu-id="52685-410">В SignalR 2.0 все обработки вызовов JavaScript возвращают объекты ошибок JavaScript вместо необработанных строк.</span><span class="sxs-lookup"><span data-stu-id="52685-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="52685-411">Это позволяет SignalR передавать более богатую информацию обработчикам ошибок.</span><span class="sxs-lookup"><span data-stu-id="52685-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="52685-412">Вы можете получить внутреннее `source` исключение из свойства ошибки.</span><span class="sxs-lookup"><span data-stu-id="52685-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="52685-413">**Клиентский код JavaScript, обрабатываемый исключением Start.Fail**</span><span class="sxs-lookup"><span data-stu-id="52685-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="52685-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="52685-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="52685-415">Новая система ASP.NET членства</span><span class="sxs-lookup"><span data-stu-id="52685-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="52685-416">ASP.NET Identity — это новая система членства для ASP.NET приложений.</span><span class="sxs-lookup"><span data-stu-id="52685-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="52685-417">ASP.NET Identity упрощает интеграцию данных профиля пользователя с данными приложения.</span><span class="sxs-lookup"><span data-stu-id="52685-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="52685-418">ASP.NET Identity также позволяет выбрать модель сохранения для профилей пользователей в приложении.</span><span class="sxs-lookup"><span data-stu-id="52685-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="52685-419">Данные можно сохранять в базе данных SQL Server или другом хранилище, в том числе хранилищах данных NoSQL , таких как таблица хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="52685-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="52685-420">Для получения дополнительной информации, см [Индивидуальные учетные записи пользователей](creating-web-projects-in-visual-studio.md#indauth) в **создании ASP.NET веб-проектов в Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="52685-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="52685-421">Проверка подлинности на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="52685-421">Claims-based authentication</span></span>

<span data-ttu-id="52685-422">ASP.NET теперь поддерживает проверку подлинности на основе утверждений, где личность пользователя представлена как набор требований доверенного эмитента.</span><span class="sxs-lookup"><span data-stu-id="52685-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="52685-423">Пользователи могут быть проверены с помощью имени пользователя и пароля, хранящегося в базе данных приложений, или с помощью поставщиков социальных идентификационных данных (например, учетных записей Майкрософт, Facebook, Google, Twitter), или с помощью организационных учетных записей через службы Azure Active Directory или Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="52685-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="52685-424">Интеграция с активным каталогом Azure и активным каталогом Windows Server</span><span class="sxs-lookup"><span data-stu-id="52685-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="52685-425">Теперь можно создавать ASP.NET проекты, которые используют Active Directory Azure или Активный каталог Windows Server (AD) для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="52685-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="52685-426">Для получения дополнительной информации см [Организационная отчетность](creating-web-projects-in-visual-studio.md#orgauth) в **создании ASP.NET веб-проектов в Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="52685-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="52685-427">Интеграция OWIN</span><span class="sxs-lookup"><span data-stu-id="52685-427">OWIN Integration</span></span>

<span data-ttu-id="52685-428">ASP.NET аутентификация теперь основана на промежуточном программном обеспечении OWIN, которое может быть использовано на любом хосте на основе OWIN.</span><span class="sxs-lookup"><span data-stu-id="52685-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="52685-429">Для получения дополнительной информации о [Microsoft OWIN Components](#TOC7) OWIN, см.</span><span class="sxs-lookup"><span data-stu-id="52685-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="52685-430">Компоненты Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="52685-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="52685-431">[Открытый веб-интерфейс для .NET](http://owin.org/) (OWIN) определяет абстракцию между веб-серверами .NET и веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="52685-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="52685-432">OWIN отсоединяет веб-приложение с сервера, делая веб-приложения хост-агностиком.</span><span class="sxs-lookup"><span data-stu-id="52685-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="52685-433">Например, можно разместить веб-приложение на основе OWIN в IIS или самостоятельно разместить его в пользовательском процессе.</span><span class="sxs-lookup"><span data-stu-id="52685-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="52685-434">Изменения, внесенные в компоненты Microsoft OWIN (также известный как проект Katana), включают новые компоненты сервера и хоста, новые библиотеки помощников и промежуточное программное обеспечение, а также новые программы по обеспечению подлинности.</span><span class="sxs-lookup"><span data-stu-id="52685-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="52685-435">Для получения дополнительной информации о OWIN и Катана, [см.](../../../aspnet/overview/owin-and-katana/index.md)</span><span class="sxs-lookup"><span data-stu-id="52685-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="52685-436">**Примечание: [приложения OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) не могут работать в классическом режиме IIS; они должны работать в интегрированном режиме.**</span><span class="sxs-lookup"><span data-stu-id="52685-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="52685-437">**Примечание: [приложения OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) должны быть запущены в полном доверии.**</span><span class="sxs-lookup"><span data-stu-id="52685-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="52685-438">Новые серверы и хосты</span><span class="sxs-lookup"><span data-stu-id="52685-438">New Servers and Hosts</span></span>

<span data-ttu-id="52685-439">С этим выпуском были добавлены новые компоненты для включения сценариев самостоятельного размещения.</span><span class="sxs-lookup"><span data-stu-id="52685-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="52685-440">Эти компоненты включают следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="52685-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="52685-441">**Microsoft.owin.host.httpListener**.</span><span class="sxs-lookup"><span data-stu-id="52685-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="52685-442">Предоставляет сервер OWIN, который использует **HttpListener** для прослушивания запросов HTTP и направления их в конвейер OWIN.</span><span class="sxs-lookup"><span data-stu-id="52685-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="52685-443">**Microsoft.Owin.Hosting** предоставляет библиотеку для разработчиков, которые хотят самостоятельно разместить конвейер OWIN в пользовательском процессе, например, консольное приложение или служба Windows.</span><span class="sxs-lookup"><span data-stu-id="52685-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="52685-444">**OwinHost**.</span><span class="sxs-lookup"><span data-stu-id="52685-444">**OwinHost**.</span></span> <span data-ttu-id="52685-445">Обеспечивает автономный исполняемый, который `Microsoft.Owin.Hosting` обертывает и позволяет самостоятельно размещать конвейер OWIN без необходимости написания пользовательского приложения хоста.</span><span class="sxs-lookup"><span data-stu-id="52685-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="52685-446">Кроме того, `Microsoft.Owin.Host.SystemWeb` пакет теперь позволяет промежуточное программное обеспечение предоставлять подсказки серверу **SystemWeb,** указывая, что промежуточное программное обеспечение должно быть вызвано на определенном этапе ASP.NET конвейера.</span><span class="sxs-lookup"><span data-stu-id="52685-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="52685-447">Эта функция особенно полезна для промежуточного программного обеспечения для проверки подлинности, которое должно работать на ранних стадиях ASP.NET конвейера.</span><span class="sxs-lookup"><span data-stu-id="52685-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="52685-448">Библиотеки для помощников и промежуточного посуды</span><span class="sxs-lookup"><span data-stu-id="52685-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="52685-449">Хотя компоненты OWIN можно писать, используя только определения функции и `Microsoft.Owin` шрифта из спецификации OWIN, новый пакет предоставляет более удобный набор абстракций.</span><span class="sxs-lookup"><span data-stu-id="52685-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="52685-450">Этот пакет объединяет несколько более ранних `Owin.Extensions`пакетов (например, , `Owin.Types`) в одну, хорошо структурированную модель объекта, которая затем может быть легко использована другими компонентами OWIN.</span><span class="sxs-lookup"><span data-stu-id="52685-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="52685-451">В самом деле, большинство компонентов Microsoft OWIN в настоящее время используют этот пакет.</span><span class="sxs-lookup"><span data-stu-id="52685-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="52685-452">[Приложения OWIN](http://www.owin.org) не могут работать в классическом режиме IIS; они должны работать в интегрированном режиме.</span><span class="sxs-lookup"><span data-stu-id="52685-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="52685-453">[Заявки OWIN](http://www.owin.org) должны быть запущены в полном доверии.</span><span class="sxs-lookup"><span data-stu-id="52685-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="52685-454">Этот релиз также включает в себя пакет Microsoft.Owin.Diagnostics, который включает в себя промежуточное программное обеспечение для проверки запущенного приложения OWIN, а также промежуточное программное обеспечение для ошибок, чтобы помочь в расследовании сбоев.</span><span class="sxs-lookup"><span data-stu-id="52685-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="52685-455">Компоненты аутентификации</span><span class="sxs-lookup"><span data-stu-id="52685-455">Authentication Components</span></span>

<span data-ttu-id="52685-456">Доступны следующие компоненты аутентификации.</span><span class="sxs-lookup"><span data-stu-id="52685-456">The following authentication components are available.</span></span>

- <span data-ttu-id="52685-457">**Microsoft.Owin.Security.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="52685-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="52685-458">Позволяет проводить аутентификацию с помощью локальных или облачных служб каталога.</span><span class="sxs-lookup"><span data-stu-id="52685-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="52685-459">**Microsoft.Owin.Security.Cookies** обеспечивает аутентификацию с помощью файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="52685-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="52685-460">Этот пакет был `Microsoft.Owin.Security.Forms`ранее назван .</span><span class="sxs-lookup"><span data-stu-id="52685-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="52685-461">**Microsoft.Owin.Security.Facebook** обеспечивает аутентификацию с помощью сервиса Facebook, основанного на OAuth.</span><span class="sxs-lookup"><span data-stu-id="52685-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="52685-462">**Microsoft.Owin.Security.Google** обеспечивает аутентификацию с помощью сервиса Google OpenID.</span><span class="sxs-lookup"><span data-stu-id="52685-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="52685-463">**Microsoft.Owin.Security.Jwt** обеспечивает аутентификацию с помощью токенов JWT.</span><span class="sxs-lookup"><span data-stu-id="52685-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="52685-464">**Microsoft.Owin.Security.MicrosoftAccount** обеспечивает аутентификацию с помощью учетных записей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="52685-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="52685-465">**Microsoft.Owin.Security.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="52685-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="52685-466">Предоставляет сервер авторизации OAuth, а также промежуточное программное обеспечение для проверки подлинности токенов носителя.</span><span class="sxs-lookup"><span data-stu-id="52685-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="52685-467">**Microsoft.Owin.Security.Twitter** обеспечивает аутентификацию с помощью сервиса Twitter, основанного на OAuth.</span><span class="sxs-lookup"><span data-stu-id="52685-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="52685-468">Этот релиз также `Microsoft.Owin.Cors` включает в себя пакет, который содержит промежуточное программное обеспечение для обработки кросс-происхождения HTTP запросов.</span><span class="sxs-lookup"><span data-stu-id="52685-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="52685-469">Поддержка подписания JWT была удалена в финальной версии Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="52685-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="52685-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="52685-470">Entity Framework 6</span></span>

<span data-ttu-id="52685-471">Список новых функций и других изменений в рамках entity Framework 6 можно узнать в [версии Entity Framework History.](https://msdn.com/data/jj574253)</span><span class="sxs-lookup"><span data-stu-id="52685-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="52685-472">ASP.NET бритва 3</span><span class="sxs-lookup"><span data-stu-id="52685-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="52685-473">ASP.NET Razor 3 включает в себя следующие новые функции:</span><span class="sxs-lookup"><span data-stu-id="52685-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="52685-474">Поддержка редактирования вкладок.</span><span class="sxs-lookup"><span data-stu-id="52685-474">Support for Tab editing.</span></span> <span data-ttu-id="52685-475">Ранее команда **Format Document,** автоматическое отформатирование и автоматическое форматирование в Visual Studio работали неправильно при использовании опции **Keep Tabs.**</span><span class="sxs-lookup"><span data-stu-id="52685-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="52685-476">Это изменение исправляет форматирование Visual Studio для кода Razor для форматирования вкладок.</span><span class="sxs-lookup"><span data-stu-id="52685-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="52685-477">Поддержка правил переписывания URL при создании ссылок.</span><span class="sxs-lookup"><span data-stu-id="52685-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="52685-478">Удаление прозрачного атрибута безопасности.</span><span class="sxs-lookup"><span data-stu-id="52685-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="52685-479">Это нарушение изменения, и делает Razor 3 несовместимы с MVC4 и ранее, в то время как Razor 2 несовместим с MVC5 или сборки, составленные против MVC5.</span><span class="sxs-lookup"><span data-stu-id="52685-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="52685-480">Razor 3 вопросы, зафиксированные в Visual Studio 2013 из предварительного релиза версии можно найти [здесь](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="52685-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="52685-481">ASP.NET приложение Приостановить</span><span class="sxs-lookup"><span data-stu-id="52685-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="52685-482">ASP.NET App Suspend — это функция, меняющая правила игры в системе .NET 4.5.1, которая коренным образом меняет пользовательский опыт и экономическую модель размещения большого количества ASP.NET сайтов на одной машине.</span><span class="sxs-lookup"><span data-stu-id="52685-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="52685-483">Для получения дополнительной информации, см [ASP.NET App Приостановить - отзывчивый общий веб-хостинг .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span><span class="sxs-lookup"><span data-stu-id="52685-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="52685-484">Известные проблемы и ломая изменения</span><span class="sxs-lookup"><span data-stu-id="52685-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="52685-485">В этом разделе описаны известные проблемы и изменения в ASP.NET и веб-инструменты для визуальной студии 2013.</span><span class="sxs-lookup"><span data-stu-id="52685-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="52685-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="52685-486">NuGet</span></span>

- <span data-ttu-id="52685-487">[Восстановление нового пакета не работает на Mono при использовании файла SLN](https://nuget.codeplex.com/workitem/3596) - будет исправлено в предстоящей загрузке nuget.exe и обновлении [пакета NuGet.CommandLine.](http://www.nuget.org/packages/NuGet.CommandLine/)</span><span class="sxs-lookup"><span data-stu-id="52685-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="52685-488">[Восстановление нового пакета не работает с проектами Wix](https://nuget.codeplex.com/workitem/3598) - будет исправлено в предстоящей загрузке nuget.exe и обновлении [пакета NuGet.CommandLine.](http://www.nuget.org/packages/NuGet.CommandLine/)</span><span class="sxs-lookup"><span data-stu-id="52685-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="52685-489">[Автоматическое восстановление пакета не работает для проектов под папкой решения](https://nuget.codeplex.com/workitem/3625) - будет исправлено в NuGet 2.8.</span><span class="sxs-lookup"><span data-stu-id="52685-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="52685-490">Веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="52685-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="52685-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`не возвращается `IQueryable<T>` всегда, как мы `$select` `$expand`добавили поддержку и .</span><span class="sxs-lookup"><span data-stu-id="52685-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="52685-492">Наши предыдущие `ODataQueryOptions<T>` образцы для всегда `ApplyTo` casted значение возвращения от . `IQueryable<T>`</span><span class="sxs-lookup"><span data-stu-id="52685-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="52685-493">Это работало ранее, потому что`$filter`параметры `$orderby` `$skip`запроса, которые мы поддерживали ранее (, , `$top`) не меняют форму запроса.</span><span class="sxs-lookup"><span data-stu-id="52685-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="52685-494">Теперь, `$select` когда `$expand` мы поддерживаем `ApplyTo` и `IQueryable<T>` возвращение значение от не будет всегда.</span><span class="sxs-lookup"><span data-stu-id="52685-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="52685-495">Если вы используете образец кода из ранее, он будет `$select` `$expand`продолжать работать, если клиент не отправляет и .</span><span class="sxs-lookup"><span data-stu-id="52685-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="52685-496">Однако, если вы `$select` `$expand` хотите поддержать, и вы должны изменить этот код к этому.</span><span class="sxs-lookup"><span data-stu-id="52685-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="52685-497">**Request.Url или RequestContext.Url является недействительным во время пакетного запроса**</span><span class="sxs-lookup"><span data-stu-id="52685-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="52685-498">В сценарии пакетирования **UrlHelper** аннулируется при доступе к **Request.Url** или **RequestContext.Url**.</span><span class="sxs-lookup"><span data-stu-id="52685-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="52685-499">Эта проблема в настоящее время отслеживается здесь: [BatchRequestContext.Url является недействительным для пакетного запроса](http://aspnetwebstack.codeplex.com/workitem/1301).</span><span class="sxs-lookup"><span data-stu-id="52685-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="52685-500">Решением этой проблемы является создание нового экземпляра **UrlHelper,** как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="52685-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="52685-501">**Создание нового экземпляра UrlHelper**</span><span class="sxs-lookup"><span data-stu-id="52685-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="52685-502">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="52685-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="52685-503">При использовании MVC5 и OrgAuth, если у вас есть представления, которые делают проверку AntiForgerToken, вы можете встретить следующую ошибку при публикации данных в представлении:</span><span class="sxs-lookup"><span data-stu-id="52685-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="52685-504">**Ошибка**.</span><span class="sxs-lookup"><span data-stu-id="52685-504">**Error**:</span></span>

    <span data-ttu-id="52685-505">*Ошибка сервера в приложении «/».*</span><span class="sxs-lookup"><span data-stu-id="52685-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="52685-506"><em>Претензия типа<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' или<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' не присутствовала на предоставленной claimsIdentity. Для обеспечения поддержки токенов анти-подлога с помощью проверки подлинности на основе утверждений, пожалуйста, убедитесь, что настроенный поставщик претензий предоставляет обе эти требования в экземплярах ClaimsIdentity, которые он генерирует. Если настроенный поставщик претензий вместо этого использует другой тип претензий в качестве уникального идентификатора, его можно настроить, установив статическое свойство AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span><span class="sxs-lookup"><span data-stu-id="52685-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="52685-507">**Инструкции по решению**.</span><span class="sxs-lookup"><span data-stu-id="52685-507">**Workaround**:</span></span>

    <span data-ttu-id="52685-508">Добавьте следующую строку в Global.asax, чтобы исправить это:</span><span class="sxs-lookup"><span data-stu-id="52685-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="52685-509">Это будет исправлено для следующего релиза.</span><span class="sxs-lookup"><span data-stu-id="52685-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="52685-510">После обновления приложения MVC4 до MVC5 создайте решение и запустите его.</span><span class="sxs-lookup"><span data-stu-id="52685-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="52685-511">Вы должны увидеть следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="52685-511">You should see the following error:</span></span>

    <span data-ttu-id="52685-512">(А) System.Web.WebPages.Razor.Configuration.HostSection не может быть отлит на сайте «B'System.web.webPages.Razor.Configuration.HostSection».</span><span class="sxs-lookup"><span data-stu-id="52685-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="52685-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="52685-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="52685-514">Тип B происходит от 'System.Web.WebPages.Razor, Версия 3.0.0.0, Культура-нейтральная, PublicKeyToken-31bf3856ad364e35' в контексте 'По умолчанию' в месте 'C:'Windows-Microsoft.NET-Framework-v4.0.30319-Временный ASP.NET Файлы 005bbd0-e8b5908e-assembly-dl3-c9cbca63'f8910382\_6273ce01-System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="52685-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="52685-515">Чтобы исправить вышеупомянутую ошибку, откройте *все* файлы Web.config (включая файлы в папке Views) в проекте и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="52685-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="52685-516">Обновление всех случаев версии "4.0.0.0. " "System.Web.Mvc" до "5.0.0.0.0".</span><span class="sxs-lookup"><span data-stu-id="52685-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="52685-517">Обновление всех случаев версии "2.0.0.0.0" &quot;"System.Web.Helpers",&quot; &quot;System.Web.WebPages и&quot; System.web.web.WebPages.Razor до "3.0.0.0"</span><span class="sxs-lookup"><span data-stu-id="52685-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="52685-518">Например, после внесения вышеуказанных изменений привязки сборки должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="52685-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="52685-519">Для получения информации о модернизации проектов MVC 4 до MVC 5, [см. Как обновить ASP.NET MVC 4 и Web API проекта ASP.NET MVC 5 и Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="52685-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="52685-520">При использовании проверки на стороне клиента с помощью ненавязчивой валидации j'ery, сообщение о проверке иногда некорректно для элемента ввода HTML с числом типа.</span><span class="sxs-lookup"><span data-stu-id="52685-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="52685-521">Ошибка проверки требуемого значения ("Необходимое поле возраста") отображается при входе недействительного номера вместо правильного сообщения о том, что требуется допустимый номер.</span><span class="sxs-lookup"><span data-stu-id="52685-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="52685-522">Эта проблема обычно встречается с эшафот код для модели с целью собственности на Создание и отодвинет представления.</span><span class="sxs-lookup"><span data-stu-id="52685-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="52685-523">Чтобы обойти этот вопрос, измените помощника редактора из:</span><span class="sxs-lookup"><span data-stu-id="52685-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="52685-524">на:</span><span class="sxs-lookup"><span data-stu-id="52685-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="52685-525">ASP.NET MVC 5 больше не поддерживает частичное доверие.</span><span class="sxs-lookup"><span data-stu-id="52685-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="52685-526">Проекты, связанные с файлами mVC или WebAPI, должны удалить атрибут [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) и атрибут [AllowPartiallyTrustedCallers.](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)</span><span class="sxs-lookup"><span data-stu-id="52685-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="52685-527">Удаление этих атрибутов позволит устранить ошибки компилятора, такие как следующие.</span><span class="sxs-lookup"><span data-stu-id="52685-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="52685-528">Обратите внимание, что в качестве побочного эффекта вы не можете использовать сборки 4.0 и 5.0 в одном приложении.</span><span class="sxs-lookup"><span data-stu-id="52685-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="52685-529">Вам нужно обновить все из них до 5.0.</span><span class="sxs-lookup"><span data-stu-id="52685-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="52685-530">SPA Template с разрешением Facebook может вызвать нестабильность в IE, в то время как веб-сайт размещается в зоне интрасети</span><span class="sxs-lookup"><span data-stu-id="52685-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="52685-531">Шаблон SPA обеспечивает внешний вход в систему с Facebook.</span><span class="sxs-lookup"><span data-stu-id="52685-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="52685-532">Когда проект, созданный с помощью шаблона, работает локально, входе может привести к сбою IE.</span><span class="sxs-lookup"><span data-stu-id="52685-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="52685-533">Решение.</span><span class="sxs-lookup"><span data-stu-id="52685-533">Solution:</span></span>

1. <span data-ttu-id="52685-534">Размещение веб-сайта в интернет-зоне; Или</span><span class="sxs-lookup"><span data-stu-id="52685-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="52685-535">Проверьте сценарий в браузере, кроме IE.</span><span class="sxs-lookup"><span data-stu-id="52685-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="52685-536">Формирование шаблонов веб-форм</span><span class="sxs-lookup"><span data-stu-id="52685-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="52685-537">Веб-формы Scaffolding был удален из VS2013 и будет доступен в будущем обновлении Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52685-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="52685-538">Тем не менее, вы все еще можете использовать леса в рамках проекта Web Forms, добавляя mVC зависимостей и генерации строительных лесов для MVC.</span><span class="sxs-lookup"><span data-stu-id="52685-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="52685-539">Ваш проект будет содержать сочетание веб-форм и MVC.</span><span class="sxs-lookup"><span data-stu-id="52685-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="52685-540">Чтобы добавить MVC в проект Web Forms, добавьте новый элемент с эшафотами и выберите **зависимости MVC 5.**</span><span class="sxs-lookup"><span data-stu-id="52685-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="52685-541">Выберите минимальный или полный в зависимости от того, нужны ли вам все файлы содержимого, такие как скрипты.</span><span class="sxs-lookup"><span data-stu-id="52685-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="52685-542">Затем добавьте эшафот для MVC, который создаст представления и контроллер в вашем проекте.</span><span class="sxs-lookup"><span data-stu-id="52685-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="52685-543">MVC и Web API Scaffolding - HTTP 404, не найдена ошибка</span><span class="sxs-lookup"><span data-stu-id="52685-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="52685-544">Если при добавлении элемента с эшафотом в проект возникнет ошибка, возможно, ваш проект останется в несогласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="52685-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="52685-545">Некоторые изменения, внесенные в строительные леса, будут отброшены назад, но другие изменения, такие как установленные пакеты NuGet, не будут отброшены назад.</span><span class="sxs-lookup"><span data-stu-id="52685-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="52685-546">Если изменения конфигурации реаутинга откатываются, пользователи получат ошибку HTTP 404 при навигации по эшафотным элементам.</span><span class="sxs-lookup"><span data-stu-id="52685-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="52685-547">Обходное решение.</span><span class="sxs-lookup"><span data-stu-id="52685-547">Workaround:</span></span>

- <span data-ttu-id="52685-548">Чтобы исправить эту ошибку для MVC, добавьте новый элемент леса и выберите MVC 5 зависимостей (минимальные или полные).</span><span class="sxs-lookup"><span data-stu-id="52685-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="52685-549">Этот процесс добавит все необходимые изменения в проект.</span><span class="sxs-lookup"><span data-stu-id="52685-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="52685-550">Чтобы исправить эту ошибку для Web API:</span><span class="sxs-lookup"><span data-stu-id="52685-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="52685-551">Добавьте класс WebApiConfig в свой проект.</span><span class="sxs-lookup"><span data-stu-id="52685-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="52685-552">Нанастройка WebApiConfig.Register\_в методе запуска приложений в Global.asax следующим образом:</span><span class="sxs-lookup"><span data-stu-id="52685-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
