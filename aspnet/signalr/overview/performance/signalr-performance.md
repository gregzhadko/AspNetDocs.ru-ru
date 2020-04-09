---
uid: signalr/overview/performance/signalr-performance
title: Производительность сигнала (англ.) Документы Майкрософт
author: bradygaster
description: Производительность SignalR
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675721"
---
# <a name="signalr-performance"></a><span data-ttu-id="d5efd-103">Производительность SignalR</span><span class="sxs-lookup"><span data-stu-id="d5efd-103">SignalR Performance</span></span>

<span data-ttu-id="d5efd-104">[Патрик Флетчер](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="d5efd-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d5efd-105">В этой теме описывается, как проектировать, измерять и повышать производительность в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5efd-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d5efd-106">Версии программного обеспечения, используемые в этой теме</span><span class="sxs-lookup"><span data-stu-id="d5efd-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="d5efd-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5efd-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="d5efd-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d5efd-108">.NET 4.5</span></span>
> - <span data-ttu-id="d5efd-109">Версия SignalR 2</span><span class="sxs-lookup"><span data-stu-id="d5efd-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="d5efd-110">Предыдущие версии этой темы</span><span class="sxs-lookup"><span data-stu-id="d5efd-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="d5efd-111">Для получения информации о более ранних версиях SignalR, см [SignalR Старые версии](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="d5efd-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="d5efd-112">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="d5efd-112">Questions and comments</span></span>
>
> <span data-ttu-id="d5efd-113">Пожалуйста, оставьте обратную связь о том, как вам понравился этот учебник и что мы могли бы улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d5efd-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d5efd-114">Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com.](http://stackoverflow.com/)</span><span class="sxs-lookup"><span data-stu-id="d5efd-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="d5efd-115">Для недавней презентации по производительности И масштабирования SignalR см. [Масштабирование Web в режиме реального времени с помощью ASP.NET SignalR.](https://channel9.msdn.com/Events/Build/2013/3-502)</span><span class="sxs-lookup"><span data-stu-id="d5efd-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="d5efd-116">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="d5efd-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="d5efd-117">Рекомендации по проектированию</span><span class="sxs-lookup"><span data-stu-id="d5efd-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="d5efd-118">Настройка сервера SignalR для производительности</span><span class="sxs-lookup"><span data-stu-id="d5efd-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="d5efd-119">Устранение проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="d5efd-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="d5efd-120">Использование счетчиков производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="d5efd-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="d5efd-121">Использование других счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="d5efd-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="d5efd-122">Прочие ресурсы</span><span class="sxs-lookup"><span data-stu-id="d5efd-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="d5efd-123">Рекомендации по проектированию</span><span class="sxs-lookup"><span data-stu-id="d5efd-123">Design considerations</span></span>

<span data-ttu-id="d5efd-124">В этом разделе описаны шаблоны, которые могут быть реализованы при проектировании приложения SignalR, чтобы гарантировать, что производительность не будет затруднена генерацией ненужного сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="d5efd-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="d5efd-125">Частота заседок сообщений</span><span class="sxs-lookup"><span data-stu-id="d5efd-125">Throttling message frequency</span></span>

<span data-ttu-id="d5efd-126">Даже в приложении, которое отправляет сообщения на высокой частоте (например, игровое приложение в реальном времени), большинству приложений не нужно отправлять больше, чем несколько сообщений в секунду.</span><span class="sxs-lookup"><span data-stu-id="d5efd-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="d5efd-127">Чтобы уменьшить объем трафика, генерируемого каждым клиентом, может быть реализован цикл сообщений, который выстраивает в очередь и отправляет сообщения не чаще, чем фиксированный тариф (т.е. до определенного количества сообщений будет отправляться каждую секунду, если в этот временной интервал для отправки будут отправляться сообщения).</span><span class="sxs-lookup"><span data-stu-id="d5efd-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="d5efd-128">Для примера приложения, которое задушит сообщения до определенной скорости (как от клиента, так и от сервера), [см.](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)</span><span class="sxs-lookup"><span data-stu-id="d5efd-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="d5efd-129">Уменьшение размера сообщения</span><span class="sxs-lookup"><span data-stu-id="d5efd-129">Reducing message size</span></span>

<span data-ttu-id="d5efd-130">Можно уменьшить размер сообщения SignalR, уменьшив размер сериализованных объектов.</span><span class="sxs-lookup"><span data-stu-id="d5efd-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="d5efd-131">В коде сервера, если вы отправляете объект, содержащий свойства, которые не должны передаваться, `JsonIgnore` не допускайте сериализации этих свойств с помощью атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5efd-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="d5efd-132">Имена свойств также сохраняются в сообщении; имена свойств можно сократить с `JsonProperty` помощью атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5efd-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="d5efd-133">Следующий пример кода показывает, как исключить отправку свойства клиенту и как сократить имена свойств:</span><span class="sxs-lookup"><span data-stu-id="d5efd-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="d5efd-134">**код сервера .NET, демонстрируя атрибут JsonIgnore, исключая отправку данных клиенту, и атрибут JsonProperty для уменьшения размера сообщения**</span><span class="sxs-lookup"><span data-stu-id="d5efd-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="d5efd-135">Для того, чтобы сохранить читаемость/обслуживание в клиентском коде, сокращенное имя собственности может быть переветрено к именам, удобным для человека, после получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="d5efd-136">Следующий пример кода демонстрирует один из возможных способов переошивания сокращенных имен на более `reMap` длинные, путем определения контракта на сообщение (отображение) и использования функции для применения контракта к оптимизированному классу сообщений:</span><span class="sxs-lookup"><span data-stu-id="d5efd-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="d5efd-137">**Код JavaScript на стороне клиента, который перенаговал сокращенные имена свойств для имен, читаемых человеком**</span><span class="sxs-lookup"><span data-stu-id="d5efd-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="d5efd-138">Имена могут быть сокращены в сообщениях от клиента к серверу, а также, используя тот же метод.</span><span class="sxs-lookup"><span data-stu-id="d5efd-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="d5efd-139">Уменьшение памяти (т.е. объем памяти, используемой для сообщения) объекта сообщения также может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="d5efd-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="d5efd-140">Например, если полный `int` диапазон не требуется, `short` или `byte` может быть использован вместо.</span><span class="sxs-lookup"><span data-stu-id="d5efd-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="d5efd-141">Поскольку сообщения хранятся в шине сообщений в памяти сервера, уменьшение размера сообщений может также решить проблемы с памятью сервера.</span><span class="sxs-lookup"><span data-stu-id="d5efd-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="d5efd-142">Настройка сервера SignalR для производительности</span><span class="sxs-lookup"><span data-stu-id="d5efd-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="d5efd-143">Следующие настройки конфигурации могут быть использованы для настройки сервера для повышения производительности в приложении SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5efd-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="d5efd-144">Для получения общей информации о том, как повысить производительность в ASP.NET приложении, см [ASP.NET.](https://msdn.microsoft.com/library/ff647787.aspx)</span><span class="sxs-lookup"><span data-stu-id="d5efd-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="d5efd-145">**Настройки конфигурации SignalR**</span><span class="sxs-lookup"><span data-stu-id="d5efd-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="d5efd-146">**DefaultMessageBufferSize**: По умолчанию SignalR сохраняет 1000 сообщений в памяти на один концентратор на подключение.</span><span class="sxs-lookup"><span data-stu-id="d5efd-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="d5efd-147">При использовании больших сообщений это может привести к проблемам с памятью, которые могут быть устранены за счет уменьшения этого значения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="d5efd-148">Эта настройка может `Application_Start` быть установлена в обработчике `Configuration` событий в ASP.NET приложении или в методе запуска класса OWIN в саморазмещении приложения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="d5efd-149">Следующий пример показывает, как уменьшить это значение, чтобы уменьшить память след вашего приложения, чтобы уменьшить количество используемой памяти сервера:</span><span class="sxs-lookup"><span data-stu-id="d5efd-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="d5efd-150">**код сервера .NET в Startup.cs для уменьшения размера буфера сообщения по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="d5efd-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="d5efd-151">**Настройки конфигурации IIS**</span><span class="sxs-lookup"><span data-stu-id="d5efd-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="d5efd-152">**Одновременное количество запросов на одно приложение:** Увеличение числа одновременных запросов IIS увеличит ресурсы серверов, доступные для обслуживания запросов.</span><span class="sxs-lookup"><span data-stu-id="d5efd-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="d5efd-153">Значение по умолчанию 5000; чтобы увеличить этот параметр, выполните следующие команды в повышенной оперативной версии:</span><span class="sxs-lookup"><span data-stu-id="d5efd-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="d5efd-154">**ApplicationPool Очередь Длина**: Это максимальное количество запросов, которые http.sys очереди для пула приложений.</span><span class="sxs-lookup"><span data-stu-id="d5efd-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="d5efd-155">Когда очередь заполнена, новые запросы получают 503 ответа «Недоступно ею» службы.</span><span class="sxs-lookup"><span data-stu-id="d5efd-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="d5efd-156">Значение по умолчанию ― 1000.</span><span class="sxs-lookup"><span data-stu-id="d5efd-156">The default value is 1000.</span></span>

    <span data-ttu-id="d5efd-157">Сокращение длины очереди для рабочего процесса в пуле приложений, вмещающих приложение, позволит сохранить ресурсы памяти.</span><span class="sxs-lookup"><span data-stu-id="d5efd-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="d5efd-158">Для получения дополнительной [информации см.](https://technet.microsoft.com/library/cc745955.aspx)</span><span class="sxs-lookup"><span data-stu-id="d5efd-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="d5efd-159">**ASP.NET настройки конфигурации**</span><span class="sxs-lookup"><span data-stu-id="d5efd-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="d5efd-160">Этот раздел включает параметры конфигурации, `aspnet.config` которые могут быть установлены в файле.</span><span class="sxs-lookup"><span data-stu-id="d5efd-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="d5efd-161">Этот файл находится в одном из двух мест, в зависимости от платформы:</span><span class="sxs-lookup"><span data-stu-id="d5efd-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="d5efd-162">ASP.NET настройки, которые могут улучшить производительность SignalR, включают в себя следующие:</span><span class="sxs-lookup"><span data-stu-id="d5efd-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="d5efd-163">**Максимальные одновременные запросы на процессор**: Увеличение этого параметра может облегчить узкие места производительности.</span><span class="sxs-lookup"><span data-stu-id="d5efd-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="d5efd-164">Чтобы увеличить этот параметр, добавьте `aspnet.config` следующую настройку конфигурации в файл:</span><span class="sxs-lookup"><span data-stu-id="d5efd-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="d5efd-165">**Запрос Предела очереди**: Когда общее `maxConcurrentRequestsPerCPU` количество подключений превышает настройку, ASP.NET начнетрегулировать запросы с помощью очереди.</span><span class="sxs-lookup"><span data-stu-id="d5efd-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="d5efd-166">Чтобы увеличить размер очереди, можно `requestQueueLimit` увеличить настройку.</span><span class="sxs-lookup"><span data-stu-id="d5efd-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="d5efd-167">Для этого добавьте следующую настройку конфигурации `processModel` в `aspnet.config` `config/machine.config` узло (а не на):</span><span class="sxs-lookup"><span data-stu-id="d5efd-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="d5efd-168">Устранение проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="d5efd-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="d5efd-169">В этом разделе описаны способы поиска узких мест в приложении.</span><span class="sxs-lookup"><span data-stu-id="d5efd-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="d5efd-170">Проверка использования WebSocket</span><span class="sxs-lookup"><span data-stu-id="d5efd-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="d5efd-171">В то время как SignalR может использовать различные переносы для связи между клиентом и сервером, WebSocket предлагает значительное преимущество в производительности, и должен использоваться, если клиент и сервер поддерживают его.</span><span class="sxs-lookup"><span data-stu-id="d5efd-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="d5efd-172">Чтобы определить, соответствует ли ваш клиент и сервер [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports)требованиям WebSocket, см.</span><span class="sxs-lookup"><span data-stu-id="d5efd-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="d5efd-173">Чтобы определить, какой транспорт используется в приложении, можно использовать инструменты разработчика браузера и изучить журналы, чтобы узнать, какой транспорт используется для подключения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="d5efd-174">Для получения информации об использовании инструментов разработки браузера в Internet Explorer и Chrome [см.](../getting-started/introduction-to-signalr.md#transports)</span><span class="sxs-lookup"><span data-stu-id="d5efd-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="d5efd-175">Использование счетчиков производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="d5efd-175">Using SignalR performance counters</span></span>

<span data-ttu-id="d5efd-176">В этом разделе описывается, как включить и использовать `Microsoft.AspNet.SignalR.Utils` счетчики производительности SignalR, найденные в пакете.</span><span class="sxs-lookup"><span data-stu-id="d5efd-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="d5efd-177">Установка сигнальщика.exe</span><span class="sxs-lookup"><span data-stu-id="d5efd-177">Installing signalr.exe</span></span>

<span data-ttu-id="d5efd-178">Счетчики производительности могут быть добавлены на сервер с помощью утилиты под названием SignalR.exe.</span><span class="sxs-lookup"><span data-stu-id="d5efd-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="d5efd-179">Чтобы установить эту утилиту, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d5efd-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="d5efd-180">В Visual Studio выберите **Инструменты** > **NuGet менеджер** > пакета**управлять NuGet пакеты для решения**</span><span class="sxs-lookup"><span data-stu-id="d5efd-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="d5efd-181">Поиск **signalr.utils**и выберите Install.</span><span class="sxs-lookup"><span data-stu-id="d5efd-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="d5efd-182">Примите лицензионное соглашение об установке пакета.</span><span class="sxs-lookup"><span data-stu-id="d5efd-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="d5efd-183">SignalR.exe будет установлен `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`для .</span><span class="sxs-lookup"><span data-stu-id="d5efd-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="d5efd-184">Установка счетчиков производительности с помощью SignalR.exe</span><span class="sxs-lookup"><span data-stu-id="d5efd-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="d5efd-185">Чтобы установить счетчики производительности SignalR, запустите SignalR.exe в повышенном командном запросе со следующим параметром:</span><span class="sxs-lookup"><span data-stu-id="d5efd-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="d5efd-186">Чтобы удалить счетчики производительности SignalR, запустите SignalR.exe в повышенном запросе команды со следующим параметром:</span><span class="sxs-lookup"><span data-stu-id="d5efd-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="d5efd-187">Счетчики производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="d5efd-187">SignalR Performance counters</span></span>

<span data-ttu-id="d5efd-188">Пакет утилит устанавливает следующие счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="d5efd-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="d5efd-189">Счетчики "Всего" измеряют количество событий с момента перезапуска последнего пула приложений или сервера.</span><span class="sxs-lookup"><span data-stu-id="d5efd-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="d5efd-190">**Метрики подключения**</span><span class="sxs-lookup"><span data-stu-id="d5efd-190">**Connection metrics**</span></span>

<span data-ttu-id="d5efd-191">Следующие метрики измеряют события жизни соединения, которые происходят.</span><span class="sxs-lookup"><span data-stu-id="d5efd-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="d5efd-192">Для получения дополнительной информации [см.](../guide-to-the-api/handling-connection-lifetime-events.md)</span><span class="sxs-lookup"><span data-stu-id="d5efd-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="d5efd-193">**Подключение к соединениям**</span><span class="sxs-lookup"><span data-stu-id="d5efd-193">**Connections Connected**</span></span>
- <span data-ttu-id="d5efd-194">**Соединения повторно подключены**</span><span class="sxs-lookup"><span data-stu-id="d5efd-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="d5efd-195">**Соединения отключены**</span><span class="sxs-lookup"><span data-stu-id="d5efd-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="d5efd-196">**Соединения Ток**</span><span class="sxs-lookup"><span data-stu-id="d5efd-196">**Connections Current**</span></span>

<span data-ttu-id="d5efd-197">**Метрики использования**</span><span class="sxs-lookup"><span data-stu-id="d5efd-197">**Message metrics**</span></span>

<span data-ttu-id="d5efd-198">Следующие метрики измеряют трафик сообщений, генерируемый SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5efd-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="d5efd-199">**Сообщения о подключении, полученные всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="d5efd-200">**Сообщения о подключении Отправлено Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="d5efd-201">**Полученные сообщения о подключении/Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="d5efd-202">**Сообщения о подключении Отправлено/Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="d5efd-203">**Метрики шины сообщений**</span><span class="sxs-lookup"><span data-stu-id="d5efd-203">**Message bus metrics**</span></span>

<span data-ttu-id="d5efd-204">Следующие метрики измеряют трафик через внутренний шину сообщений SignalR, очередь, в которой размещаются все входящие и исходящие сообщения SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5efd-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="d5efd-205">Сообщение **публикуется** при отправке или трансляции.</span><span class="sxs-lookup"><span data-stu-id="d5efd-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="d5efd-206">**Абонентом** в этом контексте является подписка на шину сообщений; это должно равняться числу клиентов плюс самому серверу.</span><span class="sxs-lookup"><span data-stu-id="d5efd-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="d5efd-207">**Распределенный работник** — это компонент, который отправляет данные на активные соединения; **Занят работник** является тот, который активно отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="d5efd-208">**Сообщения шины Сообщения Получено Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="d5efd-209">**Сообщения автобус сообщения получены / Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="d5efd-210">**Сообщения Автобус Сообщения Опубликовано Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="d5efd-211">**Сообщения автобус сообщения Опубликовано / Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="d5efd-212">**Сообщения Автобус Абоненты Текущий**</span><span class="sxs-lookup"><span data-stu-id="d5efd-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="d5efd-213">**Сообщение Автобус Абоненты Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="d5efd-214">**Подписчики автобусов сообщений/Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="d5efd-215">**Сообщение Автобус Выделенные работники**</span><span class="sxs-lookup"><span data-stu-id="d5efd-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="d5efd-216">**Сообщение Автобус Занятые рабочие**</span><span class="sxs-lookup"><span data-stu-id="d5efd-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="d5efd-217">**Сообщение Автобус Темы Текущие**</span><span class="sxs-lookup"><span data-stu-id="d5efd-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="d5efd-218">**Метрики ошибок**</span><span class="sxs-lookup"><span data-stu-id="d5efd-218">**Error metrics**</span></span>

<span data-ttu-id="d5efd-219">Следующие метрики измеряют ошибки, генерируемые трафиком сообщений SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5efd-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="d5efd-220">**Ошибки разрешения концентратора** возникают, когда не удается разрешить метод концентратора или концентратора.</span><span class="sxs-lookup"><span data-stu-id="d5efd-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="d5efd-221">Ошибки **вызова концентратора** являются исключениями, брошенными при вызове метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="d5efd-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="d5efd-222">**Ошибки транспорта** являются ошибками соединения, брошенными во время запроса или ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5efd-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="d5efd-223">**Ошибки: Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-223">**Errors: All Total**</span></span>
- <span data-ttu-id="d5efd-224">**Ошибки: Все/Сек**</span><span class="sxs-lookup"><span data-stu-id="d5efd-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="d5efd-225">**Ошибки: Общее разрешение концентратора**</span><span class="sxs-lookup"><span data-stu-id="d5efd-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="d5efd-226">**Ошибки: Разрешение концентратора/Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="d5efd-227">**Ошибки: Всего вызов концентратора**</span><span class="sxs-lookup"><span data-stu-id="d5efd-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="d5efd-228">**Ошибки: Вызов концентратора/Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="d5efd-229">**Ошибки: Транспорт Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="d5efd-230">**Ошибки: Транспорт/Сек**</span><span class="sxs-lookup"><span data-stu-id="d5efd-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="d5efd-231">**Показатели масштабирования**</span><span class="sxs-lookup"><span data-stu-id="d5efd-231">**Scaleout metrics**</span></span>

<span data-ttu-id="d5efd-232">Следующие метрики измеряют трафик и ошибки, генерируемые поставщиком масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d5efd-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="d5efd-233">**Поток** в этом контексте — это единица масштаба, используемая поставщиком масштабирования; это таблица, если используется S'L Server, Тема, если используется сервисный автобус, и подписка, если используется Redis.</span><span class="sxs-lookup"><span data-stu-id="d5efd-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="d5efd-234">Каждый поток обеспечивает упорядоченные операции чтения и записи; один поток является потенциальным узким местом масштаба, поэтому количество потоков может быть увеличено, чтобы помочь уменьшить это узкое место.</span><span class="sxs-lookup"><span data-stu-id="d5efd-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="d5efd-235">Если используется несколько потоков, SignalR будет автоматически распространять (осколок) сообщения через эти потоки таким образом, чтобы обеспечить в порядке сообщения, отправленные из любого данного соединения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="d5efd-236">Настройка [Max'UeLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) контролирует длину очереди отправки масштаба, поддерживаемую SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5efd-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="d5efd-237">Установка его на значение больше 0 разместит все сообщения в очереди отправки для отправки по одному на настроенный задняя плоскость обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d5efd-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="d5efd-238">Если размер очереди превышает настроенную длину, последующие вызовы для отправки немедленно сходят с отсутсвия с [Помощью InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) до тех пор, пока количество сообщений в очереди не будет меньше, чем снова настройки.</span><span class="sxs-lookup"><span data-stu-id="d5efd-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="d5efd-239">Очередь отключена по умолчанию, потому что реализованные backplanes обычно имеют свои собственные очереди или контроль потока на месте.</span><span class="sxs-lookup"><span data-stu-id="d5efd-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="d5efd-240">В случае s'L Server объединение соединений эффективно ограничивает количество отправлений, проходящих в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="d5efd-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="d5efd-241">По умолчанию для Сервера и Редиса используется только один поток, пять потоков используются для Service Bus, а очереди отключены, но эти настройки можно изменить через конфигурацию на сервере S'L и Сервисном автобусе:</span><span class="sxs-lookup"><span data-stu-id="d5efd-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="d5efd-242">**Код сервера .NET для настройки количества таблиц и длины очереди для резервного самолета S'L Server**</span><span class="sxs-lookup"><span data-stu-id="d5efd-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="d5efd-243">**код сервера .NET для настройки количества тем и длины очереди для резервного самолета Service Bus**</span><span class="sxs-lookup"><span data-stu-id="d5efd-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="d5efd-244">**Буферный** поток — это поток, вошедчий в неисправное состояние; когда поток находится в неисправном состоянии, все сообщения, отправленные на заднее плоскость, немедленно не сбудутся до тех пор, пока поток больше не не будет развиться.</span><span class="sxs-lookup"><span data-stu-id="d5efd-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="d5efd-245">**Длина очереди Отправки** — это количество сообщений, которые были отправлены, но еще не отправлены.</span><span class="sxs-lookup"><span data-stu-id="d5efd-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="d5efd-246">**Полученные сообщения о перечне сообщения сообщения/sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="d5efd-247">**Масштабирование потоков Всего**</span><span class="sxs-lookup"><span data-stu-id="d5efd-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="d5efd-248">**Открытые масштабные потоки**</span><span class="sxs-lookup"><span data-stu-id="d5efd-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="d5efd-249">**Масштабирование потоков буферизации**</span><span class="sxs-lookup"><span data-stu-id="d5efd-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="d5efd-250">**Общее количество ошибок масштабирования**</span><span class="sxs-lookup"><span data-stu-id="d5efd-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="d5efd-251">**Ошибки масштабирования/Sec**</span><span class="sxs-lookup"><span data-stu-id="d5efd-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="d5efd-252">**Масштабирование Отправка Длина очереди**</span><span class="sxs-lookup"><span data-stu-id="d5efd-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="d5efd-253">Для получения дополнительной информации о том, что эти счетчики измерения, см [SignalR Масштабирование с Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="d5efd-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="d5efd-254">Использование других счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="d5efd-254">Using other performance counters</span></span>

<span data-ttu-id="d5efd-255">Следующие счетчики производительности также могут быть полезны для мониторинга производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="d5efd-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="d5efd-256">**Память**</span><span class="sxs-lookup"><span data-stu-id="d5efd-256">**Memory**</span></span>

- <span data-ttu-id="d5efd-257">.NET CLR\\Память - байты во всех кучи (для w3wp)</span><span class="sxs-lookup"><span data-stu-id="d5efd-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="d5efd-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="d5efd-258">**ASP.NET**</span></span>

- <span data-ttu-id="d5efd-259">ASP.NET - Запросы Текущий</span><span class="sxs-lookup"><span data-stu-id="d5efd-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="d5efd-260">ASP.NET-Очередь</span><span class="sxs-lookup"><span data-stu-id="d5efd-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="d5efd-261">ASP.NET -Отклонено</span><span class="sxs-lookup"><span data-stu-id="d5efd-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="d5efd-262">**Процессора**</span><span class="sxs-lookup"><span data-stu-id="d5efd-262">**CPU**</span></span>

- <span data-ttu-id="d5efd-263">Информация об процессоре/Время процессора</span><span class="sxs-lookup"><span data-stu-id="d5efd-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="d5efd-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="d5efd-264">**TCP/IP**</span></span>

- <span data-ttu-id="d5efd-265">TCPv6/Соединения Созданы</span><span class="sxs-lookup"><span data-stu-id="d5efd-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="d5efd-266">TCPv4/Соединения Созданы</span><span class="sxs-lookup"><span data-stu-id="d5efd-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="d5efd-267">**Веб-сервис**</span><span class="sxs-lookup"><span data-stu-id="d5efd-267">**Web Service**</span></span>

- <span data-ttu-id="d5efd-268">Веб-служба (текущие подключения)</span><span class="sxs-lookup"><span data-stu-id="d5efd-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="d5efd-269">Веб-служба-Максимальные соединения</span><span class="sxs-lookup"><span data-stu-id="d5efd-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="d5efd-270">**Потоки**</span><span class="sxs-lookup"><span data-stu-id="d5efd-270">**Threading**</span></span>

- <span data-ttu-id="d5efd-271">.NET CLR Замки\\и темы - текущие логические темы</span><span class="sxs-lookup"><span data-stu-id="d5efd-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="d5efd-272">.NET CLR замки\\и темы - текущих физических потоков</span><span class="sxs-lookup"><span data-stu-id="d5efd-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="d5efd-273">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="d5efd-273">Other Resources</span></span>

<span data-ttu-id="d5efd-274">Для получения дополнительной информации о мониторинге и настройке ASP.NET производительности см.</span><span class="sxs-lookup"><span data-stu-id="d5efd-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="d5efd-275">[Общие сведения о производительности ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="d5efd-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="d5efd-276">ASP.NET использование нитей на IIS 7.5, IIS 7.0 и IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="d5efd-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="d5efd-277">&lt;элемент&gt; applicationPool (веб-настройки)</span><span class="sxs-lookup"><span data-stu-id="d5efd-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
