---
uid: signalr/overview/security/hub-authorization
title: Проверка подлинности и авторизация для концентраторов SignalR | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается, как ограничить доступ пользователей или ролей к методам концентратора. Версии программного обеспечения, используемые в этом разделе Visual Studio 2013 .NET 4,5 SignalR...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467514"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a>Проверка подлинности и авторизация для концентраторов SignalR

[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом разделе описывается, как ограничить доступ пользователей или ролей к методам концентратора.
>
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемые в этом разделе
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR версии 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Предыдущие версии этого раздела
>
> Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Обзор

Этот раздел состоит из следующих подразделов.

- [Авторизовать атрибут](#authorizeattribute)
- [Требовать проверку подлинности для всех концентраторов](#requireauth)
- [Настроенная авторизация](#custom)
- [Передача сведений о проверке подлинности клиентам](#passauth)
- [Параметры проверки подлинности для клиентов .NET](#authoptions)

    - [Файл cookie с проверкой подлинности на формах](#cookie)
    - [Проверка подлинности Windows.](#windows)
    - [Заголовок подключения](#header)
    - [Сертификат](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>Авторизовать атрибут

SignalR предоставляет атрибут [авторизации](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) , чтобы указать, какие пользователи или роли имеют доступ к концентратору или методу. Этот атрибут находится в пространстве имен `Microsoft.AspNet.SignalR`. Атрибут `Authorize` применяется к концентратору или определенным методам в концентраторе. При применении атрибута `Authorize` к классу Hub указанные требования к авторизации применяются ко всем методам в концентраторе. В этом разделе приводятся примеры различных типов требований к авторизации, которые можно применять. Без атрибута `Authorize` подключенный клиент может получить доступ к любому открытому методу в концентраторе.

Если в веб-приложении определена роль с именем "admin", можно указать, что только пользователи с этой ролью могут получить доступ к концентратору со следующим кодом.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

Также можно указать, что центр содержит один метод, доступный всем пользователям, и второй метод, который доступен только для пользователей, прошедших проверку подлинности, как показано ниже.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

В следующих примерах разрешаться различные сценарии авторизации:

- `[Authorize]` — только пользователи, прошедшие проверку подлинности
- `[Authorize(Roles = "Admin,Manager")]` — только пользователи, прошедшие проверку подлинности в указанных ролях
- `[Authorize(Users = "user1,user2")]` — только пользователи, прошедшие проверку подлинности с указанными именами пользователей
- `[Authorize(RequireOutgoing=false)]` — только пользователи, прошедшие проверку подлинности, могут вызывать концентратор, но вызовы от сервера к клиентам не ограничиваются авторизацией, например, когда только определенные пользователи могут отправлять сообщения, но все остальные могут получать это сообщение. Свойство Рекуиреаутгоинг может применяться только ко всему концентратору, а не к отдельным методам в концентраторе. Если для Рекуиреаутгоинг не задано значение false, с сервера вызываются только пользователи, соответствующие требованию к авторизации.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>Требовать проверку подлинности для всех концентраторов

Можно потребовать проверку подлинности для всех концентраторов и методов концентратора в приложении, вызвав метод [рекуиреаусентикатион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) при запуске приложения. Этот метод можно использовать, если у вас есть несколько концентраторов и необходимо обеспечить требование проверки подлинности для всех из них. С помощью этого метода нельзя указать требования для роли, пользователя или исходящей авторизации. Можно указать, чтобы доступ к методам концентратора был разрешен только пользователям, прошедшим проверку подлинности. Однако вы по-прежнему можете применить атрибут авторизации к концентраторам или методам, чтобы указать дополнительные требования. Все требования, указанные в атрибуте, добавляются к базовому требованию проверки подлинности.

В следующем примере показан файл запуска, который разрешает всем методам концентратора проходить проверку подлинности пользователей.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

При вызове метода `RequireAuthentication()` после обработки запроса SignalR SignalR выдаст исключение `InvalidOperationException`. SignalR создает это исключение, так как вы не можете добавить модуль в Хубпипелине после вызова конвейера. В предыдущем примере показан вызов метода `RequireAuthentication` в методе `Configuration`, который выполняется один раз перед обработкой первого запроса.

<a id="custom"></a>

## <a name="customized-authorization"></a>Настроенная авторизация

Если необходимо настроить авторизацию, можно создать класс, производный от `AuthorizeAttribute` и переопределить метод [усераусоризед](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) . Для каждого запроса SignalR вызывает этот метод, чтобы определить, имеет ли пользователь разрешение на завершение запроса. В переопределенном методе вы предоставляете необходимую логику для вашего сценария авторизации. В следующем примере показано, как обеспечить авторизацию с помощью удостоверения на основе утверждений.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>Передача сведений о проверке подлинности клиентам

Может потребоваться использовать данные проверки подлинности в коде, который выполняется на клиенте. Необходимо передать необходимые сведения при вызове методов на клиенте. Например, метод приложения разговора может передавать в качестве параметра имя пользователя, публикующий сообщение, как показано ниже.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

Или можно создать объект для представления сведений о проверке подлинности и передать этот объект в качестве параметра, как показано ниже.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

Никогда не следует передавать идентификаторы подключения одного клиента другим клиентам, так как пользователь-злоумышленник может использовать его для имитации запроса от этого клиента.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>Параметры проверки подлинности для клиентов .NET

Если у вас есть клиент .NET, например консольное приложение, взаимодействующее с концентратором, который ограничен пользователями, прошедшими проверку подлинности, можно передать учетные данные для проверки подлинности в файл cookie, заголовок соединения или сертификат. В примерах этого раздела показано, как использовать различные методы для проверки подлинности пользователя. Они не являются полнофункциональными приложениями SignalR. Дополнительные сведения о клиентах .NET с помощью SignalR см. в статье [Путеводитель по API концентраторов — клиент .NET](../guide-to-the-api/hubs-api-guide-net-client.md).

<a id="cookie"></a>

### <a name="cookie"></a>Куки-файл

Когда клиент .NET взаимодействует с концентратором, использующим проверку подлинности ASP.NET Forms, необходимо вручную задать файл cookie проверки подлинности для соединения. Файл cookie добавляется в свойство `CookieContainer` объекта [хубконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) . В следующем примере показано консольное приложение, которое получает файл cookie проверки подлинности с веб-страницы и добавляет этот файл cookie к соединению.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

Консольное приложение отправляет учетные данные в <strong>www.contoso.com/RemoteLogin</strong> , которые могут ссылаться на пустую страницу, содержащую следующий файл кода программной части.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Проверка подлинности Windows

При использовании проверки подлинности Windows можно передать учетные данные текущего пользователя с помощью свойства [дефаулткредентиалс](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) . Вы задаете учетные данные для соединения со значением Дефаулткредентиалс.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>Заголовок подключения

Если приложение не использует файлы cookie, можно передать сведения о пользователе в заголовке соединения. Например, можно передать маркер в заголовок Connection.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

Затем в центре можно проверить маркер пользователя.

<a id="certificate"></a>

### <a name="certificate"></a>Сертификат

Сертификат клиента можно передать для проверки пользователя. Сертификат добавляется при создании соединения. В следующем примере показано, как добавить сертификат клиента в соединение. в нем не отображается полное консольное приложение. Он использует класс [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , который предоставляет несколько различных способов создания сертификата.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
