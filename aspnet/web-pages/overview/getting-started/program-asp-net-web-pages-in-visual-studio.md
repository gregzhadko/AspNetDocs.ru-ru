---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Программирование ASP.NET веб-страниц (Razor) с помощью визуальной студии (ru) Документы Майкрософт
author: Rick-Anderson
description: В этом приложении объясняется, как можно использовать Visual Studio 2010 или Visual Web Developer 2010 Express для программы ASP.NET веб-страниц с помощью синтаксиса Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542902"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="b2131-103">Программирование ASP.NET веб-страниц (Razor) с помощью визуальной студии</span><span class="sxs-lookup"><span data-stu-id="b2131-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="b2131-104">; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b2131-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b2131-105">В этой статье объясняется, как можно использовать Visual Studio или Visual Web Developer Express для программы ASP.NET веб-страниц (Razor) веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="b2131-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="b2131-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="b2131-106">What you'll learn</span></span>
>
> - <span data-ttu-id="b2131-107">Что нужно установить (если что) для работы с веб-страницами ASP.NET в вашей версии Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="b2131-108">Как добавить поддержку для веб-страниц ASP.NET Visual Web Developer 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="b2131-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="b2131-109">Как использовать функции в Visual Studio для работы с ASP.NET страниц, включая IntelliSense и отладчик.</span><span class="sxs-lookup"><span data-stu-id="b2131-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b2131-110">Версии программного обеспечения, используемые в учебнике</span><span class="sxs-lookup"><span data-stu-id="b2131-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="b2131-111">ASP.NET веб-страниц (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="b2131-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="b2131-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b2131-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="b2131-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="b2131-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="b2131-114">Этот учебник также работает с ASP.NET web Pages 2, Visual Studio 2012, Visual Studio 2010 и WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="b2131-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="b2131-115">Вы можете запрограммировать ASP.NET веб-страниц с помощью синтаксиса Razor с помощью WebMatrix или многих других редакторов кода.</span><span class="sxs-lookup"><span data-stu-id="b2131-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="b2131-116">Вы также можете использовать Microsoft Visual Studio, которая является полнофункциональным интегрированной средой разработки (IDE), которая обеспечивает мощный набор инструментов для создания многих типов приложений (а не только веб-сайтов).</span><span class="sxs-lookup"><span data-stu-id="b2131-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="b2131-117">Для работы с ASP.NET страниц razor, вы можете использовать [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="b2131-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="b2131-118">Две особенно полезные функции, которые Visual Studio предоставляет для программирования с ASP.NET веб-страниц Razor являются:</span><span class="sxs-lookup"><span data-stu-id="b2131-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="b2131-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="b2131-119">*IntelliSense*.</span></span> <span data-ttu-id="b2131-120">Функция IntelliSense, встроенная в Visual Studio, более полная, чем IntelliSense в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="b2131-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="b2131-121">*Дебудгер*.</span><span class="sxs-lookup"><span data-stu-id="b2131-121">*Debugger*.</span></span> <span data-ttu-id="b2131-122">Отладчик позволяет устранить неполадки, остановив программу во время ее работы, изучая переменные и перешагнув строку кода по строке.</span><span class="sxs-lookup"><span data-stu-id="b2131-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="b2131-123">Использование Visual Studio с различными версиями ASP.NET веб-страниц</span><span class="sxs-lookup"><span data-stu-id="b2131-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="b2131-124">Для разработки ASP.NET веб-приложений в Visual Studio 2017, установите рабочую нагрузку **ASP.NET и веб-разработки.**</span><span class="sxs-lookup"><span data-stu-id="b2131-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="b2131-125">Visual Studio 2012 и Visual Studio 2013 включают поддержку ASP.NET веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="b2131-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="b2131-126">(Пакеты, необходимые для поддержки ASP.NET веб-страниц, устанавливаются при установке Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="b2131-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="b2131-127">Visual Studio 2010 не включает поддержку по умолчанию для ASP.NET web Pages.</span><span class="sxs-lookup"><span data-stu-id="b2131-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="b2131-128">Чтобы использовать ASP.NET веб-страницсы с Visual Studio 2010, необходимо установить пакет mVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b2131-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="b2131-129">Чтобы получить ASP.NET веб-страниц 2, вы установите ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b2131-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="b2131-130">В следующей таблице кратко излагается поддержка веб-страниц ASP.NET в различных версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="b2131-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="b2131-131">Visual Studio 2010</span></span> | <span data-ttu-id="b2131-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b2131-132">Visual Studio 2012</span></span> | <span data-ttu-id="b2131-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b2131-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2131-134">**Веб-страницы ASP.NET 2**</span><span class="sxs-lookup"><span data-stu-id="b2131-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="b2131-135">Установка ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="b2131-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="b2131-136">(Включено)</span><span class="sxs-lookup"><span data-stu-id="b2131-136">(Included)</span></span> | <span data-ttu-id="b2131-137">(Включено)</span><span class="sxs-lookup"><span data-stu-id="b2131-137">(Included)</span></span> |
| <span data-ttu-id="b2131-138">**Веб-страницы ASP.NET 3**</span><span class="sxs-lookup"><span data-stu-id="b2131-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="b2131-139">Обновление для ASP.NET веб-страниц 3 через NuGet</span><span class="sxs-lookup"><span data-stu-id="b2131-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="b2131-140">(Включено)</span><span class="sxs-lookup"><span data-stu-id="b2131-140">(Included)</span></span> |

<span data-ttu-id="b2131-141">Для работы с Visual Studio 2010, см [Установка поддержки для ASP.NET веб-страниц в Visual Studio 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="b2131-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="b2131-142">Запуск визуальной студии от WebMatrix</span><span class="sxs-lookup"><span data-stu-id="b2131-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="b2131-143">Если вы начали проект в WebMatrix и хотите перейти на Visual Studio, WebMatrix предоставляет кнопку, чтобы легко открыть проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="b2131-144">Для включения этой кнопки на компьютере должна быть установлена Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="b2131-145">Следующее изображение показывает кнопку в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="b2131-145">The following image shows the button in WebMatrix.</span></span>

![запуск Визуальной студии](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="b2131-147">При нажатии кнопки проект открывается в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="b2131-148">Вы можете переключаться между WebMatrix и Visual Studio без каких-либо проблем.</span><span class="sxs-lookup"><span data-stu-id="b2131-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="b2131-149">Вы будете уведомлены, если какие-либо файлы изменились в другой среде и должны быть перезагружены, чтобы получить последние изменения.</span><span class="sxs-lookup"><span data-stu-id="b2131-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="b2131-150">Создание сайта ASP.NET Razor в визуальной студии</span><span class="sxs-lookup"><span data-stu-id="b2131-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="b2131-151">Чтобы создать веб-сайт ASP.NET Razor в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b2131-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="b2131-152">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="b2131-153">В меню **файла** нажмите **новый веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="b2131-153">In the **File** menu, click **New Web Site**.</span></span>

    ![создать новый веб-сайт](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="b2131-155">В новом диалоговом окне **веб-сайта** выберите язык для использования (Visual C или Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="b2131-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="b2131-156">Выберите шаблон **веб-сайта ASP.NET (Razor).**</span><span class="sxs-lookup"><span data-stu-id="b2131-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor сайт](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="b2131-158">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b2131-158">Click **OK**.</span></span>

<span data-ttu-id="b2131-159">Ваш новый проект существует и населен некоторыми веб-страницами по умолчанию, которые помогут вам начать работу.</span><span class="sxs-lookup"><span data-stu-id="b2131-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="b2131-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b2131-160">Using IntelliSense</span></span>

<span data-ttu-id="b2131-161">Теперь, когда вы создали сайт, вы можете увидеть, как работает IntelliSense в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2131-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="b2131-162">На сайте, который вы только что создали, откройте страницу *Default.cshtml.*</span><span class="sxs-lookup"><span data-stu-id="b2131-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="b2131-163">После `<h3>` тегов на странице `@ServerInfo.` введите (включая точку).</span><span class="sxs-lookup"><span data-stu-id="b2131-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="b2131-164">Обратите внимание, как IntelliSense отображает `ServerInfo` доступные методы для помощника в списке выпадающих.</span><span class="sxs-lookup"><span data-stu-id="b2131-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="b2131-166">Выберите `GetHtml` метод из списка, а затем нажмите Enter.</span><span class="sxs-lookup"><span data-stu-id="b2131-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="b2131-167">IntelliSense автоматически заполняет метод.</span><span class="sxs-lookup"><span data-stu-id="b2131-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="b2131-168">(Как и в случае с любым `()` методом в C, вы должны добавить символы после метода.) Завершенный код `GetHtml` для метода выглядит следующим примером:</span><span class="sxs-lookup"><span data-stu-id="b2131-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="b2131-169">Нажмите ctrl-F5, чтобы запустить страницу.</span><span class="sxs-lookup"><span data-stu-id="b2131-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="b2131-170">Вот как выглядит страница при отображении в браузере:</span><span class="sxs-lookup"><span data-stu-id="b2131-170">This is what the page looks like when displayed in a browser:</span></span>

    ![страница по умолчанию в браузере](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="b2131-172">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="b2131-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="b2131-173">Использование debugger</span><span class="sxs-lookup"><span data-stu-id="b2131-173">Using the Debugger</span></span>

1. <span data-ttu-id="b2131-174">В верхней части страницы *Default.cshtml,* после `Page.Title`строки, которая начинается с, добавьте следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="b2131-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="b2131-175">В сером крае редактора слева от кода нажмите рядом с этой новой строкой, чтобы добавить *точку разрыва.*</span><span class="sxs-lookup"><span data-stu-id="b2131-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="b2131-176">Точка разрыва — это маркер, который говорит отладчику прекратить запуск программы в этот момент, чтобы вы могли видеть, что происходит.</span><span class="sxs-lookup"><span data-stu-id="b2131-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![установка точки останова](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="b2131-178">Удалите вызов `ServerInfo.GetHtml` методу и добавьте `@myTime` вызов к переменной на своем месте.</span><span class="sxs-lookup"><span data-stu-id="b2131-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="b2131-179">Этот вызов отображает текущее значение времени, возвращенное новой строкой кода.</span><span class="sxs-lookup"><span data-stu-id="b2131-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="b2131-180">Нажмите F5, чтобы запустить страницу в отладчике.</span><span class="sxs-lookup"><span data-stu-id="b2131-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="b2131-181">Страница останавливается на точке разрыва, которую вы установили.</span><span class="sxs-lookup"><span data-stu-id="b2131-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="b2131-182">Следующее изображение показывает, как выглядит страница в редакторе с точкой разрыва (желтым цветом).</span><span class="sxs-lookup"><span data-stu-id="b2131-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![точка разрыва отладки](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="b2131-184">В панели инструментов Debug нажмите кнопку **«Шаг в»** (или нажмите F11), чтобы запустить следующую строку кода.</span><span class="sxs-lookup"><span data-stu-id="b2131-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="b2131-185">Каждый раз, когда вы нажимаете на эту кнопку, вы продвигаете выполнение к следующей строке кода.</span><span class="sxs-lookup"><span data-stu-id="b2131-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Шаг в кнопку](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="b2131-187">Изучите значение `myTime` переменной, удерживая указатель мыши над ней или проверяя значения, отображаемые в окнах **Locals** и **Call Stack.**</span><span class="sxs-lookup"><span data-stu-id="b2131-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="b2131-188">Visual Studio отображает значение переменной.</span><span class="sxs-lookup"><span data-stu-id="b2131-188">Visual Studio display the value of the variable.</span></span>

    ![значение времени показа](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="b2131-190">Когда вы закончите изучение переменной и прохождение кода, нажмите F5, чтобы продолжить работу страницы, не останавливаясь на каждой строке.</span><span class="sxs-lookup"><span data-stu-id="b2131-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="b2131-191">Когда вы закончите шаг через весь код, браузер отображает страницу.</span><span class="sxs-lookup"><span data-stu-id="b2131-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="b2131-192">Чтобы узнать больше об отладчике и о том, как отладить код в Visual Studio, смотрите [Walkthrough: Отладка веб-страниц в визуальном веб-разработчике.](https://msdn.microsoft.com/library/z9e7w6cs.aspx)</span><span class="sxs-lookup"><span data-stu-id="b2131-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="b2131-193">Использование Razor в ASP.NET проектов MVC с Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b2131-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="b2131-194">Синтаксис Razor также широко используется в ASP.NET проектах MVC.</span><span class="sxs-lookup"><span data-stu-id="b2131-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="b2131-195">MVC — это мощный способ создания динамических веб-сайтов на основе шаблонов.</span><span class="sxs-lookup"><span data-stu-id="b2131-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="b2131-196">Если ваш ASP.NET веб-страницу становится трудно поддерживать, можно рассмотреть возможность его преобразования в ASP.NET приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="b2131-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="b2131-197">Например, при создании приложения MVC см. [Начало работы с ASP.NET MVC 5.](../../../mvc/overview/getting-started/introduction/getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="b2131-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="b2131-198">Установка поддержки для веб-страниц ASP.NET в визуальной студии 2010</span><span class="sxs-lookup"><span data-stu-id="b2131-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="b2131-199">В этом разделе показано, как установить Visual Web Developer Express 2010 и ASP.NET веб-страниц инструменты для визуальной студии.</span><span class="sxs-lookup"><span data-stu-id="b2131-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="b2131-200">Если у вас еще нет web-платформы Установщик, загрузите его из следующего URL:</span><span class="sxs-lookup"><span data-stu-id="b2131-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="b2131-201">Выполнить веб-платформы Установки.</span><span class="sxs-lookup"><span data-stu-id="b2131-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="b2131-202">Нажмите на вкладку **«Продукты».**</span><span class="sxs-lookup"><span data-stu-id="b2131-202">Click the **Products** tab.</span></span>

    ![Вкладка Продуктов WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="b2131-204">Поиск **ASP.NET MVC 4** (для ASP.NET веб-страниц 2), а затем нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b2131-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="b2131-205">Эти продукты включают в себя инструменты Visual Studio для создания ASP.NET веб-сайтов Razor.</span><span class="sxs-lookup"><span data-stu-id="b2131-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![Параметры установки WebPi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="b2131-207">Нажмите **Установить** для завершения установки.</span><span class="sxs-lookup"><span data-stu-id="b2131-207">Click **Install** to complete the installation.</span></span>
