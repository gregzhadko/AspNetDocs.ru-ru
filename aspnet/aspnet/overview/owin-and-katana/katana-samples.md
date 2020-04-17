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
# <a name="katana-samples"></a>Примеры Katana

[корпорацией Майкрософт](https://github.com/microsoft)

## <a name="katana-samples"></a>Примеры Katana

**ASP.NET маршруты Пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
В некоторых приложениях вы хотите подключить компоненты OWIN в таблице Asp.Net маршрутной таблице бок о бок с компонентами, не входящих в OWIN. В этом примере показано, как использовать методы расширения RouteCollection MapOwinPath и MapOwinRoute, предоставленные Microsoft.Owin.Host.SystemWeb.

**Ветвящиеся трубопроводы Образец** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
Конвейеры обработки запросов OWIN не должны быть линейными, они могут быть разветвлены для обработки запросов различными способами. В этом примере показано, как построить конвейер ветвления на основе путей запроса или других данных запросов, таких как заголовки. Эти компоненты доступны в пакете nuget microsoft.Owin.Mapping.

**Пользовательский код исходного** | [кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) образца сервера   
Показывает, как использовать пользовательский сервер OWIN при самостоятельном размещении OWIN.

**Встроенный исходный** | [код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded) образца  
Некоторые серверы OWIN могут быть запущены внутри&quot;вашего собственного процесса (самостоятельно).&quot; Этот пример показывает, как запустить приложение OWIN с помощью инструментов, предоставляемых пакетом nuget Microsoft.Owin.Hosting.

**HelloWorld Пример** | [Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN — это абстракция API сервера HTTP, которая обеспечивает переносимость приложений на различных серверах. Этот пример демонстрирует, как написать приложение Hello World, используя несколько **простых оберток** вокруг сырой абстракции OWIN и запустить его на веб-сервере, как ASP.NET.

**Привет Всемирный Сырье OWIN Образец** | [Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
Этот пример демонстрирует, как написать приложение Hello World с помощью **необработанной** абстракции OWIN и запустить его на веб-сервере, как Asp.Net.

**Код исходного кода SignalR образца** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
Показывает, как самостоятельно хозяйничать SignalR с помощью OWIN / Katana. Для получения дополнительной информации о самостоятельном хостинге SignalR, [см. Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Статических файлов Пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
Показывает, как поддерживать запросы HTTP для статических файлов с помощью OWIN / Katana.

**Исходный** | [код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) Web API   
В этом примере показано, как размещать OWIN в IIS и добавлять Web API в конвейер OWIN.

**Веб-разъем Образец** | [Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
Показывает, как поддерживать веб-розетки в OWIN с помощью класса [System.Net.WebSockets.WebSocket.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)
