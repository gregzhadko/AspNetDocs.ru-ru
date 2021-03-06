---
uid: signalr/overview/getting-started/supported-platforms
title: Поддерживаемые платформы | Документация Майкрософт
author: bradygaster
description: В этой статье описывается, какие клиенты и серверы поддерживаются SignalR.
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450126"
---
# <a name="supported-platforms"></a>Поддерживаемые платформы

по [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этой статье описывается, какие клиенты и серверы поддерживаются SignalR. 
> 
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
> 
> Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).

SignalR поддерживается в различных конфигурациях сервера и клиента. Кроме того, каждый вариант транспорта имеет собственный набор требований; Если требования к системе для транспорта недоступны, SignalR будет корректно отработкой отказа на другие транспортные протоколы. Дополнительные сведения о транспортах, поддерживаемых SignalR, см. в разделе [транспорты и резервные](introduction-to-signalr.md#transports).

## <a name="server-system-requirements"></a>Системные требования к  Server

Серверный компонент SignalR может размещаться в различных конфигурациях сервера. В этом разделе описаны поддерживаемые версии операционных систем, .NET Framework, Internet Information Server и других компонентов.

### <a name="supported-server-operating-systems"></a>Поддерживаемые серверные операционные системы

Серверный компонент SignalR может размещаться в следующих серверных или клиентских операционных системах. Обратите внимание, что для использования WebSockets требуется Windows Server 2012, Windows Server 2016 или Windows 8 (сокет можно использовать на веб-сайтах Windows Azure, если в качестве версии .NET Framework для сайта установлено значение 4,5, а веб-сокеты включены на сайте Страница "Конфигурация").

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 R2
- Windows 10
- Windows 8
- Windows 7
- Microsoft Azure

### <a name="supported-server-net-framework-version"></a>Поддерживаемая версия .NET Framework сервера

SignalR 2 поддерживается только в .NET Framework 4,5. Обновления, повышающие надежность, совместимость, стабильность и производительность, см. в разделе [Рекомендуемые обновления](#updates) .

### <a name="supported-server-iis-versions"></a>Поддерживаемые версии сервера IIS

При размещении SignalR в службах IIS поддерживаются следующие версии. Обратите внимание, что при использовании клиентской операционной системы, например, для разработки (Windows 8 или Windows 7), не следует использовать полные версии IIS или Cassini, так как будет установлено ограничение в 10 одновременных подключений, которое будет достигнуто очень быстро с момента подключения. являются временными, часто переустановленными и не удаляются сразу после того, как они больше не используются. IIS Express следует использовать в клиентских операционных системах.

Также обратите внимание, что для использования WebSocket необходимо использовать IIS 8 или IIS 8 Express, сервер должен использовать Windows 8, Windows Server 2012 или более поздней версии, а в IIS должен быть включен протокол WebSocket. Сведения о том, как включить WebSocket в IIS, см. в разделе [Поддержка протокола WebSocket iis 8,0](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).

- IIS 8 или IIS 8 Express.
- IIS 7 и 7,5. Требуется поддержка [URL-адресов](https://support.microsoft.com/kb/980368) , поддерживающих расширение.
- Службы IIS должны работать в интегрированном режиме. Классический режим не поддерживается. Если служба IIS работает в классическом режиме с использованием транспорта событий, отправленных сервером, может возникнуть задержка в сообщениях до 30 секунд.
- Размещенное приложение должно работать в режиме полного доверия.

## <a name="client-system-requirements"></a>Системные требования для клиента

SignalR можно использовать на различных клиентских платформах. В этом разделе описываются требования к системе для использования SignalR в веб-браузерах, классических приложениях Windows, приложениях Silverlight и мобильных устройствах.

### <a name="web-browsers"></a>Веб-браузеры

SignalR можно использовать в различных веб-браузерах, но, как правило, поддерживаются только последние две версии.

Приложения, использующие SignalR в браузерах, должны использовать jQuery версии 1.6.4 или основные более поздние версии (например, 1.7.2, 1.8.2 или 1.9.1).

SignalR можно использовать в следующих браузерах:

- Microsoft Internet Explorer версий 8, 9, 10 и 11. Поддерживаются современные, настольные и мобильные версии.
- Mozilla Firefox: Текущая версия-1, версии Windows и Mac.
- Google Chrome: Текущая версия-1, версии Windows и Mac.
- Safari: Current версии 1, версии Mac и iOS.
- Opera: Текущая версия-1, только Windows.
- Браузер Android

Помимо использования определенных браузеров, различные транспорты, используемые SignalR, имеют свои требования. В следующих конфигурациях поддерживаются следующие транспорты:

<a id="browser"></a>

**Требования к транспортировке веб-браузера**

| Транспортировка | Internet Explorer | Chrome (Windows или iOS) | Firefox | Safari (OSX или iOS) | Android |
| --- | --- | --- | --- | --- | --- |
| Подключения WebSocket | 10+ | Current-1 | Current-1 | Current-1 | Недоступно |
| События, отправленные сервером | Недоступно | Current-1 | Current-1 | Current-1 | Недоступно |
| фореверфраме | 8 или выше | Недоступно | Недоступно | Недоступно | 4.1 |
| Длительный опрос | 8 или выше | Current-1 | Current-1 | Current-1 | 4.1 |

\*: 6 + требуется для полной функциональности.

#### <a name="unsupported-browsers"></a>Неподдерживаемые браузеры

В то время как SignalR *может* работать без серьезных проблем в старых версиях браузера, мы не тестируем SignalR в них и, как правило, не исправляют ошибки, которые могут появиться в них.

### <a name="windows-desktop-and-silverlight-applications"></a>Классические приложения Windows и Silverlight

В дополнение к запуску в веб-браузере SignalR может размещаться в автономном клиенте Windows или в приложениях Silverlight. Приложения Windows Desktop и Silverlight SignalR имеют следующие требования к системе.

- Приложения, использующие .NET 4, поддерживаются в Windows XP SP3 или более поздней версии.
- Приложения, использующие .NET Framework 4,5, поддерживаются в Windows Vista и более поздних версиях.

Помимо требований к операционной системе и .NET Framework, транспортам, доступным для SignalR, предъявляются собственные требования. В следующих конфигурациях поддерживаются следующие транспорты:

**Требования к транспортировке Windows Desktop и Silverlight**

| Транспортировка | Приложение .NET | Silverlight |
| --- | --- | --- |
| веб-сокеты | Windows 8 + и .NET 4.5 + | Недоступно |
| Непрерывная рамка | Недоступно | Недоступно |
| События, отправленные сервером | .NET 4 + | 5+ |
| Длительный опрос | .NET 4 + | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Приложения для Магазина Windows и Windows Phone

SignalR можно использовать в приложениях для Магазина Windows и Windows Phone 8 приложений. В следующих конфигурациях поддерживаются следующие транспорты:

**Требования к транспортному хранилищу Windows и Windows Phone**

| Транспортировка | Магазин Windows/.NET | Магазин Windows/JavaScript | Windows Phone и IE | Windows Phone/.NET |
| --- | --- | --- | --- | --- |
| Подключения WebSocket | Недоступно | Win8 + | 8 или выше | Недоступно |
| Непрерывная рамка | Недоступно | Win8 + | 7.5 или выше | Недоступно |
| События, отправленные сервером | Win8 + | Недоступно | Недоступно | 8 или выше |
| Длительный опрос | Win8 + | Win8 + | 7.5 или выше | 8 или выше |

<a id="updates"></a>

## <a name="recommended-updates"></a>Рекомендуемые обновления

Для серверов SignalR рекомендуются следующие обновления:

- Обновление для .NET Framework 4,5 можно найти [здесь](https://support.microsoft.com/kb/2750149).
- Корпорация Майкрософт будет периодически выпускать QFE для ASP.NET. Их следует применять как доступные.
