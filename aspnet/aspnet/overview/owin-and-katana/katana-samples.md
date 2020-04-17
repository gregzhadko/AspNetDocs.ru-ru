---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Катана Образцы Документы Майкрософт
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540445"
---
# <a name="katana-samples"></a><span data-ttu-id="14ce8-102">Примеры Katana</span><span class="sxs-lookup"><span data-stu-id="14ce8-102">Katana Samples</span></span>

<span data-ttu-id="14ce8-103">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="14ce8-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="14ce8-104">Примеры Katana</span><span class="sxs-lookup"><span data-stu-id="14ce8-104">Katana Samples</span></span>

<span data-ttu-id="14ce8-105">**ASP.NET маршруты Пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="14ce8-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="14ce8-106">В некоторых приложениях вы хотите подключить компоненты OWIN в таблице Asp.Net маршрутной таблице бок о бок с компонентами, не входящих в OWIN.</span><span class="sxs-lookup"><span data-stu-id="14ce8-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="14ce8-107">В этом примере показано, как использовать методы расширения RouteCollection MapOwinPath и MapOwinRoute, предоставленные Microsoft.Owin.Host.SystemWeb.</span><span class="sxs-lookup"><span data-stu-id="14ce8-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="14ce8-108">**Ветвящиеся трубопроводы Образец** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="14ce8-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="14ce8-109">Конвейеры обработки запросов OWIN не должны быть линейными, они могут быть разветвлены для обработки запросов различными способами.</span><span class="sxs-lookup"><span data-stu-id="14ce8-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="14ce8-110">В этом примере показано, как построить конвейер ветвления на основе путей запроса или других данных запросов, таких как заголовки.</span><span class="sxs-lookup"><span data-stu-id="14ce8-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="14ce8-111">Эти компоненты доступны в пакете nuget microsoft.Owin.Mapping.</span><span class="sxs-lookup"><span data-stu-id="14ce8-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="14ce8-112">**Пользовательский код исходного** | [кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) образца сервера </span><span class="sxs-lookup"><span data-stu-id="14ce8-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="14ce8-113">Показывает, как использовать пользовательский сервер OWIN при самостоятельном размещении OWIN.</span><span class="sxs-lookup"><span data-stu-id="14ce8-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="14ce8-114">**Встроенный исходный** | [код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded) образца</span><span class="sxs-lookup"><span data-stu-id="14ce8-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="14ce8-115">Некоторые серверы OWIN могут быть запущены внутри&quot;вашего собственного процесса (самостоятельно).&quot;</span><span class="sxs-lookup"><span data-stu-id="14ce8-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="14ce8-116">Этот пример показывает, как запустить приложение OWIN с помощью инструментов, предоставляемых пакетом nuget Microsoft.Owin.Hosting.</span><span class="sxs-lookup"><span data-stu-id="14ce8-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="14ce8-117">**HelloWorld Пример** | [Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="14ce8-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="14ce8-118">OWIN — это абстракция API сервера HTTP, которая обеспечивает переносимость приложений на различных серверах.</span><span class="sxs-lookup"><span data-stu-id="14ce8-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="14ce8-119">Этот пример демонстрирует, как написать приложение Hello World, используя несколько **простых оберток** вокруг сырой абстракции OWIN и запустить его на веб-сервере, как ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="14ce8-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="14ce8-120">**Привет Всемирный Сырье OWIN Образец** | [Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="14ce8-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="14ce8-121">Этот пример демонстрирует, как написать приложение Hello World с помощью **необработанной** абстракции OWIN и запустить его на веб-сервере, как Asp.Net.</span><span class="sxs-lookup"><span data-stu-id="14ce8-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="14ce8-122">**Код исходного кода SignalR образца** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="14ce8-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="14ce8-123">Показывает, как самостоятельно хозяйничать SignalR с помощью OWIN / Katana.</span><span class="sxs-lookup"><span data-stu-id="14ce8-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="14ce8-124">Для получения дополнительной информации о самостоятельном хостинге SignalR, [см. Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="14ce8-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="14ce8-125">**Статических файлов Пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="14ce8-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="14ce8-126">Показывает, как поддерживать запросы HTTP для статических файлов с помощью OWIN / Katana.</span><span class="sxs-lookup"><span data-stu-id="14ce8-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="14ce8-127">**Исходный** | [код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) Web API </span><span class="sxs-lookup"><span data-stu-id="14ce8-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="14ce8-128">В этом примере показано, как размещать OWIN в IIS и добавлять Web API в конвейер OWIN.</span><span class="sxs-lookup"><span data-stu-id="14ce8-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="14ce8-129">**Веб-разъем Образец** | [Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="14ce8-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="14ce8-130">Показывает, как поддерживать веб-розетки в OWIN с помощью класса [System.Net.WebSockets.WebSocket.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="14ce8-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
