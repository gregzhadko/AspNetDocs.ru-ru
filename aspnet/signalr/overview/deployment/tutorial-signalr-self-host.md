---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: Учебник. Резидентное размещение SignalR | Документация Майкрософт
author: bradygaster
description: Этом руководстве показано, как создать локальную среду сервера SignalR 2 и способ подключения к нему с помощью клиента JavaScript. Версии программного обеспечения, используемые в этом руководстве V...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: c3fe4a08a30aa2ed116dfa36ce6206dc9cbd07f8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415080"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="14b5d-104">Учебник. Резидентное размещение SignalR</span><span class="sxs-lookup"><span data-stu-id="14b5d-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="14b5d-105">по [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="14b5d-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="14b5d-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="14b5d-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="14b5d-107">Этом руководстве показано, как создать локальную среду сервера SignalR 2 и способ подключения к нему с помощью клиента JavaScript.</span><span class="sxs-lookup"><span data-stu-id="14b5d-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="14b5d-108">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="14b5d-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="14b5d-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="14b5d-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="14b5d-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="14b5d-110">.NET 4.5</span></span>
> - <span data-ttu-id="14b5d-111">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="14b5d-111">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="14b5d-112">С помощью Visual Studio 2012 с помощью этого руководства</span><span class="sxs-lookup"><span data-stu-id="14b5d-112">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="14b5d-113">Чтобы использовать Visual Studio 2012 с этим руководством, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="14b5d-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="14b5d-114">Обновление вашей [диспетчера пакетов](http://docs.nuget.org/docs/start-here/installing-nuget) до последней версии.</span><span class="sxs-lookup"><span data-stu-id="14b5d-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="14b5d-115">Установка [установщик веб-платформы](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="14b5d-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="14b5d-116">В установщик веб-платформы, найдите и установите **ASP.NET и Web Tools 2013.1 для Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="14b5d-117">Это будет установки Visual Studio шаблоны для SignalR классов, таких как **центр**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="14b5d-118">Некоторые шаблоны (такие как **класс запуска OWIN**) будут недоступны; для этого используйте файл класса.</span><span class="sxs-lookup"><span data-stu-id="14b5d-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="14b5d-119">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="14b5d-119">Questions and comments</span></span>
>
> <span data-ttu-id="14b5d-120">Оставьте свои отзывы на том, как вам понравилось, и этот учебник и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="14b5d-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="14b5d-121">Если у вас есть вопросы, которые не имеют отношения к руководству, их можно разместить [форум по ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="14b5d-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="14b5d-122">Обзор</span><span class="sxs-lookup"><span data-stu-id="14b5d-122">Overview</span></span>

<span data-ttu-id="14b5d-123">SignalR сервера обычно размещается в приложении ASP.NET в IIS, но это также может быть резидентной (например, консольное приложение или служба Windows) с помощью библиотеки резидентного размещения.</span><span class="sxs-lookup"><span data-stu-id="14b5d-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="14b5d-124">Эта библиотека, подобно всем SignalR 2, лежит OWIN ([Open Web Interface for .NET](http://owin.org)).</span><span class="sxs-lookup"><span data-stu-id="14b5d-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="14b5d-125">OWIN определяет абстракции между веб-серверов .NET и веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="14b5d-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="14b5d-126">OWIN отделяет веб-приложения на сервер, который идеально OWIN для резидентного размещения веб-приложения в собственном процессе, за пределами служб IIS.</span><span class="sxs-lookup"><span data-stu-id="14b5d-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="14b5d-127">Причины не размещено в службах IIS:</span><span class="sxs-lookup"><span data-stu-id="14b5d-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="14b5d-128">Средах, где IIS не доступны или желательно, например существующую ферму серверов без служб IIS.</span><span class="sxs-lookup"><span data-stu-id="14b5d-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="14b5d-129">Необходимо избежать потери производительности в IIS.</span><span class="sxs-lookup"><span data-stu-id="14b5d-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="14b5d-130">Функциональные возможности SignalR — добавить в существующее приложение, в котором выполняется служба Windows, рабочей роли Azure или другой процесс.</span><span class="sxs-lookup"><span data-stu-id="14b5d-130">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="14b5d-131">Если это решение разработано как резидентного размещения для повышения производительности, рекомендуется также тестового приложения, размещенного в службах IIS, для определения преимуществ.</span><span class="sxs-lookup"><span data-stu-id="14b5d-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="14b5d-132">Этот учебник содержит следующие разделы:</span><span class="sxs-lookup"><span data-stu-id="14b5d-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="14b5d-133">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="14b5d-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="14b5d-134">Доступ к серверу с помощью клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="14b5d-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="14b5d-135">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="14b5d-135">Creating the server</span></span>

<span data-ttu-id="14b5d-136">В этом руководстве вы создадите сервер, который размещается в консольном приложении, но сервер может размещаться в любой из процесса, например службы Windows или рабочей роли Azure.</span><span class="sxs-lookup"><span data-stu-id="14b5d-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="14b5d-137">Пример кода для размещения сервера SignalR в службе Windows, см. в разделе [Self-Hosting SignalR в службе Windows](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span><span class="sxs-lookup"><span data-stu-id="14b5d-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="14b5d-138">Откройте Visual Studio 2013 с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="14b5d-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="14b5d-139">Выберите **файл**, **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="14b5d-140">Выберите **Windows** под **Visual C#** узел в **шаблоны** области и выберите **консольное приложение** шаблона.</span><span class="sxs-lookup"><span data-stu-id="14b5d-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="14b5d-141">Назовите новый проект «SignalRSelfHost» и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="14b5d-142">Откройте консоль диспетчера пакетов NuGet, выбрав **средства** > **диспетчер пакетов NuGet** > **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-142">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="14b5d-143">В консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="14b5d-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="14b5d-144">Эта команда добавляет в проект библиотеки SignalR 2 Self-Host.</span><span class="sxs-lookup"><span data-stu-id="14b5d-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="14b5d-145">В консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="14b5d-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="14b5d-146">Эта команда добавляет Microsoft.Owin.Cors библиотеки в проект.</span><span class="sxs-lookup"><span data-stu-id="14b5d-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="14b5d-147">Эта библиотека будет использоваться для поддержки между доменами, который необходим для приложения, размещающие SignalR и веб-страницы клиента, в разных доменах.</span><span class="sxs-lookup"><span data-stu-id="14b5d-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="14b5d-148">Так как будет размещаться сервер SignalR и веб-клиента на разных портах, это означает, что кросс доменные должна быть включена для обмена данными между этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="14b5d-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="14b5d-149">Замените содержимое Program.cs кодом из этого примера.</span><span class="sxs-lookup"><span data-stu-id="14b5d-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="14b5d-150">Приведенный выше код включает в себя три класса:</span><span class="sxs-lookup"><span data-stu-id="14b5d-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="14b5d-151">**Программа**, в том числе **Main** метод, определение первичного пути выполнения.</span><span class="sxs-lookup"><span data-stu-id="14b5d-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="14b5d-152">В этом методе веб-приложение типа **запуска** запускается на указанный URL-адрес (`http://localhost:8080`).</span><span class="sxs-lookup"><span data-stu-id="14b5d-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="14b5d-153">Если для конечной точки требуется безопасности, можно реализовать SSL.</span><span class="sxs-lookup"><span data-stu-id="14b5d-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="14b5d-154">См. практическое руководство по [ Настройка порта SSL-сертификат](https://msdn.microsoft.com/library/ms733791.aspx) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="14b5d-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="14b5d-155">**Запуска**, класс, содержащий конфигурацию сервера SignalR (в этом руководстве используется единственная конфигурация, это вызов `UseCors`) и вызов `MapSignalR`, который создает маршруты для любых объектов концентратора в проекте.</span><span class="sxs-lookup"><span data-stu-id="14b5d-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="14b5d-156">**MyHub**, класс концентратора SignalR, приложение будет предоставлять клиентам.</span><span class="sxs-lookup"><span data-stu-id="14b5d-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="14b5d-157">Этот класс содержит один метод, **отправки**, что клиенты будут вызывать для передачи сообщения для всех других подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="14b5d-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="14b5d-158">Скомпилируйте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="14b5d-158">Compile and run the application.</span></span> <span data-ttu-id="14b5d-159">Адрес, на котором выполняется сервер должно отображаться в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="14b5d-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="14b5d-160">Если происходит сбой выполнения с исключением `System.Reflection.TargetInvocationException was unhandled`, вам потребуется перезапустить Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="14b5d-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="14b5d-161">Остановите приложение, прежде чем переходить к следующему разделу.</span><span class="sxs-lookup"><span data-stu-id="14b5d-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="14b5d-162">Доступ к серверу с помощью клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="14b5d-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="14b5d-163">В этом разделе вы используете того же клиента JavaScript из [учебнике Приступая к работе](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="14b5d-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="14b5d-164">Сделаем только одно изменение в клиенте, что необходимо явно определить URL-адрес концентратора.</span><span class="sxs-lookup"><span data-stu-id="14b5d-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="14b5d-165">С помощью резидентного приложения сервер может не обязательно будет по тому же адресу, как URL-адрес подключения (из-за обратных прокси-серверов и подсистемы балансировки нагрузки), поэтому URL-адреса должна быть определена явно.</span><span class="sxs-lookup"><span data-stu-id="14b5d-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="14b5d-166">В **обозревателе решений**, щелкните правой кнопкой мыши решение и выберите **добавить**, **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="14b5d-167">Выберите **Web** узел и выберите **веб-приложение ASP.NET** шаблона.</span><span class="sxs-lookup"><span data-stu-id="14b5d-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="14b5d-168">Присвойте проекту имя «JavascriptClient» и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="14b5d-169">Выберите **пустой** шаблона и оставьте остальные параметры не выбран.</span><span class="sxs-lookup"><span data-stu-id="14b5d-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="14b5d-170">Выберите **Создание проекта**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="14b5d-171">В консоли диспетчера пакетов, выберите проект «JavascriptClient» в **проект по умолчанию** раскрывающегося списка и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="14b5d-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="14b5d-172">Эта команда устанавливает библиотеки SignalR и JQuery, которые вам потребуются в клиенте.</span><span class="sxs-lookup"><span data-stu-id="14b5d-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="14b5d-173">Щелкните правой кнопкой мыши проект и выберите **добавить**, **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="14b5d-174">Выберите **Web** узел и выберите HTML-страницу.</span><span class="sxs-lookup"><span data-stu-id="14b5d-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="14b5d-175">Присвойте странице имя **Default.html**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="14b5d-176">Замените содержимое новую HTML-страницу следующий код.</span><span class="sxs-lookup"><span data-stu-id="14b5d-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="14b5d-177">Убедитесь, что здесь ссылки на скрипты соответствуют скрипты в папке Scripts проекта.</span><span class="sxs-lookup"><span data-stu-id="14b5d-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="14b5d-178">Приведенный ниже (выделены в приведенном выше примере) является добавление, внесенные в клиенте, используемом в этом руководстве начало Stared (в дополнение к обновление кода до бета-версия 2 SignalR).</span><span class="sxs-lookup"><span data-stu-id="14b5d-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="14b5d-179">Эта строка кода явным образом задает URL-адрес базового подключения для SignalR на сервере.</span><span class="sxs-lookup"><span data-stu-id="14b5d-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="14b5d-180">Щелкните правой кнопкой мыши решение и выберите **назначить запускаемые проекты...** . Выберите **несколько запускаемых проектов** кнопку-переключатель и задайте обоим проектам **действие** для **запустить**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="14b5d-181">Щелкните правой кнопкой мыши на «Default.html» и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="14b5d-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="14b5d-182">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="14b5d-182">Run the application.</span></span> <span data-ttu-id="14b5d-183">Сервер и страницы приведет к запуску.</span><span class="sxs-lookup"><span data-stu-id="14b5d-183">The server and page will launch.</span></span> <span data-ttu-id="14b5d-184">Может потребоваться перезагрузить веб-страницы (или выберите **Продолжить** в отладчике) при загрузке страницы, до запуска сервера.</span><span class="sxs-lookup"><span data-stu-id="14b5d-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="14b5d-185">В браузере введите имя пользователя при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="14b5d-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="14b5d-186">Скопируйте URL-адрес страницы в другой вкладке браузера или в окне и укажите другое имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="14b5d-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="14b5d-187">Можно отправлять сообщения из одной области в другую, как в этом руководстве Приступая к работе.</span><span class="sxs-lookup"><span data-stu-id="14b5d-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
