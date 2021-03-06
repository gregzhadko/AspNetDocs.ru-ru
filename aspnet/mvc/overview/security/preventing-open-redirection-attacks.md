---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: Предотвращение атак с открытым перенаправлениемC#() | Документация Майкрософт
author: jongalloway
description: В этом учебнике объясняется, как можно предотвратить атаки с открытым перенаправлением в приложениях ASP.NET MVC. В этом учебнике обсуждаются внесенные изменения...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432588"
---
# <a name="preventing-open-redirection-attacks-c"></a>Предотвращение атак с открытой переадресацией (C#)

[Джон Гэллоуэй](https://github.com/jongalloway)

> В этом учебнике объясняется, как можно предотвратить атаки с открытым перенаправлением в приложениях ASP.NET MVC. В этом учебнике обсуждаются изменения, внесенные в AccountController в ASP.NET MVC 3, и демонстрируется применение этих изменений в существующих приложениях ASP.NET MVC 1,0 и 2.

## <a name="what-is-an-open-redirection-attack"></a>Что такое атака с открытым перенаправлением?

Любое веб-приложение, которое перенаправляет на URL-адрес, указанный через запрос, например строку запроса или данные формы, потенциально может быть изменено для перенаправления пользователей на внешний вредоносный URL-адрес. Такое изменение данных называется атакой открытого перенаправления.

Каждый раз, когда логика вашего приложения выполняет перенаправление на определенный URL-адрес, нужно убедиться, что этот адрес не был изменен. Имя входа, используемое в AccountController по умолчанию для ASP.NET MVC 1,0 и ASP.NET MVC 2, уязвимо для атак с перенаправлением. К счастью, можно легко обновить существующие приложения, чтобы использовать исправления из ASP.NET MVC 3 Preview.

Чтобы разобраться в уязвимости, рассмотрим, как перенаправление имени входа работает в проекте веб-приложения ASP.NET MVC 2 по умолчанию. В этом приложении попытка посетить действие контроллера, имеющее атрибут [авторизовать], перенаправит неавторизованных пользователей в представление/аккаунт/Логон. Это перенаправление в/аккаунт/Логон будет включать параметр строки запроса returnUrl, чтобы пользователь мог вернуться к первоначально запрошенному URL-адресу после успешного входа.

На снимке экрана ниже видно, что попытка получить доступ к представлению/аккаунт/чанжепассворд при отсутствии входа в систему приводит к перенаправлению в/аккаунт/Логон? ReturnUrl =% 2fAccount% 2fChangePassword% 2F.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**Рис. 01**. страница входа с открытым перенаправлением

Так как параметр QueryString ReturnUrl не проверяется, злоумышленник может изменить его, чтобы внедрить любой URL-адрес в параметр для проведения атаки с открытым перенаправлением. Чтобы продемонстрировать это, можно изменить параметр ReturnUrl на [http://bing.com](http://bing.com), чтобы итоговый URL-адрес входа был/аккаунт/Логон? ReturnUrl =<http://www.bing.com/>. После успешного входа на сайт мы перенаправлены на [http://bing.com](http://bing.com). Так как перенаправление не проверено, оно может указывать на вредоносный веб-узел, пытающийся обману пользователя.

### <a name="a-more-complex-open-redirection-attack"></a>Более сложная атака с открытым перенаправлением

Атаки с открытым перенаправлением особенно опасны, поскольку злоумышленник знает, что мы пытаемся войти на конкретный веб-сайт, что делает уязвимыми для [фишинговых атак](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx). Например, злоумышленник может отправить вредоносные сообщения электронной почты пользователям веб-сайта при попытке записи паролей. Давайте посмотрим, как это будет работать на сайте NerdDinner. (Обратите внимание, что активный веб-сайт NerdDinner обновлен для защиты от атак с открытым перенаправлением).

Во-первых, злоумышленник отправляет нам ссылку на страницу входа в NerdDinner, которая включает перенаправление на подложные страницы:

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

Обратите внимание, что URL-адрес возврата указывает на nerddiner.com, в котором отсутствует "n" из слова "ужин". В этом примере это домен, который контролируется злоумышленником. Когда мы доступ к приведенной выше ссылке, мы переходим на страницу допустимого входа в NerdDinner.com.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**Рис. 02**. страница входа в NerdDinner с открытым перенаправлением

При правильном входе в систему ASP.NET MVC AccountController выполняет переадресацию по URL-адресу, указанному в параметре QueryString строки returnUrl. В данном случае это URL-адрес, который злоумышленник вводит, что [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn). Если мы не очень ватчфул, то, скорее всего, мы не будем заметить это, особенно потому, что злоумышленник следит за тем, чтобы их поддельная страница отображалась точно так же, как и страница легального входа. Эта страница входа содержит сообщение об ошибке с запросом на повторное вход. Неловкий нам, нам нужно ввести пароль.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**Рис. 03**. экран входа с подложным NerdDinner

При повторном вводе имени пользователя и пароля страница с подложным входом сохраняет информацию и отправляет нам на законный сайт NerdDinner.com. На этом этапе сайт NerdDinner.com уже прошел проверку подлинности, поэтому поддельная страница входа может перенаправляться непосредственно на эту страницу. Конечным результатом является то, что у злоумышленника есть имя пользователя и пароль, и мы не осведомлены о том, что они предоставлены.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>Просмотр уязвимого кода в действии входа AccountController

Ниже показан код для действия LogOn в приложении ASP.NET MVC 2. Обратите внимание, что при успешном входе контроллер возвращает перенаправление к returnUrl. Вы видите, что для параметра returnUrl не выполняется проверка.

**Листинг 1 – ASP.NET. действие входа MVC 2 в `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

Теперь давайте взглянем на изменения в действии входа в ASP.NET MVC 3. Этот код был изменен для проверки параметра returnUrl путем вызова нового метода в классе вспомогательного класса System. Web. MVC. URL с именем `IsLocalUrl()`.

**Листинг 2 – ASP.NETое действие входа MVC 3 в `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

Это было изменено для проверки параметра URL-адреса возврата путем вызова нового метода в классе поддержки System. Web. MVC. URL `IsLocalUrl()`.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>Защита приложений ASP.NET MVC 1,0 и MVC 2

Мы можем воспользоваться преимуществами ASP.NET MVC 3 в существующих приложениях ASP.NET MVC 1,0 и 2, добавив вспомогательный метод Ислокалурл () и обновив действие LogOn для проверки параметра returnUrl.

Метод Урлхелпер Ислокалурл () на самом деле просто вызывает метод в System. Web. веб-страниц, так как эта проверка также используется приложениями веб-страницы ASP.NET.

**Листинг 3 — метод Ислокалурл () из ASP.NET MVC 3 Урлхелпер `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

Метод Исурллокалтохост содержит реальную логику проверки, как показано в листинге 4.

**Листинг 4 — метод Исурллокалтохост () из класса System. Web. Рекуестекстенсионс**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

В нашем приложении ASP.NET MVC 1,0 или 2 мы добавим метод Ислокалурл () в AccountController, но по возможности рекомендуется добавить его в отдельный вспомогательный класс. Мы будем вносить два небольших изменения в версию Ислокалурл () ASP.NET MVC 3, чтобы она работала внутри AccountController. Во-первых, мы изменим его из открытого метода на частный метод, так как доступ к открытым методам в контроллерах можно получить как к действиям контроллера. Во-вторых, мы изменим вызов, который проверяет узел с адресом URL на соответствие узлу приложения. Этот вызов использует локальное поле RequestContext в классе Урлхелпер. Вместо этого используйте. RequestContext. HttpContext. Request. URL. Host, мы будем использовать его. Request. URL. host. В следующем коде показан измененный метод Ислокалурл () для использования с классом контроллера в приложениях ASP.NET MVC 1,0 и 2.

**Листинг 5 — метод Ислокалурл (), который изменяется для использования с классом контроллера MVC**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

Теперь, когда используется метод Ислокалурл (), мы можем вызвать его из нашего действия входа, чтобы проверить параметр returnUrl, как показано в следующем коде.

**Листинг 6 — обновленный метод LogOn, который проверяет параметр returnUrl**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

Теперь мы можем протестировать атаку с открытой перенаправлением, пытаясь войти с помощью внешнего URL-адреса возврата. Будем использовать/аккаунт/Логон? ReturnUrl =<http://www.bing.com/> еще раз.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**Рис. 04**. Проверка обновленного действия входа

После успешного входа в систему мы будем перенаправлены к действию контроллера Home или index, а не к внешнему URL-адресу.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**Рис. 05**. Немонопольная атака с перенаправлением

## <a name="summary"></a>Сводка

Атаки с перенаправлением могут происходить, когда URL-адреса перенаправления передаются в качестве параметров в URL-адресе приложения. Шаблон ASP.NET MVC 3 содержит код для защиты от атак с открытым перенаправлением. Этот код можно добавить с некоторыми изменениями в приложения ASP.NET MVC 1,0 и 2. Чтобы защититься от атак с открытым перенаправлением при входе в приложения ASP.NET 1,0 и 2, добавьте метод Ислокалурл () и проверьте параметр returnUrl в действии LogOn.
