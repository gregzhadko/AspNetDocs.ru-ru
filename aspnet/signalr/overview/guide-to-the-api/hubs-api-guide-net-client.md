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
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET Руководство aPI концентраторов SignalR - .NET Клиент (C)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Этот документ содержит введение в использование API-адреса концентратов для версии SignalR 2 у клиентов .NET, таких как Windows Store (WinRT), WPF, Silverlight и консольных приложений.
>
> API Концентраторов SignalR позволяет совершать удаленные процедурные звонки (RPCs) с сервера для подключенных клиентов и от клиентов к серверу. В коде сервера вы определяете методы, которые могут вызываться клиентами, и вызываете методы, которые работают на клиенте. В клиентском коде вы определяете методы, которые можно вызывать с сервера, и вызываете методы, которые работают на сервере. SignalR заботится о всех клиента к серверу сантехника для вас.
>
> SignalR также предлагает API более низкого уровня под названием Persistent Connections. Для введения в SignalR, концентраторы, и стойкие соединения, или для учебника, который показывает, как построить полное приложение SignalR, см [SignalR - Начало работы](../getting-started/index.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемые в этой теме
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - Версия SignalR 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Предыдущие версии этой темы
>
> Для получения информации о более ранних версиях SignalR, см [SignalR Старые версии](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Пожалуйста, оставьте обратную связь о том, как вам понравился этот учебник и что мы могли бы улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com.](http://stackoverflow.com/)

## <a name="overview"></a>Обзор

Этот документ содержит следующие разделы.

- [Настройка клиента](#clientsetup)
- [Как установить соединение](#establishconnection)

    - [Кросс-доменсоединения от клиентов Silverlight](#slcrossdomain)
- [Как настроить соединение](#configureconnection)

    - [Как установить максимальное количество одновременных подключений в клиентах WPF](#maxconnections)
    - [Как указать параметры строки запроса](#querystring)
    - [Как указать транспортный метод](#transport)
    - [Как указать заголовки HTTP](#httpheaders)
    - [Как указать сертификаты клиента](#clientcertificate)
- [Как создать прокси-сервер концентратора](#proxy)
- [Как определить методы на клиенте, который может вызвать сервер](#callclient)

    - [Методы без параметров](#clientmethodswithoutparms)
    - [Методы с параметрами, определяющие типы параметров](#clientmethodswithparmtypes)
    - [Методы с параметрами, определяющие динамические объекты для параметров](#clientmethodswithdynamparms)
    - [Как удалить обработчик](#removehandler)
- [Как вызвать методы сервера от клиента](#callserver)
- [Как обрабатывать события жизни соединения](#connectionlifetime)
- [Как обрабатывать ошибки](#handleerrors)
- [Как включить журналирование на стороне клиента](#logging)
- [Образцы кода приложений WPF, Silverlight и консольных приложений для методов клиента, которые сервер может вызвать](#wpfsl)

Для примера клиентских проектов .NET см.

- [gustavo-armenta / SignalR-Образцы](https://github.com/gustavo-armenta/SignalR-Samples) на GitHub.com (WinRT, Silverlight, примеры консольных приложений).
- [DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) на GitHub.com (пример WPF).
- [SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) на GitHub.com (пример приложения для консоли).

Для получения документации о том, как запрограммировать сервер или JavaScript клиентов, см.

- [Руководство По API Концентратов SignalR - Сервер](hubs-api-guide-server.md)
- [Руководство По API Концентратов SignalR - Клиент JavaScript](hubs-api-guide-javascript-client.md)

Ссылки на темы API Справочные ссылки на .NET 4.5 версия API. Если вы используете .NET 4, [см.](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)

<a id="clientsetup"></a>

## <a name="client-setup"></a>Настройка клиента

Установите пакет [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet (не пакет [Microsoft.AspNet.SignalR).](http://nuget.org/packages/microsoft.aspnet.signalr) Этот пакет поддерживает клиентов WinRT, Silverlight, WPF, консольных приложений и Windows Phone как для .NET 4, так и для .NET 4.5.

Если версия SignalR, которая у вас есть на клиенте отличается от версии, что у вас есть на сервере, SignalR часто в состоянии адаптироваться к разнице. Например, сервер под управлением signalR версии 2 будет поддерживать клиентов, которые имеют 1.1.x установлен, а также клиентов, которые имеют версию 2 установлен. Если разница между версией на сервере и версией на клиенте слишком велика, или если клиент `InvalidOperationException` новее, чем сервер, SignalR бросает исключение, когда клиент пытается установить соединение. Сообщение об ошибке ".`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Как установить соединение

Прежде чем установить соединение, необходимо `HubConnection` создать объект и создать прокси- Чтобы установить соединение, `Start` позвоните `HubConnection` методу на объект.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> Для клиентов JavaScript необходимо зарегистрировать по крайней `Start` мере одного обработчика событий, прежде чем вызвать метод для установления соединения. Это не обязательно для клиентов .NET. Для клиентов JavaScript сгенерированный прокси-код автоматически создает прокси-серверы для всех концентраторов, которые существуют на сервере, и регистрация обработчика — это то, как вы указываете, какие концентраторы, которые намерен использовать клиент. Но для клиента .NET вы создаете прокси-серверы концентратора вручную, поэтому SignalR предполагает, что вы будете использовать любой концентратор, для которого вы создаете прокси.

Пример кода использует URL-адрес по умолчанию "/сигнальщик" для подключения к службе SignalR. Для получения информации о том, как указать другой базовый URL, см [ASP.NET.](hubs-api-guide-server.md#signalrurl)

Метод `Start` выполняется асинхронно. Чтобы убедиться, что последующие строки кода не выполняются `await` до тех пор, пока соединение `.Wait()` не будет установлено, используйте в ASP.NET 4.5 асинхронного метода или в синхронном методе. Не используйте `.Wait()` в клиенте WinRT.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Кросс-доменсоединения от клиентов Silverlight

Для получения информации о том, как включить кросс-домен соединения от клиентов Silverlight, [см.](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Как настроить соединение

Прежде чем установить соединение, можно указать любой из следующих вариантов:

- Одновременное ограничение соединений.
- Параметры строки запроса.
- Транспортный метод.
- ЗАГОЛОВКи HTTP.
- Сертификаты клиентов.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>Как установить максимальное количество одновременных подключений в клиентах WPF

В клиентах WPF может потребоваться увеличить максимальное количество одновременных подключений от значения по умолчанию 2. Рекомендуемое значение 10.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

Для получения дополнительной информации [см.](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Как указать параметры строки запроса

Если вы хотите отправить данные на сервер при подключении клиента, можно добавить параметры строки запроса к объекту соединения. В следующем примере показано, как установить параметр строки запроса в клиентском коде.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

В следующем примере показано, как прочитать параметр строки запроса в коде сервера.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Как указать транспортный метод

В процессе подключения клиент SignalR обычно ведет переговоры с сервером, чтобы определить наилучший транспорт, который поддерживается как сервером, так и клиентом. Если вы уже знаете, какой транспорт вы хотите использовать, вы можете обойти этот процесс переговоров. Чтобы указать способ транспортировки, передайте в транспортном объекте методу Start. В следующем примере показано, как указать метод транспортировки в клиентском коде.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

В названии [Microsoft.AspNet.SignalR.Client.Transports включены](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) следующие классы, которые можно использовать для указания транспорта.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [СерверСентСобытийТранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (доступно только при использовании сервера и клиента .NET 4.5.)
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Автоматически выбирает лучший транспорт, который поддерживается как клиентом, так и сервером. Это транспорт по умолчанию. Передача этого `Start` в метод имеет тот же эффект, как не проходя ни в чем.)

Транспорт ForeverFrame не включен в этот список, поскольку он используется только браузерами.

Подробнее о том, как проверить метод транспортировки в серверном коде, смотрите [ASP.NET Руководство по aPI SignalR Hubs API - Server - Как получить информацию о клиенте из свойства Контекста.](hubs-api-guide-server.md#contextproperty) Для получения дополнительной информации о транспорте и откатов, [см. Введение в SignalR - Транспорт и Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>Как указать заголовки HTTP

Чтобы установить заголовки `Headers` HTTP, используйте свойство на объекте соединения. Ниже приводится следующий пример, как добавить заголовок HTTP.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>Как указать сертификаты клиента

Чтобы добавить сертификаты `AddClientCertificate` клиента, используйте метод на объекте соединения.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Как создать прокси-сервер концентратора

Для определения методов клиента, которые концентратор может вызвать с сервера, и вызова методов на концентраторе на сервере, создайте прокси для концентратора, вызывая `CreateHubProxy` объект соединения. Строка, которую `CreateHubProxy` вы передаете, — это имя класса `HubName` концентратора или имя, указанное атрибутом, если он был использован на сервере. Сопоставление имен не зависит от регистра.

**Класс концентратора на сервере**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Создание клиентского прокси для класса концентратора**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Если вы украсите `HubName` свой класс концентратора атрибутом, используйте это имя.

**Класс концентратора на сервере**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**Создание клиентского прокси для класса концентратора**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

Если вы `HubConnection.CreateHubProxy` звоните несколько раз с тем же, `hubName`вы получите тот же кэшированный `IHubProxy` объект.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Как определить методы на клиенте, который может вызвать сервер

Чтобы определить метод, который может вызвать сервер, используйте `On` метод прокси для регистрации обработчика событий.

Сопоставление имен метода является нечувствительным. Например, `Clients.All.UpdateStockPrice` на сервере `updateStockPrice` `updatestockprice`будет `UpdateStockPrice` выполняться, или на клиенте.

Различные клиентские платформы имеют различные требования к тому, как вы пишете код метода для обновления пользовательского доступа. Приведенные примеры для клиентов WinRT (Windows Store .NET). Примеры WPF, Silverlight и консольных приложений приведены в [отдельном разделе позже в этой теме.](#wpfsl)

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Методы без параметров

Если метод, с помощью которой вы работаете, не имеет `On` параметров, используйте неродовую перегрузку метода:

**Серверный код вызова методклиента без параметров**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Код клиента WinRT для метода, вызываемого с сервера без параметров[(см. примеры WPF и Silverlight позже в этой теме)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Методы с параметрами, определяющие типы параметров

Если метод, с которой вы обрабатываете, имеет параметры, укажите типы параметров как общие типы метода. `On` Существуют общие перегрузки `On` метода, позволяющие указывать до 8 параметров (4 на Windows Phone 7). В следующем примере один параметр `UpdateStockPrice` отправляется в метод.

**Серверный код вызова метода клиента с параметром**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Класс stock, используемый для параметра**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**Код клиента WinRT для метода, вызванного с сервера с параметром[(см. примеры WPF и Silverlight позже в этой теме)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Методы с параметрами, определяющие динамические объекты для параметров

В качестве альтернативы определению параметров в `On` качестве общих типов метода можно указать параметры как динамические объекты:

**Серверный код вызова метода клиента с параметром**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Класс stock, используемый для параметра**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**Код Клиента WinRT для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра[(см. примеры WPF и Silverlight позже в этой теме)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Как удалить обработчик

Чтобы удалить обработчик, позвоните его `Dispose` методу.

**Клиентский код для метода, вызванного с сервера**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**Код клиента для удаления обработчика**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Как вызвать методы сервера от клиента

Чтобы вызвать метод на сервере, используйте `Invoke` метод на прокси-сервере концентратора.

Если метод сервера не имеет значения возврата, используйте `Invoke` негенерическую перегрузку метода.

**Код сервера для метода, не имевавого значения возврата**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Код клиента вызова метода, который не имеет значения возврата**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Если метод сервера имеет значение возврата, укажите тип `Invoke` возврата как общий тип метода.

**Код сервера для метода, который имеет значение возврата и использует сложный параметр типа**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Класс stock, используемый для значения параметра и возврата**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**Клиентский код вызова метода, который имеет значение возврата и принимает сложный параметр типа, в ASP.NET методе 4.5 async**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Клиентский код вызова метода, который имеет значение возврата и принимает сложный параметр типа, в синхронном методе**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

Метод `Invoke` выполняет асинхронно и `Task` возвращает объект. Если вы не `await` указали или, `.Wait()`следующая строка кода будет выполняться до метода, который вы ссылаетесь закончил выполнение.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Как обрабатывать события жизни соединения

SignalR предоставляет следующие события жизни соединения, которые вы можете обрабатывать:

- `Received`: Поднятыпри получать какие-либо данные о подключении. Предоставляет полученные данные.
- `ConnectionSlow`: Поднят, когда клиент обнаруживает медленное или часто падающее соединение.
- `Reconnecting`: Поднятый, когда базовый транспорт начинает воссоединение.
- `Reconnected`: Поднятый при повторном подключении основного транспорта.
- `StateChanged`: Поднят при изменении состояния соединения. Обеспечивает старое состояние и новое состояние. Для получения информации о [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)значениях состояния соединения см.
- `Closed`: Поднят освоено при отключении соединения.

Например, если вы хотите отобразить предупреждающие сообщения об ошибках, которые не являются фатальными, но `ConnectionSlow` вызывают периодические проблемы с подключением, такие как медлительность или частое падение соединения, справьтесь с событием.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

Для получения дополнительной информации, см [Понимание и обработка подключения Пожизненные события в SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Как обрабатывать ошибки

Если вы явно не включаете подробные сообщения об ошибке на сервере, объект исключения, который возвращает SignalR после ошибки, содержит минимальную информацию об ошибке. Например, если вызов `newContosoChatMessage` не удается, сообщение об`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`ошибке в объекте ошибки содержит " Отправка подробных сообщений об ошибках клиентам в производственной сфере не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

Для обработки ошибок, которые вызывает SignalR, можно добавить обработчик `Error` для события на объекте соединения.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

Для обработки ошибок из вызовов метода заверните код в блок try-catch.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Как включить журналирование на стороне клиента

Чтобы включить журнал в сторону клиента, установите `TraceLevel` и `TraceWriter` свойства на объект соединения.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Образцы кода приложений WPF, Silverlight и консольных приложений для методов клиента, которые сервер может вызвать

Образцы кода, показанные ранее для определения методов клиента, которые сервер может вызвать, применимы к клиентам WinRT. Следующие примеры показывают эквивалентный код для клиентов WPF, Silverlight и консольных приложений.

### <a name="methods-without-parameters"></a>Методы без параметров

**Клиентский код WPF для метода, вызываемого с сервера без параметров**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Клиентский код Silverlight для метода, вызываемого с сервера без параметров**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Консольный клиентский код приложения для метода, вызываемого с сервера без параметров**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Методы с параметрами, определяющие типы параметров

**Клиентский код WPF для метода, вызванного с сервера с параметром**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Клиентский код Silverlight для метода, вызванного с сервера с параметром**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Консольный клиентский код приложения для метода, вызванного с сервера с параметром**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Методы с параметрами, определяющие динамические объекты для параметров

**Клиентский код WPF для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Клиентский код Silverlight для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Консольный клиентский код приложения для метода, вызванного с сервера с параметром, с использованием динамического объекта для параметра**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
