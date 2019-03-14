---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Проверка подлинности и авторизация в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: Предоставляет общие сведения о проверки подлинности и авторизации в веб-API ASP.NET.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a78606a74b2149e68e3b01f4fe204f4a13edf4b5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039101"
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a>Проверка подлинности и авторизация в веб-API ASP.NET
====================
по [Майк Уоссон](https://github.com/MikeWasson)

Вы создали веб-API, но теперь вы хотите управлять доступом к ней. В этой серии статей мы рассмотрим некоторые возможности защиты веб-API от неавторизованных пользователей. В этой серии рассматривается проверка подлинности и авторизация.

- *Проверка подлинности* знание идентификатора пользователя. Например Алиса входе в систему с ее имя пользователя и пароль, а сервер использует пароль для проверки подлинности Алиса.
- *Авторизация* -определить, разрешено ли пользователю для выполнения действия. Например Алиса имеет разрешение на получение ресурса, но не создавать ресурс.

Первая статья в серии приводится общий обзор проверки подлинности и авторизации в веб-API ASP.NET. Другие разделы описывают распространенные сценарии проверки подлинности для веб-API.

> [!NOTE]
> Благодаря рецензентами этой серии и предоставляли ценные отзывы. Рик Андерсон, Levi Broderick, Barry Dorrans, том Дайкстра, Hongmei Ge, Дэвид Matson, Дэниэл рот, Тим Teebken.


## <a name="authentication"></a>Проверка подлинности

Веб-API предполагается, что произойдет, что проверка подлинности на узле. Для веб размещения, узел представляет IIS, который использует HTTP-модули для проверки подлинности. Можно настроить проект для использования этих модулей проверки подлинности, встроенную в IIS или ASP.NET, или написать собственный модуль HTTP для выполнения пользовательской проверки подлинности.

Когда узел проверяет подлинность пользователя, он создает *участника*, который является [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) объект, представляющий контекст безопасности, в котором работает код. Узел присоединяет участника к текущему потоку, задав **Thread.CurrentPrincipal**. Участник содержит связанный **удостоверений** объект, содержащий сведения о пользователе. Если пользователь прошел проверку подлинности, **Identity.IsAuthenticated** возвращает **true**. Для анонимных запросов **IsAuthenticated** возвращает **false**. Дополнительные сведения об участниках см. в разделе [безопасности на основе ролей](https://msdn.microsoft.com/library/shz8h065.aspx).

### <a name="http-message-handlers-for-authentication"></a>Обработчики сообщений HTTP для проверки подлинности

Вместо использования узла для проверки подлинности, можно поместить логику проверки подлинности в [обработчик сообщений HTTP](../advanced/http-message-handlers.md). В этом случае обработчик сообщений проверяет HTTP-запроса и задает участника.

Когда следует использовать обработчики сообщений для проверки подлинности? Ниже приведены некоторые компромиссы.

- Модуль HTTP видит все запросы, которые проходят через конвейер ASP.NET. Обработчик сообщений видит только те запросы, которые направляются в веб-API.
- Можно задать обработчики сообщений для каждого маршрута, который позволяет применить схему проверки подлинности для определенного маршрута.
- HTTP-модули характерны для IIS. Обработчики сообщений являются независимой от размещения, поэтому они могут использоваться с веб размещения и размещения на собственном сервере.
- HTTP-модули участвовать в IIS ведение журнала аудита и т. д.
- HTTP-модули запустите ранее в конвейере. Если вы обрабатываете проверки подлинности в обработчик сообщений, субъект не получить значение, пока не будет запущен обработчик. Кроме того участника возвращается к предыдущего участника, когда ответ покидает обработчик сообщений.

Как правило если не требуется для поддержки размещения на собственном сервере, модуль HTTP является лучшим вариантом. Если необходима поддержка размещения на собственном сервере, рассмотрите возможность обработчик сообщений.

### <a name="setting-the-principal"></a>Задание участника

Если приложение выполняет логику настраиваемой проверки подлинности, необходимо задать участника в двух местах:

- **Thread.CurrentPrincipal**. Это свойство является стандартным способом для задания участника потока в .NET.
- **HttpContext.Current.User**. Это свойство относится только к ASP.NET.

Ниже показано, как для задания участника:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Для веб размещения, необходимо задать участника в обоих местах; в противном случае контекст безопасности может стать несогласованной. Для размещения на собственном сервере, однако **HttpContext.Current** имеет значение null. Чтобы ваш код является независимой от размещения, таким образом, проверка значений null перед назначением **HttpContext.Current**, как показано.

## <a name="authorization"></a>Авторизация

Авторизация происходит позже в конвейере, ближе к контроллеру. Который позволяет вам выбрать более детализированные параметры, при предоставлении доступа к ресурсам.

- *Фильтры авторизации* запуска перед выполнением действия контроллера. Если запрос не авторизован, фильтр выдает сообщение об ошибке, и действие не вызывается.
- Действия контроллера, можно получить текущий субъект из **ApiController.User** свойство. Например может отфильтровать список ресурсов, на основе имени пользователя, возвращая только те ресурсы, принадлежащие этому пользователю.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>С помощью [авторизовать] атрибут

Веб-API предоставляет фильтр встроенной авторизации, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx). Этот фильтр проверяет, является ли пользователь проверку подлинности. В противном случае он возвращает код состояния HTTP 401 (не санкционировано) без вызова действия.

Вы можете применить фильтр глобально, на уровне контроллера или на уровне отдельных действий.

**Глобально**: Чтобы ограничить доступ для каждого контроллера веб-API, добавьте **AuthorizeAttribute** фильтра в список глобальных фильтров:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Контроллер**: Чтобы ограничить доступ для определенного контроллера, добавьте фильтр как атрибут контроллер:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Действие**: Чтобы ограничить доступ для определенных действий, добавьте атрибут в метод действия.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Кроме того, можно ограничить контроллер, а затем разрешить анонимный доступ к определенным действиям с помощью `[AllowAnonymous]` атрибута. В следующем примере `Post` метод ограничен, но `Get` метод разрешает анонимный доступ.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

В предыдущих примерах фильтр позволяет любой прошедший проверку пользователь для доступа к ограниченных методов; только анонимные пользователи хранятся. Можно также ограничить доступ к определенным пользователям или пользователям с определенными ролями:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> **AuthorizeAttribute** фильтр для контроллеров веб-API находится в **System.Web.Http** пространства имен. Аналогичный фильтр для контроллеров MVC в **System.Web.Mvc** пространство имен, которое не совместим с контроллеров веб-API.


### <a name="custom-authorization-filters"></a>Пользовательская авторизация фильтры

Чтобы написать пользовательский фильтр авторизации, являются производными от одного из следующих типов:

- **AuthorizeAttribute**. Расширьте этот класс для реализации логики авторизации на основе текущего пользователя и роли пользователя.
- **AuthorizationFilterAttribute**. Расширьте этот класс для выполнения синхронного авторизации логику, которая не зависит от обязательно текущего пользователя или роли.
- **IAuthorizationFilter**. Реализация этого интерфейса позволяет выполнить логику асинхронных авторизации; Например, если логику авторизации выполняет асинхронные вызовы ввода/вывода или сети. (Если логику авторизации ЦП, проще являются производными от **AuthorizationFilterAttribute**, так как нужно писать асинхронный метод.)

В примере ниже показан иерархию классов для **AuthorizeAttribute** класса.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Авторизация внутри действия контроллера

В некоторых случаях может позволить запрос продолжить, но изменять поведение на основе субъекта. Например сведения, что вы вернетесь может измениться в зависимости от роли пользователя. Внутри метода контроллера, можно получить текущий субъект из **ApiController.User** свойство.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]