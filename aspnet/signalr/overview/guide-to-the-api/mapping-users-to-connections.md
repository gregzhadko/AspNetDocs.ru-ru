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
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="5126c-105">Сопоставление пользователей SignalR с подключениями</span><span class="sxs-lookup"><span data-stu-id="5126c-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="5126c-106">; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5126c-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5126c-107">Эта тема показывает, как сохранить информацию о пользователях и их соединениях.</span><span class="sxs-lookup"><span data-stu-id="5126c-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="5126c-108">Патрик Флетчер помог написать эту тему.</span><span class="sxs-lookup"><span data-stu-id="5126c-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5126c-109">Версии программного обеспечения, используемые в этой теме</span><span class="sxs-lookup"><span data-stu-id="5126c-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="5126c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5126c-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="5126c-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5126c-111">.NET 4.5</span></span>
> - <span data-ttu-id="5126c-112">Версия SignalR 2</span><span class="sxs-lookup"><span data-stu-id="5126c-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="5126c-113">Предыдущие версии этой темы</span><span class="sxs-lookup"><span data-stu-id="5126c-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="5126c-114">Для получения информации о более ранних версиях SignalR, см [SignalR Старые версии](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="5126c-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="5126c-115">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="5126c-115">Questions and comments</span></span>
>
> <span data-ttu-id="5126c-116">Пожалуйста, оставьте обратную связь о том, как вам понравился этот учебник и что мы могли бы улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5126c-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5126c-117">Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com.](http://stackoverflow.com/)</span><span class="sxs-lookup"><span data-stu-id="5126c-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="5126c-118">Вступление</span><span class="sxs-lookup"><span data-stu-id="5126c-118">Introduction</span></span>

<span data-ttu-id="5126c-119">Каждый клиент, подключенный к концентратору, проходит уникальный идентификатор соединения. Это значение можно получить `Context.ConnectionId` в свойстве контекста концентратора.</span><span class="sxs-lookup"><span data-stu-id="5126c-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="5126c-120">Если приложению необходимо сопоставить пользователя с идентификатором соединения и сохранить его, можно использовать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="5126c-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="5126c-121">Поставщик идентификатора пользователя (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="5126c-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="5126c-122">[Хранилище в памяти,](#inmemory)например, словарь</span><span class="sxs-lookup"><span data-stu-id="5126c-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="5126c-123">Группа SignalR для каждого пользователя</span><span class="sxs-lookup"><span data-stu-id="5126c-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="5126c-124">[Постоянное внешнее хранилище,](#database)например таблица баз данных или хранилище таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="5126c-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="5126c-125">Каждая из этих реализаций показана в этой теме.</span><span class="sxs-lookup"><span data-stu-id="5126c-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="5126c-126">Для отслеживания `OnDisconnected`состояния `OnReconnected` подключения пользователя `Hub` используются `OnConnected`методы класса.</span><span class="sxs-lookup"><span data-stu-id="5126c-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="5126c-127">Наилучший подход к приложению зависит от:</span><span class="sxs-lookup"><span data-stu-id="5126c-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="5126c-128">Количество веб-серверов, худающих ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="5126c-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="5126c-129">Нужно ли получать список подключенных пользователей.</span><span class="sxs-lookup"><span data-stu-id="5126c-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="5126c-130">Нужно ли сохранять групповую и пользовательскую информацию при перезагрузке приложения или сервера.</span><span class="sxs-lookup"><span data-stu-id="5126c-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="5126c-131">Является ли задержка вызова внешнего сервера проблемой.</span><span class="sxs-lookup"><span data-stu-id="5126c-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="5126c-132">В следующей таблице показано, какой подход работает для этих соображений.</span><span class="sxs-lookup"><span data-stu-id="5126c-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="5126c-133">Более одного сервера</span><span class="sxs-lookup"><span data-stu-id="5126c-133">More than one server</span></span> | <span data-ttu-id="5126c-134">Получить список подключенных пользователей, подключенных к настоящее время</span><span class="sxs-lookup"><span data-stu-id="5126c-134">Get list of currently connected users</span></span> | <span data-ttu-id="5126c-135">Сохраняя информацию после перезагрузки</span><span class="sxs-lookup"><span data-stu-id="5126c-135">Persist information after restarts</span></span> | <span data-ttu-id="5126c-136">Оптимальная производительность</span><span class="sxs-lookup"><span data-stu-id="5126c-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5126c-137">Поставщик userID</span><span class="sxs-lookup"><span data-stu-id="5126c-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="5126c-138">В памяти</span><span class="sxs-lookup"><span data-stu-id="5126c-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="5126c-139">Группы для пользователей</span><span class="sxs-lookup"><span data-stu-id="5126c-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="5126c-140">Постоянный, внешний</span><span class="sxs-lookup"><span data-stu-id="5126c-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="5126c-141">Поставщик IUserID</span><span class="sxs-lookup"><span data-stu-id="5126c-141">IUserID provider</span></span>

<span data-ttu-id="5126c-142">Эта функция позволяет пользователям указать, что userId основан на IRequest через новый интерфейс IUserIdProvider.</span><span class="sxs-lookup"><span data-stu-id="5126c-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="5126c-143">**The IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="5126c-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="5126c-144">По умолчанию будет реализована реализация, которая `IPrincipal.Identity.Name` использует имя пользователя в качестве имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="5126c-145">Чтобы изменить это, зарегистрируйте реализацию `IUserIdProvider` с глобальным хостом, когда приложение начинается:</span><span class="sxs-lookup"><span data-stu-id="5126c-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="5126c-146">В пределах концентратора вы сможете отправлять сообщения этим пользователям через следующий API:</span><span class="sxs-lookup"><span data-stu-id="5126c-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="5126c-147">**Отправка сообщения конкретному пользователю**</span><span class="sxs-lookup"><span data-stu-id="5126c-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="5126c-148">Хранение памяти в памяти</span><span class="sxs-lookup"><span data-stu-id="5126c-148">In-memory storage</span></span>

<span data-ttu-id="5126c-149">Ниже приведены следующие примеры, как сохранить соединение и информацию о пользователе в словаре, который хранится в памяти.</span><span class="sxs-lookup"><span data-stu-id="5126c-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="5126c-150">Словарь использует `HashSet` для хранения идентификатора соединения. В любое время пользователь может иметь более одного подключения к приложению SignalR.</span><span class="sxs-lookup"><span data-stu-id="5126c-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="5126c-151">Например, пользователь, подключенный через несколько устройств или более одной вкладки браузера, будет иметь более одного идентификатора соединения.</span><span class="sxs-lookup"><span data-stu-id="5126c-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="5126c-152">Если приложение выключается, вся информация будет потеряна, но она будет повторно заселена по мере восстановления своих соединений.</span><span class="sxs-lookup"><span data-stu-id="5126c-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="5126c-153">Хранилище памяти не работает, если среда включает в себя более одного веб-сервера, потому что каждый сервер будет иметь отдельную коллекцию соединений.</span><span class="sxs-lookup"><span data-stu-id="5126c-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="5126c-154">Первый пример показывает класс, который управляет картированием пользователей к соединениям.</span><span class="sxs-lookup"><span data-stu-id="5126c-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="5126c-155">Ключом к HashSet будет имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="5126c-156">В следующем примере показано, как использовать класс отображения соединения из концентратора.</span><span class="sxs-lookup"><span data-stu-id="5126c-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="5126c-157">Экземпляр класса хранится в переменном `_connections`имени.</span><span class="sxs-lookup"><span data-stu-id="5126c-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="5126c-158">Группы для пользователей</span><span class="sxs-lookup"><span data-stu-id="5126c-158">Single-user groups</span></span>

<span data-ttu-id="5126c-159">Вы можете создать группу для каждого пользователя, а затем отправить сообщение этой группе, когда вы хотите достичь только этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="5126c-160">Имя каждой группы — это имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="5126c-161">Если у пользователя более одного соединения, каждый идентификатор соединения добавляется в группу пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="5126c-162">Вы не должны вручную удалять пользователя из группы при отключении пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="5126c-163">Это действие автоматически выполняется системой SignalR.</span><span class="sxs-lookup"><span data-stu-id="5126c-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="5126c-164">В следующем примере показано, как реализовать группы пользователей для пользователей.</span><span class="sxs-lookup"><span data-stu-id="5126c-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="5126c-165">Постоянное внешнее хранение</span><span class="sxs-lookup"><span data-stu-id="5126c-165">Permanent, external storage</span></span>

<span data-ttu-id="5126c-166">В этой теме показано, как использовать базу данных или хранилище таблиц Azure для хранения информации о подключении.</span><span class="sxs-lookup"><span data-stu-id="5126c-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="5126c-167">Этот подход работает, когда у вас есть несколько веб-серверов, потому что каждый веб-сервер может взаимодействовать с тем же хранилищем данных.</span><span class="sxs-lookup"><span data-stu-id="5126c-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="5126c-168">Если веб-серверы перестают работать или `OnDisconnected` приложение перезапускается, метод не вызывается.</span><span class="sxs-lookup"><span data-stu-id="5126c-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="5126c-169">Таким образом, возможно, что репозиторий данных будет иметь записи для идентификаторов соединения, которые больше не действительны.</span><span class="sxs-lookup"><span data-stu-id="5126c-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="5126c-170">Для очистки этих осиротевших записей может потребоваться аннулировать любое соединение, созданное вне временных рамок, имеющих отношение к приложению.</span><span class="sxs-lookup"><span data-stu-id="5126c-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="5126c-171">Примеры в этом разделе включают значение для отслеживания, когда соединение было создано, но не показывают, как очистить старые записи, потому что вы можете сделать это в качестве фонового процесса.</span><span class="sxs-lookup"><span data-stu-id="5126c-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="5126c-172">База данных</span><span class="sxs-lookup"><span data-stu-id="5126c-172">Database</span></span>

<span data-ttu-id="5126c-173">Ниже приведены следующие примеры, как сохранить соединение и пользовательскую информацию в базе данных.</span><span class="sxs-lookup"><span data-stu-id="5126c-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="5126c-174">Вы можете использовать любую технологию доступа к данным; однако приведенный ниже пример показывает, как определить модели с помощью рамочной системы entity.</span><span class="sxs-lookup"><span data-stu-id="5126c-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="5126c-175">Эти модели сущности соответствуют таблицам баз данных и полям.</span><span class="sxs-lookup"><span data-stu-id="5126c-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="5126c-176">Структура данных может значительно отличаться в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="5126c-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="5126c-177">Первый пример показывает, как определить сущность пользователя, которая может быть связана со многими объектами соединения.</span><span class="sxs-lookup"><span data-stu-id="5126c-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="5126c-178">Затем из концентратора можно отслеживать состояние каждого соединения с кодом, показанным ниже.</span><span class="sxs-lookup"><span data-stu-id="5126c-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="5126c-179">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="5126c-179">Azure table storage</span></span>

<span data-ttu-id="5126c-180">Следующий пример таблицы Azure похож на пример базы данных.</span><span class="sxs-lookup"><span data-stu-id="5126c-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="5126c-181">Он не включает в себя всю информацию, необходимую для запуска службы хранения таблицЫ Azure.</span><span class="sxs-lookup"><span data-stu-id="5126c-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="5126c-182">Для получения информации см. [Как использовать хранилище таблицы от .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="5126c-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="5126c-183">В следующем примере показана сущность таблицы для хранения информации о подключении.</span><span class="sxs-lookup"><span data-stu-id="5126c-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="5126c-184">Он разъединяет данные по имени пользователя и идентифицирует каждую сущность по идентификатору соединения, так что пользователь может иметь несколько подключений в любое время.</span><span class="sxs-lookup"><span data-stu-id="5126c-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="5126c-185">В концентраторе вы отслеживаете состояние соединения каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="5126c-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
