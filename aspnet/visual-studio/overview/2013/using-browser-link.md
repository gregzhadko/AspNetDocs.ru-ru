---
uid: visual-studio/overview/2013/using-browser-link
title: Использование привязывания к браузеру в Visual Studio 2013 | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395099"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="a9c7a-102">Использование привязывания к браузеру в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a9c7a-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="a9c7a-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a9c7a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a9c7a-104">Связь с браузером — это новая функция в Visual Studio 2013, который создает канал взаимодействия между средой разработки и один или несколько веб-браузеров.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="a9c7a-105">Можно использовать связь с браузером для обновления веб-приложения в нескольких браузерах одновременно, что полезно для тестирования обозреватели.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="a9c7a-106">Браузера "Обновить"</span><span class="sxs-lookup"><span data-stu-id="a9c7a-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="a9c7a-107">Просмотр панели мониторинга связи с браузером</span><span class="sxs-lookup"><span data-stu-id="a9c7a-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="a9c7a-108">Включение привязывание к браузеру для статического HTML-файлы</span><span class="sxs-lookup"><span data-stu-id="a9c7a-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="a9c7a-109">Отключение связь с браузером</span><span class="sxs-lookup"><span data-stu-id="a9c7a-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="a9c7a-110">Как это работает?</span><span class="sxs-lookup"><span data-stu-id="a9c7a-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="a9c7a-111">Браузера "Обновить"</span><span class="sxs-lookup"><span data-stu-id="a9c7a-111">Browser Refresh</span></span>

<span data-ttu-id="a9c7a-112">С помощью обновления в браузере вы можете обновить несколько браузеров, которые подключены к Visual Studio с помощью привязывания к браузеру.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="a9c7a-113">Чтобы использовать обновления в браузере, необходимо сначала создайте приложение ASP.NET, с помощью любого из шаблонов проектов.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="a9c7a-114">Отладка приложения, нажав клавишу F5 или выбрав значок со стрелкой на панели инструментов:</span><span class="sxs-lookup"><span data-stu-id="a9c7a-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="a9c7a-115">Можно также использовать раскрывающийся список для выбора конкретного браузера для отладки.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="a9c7a-116">Для отладки с помощью нескольких браузеров, установите **просмотр с помощью**.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="a9c7a-117">В **просмотр с помощью** диалоговое окно, удерживайте нажатой клавишу CTRL, чтобы выбрать более одного браузера.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="a9c7a-118">Нажмите кнопку **Обзор** для отладки с помощью выбранных браузерах.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="a9c7a-119">Связь с браузером также работает в том случае, если вы запустите браузер вне Visual Studio и перейдите к URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="a9c7a-120">Связь с браузером элементы управления находятся в раскрывающемся списке со значком круговой стрелки.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="a9c7a-121">Значок стрелки — **обновить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="a9c7a-122">Чтобы увидеть, какие браузеры подключены, наведите указатель мыши **обновить** кнопки во время отладки.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="a9c7a-123">Подключенные браузеры отображаются в окне всплывающей подсказки.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="a9c7a-124">Чтобы обновить подключенные браузеры, нажмите **обновить** кнопку или нажмите сочетание клавиш CTRL + ALT + ВВОД.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="a9c7a-125">Например на следующем рисунке показан проект ASP.NET, который я создал с помощью шаблона проекта MVC 5.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="a9c7a-126">Вы увидите приложения, работающего в двух браузеров в верхней.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="a9c7a-127">В нижней проект открыт в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="a9c7a-128">В Visual Studio, я изменил &lt;h1&gt; заголовок домашней страницы:</span><span class="sxs-lookup"><span data-stu-id="a9c7a-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="a9c7a-129">Когда я щелкнул **обновить** кнопки изменения были доступны в обоих окнах браузера:</span><span class="sxs-lookup"><span data-stu-id="a9c7a-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="a9c7a-130">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="a9c7a-130">**Notes**</span></span>

- <span data-ttu-id="a9c7a-131">Чтобы включить связь с браузером, задайте `debug=true` в [ &lt;компиляции&gt; ](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) в файле Web.config проекта.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="a9c7a-132">Приложение должно выполняться на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="a9c7a-133">Приложение должно использовать платформу .NET 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="a9c7a-134">Просмотр панели мониторинга связи с браузером</span><span class="sxs-lookup"><span data-stu-id="a9c7a-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="a9c7a-135">На панели мониторинга связи с браузером отображаются сведения о соединениях, связь с браузером.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="a9c7a-136">Для просмотра панели мониторинга, выберите в раскрывающемся меню привязывание к браузеру (маленькую стрелку рядом с полем **обновить** кнопки).</span><span class="sxs-lookup"><span data-stu-id="a9c7a-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="a9c7a-137">Нажмите кнопку **мониторинга связи с браузером**.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="a9c7a-138">Панели мониторинга перечислены подключенные браузеры и URL-адрес, к которому перешел каждым браузером.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="a9c7a-139">**Предварительные требования** разделе показаны все действия, необходимые для включить связь с браузером для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="a9c7a-140">Например на следующем рисунке показан проект где «debug» имеет значение false в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="a9c7a-141">Включение привязывание к браузеру для статического HTML-файлы</span><span class="sxs-lookup"><span data-stu-id="a9c7a-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="a9c7a-142">Чтобы включить связь с браузером для статических файлов HTML, добавьте следующее в файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="a9c7a-143">Для повышения производительности удалите этот параметр, при публикации проекта.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="a9c7a-144">Отключение связь с браузером</span><span class="sxs-lookup"><span data-stu-id="a9c7a-144">Disabling Browser Link</span></span>

<span data-ttu-id="a9c7a-145">Связь с браузером включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="a9c7a-146">Чтобы отключить его несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="a9c7a-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="a9c7a-147">В раскрывающемся меню связь с браузером, снимите флажок **включить связь с браузером**.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="a9c7a-148">В файле Web.config добавьте ключ с именем «vs: EnableBrowserLink» на значение «false» в разделе appSettings.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="a9c7a-149">В файле Web.config отладки установлен в значение false.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="a9c7a-150">Как это работает?</span><span class="sxs-lookup"><span data-stu-id="a9c7a-150">How Does It Work?</span></span>

<span data-ttu-id="a9c7a-151">Использует связи с браузером [SignalR](../../../signalr/index.md) для создания канала обмена данными между Visual Studio и браузером.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="a9c7a-152">При включении связь с браузером, Visual Studio выступает в качестве сервера SignalR, несколько клиентов (обозревателей) можно подключиться.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="a9c7a-153">Связь с браузером также регистрирует модуль HTTP ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="a9c7a-154">Этот модуль внедряет специальные &lt;скрипт&gt; ссылок в каждом запросе страницы с сервера.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="a9c7a-155">Вы увидите ссылки на скрипты, выбрав «Просмотр исходного кода» в браузере.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="a9c7a-156">Исходные файлы не изменяются.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-156">Your source files are not modified.</span></span> <span data-ttu-id="a9c7a-157">HTTP-модуль динамически внедряет ссылок на скрипты.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="a9c7a-158">Так как код на стороне обозревателя все JavaScript, он работает во всех браузерах, [SignalR поддерживает](../../../signalr/overview/getting-started/supported-platforms.md), не требуя любой подключаемый модуль обозревателя.</span><span class="sxs-lookup"><span data-stu-id="a9c7a-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
