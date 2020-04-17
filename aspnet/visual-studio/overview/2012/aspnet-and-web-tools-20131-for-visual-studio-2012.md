---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Выпуск Заметки для ASP.NET и веб-инструменты 2013.1 для визуальной студии 2012 Документы Майкрософт
author: rick-anderson
description: В этом документе описывается выпуск ASP.NET и Web Tools 2013.1 для Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543578"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="ee874-103">Заметки о выпуске ASP.NET and Web Tools 2013.1 для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ee874-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="ee874-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ee874-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ee874-105">В этом документе описывается выпуск ASP.NET и Web Tools 2013.1 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ee874-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="ee874-106">Содержимое</span><span class="sxs-lookup"><span data-stu-id="ee874-106">Contents</span></span>

- [<span data-ttu-id="ee874-107">Примечания к установке</span><span class="sxs-lookup"><span data-stu-id="ee874-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="ee874-108">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="ee874-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="ee874-109">Новые возможности в ASP.NET и веб-инструменты 2013.1 для визуальной студии 2012</span><span class="sxs-lookup"><span data-stu-id="ee874-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="ee874-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="ee874-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="ee874-111">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="ee874-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="ee874-112">ASP.NET mVC 5 шаблон</span><span class="sxs-lookup"><span data-stu-id="ee874-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="ee874-113">шаблон web API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ee874-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="ee874-114">Шаблоны элементов</span><span class="sxs-lookup"><span data-stu-id="ee874-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="ee874-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ee874-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="ee874-116">ASP.NET Леса</span><span class="sxs-lookup"><span data-stu-id="ee874-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="ee874-117">Редактор бритвы</span><span class="sxs-lookup"><span data-stu-id="ee874-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="ee874-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="ee874-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="ee874-119">Известные проблемы и ломая изменения</span><span class="sxs-lookup"><span data-stu-id="ee874-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="ee874-120">ASP.NET Леса</span><span class="sxs-lookup"><span data-stu-id="ee874-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="ee874-121">MVC и Web API Scaffolding - HTTP 404, не найдена ошибка</span><span class="sxs-lookup"><span data-stu-id="ee874-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="ee874-122">Visual Studio Express 2012 для Веб перестает работать после добавления эшафот пункт</span><span class="sxs-lookup"><span data-stu-id="ee874-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="ee874-123">ASP.NET бритва 3</span><span class="sxs-lookup"><span data-stu-id="ee874-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="ee874-124">Просмотр файла cshtml с помощью Browse With или F5 вызывает ошибку сервера</span><span class="sxs-lookup"><span data-stu-id="ee874-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="ee874-125">Урл Переписать и Тильде (яп.)</span><span class="sxs-lookup"><span data-stu-id="ee874-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="ee874-126">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="ee874-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="ee874-127">Замечания по установке</span><span class="sxs-lookup"><span data-stu-id="ee874-127">Installation Notes</span></span>

<span data-ttu-id="ee874-128">[Установка](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET и web Tools 2013.1 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ee874-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="ee874-129">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="ee874-129">Software Requirements</span></span>

<span data-ttu-id="ee874-130">Вы должны иметь либо Visual Studio 2012 или Visual Studio Express 2012 для Интернета.</span><span class="sxs-lookup"><span data-stu-id="ee874-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="ee874-131">Новые возможности в ASP.NET и веб-инструменты 2013.1 для визуальной студии 2012</span><span class="sxs-lookup"><span data-stu-id="ee874-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="ee874-132">Начальная загрузка</span><span class="sxs-lookup"><span data-stu-id="ee874-132">Bootstrap</span></span>

<span data-ttu-id="ee874-133">Когда вы подмостки MVC 5 контроллеров и представлений, разметка для представлений использует [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="ee874-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="ee874-134">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="ee874-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="ee874-135">ASP.NET mVC 5 шаблон</span><span class="sxs-lookup"><span data-stu-id="ee874-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="ee874-136">Мы добавили новый шаблон MVC 5.</span><span class="sxs-lookup"><span data-stu-id="ee874-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="ee874-137">Он ссылается на последние пакеты MVC 5 NuGet, и вы можете использовать строительные леса, чтобы добавить контроллеры и представления.</span><span class="sxs-lookup"><span data-stu-id="ee874-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="ee874-138">шаблон web API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ee874-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="ee874-139">Мы добавили новый шаблон Web API 2.</span><span class="sxs-lookup"><span data-stu-id="ee874-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="ee874-140">Он ссылается на последние web API 2 NuGet пакеты, и вы можете использовать леса, чтобы добавить контроллеры и представления.</span><span class="sxs-lookup"><span data-stu-id="ee874-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="ee874-141">Шаблоны элементов</span><span class="sxs-lookup"><span data-stu-id="ee874-141">Item Templates</span></span>

<span data-ttu-id="ee874-142">Мы добавили новые шаблоны элементов для просмотров MVC 5, веб-страниц (Razor 3) и контроллеров Web API 2.</span><span class="sxs-lookup"><span data-stu-id="ee874-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="ee874-143">Они устанавливают связанные пакеты NuGet в проект при добавлении новых элементов.</span><span class="sxs-lookup"><span data-stu-id="ee874-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="ee874-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ee874-144">Entity Framework 6</span></span>

<span data-ttu-id="ee874-145">Когда вы подмостки MVC или веб-контроллер API с помощью Entity Framework, мы используем Framework 6.</span><span class="sxs-lookup"><span data-stu-id="ee874-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="ee874-146">Для получения дополнительной информации [Entity Framework Version History](https://msdn.com/data/jj574253)о рамочной системе сущностей см.</span><span class="sxs-lookup"><span data-stu-id="ee874-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="ee874-147">Вы также можете скачать и установить Entity Framework 6 Инструменты для визуальной студии 2012.</span><span class="sxs-lookup"><span data-stu-id="ee874-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="ee874-148">Посмотреть [рамочную программу Get Entity.](https://msdn.com/data/ee712906#tooling)</span><span class="sxs-lookup"><span data-stu-id="ee874-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="ee874-149">ASP.NET Леса</span><span class="sxs-lookup"><span data-stu-id="ee874-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="ee874-150">ASP.NET Scaffolding — это платформа для генерации кода для ASP.NET веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="ee874-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="ee874-151">Это упрощает добавление шаблонного кода в проект, который взаимодействует с моделью данных.</span><span class="sxs-lookup"><span data-stu-id="ee874-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="ee874-152">В предыдущих версиях Visual Studio строительные леса ограничивались ASP.NET проектами MVC.</span><span class="sxs-lookup"><span data-stu-id="ee874-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="ee874-153">С помощью этого обновления теперь можно использовать строительные леса для любого ASP.NET проекта, включая веб-формы.</span><span class="sxs-lookup"><span data-stu-id="ee874-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="ee874-154">Это обновление не поддерживает генерацию страниц для проекта Web Forms, но вы все равно можете использовать строительные леса с веб-формами, добавляя в проект зависимости MVC.</span><span class="sxs-lookup"><span data-stu-id="ee874-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="ee874-155">Поддержка создания страниц для веб-форм будет добавлена в будущем обновлении.</span><span class="sxs-lookup"><span data-stu-id="ee874-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="ee874-156">При использовании строительных лесов мы гарантируем, что все необходимые зависимости установлены в проекте.</span><span class="sxs-lookup"><span data-stu-id="ee874-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="ee874-157">Например, если вы начинаете с проекта ASP.NET web Forms, а затем используете строительные леса для добавления контроллера Web API, необходимые пакеты и ссылки NuGet добавляются в ваш проект автоматически.</span><span class="sxs-lookup"><span data-stu-id="ee874-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="ee874-158">Чтобы добавить строительные леса MVC в проект Web Forms, добавьте **новый элемент Scaffolded** и выберите **MVC 5 Зависимости** в окне диалога.</span><span class="sxs-lookup"><span data-stu-id="ee874-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="ee874-159">Есть два варианта для строительных лесов MVC; Минимальный и полный.</span><span class="sxs-lookup"><span data-stu-id="ee874-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="ee874-160">Если вы выберете Minimal, в проект добавляются только пакеты и ссылки NuGet для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="ee874-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="ee874-161">При выборе опции Full добавлены минимальные зависимости, а также необходимые файлы содержимого для проекта MVC.</span><span class="sxs-lookup"><span data-stu-id="ee874-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="ee874-162">Поддержка контроллеров асин для строительных лесов использует новые функции async из Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="ee874-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="ee874-163">Для получения дополнительной информации и учебников, см [ASP.NET Scaffolding Обзор](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee874-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="ee874-164">Эти учебники показывают леса с Visual Studio 2013, но они также применимы к ASP.NET и Web Tools 2013.1 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ee874-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="ee874-165">Редактор бритвы</span><span class="sxs-lookup"><span data-stu-id="ee874-165">Razor Editor</span></span>

<span data-ttu-id="ee874-166">С этим обновлением, Visual Studio 2012 теперь поддерживает Razor 3 инструментария / редактирования.</span><span class="sxs-lookup"><span data-stu-id="ee874-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="ee874-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="ee874-167">NuGet 2.7</span></span>

<span data-ttu-id="ee874-168">NuGet 2.7 включает в себя богатый набор новых функций, которые подробно описаны на [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="ee874-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="ee874-169">Эта версия NuGet устраняет необходимость для пользователей явно разрешить NuGet восстановить недостающие пакеты.</span><span class="sxs-lookup"><span data-stu-id="ee874-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="ee874-170">При установке NuGet 2.7 пользователи косвенно соглашаются на автоматическое восстановление недостающих пакетов.</span><span class="sxs-lookup"><span data-stu-id="ee874-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="ee874-171">Пользователи могут отказаться от восстановления пакета через настройки NuGet в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee874-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="ee874-172">Это изменение упрощает работу восстановления пакетов.</span><span class="sxs-lookup"><span data-stu-id="ee874-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="ee874-173">Известные проблемы и ломая изменения</span><span class="sxs-lookup"><span data-stu-id="ee874-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="ee874-174">ASP.NET Леса</span><span class="sxs-lookup"><span data-stu-id="ee874-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="ee874-175">MVC и Web API Scaffolding - HTTP 404, не найдена ошибка</span><span class="sxs-lookup"><span data-stu-id="ee874-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="ee874-176">Если вы столкнулись с ошибкой при добавлении элемента с эшафотом в проект, возможно, ваш проект останется в несогласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="ee874-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="ee874-177">Некоторые изменения, внесенные в строительные леса, будут отброшены назад, но другие изменения, такие как установленные пакеты NuGet, не будут отброшены назад.</span><span class="sxs-lookup"><span data-stu-id="ee874-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="ee874-178">Если изменения конфигурации реаутинга откатываются, пользователи получат ошибку HTTP 404 при навигации по эшафотным элементам.</span><span class="sxs-lookup"><span data-stu-id="ee874-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="ee874-179">Чтобы исправить эту ошибку для MVC, добавьте новый элемент леса и выберите MVC 5 зависимостей (минимальные или полные).</span><span class="sxs-lookup"><span data-stu-id="ee874-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="ee874-180">Этот процесс добавит все необходимые изменения в проект.</span><span class="sxs-lookup"><span data-stu-id="ee874-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="ee874-181">Чтобы исправить эту ошибку для Web API:</span><span class="sxs-lookup"><span data-stu-id="ee874-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="ee874-182">Добавьте в проект следующий класс WebApiConfig.</span><span class="sxs-lookup"><span data-stu-id="ee874-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="ee874-183">Нанастройка WebApiConfig.Register\_в методе запуска приложений в Global.asax следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ee874-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="ee874-184">Visual Studio Express 2012 для Веб перестает работать после добавления эшафот пункт</span><span class="sxs-lookup"><span data-stu-id="ee874-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="ee874-185">Если Visual Studio Express 2012 для Web перестанет работать после добавления эшафота элемента с Entity Framework (например, Web API 2 Контроллер с действиями, используя Entity Framework), возможно, что Visual Studio Express не удалось загрузить родной образ сборки зависит от System.Web.Extensions.</span><span class="sxs-lookup"><span data-stu-id="ee874-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="ee874-186">Чтобы исправить эту проблему, настройте Visual Studio Express для работы с MSIL изображением System.Web.Extensions:</span><span class="sxs-lookup"><span data-stu-id="ee874-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="ee874-187">Open Command Prompt в режиме администратора.</span><span class="sxs-lookup"><span data-stu-id="ee874-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="ee874-188">Перейдите к %ProgramFiles% -Microsoft Visual Studio 11.0-Common7-IDE или %ProgramFiles (x86)% -Microsoft Visual Studio 11.0"Common7'IDE (для 64-битной Windows).</span><span class="sxs-lookup"><span data-stu-id="ee874-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="ee874-189">Открыть VWDExpress.exe.config в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="ee874-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="ee874-190">Добавьте следующую &lt;строку&gt; под элементом времени выполнения конфигурации:&gt;/&lt;</span><span class="sxs-lookup"><span data-stu-id="ee874-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="ee874-191">Перезапуск Visual Studio Express 2012 для Интернета.</span><span class="sxs-lookup"><span data-stu-id="ee874-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="ee874-192">ASP.NET бритва 3</span><span class="sxs-lookup"><span data-stu-id="ee874-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="ee874-193">Просмотр файла cshtml с помощью Browse With или F5 вызывает ошибку сервера</span><span class="sxs-lookup"><span data-stu-id="ee874-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="ee874-194">При создании проекта MVC 5 в Visual Studio 2012 (или открыть в Visual Studio 2012 проект MVC 5, который был создан в Visual Studio 2013) и попытаться просмотреть файл cshtml с помощью Browse With или F5, вы получите ошибку, которая гласит - **Ошибка сервера в '/' Приложение**.</span><span class="sxs-lookup"><span data-stu-id="ee874-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="ee874-195">Сервер пытается перейти к`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="ee874-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="ee874-196">Чтобы решить эту проблему, измените настройку **start Action** в проекте на **конкретную страницу.**</span><span class="sxs-lookup"><span data-stu-id="ee874-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="ee874-197">Вам не нужно предоставлять значение для страницы.</span><span class="sxs-lookup"><span data-stu-id="ee874-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="ee874-198">После внесения этого изменения, выбрав F5 переходит`http://localhost:XXXX`к корню приложения ( ).</span><span class="sxs-lookup"><span data-stu-id="ee874-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="ee874-199">Это поведение не то же самое, что поведение для проектов MVC 5 в Visual Studio 2013, где **настройка текущей страницы** запускает открытую страницу.</span><span class="sxs-lookup"><span data-stu-id="ee874-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="ee874-200">Урл Переписать и Тильде (яп.)</span><span class="sxs-lookup"><span data-stu-id="ee874-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="ee874-201">После обновления до ASP.NET Razor 3 или ASP.NET MVC 5, нотация tilde может больше не работать правильно, если вы используете перезаписи URL.</span><span class="sxs-lookup"><span data-stu-id="ee874-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="ee874-202">Перезапись URL-адреса влияет на нотацию tilde (я)&gt; &lt;в&gt;HTML-элементах, таких как &lt; &lt;A/ SCRIPT/ , LINK/&gt;, и в результате tilde больше не отображает карты в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="ee874-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="ee874-203">Например, если вы переписываете запросы на **asp.net/content** **asp.net,** &lt;атрибут href в&gt; A href'/content/"/ **/** разрешает **/content/content/** вместо .</span><span class="sxs-lookup"><span data-stu-id="ee874-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="ee874-204">Чтобы подавить это изменение, можно настроить контекст **IIS\_WasUrlRewritten** на ложный на каждой веб-странице или в **\_Application BeginRequest** в Global.asax.</span><span class="sxs-lookup"><span data-stu-id="ee874-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="ee874-205">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="ee874-205">Templates</span></span>

<span data-ttu-id="ee874-206">При создании ASP.NET проектов MVC с Visual Studio 2012 на Windows 8.1 или Windows Server 2012 R2, Visual Studio отображает сообщение об ошибке, в которое говорится: «Настройка Web для ASP.NET 4.5 не удалось».</span><span class="sxs-lookup"><span data-stu-id="ee874-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![ошибка конфигурации](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="ee874-208">Вы видите эту ошибку, потому что Visual Studio 2012 не включает функцию ASP.NET 4.5 при установке на эти релизы Windows.</span><span class="sxs-lookup"><span data-stu-id="ee874-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="ee874-209">Для включения или выключения ASP.NET 4.5 выполняйте действия, описанные в [функциях Включайте или выключаемого.](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)</span><span class="sxs-lookup"><span data-stu-id="ee874-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Включать или выключать функции Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="ee874-211">Кроме того, можно включить ASP.NET 4.5 через командную строку.</span><span class="sxs-lookup"><span data-stu-id="ee874-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="ee874-212">Open Command Prompt в режиме администратора.</span><span class="sxs-lookup"><span data-stu-id="ee874-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="ee874-213">Выполнить следующую команду, чтобы включить ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="ee874-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
