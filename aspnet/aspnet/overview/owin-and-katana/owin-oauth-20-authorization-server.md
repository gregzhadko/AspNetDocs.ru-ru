---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: Сервер авторизации OWIN OAuth 2.0 Документы Майкрософт
author: hongyes
description: Этот учебник поможет вам о том, как реализовать OAuth 2.0 Авторизация Сервер с помощью OWIN OAuth промежуточного. Это продвинутый учебник, который только outlin ...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540424"
---
<a name="owin-oauth-20-authorization-server"></a>Сервер авторизации OAuth 2.0 OWIN
====================
[Хонъе Сун](https://github.com/hongyes) и [Прабурадж Тиагараджан](https://github.com/Praburaj)

> Этот учебник поможет вам о том, как реализовать OAuth 2.0 Авторизация Сервер с помощью OWIN OAuth промежуточного. Это продвинутый учебник, который только излагает шаги для создания СЕРВЕРа авторизации OWIN OAuth 2.0. Это не шаг за шагом учебник. [Скачать пример кода](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).
>
> > [!NOTE]
> > Этот план не должен использоваться для создания безопасного производственного приложения. Этот учебник предназначен для предоставления только наброски о том, как реализовать OAuth 2.0 Авторизация Сервер с помощью OWIN OAuth промежуточного.
>
>
> ## <a name="software-versions"></a>Версии программного обеспечения
>
> | **Показано в учебнике** | **Также работает с** |
> | --- | --- |
> | Windows 8.1 | Windows 8, Windows 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [Визуальная студия 2013 Экспресс для рабочего стола](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). Visual Studio 2012 с последним обновлением должен работать, но учебник не был протестирован с ним, и некоторые выбор меню и диалоговые коробки отличаются. |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Если у вас есть вопросы, которые не имеют прямого отношения к учебнику, вы можете разместить их на [Katana project на GitHub](https://github.com/aspnet/AspNetKatana/). Для вопросов и комментариев, касающихся самого учебника, смотрите раздел комментариев в нижней части страницы.


[Платформа OAuth 2.0](http://tools.ietf.org/html/rfc6749) позволяет стороннему приложению получить ограниченный доступ к службе HTTP. Вместо того, чтобы использовать учетные данные владельца ресурса для доступа к защищенному ресурсу, клиент получает токен доступа (который является строкой, обозначающей определенный объем, срок службы и другие атрибуты доступа). Токены доступа выдаются сторонним клиентам сервером авторизации с одобрения владельца ресурса.

Этот учебник будет охватывать:

- Как создать сервер авторизации для поддержки четырех типов грантов авторизации и обновления токенов:
    - Разрешение код гранта
    - Неявный Грант
    - Грант владельца паролей ресурса
    - Грант на учетные данные клиентов
- Создание сервера ресурсов, защищенного токеном доступа.
- Создание клиентов OAuth 2.0.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Предварительные требования

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) или бесплатная [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), как указано в **Software Versions** в верхней части страницы.
- Знакомство с OWIN. Смотрите [Начало работы с проектом Katana](https://msdn.microsoft.com/magazine/dn451439.aspx) и [что нового в OWIN и Katana](index.md).
- Знакомство с терминологией [OAuth,](http://tools.ietf.org/html/rfc6749) включая [роли,](http://tools.ietf.org/html/rfc6749#section-1.1) [Протоколный поток](http://tools.ietf.org/html/rfc6749#section-1.2)и [Грант авторизации.](http://tools.ietf.org/html/rfc6749#section-1.3) [OAuth 2.0 введение](http://tools.ietf.org/html/rfc6749#section-1) обеспечивает хорошее введение.

## <a name="create-an-authorization-server"></a>Создание сервера авторизации

В этом уроке мы будем примерно наброски, как использовать [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) и ASP.NET MVC для создания сервера авторизации. Мы надеемся, что в скором времени обеспечить загрузку для завершенного образца, так как этот учебник не включает в себя каждый шаг. Во-первых, создайте пустое веб-приложение под названием *AuthorizationServer* и установите следующие пакеты:

- Microsoft.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- Microsoft.Owin.Security.Google (или любой другой социальный пакет входа, таких как Microsoft.Owin.Security.Facebook)

Добавьте [класс стартапа OWIN](owin-startup-class-detection.md) под корневую папку проекта под названием *Startup.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

Создайте папку *«Старт приложения».\_* Выберите папку *App\_Start* и используйте Shift-Alt-A, чтобы добавить загруженную версию файла *AuthorizationServer-App\_Start-Start.Auth.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

Приведенный выше код позволяет приложения/внешнего знака в файлах cookie и аутентификации Google, которые используются самим сервером авторизации для управления учетными записями.

Метод `UseOAuthAuthorizationServer` расширения заключается в настройке сервера авторизации. Параметры настройки:

- `AuthorizeEndpointPath`: Путь запроса, по которому клиентские приложения перенаправляют агента пользователя, чтобы получить согласие пользователей на выпуск токена или кода. Она должна начинаться с ведущих черту, например, ".`/Authorize`
- `TokenEndpointPath`: Клиентские приложения пути запроса непосредственно общаются для получения токена доступа. Она должна начинаться с ведущей черты, как "/Токен". Если клиенту выдается [секрет клиента,\_](http://tools.ietf.org/html/rfc6749#appendix-A.2)он должен быть предоставлен в этой точке.
- `ApplicationCanDisplayErrors`: Установить, `true` если веб-приложение хочет создать пользовательскую страницу `/Authorize` ошибки для клиента проверки ошибок на конечную точку. Это необходимо только в тех случаях, когда браузер не перенаправляется обратно `client_id` `redirect_uri` в клиентское приложение, например, когда или неправильно. Конечная `/Authorize` точка должна ожидать, чтобы увидеть "Oauth. Ошибка", "Оут. ОшибкаОписание" и "Оут. Свойства ErrorUri добавляются в среду OWIN.

    > [!NOTE]
    > Если это не так, сервер авторизации вернет страницу ошибки по умолчанию с деталями ошибки.
- `AllowInsecureHttp`: Верно, чтобы разрешить авторизовать и маркерные запросы, `redirect_uri` чтобы прибыть на адреса HTTP URI, и разрешить входящие параметры авторизации запроса, чтобы иметь адреса HTTP URI.

    > [!WARNING]
    > Безопасность - Это только для развития.
- `Provider`: Объект, предоставляемый приложением для обработки событий, поднятых промежуточное программное обеспечение сервера авторизации. Приложение может полностью реализовать интерфейс, или оно `OAuthAuthorizationServerProvider` может создать экземпляр и назначить делегатов, необходимых для потоков OAuth, которые поддерживает этот сервер.
- `AuthorizationCodeProvider`: Производит одноразовый код авторизации для возврата в клиентское приложение. Для обеспечения безопасности сервера **MUST** OAuth приложение `AuthorizationCodeProvider` должно предоставить экземпляр, в котором токен, произведенный `OnCreate/OnCreateAsync` событием, считается действительным только для одного `OnReceive/OnReceiveAsync`звонка.
- `RefreshTokenProvider`: Производит маркер обновления, который может быть использован для создания нового токена доступа при необходимости. Если сервер авторизации не вернет токены `/Token` обновления из конечных точек.

## <a name="account-management"></a>Управление учетными записями

OAuth не волнует, где и как вы управляете информацией учетной записи пользователя. Это [ASP.NET идентичность,](../../../identity/index.md) которая несет ответственность за это. В этом учебнике мы упростим код управления учетной записью и просто убедимся, что пользователь может войти в систему с помощью промежуточного посуды OWIN cookie. Вот упрощенный пример кода `AccountController`для:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`используется для проверки клиента с его зарегистрированным URL-адресом. `ValidateClientAuthentication`проверяет основную схему заголовка и формы тела, чтобы получить полномочия клиента.

Страница входа отображается ниже:

![](owin-oauth-20-authorization-server/_static/image1.png)

Просмотрите раздел OAUth 2 [Авторизация](http://tools.ietf.org/html/rfc6749#section-4.1) IETth 2 Авторизация Код Грант разделе сейчас.

**Поставщиком** (в таблице ниже) является [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx). Поставщик, который имеет `OAuthAuthorizationServerProvider`тип, который содержит все события сервера OAuth.

| Шаги потока из раздела Грант кода авторизации | Пример загрузки выполняет следующие шаги с: |
| --- | --- |
|  |  |
| (A) Клиент инициирует поток, направляя агента пользователя-пользователя ресурса в конечную точку авторизации. Клиент включает в себя идентификатор клиента, запрашиваемую область, локальное состояние и перенаправление URI, на который сервер авторизации отправит агента пользователя обратно после предоставления доступа (или отказа). | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Сервер авторизации проверяет подлинность владельца ресурса (через пользователя-агента) и устанавливает, предоставляет ли владелец ресурса или отказывает клиенту в запросе на доступ. | **Если пользователь предоставляет доступ&gt; &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Предполагая, что владелец ресурса предоставляет доступ, сервер авторизации перенаправляет агента пользователя обратно клиенту, используя перенаправление URI, предоставленное ранее (в запросе или во время регистрации клиента). ... |  |
|  |  |
| (D) Клиент запрашивает токен доступа из токенной точки сервера авторизации, включив код авторизации, полученный на предыдущем этапе. При совершении запроса клиент проверяет подлинность с помощью сервера авторизации. Клиент включает в себя перенаправление URI, используемое для получения кода авторизации для проверки. | Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |

Ниже показана `AuthorizationCodeProvider.CreateAsync` `ReceiveAsync` примерная реализация для создания и проверки кода авторизации и контроля.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

Приведенный выше код использует одновременный словарь в памяти для хранения кода и идентификационного билета и восстановления идентификации после получения кода. В реальном приложении он будет заменен постоянным хранилищем данных. Конечная точка авторизации предназначена для владельца ресурса предоставить доступ клиенту. Как правило, он нуждается в пользовательском интерфейсе, чтобы позволить пользователю нажать кнопку и подтвердить грант. Промежуточное программное обеспечение OWIN OAuth позволяет коду приложения обрабатывать конечную точку авторизации. В нашем примере приложения мы используем `OAuthController` контроллер MVC, называемый для его обработки. Вот пример реализации:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

Действие `Authorize` сначала проверяет, вошел ли пользователь на сервер авторизации. В противном случае промежуточное программное обеспечение для проверки подлинности вызова вызова проверяется с помощью файла cookie и перенаправляет его на страницу входа. (См. выделенный код выше.) Если пользователь вошел в систему, он будет отображать представление Authorize, как показано ниже:

![](owin-oauth-20-authorization-server/_static/image2.png)

Если выбрана кнопка **Гранта,** `Authorize` действие создаст новую идентификацию «Bearer» и восстанет с ней. Это вызовет сервер авторизации для генерации маркера носителя и отправки его обратно клиенту с полезной нагрузкой JSON.

### <a name="implicit-grant"></a>Неявный Грант

Обратитесь к разделу OAuth [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) 2 IETF.

 [Неявный поток гранта,](http://tools.ietf.org/html/rfc6749#section-4.2) показанный на рисунке 4, — это поток и отображение, за которым следует промежуточное программное обеспечение OWIN OAuth.

| Шаги потока из раздела Неявного Гранта | Пример загрузки выполняет следующие шаги с: |
| --- | --- |
|  |  |
| (A) Клиент инициирует поток, направляя агента пользователя-пользователя ресурса в конечную точку авторизации. Клиент включает в себя идентификатор клиента, запрашиваемую область, локальное состояние и перенаправление URI, на который сервер авторизации отправит агента пользователя обратно после предоставления доступа (или отказа). | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Сервер авторизации проверяет подлинность владельца ресурса (через пользователя-агента) и устанавливает, предоставляет ли владелец ресурса или отказывает клиенту в запросе на доступ. | **Если пользователь предоставляет доступ&gt; &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Предполагая, что владелец ресурса предоставляет доступ, сервер авторизации перенаправляет агента пользователя обратно клиенту, используя перенаправление URI, предоставленное ранее (в запросе или во время регистрации клиента). ... |  |
|  |  |
| (D) Клиент запрашивает токен доступа из токенной точки сервера авторизации, включив код авторизации, полученный на предыдущем этапе. При совершении запроса клиент проверяет подлинность с помощью сервера авторизации. Клиент включает в себя перенаправление URI, используемое для получения кода авторизации для проверки. |  |

Поскольку мы уже внедрили конечную точку авторизации (действие)`OAuthController.Authorize` для предоставления кода авторизации, она автоматически позволяет неявно течь. Примечание: `Provider.ValidateClientRedirectUri` используется для проверки идентификатора клиента с URL-адресом перенаправления, который защищает неявный поток грантов от отправки токена доступа злоумышленникам[(атака «Человек в середине»).](https://www.owasp.org/index.php/Man-in-the-middle_attack)

### <a name="resource-owner-password-credentials-grant"></a>Грант владельца паролей ресурса

Обратитесь к OAuth 2 [IETF Владелец ресурсов Пароль полномочия Грант](http://tools.ietf.org/html/rfc6749#section-4.3) разделе сейчас.

 [Ресурс Владелец паролей учетные данные Грант](http://tools.ietf.org/html/rfc6749#section-4.3) поток, показанный на рисунке 5 является поток и отображение которых OWIN OAuth промежуточного следует.

| Поток шаги из раздела Грант учетных данных владельца паролей ресурса | Пример загрузки выполняет следующие шаги с: |
| --- | --- |
|  |  |
| (A) Владелец ресурса предоставляет клиенту имя пользователя и пароль. |  |
|  |  |
| (B) Клиент запрашивает токен доступа из токенной точки сервера авторизации, включив учетные данные, полученные от владельца ресурса. При совершении запроса клиент проверяет подлинность с помощью сервера авторизации. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (C) Сервер авторизации проверяет подлинность клиента и проверяет учетные данные владельца ресурса, а если он действителен, выдает токен доступа. |  |

Вот пример реализации: `Provider.GrantResourceOwnerCredentials`

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> Приведенный выше код предназначен для объяснения этого раздела учебника и не должен использоваться в защищенных или производственных приложениях. Он не проверяет учетные данные владельцев ресурсов. Он предполагает, что все учетные данные действительны и создает для нее новую идентификацию. Новая идентификация будет использоваться для создания токена доступа и обновления токена. Пожалуйста, замените код собственным кодом управления защищенным счетом.


### <a name="client-credentials-grant"></a>Грант на учетные данные клиентов

Обратитесь к разделу [Грант аттестат о предоставлении клиентских полномочий](http://tools.ietf.org/html/rfc6749#section-4.4) IETF В.О.2.

 [Клиент полномочия Грант](http://tools.ietf.org/html/rfc6749#section-4.4) поток показано на рисунке 6 является поток и отображение которых OWIN OAuth промежуточного следует.

| Шаги потока из раздела Грант учетных данных клиентов | Пример загрузки выполняет следующие шаги с: |
| --- | --- |
|  |  |
| (A) Клиент проверяет подлинность с помощью сервера авторизации и запрашивает токен доступа из точки конечных токенов. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (B) Сервер авторизации проверяет подлинность клиента, и если он действителен, выдает токен доступа. |  |

Вот пример реализации: `Provider.GrantClientCredentials`

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> Приведенный выше код предназначен для объяснения этого раздела учебника и не должен использоваться в защищенных или производственных приложениях. Пожалуйста, замените код собственным защищенным кодом управления клиентами.


### <a name="refresh-token"></a>Refresh Token

Обратитесь к [разделу](http://tools.ietf.org/html/rfc6749#section-1.5) OAuth 2 OAUF 2.

 Поток [Refresh Token,](http://tools.ietf.org/html/rfc6749#section-1.5) показанный на рисунке 2, — это поток и отображение, за которым следует промежуточное программное обеспечение OWIN OAuth.

| Шаги потока из раздела Грант учетных данных клиентов | Пример загрузки выполняет следующие шаги с: |
| --- | --- |
|  |  |
| (G) Клиент запрашивает новый токен доступа, завершая проверку подлинности с сервером авторизации и представляя токен обновления. Требования к аутентификации клиента основаны на типе клиента и на политиках сервера авторизации. | Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (H) Сервер авторизации проверяет подлинность клиента и проверяет токен обновления, и если он действителен, выдает новый токен доступа (и, по желанию, новый маркер обновления). |  |

Вот пример реализации: `Provider.GrantRefreshToken`

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>Создание сервера ресурсов, защищенного токеном доступа

Создайте пустой проект веб-приложения и установите следующие пакеты в проекте:

- Microsoft.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

Создайте класс запуска и назначайте аутентификацию и Web API. См *авторизацияServer-ResourceServer-Startup.cs* в примере загрузки.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

В примере загрузки сможете ознакомиться с загружаемой загрузкой *\_авторизацииСервер-РесурсСервер-Приложение Start.Start.Auth.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

В примере загрузки сможете *скачать авторизациюServer-ResourceServer-App\_Start.Start.WebApi.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`метод позволяет CORS для всех доменов.
- `UseOAuthBearerAuthentication`метод позволяет OAuth предъявителя маркера проверки подлинности промежуточной, которая будет получать и проверять маркер носителя из заголовка авторизации в запросе.
- `Config.SuppressDefaultHostAuthenticaiton`подавляет аутентифицированный принцип хоста по умолчанию из приложения, поэтому все запросы будут анонимными после этого вызова.
- `HostAuthenticationFilter`позволяет аутентификацию только для указанного типа проверки подлинности. В этом случае это тип проверки подлинности носителя.

Для демонстрации подлинной идентификации мы создаем ApiController для вывода текущих утверждений пользователя.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

Если сервер авторизации и сервер ресурсов не находятся на одном компьютере, промежуточное программное обеспечение OAuth будет использовать различные клавиши машины для шифрования и расшифровки токена доступа к носители. Для того, чтобы общий ключ между обоими `machinekey` проектами, мы добавляем один и тот же параметр в обоих файлах *web.config.*

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>Создание клиентов OAuth 2.0

 Мы используем пакет [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet для упрощения клиентского кода.

### <a name="authorization-code-grant-client"></a>Авторизация Код Грант Клиент

 Этот клиент является приложением MVC. Это вызовет поток грантов кода авторизации, чтобы получить токен доступа из бэкэнда. Он имеет одну страницу, как показано ниже:

![](owin-oauth-20-authorization-server/_static/image3.png)

- Кнопка **Authorize** перенаправит браузер на сервер авторизации, чтобы уведомить владельца ресурса предоставить доступ к этому клиенту.
- Кнопка **Обновления** получит новый токен доступа и обновит токен с помощью токена текущего обновления.
- Кнопка **API защищенного ресурсами доступа** вызовет сервер ресурсов, чтобы получить текущие данные о претензиях пользователя и показать их на странице.

Вот пример кода `HomeController` клиента.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`требует SSL по умолчанию. Так как наше демо использует HTTP, вам нужно добавить следующие настройки в файле конфигурации:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> Безопасность - Никогда не отменяйте SSL в производственном приложении. Ваши учетные данные входа теперь отправляются в четком тексте по проводу. Приведенный выше код предназначен только для локальной отладки и разведки образцов.


### <a name="implicit-grant-client"></a>Неявный грант клиент

Этот клиент использует JavaScript для:

1. Откройте новое окно и перенаправьте на авторизуеруконечную конечную точку сервера авторизации.
2. Получите токен доступа из фрагментов URL-адресов при перенаправлении назад.

На следующем изображении показан этот процесс:

![](owin-oauth-20-authorization-server/_static/image4.png)

Клиент должен иметь две страницы: одна для домашней страницы, а другая для обратного вызова. Вот пример кода JavaScript, найденный в файле *Index.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

Вот код обработки обратных вызовов в файле *SignIn.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> Наилучшей практикой является перемещение JavaScript во внешний файл, а не вставлять его с разметкой Razor. Чтобы сохранить этот образец простым, они были объединены.


### <a name="resource-owner-password-credentials-grant-client"></a>Ресурс Владелец Пароль Полномочия Грант Клиент

Мы с помощью консольного приложения для демонстрации этого клиента. Ниже приведен код:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>Клиент скиеили учетных данных Грант Клиент

Как и в ресурсе Владелец пароль полномочия Грант, вот код приложения консоли:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
