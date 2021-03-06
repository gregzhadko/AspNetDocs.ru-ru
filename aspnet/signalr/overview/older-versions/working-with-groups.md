---
uid: signalr/overview/older-versions/working-with-groups
title: Работа с группами в SignalR 1. x | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как сохранять сведения о членстве в группах с помощью API концентратора.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467898"
---
# <a name="working-with-groups-in-signalr-1x"></a>Работа с группами в SignalR 1.x

[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом разделе описывается добавление пользователей в группы и сохранение сведений о членстве в группах.

## <a name="overview"></a>Обзор

Группы в SignalR предоставляют метод для вещания сообщений в указанные подмножества подключенных клиентов. Группа может иметь любое количество клиентов, а клиент может быть членом любого числа групп. Вам не нужно явно создавать группы. По сути, группа создается автоматически при первом указании имени в вызове Groups. Add и удаляется при удалении последнего подключения из членства в нем. Общие сведения об использовании групп см. в разделе [Управление членством в группах из класса Hub](index.md) руководства по API концентраторов.

Отсутствует API для получения списка членства в группе или списка групп. SignalR отправляет сообщения клиентам и группам, основанным на модели публикации и подтипа, а сервер не поддерживает списки групп или членства в группах. Это обеспечивает максимальную масштабируемость, так как при добавлении узла в веб-ферму любое состояние, которое обслуживает SignalR, должно быть распространено на новый узел.

При добавлении пользователя в группу с помощью метода `Groups.Add` пользователь получает сообщения, направленные в эту группу, на время текущего соединения, но членство пользователя в этой группе не сохраняется за пределами текущего соединения. Если вы хотите постоянно сохранять сведения о группах и членстве в группах, эти данные необходимо хранить в репозитории, например в базе данных или в хранилище таблиц Azure. Затем каждый раз, когда пользователь подключается к вашему приложению, вы получаете из репозитория, в который входит пользователь, и вручную добавляете этого пользователя в эти группы.

При повторном подключении после временного перерыва пользователь автоматически повторно присоединяется к ранее назначенным группам. Автоматическое пересоединение группы применяется только при повторном подключении, а не при установке нового соединения. Маркер с цифровой подписью передается из клиента, содержащего список ранее назначенных групп. Если необходимо проверить, относится ли пользователь к запрошенным группам, можно переопределить поведение по умолчанию.

Этот раздел включает следующие подразделы:

- [Добавление и удаление пользователей](#add)
- [Вызов членов группы](#call)
- [Хранение членства в группе в базе данных](#storedatabase)
- [Хранение членства в группах в хранилище таблиц Azure](#storeazuretable)
- [Проверка членства в группе при повторном подключении](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>Добавление и удаление пользователей

Чтобы добавить или удалить пользователей из группы, вызовите методы [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) или [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) и передайте в качестве параметров идентификатор подключения пользователя и имя группы. При завершении соединения не требуется вручную удалять пользователя из группы.

В следующем примере показаны методы `Groups.Add` и `Groups.Remove`, используемые в методах концентратора.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

Методы `Groups.Add` и `Groups.Remove` выполняются асинхронно.

Если вы хотите добавить клиент в группу и сразу же отправить сообщение клиенту с помощью группы, необходимо убедиться в том, что метод Groups. Add завершается первым. В следующих примерах кода показано, как это сделать, используя код, который работает в .NET 4,5, а другой — с помощью кода, который работает в .NET 4.

#### <a name="asynchronous-net-45-example"></a>Пример асинхронного .NET 4,5

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>Пример асинхронного .NET 4

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

В общем случае не следует включать `await` при вызове метода `Groups.Remove`, так как идентификатор подключения, который вы пытаетесь удалить, может больше не быть доступен. В этом случае `TaskCanceledException` создается после истечения времени ожидания запроса. Если приложение должно гарантировать, что пользователь был удален из группы перед отправкой сообщения в группу, можно добавить `await` перед группами. Удалите, а затем перехватите исключение `TaskCanceledException`, которое может быть выдано.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>Вызов членов группы

Можно отправить сообщения всем членам группы или только указанным членам группы, как показано в следующих примерах.

- **Все** подключенные клиенты в указанной группе. 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- Все подключенные клиенты в указанной группе, **за исключением указанных клиентов**, идентифицируемые по идентификатору соединения. 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- Все подключенные клиенты в указанной группе, **Кроме вызывающего клиента**. 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>Хранение членства в группе в базе данных

В следующих примерах показано, как хранить сведения о группах и пользователях в базе данных. Можно использовать любую технологию доступа к данным. Однако в приведенном ниже примере показано, как определить модели с помощью Entity Framework. Эти модели сущностей соответствуют таблицам и полям базы данных. Структура данных может значительно варьироваться в зависимости от требований приложения. Этот пример включает класс с именем `ConversationRoom`, который будет уникальным для приложения, позволяющего пользователям присоединяться к беседам по различным темам, таким как спорт или садом. Этот пример также включает класс для соединений. Класс Connection не является абсолютно необходимым для отслеживания членства в группах, но часто является частью надежного решения для отслеживания пользователей.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

Затем в центре можно получить сведения о группах и пользователях из базы данных и вручную добавить пользователя в соответствующие группы. В примере не содержится код для отслеживания пользовательских соединений. В этом примере ключевое слово `await` не применяется перед `Groups.Add`, так как сообщение не отправляется сразу членам группы. Если вы хотите отправить сообщение всем членам группы сразу после добавления нового члена, необходимо применить ключевое слово `await`, чтобы убедиться, что асинхронная операция завершена.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Хранение членства в группах в хранилище таблиц Azure

Использование хранилища таблиц Azure для хранения данных группы и пользователя аналогично использованию базы данных. В следующем примере показана сущность таблицы, в которой хранится имя пользователя и имя группы.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

В центре вы получаете назначенные группы при подключении пользователя.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>Проверка членства в группе при повторном подключении

По умолчанию SignalR автоматически переназначит пользователя соответствующим группам при повторном подключении из временного перерыва, например при удалении и повторном установлении соединения до истечения времени ожидания соединения. Сведения о группе пользователя передаются в токене при повторном подключении, и этот маркер проверяется на сервере. Сведения о процедуре проверки повторного присоединения пользователей к группам см. в разделе [повторное присоединение групп при восстановлении](index.md)соединения.

В общем случае следует использовать поведение по умолчанию автоматического повторного присоединения групп при восстановлении соединения. Группы SignalR не предназначены для обеспечения безопасности при ограничении доступа к конфиденциальным данным. Однако если приложение должно проверить членство пользователя в группе при повторном подключении, можно переопределить поведение по умолчанию. Изменение поведения по умолчанию может добавить нагрузку в базу данных, так как членство пользователя в группе необходимо получить для каждого повторного подключения, а не только при подключении пользователя.

Если необходимо проверить членство в группе при повторном подключении, создайте новый модуль конвейера концентратора, который возвращает список назначенных групп, как показано ниже.

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

Затем добавьте этот модуль в конвейер концентратора, как показано ниже.

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
