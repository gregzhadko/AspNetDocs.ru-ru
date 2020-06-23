---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: Учебник. самостоятельный узел SignalR | Документация Майкрософт
author: bradygaster
description: В этом руководстве показано, как создать саморазмещенный сервер SignalR 2 и как подключиться к нему с помощью клиента JavaScript. Версии программного обеспечения, используемые в руководстве V...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 7470e0d6b68772ccfd979c834b7db81fbba3ca78
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240621"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="f2917-104">Учебник. Резидентное размещение SignalR</span><span class="sxs-lookup"><span data-stu-id="f2917-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="f2917-105">по [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="f2917-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f2917-106">В этом руководстве показано, как создать саморазмещенный сервер SignalR 2 и как подключиться к нему с помощью клиента JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f2917-106">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f2917-107">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="f2917-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="f2917-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f2917-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="f2917-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f2917-109">.NET 4.5</span></span>
> - <span data-ttu-id="f2917-110">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="f2917-110">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="f2917-111">Использование Visual Studio 2012 с этим руководством</span><span class="sxs-lookup"><span data-stu-id="f2917-111">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="f2917-112">Чтобы использовать Visual Studio 2012 с этим руководством, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f2917-112">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="f2917-113">Обновите [Диспетчер пакетов](http://docs.nuget.org/docs/start-here/installing-nuget) до последней версии.</span><span class="sxs-lookup"><span data-stu-id="f2917-113">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="f2917-114">Установите [установщик веб-платформы](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2917-114">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="f2917-115">В установщике веб-платформы найдите и установите **ASP.NET and Web Tools 2013,1 для Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="f2917-115">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="f2917-116">При этом будут установлены шаблоны Visual Studio для классов SignalR, таких как **Hub**.</span><span class="sxs-lookup"><span data-stu-id="f2917-116">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="f2917-117">Некоторые шаблоны (например, **класс запуска OWIN**) будут недоступны. Вместо этого используйте файл класса.</span><span class="sxs-lookup"><span data-stu-id="f2917-117">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="f2917-118">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="f2917-118">Questions and comments</span></span>
>
> <span data-ttu-id="f2917-119">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f2917-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="f2917-120">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="f2917-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="f2917-121">Обзор</span><span class="sxs-lookup"><span data-stu-id="f2917-121">Overview</span></span>

<span data-ttu-id="f2917-122">Сервер SignalR обычно размещается в приложении ASP.NET в службах IIS, но его также можно размещать в собственном расположении (например, в консольном приложении или службе Windows) с помощью библиотеки самообслуживания.</span><span class="sxs-lookup"><span data-stu-id="f2917-122">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="f2917-123">Эта библиотека, как и весь SignalR 2, построена на OWIN ([открытый веб-интерфейс для .NET](http://owin.org)).</span><span class="sxs-lookup"><span data-stu-id="f2917-123">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="f2917-124">OWIN определяет абстракцию между веб-серверами и веб-приложениями .NET.</span><span class="sxs-lookup"><span data-stu-id="f2917-124">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="f2917-125">OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS.</span><span class="sxs-lookup"><span data-stu-id="f2917-125">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="f2917-126">Причины отсутствия размещения в IIS включают:</span><span class="sxs-lookup"><span data-stu-id="f2917-126">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="f2917-127">Среды, в которых IIS недоступен или нежелательно, например Существующая ферма серверов без служб IIS.</span><span class="sxs-lookup"><span data-stu-id="f2917-127">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="f2917-128">Необходимо избегать издержек на производительность служб IIS.</span><span class="sxs-lookup"><span data-stu-id="f2917-128">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="f2917-129">Функции SignalR необходимо добавить в существующее приложение, которое выполняется в службе Windows, рабочей роли Azure или другом процессе.</span><span class="sxs-lookup"><span data-stu-id="f2917-129">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="f2917-130">Если решение разрабатывается как самообслуживающее по соображениям производительности, рекомендуется также протестировать приложение, размещенное в службах IIS, чтобы определить преимущество в производительности.</span><span class="sxs-lookup"><span data-stu-id="f2917-130">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="f2917-131">Этот учебник содержит следующие подразделы:</span><span class="sxs-lookup"><span data-stu-id="f2917-131">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="f2917-132">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="f2917-132">Creating the server</span></span>](#server)
- [<span data-ttu-id="f2917-133">Доступ к серверу с помощью клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="f2917-133">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="f2917-134">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="f2917-134">Creating the server</span></span>

<span data-ttu-id="f2917-135">В этом руководстве вы создадите сервер, размещенный в консольном приложении, но сервер может размещаться в любом процессе, например в службе Windows или рабочей роли Azure.</span><span class="sxs-lookup"><span data-stu-id="f2917-135">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="f2917-136">Пример кода для размещения сервера SignalR в службе Windows см. [в разделе самостоятельное размещение SignalR в службе Windows](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span><span class="sxs-lookup"><span data-stu-id="f2917-136">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="f2917-137">Откройте Visual Studio 2013 с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="f2917-137">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="f2917-138">Выберите **файл**, **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="f2917-138">Select **File**, **New Project**.</span></span> <span data-ttu-id="f2917-139">Выберите **Windows** в узле **Visual C#** в области **шаблоны** и выберите шаблон **консольное приложение** .</span><span class="sxs-lookup"><span data-stu-id="f2917-139">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="f2917-140">Назовите новый проект "Сигналрселфхост" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f2917-140">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="f2917-141">Откройте консоль диспетчера пакетов NuGet, выбрав **инструменты**  >  **Диспетчер пакетов NuGet**  >  **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="f2917-141">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="f2917-142">В консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2917-142">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="f2917-143">Эта команда добавляет в проект библиотеки саморазмещения SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="f2917-143">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="f2917-144">В консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2917-144">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="f2917-145">Эта команда добавляет библиотеку Microsoft. Owin. CORS в проект.</span><span class="sxs-lookup"><span data-stu-id="f2917-145">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="f2917-146">Эта библиотека будет использоваться для междоменной поддержки, которая необходима для приложений, которые размещают SignalR и клиент веб-страниц в разных доменах.</span><span class="sxs-lookup"><span data-stu-id="f2917-146">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="f2917-147">Поскольку сервер SignalR и веб-клиент будут размещаться на разных портах, это означает, что для взаимодействия между этими компонентами должно быть включено междоменное взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="f2917-147">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="f2917-148">Замените содержимое файла Program.cs на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="f2917-148">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="f2917-149">Приведенный выше код включает три класса:</span><span class="sxs-lookup"><span data-stu-id="f2917-149">The above code includes three classes:</span></span>

    - <span data-ttu-id="f2917-150">**Программа**, включая метод **Main** , определяющий основной путь выполнения.</span><span class="sxs-lookup"><span data-stu-id="f2917-150">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="f2917-151">В этом методе веб-приложение типа **Startup** запускается по указанному URL-адресу ( `http://localhost:8080` ).</span><span class="sxs-lookup"><span data-stu-id="f2917-151">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="f2917-152">Если для конечной точки требуется обеспечение безопасности, можно реализовать протокол SSL.</span><span class="sxs-lookup"><span data-stu-id="f2917-152">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="f2917-153">Дополнительные сведения см. [в разделе как настроить порт с помощью SSL-сертификата](https://msdn.microsoft.com/library/ms733791.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f2917-153">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="f2917-154">**Startup**, класс, содержащий конфигурацию сервера SignalR (единственной конфигурацией, используемой в этом руководстве, является вызов `UseCors` ) и вызов метода `MapSignalR` , который создает маршруты для всех объектов-концентраторов в проекте.</span><span class="sxs-lookup"><span data-stu-id="f2917-154">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="f2917-155">**Михуб**, класс концентратора SignalR, который приложение будет предоставлять клиентам.</span><span class="sxs-lookup"><span data-stu-id="f2917-155">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="f2917-156">Этот класс содержит один метод **Send**, который клиенты будут вызывать для передачи сообщения на все остальные подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="f2917-156">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="f2917-157">Скомпилируйте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="f2917-157">Compile and run the application.</span></span> <span data-ttu-id="f2917-158">Адрес, который работает на сервере, должен отображаться в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="f2917-158">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="f2917-159">В случае сбоя выполнения с исключением необходимо `System.Reflection.TargetInvocationException was unhandled` перезапустить Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="f2917-159">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="f2917-160">Перед переходом к следующему разделу закройте приложение.</span><span class="sxs-lookup"><span data-stu-id="f2917-160">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="f2917-161">Доступ к серверу с помощью клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="f2917-161">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="f2917-162">В этом разделе вы будете использовать тот же клиент JavaScript из [учебника по начало работы](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="f2917-162">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="f2917-163">В клиенте будет внесено только одно изменение, которое заключается в явном определении URL-адреса концентратора.</span><span class="sxs-lookup"><span data-stu-id="f2917-163">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="f2917-164">При использовании автономного приложения сервер может не быть на том же адресе, что и URL-адрес соединения (из-за обратных посредников и подсистем балансировки нагрузки), поэтому URL-адрес необходимо определить явным образом.</span><span class="sxs-lookup"><span data-stu-id="f2917-164">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="f2917-165">В **Обозреватель решений**щелкните решение правой кнопкой мыши и выберите **Добавить**, **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="f2917-165">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="f2917-166">Выберите **веб-** узел и выберите шаблон **веб-приложение ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="f2917-166">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="f2917-167">Присвойте проекту имя "Жаваскриптклиент" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f2917-167">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="f2917-168">Выберите **пустой** шаблон и оставьте невыбранными оставшиеся параметры.</span><span class="sxs-lookup"><span data-stu-id="f2917-168">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="f2917-169">Выберите **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="f2917-169">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="f2917-170">В консоли диспетчера пакетов выберите проект Жаваскриптклиент в раскрывающемся списке **проект по умолчанию** и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2917-170">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="f2917-171">Эта команда устанавливает библиотеки SignalR и JQuery, которые понадобятся в клиенте.</span><span class="sxs-lookup"><span data-stu-id="f2917-171">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="f2917-172">Щелкните проект правой кнопкой мыши и выберите **Добавить**, **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="f2917-172">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="f2917-173">Выберите **веб-** узел и выберите HTML-страница.</span><span class="sxs-lookup"><span data-stu-id="f2917-173">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="f2917-174">Присвойте странице имя **Default.html**.</span><span class="sxs-lookup"><span data-stu-id="f2917-174">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="f2917-175">Замените содержимое новой HTML-страницы следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="f2917-175">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="f2917-176">Убедитесь, что ссылки на скрипты соответствуют скриптам в папке Scripts проекта.</span><span class="sxs-lookup"><span data-stu-id="f2917-176">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="f2917-177">Следующий код (выделенный в приведенном выше примере кода) — это дополнение, которое вы внесли в клиент, который использовался в учебнике Приступая к работе (в дополнение к обновлению кода до бета-версии 2 SignalR).</span><span class="sxs-lookup"><span data-stu-id="f2917-177">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="f2917-178">Эта строка кода явным образом задает базовый URL-адрес соединения для SignalR на сервере.</span><span class="sxs-lookup"><span data-stu-id="f2917-178">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="f2917-179">Щелкните решение правой кнопкой мыши и выберите команду **задать запускаемые проекты...**. Выберите переключатель **Несколько запускаемых проектов** и задайте для параметра **действие** оба проекта значение **запустить**.</span><span class="sxs-lookup"><span data-stu-id="f2917-179">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="f2917-180">Щелкните правой кнопкой мыши "Default.html" и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="f2917-180">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="f2917-181">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="f2917-181">Run the application.</span></span> <span data-ttu-id="f2917-182">Сервер и страница будут запущены.</span><span class="sxs-lookup"><span data-stu-id="f2917-182">The server and page will launch.</span></span> <span data-ttu-id="f2917-183">Может потребоваться перезагрузить веб-страницу (или выбрать **продолжить** в отладчике), если страница загружается до запуска сервера.</span><span class="sxs-lookup"><span data-stu-id="f2917-183">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="f2917-184">В браузере при появлении запроса укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2917-184">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="f2917-185">Скопируйте URL-адрес страницы на другую вкладку или окно браузера и укажите другое имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2917-185">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="f2917-186">Вы сможете отправить сообщения с одной панели браузера на другую, как описано в начало работы руководстве.</span><span class="sxs-lookup"><span data-stu-id="f2917-186">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
