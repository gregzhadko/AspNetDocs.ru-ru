---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET руководство aPI концентратов SignalR - Сервер (C) Документы Майкрософт
author: bradygaster
description: Этот документ содержит введение в программирование серверной стороны ASP.NET SignalR Концентраты API для SignalR версии 2, с образцами кода, демонстрирующими...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675805"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="48a0c-103">ASP.NET руководство aPI концентратов SignalR - Сервер (C)</span><span class="sxs-lookup"><span data-stu-id="48a0c-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="48a0c-104">[Патрик Флетчер](https://github.com/pfletcher), [Том Дикстра](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="48a0c-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="48a0c-105">Этот документ содержит введение в программирование серверной стороны ASP.NET SignalR Концентраты API для SignalR версии 2, с образцами кода, демонстрирующими общие варианты.</span><span class="sxs-lookup"><span data-stu-id="48a0c-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="48a0c-106">API Концентраторов SignalR позволяет совершать удаленные процедурные звонки (RPCs) с сервера для подключенных клиентов и от клиентов к серверу.</span><span class="sxs-lookup"><span data-stu-id="48a0c-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="48a0c-107">В коде сервера вы определяете методы, которые могут вызываться клиентами, и вызываете методы, которые работают на клиенте.</span><span class="sxs-lookup"><span data-stu-id="48a0c-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="48a0c-108">В клиентском коде вы определяете методы, которые можно вызывать с сервера, и вызываете методы, которые работают на сервере.</span><span class="sxs-lookup"><span data-stu-id="48a0c-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="48a0c-109">SignalR заботится о всех клиента к серверу сантехника для вас.</span><span class="sxs-lookup"><span data-stu-id="48a0c-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="48a0c-110">SignalR также предлагает API более низкого уровня под названием Persistent Connections.</span><span class="sxs-lookup"><span data-stu-id="48a0c-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="48a0c-111">Для введения в SignalR, концентраторы, и стойкие соединения, [см.](../getting-started/introduction-to-signalr.md)</span><span class="sxs-lookup"><span data-stu-id="48a0c-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="48a0c-112">Версии программного обеспечения, используемые в этой теме</span><span class="sxs-lookup"><span data-stu-id="48a0c-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="48a0c-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="48a0c-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="48a0c-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="48a0c-114">.NET 4.5</span></span>
> - <span data-ttu-id="48a0c-115">Версия SignalR 2</span><span class="sxs-lookup"><span data-stu-id="48a0c-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="48a0c-116">Версии тем</span><span class="sxs-lookup"><span data-stu-id="48a0c-116">Topic versions</span></span>
> 
> <span data-ttu-id="48a0c-117">Для получения информации о более ранних версиях SignalR, см [SignalR Старые версии](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="48a0c-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="48a0c-118">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="48a0c-118">Questions and comments</span></span>
> 
> <span data-ttu-id="48a0c-119">Пожалуйста, оставьте обратную связь о том, как вам понравился этот учебник и что мы могли бы улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="48a0c-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="48a0c-120">Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com.](http://stackoverflow.com/)</span><span class="sxs-lookup"><span data-stu-id="48a0c-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="48a0c-121">Обзор</span><span class="sxs-lookup"><span data-stu-id="48a0c-121">Overview</span></span>

<span data-ttu-id="48a0c-122">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="48a0c-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="48a0c-123">Как зарегистрировать промежуточное программное обеспечение SignalR</span><span class="sxs-lookup"><span data-stu-id="48a0c-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="48a0c-124">URL/сигнальщик</span><span class="sxs-lookup"><span data-stu-id="48a0c-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="48a0c-125">Настройка параметров SignalR</span><span class="sxs-lookup"><span data-stu-id="48a0c-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="48a0c-126">Как создавать и использовать классы концентраторов</span><span class="sxs-lookup"><span data-stu-id="48a0c-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="48a0c-127">Срок службы объекта концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="48a0c-128">Верблюжья оболочка имен концентраторов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="48a0c-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="48a0c-129">Несколько концентратов</span><span class="sxs-lookup"><span data-stu-id="48a0c-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="48a0c-130">Сильно набранные концентраторы</span><span class="sxs-lookup"><span data-stu-id="48a0c-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="48a0c-131">Как определить методы в классе концентратора, которые клиенты могут вызвать</span><span class="sxs-lookup"><span data-stu-id="48a0c-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="48a0c-132">Верблюжья оболочка имен методов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="48a0c-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="48a0c-133">Когда выполнять асинхронно</span><span class="sxs-lookup"><span data-stu-id="48a0c-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="48a0c-134">Определение перегрузок</span><span class="sxs-lookup"><span data-stu-id="48a0c-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="48a0c-135">Отчетность о прогрессе от вызовов метода концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="48a0c-136">Как вызвать методы клиента из класса концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="48a0c-137">Выбор клиентов, которые получат RPC</span><span class="sxs-lookup"><span data-stu-id="48a0c-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="48a0c-138">Отсутствие проверки времени компиляции для имен методов</span><span class="sxs-lookup"><span data-stu-id="48a0c-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="48a0c-139">Соответствие имени нечувствительных методов для дел</span><span class="sxs-lookup"><span data-stu-id="48a0c-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="48a0c-140">Асинхронное исполнение</span><span class="sxs-lookup"><span data-stu-id="48a0c-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="48a0c-141">Как управлять членством в группе из класса концентратор</span><span class="sxs-lookup"><span data-stu-id="48a0c-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="48a0c-142">Асинхронное выполнение методов добавления и удаления</span><span class="sxs-lookup"><span data-stu-id="48a0c-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="48a0c-143">Сохранение членства в группе</span><span class="sxs-lookup"><span data-stu-id="48a0c-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="48a0c-144">Группы для пользователей</span><span class="sxs-lookup"><span data-stu-id="48a0c-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="48a0c-145">Как обрабатывать события жизни соединения в классе концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="48a0c-146">При вызове OnConnected, OnDisconnected и OnReconnected</span><span class="sxs-lookup"><span data-stu-id="48a0c-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="48a0c-147">Состояние вызываемого абонента не заселены</span><span class="sxs-lookup"><span data-stu-id="48a0c-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="48a0c-148">Как получить информацию о клиенте из свойства Контекста</span><span class="sxs-lookup"><span data-stu-id="48a0c-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="48a0c-149">Как передать состояние между клиентами и классом концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="48a0c-150">Как обрабатывать ошибки в классе концентратор</span><span class="sxs-lookup"><span data-stu-id="48a0c-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="48a0c-151">Как вызвать методы клиентов и управлять группами из-за пределов класса концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="48a0c-152">Вызов методов клиента</span><span class="sxs-lookup"><span data-stu-id="48a0c-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="48a0c-153">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="48a0c-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="48a0c-154">Как включить трассировку</span><span class="sxs-lookup"><span data-stu-id="48a0c-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="48a0c-155">Как настроить конвейер концентров</span><span class="sxs-lookup"><span data-stu-id="48a0c-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="48a0c-156">Для получения документации о том, как программировать клиентов, см.</span><span class="sxs-lookup"><span data-stu-id="48a0c-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="48a0c-157">Руководство По API Концентратов SignalR - Клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="48a0c-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="48a0c-158">Руководство По API Концентраторов SignalR - Клиент .NET</span><span class="sxs-lookup"><span data-stu-id="48a0c-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="48a0c-159">Компоненты сервера для SignalR 2 доступны только в .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="48a0c-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="48a0c-160">Серверы под управлением .NET 4.0 должны использовать SignalR v1.x.</span><span class="sxs-lookup"><span data-stu-id="48a0c-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="48a0c-161">Как зарегистрировать промежуточное программное обеспечение SignalR</span><span class="sxs-lookup"><span data-stu-id="48a0c-161">How to register SignalR middleware</span></span>

<span data-ttu-id="48a0c-162">Чтобы определить маршрут, который клиенты будут использовать `MapSignalR` для подключения к концентратору, позвоните в метод, когда приложение начинает сятворное.</span><span class="sxs-lookup"><span data-stu-id="48a0c-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="48a0c-163">`MapSignalR`— [это метод](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` расширения для класса.</span><span class="sxs-lookup"><span data-stu-id="48a0c-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="48a0c-164">Ниже приводится следующий пример, как определить маршрут концентраторов SignalR с помощью класса запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="48a0c-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="48a0c-165">Если вы добавляете функциональность SignalR в ASP.NET приложение MVC, убедитесь, что маршрут SignalR добавляется перед другими маршрутами.</span><span class="sxs-lookup"><span data-stu-id="48a0c-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="48a0c-166">Для получения дополнительной информации [см.](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)</span><span class="sxs-lookup"><span data-stu-id="48a0c-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="48a0c-167">URL/сигнальщик</span><span class="sxs-lookup"><span data-stu-id="48a0c-167">The /signalr URL</span></span>

<span data-ttu-id="48a0c-168">По умолчанию URL-адрес маршрута, который клиенты будут использовать для подключения к концентратору, является "/сигнальным".</span><span class="sxs-lookup"><span data-stu-id="48a0c-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="48a0c-169">(Не путайте этот URL с URL-адресом "/signalr/hubs", который предназначен для автоматического генерируемого файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="48a0c-170">Для получения дополнительной информации о сгенерированном прокси-сервере см. Руководство [SignalR Hubs API - JavaScript Client - Сгенерированный прокси и что он делает для вас.)](hubs-api-guide-javascript-client.md#genproxy)</span><span class="sxs-lookup"><span data-stu-id="48a0c-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="48a0c-171">Там могут быть чрезвычайные обстоятельства, которые делают этот базовый URL не приговочен к удобосона для SignalR; например, у вас есть папка в проекте под названием *сигнальный сигнализатор,* и вы не хотите менять имя.</span><span class="sxs-lookup"><span data-stu-id="48a0c-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="48a0c-172">В этом случае можно изменить базовый URL, как показано в следующих примерах (заменить "/сигнализатор" в коде образца нужным URL).</span><span class="sxs-lookup"><span data-stu-id="48a0c-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="48a0c-173">**Код сервера, который определяет URL**</span><span class="sxs-lookup"><span data-stu-id="48a0c-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="48a0c-174">**Клиентский код JavaScript, который определяет URL (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="48a0c-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="48a0c-175">**Клиентский код JavaScript, который определяет URL (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="48a0c-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="48a0c-176">**клиентский код .NET, который определяет URL**</span><span class="sxs-lookup"><span data-stu-id="48a0c-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="48a0c-177">Настройка параметров SignalR</span><span class="sxs-lookup"><span data-stu-id="48a0c-177">Configuring SignalR Options</span></span>

<span data-ttu-id="48a0c-178">Перегрузки `MapSignalR` метода позволяют указать пользовательский URL-адрес, разрешитель пользовательских зависимостей и следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="48a0c-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="48a0c-179">Включите кросс-домен ныевызови с помощью CORS или JSONP от клиентов браузера.</span><span class="sxs-lookup"><span data-stu-id="48a0c-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="48a0c-180">Обычно, если браузер загружает страницу с `http://contoso.com`, соединение `http://contoso.com/signalr`SignalR находится в том же домене, в .</span><span class="sxs-lookup"><span data-stu-id="48a0c-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="48a0c-181">Если страница `http://contoso.com` из делает `http://fabrikam.com/signalr`подключение к, то есть кросс-домен соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="48a0c-182">По соображениям безопасности соединения кросс-домена отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="48a0c-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="48a0c-183">Для получения дополнительной информации смотрите [ASP.NET Руководство API Концентраторки SignalR - JavaScript Клиент - Как установить кросс-домен соединение](hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="48a0c-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="48a0c-184">Включить подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="48a0c-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="48a0c-185">При возникновении ошибок поведение SignalR по умолчанию заключается в отправке клиентам уведомления без подробной информации о том, что произошло.</span><span class="sxs-lookup"><span data-stu-id="48a0c-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="48a0c-186">Отправка подробной информации об ошибках клиентам не рекомендуется в производстве, так как вредоносные пользователи могут использовать эту информацию при атаках на ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="48a0c-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="48a0c-187">Для устранения неполадок можно использовать эту опцию для временного включения более информативной отчетности об ошибках.</span><span class="sxs-lookup"><span data-stu-id="48a0c-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="48a0c-188">Отключить автоматически генерируемые прокси-файлы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="48a0c-189">По умолчанию файл JavaScript с прокси-файлами для классов концентратора генерируется в ответ на URL "/сигнальщик/концентратор".</span><span class="sxs-lookup"><span data-stu-id="48a0c-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="48a0c-190">Если вы не хотите использовать прокси JavaScript, или если вы хотите создать этот файл вручную и обратиться к физическому файлу в ваших клиентах, вы можете использовать эту опцию, чтобы отключить генерацию прокси.</span><span class="sxs-lookup"><span data-stu-id="48a0c-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="48a0c-191">Для получения дополнительной информации см. [Руководство SignalR Hubs API - JavaScript Client - Как создать физический файл для прокси-сервера SignalR.](hubs-api-guide-javascript-client.md#manualproxy)</span><span class="sxs-lookup"><span data-stu-id="48a0c-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="48a0c-192">В следующем примере показано, как указать URL-адрес соединения `MapSignalR` SignalR и эти параметры в вызове к методу.</span><span class="sxs-lookup"><span data-stu-id="48a0c-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="48a0c-193">Чтобы указать пользовательский URL, замените "/сигнализатор" в примере URL-адресом, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="48a0c-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="48a0c-194">Как создавать и использовать классы концентраторов</span><span class="sxs-lookup"><span data-stu-id="48a0c-194">How to create and use Hub classes</span></span>

<span data-ttu-id="48a0c-195">Чтобы создать концентратор, создайте класс, который происходит от [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="48a0c-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="48a0c-196">Ниже приводится простой класс концентратора для приложения чата.</span><span class="sxs-lookup"><span data-stu-id="48a0c-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="48a0c-197">В этом примере подключенный `NewContosoChatMessage` клиент может вызвать метод, и когда он это делает, полученные данные передаются всем подключенным клиентам.</span><span class="sxs-lookup"><span data-stu-id="48a0c-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="48a0c-198">Срок службы объекта концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-198">Hub object lifetime</span></span>

<span data-ttu-id="48a0c-199">Вы не вызываете класс концентратора и не вызываете его методы из собственного кода на сервере; все, что делается для вас конвейером Концентраторов SignalR.</span><span class="sxs-lookup"><span data-stu-id="48a0c-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="48a0c-200">SignalR создает новый экземпляр класса концентратора каждый раз, когда ему необходимо обрабатывать операцию концентратора, например, когда клиент подключается, отключается или делает вызов метода на сервер.</span><span class="sxs-lookup"><span data-stu-id="48a0c-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="48a0c-201">Поскольку экземпляры класса концентратора являются временными, их нельзя использовать для поддержания состояния от одного вызова метода к другому.</span><span class="sxs-lookup"><span data-stu-id="48a0c-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="48a0c-202">Каждый раз, когда сервер получает вызов метода от клиента, новый экземпляр класса концентратора обрабатывает сообщение.</span><span class="sxs-lookup"><span data-stu-id="48a0c-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="48a0c-203">Для поддержания состояния через несколько вызовов соединений и методов используйте некоторый другой метод, такой `Hub`как база данных, или статическая переменная на классе концентратора, или другой класс, который не вытекает из.</span><span class="sxs-lookup"><span data-stu-id="48a0c-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="48a0c-204">Если вы сохраняете данные в памяти, используя такой метод, как статическая переменная в классе концентратора, данные будут потеряны при переработке домена приложения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="48a0c-205">Если вы хотите отправлять сообщения клиентам из собственного кода, который работает за пределами класса концентратора, вы не можете сделать это, мгновенно экземпляр класса концентратор, но вы можете сделать это, получив ссылку на контекстный объект SignalR для вашего класса концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="48a0c-206">Для получения дополнительной информации смотрите [Как вызвать методы клиента и управлять группами из-за пределов класса концентратора](#callfromoutsidehub) позже в этой теме.</span><span class="sxs-lookup"><span data-stu-id="48a0c-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="48a0c-207">Верблюжья оболочка имен концентраторов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="48a0c-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="48a0c-208">По умолчанию клиенты JavaScript ссылаются на концентраторы, используя верблюжью версию имени класса.</span><span class="sxs-lookup"><span data-stu-id="48a0c-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="48a0c-209">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать конвенциям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="48a0c-210">Предыдущий пример будет отсутстать в `contosoChatHub` коде JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="48a0c-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="48a0c-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="48a0c-212">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="48a0c-213">Если требуется указать другое имя для `HubName` клиентов, добавьте атрибут.</span><span class="sxs-lookup"><span data-stu-id="48a0c-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="48a0c-214">При использовании `HubName` атрибута имя не изменяется для случаес верблюда на клиентах JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="48a0c-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="48a0c-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="48a0c-216">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="48a0c-217">Несколько концентратов</span><span class="sxs-lookup"><span data-stu-id="48a0c-217">Multiple Hubs</span></span>

<span data-ttu-id="48a0c-218">Можно определить несколько классов концентраторов в приложении.</span><span class="sxs-lookup"><span data-stu-id="48a0c-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="48a0c-219">При этом соединение является общим, но группы разделены:</span><span class="sxs-lookup"><span data-stu-id="48a0c-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="48a0c-220">Все клиенты будут использовать один и тот же URL для установления соединения SignalR с вашим сервисом ("/сигнализатор" или пользовательский URL, если вы указали один), и это соединение используется для всех концентраторов, определенных службой.</span><span class="sxs-lookup"><span data-stu-id="48a0c-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="48a0c-221">Для нескольких концентратов разница в производительности не существует по сравнению с определением всех функциональных возможностей концентратора в одном классе.</span><span class="sxs-lookup"><span data-stu-id="48a0c-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="48a0c-222">Все концентраторы получают одинаковую информацию о запросе HTTP.</span><span class="sxs-lookup"><span data-stu-id="48a0c-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="48a0c-223">Поскольку все концентраторы имеют одно и то же соединение, единственная информация о запросе HTTP, которую получает сервер, это то, что входит в исходный запрос HTTP, который устанавливает соединение SignalR.</span><span class="sxs-lookup"><span data-stu-id="48a0c-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="48a0c-224">Если вы используете запрос на подключение для передачи информации от клиента серверу, указывая строку запроса, вы не можете предоставить различные строки запроса для различных концентраторов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="48a0c-225">Все концентраторы получат одну и ту же информацию.</span><span class="sxs-lookup"><span data-stu-id="48a0c-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="48a0c-226">Сгенерированный файл прокси JavaScript будет содержать прокси для всех концентраторов в одном файле.</span><span class="sxs-lookup"><span data-stu-id="48a0c-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="48a0c-227">Для получения информации о прокси JavaScript, см [SignalR концентраторов API Руководство - JavaScript Клиент - Сгенерированный прокси и что он делает для вас](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="48a0c-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="48a0c-228">Группы определяются в концентрах.</span><span class="sxs-lookup"><span data-stu-id="48a0c-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="48a0c-229">В SignalR вы можете определить группы именованных для трансляции подмножества подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="48a0c-230">Группы поддерживаются отдельно для каждого концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="48a0c-231">Например, группа под названием "Администраторы" будет `ContosoChatHub` включать в себя один набор клиентов для вашего `StockTickerHub` класса, и одно и то же имя группы будет относиться к другому набору клиентов для вашего класса.</span><span class="sxs-lookup"><span data-stu-id="48a0c-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="48a0c-232">Сильно набранные концентраторы</span><span class="sxs-lookup"><span data-stu-id="48a0c-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="48a0c-233">Чтобы определить интерфейс для методов концентратора, на которые клиент может ссылаться (и `Hub<T>` включить Intellisense на методах концентратора), вывемите концентратор из (введенного в SignalR 2.1), а `Hub`не:</span><span class="sxs-lookup"><span data-stu-id="48a0c-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="48a0c-234">Как определить методы в классе концентратора, которые клиенты могут вызвать</span><span class="sxs-lookup"><span data-stu-id="48a0c-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="48a0c-235">Чтобы разоблачить метод в концентраторе, который вы хотите быть callable от клиента, объявить общедоступный метод, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="48a0c-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="48a0c-236">Можно указать тип возврата и параметры, включая сложные типы и массивы, как в любом методе C.</span><span class="sxs-lookup"><span data-stu-id="48a0c-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="48a0c-237">Любые данные, которые вы получаете по параметрам или возвращаетесь к вызывающему абоненту, передаются между клиентом и сервером с помощью JSON, а SignalR автоматически обрабатывает привязку сложных объектов и массивов объектов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="48a0c-238">Верблюжья оболочка имен методов в клиентах JavaScript</span><span class="sxs-lookup"><span data-stu-id="48a0c-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="48a0c-239">По умолчанию клиенты JavaScript ссылаются на методы концентратора, используя верблюжью версию имени метода.</span><span class="sxs-lookup"><span data-stu-id="48a0c-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="48a0c-240">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать конвенциям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="48a0c-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="48a0c-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="48a0c-242">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="48a0c-243">Если требуется указать другое имя для `HubMethodName` клиентов, добавьте атрибут.</span><span class="sxs-lookup"><span data-stu-id="48a0c-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="48a0c-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="48a0c-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="48a0c-245">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="48a0c-246">Когда выполнять асинхронно</span><span class="sxs-lookup"><span data-stu-id="48a0c-246">When to execute asynchronously</span></span>

<span data-ttu-id="48a0c-247">Если метод будет длительным или должен выполнять работу, которая предполагает ожидание, например, поиск базы данных или вызов веб-службы, `void` сделайте метод концентратора асинхронным, вернув [задачу](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (вместо возврата) или объект [Task&lt;&gt; T](https://msdn.microsoft.com/library/dd321424.aspx) (вместо типа `T` возврата).</span><span class="sxs-lookup"><span data-stu-id="48a0c-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="48a0c-248">При возвращении `Task` объекта из метода SignalR `Task` ждет завершения, а затем отправляет необернутый результат клиенту, поэтому нет никакой разницы в том, как кодировать вызов метода в клиенте.</span><span class="sxs-lookup"><span data-stu-id="48a0c-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="48a0c-249">Создание асинхронного метода концентратора позволяет избежать блокировки соединения при использовании транспорта WebSocket.</span><span class="sxs-lookup"><span data-stu-id="48a0c-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="48a0c-250">Когда метод концентратора выполняется синхронно, а перенос — WebSocket, последующие вызовы методов на концентраторе из одного и того же клиента блокируются до завершения метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="48a0c-251">В следующем примере показан тот же метод, закодированный для синхронного или асинхронного запуска, за которым следует клиентский код JavaScript, который работает для вызова любой из версий.</span><span class="sxs-lookup"><span data-stu-id="48a0c-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="48a0c-252">**Синхронный**</span><span class="sxs-lookup"><span data-stu-id="48a0c-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="48a0c-253">**Асинхронных**</span><span class="sxs-lookup"><span data-stu-id="48a0c-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="48a0c-254">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="48a0c-255">Для получения дополнительной информации о том, как использовать асинхронные методы в ASP.NET 4.5, см [ASP.NET.](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)</span><span class="sxs-lookup"><span data-stu-id="48a0c-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="48a0c-256">Определение перегрузок</span><span class="sxs-lookup"><span data-stu-id="48a0c-256">Defining Overloads</span></span>

<span data-ttu-id="48a0c-257">Если вы хотите определить перегрузки для метода, количество параметров в каждой перегрузке должно быть разным.</span><span class="sxs-lookup"><span data-stu-id="48a0c-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="48a0c-258">Если вы дифференцируете перегрузку, просто указав различные типы параметров, ваш класс концентратора будет компилироваться, но служба SignalR будет забрасывать исключение во время выполнения, когда клиенты пытаются вызвать одну из перегрузок.</span><span class="sxs-lookup"><span data-stu-id="48a0c-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="48a0c-259">Отчетность о прогрессе от вызовов метода концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="48a0c-260">SignalR 2.1 добавляет поддержку [модели представления о ходе работы,](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) введенной в .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="48a0c-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="48a0c-261">Для реализации отчетов `IProgress<T>` о ходе работы определите параметр для метода концентратора, к который клиент может получить доступ:</span><span class="sxs-lookup"><span data-stu-id="48a0c-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="48a0c-262">При написании длительного метода сервера важно использовать асинхронный шаблон программирования, такой как Async/Await, а не блокировать поток концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="48a0c-263">Как вызвать методы клиента из класса концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="48a0c-264">Чтобы вызвать методы клиента с `Clients` сервера, используйте свойство в методе в классе концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="48a0c-265">В следующем примере показан `addNewMessageToPage` серверный код, который вызывает всех подключенных клиентов, и клиентский код, определяющий метод в клиенте JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48a0c-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="48a0c-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="48a0c-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="48a0c-267">Ссылаясь на метод клиента является асинхронной `Task`операцией и возвращает .</span><span class="sxs-lookup"><span data-stu-id="48a0c-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="48a0c-268">Используйте `await` в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="48a0c-268">Use `await`:</span></span>

* <span data-ttu-id="48a0c-269">Чтобы убедиться, что сообщение отправлено без ошибочной ошибки.</span><span class="sxs-lookup"><span data-stu-id="48a0c-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="48a0c-270">Включить ошибки в ловле и обработке ошибок в блоке try-catch.</span><span class="sxs-lookup"><span data-stu-id="48a0c-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="48a0c-271">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="48a0c-272">Вы не можете получить значение возврата от метода клиента; синтаксис, `int x = Clients.All.add(1,1)` такой как не работает.</span><span class="sxs-lookup"><span data-stu-id="48a0c-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="48a0c-273">Можно указать сложные типы и массивы для параметров.</span><span class="sxs-lookup"><span data-stu-id="48a0c-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="48a0c-274">Следующий пример передает сложный тип клиенту в параметре метода.</span><span class="sxs-lookup"><span data-stu-id="48a0c-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="48a0c-275">**Код сервера, который вызывает метод клиента с помощью сложного объекта**</span><span class="sxs-lookup"><span data-stu-id="48a0c-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="48a0c-276">**Код сервера, определяющий сложный объект**</span><span class="sxs-lookup"><span data-stu-id="48a0c-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="48a0c-277">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="48a0c-278">Выбор клиентов, которые получат RPC</span><span class="sxs-lookup"><span data-stu-id="48a0c-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="48a0c-279">Свойство Клиентов возвращает объект [HubConnectionContext,](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) который предоставляет несколько вариантов указания, какие клиенты получат RPC:</span><span class="sxs-lookup"><span data-stu-id="48a0c-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="48a0c-280">Все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="48a0c-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="48a0c-281">Только звоняющий клиент.</span><span class="sxs-lookup"><span data-stu-id="48a0c-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="48a0c-282">Все клиенты, кроме вызываемого клиента.</span><span class="sxs-lookup"><span data-stu-id="48a0c-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="48a0c-283">Конкретный клиент, идентифицированный по идентификатору соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="48a0c-284">Этот пример `addContosoChatMessageToPage` вызывает вызываемого клиента и `Clients.Caller`имеет такой же эффект как использование .</span><span class="sxs-lookup"><span data-stu-id="48a0c-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="48a0c-285">Все подключенные клиенты, за исключением указанных клиентов, идентифицируются по идентификатору подключения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="48a0c-286">Все подключенные клиенты в определенной группе.</span><span class="sxs-lookup"><span data-stu-id="48a0c-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="48a0c-287">Все подключенные клиенты в указанной группе, за исключением указанных клиентов, идентифицированных по идентификатору подключения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="48a0c-288">Все подключенные клиенты в указанной группе, кроме вызываемого клиента.</span><span class="sxs-lookup"><span data-stu-id="48a0c-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="48a0c-289">Конкретный пользователь, идентифицированный userId.</span><span class="sxs-lookup"><span data-stu-id="48a0c-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="48a0c-290">По умолчанию `IPrincipal.Identity.Name`это, но это может быть изменено путем [регистрации реализации IUserIdProvider с глобальным хостом.](mapping-users-to-connections.md#IUserIdProvider)</span><span class="sxs-lookup"><span data-stu-id="48a0c-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="48a0c-291">Все клиенты и группы в списке идентимативных идентипов связи.</span><span class="sxs-lookup"><span data-stu-id="48a0c-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="48a0c-292">Список групп.</span><span class="sxs-lookup"><span data-stu-id="48a0c-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="48a0c-293">Пользователь по имени.</span><span class="sxs-lookup"><span data-stu-id="48a0c-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="48a0c-294">Список имен пользователей (введен в SignalR 2.1).</span><span class="sxs-lookup"><span data-stu-id="48a0c-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="48a0c-295">Отсутствие проверки времени компиляции для имен методов</span><span class="sxs-lookup"><span data-stu-id="48a0c-295">No compile-time validation for method names</span></span>

<span data-ttu-id="48a0c-296">Имя метода, указанное, интерпретируется как динамический объект, что означает отсутствие IntelliSense или проверки времени компиляции для него.</span><span class="sxs-lookup"><span data-stu-id="48a0c-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="48a0c-297">Выражение оценивается во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="48a0c-298">Когда вызов метода выполняется, SignalR отправляет клиенту имя метода и значения параметров, и если у клиента есть метод, который соответствует имени, этот метод вызывается и значения параметра передаются ему.</span><span class="sxs-lookup"><span data-stu-id="48a0c-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="48a0c-299">Если на клиенте не найдено подходящего метода, ошибка не возникает.</span><span class="sxs-lookup"><span data-stu-id="48a0c-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="48a0c-300">Для получения информации о формате данных, которые SignalR передает клиенту за кулисами при вызове метода клиента, [см.](../getting-started/introduction-to-signalr.md)</span><span class="sxs-lookup"><span data-stu-id="48a0c-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="48a0c-301">Соответствие имени нечувствительных методов для дел</span><span class="sxs-lookup"><span data-stu-id="48a0c-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="48a0c-302">Сопоставление имен метода является нечувствительным.</span><span class="sxs-lookup"><span data-stu-id="48a0c-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="48a0c-303">Например, `Clients.All.addContosoChatMessageToPage` на сервере `AddContosoChatMessageToPage` `addcontosochatmessagetopage`будет `addContosoChatMessageToPage` выполняться, или на клиенте.</span><span class="sxs-lookup"><span data-stu-id="48a0c-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="48a0c-304">Асинхронное исполнение</span><span class="sxs-lookup"><span data-stu-id="48a0c-304">Asynchronous execution</span></span>

<span data-ttu-id="48a0c-305">Метод, который вы называете, выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="48a0c-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="48a0c-306">Любой код, который приходит после вызова метода клиенту, будет выполняться немедленно, не дожидаясь, пока SignalR закончит передачу данных клиентам, если только вы не укажете, что последующие строки кода должны ждать завершения метода.</span><span class="sxs-lookup"><span data-stu-id="48a0c-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="48a0c-307">Следующий пример кода показывает, как последовательно выполнять два метода клиента.</span><span class="sxs-lookup"><span data-stu-id="48a0c-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="48a0c-308">**Использование Await (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="48a0c-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="48a0c-309">Если вы `await` используете, чтобы ждать, пока клиент метод заканчивается до следующей строки кода выполняет, это не означает, что клиенты будут на самом деле получить сообщение до следующей строки кода выполняет.</span><span class="sxs-lookup"><span data-stu-id="48a0c-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="48a0c-310">"Завершение" вызова метода клиента означает только то, что SignalR сделал все необходимое для отправки сообщения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="48a0c-311">Если вам нужна проверка, что клиенты получили сообщение, вы должны запрограммировать этот механизм самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="48a0c-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="48a0c-312">Например, можно закодировать `MessageReceived` метод в концентраторе, а в `addContosoChatMessageToPage` методе клиента вы можете вызвать `MessageReceived` после того, как вы сделаете любую работу, которую вам нужно сделать для клиента.</span><span class="sxs-lookup"><span data-stu-id="48a0c-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="48a0c-313">В `MessageReceived` концентраторе вы можете выполнять любую работу, зависят от фактического приема клиента и обработки первоначального вызова метода.</span><span class="sxs-lookup"><span data-stu-id="48a0c-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="48a0c-314">Как использовать переменную строки в качестве имени метода</span><span class="sxs-lookup"><span data-stu-id="48a0c-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="48a0c-315">Если вы хотите вызвать метод клиента, используя строку переменной, `Clients.Others`как `Clients.Caller`имя метода, литые `Clients.All` (или , и т.д.), а `IClientProxy` затем вызвать вызов вызова [(методИг, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="48a0c-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="48a0c-316">Как управлять членством в группе из класса концентратор</span><span class="sxs-lookup"><span data-stu-id="48a0c-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="48a0c-317">Группы в SignalR предоставляют метод передачи сообщений указанным подмноещем подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="48a0c-318">Группа может иметь любое количество клиентов, а клиент может быть членом любого количества групп.</span><span class="sxs-lookup"><span data-stu-id="48a0c-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="48a0c-319">Для управления членством в группе используйте `Groups` методы [добавления](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) и [удаления,](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) предоставляемые свойством класса концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="48a0c-320">В следующем примере показаны `Groups.Add` `Groups.Remove` методы и методы, используемые в методах концентратора, которые называются кодом клиента, а затем клиентским кодом JavaScript, который их вызывает.</span><span class="sxs-lookup"><span data-stu-id="48a0c-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="48a0c-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="48a0c-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="48a0c-322">**Клиент JavaScript с помощью генерируемого прокси**</span><span class="sxs-lookup"><span data-stu-id="48a0c-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="48a0c-323">Не нужно явно создавать группы.</span><span class="sxs-lookup"><span data-stu-id="48a0c-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="48a0c-324">Фактически группа автоматически создается при первом удеворе `Groups.Add`в вызове, и она удаляется при удалении последнего соединения из членства в ней.</span><span class="sxs-lookup"><span data-stu-id="48a0c-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="48a0c-325">API не может получить список членов группы или список групп.</span><span class="sxs-lookup"><span data-stu-id="48a0c-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="48a0c-326">SignalR отправляет сообщения клиентам и группам на основе [модели паб/суб,](http://en.wikipedia.org/wiki/Publish/subscribe)а сервер не ведет списки групп или групп.</span><span class="sxs-lookup"><span data-stu-id="48a0c-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="48a0c-327">Это помогает максимизировать масштабируемость, потому что всякий раз, когда вы добавляете узел на веб-ферму, любое состояние, которое поддерживает SignalR, должно распространяться на новый узел.</span><span class="sxs-lookup"><span data-stu-id="48a0c-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="48a0c-328">Асинхронное выполнение методов добавления и удаления</span><span class="sxs-lookup"><span data-stu-id="48a0c-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="48a0c-329">И `Groups.Add` `Groups.Remove` методы выполняют асинхронно.</span><span class="sxs-lookup"><span data-stu-id="48a0c-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="48a0c-330">Если вы хотите добавить клиента в группу и немедленно отправить сообщение клиенту с помощью группы, вы должны убедиться, что `Groups.Add` метод заканчивается первым.</span><span class="sxs-lookup"><span data-stu-id="48a0c-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="48a0c-331">Следующий пример кода показывает, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="48a0c-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="48a0c-332">**Добавление клиента в группу, а затем обмен сообщениями с этим клиентом**</span><span class="sxs-lookup"><span data-stu-id="48a0c-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="48a0c-333">Сохранение членства в группе</span><span class="sxs-lookup"><span data-stu-id="48a0c-333">Group membership persistence</span></span>

<span data-ttu-id="48a0c-334">SignalR отслеживает соединения, а не пользователей, так что если вы хотите, чтобы пользователь был `Groups.Add` в одной группе каждый раз, когда пользователь устанавливает соединение, вы должны звонить каждый раз, когда пользователь устанавливает новое соединение.</span><span class="sxs-lookup"><span data-stu-id="48a0c-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="48a0c-335">После временной потери подключения, иногда SignalR может восстановить соединение автоматически.</span><span class="sxs-lookup"><span data-stu-id="48a0c-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="48a0c-336">В этом случае SignalR восстанавливает одно и то же соединение, не устанавливая новое соединение, и поэтому членство клиента в группе автоматически восстанавливается.</span><span class="sxs-lookup"><span data-stu-id="48a0c-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="48a0c-337">Это возможно даже в том случае, если временный сбой является результатом перезагрузки сервера или сбоя, потому что состояние соединения для каждого клиента, включая членство в группе, округло ежектно езнадля клиенту.</span><span class="sxs-lookup"><span data-stu-id="48a0c-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="48a0c-338">Если сервер выходит из системы и заменяется новым сервером до отключения соединения, клиент может автоматически подключиться к новому серверу и повторно зарегистрироваться в группах, членами которыми он является.</span><span class="sxs-lookup"><span data-stu-id="48a0c-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="48a0c-339">Когда соединение не может быть восстановлено автоматически после потери подключения, или когда время подключения, или когда клиент отключается (например, когда браузер переходит на новую страницу), членство в группе теряется.</span><span class="sxs-lookup"><span data-stu-id="48a0c-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="48a0c-340">В следующий раз, когда пользователь подключится, появится новое соединение.</span><span class="sxs-lookup"><span data-stu-id="48a0c-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="48a0c-341">Для поддержания членства в группе, когда один и тот же пользователь устанавливает новое соединение, приложение должно отслеживать связи между пользователями и группами и восстанавливать членство в группе каждый раз, когда пользователь устанавливает новое соединение.</span><span class="sxs-lookup"><span data-stu-id="48a0c-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="48a0c-342">Более подробную информацию о соединениях и ресоединениях можно узнать по этой теме, [как обрабатывать события жизни соединения в классе концентраторов.](#connectionlifetime)</span><span class="sxs-lookup"><span data-stu-id="48a0c-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="48a0c-343">Группы для пользователей</span><span class="sxs-lookup"><span data-stu-id="48a0c-343">Single-user groups</span></span>

<span data-ttu-id="48a0c-344">Приложения, которые используют SignalR, как правило, должны отслеживать связи между пользователями и соединениями, чтобы знать, какой пользователь отправил сообщение и какой пользователь (ы) должен получать сообщение.</span><span class="sxs-lookup"><span data-stu-id="48a0c-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="48a0c-345">Для этого группы используются в одном из двух часто используемых шаблонов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="48a0c-346">Группы для пользователей.</span><span class="sxs-lookup"><span data-stu-id="48a0c-346">Single-user groups.</span></span>

    <span data-ttu-id="48a0c-347">Вы можете указать имя пользователя в качестве имени группы и добавить идентификатор текущего соединения в группу каждый раз, когда пользователь подключается или подключается.</span><span class="sxs-lookup"><span data-stu-id="48a0c-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="48a0c-348">Отправка сообщений пользователю, который вы отправляете группе.</span><span class="sxs-lookup"><span data-stu-id="48a0c-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="48a0c-349">Недостатком этого метода является то, что группа не предоставляет вам способ узнать, находится ли пользователь в сети или в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="48a0c-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="48a0c-350">Отслеживание ассоциаций между именами пользователей и идентизацией соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="48a0c-351">Вы можете хранить связь между именем каждого пользователя и одним или более идентизациями связи в словаре или базе данных, а также обновлять сохраненные данные каждый раз, когда пользователь подключается или отключается.</span><span class="sxs-lookup"><span data-stu-id="48a0c-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="48a0c-352">Для отправки сообщений пользователю указаны иноъемые данные соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="48a0c-353">Недостатком этого метода является то, что он занимает больше памяти.</span><span class="sxs-lookup"><span data-stu-id="48a0c-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="48a0c-354">Как обрабатывать события жизни соединения в классе концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="48a0c-355">Типичными причинами обработки событий жизни соединения являются отслеживание того, подключен пользователь или нет, а также отслеживание связи между именами пользователей и идентимативами связи.</span><span class="sxs-lookup"><span data-stu-id="48a0c-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="48a0c-356">Чтобы запустить свой собственный код, когда клиенты `OnConnected` `OnDisconnected`подключаются или отключаются, переопределить , и `OnReconnected` виртуальные методы класса концентратора, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="48a0c-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="48a0c-357">При вызове OnConnected, OnDisconnected и OnReconnected</span><span class="sxs-lookup"><span data-stu-id="48a0c-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="48a0c-358">Каждый раз, когда браузер переходит на новую страницу, необходимо установить `OnDisconnected` новое соединение, `OnConnected` что означает, что SignalR будет выполнять метод с последующим методом.</span><span class="sxs-lookup"><span data-stu-id="48a0c-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="48a0c-359">SignalR всегда создает новый идентификатор соединения при установлении нового соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="48a0c-360">Метод `OnReconnected` вызывается, когда произошел временный перерыв в подключении, который SignalR может автоматически восстановить, например, когда кабель временно отключен и восстановлен до отключения соединения. Метод `OnDisconnected` вызывается при отключении клиента и включении SignalR в автоматическое соединение, например, при переходе браузера на новую страницу.</span><span class="sxs-lookup"><span data-stu-id="48a0c-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="48a0c-361">Таким образом, возможная последовательность событий `OnConnected` `OnReconnected`для `OnDisconnected`данного клиента, ; или `OnConnected` `OnDisconnected`, .</span><span class="sxs-lookup"><span data-stu-id="48a0c-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="48a0c-362">Вы не увидите `OnConnected`последовательность, `OnDisconnected` `OnReconnected` для данного соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="48a0c-363">Метод `OnDisconnected` не вызывается в некоторых сценариях, например, когда сервер выходит из-под засетки или домен приложения перерабатывается.</span><span class="sxs-lookup"><span data-stu-id="48a0c-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="48a0c-364">Когда другой сервер выходит в линию или домен App завершает переработку, некоторые `OnReconnected` клиенты могут восстановить соединение и запустить событие.</span><span class="sxs-lookup"><span data-stu-id="48a0c-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="48a0c-365">Для получения дополнительной информации, см [Понимание и обработка подключения Пожизненные события в SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="48a0c-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="48a0c-366">Состояние вызываемого абонента не заселены</span><span class="sxs-lookup"><span data-stu-id="48a0c-366">Caller state not populated</span></span>

<span data-ttu-id="48a0c-367">Методы обработчика событий срока службы соединения вызываются с сервера, что означает, что любое состояние, которое вы размещаете в `state` объекте на клиенте, не будет заполнено в `Caller` свойстве на сервере.</span><span class="sxs-lookup"><span data-stu-id="48a0c-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="48a0c-368">Для получения `state` информации `Caller` об объекте и свойстве, см. [Как передать состояние между клиентами и классом концентратора](#passstate) позже в этой теме.</span><span class="sxs-lookup"><span data-stu-id="48a0c-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="48a0c-369">Как получить информацию о клиенте из свойства Контекста</span><span class="sxs-lookup"><span data-stu-id="48a0c-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="48a0c-370">Чтобы получить информацию о `Context` клиенте, используйте свойство класса концентратор.</span><span class="sxs-lookup"><span data-stu-id="48a0c-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="48a0c-371">Свойство `Context` возвращает объект [HubCallerContext,](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) который предоставляет доступ к следующей информации:</span><span class="sxs-lookup"><span data-stu-id="48a0c-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="48a0c-372">Идентификатор подключения вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="48a0c-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="48a0c-373">Идентификатор соединения — это GUID, назначенный SignalR (вы не можете указать значение в собственном коде).</span><span class="sxs-lookup"><span data-stu-id="48a0c-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="48a0c-374">Для каждого соединения имеется один идентификатор соединения, и один идентификатор соединения используется всеми концентраторами, если в приложении есть несколько концентраторов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="48a0c-375">Данные заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="48a0c-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="48a0c-376">Вы также можете получить `Context.Headers`http заголовки от .</span><span class="sxs-lookup"><span data-stu-id="48a0c-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="48a0c-377">Причина нескольких ссылок на одно и `Context.Headers` то же, `Context.Request` что был создан `Context.Headers` во-первых, свойство было добавлено позже, и был сохранен для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="48a0c-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="48a0c-378">Данные строки запроса.</span><span class="sxs-lookup"><span data-stu-id="48a0c-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="48a0c-379">Вы также можете получить данные строки запроса от `Context.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="48a0c-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="48a0c-380">Строка запроса, которую вы получаете в этом свойстве, используется с запросом HTTP, который установил соединение SignalR.</span><span class="sxs-lookup"><span data-stu-id="48a0c-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="48a0c-381">Параметры строки запроса можно добавить в клиенте, настроив соединение, которое является удобным способом передачи данных о клиенте от клиента на сервер.</span><span class="sxs-lookup"><span data-stu-id="48a0c-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="48a0c-382">Ниже приводится один из способов добавления строки запроса в клиент JavaScript при использовании сгенерированного прокси.</span><span class="sxs-lookup"><span data-stu-id="48a0c-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="48a0c-383">Для получения дополнительной информации о параметрах строки запроса смотрите руководства API для клиентов [JavaScript](hubs-api-guide-javascript-client.md) и [.NET.](hubs-api-guide-net-client.md)</span><span class="sxs-lookup"><span data-stu-id="48a0c-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="48a0c-384">Можно найти метод транспортировки, используемый для соединения в данных строки запроса, а также некоторые другие значения, используемые внутри SignalR:</span><span class="sxs-lookup"><span data-stu-id="48a0c-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="48a0c-385">Значение `transportMethod` будет "webSockets", "serverSentEvents", "foreverFrame" или "longPolling".</span><span class="sxs-lookup"><span data-stu-id="48a0c-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="48a0c-386">Обратите внимание, что если `OnConnected` вы проверите это значение в методе обработчика событий, то в некоторых сценариях вы можете получить транспортное значение, которое не является окончательным согласованным методом транспортировки для соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="48a0c-387">В этом случае метод будет закидывать исключение и будет вызван позже, когда будет установлен окончательный метод транспортировки.</span><span class="sxs-lookup"><span data-stu-id="48a0c-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="48a0c-388">Печенье.</span><span class="sxs-lookup"><span data-stu-id="48a0c-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="48a0c-389">Вы также можете получить `Context.RequestCookies`печенье от .</span><span class="sxs-lookup"><span data-stu-id="48a0c-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="48a0c-390">сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="48a0c-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="48a0c-391">Объект HttpContext для запроса:</span><span class="sxs-lookup"><span data-stu-id="48a0c-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="48a0c-392">Используйте этот метод `HttpContext.Current` вместо `HttpContext` того, чтобы получить объект для подключения SignalR.</span><span class="sxs-lookup"><span data-stu-id="48a0c-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="48a0c-393">Как передать состояние между клиентами и классом концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="48a0c-394">Клиент прокси предоставляет `state` объект, в котором вы можете хранить данные, которые вы хотите быть переданы на сервер с каждым методом вызова.</span><span class="sxs-lookup"><span data-stu-id="48a0c-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="48a0c-395">На сервере вы можете получить `Clients.Caller` доступ к этим данным в свойстве в методах концентратора, которые вызываются клиентами.</span><span class="sxs-lookup"><span data-stu-id="48a0c-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="48a0c-396">Свойство `Clients.Caller` не заселены для методов `OnConnected`обработчика событий срока службы соединения, `OnDisconnected`и `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="48a0c-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="48a0c-397">Создание или обновление данных в объекте `state` и свойстве `Clients.Caller` работает в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="48a0c-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="48a0c-398">Вы можете обновить значения на сервере, и они передаются обратно клиенту.</span><span class="sxs-lookup"><span data-stu-id="48a0c-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="48a0c-399">В следующем примере показан клиентский код JavaScript, который хранит состояние для передачи на сервер с каждым вызовом метода.</span><span class="sxs-lookup"><span data-stu-id="48a0c-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="48a0c-400">В следующем примере показан эквивалентный код в клиенте .NET.</span><span class="sxs-lookup"><span data-stu-id="48a0c-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="48a0c-401">В классе концентратора вы `Clients.Caller` можете получить доступ к этим данным в свойстве.</span><span class="sxs-lookup"><span data-stu-id="48a0c-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="48a0c-402">В следующем примере показан код, который извлекает состояние, упомянутое в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="48a0c-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="48a0c-403">Этот механизм для сохраняющегося состояния не предназначен для больших объемов данных, так как все, что вы кладете в свойство `state` или `Clients.Caller` свойство, округляется с каждым вызовом метода.</span><span class="sxs-lookup"><span data-stu-id="48a0c-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="48a0c-404">Это полезно для небольших элементов, таких как имена пользователей или счетчики.</span><span class="sxs-lookup"><span data-stu-id="48a0c-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="48a0c-405">В VB.NET или в концентраторе сильного типа, объект состояния `Clients.Caller`вызываемого не может быть доступен через; вместо этого, использование `Clients.CallerState` (введено в SignalR 2.1):</span><span class="sxs-lookup"><span data-stu-id="48a0c-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="48a0c-406">**Использование состояния Caller в C #**</span><span class="sxs-lookup"><span data-stu-id="48a0c-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="48a0c-407">**Использование CallerState в визуальном базовом**</span><span class="sxs-lookup"><span data-stu-id="48a0c-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="48a0c-408">Как обрабатывать ошибки в классе концентратор</span><span class="sxs-lookup"><span data-stu-id="48a0c-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="48a0c-409">Для обработки ошибок, возникающих в методах класса концентратора, сначала убедитесь, что вы «наблюдаете» любые исключения из операций async (например, ссылаясь на клиентские методы) с помощью. `await`</span><span class="sxs-lookup"><span data-stu-id="48a0c-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="48a0c-410">Затем используйте один или несколько из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="48a0c-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="48a0c-411">Оберните код метода в блоки try-catch и ввейди объект исключения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="48a0c-412">Для отладки можно отправить исключение клиенту, но по соображениям безопасности отправка подробной информации клиентам в производстве не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="48a0c-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="48a0c-413">Создайте модуль конвейера концентраторов, который обрабатывает метод [OnIncomingError.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="48a0c-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="48a0c-414">В следующем примере показан модуль конвейера, который регистрирует ошибки, а затем код в Startup.cs который вводит модуль в конвейер концентраторов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="48a0c-415">Используйте `HubException` класс (введен в SignalR 2).</span><span class="sxs-lookup"><span data-stu-id="48a0c-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="48a0c-416">Эта ошибка может быть брошена из любого вызова концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="48a0c-417">Конструктор `HubError` принимает строку сообщения и объект для хранения дополнительных данных об ошибке.</span><span class="sxs-lookup"><span data-stu-id="48a0c-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="48a0c-418">SignalR автоматически заследует исключение и отправляет его клиенту, где он будет использоваться для отклонения или отказа вызова метода концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="48a0c-419">Следующие примеры кода демонстрируют, как бросить вызов `HubException` во время вызова концентратора и как обрабатывать исключение для клиентов JavaScript и .NET.</span><span class="sxs-lookup"><span data-stu-id="48a0c-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="48a0c-420">**Серверный код, демонстрирующий класс HubException**</span><span class="sxs-lookup"><span data-stu-id="48a0c-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="48a0c-421">**Клиентский код JavaScript, демонстрирующий реакцию на бросание HubException в концентратор**</span><span class="sxs-lookup"><span data-stu-id="48a0c-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="48a0c-422">**клиентский код .NET демонстрирует реакцию на бросание HubException в концентратор**</span><span class="sxs-lookup"><span data-stu-id="48a0c-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="48a0c-423">Более подробную информацию о модулях конвейера концентратора можно [найти](#hubpipeline) в этой теме позже.</span><span class="sxs-lookup"><span data-stu-id="48a0c-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="48a0c-424">Как включить трассировку</span><span class="sxs-lookup"><span data-stu-id="48a0c-424">How to enable tracing</span></span>

<span data-ttu-id="48a0c-425">Чтобы включить отслеживание сервера, добавьте элемент system.diagnostics в файл Web.config, как показано в этом примере:</span><span class="sxs-lookup"><span data-stu-id="48a0c-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="48a0c-426">При запуске приложения в Visual Studio можно просматривать журналы в окне **вывода.**</span><span class="sxs-lookup"><span data-stu-id="48a0c-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="48a0c-427">Как вызвать методы клиентов и управлять группами из-за пределов класса концентратора</span><span class="sxs-lookup"><span data-stu-id="48a0c-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="48a0c-428">Чтобы вызвать методы клиента из другого класса, чем класс концентратора, получите ссылку на контекстный объект SignalR для концентратора и используйте его для вызова методов клиента или управления группами.</span><span class="sxs-lookup"><span data-stu-id="48a0c-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="48a0c-429">Следующий `StockTicker` класс примера получает объект контекста, хранит его в экземпляре класса, хранит экземпляр класса в статичном `updateStockPrice` свойстве и использует контекст из `StockTickerHub`экземпляра класса singleton для вызова метода на клиентов, подключенных к названному концентратору.</span><span class="sxs-lookup"><span data-stu-id="48a0c-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="48a0c-430">Если вам нужно использовать контекст несколько раз в долгоживущих объекта, получить ссылку один раз и сохранить его, а не получать его снова каждый раз.</span><span class="sxs-lookup"><span data-stu-id="48a0c-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="48a0c-431">Получение контекста один раз гарантирует, что SignalR отправляет сообщения клиентам в той же последовательности, в которой методы концентратора делают вызовы метода клиента.</span><span class="sxs-lookup"><span data-stu-id="48a0c-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="48a0c-432">Для учебника, который показывает, как использовать контекст SignalR для концентратора, см [ASP.NET.](../getting-started/tutorial-server-broadcast-with-signalr.md)</span><span class="sxs-lookup"><span data-stu-id="48a0c-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="48a0c-433">Вызов методов клиента</span><span class="sxs-lookup"><span data-stu-id="48a0c-433">Calling client methods</span></span>

<span data-ttu-id="48a0c-434">Вы можете указать, какие клиенты получат RPC, но у вас меньше вариантов, чем при вызове из класса концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="48a0c-435">Причиной этого является то, что контекст не связан с конкретным вызовом от клиента, поэтому любые `Clients.Others`методы, которые требуют знания текущего идентификатора соединения, такие как, или `Clients.Caller` `Clients.OthersInGroup`, не доступны.</span><span class="sxs-lookup"><span data-stu-id="48a0c-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="48a0c-436">Доступны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="48a0c-436">The following options are available:</span></span>

- <span data-ttu-id="48a0c-437">Все подключенные клиенты.</span><span class="sxs-lookup"><span data-stu-id="48a0c-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="48a0c-438">Конкретный клиент, идентифицированный по идентификатору соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="48a0c-439">Все подключенные клиенты, за исключением указанных клиентов, идентифицируются по идентификатору подключения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="48a0c-440">Все подключенные клиенты в определенной группе.</span><span class="sxs-lookup"><span data-stu-id="48a0c-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="48a0c-441">Все подключенные клиенты в указанной группе, за исключением указанных клиентов, идентифицированных по идентификатору соединения.</span><span class="sxs-lookup"><span data-stu-id="48a0c-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="48a0c-442">Если вы звоните в свой класс, не являющийся концентратором, из методов `Clients.AllExcept`в `Clients.Group` классе концентратора, вы можете сдать идентификатор текущего соединения и использовать его с `Clients.Client`помощью, или для имитации, `Clients.Caller` `Clients.Others`или `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="48a0c-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="48a0c-443">В следующем примере `MoveShapeHub` класс передает идентификатор соединения классу, `Broadcaster` чтобы `Broadcaster` класс мог имитировать. `Clients.Others`</span><span class="sxs-lookup"><span data-stu-id="48a0c-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="48a0c-444">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="48a0c-444">Managing group membership</span></span>

<span data-ttu-id="48a0c-445">Для управления группами у вас есть те же варианты, что и в классе концентраторов.</span><span class="sxs-lookup"><span data-stu-id="48a0c-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="48a0c-446">Добавление клиента в группу</span><span class="sxs-lookup"><span data-stu-id="48a0c-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="48a0c-447">Удалить клиента из группы</span><span class="sxs-lookup"><span data-stu-id="48a0c-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="48a0c-448">Как настроить конвейер концентров</span><span class="sxs-lookup"><span data-stu-id="48a0c-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="48a0c-449">SignalR позволяет вводить свой собственный код в конвейер концентратора.</span><span class="sxs-lookup"><span data-stu-id="48a0c-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="48a0c-450">В следующем примере показан модуль конвейера пользовательского центра, который регистрирует каждый входящий вызов метода, полученный от вызова клиента и исходящего вызова метода, вызываемого на клиента:</span><span class="sxs-lookup"><span data-stu-id="48a0c-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="48a0c-451">Следующий код в *файле Startup.cs* регистрирует модуль для запуска в конвейере концентратора:</span><span class="sxs-lookup"><span data-stu-id="48a0c-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="48a0c-452">Есть много различных методов, которые можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="48a0c-452">There are many different methods that you can override.</span></span> <span data-ttu-id="48a0c-453">Для получения полного [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)списка см.</span><span class="sxs-lookup"><span data-stu-id="48a0c-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
