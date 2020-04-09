---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Учебник: Сервер вещания с SignalR 2 Документы Майкрософт'
author: tdykstra
description: В этом учебнике показано, как создать веб-приложение, которое использует ASP.NET SignalR 2 для обеспечения функциональности вещания сервера.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675727"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="e8444-103">Учебник: Сервер вещания с SignalR 2</span><span class="sxs-lookup"><span data-stu-id="e8444-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="e8444-104">В этом учебнике показано, как создать веб-приложение, которое использует ASP.NET SignalR 2 для обеспечения функциональности вещания сервера.</span><span class="sxs-lookup"><span data-stu-id="e8444-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="e8444-105">Трансляция сервера означает, что сервер запускает сообщения, отправленные клиентам.</span><span class="sxs-lookup"><span data-stu-id="e8444-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="e8444-106">Приложение, которое вы создадите в этом учебнике, имитирует биржевый тикер, типичный сценарий для функциональности вещания сервера.</span><span class="sxs-lookup"><span data-stu-id="e8444-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="e8444-107">Периодически сервер случайным образом обновляет цены на акции и транслирует обновления всем подключенным клиентам.</span><span class="sxs-lookup"><span data-stu-id="e8444-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="e8444-108">В браузере числа и символы **%** в **изменении** и столбцах динамически меняются в ответ на уведомления с сервера.</span><span class="sxs-lookup"><span data-stu-id="e8444-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="e8444-109">Если вы откроете дополнительные браузеры по тому же URL-, все они отображают одни и те же данные и одинаковые изменения в данных.</span><span class="sxs-lookup"><span data-stu-id="e8444-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Создание веб-страниц](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="e8444-111">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="e8444-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8444-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="e8444-112">Create the project</span></span>
> * <span data-ttu-id="e8444-113">Настройка кода сервера</span><span class="sxs-lookup"><span data-stu-id="e8444-113">Set up the server code</span></span>
> * <span data-ttu-id="e8444-114">Изучить код сервера</span><span class="sxs-lookup"><span data-stu-id="e8444-114">Examine the server code</span></span>
> * <span data-ttu-id="e8444-115">Настройка кода клиента</span><span class="sxs-lookup"><span data-stu-id="e8444-115">Set up the client code</span></span>
> * <span data-ttu-id="e8444-116">Изучить код клиента</span><span class="sxs-lookup"><span data-stu-id="e8444-116">Examine the client code</span></span>
> * <span data-ttu-id="e8444-117">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="e8444-117">Test the application</span></span>
> * <span data-ttu-id="e8444-118">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="e8444-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8444-119">Если вы не хотите работать над этапами создания приложения, вы можете установить пакет SignalR.Sample в новый проект Пустого ASP.NET Web Application.</span><span class="sxs-lookup"><span data-stu-id="e8444-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="e8444-120">Если вы установите пакет NuGet, не выполняя шагов в этом учебнике, вы должны следовать инструкциям в файле *readme.txt.*</span><span class="sxs-lookup"><span data-stu-id="e8444-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="e8444-121">Для запуска пакета необходимо добавить класс запуска OWIN, который вызывает `ConfigureSignalR` метод в установленном пакете.</span><span class="sxs-lookup"><span data-stu-id="e8444-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="e8444-122">Вы получите ошибку, если не добавите класс запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="e8444-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="e8444-123">Смотрите раздел [«Установка образца StockTicker»](#install-the-stockticker-sample) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e8444-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8444-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e8444-124">Prerequisites</span></span>

* <span data-ttu-id="e8444-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с рабочей нагрузкой **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="e8444-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="e8444-126">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="e8444-126">Create the project</span></span>

<span data-ttu-id="e8444-127">В этом разделе показано, как использовать Visual Studio 2017 для создания пустого веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e8444-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="e8444-128">В Visual Studio создайте веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e8444-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Создание веб-страниц](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="e8444-130">В **Новом ASP.NET веб-приложении - SignalR.StockTicker** окно, оставьте **Пустые** выбранные и выбрать **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8444-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="e8444-131">Настройка кода сервера</span><span class="sxs-lookup"><span data-stu-id="e8444-131">Set up the server code</span></span>

<span data-ttu-id="e8444-132">В этом разделе вы настраиваете код, который работает на сервере.</span><span class="sxs-lookup"><span data-stu-id="e8444-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="e8444-133">Создание класса stock</span><span class="sxs-lookup"><span data-stu-id="e8444-133">Create the Stock class</span></span>

<span data-ttu-id="e8444-134">Вы начинаете с создания класса *модели Stock,* который вы будете использовать для хранения и передачи информации о запасе.</span><span class="sxs-lookup"><span data-stu-id="e8444-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="e8444-135">В **Solution Explorer**, правой кнопкой мыши проекта и выберите **Добавить** > **класс**.</span><span class="sxs-lookup"><span data-stu-id="e8444-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="e8444-136">Назовите класс *Stock* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="e8444-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="e8444-137">Замените код в *файле Stock.cs* этим кодом:</span><span class="sxs-lookup"><span data-stu-id="e8444-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="e8444-138">Два свойства, которые вы установите при `Symbol` создании запасов (например, `Price`MSFT для Microsoft) и .</span><span class="sxs-lookup"><span data-stu-id="e8444-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="e8444-139">Другие свойства зависят от `Price`того, как и когда вы установите .</span><span class="sxs-lookup"><span data-stu-id="e8444-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="e8444-140">При первом установке `Price`значение распространяется на. `DayOpen`</span><span class="sxs-lookup"><span data-stu-id="e8444-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="e8444-141">После этого, когда `Price`вы устанавливаете, `Change` `PercentChange` приложение вычисляет значения `Price` `DayOpen`и свойства на основе разницы между и .</span><span class="sxs-lookup"><span data-stu-id="e8444-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="e8444-142">Создание классов StockTickerHub и StockTicker</span><span class="sxs-lookup"><span data-stu-id="e8444-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="e8444-143">Для обработки взаимодействия от сервера с клиентом вы будете использовать API концентратора SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="e8444-144">Класс, `StockTickerHub` который вытекает из `Hub` класса SignalR, будет обрабатывать прием подключений и методов вызовов от клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="e8444-145">Также необходимо поддерживать данные о `Timer` запасах и запускать объект.</span><span class="sxs-lookup"><span data-stu-id="e8444-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="e8444-146">Объект `Timer` будет периодически запускать обновления цен независимо от клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="e8444-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="e8444-147">Вы не можете поместить эти `Hub` функции в класс, потому что концентраторы являются переходными.</span><span class="sxs-lookup"><span data-stu-id="e8444-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="e8444-148">Приложение создает `Hub` экземпляр класса для каждой задачи в концентраторе, например, соединения и звонки от клиента к серверу.</span><span class="sxs-lookup"><span data-stu-id="e8444-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="e8444-149">Таким образом, механизм, который хранит данные о запасах, обновляет цены и транслирует обновления цен, должен работать в отдельном классе.</span><span class="sxs-lookup"><span data-stu-id="e8444-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="e8444-150">Вы назовете класс. `StockTicker`</span><span class="sxs-lookup"><span data-stu-id="e8444-150">You'll name the class `StockTicker`.</span></span>

![Вещание от StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="e8444-152">Требуется только один `StockTicker` экземпляр класса для запуска на сервере, поэтому вам нужно `StockTickerHub` настроить ссылку `StockTicker` из каждого экземпляра на экземпляр синглтона.</span><span class="sxs-lookup"><span data-stu-id="e8444-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="e8444-153">Класс `StockTicker` должен транслироваться клиентам, потому что он имеет `StockTicker` данные о `Hub` запасах и вызывает обновления, но не является классом.</span><span class="sxs-lookup"><span data-stu-id="e8444-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="e8444-154">Класс `StockTicker` должен получить ссылку на контекстный объект соединения SignalR Hub.</span><span class="sxs-lookup"><span data-stu-id="e8444-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="e8444-155">Затем он может использовать контекстный объект соединения SignalR для трансляции для клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="e8444-156">Создание StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="e8444-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="e8444-157">В **Solution Explorer**, правой кнопкой мыши проекта и выберите **Добавить** > **новый пункт**.</span><span class="sxs-lookup"><span data-stu-id="e8444-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="e8444-158">В **Добавить новый пункт - SignalR.StockTicker**, выберите **Установленный** > **визуальный C'** > **Web** > **SignalR,** а затем выберите **SignalR концентратор класса (v2)**.</span><span class="sxs-lookup"><span data-stu-id="e8444-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="e8444-159">Назовите класс *StockTickerHub* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="e8444-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="e8444-160">Этот шаг создает файл *StockTickerHub.cs* класса.</span><span class="sxs-lookup"><span data-stu-id="e8444-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="e8444-161">Одновременно он добавляет набор файлов скриптов и ссылок на сборку, которые поддерживают SignalR в проект.</span><span class="sxs-lookup"><span data-stu-id="e8444-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="e8444-162">Замените код в *файле StockTickerHub.cs* этим кодом:</span><span class="sxs-lookup"><span data-stu-id="e8444-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="e8444-163">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="e8444-163">Save the file.</span></span>

<span data-ttu-id="e8444-164">Приложение использует класс [концентратора](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) для определения методов, которые клиенты могут вызвать на сервере.</span><span class="sxs-lookup"><span data-stu-id="e8444-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="e8444-165">Вы определяете один `GetAllStocks()`метод: .</span><span class="sxs-lookup"><span data-stu-id="e8444-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="e8444-166">Когда клиент первоначально подключается к серверу, он будет называть этот метод, чтобы получить список всех акций с их текущими ценами.</span><span class="sxs-lookup"><span data-stu-id="e8444-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="e8444-167">Метод может работать синхронно `IEnumerable<Stock>` и возвращаться, поскольку он возвращает данные из памяти.</span><span class="sxs-lookup"><span data-stu-id="e8444-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="e8444-168">Если метод должен был получить данные, делая что-то, что предполагает ожидание, например, поиск базы данных или вызов веб-службы, вы бы указали `Task<IEnumerable<Stock>>` в качестве значения возврата для обеспечения асинхронной обработки.</span><span class="sxs-lookup"><span data-stu-id="e8444-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="e8444-169">Для получения дополнительной информации, см [ASP.NET SignalR концентраторов API Руководство - Сервер - Когда выполнять асинхронно](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="e8444-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="e8444-170">Атрибут `HubName` определяет, как приложение будет ссылаться на код Концентратора javaScript на клиенте.</span><span class="sxs-lookup"><span data-stu-id="e8444-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="e8444-171">Имя клиента по умолчанию, если вы не используете этот атрибут, является верблюжьей `stockTickerHub`версией имени класса, которая в этом случае будет.</span><span class="sxs-lookup"><span data-stu-id="e8444-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="e8444-172">Как вы увидите позже `StockTicker` при создании класса, приложение создает единичный `Instance` экземпляр этого класса в своем статичном свойстве.</span><span class="sxs-lookup"><span data-stu-id="e8444-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="e8444-173">Этот однотонный `StockTicker` экземпляр находится в памяти независимо от того, сколько клиентов подключаются или отключаются.</span><span class="sxs-lookup"><span data-stu-id="e8444-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="e8444-174">Этот экземпляр является `GetAllStocks()` то, что метод использует для возвращения текущей информации о запасах.</span><span class="sxs-lookup"><span data-stu-id="e8444-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="e8444-175">Создание StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="e8444-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="e8444-176">В **Solution Explorer**, правой кнопкой мыши проекта и выберите **Добавить** > **класс**.</span><span class="sxs-lookup"><span data-stu-id="e8444-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="e8444-177">Назовите класс *StockTicker* и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="e8444-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="e8444-178">Замените код в *файле StockTicker.cs* этим кодом:</span><span class="sxs-lookup"><span data-stu-id="e8444-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="e8444-179">Поскольку все потоки будут работать в одном экземпляре кода StockTicker, класс StockTicker должен быть безопасным для потоков.</span><span class="sxs-lookup"><span data-stu-id="e8444-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="e8444-180">Изучить код сервера</span><span class="sxs-lookup"><span data-stu-id="e8444-180">Examine the server code</span></span>

<span data-ttu-id="e8444-181">Если вы изучите код сервера, это поможет вам понять, как работает приложение.</span><span class="sxs-lookup"><span data-stu-id="e8444-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="e8444-182">Хранение экземпляра синглтона в статичном поле</span><span class="sxs-lookup"><span data-stu-id="e8444-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="e8444-183">Код инициализирует `_instance` статическое поле, которое поддерживает `Instance` свойство экземпляром класса.</span><span class="sxs-lookup"><span data-stu-id="e8444-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="e8444-184">Поскольку конструктор является частным, это единственный экземпляр класса, который может создать приложение.</span><span class="sxs-lookup"><span data-stu-id="e8444-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="e8444-185">Приложение использует [Ленивый инициализации](/dotnet/framework/performance/lazy-initialization) `_instance` для поля.</span><span class="sxs-lookup"><span data-stu-id="e8444-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="e8444-186">Это не по причинам производительности.</span><span class="sxs-lookup"><span data-stu-id="e8444-186">It's not for performance reasons.</span></span> <span data-ttu-id="e8444-187">Это, чтобы убедиться, что создание экземпляра является безопасным для потоков.</span><span class="sxs-lookup"><span data-stu-id="e8444-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="e8444-188">Каждый раз, когда клиент подключается к серверу, новый экземпляр класса StockTickerHub, работающий `StockTicker.Instance` в отдельном потоке, `StockTickerHub` получает экземпляр StockTicker singleton из статического свойства, как вы видели ранее в классе.</span><span class="sxs-lookup"><span data-stu-id="e8444-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="e8444-189">Хранение данных о запасах в параллельном словаре</span><span class="sxs-lookup"><span data-stu-id="e8444-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="e8444-190">Конструктор инициализирует коллекцию `_stocks` с некоторыми выборочными данными о запасах и `GetAllStocks` возвращает запасы.</span><span class="sxs-lookup"><span data-stu-id="e8444-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="e8444-191">Как вы видели ранее, эта коллекция `StockTickerHub.GetAllStocks`акций возвращается, `Hub` который является методом сервера в классе, который клиенты могут позвонить.</span><span class="sxs-lookup"><span data-stu-id="e8444-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="e8444-192">Сбор запасов определяется как тип [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) для безопасности потоков.</span><span class="sxs-lookup"><span data-stu-id="e8444-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="e8444-193">В качестве альтернативы можно использовать объект [словаря](https://msdn.microsoft.com/library/xfhwa508.aspx) и явно заблокировать словарь при внесении изменений в него.</span><span class="sxs-lookup"><span data-stu-id="e8444-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="e8444-194">Для этого примера приложения можно хранить данные приложения в памяти и терять `StockTicker` данные, когда приложение избавляется от экземпляра.</span><span class="sxs-lookup"><span data-stu-id="e8444-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="e8444-195">В реальном приложении вы будете работать с запасом данных бэк-энда, как база данных.</span><span class="sxs-lookup"><span data-stu-id="e8444-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="e8444-196">Периодические обновления цен на акции</span><span class="sxs-lookup"><span data-stu-id="e8444-196">Periodically updating stock prices</span></span>

<span data-ttu-id="e8444-197">Конструктор запускает `Timer` объект, который периодически вызывает методы, которые обновляют цены на акции на случайной основе.</span><span class="sxs-lookup"><span data-stu-id="e8444-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="e8444-198">`Timer`вызовов, `UpdateStockPrices`который проходит в нулевых в параметре состояния.</span><span class="sxs-lookup"><span data-stu-id="e8444-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="e8444-199">Перед обновлением цен приложение запирает `_updateStockPricesLock` объект.</span><span class="sxs-lookup"><span data-stu-id="e8444-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="e8444-200">Код проверяет, обновляет ли другой поток цены, `TryUpdateStockPrice` а затем призывает каждую акцию в списке.</span><span class="sxs-lookup"><span data-stu-id="e8444-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="e8444-201">Метод `TryUpdateStockPrice` решает, следует ли изменить цену акций, и сколько изменить его.</span><span class="sxs-lookup"><span data-stu-id="e8444-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="e8444-202">Если цена акций меняется, приложение призывает `BroadcastStockPrice` транслировать изменение цены акций для всех подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="e8444-203">Флаг, `_updatingStockPrices` обозначенный [летучим,](https://msdn.microsoft.com/library/x13ttww7.aspx) чтобы убедиться, что он без покоя.</span><span class="sxs-lookup"><span data-stu-id="e8444-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="e8444-204">В реальном приложении `TryUpdateStockPrice` метод вызовет веб-службу, чтобы найти цену.</span><span class="sxs-lookup"><span data-stu-id="e8444-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="e8444-205">В этом коде приложение использует генератор случайных чисел для внесения изменений случайным образом.</span><span class="sxs-lookup"><span data-stu-id="e8444-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="e8444-206">Получение контекста SignalR, чтобы класс StockTicker мог транслировать сядовещание клиентам</span><span class="sxs-lookup"><span data-stu-id="e8444-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="e8444-207">Поскольку изменения цен происходят `StockTicker` здесь, в объекте, это `updateStockPrice` объект, который должен вызвать метод на всех подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="e8444-208">В `Hub` классе у вас есть API для вызова `StockTicker` методов клиента, `Hub` но он не вытекает `Hub` из класса и не имеет ссылки на какой-либо объект.</span><span class="sxs-lookup"><span data-stu-id="e8444-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="e8444-209">Для трансляции подключенным `StockTicker` клиентам класс должен получить экземпляр `StockTickerHub` контекста SignalR для класса и использовать его для вызова методов для клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="e8444-210">Код получает ссылку на контекст SignalR, когда он создает экземпляр класса синглтон, передает эту ссылку `Clients` на конструктор, и конструктор помещает его в свойство.</span><span class="sxs-lookup"><span data-stu-id="e8444-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="e8444-211">Существует две причины, по которым вы хотите получить контекст только один раз: получение контекста является дорогостоящей задачей, и получение его один раз гарантирует, что приложение сохраняет предполагаемый порядок сообщений, отправляемых клиентам.</span><span class="sxs-lookup"><span data-stu-id="e8444-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="e8444-212">Получение `Clients` свойства контекста и размещение `StockTickerClient` его в свойстве позволяет писать код для вызова клиентских `Hub` методов, который выглядит так же, как это было бы в классе.</span><span class="sxs-lookup"><span data-stu-id="e8444-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="e8444-213">Например, для трансляции для `Clients.All.updateStockPrice(stock)`всех клиентов вы можете написать .</span><span class="sxs-lookup"><span data-stu-id="e8444-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="e8444-214">`updateStockPrice` Метод, который вы вызываете, `BroadcastStockPrice` еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e8444-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="e8444-215">Вы добавите его позже, когда вы напишете код, который работает на клиенте.</span><span class="sxs-lookup"><span data-stu-id="e8444-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="e8444-216">Вы можете `updateStockPrice` сослаться `Clients.All` на здесь, потому что это динамическое, что означает, что приложение будет оценивать выражение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="e8444-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="e8444-217">Когда вызов этого метода выполняется, SignalR отправит клиенту имя метода и значение `updateStockPrice`параметра, и если у клиента есть метод под названием, приложение вызовет этот метод и передаст ему значение параметра.</span><span class="sxs-lookup"><span data-stu-id="e8444-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="e8444-218">`Clients.All`означает отправку всем клиентам.</span><span class="sxs-lookup"><span data-stu-id="e8444-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="e8444-219">SignalR дает вам другие варианты, чтобы указать, какие клиенты или группы клиентов, чтобы отправить.</span><span class="sxs-lookup"><span data-stu-id="e8444-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="e8444-220">Для получения дополнительной информации [см.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="e8444-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="e8444-221">Регистрация маршрута SignalR</span><span class="sxs-lookup"><span data-stu-id="e8444-221">Register the SignalR route</span></span>

<span data-ttu-id="e8444-222">Сервер должен знать, какой URL перехватить и направить на SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="e8444-223">Для этого добавьте класс стартапов OWIN:</span><span class="sxs-lookup"><span data-stu-id="e8444-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="e8444-224">В **Solution Explorer**, правой кнопкой мыши проекта и выберите **Добавить** > **новый пункт**.</span><span class="sxs-lookup"><span data-stu-id="e8444-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="e8444-225">В **Добавлении Новый пункт - SignalR.StockTicker** выберите **установленный** > **визуальный C'** > **Web,** а затем выберите класс запуска **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="e8444-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="e8444-226">Назовите класс *Startup* и выберите **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8444-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="e8444-227">Замените код по умолчанию в *файле Startup.cs* этим кодом:</span><span class="sxs-lookup"><span data-stu-id="e8444-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="e8444-228">Теперь вы закончили настройку серверного кода.</span><span class="sxs-lookup"><span data-stu-id="e8444-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="e8444-229">В следующем разделе вы настроили клиента.</span><span class="sxs-lookup"><span data-stu-id="e8444-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="e8444-230">Настройка кода клиента</span><span class="sxs-lookup"><span data-stu-id="e8444-230">Set up the client code</span></span>

<span data-ttu-id="e8444-231">В этом разделе вы настраиваете код, который работает на клиенте.</span><span class="sxs-lookup"><span data-stu-id="e8444-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="e8444-232">Создание html-страницы и файла JavaScript</span><span class="sxs-lookup"><span data-stu-id="e8444-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="e8444-233">Страница HTML будет отображать данные, а файл JavaScript организует данные.</span><span class="sxs-lookup"><span data-stu-id="e8444-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="e8444-234">Создание StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="e8444-234">Create StockTicker.html</span></span>

<span data-ttu-id="e8444-235">Во-первых, вы добавите HTML-клиент.</span><span class="sxs-lookup"><span data-stu-id="e8444-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="e8444-236">В **Solution Explorer**, правой кнопкой мыши проекта и выберите **Добавить** > **HTML Страницы**.</span><span class="sxs-lookup"><span data-stu-id="e8444-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="e8444-237">Назовите файл *StockTicker* и выберите **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8444-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="e8444-238">Замените код по умолчанию в файле *StockTicker.html* этим кодом:</span><span class="sxs-lookup"><span data-stu-id="e8444-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="e8444-239">HTML создает таблицу с пятью столбцов, строкой заголовка и строкой данных с одной ячейкой, которая охватывает все пять столбцов.</span><span class="sxs-lookup"><span data-stu-id="e8444-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="e8444-240">Строка данных показывает "загрузку..." на мгновение, когда приложение запускается.</span><span class="sxs-lookup"><span data-stu-id="e8444-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="e8444-241">Код JavaScript удалит эту строку и добавит в свое место строки с запасами данных, извлеченных с сервера.</span><span class="sxs-lookup"><span data-stu-id="e8444-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="e8444-242">Теги скрипта указывают:</span><span class="sxs-lookup"><span data-stu-id="e8444-242">The script tags specify:</span></span>

    * <span data-ttu-id="e8444-243">Файл скрипта j''s.</span><span class="sxs-lookup"><span data-stu-id="e8444-243">The jQuery script file.</span></span>

    * <span data-ttu-id="e8444-244">Файл ядра SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="e8444-245">Файл скриптов SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="e8444-246">Файл сценария StockTicker, который вы создадите позже.</span><span class="sxs-lookup"><span data-stu-id="e8444-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="e8444-247">Приложение динамически генерирует файл скриптов SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="e8444-248">Он определяет URL-адрес "/signalr/hubs" и определяет прокси-методы для методов на классе `StockTickerHub.GetAllStocks`концентратора, в данном случае для .</span><span class="sxs-lookup"><span data-stu-id="e8444-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="e8444-249">Если вы предпочитаете, вы можете создать этот файл JavaScript вручную с помощью [SignalR Утилиты](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span><span class="sxs-lookup"><span data-stu-id="e8444-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="e8444-250">Не забудьте отключить создание динамического файла в вызове метода. `MapHubs`</span><span class="sxs-lookup"><span data-stu-id="e8444-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="e8444-251">В **Solution Explorer**расширьте **скрипты.**</span><span class="sxs-lookup"><span data-stu-id="e8444-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="e8444-252">В проекте видны библиотеки сценариев для j''query и SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e8444-253">Менеджер пакетов установит более позднюю версию скриптов SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="e8444-254">Обновление ссылок на сценарий в блоке кода в соответствии с версиями файлов скрипта в проекте.</span><span class="sxs-lookup"><span data-stu-id="e8444-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="e8444-255">В **Solution Explorer**, правой кнопкой мыши *StockTicker.html*, а затем выберите **Установить в качестве стартовой страницы**.</span><span class="sxs-lookup"><span data-stu-id="e8444-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="e8444-256">Создание StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="e8444-256">Create StockTicker.js</span></span>

<span data-ttu-id="e8444-257">Теперь создайте файл JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e8444-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="e8444-258">В **Solution Explorer**, правой кнопкой мыши проекта и выберите **Добавить** > **JavaScript файл**.</span><span class="sxs-lookup"><span data-stu-id="e8444-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="e8444-259">Назовите файл *StockTicker* и выберите **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8444-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="e8444-260">Добавьте этот код в файл *StockTicker.js:*</span><span class="sxs-lookup"><span data-stu-id="e8444-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="e8444-261">Изучить код клиента</span><span class="sxs-lookup"><span data-stu-id="e8444-261">Examine the client code</span></span>

<span data-ttu-id="e8444-262">Если вы изучите клиентский код, это поможет вам узнать, как клиентский код взаимодействует с серверным кодом, чтобы приложение работало.</span><span class="sxs-lookup"><span data-stu-id="e8444-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="e8444-263">Запуск соединения</span><span class="sxs-lookup"><span data-stu-id="e8444-263">Starting the connection</span></span>

<span data-ttu-id="e8444-264">`$.connection`относится к прокси SignalR.</span><span class="sxs-lookup"><span data-stu-id="e8444-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="e8444-265">Код получает ссылку на прокси `StockTickerHub` для класса и `ticker` помещает его в переменную.</span><span class="sxs-lookup"><span data-stu-id="e8444-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="e8444-266">Имя прокси — это имя, `HubName` которое было установлено атрибутом:</span><span class="sxs-lookup"><span data-stu-id="e8444-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="e8444-267">После определения всех переменных и функций последняя строка кода в файле инициализирует соединение SignalR, вызывая функцию SignalR. `start`</span><span class="sxs-lookup"><span data-stu-id="e8444-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="e8444-268">Функция `start` выполняет асинхронно и возвращает [отложенный объект j's'ry.](http://api.jquery.com/category/deferred-object/)</span><span class="sxs-lookup"><span data-stu-id="e8444-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="e8444-269">Можно вызвать выполненную функцию, чтобы указать функцию вызова, когда приложение завершает асинхронное действие.</span><span class="sxs-lookup"><span data-stu-id="e8444-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="e8444-270">Получение всех запасов</span><span class="sxs-lookup"><span data-stu-id="e8444-270">Getting all the stocks</span></span>

<span data-ttu-id="e8444-271">Функция `init` вызывает `getAllStocks` функцию на сервере и использует информацию, которую сервер возвращает для обновления таблицы запасов.</span><span class="sxs-lookup"><span data-stu-id="e8444-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="e8444-272">Обратите внимание, что по умолчанию, вы должны использовать camelCasing на клиенте, даже если имя метода pascal-cased на сервере.</span><span class="sxs-lookup"><span data-stu-id="e8444-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="e8444-273">Правило camelCasing применяется только к методам, а не к объектам.</span><span class="sxs-lookup"><span data-stu-id="e8444-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="e8444-274">Например, вы `stock.Symbol` ссылаетесь `stock.symbol` `stock.price`на и, `stock.Price`нет или .</span><span class="sxs-lookup"><span data-stu-id="e8444-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="e8444-275">В `init` методе приложение создает HTML для строки таблицы для каждого `formatStock` объекта акций, полученного от сервера, вызывая для формата `stock` свойства объекта, а затем вызывая `supplant` для замены заполнителей в `rowTemplate` переменной значения множества `stock` объектов.</span><span class="sxs-lookup"><span data-stu-id="e8444-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="e8444-276">Полученный HTML затем пригозывается к таблице запасов.</span><span class="sxs-lookup"><span data-stu-id="e8444-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="e8444-277">Вы `init` звоните, передавая `callback` его в качестве функции, `start` которая выполняет после асинхронной функции заканчивается.</span><span class="sxs-lookup"><span data-stu-id="e8444-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="e8444-278">Если вы `init` назвали отдельное заявление `start`JavaScript после вызова, функция выйдет из строя, потому что она будет работать немедленно, не дожидаясь завершения работы функции запуска, чтобы закончить создание соединения.</span><span class="sxs-lookup"><span data-stu-id="e8444-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="e8444-279">В этом случае `init` функция будет пытаться вызвать функцию `getAllStocks` до того, как приложение установит подключение к серверу.</span><span class="sxs-lookup"><span data-stu-id="e8444-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="e8444-280">Получение обновленных цен на акции</span><span class="sxs-lookup"><span data-stu-id="e8444-280">Getting updated stock prices</span></span>

<span data-ttu-id="e8444-281">Когда сервер изменяет цену акции, он `updateStockPrice` вызывает подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="e8444-282">Приложение добавляет функцию в свойство `stockTicker` клиента прокси, чтобы сделать его доступным для звонков с сервера.</span><span class="sxs-lookup"><span data-stu-id="e8444-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="e8444-283">`updateStockPrice` Функция форматирует объект акции, полученный от сервера, в `init` строку таблицы так же, как и в функции.</span><span class="sxs-lookup"><span data-stu-id="e8444-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="e8444-284">Вместо того, чтобы привить строку к таблице, он находит текущий ряд акции в таблице и заменяет эту строку на новую.</span><span class="sxs-lookup"><span data-stu-id="e8444-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="e8444-285">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="e8444-285">Test the application</span></span>

<span data-ttu-id="e8444-286">Вы можете проверить приложение, чтобы убедиться, что оно работает.</span><span class="sxs-lookup"><span data-stu-id="e8444-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="e8444-287">Вы увидите все окна браузера отображать живой стол акции с ценами на акции колеблются.</span><span class="sxs-lookup"><span data-stu-id="e8444-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="e8444-288">В панели инструментов включите **отладку скриптов,** а затем выберите кнопку воспроизведения для запуска приложения в режиме Debug.</span><span class="sxs-lookup"><span data-stu-id="e8444-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Скриншот включения пользователя в режим отладки и выбора воспроизведения.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="e8444-290">Окно браузера откроется отображение **Live Stock Таблица**.</span><span class="sxs-lookup"><span data-stu-id="e8444-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="e8444-291">Таблица акций сначала показывает "загрузку..." линия, то, после короткого времени, приложение показывает первоначальные данные акций, а затем цены на акции начинают меняться.</span><span class="sxs-lookup"><span data-stu-id="e8444-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="e8444-292">Копируйте URL-адрес из браузера, открывай два других браузера и вставьте URL-адреса в адресные бары.</span><span class="sxs-lookup"><span data-stu-id="e8444-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="e8444-293">Первоначальный дисплей акций такой же, как первый браузер и изменения происходят одновременно.</span><span class="sxs-lookup"><span data-stu-id="e8444-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="e8444-294">Закройте все браузеры, откройте новый браузер и перейдите на тот же URL.</span><span class="sxs-lookup"><span data-stu-id="e8444-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="e8444-295">Объект StockTicker singleton продолжал работать на сервере.</span><span class="sxs-lookup"><span data-stu-id="e8444-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="e8444-296">**Таблица Live Stock** показывает, что акции продолжают меняться.</span><span class="sxs-lookup"><span data-stu-id="e8444-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="e8444-297">Исходная таблица не просматривается с нулевыми цифрами изменений.</span><span class="sxs-lookup"><span data-stu-id="e8444-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="e8444-298">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="e8444-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="e8444-299">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="e8444-299">Enable logging</span></span>

<span data-ttu-id="e8444-300">SignalR имеет встроенную функцию регистрации, которую вы можете включить на клиента, чтобы помочь в устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="e8444-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="e8444-301">В этом разделе вы можете войти в систему и увидеть примеры, которые показывают, как журналы показывают, какой из следующих методов транспортировки Использует SignalR:</span><span class="sxs-lookup"><span data-stu-id="e8444-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="e8444-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), поддерживается IIS 8 и текущих браузеров.</span><span class="sxs-lookup"><span data-stu-id="e8444-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="e8444-303">[События, отправляемые серверами,](http://en.wikipedia.org/wiki/Server-sent_events)поддерживаемые браузерами, помимо Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="e8444-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="e8444-304">[Навсегда кадр](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), поддерживается Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="e8444-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="e8444-305">[Ajax долго опроса](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), поддерживается всеми браузерами.</span><span class="sxs-lookup"><span data-stu-id="e8444-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="e8444-306">Для любого данного соединения SignalR выбирает лучший способ транспортировки, который поддерживает ся сервер и клиент.</span><span class="sxs-lookup"><span data-stu-id="e8444-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="e8444-307">Открыть *StockTicker.js*.</span><span class="sxs-lookup"><span data-stu-id="e8444-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="e8444-308">Добавьте эту выделенную строку кода, чтобы включить журнал непосредственно перед кодом, который инициализирует соединение в конце файла:</span><span class="sxs-lookup"><span data-stu-id="e8444-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="e8444-309">Нажмите **F5** для запуска проекта.</span><span class="sxs-lookup"><span data-stu-id="e8444-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="e8444-310">Откройте окно инструментов для разработчиков браузера и выберите консоль, чтобы просмотреть журналы.</span><span class="sxs-lookup"><span data-stu-id="e8444-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="e8444-311">Возможно, вам придется обновить страницу, чтобы увидеть журналы SignalR переговоров метод транспортировки для нового соединения.</span><span class="sxs-lookup"><span data-stu-id="e8444-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="e8444-312">Если вы работаете Internet Explorer 10 на Windows 8 (IIS 8), способ транспортировки **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="e8444-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="e8444-313">Если вы работаете Internet Explorer 10 на Windows 7 (IIS 7.5), способ транспортировки **iframe**.</span><span class="sxs-lookup"><span data-stu-id="e8444-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="e8444-314">Если вы работаете Firefox 19 на Windows 8 (IIS 8), способ транспортировки **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="e8444-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="e8444-315">В Firefox установите надстройку Firebug, чтобы получить окно консоли.</span><span class="sxs-lookup"><span data-stu-id="e8444-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="e8444-316">Если вы работаете Firefox 19 на Windows 7 (IIS 7.5), способ транспортировки — это события, **отправляемые сервером.**</span><span class="sxs-lookup"><span data-stu-id="e8444-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="e8444-317">Установка образца StockTicker</span><span class="sxs-lookup"><span data-stu-id="e8444-317">Install the StockTicker sample</span></span>

<span data-ttu-id="e8444-318">[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) устанавливает приложение StockTicker.</span><span class="sxs-lookup"><span data-stu-id="e8444-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="e8444-319">Пакет NuGet включает в себя больше возможностей, чем упрощенная версия, которую вы создали с нуля.</span><span class="sxs-lookup"><span data-stu-id="e8444-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="e8444-320">В этом разделе учебника вы устанавливаете пакет NuGet и просматриваете новые функции и код, который их реализует.</span><span class="sxs-lookup"><span data-stu-id="e8444-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8444-321">Если вы установите пакет, не выполняя более ранние шаги этого руководства, вы должны добавить класс запуска OWIN в свой проект.</span><span class="sxs-lookup"><span data-stu-id="e8444-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="e8444-322">Этот файл readme.txt для пакета NuGet объясняет этот шаг.</span><span class="sxs-lookup"><span data-stu-id="e8444-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="e8444-323">Установка пакета SignalR.Sample NuGet</span><span class="sxs-lookup"><span data-stu-id="e8444-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="e8444-324">В **Solution Explorer**, правой кнопкой мыши проекта и выберите Управление **NuGet пакеты**.</span><span class="sxs-lookup"><span data-stu-id="e8444-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="e8444-325">В **NuGet менеджер пакета: SignalR.StockTicker**, выберите **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="e8444-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="e8444-326">Из **источника пакета**выберите **nuget.org**.</span><span class="sxs-lookup"><span data-stu-id="e8444-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="e8444-327">Введите *SignalR.Sample* в поле поиска и выберите **Microsoft.AspNet.SignalR.Sample** > **Install.**</span><span class="sxs-lookup"><span data-stu-id="e8444-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="e8444-328">В **Solution Explorer**расширьте папку *SignalR.Sample.*</span><span class="sxs-lookup"><span data-stu-id="e8444-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="e8444-329">Установка пакета SignalR.Sample создала папку и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="e8444-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="e8444-330">В папке *SignalR.Sample,* правой кнопкой мыши *StockTicker.html*, а затем выберите **Установить Как стартовая страница**.</span><span class="sxs-lookup"><span data-stu-id="e8444-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e8444-331">Установка пакета SignalR.Sample NuGet может изменить версию j's, которая у вас есть в папке *Скриптов.*</span><span class="sxs-lookup"><span data-stu-id="e8444-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="e8444-332">Новый файл *StockTicker.html,* который пакет устанавливается в папку *SignalR.Sample,* будет синхронизирован с версией j''ry, которую устанавливает пакет, но если вы хотите запустить исходный файл *StockTicker.html* снова, возможно, вам придется сначала обновить ссылку на j''образ в теге скрипта.</span><span class="sxs-lookup"><span data-stu-id="e8444-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="e8444-333">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="e8444-333">Run the application</span></span>

 <span data-ttu-id="e8444-334">Таблица, которую вы видели в первом приложении, имела полезные функции.</span><span class="sxs-lookup"><span data-stu-id="e8444-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="e8444-335">Полное приложение биржевых тикеров показывает новые функции: горизонтально прокрутки окна, которые показывают данные о запасах и акции, которые меняют цвет, как они поднимаются и падают.</span><span class="sxs-lookup"><span data-stu-id="e8444-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="e8444-336">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="e8444-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="e8444-337">При первом запуске приложения "рынок" "закрыт", и вы видите статичную таблицу и окно тикера, которое не прокручивается.</span><span class="sxs-lookup"><span data-stu-id="e8444-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="e8444-338">Выберите **открытый рынок**.</span><span class="sxs-lookup"><span data-stu-id="e8444-338">Select **Open Market**.</span></span>

    ![Скриншот живого тикера.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="e8444-340">Коробка **Live Stock Ticker** начинает прокручиваться горизонтально, и сервер начинает периодически транслировать изменения цен на акции на случайной основе.</span><span class="sxs-lookup"><span data-stu-id="e8444-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="e8444-341">Каждый раз, когда цена акций меняется, приложение обновляет как **Live Stock Table** и Live Stock **Ticker**.</span><span class="sxs-lookup"><span data-stu-id="e8444-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="e8444-342">Когда изменение цены акции является положительным, приложение показывает акции с зеленым фоном.</span><span class="sxs-lookup"><span data-stu-id="e8444-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="e8444-343">Когда изменение отрицательное, приложение показывает акции с красным фоном.</span><span class="sxs-lookup"><span data-stu-id="e8444-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="e8444-344">Выберите **Близкий рынок**.</span><span class="sxs-lookup"><span data-stu-id="e8444-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="e8444-345">Обновления таблицы останавливаются.</span><span class="sxs-lookup"><span data-stu-id="e8444-345">The table updates stop.</span></span>

    * <span data-ttu-id="e8444-346">Тикер останавливает прокрутку.</span><span class="sxs-lookup"><span data-stu-id="e8444-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="e8444-347">Выберите **Сброс**.</span><span class="sxs-lookup"><span data-stu-id="e8444-347">Select **Reset**.</span></span>

    * <span data-ttu-id="e8444-348">Все данные о запасах сбросить.</span><span class="sxs-lookup"><span data-stu-id="e8444-348">All stock data is reset.</span></span>

    * <span data-ttu-id="e8444-349">Приложение восстанавливает исходное состояние до начала изменения цен.</span><span class="sxs-lookup"><span data-stu-id="e8444-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="e8444-350">Копируйте URL-адрес из браузера, открывай два других браузера и вставьте URL-адреса в адресные бары.</span><span class="sxs-lookup"><span data-stu-id="e8444-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="e8444-351">В каждом браузере динамически обновляются одни и те же данные.</span><span class="sxs-lookup"><span data-stu-id="e8444-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="e8444-352">При выборе любого элемента управления все браузеры отвечают одинаково одновременно.</span><span class="sxs-lookup"><span data-stu-id="e8444-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="e8444-353">Live Фондовый Тикер дисплей</span><span class="sxs-lookup"><span data-stu-id="e8444-353">Live Stock Ticker display</span></span>

<span data-ttu-id="e8444-354">Дисплей **Live Stock Ticker** — это `<div>` неупорядоченный список в элементе, отформатированный в одну строку стилями CSS.</span><span class="sxs-lookup"><span data-stu-id="e8444-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="e8444-355">Приложение инициализирует и обновляет тикер так же, как таблица: путем замены заполнителей `<li>` в строке шаблона и динамического добавления `<li>` элементов в `<ul>` элемент.</span><span class="sxs-lookup"><span data-stu-id="e8444-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="e8444-356">Приложение включает в себя прокрутку `animate` с помощью функции j'ery, `<div>`чтобы изменять маржу слева от неупорядоченного списка в пределах .</span><span class="sxs-lookup"><span data-stu-id="e8444-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="e8444-357">SignalR.Sample StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="e8444-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="e8444-358">Фондовый тиккер HTML-код:</span><span class="sxs-lookup"><span data-stu-id="e8444-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="e8444-359">SignalR.Sample StockTicker.css</span><span class="sxs-lookup"><span data-stu-id="e8444-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="e8444-360">Код биржевого тикера CSS:</span><span class="sxs-lookup"><span data-stu-id="e8444-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="e8444-361">SignalR.Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="e8444-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="e8444-362">Код j''s, который делает его прокрутки:</span><span class="sxs-lookup"><span data-stu-id="e8444-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="e8444-363">Дополнительные методы на сервере, которые клиент может вызвать</span><span class="sxs-lookup"><span data-stu-id="e8444-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="e8444-364">Чтобы добавить гибкости в приложение, есть дополнительные методы, которые приложение может вызвать.</span><span class="sxs-lookup"><span data-stu-id="e8444-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="e8444-365">SignalR.Образец StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="e8444-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="e8444-366">Класс `StockTickerHub` определяет четыре дополнительных метода, которые клиент может вызвать:</span><span class="sxs-lookup"><span data-stu-id="e8444-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="e8444-367">Приложение вызывает `OpenMarket` `CloseMarket`, `Reset` , и в ответ на кнопки в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e8444-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="e8444-368">Они демонстрируют модель одного клиента, вызывающего изменение состояния, немедленно распространяемого для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="e8444-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="e8444-369">Каждый из этих методов `StockTicker` вызывает метод в классе, который вызывает изменение состояния рынка, а затем передает новое состояние.</span><span class="sxs-lookup"><span data-stu-id="e8444-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="e8444-370">SignalR.Образец StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="e8444-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="e8444-371">В `StockTicker` классе приложение поддерживает состояние рынка с свойством, `MarketState` которое возвращает `MarketState` значение enum:</span><span class="sxs-lookup"><span data-stu-id="e8444-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="e8444-372">Каждый из методов, изменяющие состояние рынка, `StockTicker` делает это внутри блока блокировки, поскольку класс должен быть безопасным для потоков:</span><span class="sxs-lookup"><span data-stu-id="e8444-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="e8444-373">Чтобы убедиться, что этот код `_marketState` является безопасным `MarketState` для потоков, поле, которое поддерживает свойство назначено: `volatile`</span><span class="sxs-lookup"><span data-stu-id="e8444-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="e8444-374">`BroadcastMarketStateChange` Методы `BroadcastMarketReset` и методы аналогичны методу BroadcastStockPrice, который вы уже видели, за исключением того, что они называют различные методы, определенные в клиенте:</span><span class="sxs-lookup"><span data-stu-id="e8444-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="e8444-375">Дополнительные функции клиента, которые сервер может вызвать</span><span class="sxs-lookup"><span data-stu-id="e8444-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="e8444-376">Функция `updateStockPrice` теперь обрабатывает как таблицу, так и `jQuery.Color` дисплей тикера, и она использует для вспышки красного и зеленого цветов.</span><span class="sxs-lookup"><span data-stu-id="e8444-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="e8444-377">Новые функции в *SignalR.StockTicker.js* позволяют отключить и отключить кнопки в зависимости от состояния рынка.</span><span class="sxs-lookup"><span data-stu-id="e8444-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="e8444-378">Они также останавливают или начинают горизонтальную прокрутку **Live Stock Ticker.**</span><span class="sxs-lookup"><span data-stu-id="e8444-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="e8444-379">Так как многие функции добавляются к `ticker.client`, приложение использует [функцию расширения j'sry,](http://api.jquery.com/jQuery.extend/) чтобы добавить их.</span><span class="sxs-lookup"><span data-stu-id="e8444-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="e8444-380">Дополнительная настройка клиента после установления соединения</span><span class="sxs-lookup"><span data-stu-id="e8444-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="e8444-381">После того, как клиент устанавливает соединение, он имеет некоторые дополнительные работы, чтобы сделать:</span><span class="sxs-lookup"><span data-stu-id="e8444-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="e8444-382">Узнайте, открыт ли рынок или закрыт `marketOpened` `marketClosed` для вызова соответствующей или функциональной функции.</span><span class="sxs-lookup"><span data-stu-id="e8444-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="e8444-383">Прикрепите вызовы метода сервера к кнопкам.</span><span class="sxs-lookup"><span data-stu-id="e8444-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="e8444-384">Методы сервера не подключены к кнопкам до тех пор, пока приложение не установит соединение.</span><span class="sxs-lookup"><span data-stu-id="e8444-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="e8444-385">Таким образом, код не может вызвать методы сервера до их появления.</span><span class="sxs-lookup"><span data-stu-id="e8444-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8444-386">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e8444-386">Additional resources</span></span>

<span data-ttu-id="e8444-387">В этом уроке вы узнали, как запрограммировать приложение SignalR, которое транслирует сообщения с сервера всем подключенным клиентам.</span><span class="sxs-lookup"><span data-stu-id="e8444-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="e8444-388">Теперь вы можете транслировать сообщения на периодической основе и в ответ на уведомления от любого клиента.</span><span class="sxs-lookup"><span data-stu-id="e8444-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="e8444-389">Вы можете использовать концепцию многопоточного экземпляра синглтона для поддержания состояния сервера в многопользовательских сценариях онлайн-игр.</span><span class="sxs-lookup"><span data-stu-id="e8444-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="e8444-390">Например, [см. игру ShootR на основе SignalR](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="e8444-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="e8444-391">Для учебников, которые показывают одноранговой сценарии общения, [см. Начало работы с SignalR](introduction-to-signalr.md) и [в режиме реального времени обновление с SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="e8444-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="e8444-392">Для получения дополнительной информации о SignalR см.</span><span class="sxs-lookup"><span data-stu-id="e8444-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="e8444-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="e8444-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="e8444-394">Проект SignalR</span><span class="sxs-lookup"><span data-stu-id="e8444-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="e8444-395">SignalR GitHub и образцы</span><span class="sxs-lookup"><span data-stu-id="e8444-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="e8444-396">SignalR Вики</span><span class="sxs-lookup"><span data-stu-id="e8444-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="e8444-397">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8444-397">Next steps</span></span>

<span data-ttu-id="e8444-398">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="e8444-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8444-399">Создан проект</span><span class="sxs-lookup"><span data-stu-id="e8444-399">Created the project</span></span>
> * <span data-ttu-id="e8444-400">Настройка кода сервера</span><span class="sxs-lookup"><span data-stu-id="e8444-400">Set up the server code</span></span>
> * <span data-ttu-id="e8444-401">Изучение кода сервера</span><span class="sxs-lookup"><span data-stu-id="e8444-401">Examined the server code</span></span>
> * <span data-ttu-id="e8444-402">Настройка кода клиента</span><span class="sxs-lookup"><span data-stu-id="e8444-402">Set up the client code</span></span>
> * <span data-ttu-id="e8444-403">Изучение кода клиента</span><span class="sxs-lookup"><span data-stu-id="e8444-403">Examined the client code</span></span>
> * <span data-ttu-id="e8444-404">тестирование приложения.</span><span class="sxs-lookup"><span data-stu-id="e8444-404">Tested the application</span></span>
> * <span data-ttu-id="e8444-405">Включенная регистрация</span><span class="sxs-lookup"><span data-stu-id="e8444-405">Enabled logging</span></span>

<span data-ttu-id="e8444-406">Перейти к следующей статье, чтобы узнать, как создать веб-приложение в режиме реального времени, который использует ASP.NET SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="e8444-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e8444-407">Создание веб-приложения в режиме реального времени с помощью SignalR</span><span class="sxs-lookup"><span data-stu-id="e8444-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
