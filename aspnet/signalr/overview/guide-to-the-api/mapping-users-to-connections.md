---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: Картирование пользователей SignalR к соединениям (ru) Документы Майкрософт
author: bradygaster
description: Эта тема показывает, как сохранить информацию о пользователях и их соединениях. Патрик Флетчер помог написать эту тему. Версии программного обеспечения, используемые в этой теме...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675781"
---
# <a name="mapping-signalr-users-to-connections"></a>Сопоставление пользователей SignalR с подключениями

; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Эта тема показывает, как сохранить информацию о пользователях и их соединениях.
>
> Патрик Флетчер помог написать эту тему.
>
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемые в этой теме
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

## <a name="introduction"></a>Вступление

Каждый клиент, подключенный к концентратору, проходит уникальный идентификатор соединения. Это значение можно получить `Context.ConnectionId` в свойстве контекста концентратора. Если приложению необходимо сопоставить пользователя с идентификатором соединения и сохранить его, можно использовать одно из следующих:

- [Поставщик идентификатора пользователя (SignalR 2)](#IUserIdProvider)
- [Хранилище в памяти,](#inmemory)например, словарь
- [Группа SignalR для каждого пользователя](#groups)
- [Постоянное внешнее хранилище,](#database)например таблица баз данных или хранилище таблицы Azure

Каждая из этих реализаций показана в этой теме. Для отслеживания `OnDisconnected`состояния `OnReconnected` подключения пользователя `Hub` используются `OnConnected`методы класса.

Наилучший подход к приложению зависит от:

- Количество веб-серверов, худающих ваше приложение.
- Нужно ли получать список подключенных пользователей.
- Нужно ли сохранять групповую и пользовательскую информацию при перезагрузке приложения или сервера.
- Является ли задержка вызова внешнего сервера проблемой.

В следующей таблице показано, какой подход работает для этих соображений.

|  | Более одного сервера | Получить список подключенных пользователей, подключенных к настоящее время | Сохраняя информацию после перезагрузки | Оптимальная производительность |
| --- | --- | --- | --- | --- |
| Поставщик userID | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| В памяти |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Группы для пользователей | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Постоянный, внешний | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>Поставщик IUserID

Эта функция позволяет пользователям указать, что userId основан на IRequest через новый интерфейс IUserIdProvider.

**The IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

По умолчанию будет реализована реализация, которая `IPrincipal.Identity.Name` использует имя пользователя в качестве имени пользователя. Чтобы изменить это, зарегистрируйте реализацию `IUserIdProvider` с глобальным хостом, когда приложение начинается:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

В пределах концентратора вы сможете отправлять сообщения этим пользователям через следующий API:

**Отправка сообщения конкретному пользователю**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Хранение памяти в памяти

Ниже приведены следующие примеры, как сохранить соединение и информацию о пользователе в словаре, который хранится в памяти. Словарь использует `HashSet` для хранения идентификатора соединения. В любое время пользователь может иметь более одного подключения к приложению SignalR. Например, пользователь, подключенный через несколько устройств или более одной вкладки браузера, будет иметь более одного идентификатора соединения.

Если приложение выключается, вся информация будет потеряна, но она будет повторно заселена по мере восстановления своих соединений. Хранилище памяти не работает, если среда включает в себя более одного веб-сервера, потому что каждый сервер будет иметь отдельную коллекцию соединений.

Первый пример показывает класс, который управляет картированием пользователей к соединениям. Ключом к HashSet будет имя пользователя.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

В следующем примере показано, как использовать класс отображения соединения из концентратора. Экземпляр класса хранится в переменном `_connections`имени.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Группы для пользователей

Вы можете создать группу для каждого пользователя, а затем отправить сообщение этой группе, когда вы хотите достичь только этого пользователя. Имя каждой группы — это имя пользователя. Если у пользователя более одного соединения, каждый идентификатор соединения добавляется в группу пользователя.

Вы не должны вручную удалять пользователя из группы при отключении пользователя. Это действие автоматически выполняется системой SignalR.

В следующем примере показано, как реализовать группы пользователей для пользователей.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Постоянное внешнее хранение

В этой теме показано, как использовать базу данных или хранилище таблиц Azure для хранения информации о подключении. Этот подход работает, когда у вас есть несколько веб-серверов, потому что каждый веб-сервер может взаимодействовать с тем же хранилищем данных. Если веб-серверы перестают работать или `OnDisconnected` приложение перезапускается, метод не вызывается. Таким образом, возможно, что репозиторий данных будет иметь записи для идентификаторов соединения, которые больше не действительны. Для очистки этих осиротевших записей может потребоваться аннулировать любое соединение, созданное вне временных рамок, имеющих отношение к приложению. Примеры в этом разделе включают значение для отслеживания, когда соединение было создано, но не показывают, как очистить старые записи, потому что вы можете сделать это в качестве фонового процесса.

### <a name="database"></a>База данных

Ниже приведены следующие примеры, как сохранить соединение и пользовательскую информацию в базе данных. Вы можете использовать любую технологию доступа к данным; однако приведенный ниже пример показывает, как определить модели с помощью рамочной системы entity. Эти модели сущности соответствуют таблицам баз данных и полям. Структура данных может значительно отличаться в зависимости от требований приложения.

Первый пример показывает, как определить сущность пользователя, которая может быть связана со многими объектами соединения.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Затем из концентратора можно отслеживать состояние каждого соединения с кодом, показанным ниже.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Хранилище таблиц Azure

Следующий пример таблицы Azure похож на пример базы данных. Он не включает в себя всю информацию, необходимую для запуска службы хранения таблицЫ Azure. Для получения информации см. [Как использовать хранилище таблицы от .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

В следующем примере показана сущность таблицы для хранения информации о подключении. Он разъединяет данные по имени пользователя и идентифицирует каждую сущность по идентификатору соединения, так что пользователь может иметь несколько подключений в любое время.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

В концентраторе вы отслеживаете состояние соединения каждого пользователя.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
