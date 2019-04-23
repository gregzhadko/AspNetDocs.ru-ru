---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: Предотвращение открытой переадресацией (C#) | Документация Майкрософт
author: jongalloway
description: В этом учебнике объясняется, как предотвратить открытой переадресацией в приложениях ASP.NET MVC. В этом руководстве рассматриваются изменения, внесенные...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 1d83ede97ec37166d8dec32ff9e21c65423f3fc5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59408489"
---
# <a name="preventing-open-redirection-attacks-c"></a>Предотвращение атак с открытой переадресацией (C#)

по [Джон Гэллоуэй](https://github.com/jongalloway)

> В этом учебнике объясняется, как предотвратить открытой переадресацией в приложениях ASP.NET MVC. Этом руководстве описываются изменения, внесенные в AccountController в ASP.NET MVC 3 и показано, как применять эти изменения в вашей существующей ASP.NET MVC 1.0 и 2 приложения.


## <a name="what-is-an-open-redirection-attack"></a>Что такое Атака перенаправления открытым?

Любой веб-приложение, которое перенаправляет на URL-адрес, который задается с помощью запроса, такие как данные строки запроса или формы потенциально могут быть подделаны для перенаправления пользователей на внешний, вредоносный URL-адрес. Такое изменение данных называется атакой открытого перенаправления.

Каждый раз, когда логика вашего приложения выполняет перенаправление на определенный URL-адрес, нужно убедиться, что этот адрес не был изменен. Имя входа, используемое в AccountController по умолчанию для ASP.NET MVC 1.0 и ASP.NET MVC 2 становится уязвимым для атак путем перенаправления открыть. К счастью это легко обновить существующие приложения, чтобы воспользоваться исправлениями из предварительной версии ASP.NET MVC 3.

Чтобы понять уязвимость, давайте взглянем на принципах перенаправление входа в проект веб-приложение ASP.NET MVC 2 по умолчанию. В этом приложении пытающийся открыть действие контроллера, в котором есть атрибут [Authorize] перенаправляет неавторизованных пользователей к представлению /Account/LogOn. Это перенаправление к /Account/LogOn будет включать параметр строки запроса returnUrl таким образом, пользователю могут быть возвращены на первоначально запрошенный URL-адрес, после успешного входа.

В нашем примере мы видим, что попытка доступа к данному представлению /Account/ChangePassword при входе не приводит к перенаправления с /Account/LogOn? ReturnUrl = % 2fAccount % 2fChangePassword % 2f.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**Рис 01**: Страница входа с открытое перенаправление

Так как параметр строки запроса ReturnUrl не проверяется, злоумышленник может изменить его, чтобы внедрить любой URL-адрес в качестве параметра для проведения атаки открытое перенаправление. Чтобы продемонстрировать это, можно изменить параметр ReturnUrl [ http://bing.com ](http://bing.com), поэтому полученный URL-адрес входа будет/учетной записи и входа в систему? ReturnUrl =<http://www.bing.com/>. После успешного входа на сайт, то будут перенаправлены в [ http://bing.com ](http://bing.com). Так как это перенаправление не проверяется, он вместо этого может указывать на вредоносный сайт, которые пытаются обмануть пользователя.

### <a name="a-more-complex-open-redirection-attack"></a>Более сложные откройте Атака перенаправления

Открытое перенаправление атаки особенно опасны, потому, что злоумышленник знает, что мы пытаемся войдите определенного веб-сайта, что позволяет нам уязвимым для [фишинга](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx). Например злоумышленник может отправить вредоносных сообщений электронной почты для пользователей веб-сайта при попытке записать свои пароли. Давайте рассмотрим, как это будет работать на сайте NerdDinner. (Обратите внимание, что на действующем сайте NerdDinner был обновлен для защиты от атак открытое перенаправление.)

Во-первых злоумышленник отправляет нам ссылку на страницу входа в NerdDinner, включающий перенаправление на подложных страницу:

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

Обратите внимание, что URL-адрес возврата указывает nerddiner.com, в которой отсутствует буквой «n» из компании dinner word. В этом примере это домен, злоумышленник контролирует. Когда мы обращаются к ссылку выше, мы будете перенаправлены на странице входа законным NerdDinner.com.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**Рис. 02**: Страница входа NerdDinner с открытое перенаправление

Когда мы правильно войти в систему, действие входа ASP.NET MVC AccountController перенаправляет нам URL-адрес, указанный в параметре строки запроса returnUrl. В данном случае это URL-адрес, злоумышленник вошел, который является [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn). Если мы не очень непонятны, он скорее всего, мы не заметят, особенно в том случае, поскольку злоумышленник не осторожность, чтобы убедиться, что их подложных страница выглядит так же, как на страницу входа законным. Эта страница для входа — это сообщение Ошибка, запрос, что мы снова войти в систему. Неловкий нами, мы должны ввели пароль.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**Рис 03**: Поддельного экрана входа NerdDinner

Когда мы заново, наши имя пользователя и пароль, страница подложных входа сохраняет сведения о и отправляет нам NerdDinner.com настоящий узел. На этом этапе NerdDinner.com сайта уже проверку подлинности нам, поэтому можно перенаправить на страницу входа подложных непосредственно на эту страницу. Конечным результатом является злоумышленник имеет наших имя пользователя и пароль, что мы не знают, что мы предоставляем его к ним.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>Просмотрев уязвимого кода в действии входа AccountController

Ниже приведен код для действия входа в приложение ASP.NET MVC 2. Обратите внимание, что после успешного входа, контроллер возвращает перенаправление на returnUrl. Вы увидите, что проверка не выполняется с параметром returnUrl.

**В листинге 1 — действия ASP.NET MVC 2 входа в `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

Теперь давайте взглянем на изменения в ASP.NET MVC 3 входа действия. Этот код был изменен для проверки параметра returnUrl путем вызова нового метода во вспомогательном классе System.Web.Mvc.Url с именем `IsLocalUrl()`.

**Листинг 2 – действия ASP.NET MVC 3 входа в `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

Это свойство изменено для проверки значения, возвращаемого URL-адрес, вызвав новый метод во вспомогательном классе System.Web.Mvc.Url, `IsLocalUrl()`.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>Защита MVC 2 и ASP.NET MVC 1.0 приложений

Мы можно воспользоваться преимуществами изменения ASP.NET MVC 3 в наши существующие ASP.NET MVC 1.0 и 2 приложения путем добавления вспомогательного метода IsLocalUrl() и выполняется обновление действия входа для проверки параметра returnUrl.

Метод UrlHelper IsLocalUrl(), фактически вызов метода в System.Web.WebPages, как эта проверка также используется приложениями веб-страниц ASP.NET.

**Листинг 3 – метод IsLocalUrl() из ASP.NET MVC 3 UrlHelper `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

Метод IsUrlLocalToHost содержит логики проверки, как показано в листинге 4.

**Листинг 4 – метод IsUrlLocalToHost() класса System.Web.WebPages RequestExtensions**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

В нашем ASP.NET MVC 1.0 или 2 приложения мы добавим метод IsLocalUrl() AccountController, но настоятельно рекомендуется, чтобы добавить его в отдельном вспомогательном классе, если это возможно. Мы сделать две небольшие изменения в ASP.NET MVC 3 версию IsLocalUrl(), чтобы он будет работать внутри AccountController. Во-первых мы изменим его из открытого метода в закрытый метод, так как открытые методы в контроллерах доступны в виде действий контроллера. Во-вторых мы изменим проверки узла URL-адрес для узла приложения. Что вызов использует локальный RequestContext в класс UrlHelper. Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host. Ниже приведен измененный метод IsLocalUrl() для использования с классом контроллера в ASP.NET MVC 1.0 и 2 приложения.

**В листинге 5 – IsLocalUrl() метод, который изменяется для использования с классом контроллера MVC**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

Теперь, когда метод IsLocalUrl() находится в месте, можно вызывать его из действии входа для проверки параметра returnUrl, как показано в следующем коде.

**В листинге 6 – Updated входа, который проверяет параметр returnUrl**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

Теперь мы можем протестировать атака открытое перенаправление, попытавшись выполнить вход с использованием внешних URL-адрес возврата. Давайте используем /Account/LogOn? ReturnUrl =<http://www.bing.com/> еще раз.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**Рис. 04**: Тестирование обновление действия входа в систему

После успешного входа в систему, мы перенаправляются на действие контроллера Home/Index, а не внешний URL-адрес.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**05 рис**: Откройте изменило Атака перенаправления

## <a name="summary"></a>Сводка

Открытой переадресацией может произойти при перенаправлении URL-адреса передаются как параметры в URL-адрес для приложения. ASP.NET MVC 3, шаблон включает код для защиты от откройте атак путем перенаправления. Вы можете добавить этот код с некоторыми изменениями в ASP.NET MVC 1.0 и 2 приложения. Для защиты от атак открытое перенаправление, при входе в ASP.NET 1.0 и 2 приложения, добавьте метод IsLocalUrl() и проверить параметр returnUrl в действии входа в систему.
