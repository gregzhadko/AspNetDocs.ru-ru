---
uid: signalr/overview/older-versions/working-with-groups
title: Работа с группами в SignalR 1.x | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как сохранять данные членства в группе с помощью API концентратора.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: e8ef7b34af4341fb97f54e2aab1d8971cce46af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026931"
---
<a name="working-with-groups-in-signalr-1x"></a>Работа с группами в SignalR 1.x
====================
по [Флетчера Патрик](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом разделе описывается добавление пользователей в группы и сохранять данные членства в группе.


## <a name="overview"></a>Обзор

Группами в SignalR предоставляют метод широковещательная рассылка сообщений для заданного подмножества подключенных клиентов. Группа может иметь любое число клиентов, и клиент может быть членом любое количество групп. Не нужно явно создавать группы. По сути группа автоматически создается первый раз, укажите его имя в вызове Groups.Add, и она будет удалена при удалении последнего соединения из членства в ней. Введение в использование групп, см. в разделе [как управлять членством в группах из классу Hub](index.md) в API концентраторов — руководство по Server.

Не существует API для получения списка членства в группе или список групп. SignalR отправляет сообщения клиентов и группы на основе модели публикации и подписки, а сервер не ведет список групп или членства в группах. Это помогает добиться максимальной масштабируемости, так как каждый раз при добавлении узла к веб-ферме, любое состояние, которое поддерживает SignalR должен быть распространены на новый узел.

При добавлении пользователя в группу с помощью `Groups.Add` метод, пользователь получает сообщения, направленных в эту группу, в течение текущего соединения, но членства пользователя в этой группе не сохраняется вне текущего соединения. Если вы хотите окончательно сохранить сведения о группах и членства в группе, необходимо хранить их в репозитории, например базы данных или хранилище таблиц Azure. Затем каждый раз при подключении пользователя к приложению, извлечь из хранилища, каким группам принадлежит пользователь и вручную добавить этого пользователя к группам.

При повторном подключении после к временному нарушению работы, пользователь автоматически повторно присоединяет ранее назначенные группы. Автоматическое повторное присоединение группы применяется только при повторном подключении не в том случае, при установке нового подключения. Токен цифровую подпись передается от клиента, который содержит список ранее назначенные группы. Если вы хотите проверить, принадлежит ли пользователь в запрошенной группы, можно переопределить поведение по умолчанию.

Этот раздел включает следующие подразделы:

- [Добавление и удаление пользователей](#add)
- [Вызов членов группы](#call)
- [Хранение в базе данных членства в группе](#storedatabase)
- [Сохранение членства в группе в хранилище таблиц Azure](#storeazuretable)
- [Проверка членства в группе, при повторном подключении](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>Добавление и удаление пользователей

Чтобы добавить или удалить пользователей из группы, следует вызвать [добавить](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) или [удалить](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) методы и передайте идентификатор соединения пользователя и имя группы в качестве параметров. Необходимо вручную удалить пользователя из группы, по окончании соединения.

В следующем примере показан `Groups.Add` и `Groups.Remove` методы, используемые в методах Hub.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` И `Groups.Remove` методы асинхронного выполнения.

Если вы хотите добавить в клиент группу и немедленно отправить клиенту сообщение с помощью в группу, необходимо убедитесь в том, что метод Groups.Add завершается первой. В следующих примерах кода показано, как это сделать с помощью кода, который работает в .NET 4.5, а другой с помощью кода, который работает в .NET 4.

#### <a name="asynchronous-net-45-example"></a>Асинхронные .NET 4.5 пример

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>Асинхронные .NET 4 пример

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

В общем случае не следует включать `await` при вызове `Groups.Remove` метод так как идентификатор подключения, который вы пытаетесь удалить больше не могут быть доступны. В этом случае `TaskCanceledException` возникает после тайм-аута запроса. Если приложение должно убедиться, что пользователь удален из группы перед отправкой сообщения в группу, можно добавить `await` перед Groups.Remove, а затем catch `TaskCanceledException` исключение, которое может быть создано.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>Вызов членов группы

Можно отправлять сообщения для всех участников группы или только указанные члены группы, как показано в следующих примерах.

- **Все** подключенных клиентов в указанной группе. 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- Все подключенные клиенты в указанной группе **указанным клиентам, за исключением**, идентифицируемый идентификатор соединения. 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- Все подключенные клиенты в указанной группе **, кроме вызывающего клиента**. 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>Хранение в базе данных членства в группе

Следующие примеры показывают, как сохранять сведения о пользователей и групп в базе данных. Можно использовать любые технологии доступа к данным; Тем не менее в приведенном ниже примере показано, как для определения моделей с помощью Entity Framework. Эти модели сущности соответствуют таблиц базы данных и полей. Структуру данных может значительно изменяться в зависимости от требований приложения. Этот пример включает класс с именем `ConversationRoom` которой бы быть уникальными в приложение, которое позволяет пользователям присоединяться к беседы о различных задач, таких как спорта и садоводство. Этот пример также содержит класс для соединения. Класс подключения не являются необходимыми для отслеживания членство в группе, но часто является частью надежное решение для отслеживания пользователей.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

Затем в концентраторе, можно извлечь данные группы и пользователя из базы данных и вручную добавить пользователя в соответствующие группы. Пример не содержит код для отслеживания пользовательских соединений. В этом примере `await` ключевое слово не применяется перед `Groups.Add` потому, что сообщение не отправляется сразу же членами группы. Если вы хотите отправить сообщение всем членам группы сразу после добавления нового члена, можно применить `await` ключевое слово, чтобы убедиться, что асинхронная операция завершена.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Сохранение членства в группе в хранилище таблиц Azure

Использование табличного хранилища Azure для хранения информации, пользователей и групп похоже на использование базы данных. В следующем примере показано сущности таблицы, в котором хранится имя пользователя и имя группы.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

В концентраторе вы получите назначенных групп при подключении.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>Проверка членства в группе, при повторном подключении

По умолчанию SignalR автоматически повторно назначает пользователя в соответствующие группы при повторном подключении из к временному нарушению работы, например при удалении и заново установить соединение, время ожидания соединения. Сведения о группе пользователя передается в токене при повторном подключении, и этот маркер проверяется на сервере. Сведения о процессе проверки для повторное присоединение пользователей к группам, см. в разделе [повторное присоединение групп при повторном подключении](index.md).

В общем случае следует использовать поведение по умолчанию автоматически повторное присоединение что групп на повторное подключение. SignalR группы не следует рассматривать как механизм безопасности для ограничения доступа к конфиденциальным данным. Тем не менее если приложение необходимо тщательно проверить членство в группе пользователей, при повторном подключении, можно переопределить поведение по умолчанию. Изменение поведения по умолчанию можно добавить и нагрузку в базу данных так, как членство в группе пользователей, которые должны быть получены, для каждого повторного подключения, а не только в том случае, когда пользователь подключается.

Если вам необходимо проверить членство в группе на повторное подключение, создание нового модуля конвейер концентратора, который возвращает список всех назначенных групп, как показано ниже.

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

Затем добавьте этот модуль в конвейер концентратора, как показано ниже.

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]