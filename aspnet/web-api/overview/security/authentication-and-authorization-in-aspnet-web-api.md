---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Аутентификация и авторизация в ASP.NET Web API Документы Майкрософт
author: MikeWasson
description: Дает общий обзор проверки подлинности и авторизации в ASP.NET Web API.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675865"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Проверка подлинности и авторизация веб-API ASP.NET

[Майк Уоссон](https://github.com/MikeWasson)

Вы создали веб-API, но теперь вы хотите контролировать доступ к нему. В этой серии статей мы рассмотрим некоторые варианты защиты веб-API от неавторизованных пользователей. Эта серия будет охватывать как аутентификацию, так и авторизацию.

- *Аутентификация* — это знание личности пользователя. Например, Алиса входит в систему с именем пользователя и паролем, и сервер использует пароль для проверки подлинности Алисы.
- *Авторизация* решает, разрешено ли пользователю выполнять действие. Например, у Алисы есть разрешение на получение ресурса, но не на создание ресурса.

Первая статья серии дает общий обзор проверки подлинности и авторизации в ASP.NET Web API. Другие темы описывают общие сценарии аутентификации для Web API.

> [!NOTE]
> Спасибо людям, которые рассмотрели эту серию и предоставили ценную обратную связь: Рик Андерсон, Леви Бродерик, Барри Дорранс, Том Дайкстра, Hongmei Ge, Дэвид Мэтсон, Даниэль Рот, Тим Teebken.

## <a name="authentication"></a>Аутентификация

Web API предполагает, что аутентификация происходит в хосте. Для веб-хостинга хостом является IIS, который использует модули HTTP для проверки подлинности. Вы можете настроить проект, чтобы использовать любой из модулей аутентификации, встроенных в IIS или ASP.NET, или написать свой собственный модуль HTTP для выполнения пользовательской аутентификации.

Когда узла проверяет подлинность пользователя, он создает *основной*объект, который представляет собой объект [IPrincipal,](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) представляющий контекст безопасности, под которым работает код. Хост прикрепляет основной к текущему потоку, установив **Thread.CurrentPrincipal**. Основной элемент содержит связанный объект **Identity,** содержащий информацию о пользователе. Если пользователь проверен, **Identity.IsAuthenticated собственности** **возвращается верно**. Для анонимных запросов, **IsAuthenticated** возвращает **ложные**. Для получения дополнительной информации [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx)о принципах см.

### <a name="http-message-handlers-for-authentication"></a>ОБработчики сообщений HTTP для аутентификации

Вместо использования хоста для проверки подлинности можно поместить логику проверки подлинности в [обработчик сообщений HTTP.](../advanced/http-message-handlers.md) В этом случае обработчик сообщений изучает запрос HTTP и устанавливает принцип.

Когда следует использовать обработчики сообщений для проверки подлинности? Вот некоторые компромиссы:

- Модуль HTTP просматривает все запросы, которые проходят через конвейер ASP.NET. Обработчик сообщений видит только запросы, которые направляются в Web API.
- Можно настроить обработчики сообщений на маршрут, что позволяет применить схему проверки подлинности к определенному маршруту.
- Модули HTTP специфичны для IIS. Обработчики сообщений являются хост-агностиками, поэтому их можно использовать как с веб-хостингом, так и с автохостингом.
- Модули HTTP участвуют в регистрации, аудите ИИС и так далее.
- Модули HTTP работают ранее в конвейере. Если вы обрабатываете проверку подлинности в обработчике сообщений, принцип не устанавливается до тех пор, пока обработчик не заработает. Кроме того, основной возвращается к предыдущему принципу, когда ответ покидает обработчик сообщений.

Как правило, если вам не нужно поддерживать самостоятельное размещение, модуль HTTP является лучшим вариантом. Если вам необходимо поддерживать самостоятельное размещение, подумайте об обработчике сообщений.

### <a name="setting-the-principal"></a>Установка директора

Если приложение выполняет любую пользовательскую логику проверки подлинности, необходимо установить принцип в двух местах:

- **Thread.CurrentPrincipal**. Это свойство является стандартным способом установить принцип потока в .NET.
- **HttpContext.Current.User**. Это свойство характерно для ASP.NET.

Следующий код показывает, как установить принцип:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Для веб-хостинга, вы должны установить основной в обоих местах; в противном случае контекст безопасности может стать непоследовательным. Для самостоятельного хостинга, однако, **HttpContext.Current** является недействительным. Чтобы убедиться, что ваш код является хост-агностиком, поэтому проверьте наличие нуля перед назначением **httpContext.Current**, как показано на рисунке.

## <a name="authorization"></a>Авторизация

Авторизация происходит позже в конвейере, ближе к контроллеру. Это позволяет делать более детальный выбор, когда вы предоставляете доступ к ресурсам.

- *Фильтры авторизации* запускаться до действия контроллера. Если запрос не авторизован, фильтр возвращает ответ на ошибку, и действие не вызывается.
- В рамках действия контроллера вы можете получить текущий принцип из свойства **ApiController.User.** Например, можно отфильтровать список ресурсов на основе имени пользователя, вернув только те ресурсы, которые принадлежат этому пользователю.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>Использование атрибута «Авторизуализацию»

Web API предоставляет встроенный фильтр авторизации, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx). Этот фильтр проверяет, проверяется ли подлинность пользователя. В противном случае он возвращает код статуса HTTP 401 (несанкционированный), не ссылаясь на действие.

