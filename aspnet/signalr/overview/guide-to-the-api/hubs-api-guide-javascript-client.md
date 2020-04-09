---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Концентраторы API Руководство - JavaScript Клиент (ru) Документы Майкрософт
author: bradygaster
description: Этот документ содержит введение в использование API-интерфейса концентратов для версии SignalR 2 у клиентов JavaScript, таких как браузеры и приложение Windows Store (WinJS).
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675715"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="50cef-103">ASP.NET SignalR Концентраторы API Руководство - JavaScript Клиент</span><span class="sxs-lookup"><span data-stu-id="50cef-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="50cef-104">Этот документ предусматривает введение в использование API-интерфейса концентратов для версии SignalR 2 у клиентов JavaScript, таких как браузеры и приложения Windows Store (WinJS).</span><span class="sxs-lookup"><span data-stu-id="50cef-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="50cef-105">API Концентраторов SignalR позволяет совершать удаленные процедурные звонки (RPCs) с сервера для подключенных клиентов и от клиентов к серверу.</span><span class="sxs-lookup"><span data-stu-id="50cef-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="50cef-106">В коде сервера вы определяете методы, которые могут вызываться клиентами, и вызываете методы, которые работают на клиенте.</span><span class="sxs-lookup"><span data-stu-id="50cef-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="50cef-107">В клиентском коде вы определяете методы, которые можно вызывать с сервера, и вызываете методы, которые работают на сервере.</span><span class="sxs-lookup"><span data-stu-id="50cef-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="50cef-108">SignalR заботится о всех клиента к серверу сантехника для вас.</span><span class="sxs-lookup"><span data-stu-id="50cef-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="50cef-109">SignalR также предлагает API более низкого уровня под названием Persistent Connections.</span><span class="sxs-lookup"><span data-stu-id="50cef-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="50cef-110">Для введения в SignalR, концентраторы, и стойкие соединения, [см.](../getting-started/introduction-to-signalr.md)</span><span class="sxs-lookup"><span data-stu-id="50cef-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="50cef-111">Версии программного обеспечения, используемые в этой теме</span><span class="sxs-lookup"><span data-stu-id="50cef-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="50cef-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="50cef-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="50cef-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="50cef-113">.NET 4.5</span></span>
> - <span data-ttu-id="50cef-114">Версия SignalR 2</span><span class="sxs-lookup"><span data-stu-id="50cef-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="50cef-115">Предыдущие версии этой темы</span><span class="sxs-lookup"><span data-stu-id="50cef-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="50cef-116">Для получения информации о более ранних версиях SignalR, см [SignalR Старые версии](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="50cef-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="50cef-117">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="50cef-117">Questions and comments</span></span>
>
> <span data-ttu-id="50cef-118">Пожалуйста, оставьте обратную связь о том, как вам понравился этот учебник и что мы могли бы улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="50cef-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="50cef-119">Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com.](http://stackoverflow.com/)</span><span class="sxs-lookup"><span data-stu-id="50cef-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="50cef-120">Обзор</span><span class="sxs-lookup"><span data-stu-id="50cef-120">Overview</span></span>

<span data-ttu-id="50cef-121">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="50cef-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="50cef-122">Сгенерированный прокси и то, что он делает для вас</span><span class="sxs-lookup"><span data-stu-id="50cef-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="50cef-123">Когда использовать генерируемый прокси</span><span class="sxs-lookup"><span data-stu-id="50cef-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="50cef-124">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="50cef-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="50cef-125">Как ссылаться на динамически сгенерированный прокси</span><span class="sxs-lookup"><span data-stu-id="50cef-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="50cef-126">Как создать физический файл для прокси-сервера SignalR</span><span class="sxs-lookup"><span data-stu-id="50cef-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="50cef-127">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="50cef-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="50cef-128">$.connection.hub - это тот же объект, который создает $.hubConnection()</span><span class="sxs-lookup"><span data-stu-id="50cef-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="50cef-129">Асинхронное выполнение метода старта</span><span class="sxs-lookup"><span data-stu-id="50cef-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="50cef-130">Как установить кросс-доменсоединение</span><span class="sxs-lookup"><span data-stu-id="50cef-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="50cef-131">Как настроить соединение</span><span class="sxs-lookup"><span data-stu-id="50cef-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="50cef-132">Как указать параметры строки запроса</span><span class="sxs-lookup"><span data-stu-id="50cef-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="50cef-133">Как указать транспортный метод</span><span class="sxs-lookup"><span data-stu-id="50cef-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="50cef-134">Как получить прокси для класса концентратор</span><span class="sxs-lookup"><span data-stu-id="50cef-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="50cef-135">Как определить методы на клиенте, который может вызвать сервер</span><span class="sxs-lookup"><span data-stu-id="50cef-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="50cef-136">Как вызвать методы сервера от клиента</span><span class="sxs-lookup"><span data-stu-id="50cef-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="50cef-137">Как обрабатывать события жизни соединения</span><span class="sxs-lookup"><span data-stu-id="50cef-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="50cef-138">Как обрабатывать ошибки</span><span class="sxs-lookup"><span data-stu-id="50cef-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="50cef-139">Как включить журналирование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="50cef-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="50cef-140">Для получения документации о том, как запрограммировать сервер или клиентов .NET, см.</span><span class="sxs-lookup"><span data-stu-id="50cef-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="50cef-141">Руководство По API Концентратов SignalR - Сервер</span><span class="sxs-lookup"><span data-stu-id="50cef-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="50cef-142">Руководство По API Концентраторов SignalR - Клиент .NET</span><span class="sxs-lookup"><span data-stu-id="50cef-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="50cef-143">Компонент сервера SignalR 2 доступен только на .NET 4.5 (хотя есть клиент .NET для SignalR 2 на .NET 4.0).</span><span class="sxs-lookup"><span data-stu-id="50cef-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="50cef-144">Сгенерированный прокси и то, что он делает для вас</span><span class="sxs-lookup"><span data-stu-id="50cef-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="50cef-145">Вы можете запрограммировать клиента JavaScript для связи с службой SignalR с прокси или без нее, который SignalR генерирует для вас.</span><span class="sxs-lookup"><span data-stu-id="50cef-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="50cef-146">Прокси-сервер упрощает синтаксис кода, который используется для подключения, записывает методы, которые вызывает сервер, и методы вызова на сервере.</span><span class="sxs-lookup"><span data-stu-id="50cef-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="50cef-147">Когда вы пишете код для вызова методов вызова сервера, генерируемый `serverMethod(arg1, arg2)` `invoke('serverMethod', arg1, arg2)`прокси позволяет использовать синтаксис, который выглядит так, как будто вы исполняете локальную функцию: вы можете писать вместо .</span><span class="sxs-lookup"><span data-stu-id="50cef-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="50cef-148">Сгенерированный прокси-синтаксис также допускает немедленную и понятную ошибку на стороне клиента, если вы неправильно введите имя метода сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="50cef-149">И если вы вручную создаете файл, который определяет прокси, вы также можете получить поддержку IntelliSense для написания кода, который вызывает методы сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="50cef-150">Например, предположим, что на сервере есть следующий класс концентратора:</span><span class="sxs-lookup"><span data-stu-id="50cef-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="50cef-151">Следующие примеры кода показывают, как выглядит код `NewContosoChatMessage` JavaScript для вызова метода `addContosoChatMessageToPage` на сервере и получения вызовов метода с сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="50cef-152">**С генерируемым прокси**</span><span class="sxs-lookup"><span data-stu-id="50cef-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="50cef-153">**Без сгенерированного прокси**</span><span class="sxs-lookup"><span data-stu-id="50cef-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="50cef-154">Когда использовать генерируемый прокси</span><span class="sxs-lookup"><span data-stu-id="50cef-154">When to use the generated proxy</span></span>

<span data-ttu-id="50cef-155">Если вы хотите зарегистрировать несколько обработчиков событий для метода клиента, который вызывает сервер, вы не можете использовать генерируемый прокси.</span><span class="sxs-lookup"><span data-stu-id="50cef-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="50cef-156">В противном случае можно использовать генерируемый прокси или не основываться на предпочтениях кодирования.</span><span class="sxs-lookup"><span data-stu-id="50cef-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="50cef-157">Если вы решите не использовать его, вам не нужно ссылаться на URL-адрес "signalr/hubs" в элементе `script` в ашего клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="50cef-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="50cef-158">Настройка клиента</span><span class="sxs-lookup"><span data-stu-id="50cef-158">Client setup</span></span>

<span data-ttu-id="50cef-159">Клиенту JavaScript требуются ссылки на j''s и ядро JavaScript файла SignalR.</span><span class="sxs-lookup"><span data-stu-id="50cef-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="50cef-160">Версия j'query должна быть 1.6.4 или основных более поздних версий, таких как 1.7.2, 1.8.2, или 1.9.1.</span><span class="sxs-lookup"><span data-stu-id="50cef-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="50cef-161">Если вы решили использовать сгенерированный прокси- и справку о сгенерированном файле JavaScript SignalR.</span><span class="sxs-lookup"><span data-stu-id="50cef-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="50cef-162">Ниже приводится следующий пример, как могут выглядеть ссылки на странице HTML, использующей генерируемый прокси.</span><span class="sxs-lookup"><span data-stu-id="50cef-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="50cef-163">Эти ссылки должны быть включены в этот порядок: j''sfirst, ядро SignalR после этого, и прокси SignalR последние.</span><span class="sxs-lookup"><span data-stu-id="50cef-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="50cef-164">Как ссылаться на динамически сгенерированный прокси</span><span class="sxs-lookup"><span data-stu-id="50cef-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="50cef-165">В предыдущем примере ссылка на прокси SignalR— динамически сгенерированный код JavaScript, а не на физический файл.</span><span class="sxs-lookup"><span data-stu-id="50cef-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="50cef-166">SignalR создает код JavaScript для прокси на лету и подает его клиенту в ответ на URL-адрес "/signalr/hubs".</span><span class="sxs-lookup"><span data-stu-id="50cef-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="50cef-167">Если в `MapSignalR` методе указан другой базовый URL для соединений SignalR на сервере, URL-адрес для динамического прокси-файла является пользовательским URL-адресом с приложеным к нему "/концентратами".</span><span class="sxs-lookup"><span data-stu-id="50cef-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="50cef-168">Для клиентов JavaScript Windows 8 (Windows Store) используйте физический прокси-файл вместо динамического файла.</span><span class="sxs-lookup"><span data-stu-id="50cef-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="50cef-169">Для получения дополнительной информации, см [Как создать физический файл для SignalR генерируется прокси](#manualproxy) позже в этой теме.</span><span class="sxs-lookup"><span data-stu-id="50cef-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="50cef-170">В ASP.NET MVC 4 или 5 Razor view, используйте tilde для обозначения корня приложения в вашем справочнике файла прокси:</span><span class="sxs-lookup"><span data-stu-id="50cef-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="50cef-171">Для получения дополнительной информации об использовании SignalR в MVC 5, см. [Начало работы с SignalR и MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="50cef-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="50cef-172">В ASP.NET MVC 3 Razor, используйте `Url.Content` для вашего прокси-файла:</span><span class="sxs-lookup"><span data-stu-id="50cef-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="50cef-173">В ASP.NET приложения Web `ResolveClientUrl` Forms используйте для своих прокси-файлов или зарегистрируйте ее через ScriptManager, используя относительный путь root app (начиная с tilde):</span><span class="sxs-lookup"><span data-stu-id="50cef-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="50cef-174">Как правило, используйте тот же метод для указания URL-адреса "/signalr/hubs", который используется для файлов CSS или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="50cef-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="50cef-175">Если вы указали URL-адрес без использования tilde, в некоторых сценариях ваше приложение будет работать правильно при тестировании в Visual Studio с помощью IIS Express, но не сошибкой при развертывании на полном IIS.</span><span class="sxs-lookup"><span data-stu-id="50cef-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="50cef-176">Для получения дополнительной информации смотрите **разрешение ссылок на ресурсы корневого уровня** в [веб-серверах в Visual Studio для ASP.NET web-проектов](https://msdn.microsoft.com/library/58wxa9w5.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="50cef-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="50cef-177">При запуске веб-проекта в Visual Studio 2017 в режиме отладки, и если вы используете Internet Explorer в качестве браузера, вы можете увидеть прокси-файл в **Solution Explorer** под **скриптами.**</span><span class="sxs-lookup"><span data-stu-id="50cef-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="50cef-178">Чтобы увидеть содержимое файла, дважды щелкните **концентраторов.**</span><span class="sxs-lookup"><span data-stu-id="50cef-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="50cef-179">Если вы не используете Visual Studio 2012 или 2013 и Internet Explorer, или если вы не находитесь в режиме отладки, вы также можете получить содержимое файла, просматривая URL"/signalR/hubs.</span><span class="sxs-lookup"><span data-stu-id="50cef-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="50cef-180">Например, если ваш сайт `http://localhost:56699`работает `http://localhost:56699/SignalR/hubs` на , перейдите в вашем браузере.</span><span class="sxs-lookup"><span data-stu-id="50cef-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="50cef-181">Как создать физический файл для прокси-сервера SignalR</span><span class="sxs-lookup"><span data-stu-id="50cef-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="50cef-182">В качестве альтернативы динамически сгенерированному прокси можно создать физический файл с прокси-кодом и ссылкой на этот файл.</span><span class="sxs-lookup"><span data-stu-id="50cef-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="50cef-183">Вы можете сделать это для контроля над поведением кэширования или комплектации, или получить IntelliSense, когда вы кодирования вызовов для серверных методов.</span><span class="sxs-lookup"><span data-stu-id="50cef-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="50cef-184">Чтобы создать прокси-файл, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="50cef-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="50cef-185">Установите пакет [Microsoft.AspNet.Signalr.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet.</span><span class="sxs-lookup"><span data-stu-id="50cef-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="50cef-186">Откройте запрос команды и просмотрите папку *инструментов,* содержащую файл SignalR.exe.</span><span class="sxs-lookup"><span data-stu-id="50cef-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="50cef-187">Папка инструментов находится в следующем месте:</span><span class="sxs-lookup"><span data-stu-id="50cef-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="50cef-188">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50cef-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="50cef-189">Путь к *вашему .dll* обычно является папкой *бен* в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="50cef-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="50cef-190">Эта команда создает файл под названием *server.js* в той же папке *с signalr.exe.*</span><span class="sxs-lookup"><span data-stu-id="50cef-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="50cef-191">Поместите файл *server.js* в соответствующую папку в проекте, переименуйте его по мере необходимости для приложения и добавьте ссылку на него вместо ссылки "сигнал"/концентраторы" ссылки.</span><span class="sxs-lookup"><span data-stu-id="50cef-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="50cef-192">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="50cef-192">How to establish a connection</span></span>

<span data-ttu-id="50cef-193">Прежде чем установить соединение, необходимо создать объект соединения, создать прокси-сервер и зарегистрировать обработчики событий для методов, которые можно вызвать с сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="50cef-194">При настройке обработчиков прокси и событий установите соединение, вызывая `start` метод.</span><span class="sxs-lookup"><span data-stu-id="50cef-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="50cef-195">Если вы используете сгенерированный прокси-сервер, вам не нужно создавать объект соединения в своем собственном коде, потому что сгенерированный прокси-код делает это за вас.</span><span class="sxs-lookup"><span data-stu-id="50cef-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="50cef-196">**Установить соединение (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="50cef-197">**Установить соединение (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="50cef-198">Пример кода использует URL-адрес по умолчанию "/сигнальщик" для подключения к службе SignalR.</span><span class="sxs-lookup"><span data-stu-id="50cef-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="50cef-199">Для получения информации о том, как указать другой базовый URL, см [ASP.NET.](hubs-api-guide-server.md#signalrurl)</span><span class="sxs-lookup"><span data-stu-id="50cef-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="50cef-200">По умолчанию местоположение концентратора является текущим сервером; если вы подключаетесь к другому серверу, укажите URL перед вызовом метода, `start` как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="50cef-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="50cef-201">Обычно вы регистрируете обработчики событий перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="50cef-202">Если вы хотите зарегистрировать некоторые обработчики событий после установления соединения, вы можете сделать это, но `start` вы должны зарегистрировать по крайней мере один из обработчика событий (ы) перед вызовом метода.</span><span class="sxs-lookup"><span data-stu-id="50cef-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="50cef-203">Одной из причин этого является то, что в приложении может быть много `OnConnected` концентратов, но вы не хотели бы запускать событие в каждом концентраторе, если вы собираетесь использовать только один из них.</span><span class="sxs-lookup"><span data-stu-id="50cef-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="50cef-204">Когда соединение установлено, наличие метода клиента на прокси концентратора является `OnConnected` то, что говорит SignalR, чтобы вызвать событие.</span><span class="sxs-lookup"><span data-stu-id="50cef-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="50cef-205">Если вы не зарегистрируете обработчики событий перед вызовом `start` метода, вы сможете вызвать `OnConnected` методы на концентраторе, но метод концентратора не будет вызываться, и никакие клиентские методы не будут вызываться с сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="50cef-206">$.connection.hub - это тот же объект, который создает $.hubConnection()</span><span class="sxs-lookup"><span data-stu-id="50cef-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="50cef-207">Как вы можете видеть на примерах, при `$.connection.hub` использовании генерируемого прокси относится к объекту соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="50cef-208">Это тот же объект, который `$.hubConnection()` вы получаете, позвонив, когда вы не используете сгенерированный прокси.</span><span class="sxs-lookup"><span data-stu-id="50cef-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="50cef-209">Сгенерированный прокси-код создает соединение для вас, выполняя следующее утверждение:</span><span class="sxs-lookup"><span data-stu-id="50cef-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Создание соединения в генерируемом файле прокси](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="50cef-211">Когда вы используете сгенерированный прокси, `$.connection.hub` вы можете сделать что-нибудь с тем, что вы можете сделать с объектом соединения, когда вы не используете сгенерированный прокси.</span><span class="sxs-lookup"><span data-stu-id="50cef-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="50cef-212">Асинхронное выполнение метода старта</span><span class="sxs-lookup"><span data-stu-id="50cef-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="50cef-213">Метод `start` выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="50cef-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="50cef-214">Он возвращает [объект j's'ry Отложенный,](http://api.jquery.com/category/deferred-object/)что означает, что вы `pipe`можете `done`добавить функции обратного вызова, такие как , и `fail`.</span><span class="sxs-lookup"><span data-stu-id="50cef-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="50cef-215">Если у вас есть код, который вы хотите выполнить после создания соединения, например, вызов на сервер, поместите этот код в функцию обратного вызова или позвоните ему из функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="50cef-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="50cef-216">Метод `.done` обратного вызова выполняется после создания соединения, и после того, `OnConnected` как любой код, который у вас есть в методе обработчика событий на сервере, завершает выполнение.</span><span class="sxs-lookup"><span data-stu-id="50cef-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="50cef-217">Если вы поместите заявление "Now connected" из предыдущего примера в качестве следующей строки кода после вызова `start` метода (не в обратном `.done` деле), `console.log` строка будет выполняться до создания соединения, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="50cef-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Неправильный способ записи кода, который работает после установления соединения](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="50cef-219">Как установить кросс-доменсоединение</span><span class="sxs-lookup"><span data-stu-id="50cef-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="50cef-220">Обычно, если браузер загружает страницу с `http://contoso.com`, соединение `http://contoso.com/signalr`SignalR находится в том же домене, в .</span><span class="sxs-lookup"><span data-stu-id="50cef-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="50cef-221">Если страница `http://contoso.com` из делает `http://fabrikam.com/signalr`подключение к, то есть кросс-домен соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="50cef-222">По соображениям безопасности соединения кросс-домена отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="50cef-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="50cef-223">В SignalR 1.x запросы на перекрестный домен контролировались одним флагом EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="50cef-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="50cef-224">Этот флаг контролировал запросы JSONP и CORS.</span><span class="sxs-lookup"><span data-stu-id="50cef-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="50cef-225">Для большей гибкости вся поддержка CORS была удалена из серверного компонента SignalR (клиенты JavaScript по-прежнему используют CORS обычно, если обнаруживается, что браузер поддерживает его), и для поддержки этих сценариев было предоставлено новое промежуточное программное обеспечение OWIN.</span><span class="sxs-lookup"><span data-stu-id="50cef-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="50cef-226">Если JSONP требуется для клиента (для поддержки запросов кросс-домена в старых `EnableJSONP` браузерах), он должен быть включен явно, установив на `HubConfiguration` объекте, как `true`показано ниже.</span><span class="sxs-lookup"><span data-stu-id="50cef-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="50cef-227">JSONP отключен по умолчанию, так как он менее безопасен, чем CORS.</span><span class="sxs-lookup"><span data-stu-id="50cef-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="50cef-228">**Добавление В свой проект Microsoft.Owin.Cors:** Чтобы установить эту библиотеку, запустите следующую команду в консоли менеджера пакетов:</span><span class="sxs-lookup"><span data-stu-id="50cef-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="50cef-229">Эта команда добавит версию пакета 2.1.0 в проект.</span><span class="sxs-lookup"><span data-stu-id="50cef-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="50cef-230">Вызов UseCors</span><span class="sxs-lookup"><span data-stu-id="50cef-230">Calling UseCors</span></span>

 <span data-ttu-id="50cef-231">Следующий фрагмент кода демонстрирует, как реализовать соединения кросс-домена в SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="50cef-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="50cef-232">**Реализация запросов кросс-домена в SignalR 2**</span><span class="sxs-lookup"><span data-stu-id="50cef-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="50cef-233">Следующий код показывает, как включить CORS или JSONP в проекте SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="50cef-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="50cef-234">Этот образец `Map` `RunSignalR` кода `MapSignalR`использует и вместо , так что CORS промежуточное программное обеспечение работает только для `MapSignalR`запросов SignalR, которые требуют поддержки CORS (а не для всего трафика на пути, указанном в .) Карта также может быть использована для любого другого промежуточного посуды, которая должна работать для конкретного приставки URL, а не для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="50cef-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="50cef-235">Не устанавливайте `jQuery.support.cors` к истине в вашем коде.</span><span class="sxs-lookup"><span data-stu-id="50cef-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![Не устанавливайте j'sry.support.cors на истину](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="50cef-237">SignalR обрабатывает использование CORS.</span><span class="sxs-lookup"><span data-stu-id="50cef-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="50cef-238">Установка `jQuery.support.cors` на истинное отскакивает JSONP, потому что это заставляет SignalR предположить, что браузер поддерживает CORS.</span><span class="sxs-lookup"><span data-stu-id="50cef-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="50cef-239">При подключении к URL-адресу localhost Internet Explorer 10 не будет считать его кросс-доменом, поэтому приложение будет работать локально с IE 10, даже если вы не включили кросс-доменсоединения на сервере.</span><span class="sxs-lookup"><span data-stu-id="50cef-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="50cef-240">Для получения информации об использовании кросс-доменных соединений с Internet Explorer 9, [см.](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)</span><span class="sxs-lookup"><span data-stu-id="50cef-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="50cef-241">Для получения информации об использовании кросс-доменсоединений с Chrome, [см.](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)</span><span class="sxs-lookup"><span data-stu-id="50cef-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="50cef-242">Пример кода использует URL-адрес по умолчанию "/сигнальщик" для подключения к службе SignalR.</span><span class="sxs-lookup"><span data-stu-id="50cef-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="50cef-243">Для получения информации о том, как указать другой базовый URL, см [ASP.NET.](hubs-api-guide-server.md#signalrurl)</span><span class="sxs-lookup"><span data-stu-id="50cef-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="50cef-244">Как настроить соединение</span><span class="sxs-lookup"><span data-stu-id="50cef-244">How to configure the connection</span></span>

<span data-ttu-id="50cef-245">Прежде чем установить соединение, можно указать параметры строки запроса или указать метод транспортировки.</span><span class="sxs-lookup"><span data-stu-id="50cef-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="50cef-246">Как указать параметры строки запроса</span><span class="sxs-lookup"><span data-stu-id="50cef-246">How to specify query string parameters</span></span>

<span data-ttu-id="50cef-247">Если вы хотите отправить данные на сервер при подключении клиента, можно добавить параметры строки запроса к объекту соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="50cef-248">Ниже приведены следующие примеры, как установить параметр строки запроса в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="50cef-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="50cef-249">**Установите значение строки запроса перед вызовом метода запуска (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="50cef-250">**Установите значение строки запроса перед вызовом метода запуска (без сгенерированного прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="50cef-251">В следующем примере показано, как прочитать параметр строки запроса в коде сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="50cef-252">Как указать транспортный метод</span><span class="sxs-lookup"><span data-stu-id="50cef-252">How to specify the transport method</span></span>

<span data-ttu-id="50cef-253">В процессе подключения клиент SignalR обычно ведет переговоры с сервером, чтобы определить наилучший транспорт, который поддерживается как сервером, так и клиентом.</span><span class="sxs-lookup"><span data-stu-id="50cef-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="50cef-254">Если вы уже знаете, какой транспорт вы хотите использовать, вы можете обойти этот `start` процесс переговоров, указав метод транспортировки при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="50cef-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="50cef-255">**Код клиента, который определяет способ транспортировки (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="50cef-256">**Код клиента, который определяет способ транспортировки (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="50cef-257">В качестве альтернативы можно указать несколько методов транспортировки в порядке, в котором вы хотите SignalR попробовать их:</span><span class="sxs-lookup"><span data-stu-id="50cef-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="50cef-258">**Код клиента, который определяет пользовательскую схему резервного копирования транспорта (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="50cef-259">**Код клиента, который определяет пользовательскую схему резервного копирования транспорта (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="50cef-260">Для указания метода транспортировки можно использовать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="50cef-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="50cef-261">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="50cef-261">"webSockets"</span></span>
- <span data-ttu-id="50cef-262">"навсегдаФрейм"</span><span class="sxs-lookup"><span data-stu-id="50cef-262">"foreverFrame"</span></span>
- <span data-ttu-id="50cef-263">"серверСентСобытия"</span><span class="sxs-lookup"><span data-stu-id="50cef-263">"serverSentEvents"</span></span>
- <span data-ttu-id="50cef-264">"ДлинныйОпрос"</span><span class="sxs-lookup"><span data-stu-id="50cef-264">"longPolling"</span></span>

<span data-ttu-id="50cef-265">Ниже приведены следующие примеры, как узнать, какой способ транспортировки используется соединением.</span><span class="sxs-lookup"><span data-stu-id="50cef-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="50cef-266">**Клиентский код, отображающие транспортный метод, используемый соединением (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="50cef-267">**Клиентский код, отображающие транспортный метод, используемый соединением (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="50cef-268">Подробнее о том, как проверить метод транспортировки в серверном коде, смотрите [ASP.NET Руководство по aPI SignalR Hubs API - Server - Как получить информацию о клиенте из свойства Контекста.](hubs-api-guide-server.md#contextproperty)</span><span class="sxs-lookup"><span data-stu-id="50cef-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="50cef-269">Для получения дополнительной информации о транспорте и откатов, [см. Введение в SignalR - Транспорт и Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="50cef-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="50cef-270">Как получить прокси для класса концентратор</span><span class="sxs-lookup"><span data-stu-id="50cef-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="50cef-271">Каждый объект соединения, который создается, инкапсулирует информацию о подключении к службе SignalR, содержащей один или несколько классов концентраторов.</span><span class="sxs-lookup"><span data-stu-id="50cef-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="50cef-272">Для связи с классом концентратора используется прокси-объект, который вы создаете самостоятельно (если вы не используете сгенерированный прокси) или который генерируется для вас.</span><span class="sxs-lookup"><span data-stu-id="50cef-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="50cef-273">На клиенте прокси-имя — это верблюжья версия названия класса Концентратор.</span><span class="sxs-lookup"><span data-stu-id="50cef-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="50cef-274">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать конвенциям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="50cef-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="50cef-275">**Класс концентратора на сервере**</span><span class="sxs-lookup"><span data-stu-id="50cef-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="50cef-276">**Получить ссылку на сгенерированный прокси клиента для концентратора**</span><span class="sxs-lookup"><span data-stu-id="50cef-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="50cef-277">**Создание клиентского прокси для класса концентратора (без сгенерированного прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="50cef-278">Если вы украсите `HubName` свой класс концентратора атрибутом, используйте точное имя, не меняя чехол.</span><span class="sxs-lookup"><span data-stu-id="50cef-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="50cef-279">**Класс концентратора на сервере с атрибутом HubName**</span><span class="sxs-lookup"><span data-stu-id="50cef-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="50cef-280">**Получить ссылку на сгенерированный прокси клиента для концентратора**</span><span class="sxs-lookup"><span data-stu-id="50cef-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="50cef-281">**Создание клиентского прокси для класса концентратора (без сгенерированного прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="50cef-282">Как определить методы на клиенте, который может вызвать сервер</span><span class="sxs-lookup"><span data-stu-id="50cef-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="50cef-283">Чтобы определить метод, который сервер может вызвать из концентратора, `client` добавьте обработчик событий `on` в прокси-сервер концентратора, используя свойство генерируемого прокси, или позвоните по этому методу, если вы не используете генерируемый прокси.</span><span class="sxs-lookup"><span data-stu-id="50cef-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="50cef-284">Параметры могут быть сложными объектами.</span><span class="sxs-lookup"><span data-stu-id="50cef-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="50cef-285">До вызова метода `start` для установления соединения добавьте обработчик события.</span><span class="sxs-lookup"><span data-stu-id="50cef-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="50cef-286">(Если вы хотите добавить обработчики событий после вызова `start` метода, см. заметку в Как [установить соединение](#establishconnection) ранее в этом документе, и использовать синтаксис, показанный для определения метода без использования генерируемого прокси.)</span><span class="sxs-lookup"><span data-stu-id="50cef-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="50cef-287">Сопоставление имен метода является нечувствительным.</span><span class="sxs-lookup"><span data-stu-id="50cef-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="50cef-288">Например, `Clients.All.addContosoChatMessageToPage` на сервере `AddContosoChatMessageToPage` `addContosoChatMessageToPage`будет `addcontosochatmessagetopage` выполняться, или на клиенте.</span><span class="sxs-lookup"><span data-stu-id="50cef-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="50cef-289">**Определение метода на клиенте (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="50cef-290">**Альтернативный способ определения метода на клиенте (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="50cef-291">**Определите метод на клиенте (без сгенерированного прокси или при добавлении после вызова метода запуска)**</span><span class="sxs-lookup"><span data-stu-id="50cef-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="50cef-292">**Код сервера, который вызывает метод клиента**</span><span class="sxs-lookup"><span data-stu-id="50cef-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="50cef-293">Следующие примеры включают сложный объект в качестве параметра метода.</span><span class="sxs-lookup"><span data-stu-id="50cef-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="50cef-294">**Определение метода на клиенте, который принимает сложный объект (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="50cef-295">**Определение метода по клиенту, который принимает сложный объект (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="50cef-296">**Код сервера, определяющий сложный объект**</span><span class="sxs-lookup"><span data-stu-id="50cef-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="50cef-297">**Код сервера, который вызывает метод клиента с помощью сложного объекта**</span><span class="sxs-lookup"><span data-stu-id="50cef-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="50cef-298">Как вызвать методы сервера от клиента</span><span class="sxs-lookup"><span data-stu-id="50cef-298">How to call server methods from the client</span></span>

<span data-ttu-id="50cef-299">Чтобы вызвать метод сервера от `server` клиента, используйте `invoke` свойство генерируемого прокси или метод на прокси-концентраторе, если вы не используете сгенерированный прокси.</span><span class="sxs-lookup"><span data-stu-id="50cef-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="50cef-300">Значение возврата или параметры могут быть сложными объектами.</span><span class="sxs-lookup"><span data-stu-id="50cef-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="50cef-301">Передайте в верблюжьем корпусе версию названия метода на концентраторе.</span><span class="sxs-lookup"><span data-stu-id="50cef-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="50cef-302">SignalR автоматически вносит это изменение, чтобы код JavaScript мог соответствовать конвенциям JavaScript.</span><span class="sxs-lookup"><span data-stu-id="50cef-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="50cef-303">Ниже приведены приведенные примеры, как вызвать метод сервера, который не имеет значения возврата, и как вызвать метод сервера, который имеет значение возврата.</span><span class="sxs-lookup"><span data-stu-id="50cef-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="50cef-304">**Метод сервера без атрибута HubMethodName**</span><span class="sxs-lookup"><span data-stu-id="50cef-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="50cef-305">**Код сервера, определяющий сложный объект, передаваемый в параметре**</span><span class="sxs-lookup"><span data-stu-id="50cef-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="50cef-306">**Клиентский код, который вызывает метод сервера (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="50cef-307">**Клиентский код, который вызывает метод сервера (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="50cef-308">Если вы украсили `HubMethodName` метод концентратора атрибутом, используйте это имя без изменения случая.</span><span class="sxs-lookup"><span data-stu-id="50cef-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="50cef-309">**Метод сервера** с атрибутом HubMethodName</span><span class="sxs-lookup"><span data-stu-id="50cef-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="50cef-310">**Клиентский код, который вызывает метод сервера (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="50cef-311">**Клиентский код, который вызывает метод сервера (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="50cef-312">Предыдущие примеры показывают, как вызвать метод сервера, не имеющий значения возврата.</span><span class="sxs-lookup"><span data-stu-id="50cef-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="50cef-313">Ниже приведены приведенные примеры, как вызвать метод сервера с обратным значением.</span><span class="sxs-lookup"><span data-stu-id="50cef-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="50cef-314">**Код сервера для метода, который имеет значение возврата**</span><span class="sxs-lookup"><span data-stu-id="50cef-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="50cef-315">**Класс акции, используемый для** значения возврата</span><span class="sxs-lookup"><span data-stu-id="50cef-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="50cef-316">**Клиентский код, который вызывает метод сервера (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="50cef-317">**Клиентский код, который вызывает метод сервера (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="50cef-318">Как обрабатывать события жизни соединения</span><span class="sxs-lookup"><span data-stu-id="50cef-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="50cef-319">SignalR предоставляет следующие события жизни соединения, которые вы можете обрабатывать:</span><span class="sxs-lookup"><span data-stu-id="50cef-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="50cef-320">`starting`: Поднятые перед отправкой данных по подключению.</span><span class="sxs-lookup"><span data-stu-id="50cef-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="50cef-321">`received`: Поднятыпри получать какие-либо данные о подключении.</span><span class="sxs-lookup"><span data-stu-id="50cef-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="50cef-322">Предоставляет полученные данные.</span><span class="sxs-lookup"><span data-stu-id="50cef-322">Provides the received data.</span></span>
- <span data-ttu-id="50cef-323">`connectionSlow`: Поднят, когда клиент обнаруживает медленное или часто падающее соединение.</span><span class="sxs-lookup"><span data-stu-id="50cef-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="50cef-324">`reconnecting`: Поднятый, когда базовый транспорт начинает воссоединение.</span><span class="sxs-lookup"><span data-stu-id="50cef-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="50cef-325">`reconnected`: Поднятый при повторном подключении основного транспорта.</span><span class="sxs-lookup"><span data-stu-id="50cef-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="50cef-326">`stateChanged`: Поднят при изменении состояния соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="50cef-327">Обеспечивает старое состояние и новое состояние (подключение, подключение, воссоединение или отключение).</span><span class="sxs-lookup"><span data-stu-id="50cef-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="50cef-328">`disconnected`: Поднят освоено при отключении соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="50cef-329">Например, если вы хотите отображать предупреждающие сообщения при возникновении проблем `connectionSlow` с подключением, которые могут привести к заметным задержкам, свяжетесь с событием.</span><span class="sxs-lookup"><span data-stu-id="50cef-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="50cef-330">**Обработка события connectionSlow (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="50cef-331">**Обработка события connectionSlow (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="50cef-332">Для получения дополнительной информации, см [Понимание и обработка подключения Пожизненные события в SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="50cef-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="50cef-333">Как обрабатывать ошибки</span><span class="sxs-lookup"><span data-stu-id="50cef-333">How to handle errors</span></span>

<span data-ttu-id="50cef-334">Клиент SignalR JavaScript `error` предоставляет событие, для которого можно добавить обработчик.</span><span class="sxs-lookup"><span data-stu-id="50cef-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="50cef-335">Можно также использовать метод сбоя для добавления обработчика для ошибок, которые являются результатом вызова метода сервера.</span><span class="sxs-lookup"><span data-stu-id="50cef-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="50cef-336">Если вы явно не включаете подробные сообщения об ошибке на сервере, объект исключения, который возвращает SignalR после ошибки, содержит минимальную информацию об ошибке.</span><span class="sxs-lookup"><span data-stu-id="50cef-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="50cef-337">Например, если вызов `newContosoChatMessage` не удается, сообщение об`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`ошибке в объекте ошибки содержит " Отправка подробных сообщений об ошибках клиентам в производственной сфере не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.</span><span class="sxs-lookup"><span data-stu-id="50cef-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="50cef-338">В следующем примере показано, как добавить обработчик для события ошибки.</span><span class="sxs-lookup"><span data-stu-id="50cef-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="50cef-339">**Добавить обработчик ошибок (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="50cef-340">**Добавить обработчик ошибок (без сгенерированного прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="50cef-341">В следующем примере показано, как обрабатывать ошибку из вызова метода.</span><span class="sxs-lookup"><span data-stu-id="50cef-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="50cef-342">**Обработка ошибки от вызова метода (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="50cef-343">**Обработка ошибки от вызова метода (без сгенерированного прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="50cef-344">Если вызов метода не `error` удается, событие также поднимается, поэтому ваш код в обработчике `error` метода и в обратном `.fail` вызове метода будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="50cef-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="50cef-345">Как включить журналирование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="50cef-345">How to enable client-side logging</span></span>

<span data-ttu-id="50cef-346">Чтобы включить систему входа в систему на стороне клиента на соединение, установите `logging` свойство на объекте соединения перед вызовом метода `start` для установления соединения.</span><span class="sxs-lookup"><span data-stu-id="50cef-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="50cef-347">**Включить журнал (с генерируемым прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="50cef-348">**Включить журнал (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="50cef-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="50cef-349">Чтобы увидеть журналы, откройте инструменты разработчика браузера и перейдите на вкладку Console. Для учебника, который показывает пошаговые инструкции и скриншоты, которые показывают, как это сделать, см [ASP.NET.](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)</span><span class="sxs-lookup"><span data-stu-id="50cef-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
