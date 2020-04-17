---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Использование CAPTCHA для предотвращения Ботов от использования вашего ASP.NET веб-razor) сайт Документы Майкрософт
author: rick-anderson
description: В этой статье объясняется, как использовать ReCaptcha (мера безопасности), чтобы предотвратить автоматизированные программы (боты) от выполнения задач в ASP.NET веб-страниц (Razor) мы ...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543760"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Использование CAPTCHA для предотвращения ботов от использования ASP.NET веб-razor) сайт

[корпорацией Майкрософт](https://github.com/microsoft)

> В этой статье объясняется, как использовать ReCaptcha (мера безопасности) для предотвращения автоматизированных программ (ботов) от выполнения задач в веб-сайте ASP.NET web Pages (Razor).
> 
> **Из этого руководства вы узнаете, как выполнять такие задачи:** 
> 
> - Как добавить тест CAPTCHA на ваш сайт.
> 
> Вот ASP.NET функции, представленные в статье:
> 
> - Помощник. `ReCaptcha`
> 
> > [!NOTE]
> > Информация в этой статье относится к ASP.NET веб-страниц 1.0 и web Pages 2.

## <a name="about-captchas"></a>О КАПЦА

Каждый раз, когда вы позволяете людям зарегистрироваться на вашем сайте, или даже просто ввести имя и URL (например, для блога комментарий), вы можете получить поток поддельных имен. Они часто оставляют автоматизированные программы (боты), которые пытаются оставить URL-адреса в каждом веб-сайте они могут найти. (Общая мотивация заключается в том, чтобы разместить URL-адреса продуктов для продажи.)

Вы можете помочь убедиться, что пользователь является реальным человеком, а не компьютерной программой, используя *CAPTCHA* для проверки пользователей, когда они регистрируются или иным образом вводят свое имя и сайт. CAPTCHA означает полностью автоматизированный тест общественного Тьюринга, чтобы рассказать Компьютеры и люди Помимо. CAPTCHA – это тест *на вызов,* в котором пользователю предлагается сделать что-то, что легко сделать человеку, но трудно для автоматизированной программы. Наиболее распространенным типом CAPTCHA является тип, где вы видите некоторые искаженные буквы и просят ввести их. (Предполагалось, что искажение затрудняет расшифровку букв ботами.)

## <a name="adding-a-recaptcha-test"></a>Добавление reCaptcha тест

На ASP.NET страницах можно `ReCaptcha` использовать помощника для отображаемтести CAPTCHA,[http://recaptcha.net](http://recaptcha.net)основанного на сервисе ReCaptcha (). Помощник `ReCaptcha` отображает изображение двух искаженных слов, которые пользователи должны ввести правильно, прежде чем страница будет проверена. Ответ пользователя проверяется службой ReCaptcha.Net.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Зарегистрируйте свой[http://recaptcha.net](http://recaptcha.net)сайт по адресу ReCaptcha.Net (). После завершения регистрации вы получите открытый ключ и закрытый ключ.
2. Если вы еще этого не сделали веб-страницы ASP.NET Web Helpers Library, описанную в [ASP.NET веб-страниц.](https://go.microsoft.com/fwlink/?LinkId=252372)
3. Если у вас еще нет файла * \_AppStart.cshtml,* в корневой папке веб-сайта создайте файл под названием * \_AppStart.cshtml.*
4. Добавьте `Recaptcha` следующие настройки помощника в файл * \_AppStart.cshtml:* 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Установите `PublicKey` `PrivateKey` и свойства, используя свои собственные государственные и частные ключи.
6. Сохраните файл * \_AppStart.cshtml* и закройте его.
7. В корневой папке веб-сайта создайте новую страницу под названием *Recaptcha.cshtml*.
8. Замените существующее содержимое следующим: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. Выполнить страницу *Recaptcha.cshtml* в браузере. Если `PrivateKey` значение действительно, страница отображает управление ReCaptcha и кнопку. Если бы вы не установили ключи глобально в * \_AppStart.html,* на странице была бы отображалась ошибка. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Введите слова для теста. Если вы пройдете тест ReCaptcha, вы увидите сообщение на этот счет. В противном случае вы видите сообщение об ошибке и повторно отображается элемент управления ReCaptcha.

> [!NOTE]
> Если ваш компьютер находится на домене, который использует прокси-сервер, возможно, потребуется настроить `defaultproxy` элемент файла *Web.config.* В следующем примере показан файл *Web.config* с элементом, `defaultproxy` настроенным для работы службы ReCaptcha.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Настройка поведения по всему сайту для ASP.NET веб-страниц](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha сайт](https://www.google.com/recaptcha)
