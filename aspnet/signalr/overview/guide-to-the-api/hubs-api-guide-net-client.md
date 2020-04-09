---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET Руководство aPI концентраторов SignalR - .NET Клиент (C) Документы Майкрософт
author: bradygaster
description: Этот документ содержит введение в использование API-адреса концентратов для версии SignalR 2 у клиентов .NET, таких как Магазин Windows (WinRT), WPF, Silverlight и против...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675931"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="df6de-103">ASP.NET Руководство aPI концентраторов SignalR - .NET Клиент (C)</span><span class="sxs-lookup"><span data-stu-id="df6de-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="df6de-104">Этот документ содержит введение в использование API-адреса концентратов для версии SignalR 2 у клиентов .NET, таких как Windows Store (WinRT), WPF, Silverlight и консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="df6de-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="df6de-105">API Концентраторов SignalR позволяет совершать удаленные процедурные звонки (RPCs) с сервера для подключенных клиентов и от клиентов к серверу.</span><span class="sxs-lookup"><span data-stu-id="df6de-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="df6de-106">В коде сервера вы определяете методы, которые могут вызываться клиентами, и вызываете методы, которые работают на клиенте.</span><span class="sxs-lookup"><span data-stu-id="df6de-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="df6de-107">В клиентском коде вы определяете методы, которые можно вызывать с сервера, и вызываете методы, которые работают на сервере.</span><span class="sxs-lookup"><span data-stu-id="df6de-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="df6de-108">SignalR заботится о всех клиента к серверу сантехника для вас.</span><span class="sxs-lookup"><span data-stu-id="df6de-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="df6de-109">SignalR также предлагает API более низкого уровня под названием Persistent Connections.</span><span class="sxs-lookup"><span data-stu-id="df6de-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="df6de-110">Для введения в SignalR, концентраторы, и стойкие соединения, или для учебника, который показывает, как построить полное приложение SignalR, см [SignalR - Начало работы](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="df6de-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="df6de-111">Версии программного обеспечения, используемые в этой теме</span><span class="sxs-lookup"><span data-stu-id="df6de-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="df6de-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="df6de-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="df6de-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="df6de-113">.NET 4.5</span></span>
> - <span data-ttu-id="df6de-114">Версия SignalR 2</span><span class="sxs-lookup"><span data-stu-id="df6de-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="df6de-115">Предыдущие версии этой темы</span><span class="sxs-lookup"><span data-stu-id="df6de-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="df6de-116">Для получения информации о более ранних версиях SignalR, см [SignalR Старые версии](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="df6de-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="df6de-117">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="df6de-117">Questions and comments</span></span>
>
> <span data-ttu-id="df6de-118">Пожалуйста, оставьте обратную связь о том, как вам понравился этот учебник и что мы могли бы улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="df6de-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="df6de-119">Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com.](http://stackoverflow.com/)</span><span class="sxs-lookup"><span data-stu-id="df6de-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="df6de-120">Обзор</span><span class="sxs-lookup"><span data-stu-id="df6de-120">Overview</span></span>

<span data-ttu-id="df6de-121">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="df6de-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="df6de-122">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="df6de-123">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="df6de-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="df6de-124">Кросс-доменсоединения от клиентов Silverlight</span><span class="sxs-lookup"><span data-stu-id="df6de-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="df6de-125">Как настроить соединение</span><span class="sxs-lookup"><span data-stu-id="df6de-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="df6de-126">Как установить максимальное количество одновременных подключений в клиентах WPF</span><span class="sxs-lookup"><span data-stu-id="df6de-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="df6de-127">Как указать параметры строки запроса</span><span class="sxs-lookup"><span data-stu-id="df6de-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="df6de-128">Как указать транспортный метод</span><span class="sxs-lookup"><span data-stu-id="df6de-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="df6de-129">Как указать заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="df6de-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="df6de-130">Как указать сертификаты клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="df6de-131">Как создать прокси-сервер концентратора</span><span class="sxs-lookup"><span data-stu-id="df6de-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="df6de-132">Как определить методы на клиенте, который может вызвать сервер</span><span class="sxs-lookup"><span data-stu-id="df6de-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="df6de-133">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="df6de-134">Методы с параметрами, определяющие типы параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="df6de-135">Методы с параметрами, определяющие динамические объекты для параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="df6de-136">Как удалить обработчик</span><span class="sxs-lookup"><span data-stu-id="df6de-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="df6de-137">Как вызвать методы сервера от клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="df6de-138">Как обрабатывать события жизни соединения</span><span class="sxs-lookup"><span data-stu-id="df6de-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="df6de-139">Как обрабатывать ошибки</span><span class="sxs-lookup"><span data-stu-id="df6de-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="df6de-140">Как включить журналирование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="df6de-141">Образцы кода приложений WPF, Silverlight и консольных приложений для методов клиента, которые сервер может вызвать</span><span class="sxs-lookup"><span data-stu-id="df6de-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="df6de-142">Для примера клиентских проектов .NET см.</span><span class="sxs-lookup"><span data-stu-id="df6de-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="df6de-143">[gustavo-armenta / SignalR-Образцы](https://github.com/gustavo-armenta/SignalR-Samples) на GitHub.com (WinRT, Silverlight, примеры консольных приложений).</span><span class="sxs-lookup"><span data-stu-id="df6de-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="df6de-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) на GitHub.com (пример WPF).</span><span class="sxs-lookup"><span data-stu-id="df6de-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="df6de-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) на GitHub.com (пример приложения для консоли).</span><span class="sxs-lookup"><span data-stu-id="df6de-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="df6de-146">Для получения документации о том, как запрограммировать сервер или JavaScript клиентов, см.</span><span class="sxs-lookup"><span data-stu-id="df6de-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="df6de-147">Руководство По API Концентратов SignalR - Сервер</span><span class="sxs-lookup"><span data-stu-id="df6de-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="df6de-148">Руководство По API Концентратов SignalR - Клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="df6de-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="df6de-149">Ссылки на темы API Справочные ссылки на .NET 4.5 версия API.</span><span class="sxs-lookup"><span data-stu-id="df6de-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="df6de-150">Если вы используете .NET 4, [см.](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="df6de-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="df6de-151">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-151">Client setup</span></span>

<span data-ttu-id="df6de-152">Установите пакет [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet (не пакет [Microsoft.AspNet.SignalR).](http://nuget.org/packages/microsoft.aspnet.signalr)</span><span class="sxs-lookup"><span data-stu-id="df6de-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="df6de-153">Этот пакет поддерживает клиентов WinRT, Silverlight, WPF, консольных приложений и Windows Phone как для .NET 4, так и для .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="df6de-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="df6de-154">Если версия SignalR, которая у вас есть на клиенте отличается от версии, что у вас есть на сервере, SignalR часто в состоянии адаптироваться к разнице.</span><span class="sxs-lookup"><span data-stu-id="df6de-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="df6de-155">Например, сервер под управлением signalR версии 2 будет поддерживать клиентов, которые имеют 1.1.x установлен, а также клиентов, которые имеют версию 2 установлен.</span><span class="sxs-lookup"><span data-stu-id="df6de-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="df6de-156">Если разница между версией на сервере и версией на клиенте слишком велика, или если клиент `InvalidOperationException` новее, чем сервер, SignalR бросает исключение, когда клиент пытается установить соединение.</span><span class="sxs-lookup"><span data-stu-id="df6de-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="df6de-157">Сообщение об ошибке ".`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`</span><span class="sxs-lookup"><span data-stu-id="df6de-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="df6de-158">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="df6de-158">How to establish a connection</span></span>

<span data-ttu-id="df6de-159">Прежде чем установить соединение, необходимо `HubConnection` создать объект и создать прокси-</span><span class="sxs-lookup"><span data-stu-id="df6de-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="df6de-160">Чтобы установить соединение, `Start` позвоните `HubConnection` методу на объект.</span><span class="sxs-lookup"><span data-stu-id="df6de-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="df6de-161">Для клиентов JavaScript необходимо зарегистрировать по крайней `Start` мере одного обработчика событий, прежде чем вызвать метод для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="df6de-162">Это не обязательно для клиентов .NET.</span><span class="sxs-lookup"><span data-stu-id="df6de-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="df6de-163">Для клиентов JavaScript сгенерированный прокси-код автоматически создает прокси-серверы для всех концентраторов, которые существуют на сервере, и регистрация обработчика — это то, как вы указываете, какие концентраторы, которые намерен использовать клиент.</span><span class="sxs-lookup"><span data-stu-id="df6de-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="df6de-164">Но для клиента .NET вы создаете прокси-серверы концентратора вручную, поэтому SignalR предполагает, что вы будете использовать любой концентратор, для которого вы создаете прокси.</span><span class="sxs-lookup"><span data-stu-id="df6de-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="df6de-165">Пример кода использует URL-адрес по умолчанию "/сигнальщик" для подключения к службе SignalR.</span><span class="sxs-lookup"><span data-stu-id="df6de-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="df6de-166">Для получения информации о том, как указать другой базовый URL, см [ASP.NET.](hubs-api-guide-server.md#signalrurl)</span><span class="sxs-lookup"><span data-stu-id="df6de-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="df6de-167">Метод `Start` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="df6de-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="df6de-168">Чтобы убедиться, что последующие строки кода не выполняются `await` до тех пор, пока соединение `.Wait()` не будет установлено, используйте в ASP.NET 4.5 асинхронного метода или в синхронном методе.</span><span class="sxs-lookup"><span data-stu-id="df6de-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="df6de-169">Не используйте `.Wait()` в клиенте WinRT.</span><span class="sxs-lookup"><span data-stu-id="df6de-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="df6de-170">Кросс-доменсоединения от клиентов Silverlight</span><span class="sxs-lookup"><span data-stu-id="df6de-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="df6de-171">Для получения информации о том, как включить кросс-домен соединения от клиентов Silverlight, [см.](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="df6de-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="df6de-172">Как настроить соединение</span><span class="sxs-lookup"><span data-stu-id="df6de-172">How to configure the connection</span></span>

<span data-ttu-id="df6de-173">Прежде чем установить соединение, можно указать любой из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="df6de-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="df6de-174">Одновременное ограничение соединений.</span><span class="sxs-lookup"><span data-stu-id="df6de-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="df6de-175">Параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="df6de-175">Query string parameters.</span></span>
- <span data-ttu-id="df6de-176">Транспортный метод.</span><span class="sxs-lookup"><span data-stu-id="df6de-176">The transport method.</span></span>
- <span data-ttu-id="df6de-177">ЗАГОЛОВКи HTTP.</span><span class="sxs-lookup"><span data-stu-id="df6de-177">HTTP headers.</span></span>
- <span data-ttu-id="df6de-178">Сертификаты клиентов.</span><span class="sxs-lookup"><span data-stu-id="df6de-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="df6de-179">Как установить максимальное количество одновременных подключений в клиентах WPF</span><span class="sxs-lookup"><span data-stu-id="df6de-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="df6de-180">В клиентах WPF может потребоваться увеличить максимальное количество одновременных подключений от значения по умолчанию 2.</span><span class="sxs-lookup"><span data-stu-id="df6de-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="df6de-181">Рекомендуемое значение 10.</span><span class="sxs-lookup"><span data-stu-id="df6de-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="df6de-182">Для получения дополнительной информации [см.](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)</span><span class="sxs-lookup"><span data-stu-id="df6de-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="df6de-183">Как указать параметры строки запроса</span><span class="sxs-lookup"><span data-stu-id="df6de-183">How to specify query string parameters</span></span>

<span data-ttu-id="df6de-184">Если вы хотите отправить данные на сервер при подключении клиента, можно добавить параметры строки запроса к объекту соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="df6de-185">В следующем примере показано, как установить параметр строки запроса в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="df6de-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="df6de-186">В следующем примере показано, как прочитать параметр строки запроса в коде сервера.</span><span class="sxs-lookup"><span data-stu-id="df6de-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="df6de-187">Как указать транспортный метод</span><span class="sxs-lookup"><span data-stu-id="df6de-187">How to specify the transport method</span></span>

<span data-ttu-id="df6de-188">В процессе подключения клиент SignalR обычно ведет переговоры с сервером, чтобы определить наилучший транспорт, который поддерживается как сервером, так и клиентом.</span><span class="sxs-lookup"><span data-stu-id="df6de-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="df6de-189">Если вы уже знаете, какой транспорт вы хотите использовать, вы можете обойти этот процесс переговоров.</span><span class="sxs-lookup"><span data-stu-id="df6de-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="df6de-190">Чтобы указать способ транспортировки, передайте в транспортном объекте методу Start.</span><span class="sxs-lookup"><span data-stu-id="df6de-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="df6de-191">В следующем примере показано, как указать метод транспортировки в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="df6de-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="df6de-192">В названии [Microsoft.AspNet.SignalR.Client.Transports включены](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) следующие классы, которые можно использовать для указания транспорта.</span><span class="sxs-lookup"><span data-stu-id="df6de-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="df6de-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="df6de-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="df6de-194">[СерверСентСобытийТранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="df6de-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="df6de-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (доступно только при использовании сервера и клиента .NET 4.5.)</span><span class="sxs-lookup"><span data-stu-id="df6de-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="df6de-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Автоматически выбирает лучший транспорт, который поддерживается как клиентом, так и сервером.</span><span class="sxs-lookup"><span data-stu-id="df6de-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="df6de-197">Это транспорт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="df6de-197">This is the default transport.</span></span> <span data-ttu-id="df6de-198">Передача этого `Start` в метод имеет тот же эффект, как не проходя ни в чем.)</span><span class="sxs-lookup"><span data-stu-id="df6de-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="df6de-199">Транспорт ForeverFrame не включен в этот список, поскольку он используется только браузерами.</span><span class="sxs-lookup"><span data-stu-id="df6de-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="df6de-200">Подробнее о том, как проверить метод транспортировки в серверном коде, смотрите [ASP.NET Руководство по aPI SignalR Hubs API - Server - Как получить информацию о клиенте из свойства Контекста.](hubs-api-guide-server.md#contextproperty)</span><span class="sxs-lookup"><span data-stu-id="df6de-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="df6de-201">Для получения дополнительной информации о транспорте и откатов, [см. Введение в SignalR - Транспорт и Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="df6de-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="df6de-202">Как указать заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="df6de-202">How to specify HTTP headers</span></span>

<span data-ttu-id="df6de-203">Чтобы установить заголовки `Headers` HTTP, используйте свойство на объекте соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="df6de-204">Ниже приводится следующий пример, как добавить заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="df6de-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="df6de-205">Как указать сертификаты клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-205">How to specify client certificates</span></span>

<span data-ttu-id="df6de-206">Чтобы добавить сертификаты `AddClientCertificate` клиента, используйте метод на объекте соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="df6de-207">Как создать прокси-сервер концентратора</span><span class="sxs-lookup"><span data-stu-id="df6de-207">How to create the Hub proxy</span></span>

<span data-ttu-id="df6de-208">Для определения методов клиента, которые концентратор может вызвать с сервера, и вызова методов на концентраторе на сервере, создайте прокси для концентратора, вызывая `CreateHubProxy` объект соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="df6de-209">Строка, которую `CreateHubProxy` вы передаете, — это имя класса `HubName` концентратора или имя, указанное атрибутом, если он был использован на сервере.</span><span class="sxs-lookup"><span data-stu-id="df6de-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="df6de-210">Сопоставление имен не зависит от регистра.</span><span class="sxs-lookup"><span data-stu-id="df6de-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="df6de-211">**Класс концентратора на сервере**</span><span class="sxs-lookup"><span data-stu-id="df6de-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="df6de-212">**Создание клиентского прокси для класса концентратора**</span><span class="sxs-lookup"><span data-stu-id="df6de-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="df6de-213">Если вы украсите `HubName` свой класс концентратора атрибутом, используйте это имя.</span><span class="sxs-lookup"><span data-stu-id="df6de-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="df6de-214">**Класс концентратора на сервере**</span><span class="sxs-lookup"><span data-stu-id="df6de-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="df6de-215">**Создание клиентского прокси для класса концентратора**</span><span class="sxs-lookup"><span data-stu-id="df6de-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="df6de-216">Если вы `HubConnection.CreateHubProxy` звоните несколько раз с тем же, `hubName`вы получите тот же кэшированный `IHubProxy` объект.</span><span class="sxs-lookup"><span data-stu-id="df6de-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="df6de-217">Как определить методы на клиенте, который может вызвать сервер</span><span class="sxs-lookup"><span data-stu-id="df6de-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="df6de-218">Чтобы определить метод, который может вызвать сервер, используйте `On` метод прокси для регистрации обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="df6de-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="df6de-219">Сопоставление имен метода является нечувствительным.</span><span class="sxs-lookup"><span data-stu-id="df6de-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="df6de-220">Например, `Clients.All.UpdateStockPrice` на сервере `updateStockPrice` `updatestockprice`будет `UpdateStockPrice` выполняться, или на клиенте.</span><span class="sxs-lookup"><span data-stu-id="df6de-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="df6de-221">Различные клиентские платформы имеют различные требования к тому, как вы пишете код метода для обновления пользовательского доступа.</span><span class="sxs-lookup"><span data-stu-id="df6de-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="df6de-222">Приведенные примеры для клиентов WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="df6de-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="df6de-223">Примеры WPF, Silverlight и консольных приложений приведены в [отдельном разделе позже в этой теме.](#wpfsl)</span><span class="sxs-lookup"><span data-stu-id="df6de-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="df6de-224">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-224">Methods without parameters</span></span>

<span data-ttu-id="df6de-225">Если метод, с помощью которой вы работаете, не имеет `On` параметров, используйте неродовую перегрузку метода:</span><span class="sxs-lookup"><span data-stu-id="df6de-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="df6de-226">**Серверный код вызова методклиента без параметров**</span><span class="sxs-lookup"><span data-stu-id="df6de-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="df6de-227">**Код клиента WinRT для метода, вызываемого с сервера без параметров[(см. примеры WPF и Silverlight позже в этой теме)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="df6de-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="df6de-228">Методы с параметрами, определяющие типы параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="df6de-229">Если метод, с которой вы обрабатываете, имеет параметры, укажите типы параметров как общие типы метода. `On`</span><span class="sxs-lookup"><span data-stu-id="df6de-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="df6de-230">Существуют общие перегрузки `On` метода, позволяющие указывать до 8 параметров (4 на Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="df6de-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="df6de-231">В следующем примере один параметр `UpdateStockPrice` отправляется в метод.</span><span class="sxs-lookup"><span data-stu-id="df6de-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="df6de-232">**Серверный код вызова метода клиента с параметром**</span><span class="sxs-lookup"><span data-stu-id="df6de-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="df6de-233">**Класс stock, используемый для параметра**</span><span class="sxs-lookup"><span data-stu-id="df6de-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="df6de-234">**Код клиента WinRT для метода, вызванного с сервера с параметром[(см. примеры WPF и Silverlight позже в этой теме)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="df6de-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="df6de-235">Методы с параметрами, определяющие динамические объекты для параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="df6de-236">В качестве альтернативы определению параметров в `On` качестве общих типов метода можно указать параметры как динамические объекты:</span><span class="sxs-lookup"><span data-stu-id="df6de-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="df6de-237">**Серверный код вызова метода клиента с параметром**</span><span class="sxs-lookup"><span data-stu-id="df6de-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="df6de-238">**Класс stock, используемый для параметра**</span><span class="sxs-lookup"><span data-stu-id="df6de-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="df6de-239">**Код Клиента WinRT для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра[(см. примеры WPF и Silverlight позже в этой теме)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="df6de-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="df6de-240">Как удалить обработчик</span><span class="sxs-lookup"><span data-stu-id="df6de-240">How to remove a handler</span></span>

<span data-ttu-id="df6de-241">Чтобы удалить обработчик, позвоните его `Dispose` методу.</span><span class="sxs-lookup"><span data-stu-id="df6de-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="df6de-242">**Клиентский код для метода, вызванного с сервера**</span><span class="sxs-lookup"><span data-stu-id="df6de-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="df6de-243">**Код клиента для удаления обработчика**</span><span class="sxs-lookup"><span data-stu-id="df6de-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="df6de-244">Как вызвать методы сервера от клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-244">How to call server methods from the client</span></span>

<span data-ttu-id="df6de-245">Чтобы вызвать метод на сервере, используйте `Invoke` метод на прокси-сервере концентратора.</span><span class="sxs-lookup"><span data-stu-id="df6de-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="df6de-246">Если метод сервера не имеет значения возврата, используйте `Invoke` негенерическую перегрузку метода.</span><span class="sxs-lookup"><span data-stu-id="df6de-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="df6de-247">**Код сервера для метода, не имевавого значения возврата**</span><span class="sxs-lookup"><span data-stu-id="df6de-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="df6de-248">**Код клиента вызова метода, который не имеет значения возврата**</span><span class="sxs-lookup"><span data-stu-id="df6de-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="df6de-249">Если метод сервера имеет значение возврата, укажите тип `Invoke` возврата как общий тип метода.</span><span class="sxs-lookup"><span data-stu-id="df6de-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="df6de-250">**Код сервера для метода, который имеет значение возврата и использует сложный параметр типа**</span><span class="sxs-lookup"><span data-stu-id="df6de-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="df6de-251">**Класс stock, используемый для значения параметра и возврата**</span><span class="sxs-lookup"><span data-stu-id="df6de-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="df6de-252">**Клиентский код вызова метода, который имеет значение возврата и принимает сложный параметр типа, в ASP.NET методе 4.5 async**</span><span class="sxs-lookup"><span data-stu-id="df6de-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="df6de-253">**Клиентский код вызова метода, который имеет значение возврата и принимает сложный параметр типа, в синхронном методе**</span><span class="sxs-lookup"><span data-stu-id="df6de-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="df6de-254">Метод `Invoke` выполняет асинхронно и `Task` возвращает объект.</span><span class="sxs-lookup"><span data-stu-id="df6de-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="df6de-255">Если вы не `await` указали или, `.Wait()`следующая строка кода будет выполняться до метода, который вы ссылаетесь закончил выполнение.</span><span class="sxs-lookup"><span data-stu-id="df6de-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="df6de-256">Как обрабатывать события жизни соединения</span><span class="sxs-lookup"><span data-stu-id="df6de-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="df6de-257">SignalR предоставляет следующие события жизни соединения, которые вы можете обрабатывать:</span><span class="sxs-lookup"><span data-stu-id="df6de-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="df6de-258">`Received`: Поднятыпри получать какие-либо данные о подключении.</span><span class="sxs-lookup"><span data-stu-id="df6de-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="df6de-259">Предоставляет полученные данные.</span><span class="sxs-lookup"><span data-stu-id="df6de-259">Provides the received data.</span></span>
- <span data-ttu-id="df6de-260">`ConnectionSlow`: Поднят, когда клиент обнаруживает медленное или часто падающее соединение.</span><span class="sxs-lookup"><span data-stu-id="df6de-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="df6de-261">`Reconnecting`: Поднятый, когда базовый транспорт начинает воссоединение.</span><span class="sxs-lookup"><span data-stu-id="df6de-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="df6de-262">`Reconnected`: Поднятый при повторном подключении основного транспорта.</span><span class="sxs-lookup"><span data-stu-id="df6de-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="df6de-263">`StateChanged`: Поднят при изменении состояния соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="df6de-264">Обеспечивает старое состояние и новое состояние.</span><span class="sxs-lookup"><span data-stu-id="df6de-264">Provides the old state and the new state.</span></span> <span data-ttu-id="df6de-265">Для получения информации о [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)значениях состояния соединения см.</span><span class="sxs-lookup"><span data-stu-id="df6de-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="df6de-266">`Closed`: Поднят освоено при отключении соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="df6de-267">Например, если вы хотите отобразить предупреждающие сообщения об ошибках, которые не являются фатальными, но `ConnectionSlow` вызывают периодические проблемы с подключением, такие как медлительность или частое падение соединения, справьтесь с событием.</span><span class="sxs-lookup"><span data-stu-id="df6de-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="df6de-268">Для получения дополнительной информации, см [Понимание и обработка подключения Пожизненные события в SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="df6de-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="df6de-269">Как обрабатывать ошибки</span><span class="sxs-lookup"><span data-stu-id="df6de-269">How to handle errors</span></span>

<span data-ttu-id="df6de-270">Если вы явно не включаете подробные сообщения об ошибке на сервере, объект исключения, который возвращает SignalR после ошибки, содержит минимальную информацию об ошибке.</span><span class="sxs-lookup"><span data-stu-id="df6de-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="df6de-271">Например, если вызов `newContosoChatMessage` не удается, сообщение об`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`ошибке в объекте ошибки содержит " Отправка подробных сообщений об ошибках клиентам в производственной сфере не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.</span><span class="sxs-lookup"><span data-stu-id="df6de-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="df6de-272">Для обработки ошибок, которые вызывает SignalR, можно добавить обработчик `Error` для события на объекте соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="df6de-273">Для обработки ошибок из вызовов метода заверните код в блок try-catch.</span><span class="sxs-lookup"><span data-stu-id="df6de-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="df6de-274">Как включить журналирование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="df6de-274">How to enable client-side logging</span></span>

<span data-ttu-id="df6de-275">Чтобы включить журнал в сторону клиента, установите `TraceLevel` и `TraceWriter` свойства на объект соединения.</span><span class="sxs-lookup"><span data-stu-id="df6de-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="df6de-276">Образцы кода приложений WPF, Silverlight и консольных приложений для методов клиента, которые сервер может вызвать</span><span class="sxs-lookup"><span data-stu-id="df6de-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="df6de-277">Образцы кода, показанные ранее для определения методов клиента, которые сервер может вызвать, применимы к клиентам WinRT.</span><span class="sxs-lookup"><span data-stu-id="df6de-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="df6de-278">Следующие примеры показывают эквивалентный код для клиентов WPF, Silverlight и консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="df6de-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="df6de-279">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-279">Methods without parameters</span></span>

<span data-ttu-id="df6de-280">**Клиентский код WPF для метода, вызываемого с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="df6de-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="df6de-281">**Клиентский код Silverlight для метода, вызываемого с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="df6de-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="df6de-282">**Консольный клиентский код приложения для метода, вызываемого с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="df6de-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="df6de-283">Методы с параметрами, определяющие типы параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="df6de-284">**Клиентский код WPF для метода, вызванного с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="df6de-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="df6de-285">**Клиентский код Silverlight для метода, вызванного с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="df6de-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="df6de-286">**Консольный клиентский код приложения для метода, вызванного с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="df6de-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="df6de-287">Методы с параметрами, определяющие динамические объекты для параметров</span><span class="sxs-lookup"><span data-stu-id="df6de-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="df6de-288">**Клиентский код WPF для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="df6de-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="df6de-289">**Клиентский код Silverlight для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="df6de-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="df6de-290">**Консольный клиентский код приложения для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="df6de-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
