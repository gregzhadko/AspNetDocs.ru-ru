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
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="77bd0-103">Использование CAPTCHA для предотвращения ботов от использования ASP.NET веб-razor) сайт</span><span class="sxs-lookup"><span data-stu-id="77bd0-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="77bd0-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="77bd0-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="77bd0-105">В этой статье объясняется, как использовать ReCaptcha (мера безопасности) для предотвращения автоматизированных программ (ботов) от выполнения задач в веб-сайте ASP.NET web Pages (Razor).</span><span class="sxs-lookup"><span data-stu-id="77bd0-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="77bd0-106">**Из этого руководства вы узнаете, как выполнять такие задачи:**</span><span class="sxs-lookup"><span data-stu-id="77bd0-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="77bd0-107">Как добавить тест CAPTCHA на ваш сайт.</span><span class="sxs-lookup"><span data-stu-id="77bd0-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="77bd0-108">Вот ASP.NET функции, представленные в статье:</span><span class="sxs-lookup"><span data-stu-id="77bd0-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="77bd0-109">Помощник. `ReCaptcha`</span><span class="sxs-lookup"><span data-stu-id="77bd0-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="77bd0-110">Информация в этой статье относится к ASP.NET веб-страниц 1.0 и web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="77bd0-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="77bd0-111">О КАПЦА</span><span class="sxs-lookup"><span data-stu-id="77bd0-111">About CAPTCHAs</span></span>

<span data-ttu-id="77bd0-112">Каждый раз, когда вы позволяете людям зарегистрироваться на вашем сайте, или даже просто ввести имя и URL (например, для блога комментарий), вы можете получить поток поддельных имен.</span><span class="sxs-lookup"><span data-stu-id="77bd0-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="77bd0-113">Они часто оставляют автоматизированные программы (боты), которые пытаются оставить URL-адреса в каждом веб-сайте они могут найти.</span><span class="sxs-lookup"><span data-stu-id="77bd0-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="77bd0-114">(Общая мотивация заключается в том, чтобы разместить URL-адреса продуктов для продажи.)</span><span class="sxs-lookup"><span data-stu-id="77bd0-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="77bd0-115">Вы можете помочь убедиться, что пользователь является реальным человеком, а не компьютерной программой, используя *CAPTCHA* для проверки пользователей, когда они регистрируются или иным образом вводят свое имя и сайт.</span><span class="sxs-lookup"><span data-stu-id="77bd0-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="77bd0-116">CAPTCHA означает полностью автоматизированный тест общественного Тьюринга, чтобы рассказать Компьютеры и люди Помимо.</span><span class="sxs-lookup"><span data-stu-id="77bd0-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="77bd0-117">CAPTCHA – это тест *на вызов,* в котором пользователю предлагается сделать что-то, что легко сделать человеку, но трудно для автоматизированной программы.</span><span class="sxs-lookup"><span data-stu-id="77bd0-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="77bd0-118">Наиболее распространенным типом CAPTCHA является тип, где вы видите некоторые искаженные буквы и просят ввести их.</span><span class="sxs-lookup"><span data-stu-id="77bd0-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="77bd0-119">(Предполагалось, что искажение затрудняет расшифровку букв ботами.)</span><span class="sxs-lookup"><span data-stu-id="77bd0-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="77bd0-120">Добавление reCaptcha тест</span><span class="sxs-lookup"><span data-stu-id="77bd0-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="77bd0-121">На ASP.NET страницах можно `ReCaptcha` использовать помощника для отображаемтести CAPTCHA,[http://recaptcha.net](http://recaptcha.net)основанного на сервисе ReCaptcha ().</span><span class="sxs-lookup"><span data-stu-id="77bd0-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="77bd0-122">Помощник `ReCaptcha` отображает изображение двух искаженных слов, которые пользователи должны ввести правильно, прежде чем страница будет проверена.</span><span class="sxs-lookup"><span data-stu-id="77bd0-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="77bd0-123">Ответ пользователя проверяется службой ReCaptcha.Net.</span><span class="sxs-lookup"><span data-stu-id="77bd0-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="77bd0-124">Зарегистрируйте свой[http://recaptcha.net](http://recaptcha.net)сайт по адресу ReCaptcha.Net ().</span><span class="sxs-lookup"><span data-stu-id="77bd0-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="77bd0-125">После завершения регистрации вы получите открытый ключ и закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="77bd0-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="77bd0-126">Если вы еще этого не сделали веб-страницы ASP.NET Web Helpers Library, описанную в [ASP.NET веб-страниц.](https://go.microsoft.com/fwlink/?LinkId=252372)</span><span class="sxs-lookup"><span data-stu-id="77bd0-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="77bd0-127">Если у вас еще нет файла \* \_AppStart.cshtml,\* в корневой папке веб-сайта создайте файл под названием \* \_AppStart.cshtml.\*</span><span class="sxs-lookup"><span data-stu-id="77bd0-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="77bd0-128">Добавьте `Recaptcha` следующие настройки помощника в файл \* \_AppStart.cshtml:\*</span><span class="sxs-lookup"><span data-stu-id="77bd0-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="77bd0-129">Установите `PublicKey` `PrivateKey` и свойства, используя свои собственные государственные и частные ключи.</span><span class="sxs-lookup"><span data-stu-id="77bd0-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="77bd0-130">Сохраните файл \* \_AppStart.cshtml\* и закройте его.</span><span class="sxs-lookup"><span data-stu-id="77bd0-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="77bd0-131">В корневой папке веб-сайта создайте новую страницу под названием *Recaptcha.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="77bd0-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="77bd0-132">Замените существующее содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="77bd0-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="77bd0-133">Выполнить страницу *Recaptcha.cshtml* в браузере.</span><span class="sxs-lookup"><span data-stu-id="77bd0-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="77bd0-134">Если `PrivateKey` значение действительно, страница отображает управление ReCaptcha и кнопку.</span><span class="sxs-lookup"><span data-stu-id="77bd0-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="77bd0-135">Если бы вы не установили ключи глобально в \* \_AppStart.html,\* на странице была бы отображалась ошибка.</span><span class="sxs-lookup"><span data-stu-id="77bd0-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="77bd0-136">Введите слова для теста.</span><span class="sxs-lookup"><span data-stu-id="77bd0-136">Enter the words for the test.</span></span> <span data-ttu-id="77bd0-137">Если вы пройдете тест ReCaptcha, вы увидите сообщение на этот счет.</span><span class="sxs-lookup"><span data-stu-id="77bd0-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="77bd0-138">В противном случае вы видите сообщение об ошибке и повторно отображается элемент управления ReCaptcha.</span><span class="sxs-lookup"><span data-stu-id="77bd0-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="77bd0-139">Если ваш компьютер находится на домене, который использует прокси-сервер, возможно, потребуется настроить `defaultproxy` элемент файла *Web.config.*</span><span class="sxs-lookup"><span data-stu-id="77bd0-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="77bd0-140">В следующем примере показан файл *Web.config* с элементом, `defaultproxy` настроенным для работы службы ReCaptcha.</span><span class="sxs-lookup"><span data-stu-id="77bd0-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="77bd0-141">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="77bd0-141">Additional Resources</span></span>

- [<span data-ttu-id="77bd0-142">Настройка поведения по всему сайту для ASP.NET веб-страниц</span><span class="sxs-lookup"><span data-stu-id="77bd0-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="77bd0-143">ReCaptcha сайт</span><span class="sxs-lookup"><span data-stu-id="77bd0-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
