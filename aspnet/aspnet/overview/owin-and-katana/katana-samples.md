---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Примеры Katana | Документация Майкрософт
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379078"
---
# <a name="katana-samples"></a><span data-ttu-id="714c6-102">Примеры Katana</span><span class="sxs-lookup"><span data-stu-id="714c6-102">Katana Samples</span></span>

<span data-ttu-id="714c6-103">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="714c6-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="714c6-104">Примеры Katana</span><span class="sxs-lookup"><span data-stu-id="714c6-104">Katana Samples</span></span>

<span data-ttu-id="714c6-105">**ASP.NET направляет образец** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="714c6-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="714c6-106">В некоторых приложениях требуется подключить компоненты OWIN в таблице маршрутов Asp.Net параллельно с компонентами не OWIN.</span><span class="sxs-lookup"><span data-stu-id="714c6-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="714c6-107">В этом примере показано, как использовать методы расширения RouteCollection MapOwinPath и MapOwinRoute, предоставляемые Microsoft.Owin.Host.SystemWeb.</span><span class="sxs-lookup"><span data-stu-id="714c6-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="714c6-108">**Ветвление конвейеров образец** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="714c6-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="714c6-109">Конвейера обработки запросов OWIN не обязательно должны быть линейными, они могут быть разветвлены для обработки запросов по-разному.</span><span class="sxs-lookup"><span data-stu-id="714c6-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="714c6-110">В этом примере показано, как для формирования ветвления конвейера, на основе путей запросов или другие данные запроса, такие как заголовки.</span><span class="sxs-lookup"><span data-stu-id="714c6-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="714c6-111">Эти компоненты доступны в пакете nuget Microsoft.Owin.Mapping.</span><span class="sxs-lookup"><span data-stu-id="714c6-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="714c6-112">**Пример пользовательского сервера** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)</span><span class="sxs-lookup"><span data-stu-id="714c6-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)</span></span>   
<span data-ttu-id="714c6-113">Показано, как использовать пользовательский сервер OWIN при саморазмещением OWIN.</span><span class="sxs-lookup"><span data-stu-id="714c6-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="714c6-114">**Образец Embedded** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="714c6-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="714c6-115">Некоторые серверы OWIN может выполняться внутри собственного процесса (&quot;резидентным&quot;).</span><span class="sxs-lookup"><span data-stu-id="714c6-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="714c6-116">В этом примере показано, как запустить приложение OWIN с помощью средств, предоставляемых пакетом nuget Microsoft.Owin.Hosting.</span><span class="sxs-lookup"><span data-stu-id="714c6-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="714c6-117">**Образец HelloWorld** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="714c6-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="714c6-118">OWIN — это сервер HTTP API абстракции, который обеспечивает возможность переноса приложений на различных серверах.</span><span class="sxs-lookup"><span data-stu-id="714c6-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="714c6-119">В этом примере показано, как создать приложение Hello World с помощью некоторых **простыми оболочками** вокруг необработанные абстракции OWIN и запустите его на веб-сервере, такие как ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="714c6-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="714c6-120">**Пример Hello World необработанные OWIN** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="714c6-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="714c6-121">В этом примере показано, как писать приложения Hello World с помощью **необработанные** абстракции OWIN и запустите его на веб-сервере, такие как Asp.Net.</span><span class="sxs-lookup"><span data-stu-id="714c6-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="714c6-122">**Пример SignalR** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="714c6-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="714c6-123">Показано, как Резидентное размещение SignalR с помощью OWIN и Katana.</span><span class="sxs-lookup"><span data-stu-id="714c6-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="714c6-124">Дополнительные сведения о SignalR размещения на собственном сервере, см. в разделе [руководства: Резидентное размещение SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="714c6-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="714c6-125">**Статические файлы образца** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)</span><span class="sxs-lookup"><span data-stu-id="714c6-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)</span></span>   
<span data-ttu-id="714c6-126">Показано, как для поддержки HTTP-запросы для статических файлов с помощью OWIN и Katana.</span><span class="sxs-lookup"><span data-stu-id="714c6-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="714c6-127">**Веб-API** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)</span><span class="sxs-lookup"><span data-stu-id="714c6-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)</span></span>   
<span data-ttu-id="714c6-128">В этом примере показано, как размещение OWIN в службах IIS и добавление веб-API в конвейер OWIN.</span><span class="sxs-lookup"><span data-stu-id="714c6-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="714c6-129">**Веб-сокета образец** | [исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)</span><span class="sxs-lookup"><span data-stu-id="714c6-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)</span></span>   
<span data-ttu-id="714c6-130">Показано, как обеспечить поддержку веб-сокеты в OWIN с помощью [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="714c6-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
