---
uid: signalr/overview/older-versions/troubleshooting
title: Устранение неполадок SignalR (SignalR 1.x) Документы Майкрософт
author: bradygaster
description: В этой статье описаны общие проблемы с разработкой приложений SignalR.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543097"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="71355-103">Устранение неполадок SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="71355-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="71355-104">[Патрик Флетчер](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="71355-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="71355-105">В этом документе описаны общие проблемы устранения неполадок с SignalR.</span><span class="sxs-lookup"><span data-stu-id="71355-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="71355-106">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="71355-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="71355-107">Методы вызова между клиентом и сервером бесшумно не удается</span><span class="sxs-lookup"><span data-stu-id="71355-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="71355-108">Другие проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="71355-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="71355-109">Компиляция и ошибки на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="71355-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="71355-110">Вопросы визуальной студии</span><span class="sxs-lookup"><span data-stu-id="71355-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="71355-111">Вопросы, связанные с информационными услугами Интернета</span><span class="sxs-lookup"><span data-stu-id="71355-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="71355-112">Проблемы Azure</span><span class="sxs-lookup"><span data-stu-id="71355-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="71355-113">Методы вызова между клиентом и сервером бесшумно не удается</span><span class="sxs-lookup"><span data-stu-id="71355-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="71355-114">В этом разделе описаны возможные причины сбоя вызова метода между клиентом и сервером без значимого сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="71355-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="71355-115">В приложении SignalR сервер не имеет информации о методах, которые реализует клиент; когда сервер ссылается на метод клиента, имя метода и данные параметров отправляются клиенту, а метод выполняется только в том случае, если он существует в формате, указанном сервером.</span><span class="sxs-lookup"><span data-stu-id="71355-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="71355-116">Если на клиенте нет способа сопоставления, ничего не происходит, и сообщение об ошибке не поднимается на сервере.</span><span class="sxs-lookup"><span data-stu-id="71355-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="71355-117">Для дальнейшего изучения методов клиента, не вызываемых, можно включить журнал, прежде чем вызвать метод запуска на концентраторе, чтобы узнать, какие вызовы поступают с сервера.</span><span class="sxs-lookup"><span data-stu-id="71355-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="71355-118">Чтобы включить журнал в приложении JavaScript, [см. Как включить журнал клиентов (клиентская версия JavaScript)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="71355-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="71355-119">Чтобы включить вход в клиентское приложение .NET, [см. Как включить журнал клиентов (.NET Клиентская версия)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="71355-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="71355-120">Метод неправильного проработки, неправильная подпись метода или неправильное название концентратора</span><span class="sxs-lookup"><span data-stu-id="71355-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="71355-121">Если имя или подпись вызываемого метода точно не совпадают с соответствующим методом клиента, вызов завершится неудачей.</span><span class="sxs-lookup"><span data-stu-id="71355-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="71355-122">Убедитесь, что имя метода, вызванное сервером, совпадает с именем метода на клиенте.</span><span class="sxs-lookup"><span data-stu-id="71355-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="71355-123">Кроме того, SignalR создает прокси-концентратор, используя методы верблюжьего `SendMessage` корпуса, как `sendMessage` это уместно в JavaScript, поэтому метод, вызванный на сервер, будет вызываться в клиентском прокси.</span><span class="sxs-lookup"><span data-stu-id="71355-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="71355-124">Если вы `HubName` используете атрибут в коде сервера, убедитесь, что используемое имя соответствует имени, используемому для создания концентратора клиента.</span><span class="sxs-lookup"><span data-stu-id="71355-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="71355-125">Если вы не `HubName` используете атрибут, убедитесь, что имя концентратора в клиенте JavaScript является случаем верблюда, например, chatHub вместо ChatHub.</span><span class="sxs-lookup"><span data-stu-id="71355-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="71355-126">Двойное имя метода на клиенте</span><span class="sxs-lookup"><span data-stu-id="71355-126">Duplicate method name on client</span></span>

<span data-ttu-id="71355-127">Убедитесь, что у вас нет дубликата метода на клиенте, который отличается только в зависимости от случая.</span><span class="sxs-lookup"><span data-stu-id="71355-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="71355-128">Если в клиентском приложении есть метод, называемый, `sendMessage` `SendMessage` убедитесь, что не существует также метода, называемого также.</span><span class="sxs-lookup"><span data-stu-id="71355-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="71355-129">Пропавший парсер JSON на клиенте</span><span class="sxs-lookup"><span data-stu-id="71355-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="71355-130">SignalR требует присутствия parser JSON для сериализации звонков между сервером и клиентом.</span><span class="sxs-lookup"><span data-stu-id="71355-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="71355-131">Если у вашего клиента нет встроенного парора JSON (например, Internet Explorer 7), его необходимо включить в приложение.</span><span class="sxs-lookup"><span data-stu-id="71355-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="71355-132">Вы можете скачать Parser JSON [здесь](http://nuget.org/packages/json2).</span><span class="sxs-lookup"><span data-stu-id="71355-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="71355-133">Смешивание концентратора и синтаксиса PersistentConnection</span><span class="sxs-lookup"><span data-stu-id="71355-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="71355-134">SignalR использует две коммуникационные модели: концентраторы и стойкие соединения.</span><span class="sxs-lookup"><span data-stu-id="71355-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="71355-135">Синтаксис для вызова этих двух моделей связи отличается в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="71355-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="71355-136">Если вы добавили концентратор в код сервера, убедитесь, что весь ваш клиентский код использует соответствующий синтаксис концентратора.</span><span class="sxs-lookup"><span data-stu-id="71355-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="71355-137">**Клиентский код JavaScript, создающий постоянноеподключение в клиенте JavaScript**</span><span class="sxs-lookup"><span data-stu-id="71355-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="71355-138">**Клиентский код JavaScript, создающий прокси-сервер концентратора в клиенте Javascript**</span><span class="sxs-lookup"><span data-stu-id="71355-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="71355-139">**Серверный код C', который отображает маршрут к постоянному подключению**</span><span class="sxs-lookup"><span data-stu-id="71355-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="71355-140">**Серверный код C,c, который отображает маршрут к концентратору или нескольким концентратам, если у вас есть несколько приложений**</span><span class="sxs-lookup"><span data-stu-id="71355-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="71355-141">Подключение началось до добавления подписки</span><span class="sxs-lookup"><span data-stu-id="71355-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="71355-142">Если подключение концентратора запущено до того, как методы, которые можно вызвать с сервера, будут добавлены к прокси-, сообщения не будут получены.</span><span class="sxs-lookup"><span data-stu-id="71355-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="71355-143">Следующий код JavaScript не запустит концентратор должным образом:</span><span class="sxs-lookup"><span data-stu-id="71355-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="71355-144">**Неправильный клиентский код JavaScript, который не позволит получать сообщения концентратов**</span><span class="sxs-lookup"><span data-stu-id="71355-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="71355-145">Вместо этого добавьте подписку на метод перед вызовом Start:</span><span class="sxs-lookup"><span data-stu-id="71355-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="71355-146">**Клиентский код JavaScript, который правильно добавляет подписки в концентратор**</span><span class="sxs-lookup"><span data-stu-id="71355-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="71355-147">Отсутствует имя метода на прокси-сервере концентратора</span><span class="sxs-lookup"><span data-stu-id="71355-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="71355-148">Убедитесь, что метод, определенный на сервере, подписан на клиента.</span><span class="sxs-lookup"><span data-stu-id="71355-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="71355-149">Несмотря на то, что сервер определяет метод, он все равно должен быть добавлен в прокси-сервер клиента.</span><span class="sxs-lookup"><span data-stu-id="71355-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="71355-150">Методы могут быть добавлены в прокси клиента следующим образом (обратите `client` внимание, что метод добавляется к члену концентратора непосредственно):</span><span class="sxs-lookup"><span data-stu-id="71355-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="71355-151">**Клиентский код JavaScript, который добавляет методы в прокси-сервер концентратора**</span><span class="sxs-lookup"><span data-stu-id="71355-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="71355-152">Методы концентратора или концентратора, не объявленные общедоступными</span><span class="sxs-lookup"><span data-stu-id="71355-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="71355-153">Чтобы быть видимым на клиенте, реализация концентратора и методы должны быть объявлены как. `public`</span><span class="sxs-lookup"><span data-stu-id="71355-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="71355-154">Доступ концентратора из другого приложения</span><span class="sxs-lookup"><span data-stu-id="71355-154">Accessing hub from a different application</span></span>

<span data-ttu-id="71355-155">Доступ к концентрам SignalR можно получить только через приложения, реализующие клиентов SignalR.</span><span class="sxs-lookup"><span data-stu-id="71355-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="71355-156">SignalR не может сотрудничать с другими библиотеками связи (например, С веб-сервисами SOAP или WCF). Если для вашей целевой платформы нет клиента SignalR, вы не можете получить прямой доступ к конечному моменту сервера.</span><span class="sxs-lookup"><span data-stu-id="71355-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="71355-157">Ручной сериализации данных</span><span class="sxs-lookup"><span data-stu-id="71355-157">Manually serializing data</span></span>

<span data-ttu-id="71355-158">SignalR будет автоматически использовать JSON для сериализации параметров вашего метода - нет необходимости делать это самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="71355-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="71355-159">Метод удаленного концентратора не выполняется на клиенте в функции OnDisconnected</span><span class="sxs-lookup"><span data-stu-id="71355-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="71355-160">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-160">This behavior is by design.</span></span> <span data-ttu-id="71355-161">При `OnDisconnected` вызове концентратор `Disconnected` уже вошел в состояние, что не позволяет вызывать дальнейшие методы концентратора.</span><span class="sxs-lookup"><span data-stu-id="71355-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="71355-162">**Код сервера C,C, который правильно выполняет код в событии OnDisconnected**</span><span class="sxs-lookup"><span data-stu-id="71355-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="71355-163">Ограничение подключения достигнуто</span><span class="sxs-lookup"><span data-stu-id="71355-163">Connection limit reached</span></span>

<span data-ttu-id="71355-164">При использовании полной версии IIS на клиентской операционной системе, такой как Windows 7, вводится ограничение на подключение в 10.</span><span class="sxs-lookup"><span data-stu-id="71355-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="71355-165">При использовании клиентской ОС, вместо этого используйте IIS Express, чтобы избежать этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="71355-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="71355-166">Кросс-доменное соединение не настроено должным образом</span><span class="sxs-lookup"><span data-stu-id="71355-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="71355-167">Если соединение кросс-домена (соединение, для которого URL SignalR не находится в том же домене, что и страница хостинга) настроено неправильно, соединение может выйти из строя без сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="71355-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="71355-168">Для получения информации о том, как включить кросс-домен связи, см [Как установить кросс-домен соединение](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="71355-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="71355-169">Подключение с использованием NTLM (Active Directory) не работает в клиенте .NET</span><span class="sxs-lookup"><span data-stu-id="71355-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="71355-170">Подключение в клиентском приложении .NET, используюваесебя безопасность домена, может выработать сядек, если соединение не настроено должным образом.</span><span class="sxs-lookup"><span data-stu-id="71355-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="71355-171">Чтобы использовать SignalR в среде домена, установите необходимое свойство подключения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="71355-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="71355-172">**Клиентский код C', реализуемый учетные данные соединения**</span><span class="sxs-lookup"><span data-stu-id="71355-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="71355-173">Другие проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="71355-173">Other connection issues</span></span>

<span data-ttu-id="71355-174">В этом разделе описаны причины и решения для конкретных симптомов или сообщений об ошибках, которые возникают во время соединения.</span><span class="sxs-lookup"><span data-stu-id="71355-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="71355-175">Ошибка "Старт должен быть вызван до отправки данных"</span><span class="sxs-lookup"><span data-stu-id="71355-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="71355-176">Эта ошибка обычно видна, если код ссылается на объекты SignalR до начала соединения.</span><span class="sxs-lookup"><span data-stu-id="71355-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="71355-177">Проводная связь для обработчиков и тому подобное вызовет методы, определенные на сервере, должны быть добавлены после завершения соединения.</span><span class="sxs-lookup"><span data-stu-id="71355-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="71355-178">Обратите внимание, `Start` что вызов является асинхронным, поэтому код после вызова может быть выполнен до его завершения.</span><span class="sxs-lookup"><span data-stu-id="71355-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="71355-179">Лучший способ добавить обработчики после полного подключения — поместить их в функцию обратного вызова, которая передается в качестве параметра методу запуска:</span><span class="sxs-lookup"><span data-stu-id="71355-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="71355-180">**Клиентский код JavaScript, который правильно добавляет обработчики событий, которые ссылаются на объекты SignalR**</span><span class="sxs-lookup"><span data-stu-id="71355-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="71355-181">Эта ошибка также будет видна, если соединение останавливается, в то время как объекты SignalR все еще ссылаются.</span><span class="sxs-lookup"><span data-stu-id="71355-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="71355-182">Ошибка "301 Перемещено постоянно" или "302 перемещенвременно"</span><span class="sxs-lookup"><span data-stu-id="71355-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="71355-183">Эта ошибка может быть замечена, если проект содержит папку под названием SignalR, которая будет мешать автоматически созданного прокси.</span><span class="sxs-lookup"><span data-stu-id="71355-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="71355-184">Чтобы избежать этой ошибки, не `SignalR` используйте папку, называемую в приложении, или выключите автоматическое генерирование прокси.</span><span class="sxs-lookup"><span data-stu-id="71355-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="71355-185">Для получения более подробной информации [ознакомьтесь с The Generated Proxy и тем, что он делает для вас.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)</span><span class="sxs-lookup"><span data-stu-id="71355-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="71355-186">Ошибка "403 Запрещена" в клиенте .NET или Silverlight</span><span class="sxs-lookup"><span data-stu-id="71355-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="71355-187">Эта ошибка может произойти в средах кросс-домена, где связь между доменами не включена должным образом.</span><span class="sxs-lookup"><span data-stu-id="71355-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="71355-188">Для получения информации о том, как включить кросс-домен связи, см [Как установить кросс-домен соединение](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="71355-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="71355-189">Чтобы установить кросс-домен соединение в клиенте Silverlight, [см.](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)</span><span class="sxs-lookup"><span data-stu-id="71355-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="71355-190">Ошибка "404 не найдена"</span><span class="sxs-lookup"><span data-stu-id="71355-190">"404 Not Found" error</span></span>

<span data-ttu-id="71355-191">Есть несколько причин для этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="71355-191">There are several causes for this issue.</span></span> <span data-ttu-id="71355-192">Проверить все следующие:</span><span class="sxs-lookup"><span data-stu-id="71355-192">Verify all of the following:</span></span>

- <span data-ttu-id="71355-193">**Ссылка на прокси-адрес концентратора не отформатирована правильно:** Эта ошибка обычно видна, если ссылка на сгенерированный прокси-адрес концентратора не отформатирована правильно.</span><span class="sxs-lookup"><span data-stu-id="71355-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="71355-194">Убедитесь, что ссылка на адрес концентратора сделана должным образом.</span><span class="sxs-lookup"><span data-stu-id="71355-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="71355-195">Узнайте, как ссылаться на [динамически сгенерированный прокси](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) для получения подробной информации.</span><span class="sxs-lookup"><span data-stu-id="71355-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="71355-196">**Добавление маршрутов в приложение перед добавлением маршрута концентратора:** Если приложение использует другие маршруты, убедитесь, `MapHubs`что первый добавленный маршрут является вызовом.</span><span class="sxs-lookup"><span data-stu-id="71355-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="71355-197">"500 Внутренняя ошибка сервера"</span><span class="sxs-lookup"><span data-stu-id="71355-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="71355-198">Это очень общая ошибка, которая может иметь широкий спектр причин.</span><span class="sxs-lookup"><span data-stu-id="71355-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="71355-199">Детали ошибки должны отображаться в журнале событий сервера или могут быть найдены при отладке сервера.</span><span class="sxs-lookup"><span data-stu-id="71355-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="71355-200">Более подробная информация об ошибках может быть получена путем включения подробных ошибок на сервере.</span><span class="sxs-lookup"><span data-stu-id="71355-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="71355-201">Для получения дополнительной [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)информации см.</span><span class="sxs-lookup"><span data-stu-id="71355-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="71355-202">Ошибка &lt;"TypeError:&gt; hubType является неопределенным" ошибка</span><span class="sxs-lookup"><span data-stu-id="71355-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="71355-203">Эта ошибка приведет, если `MapHubs` вызов не сделан должным образом.</span><span class="sxs-lookup"><span data-stu-id="71355-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="71355-204">Узнайте, [как зарегистрировать маршрут SignalR и настроить параметры SignalR](../guide-to-the-api/hubs-api-guide-server.md#route) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="71355-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="71355-205">JsonSerializationИсключение не справился с помощью пользовательского кода</span><span class="sxs-lookup"><span data-stu-id="71355-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="71355-206">Убедитесь, что параметры, которые вы отправляете на методы, не включают несериализируемые типы (например, файлообработки или соединения баз данных).</span><span class="sxs-lookup"><span data-stu-id="71355-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="71355-207">Если вам нужно использовать участников на объекте на стороне сервера, который вы не хотите, чтобы их `JSONIgnore` отправляли клиенту (либо в целях безопасности, либо по причинам сериализации), используйте атрибут.</span><span class="sxs-lookup"><span data-stu-id="71355-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="71355-208">Ошибка "Ошибка протокола: Неизвестный транспорт" ошибка</span><span class="sxs-lookup"><span data-stu-id="71355-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="71355-209">Эта ошибка может возникнуть, если клиент не поддерживает переносы, которые использует SignalR.</span><span class="sxs-lookup"><span data-stu-id="71355-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="71355-210">См [Транспорти и Fallbacks](../getting-started/introduction-to-signalr.md#transports) для получения информации о том, какие браузеры могут быть использованы с SignalR.</span><span class="sxs-lookup"><span data-stu-id="71355-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="71355-211">"Поколение прокси-серверов JavaScript Hub отключено."</span><span class="sxs-lookup"><span data-stu-id="71355-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="71355-212">Эта ошибка будет `DisableJavaScriptProxies` происходить, если установлен, а также `signalr/hubs`в том числе ссылка на динамически сгенерированных прокси на .</span><span class="sxs-lookup"><span data-stu-id="71355-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="71355-213">Для получения дополнительной информации о создании прокси вручную, смотрите [сгенерированный прокси и что он делает для вас.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)</span><span class="sxs-lookup"><span data-stu-id="71355-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="71355-214">"Идентификатор соединения находится в неправильном формате" или "Идентификация пользователя не может изменяться во время активного подключения SignalR" ошибка</span><span class="sxs-lookup"><span data-stu-id="71355-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="71355-215">Эта ошибка может быть замечена, если используется аутентификация, и клиент вырегистрируется до того, как соединение остановлено.</span><span class="sxs-lookup"><span data-stu-id="71355-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="71355-216">Решение состоит в том, чтобы остановить подключение SignalR перед регистрацией клиента.</span><span class="sxs-lookup"><span data-stu-id="71355-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="71355-217">"Непойманная ошибка: SignalR: jquery не найдено.</span><span class="sxs-lookup"><span data-stu-id="71355-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="71355-218">Пожалуйста, убедитесь, что j'ery ссылается до ошибки файла SignalR.js</span><span class="sxs-lookup"><span data-stu-id="71355-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="71355-219">Клиент SignalR JavaScript требует запуска j''i.</span><span class="sxs-lookup"><span data-stu-id="71355-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="71355-220">Убедитесь, что ваша ссылка на j'ery верна, что используемый путь является действительным, и что ссылка на j'ery находится до ссылки на SignalR.</span><span class="sxs-lookup"><span data-stu-id="71355-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="71355-221">"Uncaught TypeError: Не&lt;может&gt;читать свойство ' собственности ' неопределенных" ошибка</span><span class="sxs-lookup"><span data-stu-id="71355-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="71355-222">Эта ошибка является результатом не имеющих j'sry или концентраторов прокси ссылки должным образом.</span><span class="sxs-lookup"><span data-stu-id="71355-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="71355-223">Убедитесь, что ваша ссылка на прокси j'ery и концентраторы верна, что используемый путь действителен, и что ссылка на j'ery находится до ссылки на прокси концентратов.</span><span class="sxs-lookup"><span data-stu-id="71355-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="71355-224">Ссылка по умолчанию на прокси-сервер концентраторов должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="71355-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="71355-225">**HTML клиент-код, который правильно ссылается на прокси концентраторов**</span><span class="sxs-lookup"><span data-stu-id="71355-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="71355-226">"RuntimeBinderException был необработан из-за ошибки кода пользователя"</span><span class="sxs-lookup"><span data-stu-id="71355-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="71355-227">Эта ошибка может возникнуть при `Hub.On` неправильной перегрузке.</span><span class="sxs-lookup"><span data-stu-id="71355-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="71355-228">Если метод имеет значение возврата, тип возврата должен быть указан как общий параметр типа:</span><span class="sxs-lookup"><span data-stu-id="71355-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="71355-229">**Метод, определяемый на клиенте (без генерируемого прокси)**</span><span class="sxs-lookup"><span data-stu-id="71355-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="71355-230">Идентификатор соединения несовместим или разрывы связи между загрузками страниц</span><span class="sxs-lookup"><span data-stu-id="71355-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="71355-231">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-231">This behavior is by design.</span></span> <span data-ttu-id="71355-232">Поскольку объект концентратора размещается в объекте страницы, концентратор уничтожается при обновлении страницы.</span><span class="sxs-lookup"><span data-stu-id="71355-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="71355-233">Многостраничное приложение должно поддерживать связь между пользователями и идентизацией связи, чтобы они были последовательными между загрузками страниц.</span><span class="sxs-lookup"><span data-stu-id="71355-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="71355-234">Итики подключения могут храниться на `ConcurrentDictionary` сервере как в объекте, так и в базе данных.</span><span class="sxs-lookup"><span data-stu-id="71355-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="71355-235">Ошибка "Value не может быть нулевым"</span><span class="sxs-lookup"><span data-stu-id="71355-235">"Value cannot be null" error</span></span>

<span data-ttu-id="71355-236">Методы сервера с дополнительными параметрами в настоящее время не поддерживаются; если дополнительный параметр опущен, метод выйдет из строя.</span><span class="sxs-lookup"><span data-stu-id="71355-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="71355-237">Для получения дополнительной [информации см.](https://github.com/SignalR/SignalR/issues/324)</span><span class="sxs-lookup"><span data-stu-id="71355-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="71355-238">"Firefox не может установить подключение &lt;к&gt;серверу по адресу " Ошибка в Firebug</span><span class="sxs-lookup"><span data-stu-id="71355-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="71355-239">Это сообщение об ошибке можно увидеть в Firebug, если переговоры о транспорте WebSocket не удались, и вместо него используется другой транспорт.</span><span class="sxs-lookup"><span data-stu-id="71355-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="71355-240">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="71355-241">"Удаленный сертификат недействителен в соответствии с процедурой проверки" ошибка в клиентском приложении .NET</span><span class="sxs-lookup"><span data-stu-id="71355-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="71355-242">Если серверу требуются пользовательские сертификаты клиента, то вы можете добавить сертификат x509 к подключению до того, как будет сделан запрос.</span><span class="sxs-lookup"><span data-stu-id="71355-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="71355-243">Добавьте сертификат к `Connection.AddClientCertificate`подключению с помощью .</span><span class="sxs-lookup"><span data-stu-id="71355-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="71355-244">Подключение падает после проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="71355-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="71355-245">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-245">This behavior is by design.</span></span> <span data-ttu-id="71355-246">Учетные данные аутентификации не могут быть изменены во время активного подключения; для обновления учетных данных соединение должно быть остановлено и перезапущено.</span><span class="sxs-lookup"><span data-stu-id="71355-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="71355-247">OnConnected вызывается дважды при использовании j's'ry Mobile</span><span class="sxs-lookup"><span data-stu-id="71355-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="71355-248">`initializePage` Функция j's Mobile заставляет скрипты на каждой странице повторно выполняться, создавая тем самым второе соединение.</span><span class="sxs-lookup"><span data-stu-id="71355-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="71355-249">Решения для этой проблемы включают в себя:</span><span class="sxs-lookup"><span data-stu-id="71355-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="71355-250">Включите ссылку на j'ery Mobile перед файлом JavaScript.</span><span class="sxs-lookup"><span data-stu-id="71355-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="71355-251">Отпустите `initializePage` функцию, установив. `$.mobile.autoInitializePage = false`</span><span class="sxs-lookup"><span data-stu-id="71355-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="71355-252">Подождите, пока страница закончится инициализацией, прежде чем начать соединение.</span><span class="sxs-lookup"><span data-stu-id="71355-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="71355-253">Сообщения задерживаются в приложениях Silverlight с помощью событий Сервера Отправлено</span><span class="sxs-lookup"><span data-stu-id="71355-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="71355-254">Сообщения задерживаются при использовании событий, отправляемых на сервере Silverlight.</span><span class="sxs-lookup"><span data-stu-id="71355-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="71355-255">Чтобы вместо этого принудить к использованию длинные опросы, используйте следующее при запуске соединения:</span><span class="sxs-lookup"><span data-stu-id="71355-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="71355-256">"Разрешение отказано" с использованием протокола Forever Frame</span><span class="sxs-lookup"><span data-stu-id="71355-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="71355-257">Это известный вопрос, описанный [здесь](https://github.com/SignalR/SignalR/issues/1963).</span><span class="sxs-lookup"><span data-stu-id="71355-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="71355-258">Этот симптом можно увидеть с помощью последней библиотеки J'ery; обходной путь заключается в том, чтобы понизить ваше приложение до J's1.8.2.</span><span class="sxs-lookup"><span data-stu-id="71355-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="71355-259">Компиляция и ошибки на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="71355-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="71355-260">Следующий раздел содержит возможные решения для компилятора и ошибок в расписании выполнения сервера.</span><span class="sxs-lookup"><span data-stu-id="71355-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="71355-261">Ссылка на экземпляр концентратора является нулевой</span><span class="sxs-lookup"><span data-stu-id="71355-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="71355-262">Поскольку экземпляр концентратора создается для каждого соединения, вы не можете создать экземпляр концентратора в коде самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="71355-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="71355-263">Чтобы вызвать методы концентратора из-за пределов самого концентратора, [см. Как вызвать методы клиента и управлять группами из-за пределов класса концентратора,](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) чтобы получить ссылку на контекст концентратора.</span><span class="sxs-lookup"><span data-stu-id="71355-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="71355-264">HTTPContext.Current.Session является недействительным</span><span class="sxs-lookup"><span data-stu-id="71355-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="71355-265">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-265">This behavior is by design.</span></span> <span data-ttu-id="71355-266">SignalR не поддерживает состояние сеанса ASP.NET, так как включение состояния сеанса приведет к разбивке дуплексных сообщений.</span><span class="sxs-lookup"><span data-stu-id="71355-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="71355-267">Нет подходящего метода для переопределения</span><span class="sxs-lookup"><span data-stu-id="71355-267">No suitable method to override</span></span>

<span data-ttu-id="71355-268">Вы можете увидеть эту ошибку, если вы используете код из старой документации или блогов.</span><span class="sxs-lookup"><span data-stu-id="71355-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="71355-269">Убедитесь, что вы не ссылаетесь на названия методов, которые `OnConnectedAsync`были изменены или измотаны (например).</span><span class="sxs-lookup"><span data-stu-id="71355-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="71355-270">HostContextExtensions.WebSocketServerUrl является недействительным</span><span class="sxs-lookup"><span data-stu-id="71355-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="71355-271">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-271">This behavior is by design.</span></span> <span data-ttu-id="71355-272">Этот член является амортизированным и не должен использоваться.</span><span class="sxs-lookup"><span data-stu-id="71355-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="71355-273">"Маршрут под названием 'signalr.hubs' уже находится в сборе маршрутов" ошибка</span><span class="sxs-lookup"><span data-stu-id="71355-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="71355-274">Эта ошибка будет `MapHubs` видна, если она называется в два раза вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="71355-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="71355-275">Некоторые примеры `MapHubs` приложений называются непосредственно в файле глобального приложения; другие делают звонок в типе обертки.</span><span class="sxs-lookup"><span data-stu-id="71355-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="71355-276">Убедитесь, что приложение не выполняет и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="71355-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="71355-277">Вопросы визуальной студии</span><span class="sxs-lookup"><span data-stu-id="71355-277">Visual Studio issues</span></span>

<span data-ttu-id="71355-278">В этом разделе описаны проблемы, возникающие в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71355-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="71355-279">Узел документов скрипта не отображается в Исследователе решения</span><span class="sxs-lookup"><span data-stu-id="71355-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="71355-280">Некоторые из наших учебников направляют вас к узлом "Документы сценариев" в Solution Explorer во время отладки.</span><span class="sxs-lookup"><span data-stu-id="71355-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="71355-281">Этот узло производится отладчиком JavaScript и будет отображаться только при отладке клиентов браузера в Internet Explorer; узел не появится при использовании Chrome или Firefox.</span><span class="sxs-lookup"><span data-stu-id="71355-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="71355-282">Отладка JavaScript также не будет работать, если работает другой отладчик клиента, например отладчик Silverlight.</span><span class="sxs-lookup"><span data-stu-id="71355-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="71355-283">SignalR не работает на Visual Studio 2008 или раньше</span><span class="sxs-lookup"><span data-stu-id="71355-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="71355-284">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="71355-284">This behavior is by design.</span></span> <span data-ttu-id="71355-285">SignalR требует .NET Framework 4 или более поздней позже; это требует, чтобы приложения SignalR разрабатывались в Visual Studio 2010 или позже.</span><span class="sxs-lookup"><span data-stu-id="71355-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="71355-286">Вопросы ИИС</span><span class="sxs-lookup"><span data-stu-id="71355-286">IIS issues</span></span>

<span data-ttu-id="71355-287">Этот раздел содержит проблемы с Информационными службами Интернета.</span><span class="sxs-lookup"><span data-stu-id="71355-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="71355-288">Веб-сайт выходит из строя после вызова MapHubs</span><span class="sxs-lookup"><span data-stu-id="71355-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="71355-289">Эта проблема была исправлена в последней версии SignalR.</span><span class="sxs-lookup"><span data-stu-id="71355-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="71355-290">Убедитесь, что вы используете последнюю выпущенную версию SignalR, обновляя установку с помощью NuGet.</span><span class="sxs-lookup"><span data-stu-id="71355-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="71355-291">Проблемы Azure</span><span class="sxs-lookup"><span data-stu-id="71355-291">Azure issues</span></span>

<span data-ttu-id="71355-292">Этот раздел содержит проблемы с Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="71355-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="71355-293">Сообщения не принимаются через заднюю плоскость Azure после изменения названий тем</span><span class="sxs-lookup"><span data-stu-id="71355-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="71355-294">Темы, используемые задней плоскостью Azure, не предназначены для настройки пользователя.</span><span class="sxs-lookup"><span data-stu-id="71355-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