Вы можете применять фильтр глобально, на уровне контроллера или на уровне отдельных действий.

**Глобально:** Чтобы ограничить доступ для каждого контроллера Web API, добавьте фильтр **AuthorizeAttribute** в глобальный список фильтров:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Контроллер**: Чтобы ограничить доступ для определенного контроллера, добавьте фильтр в качестве атрибута для контроллера:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Действие**: Чтобы ограничить доступ для определенных действий, добавьте атрибут в метод действия:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Кроме того, можно ограничить контроллер, а затем разрешить анонимный `[AllowAnonymous]` доступ к определенным действиям, используя атрибут. В следующем примере `Post` метод ограничен, `Get` но метод позволяет анонимный доступ.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

В предыдущих примерах фильтр позволяет любому подлинному пользователю получить доступ к ограниченным методам; только анонимные пользователи не достатомы. Вы также можете ограничить доступ к определенным пользователям или пользователям в определенных ролях:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Фильтр **AuthorizeAttribute** для контроллеров Web API находится в пространстве имен **System.Web.Http.** Аналогичный фильтр для контроллеров MVC существует в пространстве имен **System.Web.Mvc,** который не совместим с контроллерами Web API.

### <a name="custom-authorization-filters"></a>Пользовательские фильтры авторизации

Чтобы написать пользовательский фильтр авторизации, вытекают из одного из этих типов:

- **АвторизутАтрибут**. Расширьте этот класс для выполнения логики авторизации на основе текущего пользователя и ролей пользователя.
- **АвторизацияФильтрАтрибут**. Расширьте этот класс для выполнения синхронной логики авторизации, которая не обязательно основана на текущем пользователе или роли.
- **IАвторизацияФильтр**. Реализация этого интерфейса для выполнения асинхронной логики авторизации; например, если логика авторизации делает асинхронные ввод/во-х или сетевые вызовы. (Если логика авторизации связана с процессором, проще получить из **AuthorizationFilterAttribute,** потому что тогда вам не нужно писать асинхронный метод.)

Следующая диаграмма показывает иерархию классов для класса **AuthorizeAttribute.**

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Авторизация внутри действия контроллера

В некоторых случаях можно разрешить продолжение запроса, но изменить поведение на основе основного принципала. Например, возвращается информация может изменяться в зависимости от роли пользователя. В рамках метода контроллера можно получить текущий принцип из свойства **ApiController.User.**

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
