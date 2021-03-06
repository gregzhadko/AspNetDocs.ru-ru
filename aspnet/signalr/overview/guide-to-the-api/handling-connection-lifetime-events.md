---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: Понимание и обработка подключения Пожизненные события в SignalR (ru) Документы Майкрософт
author: bradygaster
description: В этой статье описывается, как использовать события, выставленные API концентраторов.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675829"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>Общие сведения и обработка событий времени существования подключений в SignalR

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этой статье приводится обзор событий соединения SignalR, переподключения и отключения, которые можно обрабатывать, а также параметры тайм-аута и сохранения, которые можно настроить.
>
> Статья предполагает, что у вас уже есть некоторые знания SignalR и событий жизни соединения. Для введения в SignalR, [см.](../getting-started/introduction-to-signalr.md) Для списков событий жизни соединения см.
>
> - [Как обрабатывать события жизни соединения в классе концентратора](hubs-api-guide-server.md#connectionlifetime)
> - [Как обрабатывать события срока службы соединения в клиентах JavaScript](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [Как обрабатывать события срока службы соединения в клиентах .NET](hubs-api-guide-net-client.md#connectionlifetime)
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

Эта статья состоит из следующих разделов:

- [Терминология и сценарии стыковки](#terminology)

    - [Соединения SignalR, транспортные соединения и физические соединения](#signalrvstransport)
    - [Сценарии отключения транспорта](#transportdisconnect)
    - [Сценарии отключения клиента](#clientdisconnect)
    - [Сценарии отключения сервера](#serverdisconnect)
- [Настройки тайм-аута и сохранения](#timeoutkeepalive)

    - [ПодключениеВремя](#connectiontimeout)
    - [ОтключениеTimeout](#disconnecttimeout)
    - [Keepalive](#keepalive)
    - [Как изменить настройки тайм-аута и сохранить](#changetimeout)
- [Как уведомить пользователя об отключении](#notifydisconnect)
- [Как постоянно воссоединиться](#continuousreconnect)
- [Как отключить клиента в серверном коде](#disconnectclientfromserver)
- [Обнаружение причины отключения](#detectingreasonfordisconnection)

Ссылки на темы API Справочные ссылки на .NET 4.5 версия API. Если вы используете .NET 4, [см.](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Терминология и сценарии стыковки

Обработчик `OnReconnected` событий в концентраторе SignalR может выполняться сразу после, `OnConnected` но не после `OnDisconnected` для данного клиента. Причина, по которой повторное подключение может быть восстановлено без отключения, заключается в том, что в SignalR используется несколько способов использования слова «соединение».

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>Соединения SignalR, транспортные соединения и физические соединения

Эта статья будет различать *соединения SignalR,* *транспортные соединения,* и *физические соединения:*

- **Соединение SignalR** относится к логической взаимосвязи между клиентом и URL сервера, поддерживаемым API SignalR и однозначно идентифицированным идентификатором соединения. Данные об этой взаимосвязи поддерживаются SignalR и используются для установления транспортного сообщения. Связь заканчивается, и SignalR распоряжается `Stop` данными, когда клиент вызывает метод или ограничение тайм-аута достигается, в то время как SignalR пытается восстановить утраченное транспортное соединение.
- **Транспортное соединение** относится к логической взаимосвязи между клиентом и сервером, поддерживаемой одним из четырех транспортных AI: WebSockets, события, отправленные сервером, навсегда кадр, или длинный опрос. SignalR использует транспортный API для создания транспортного соединения, а транспортный API зависит от наличия физического сетевого соединения для создания транспортного соединения. Транспортное соединение заканчивается, когда SignalR прекращает его или когда транспортный API обнаруживает, что физическое соединение нарушено.
- **Физическое соединение** относится к физическим сетевым ссылкам - проводам, беспроводным сигналам, маршрутизаторам и т.д., которые облегчают связь между клиентским компьютером и серверным компьютером. Для установления транспортного сообщения необходимо подключение к транспортному соединению, а для установления связи signalR необходимо установить транспортное сообщение. Однако нарушение физического соединения не всегда немедленно завершает транспортное соединение или соединение SignalR, как будет объяснено позже в этой теме.

На следующей диаграмме соединение SignalR представлено API Концентров и слоем PersistentConnection API SignalR, транспортное соединение представлено слоем Transports, а физическое соединение представлено линиями между сервером и клиентами.

![Диаграмма архитектуры SignalR](handling-connection-lifetime-events/_static/image1.png)

Когда вы `Start` вызываете метод в клиенте SignalR, вы предоставляете клиентский код SignalR со всей информацией, необходимой для установления физического подключения к серверу. Клиентский код SignalR использует эту информацию для запроса HTTP и установления физического соединения, используюго один из четырех транспортных методов. Если транспортное соединение выходит из строя или сервер выходит из строя, соединение SignalR не проходит немедленно, потому что клиент по-прежнему имеет информацию, необходимую для автоматического восстановления нового транспортного соединения с тем же URL SignalR. В этом сценарии никакое вмешательство со стороны приложения пользователя не требуется, и когда код клиента SignalR устанавливает новое транспортное соединение, он не начинает новое соединение SignalR. Непрерывность соединения SignalR отражается в том, что идентификатор соединения, `Start` который создается при вызове метода, не изменяется.

Обработчик `OnReconnected` событий в концентраторе выполняется при автоматическом восстановлении транспортного соединения после потери. Обработчик `OnDisconnected` событий выполняется в конце соединения SignalR. Соединение SignalR может закончиться любым из следующих способов:

- Если клиент вызывает `Stop` метод, на сервер отправляется стоп-сообщение, и клиент и сервер немедленно заканчивают подключение SignalR.
- После потери связи между клиентом и сервером клиент пытается восстановить соединение, и сервер ждет повторного подключения клиента. Если попытки повторного подключения не увенчались успехом и срок отсоединения заканчивается, как клиент, так и сервер заканчивают соединение SignalR. Клиент прекращает попытки повторного подключения, и сервер избавляется от своего представления соединения SignalR.
- Если клиент прекращает работу, не `Stop` имея возможности вызвать метод, сервер ждет повторного подключения клиента, а затем завершает подключение SignalR после периода отключения.
- Если сервер прекращает работу, клиент пытается восстановить соединение (повторно создать транспортное соединение), а затем завершает подключение SignalR после периода отключения.

Когда нет проблем с подключением, и пользовательское приложение `Stop` завершает соединение SignalR, вызывая метод, соединение SignalR и транспортное соединение начинаются и заканчиваются примерно в одно и то же время. В следующих разделах более подробно описаны другие сценарии.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Сценарии отключения транспорта

Физические соединения могут быть медленными или могут быть перерывы в подключении. В зависимости от таких факторов, как продолжительность прерывания, транспортное сообщение может быть прекращено. Затем SignalR пытается восстановить транспортное соединение. Иногда API транспортного сообщения обнаруживает прерывание и отбрасывает транспортное соединение, и SignalR сразу обнаруживает, что соединение потеряно. В других сценариях ни API транспортного соединения, ни SignalR не узнают сразу о потере подключения. Для всех переносов, за исключением длинных опросов, клиент SignalR использует функцию, называемую *keepalive,* чтобы проверить потерю подключения, которую транспортный API не может обнаружить. Для получения информации о длительных связях с опросами, см [Таймаут и keepalive настройки](#timeoutkeepalive) позже в этой теме.

Когда соединение неактивно, сервер периодически отправляет клиенту пакет keepalive. На дату написания этой статьи частота по умолчанию составляет каждые 10 секунд. Слушая эти пакеты, клиенты могут сказать, есть ли проблемы с подключением. Если пакет keepalive не получен, когда ожидается, через некоторое время клиент предполагает, что возникают проблемы с подключением, такие как медлительность или перерывы. Если keepalive по-прежнему не получен после более длительного времени, клиент предполагает, что соединение было удалено, и он начинает пытаться восстановить соединение.

Следующая диаграмма иллюстрирует события клиента и сервера, которые возникают в типичном сценарии, когда возникают проблемы с физическим соединением, которые не сразу распознаются aPI транспортировки. Диаграмма применяется к следующим обстоятельствам:

- Транспорт — это WebSockets, навсегда кадр, или сервер-отправленные события.
- Существуют различные периоды прерывания в физическом подключении сети.
- Транспортный API не узнает о прерываниях, поэтому SignalR полагается на функциональность keepalive для их обнаружения.

![Транспортные отключения](handling-connection-lifetime-events/_static/image2.png)

Если клиент переходит в режим повторного подключения, но не может установить транспортное соединение в пределах срока отключения, сервер прекращает подключение SignalR. Когда это происходит, сервер выполняет метод `OnDisconnected` концентратора и выстраивает в очередь сообщение отключения для отправки клиенту в случае, если клиенту удастся подключиться позже. Если клиент переподключен, он получает команду отключения и `Stop` вызывает метод. В этом `OnReconnected` случае не выполняется при повторном `OnDisconnected` подключении клиента и `Stop`не выполняется при вызове клиента. Следующая диаграмма иллюстрирует этот сценарий.

![Транспортные сбои - тайм-аут сервера](handling-connection-lifetime-events/_static/image3.png)

События жизни соединения SignalR, которые могут быть подняты на клиенте:

- `ConnectionSlow`клиентского события.

    Поднятый, когда предустановленная доля периода тайм-аута keepalive прошла с момента получения последнего сообщения или пинг-пинга keepalive. Период предупреждения о тайм-ауте по умолчанию составляет 2/3 тайм-аута keepalive. Timeout keepalive составляет 20 секунд, поэтому предупреждение происходит примерно в 13 секунд.

    По умолчанию сервер отправляет пинги keepalive каждые 10 секунд, а клиент проверяет на наличие пингов примерно каждые 2 секунды (одна треть разницы между значением тайм-аута keepalive и значением предупреждения о тайм-ауте keepalive).

    Если транспортному API узнает об отключении, SignalR может быть проинформирован об отключении до того, как пройдет период предупреждения о тайм-ауте keepalive. В этом случае `ConnectionSlow` событие не будет поднято, и SignalR будет идти непосредственно к событию. `Reconnecting`
- `Reconnecting`клиентского события.

    Поднятый, когда (a) транспортный API обнаруживает, что соединение потеряно, или (b) период тайм-аута keepalive прошел с момента получения последнего сообщения или пинга keepalive. Клиентский код SignalR начинает попытки повторного подключения. Вы можете справиться с этим событием, если вы хотите, чтобы ваше приложение приняло некоторые меры, когда транспортное соединение потеряно. Период тайм-аута по умолчанию в настоящее время составляет 20 секунд.

    Если ваш клиентский код пытается вызвать метод концентратора, пока SignalR находится в режиме повторного подключения, SignalR попытается отправить команду. В большинстве случаев такие попытки не увенчаются успехом, но в некоторых случаях они могут увенчаться успехом. Для событий, отправляемых на сервер, навсегда кадра и длительных переносов опроса, SignalR использует два канала связи, один из них клиент использует для отправки сообщений и тот, который он использует для получения сообщений. Канал, используемый для получения, является постоянно открытым, и это тот, который закрывается, когда физическое соединение прерывается. Канал, используемый для отправки остается доступным, поэтому, если физическое подключение будет восстановлено, вызов метода от клиента к серверу может быть успешным до того, как канал получения будет восстановлен. Возвратное значение не будет получено до тех пор, пока SignalR не откроет канал, используемый для получения.
- `Reconnected`клиентского события.

    Поднят о восстановлении транспортного сообщения. Обработчик `OnReconnected` событий в концентраторе выполняет.
- `Closed`событие клиента`disconnected` (событие в JavaScript).

    Поднятый, когда период отключения ключа истекает, в то время как клиентский код SignalR пытается восстановить соединение после потери транспортного соединения. Время отключения по умолчанию составляет 30 секунд. (Это событие также возникает, когда `Stop` соединение заканчивается, потому что метод вызывается.)

Перебои с транспортным соединением, которые не обнаруживаются транспортным API и не задерживают прием пингов keepalive с сервера дольше, чем период предупреждения о тайм-ауте keepalive, могут не привести к поднятию каких-либо событий, вызванных пожизненным периодом подключения.

Некоторые сетевые среды намеренно закрывают холостые соединения, а другая функция пакетов keepalive заключается в том, чтобы помочь предотвратить это, сообщив этим сетям, что используется соединение SignalR. В крайних случаях частоты keepalive pings по умолчанию может быть недостаточно для предотвращения закрытых подключений. В этом случае вы можете настроить keepalive пинги, которые будут отправлены чаще. Для получения дополнительной информации смотрите [настройки Тайм-аута и keepalive](#timeoutkeepalive) позже в этой теме.

> [!NOTE]
>
> **Важно**: Последовательность событий, описанных здесь, не гарантируется. SignalR делает все возможное для повышения жизненных событий соединения предсказуемым образом в соответствии с этой схемой, но существует множество различных сетевых событий и множество способов, с помощью которых основные коммуникационные системы, такие как транспортные AI, обрабатывают их. Например, `Reconnected` событие может не быть поднято при повторном подключении клиента или `OnConnected` обработчик на сервере может быть запущен, когда попытка установить соединение не увенчалась успехом. Эта тема описывает только эффекты, которые обычно производятся определенными типичными обстоятельствами.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>Сценарии отключения клиента

В клиенте браузера клиентский код SignalR, который поддерживает соединение SignalR, работает в контексте JavaScript веб-страницы. Вот почему соединение SignalR должно заканчиваться при переходе с одной страницы на другую, и именно поэтому у вас есть несколько подключений с несколькими идентификаторами связи, если вы подключаетесь из нескольких окон браузера или вкладок. Когда пользователь закрывает окно или вкладку браузера, или переходит на новую страницу или обновляет страницу, соединение SignalR немедленно заканчивается, потому что клиентский код SignalR обрабатывает это событие браузера для вас и вызывает `Stop` метод. В этих сценариях или на любой `Stop` клиентской `OnDisconnected` платформе, когда приложение вызывает метод, обработчик событий выполняет сятворчивое непосредственно на сервере, и клиент поднимает `Closed` событие (событие названо `disconnected` в JavaScript).

Если клиентское приложение или компьютер, который работает на сбои или переходит в спящий режим (например, когда пользователь закрывает ноутбук), сервер не информируется о том, что произошло. Насколько известно серверу, потеря клиента может быть вызвана прерыванием подключения, и клиент может попытаться восстановить соединение. Таким образом, в этих сценариях сервер ждет, чтобы дать `OnDisconnected` клиенту возможность повторного подключения, и не выполняется до истечения периода отключения времени (около 30 секунд по умолчанию). Следующая диаграмма иллюстрирует этот сценарий.

![Сбой в работе клиентского компьютера](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Сценарии отключения сервера

Когда сервер переходит в автономный режим - он перезагружается, выходит из строя, утилизирует домен приложения и т.д. - результат может быть похож на потерянное соединение, или транспортный API и SignalR могут сразу же узнать, что сервер исчез, и SignalR может начать пытаться восстановить связь, не поднимая `ConnectionSlow` события. Если клиент переходит в режим повторного подключения, и если сервер восстанавливается или перезапускается или новый сервер будет введен в строй до истечения периода отключения, клиент будет повторно подключаться к восстановленному или новому серверу. В этом случае подключение SignalR продолжается `Reconnected` на клиенте и событие поднимается. На первом сервере, `OnDisconnected` никогда не выполняется, `OnReconnected` и на `OnConnected` новом сервере, выполняется, хотя никогда не был выполнен для этого клиента на этом сервере раньше. (Эффект тот же, если клиент воссоединяется с тем же сервером после перезагрузки или рециркуляции домена приложения, потому что при перезагрузке сервера у него нет памяти о предыдущей активности подключения.) Следующая диаграмма предполагает, что транспортный API сразу же `ConnectionSlow` узнает о потерянном подключении, поэтому событие не поднимается.

![Сбой и переподключение сервера](handling-connection-lifetime-events/_static/image5.png)

Если сервер не становится доступным в период отключения, соединение SignalR заканчивается. В этом случае `Closed` событие`disconnected` (в JavaScript клиентов) `OnDisconnected` поднимается на клиента, но никогда не вызывается на сервере. Следующая диаграмма предполагает, что транспортный API не узнает о потерянном подключении, поэтому `ConnectionSlow` он обнаруживается функциональностью SignalR keepalive и событие поднимается.

![Сбой и тайм-аут сервера](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Настройки тайм-аута и сохранения

Значения `ConnectionTimeout`по `DisconnectTimeout`умолчанию и `KeepAlive` значения подходят для большинства сценариев, но могут быть изменены, если среда имеет особые потребности. Например, если сетевая среда закрывает соединения, которые простаивают в течение 5 секунд, возможно, придется уменьшить значение keepalive.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

Этот параметр представляет собой время, чтобы оставить транспортное соединение открытым и ждать ответа, прежде чем закрыть его и открыть новое соединение. Значение по умолчанию составляет 110 секунд.

Эта настройка применяется только тогда, когда функция keepalive отключена, что обычно применяется только к длительному транспорту для голосования. Следующая диаграмма иллюстрирует влияние этого параметра на длительное транспортное соединение для голосования.

![Длинное транспортное соединение для голосования](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>ОтключениеTimeout

Этот параметр представляет собой время ожидания после потери транспортного соединения перед поднятием `Disconnected` события. Значение по умолчанию — 30 секунд. При установке, `DisconnectTimeout` `KeepAlive` `DisconnectTimeout` автоматически устанавливается 1/3 от значения.

<a id="keepalive"></a>

### <a name="keepalive"></a>Keepalive

Этот параметр представляет собой время ожидания перед отправкой пакета keepalive по простояю соединения. Значение по умолчанию — 10 секунд. Это значение не должно быть больше, `DisconnectTimeout` чем 1/3 от значения.

Если вы хотите `DisconnectTimeout` установить `KeepAlive` оба `DisconnectTimeout`и, `KeepAlive`установить после . В `KeepAlive` противном случае параметр будет перезаписан при `DisconnectTimeout` автоматическом наборе `KeepAlive` до 1/3 значения тайм-аута.

Если вы хотите отключить функцию keepalive, установите `KeepAlive` на нулевую. Функциональность Keepalive автоматически отключается для длительного транспортировки.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>Как изменить настройки тайм-аута и сохранить

Чтобы изменить значения по умолчанию для этих `Application_Start` параметров, установите их в *файле Global.asax,* как показано в следующем примере. Значения, указанные в коде выборки, такие же, как и значения по умолчанию.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>Как уведомить пользователя об отключении

В некоторых приложениях может потребоваться отобразить сообщение пользователю при вознике проблемы с подключением. У вас есть несколько вариантов того, как и когда это сделать. Следующие образцы кода для клиента JavaScript с помощью генерируемого прокси.

- Обработка `connectionSlow` события для отображения сообщения, как только SignalR знает о проблемах соединения, прежде чем он переходит в режим повторного подключения.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- Обработка `reconnecting` события для отображения сообщения, когда SignalR знает об отключении и перешел в режим повторного подключения.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Обработка `disconnected` события для отображения сообщения, когда попытка повторного подключения приурочена к этому. В этом случае единственным способом восстановить соединение с сервером является перезагрузка соединения SignalR, позвонив `Start` в метод, который создаст новый идентификатор соединения. Следующий пример кода использует флаг, чтобы убедиться, что вы выдаете уведомление только после повторного тайм-аута, а не после нормального окончания соединения SignalR, вызванного вызовом метода. `Stop`

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Как постоянно воссоединиться

В некоторых приложениях может потребоваться автоматически восстановить соединение после его потери и время от времени попытка повторного подключения. Для этого можно вызвать `Start` метод `Closed` от обработчика событий (обработчик`disconnected` событий на клиентах JavaScript). Вы можете подождать некоторое время, прежде чем звонить, `Start` чтобы избежать этого слишком часто, когда сервер или физическое соединение недоступны. Следующий пример кода предназначен для клиента JavaScript, использующего сгенерированный прокси.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Потенциальная проблема, о которой следует знать мобильным клиентам, заключается в том, что непрерывные попытки переподключения при недоступности сервера или физического соединения могут привести к ненужной утечке батареи.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Как отключить клиента в серверном коде

Версия SignalR 2 не имеет встроенного сервера API для отключения клиентов. Есть [планы по добавлению этой функциональности в будущем.](https://github.com/SignalR/SignalR/issues/2101) В текущем выпуске SignalR самый простой способ отключить клиента от сервера — реализовать метод отключения клиента и вызвать этот метод с сервера. Следующий пример кода показывает метод отключения для клиента JavaScript с помощью генерируемого прокси.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Безопасность - Ни этот метод для отключения клиентов, ни предлагаемый встроенный API не будут рассматривать сценарий взломанных клиентов, `stopClient` которые работают вредоносный код, так как клиенты могут повторно подключиться или взломанный код может удалить метод или изменить то, что он делает. Подходящее место для реализации защиты от состояния отказа в обслуживании (DOS) находится не в рамочном или серверном слое, а скорее в передний конец инфраструктуры.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>Обнаружение причины отключения

SignalR 2.1 добавляет перегрузку `OnDisconnect` на событие сервера, которая указывает, если клиент намеренно отключен, а не время. Параметр `StopCalled` верен, если клиент явно закрыл соединение. В JavaScript, если ошибка сервера привела клиента к отключению, информация об ошибке будет передана клиенту как `$.connection.hub.lastError`.

**Код сервера `stopCalled` На КЗ: параметр**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**Клиентский код JavaScript: доступ `lastError` в `disconnect` случае.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
