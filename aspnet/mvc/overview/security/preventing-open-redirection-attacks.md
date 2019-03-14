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
ms.openlocfilehash: 767f9c85527fbcdf34e700eb32fe0c6cad30bf0c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027401"
---
<a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="84921-104">Предотвращение атак с открытой переадресацией (C#)</span><span class="sxs-lookup"><span data-stu-id="84921-104">Preventing Open Redirection Attacks (C#)</span></span>
====================
<span data-ttu-id="84921-105">по [Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="84921-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="84921-106">В этом учебнике объясняется, как предотвратить открытой переадресацией в приложениях ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="84921-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="84921-107">Этом руководстве описываются изменения, внесенные в AccountController в ASP.NET MVC 3 и показано, как применять эти изменения в вашей существующей ASP.NET MVC 1.0 и 2 приложения.</span><span class="sxs-lookup"><span data-stu-id="84921-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>


## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="84921-108">Что такое Атака перенаправления открытым?</span><span class="sxs-lookup"><span data-stu-id="84921-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="84921-109">Любой веб-приложение, которое перенаправляет на URL-адрес, который задается с помощью запроса, такие как данные строки запроса или формы потенциально могут быть подделаны для перенаправления пользователей на внешний, вредоносный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="84921-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="84921-110">Такое изменение данных называется атакой открытого перенаправления.</span><span class="sxs-lookup"><span data-stu-id="84921-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="84921-111">Каждый раз, когда логика вашего приложения выполняет перенаправление на определенный URL-адрес, нужно убедиться, что этот адрес не был изменен.</span><span class="sxs-lookup"><span data-stu-id="84921-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="84921-112">Имя входа, используемое в AccountController по умолчанию для ASP.NET MVC 1.0 и ASP.NET MVC 2 становится уязвимым для атак путем перенаправления открыть.</span><span class="sxs-lookup"><span data-stu-id="84921-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="84921-113">К счастью это легко обновить существующие приложения, чтобы воспользоваться исправлениями из предварительной версии ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="84921-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="84921-114">Чтобы понять уязвимость, давайте взглянем на принципах перенаправление входа в проект веб-приложение ASP.NET MVC 2 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="84921-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="84921-115">В этом приложении пытающийся открыть действие контроллера, в котором есть атрибут [Authorize] перенаправляет неавторизованных пользователей к представлению /Account/LogOn.</span><span class="sxs-lookup"><span data-stu-id="84921-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="84921-116">Это перенаправление к /Account/LogOn будет включать параметр строки запроса returnUrl таким образом, пользователю могут быть возвращены на первоначально запрошенный URL-адрес, после успешного входа.</span><span class="sxs-lookup"><span data-stu-id="84921-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="84921-117">В нашем примере мы видим, что попытка доступа к данному представлению /Account/ChangePassword при входе не приводит к перенаправления с /Account/LogOn? ReturnUrl = % 2fAccount % 2fChangePassword % 2f.</span><span class="sxs-lookup"><span data-stu-id="84921-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="84921-118">**Рис 01**: Страница входа с открытое перенаправление</span><span class="sxs-lookup"><span data-stu-id="84921-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="84921-119">Так как параметр строки запроса ReturnUrl не проверяется, злоумышленник может изменить его, чтобы внедрить любой URL-адрес в качестве параметра для проведения атаки открытое перенаправление.</span><span class="sxs-lookup"><span data-stu-id="84921-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="84921-120">Чтобы продемонстрировать это, можно изменить параметр ReturnUrl [ http://bing.com ](http://bing.com), поэтому полученный URL-адрес входа будет/учетной записи и входа в систему? ReturnUrl =<http://www.bing.com/>.</span><span class="sxs-lookup"><span data-stu-id="84921-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="84921-121">После успешного входа на сайт, то будут перенаправлены в [ http://bing.com ](http://bing.com).</span><span class="sxs-lookup"><span data-stu-id="84921-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com).</span></span> <span data-ttu-id="84921-122">Так как это перенаправление не проверяется, он вместо этого может указывать на вредоносный сайт, которые пытаются обмануть пользователя.</span><span class="sxs-lookup"><span data-stu-id="84921-122">Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="84921-123">Более сложные откройте Атака перенаправления</span><span class="sxs-lookup"><span data-stu-id="84921-123">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="84921-124">Открытое перенаправление атаки особенно опасны, потому, что злоумышленник знает, что мы пытаемся войдите определенного веб-сайта, что позволяет нам уязвимым для [фишинга](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span><span class="sxs-lookup"><span data-stu-id="84921-124">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="84921-125">Например злоумышленник может отправить вредоносных сообщений электронной почты для пользователей веб-сайта при попытке записать свои пароли.</span><span class="sxs-lookup"><span data-stu-id="84921-125">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="84921-126">Давайте рассмотрим, как это будет работать на сайте NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="84921-126">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="84921-127">(Обратите внимание, что на действующем сайте NerdDinner был обновлен для защиты от атак открытое перенаправление.)</span><span class="sxs-lookup"><span data-stu-id="84921-127">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="84921-128">Во-первых злоумышленник отправляет нам ссылку на страницу входа в NerdDinner, включающий перенаправление на подложных страницу:</span><span class="sxs-lookup"><span data-stu-id="84921-128">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="84921-129">Обратите внимание, что URL-адрес возврата указывает nerddiner.com, в которой отсутствует буквой «n» из компании dinner word.</span><span class="sxs-lookup"><span data-stu-id="84921-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="84921-130">В этом примере это домен, злоумышленник контролирует.</span><span class="sxs-lookup"><span data-stu-id="84921-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="84921-131">Когда мы обращаются к ссылку выше, мы будете перенаправлены на странице входа законным NerdDinner.com.</span><span class="sxs-lookup"><span data-stu-id="84921-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="84921-132">**Рис. 02**: Страница входа NerdDinner с открытое перенаправление</span><span class="sxs-lookup"><span data-stu-id="84921-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="84921-133">Когда мы правильно войти в систему, действие входа ASP.NET MVC AccountController перенаправляет нам URL-адрес, указанный в параметре строки запроса returnUrl.</span><span class="sxs-lookup"><span data-stu-id="84921-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="84921-134">В данном случае это URL-адрес, злоумышленник вошел, который является [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="84921-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="84921-135">Если мы не очень непонятны, он скорее всего, мы не заметят, особенно в том случае, поскольку злоумышленник не осторожность, чтобы убедиться, что их подложных страница выглядит так же, как на страницу входа законным.</span><span class="sxs-lookup"><span data-stu-id="84921-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="84921-136">Эта страница для входа — это сообщение Ошибка, запрос, что мы снова войти в систему.</span><span class="sxs-lookup"><span data-stu-id="84921-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="84921-137">Неловкий нами, мы должны ввели пароль.</span><span class="sxs-lookup"><span data-stu-id="84921-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="84921-138">**Рис 03**: Поддельного экрана входа NerdDinner</span><span class="sxs-lookup"><span data-stu-id="84921-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="84921-139">Когда мы заново, наши имя пользователя и пароль, страница подложных входа сохраняет сведения о и отправляет нам NerdDinner.com настоящий узел.</span><span class="sxs-lookup"><span data-stu-id="84921-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="84921-140">На этом этапе NerdDinner.com сайта уже проверку подлинности нам, поэтому можно перенаправить на страницу входа подложных непосредственно на эту страницу.</span><span class="sxs-lookup"><span data-stu-id="84921-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="84921-141">Конечным результатом является злоумышленник имеет наших имя пользователя и пароль, что мы не знают, что мы предоставляем его к ним.</span><span class="sxs-lookup"><span data-stu-id="84921-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="84921-142">Просмотрев уязвимого кода в действии входа AccountController</span><span class="sxs-lookup"><span data-stu-id="84921-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="84921-143">Ниже приведен код для действия входа в приложение ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="84921-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="84921-144">Обратите внимание, что после успешного входа, контроллер возвращает перенаправление на returnUrl.</span><span class="sxs-lookup"><span data-stu-id="84921-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="84921-145">Вы увидите, что проверка не выполняется с параметром returnUrl.</span><span class="sxs-lookup"><span data-stu-id="84921-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="84921-146">**В листинге 1 — действия ASP.NET MVC 2 входа в `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="84921-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="84921-147">Теперь давайте взглянем на изменения в ASP.NET MVC 3 входа действия.</span><span class="sxs-lookup"><span data-stu-id="84921-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="84921-148">Этот код был изменен для проверки параметра returnUrl путем вызова нового метода во вспомогательном классе System.Web.Mvc.Url с именем `IsLocalUrl()`.</span><span class="sxs-lookup"><span data-stu-id="84921-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="84921-149">**Листинг 2 – действия ASP.NET MVC 3 входа в `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="84921-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="84921-150">Это свойство изменено для проверки значения, возвращаемого URL-адрес, вызвав новый метод во вспомогательном классе System.Web.Mvc.Url, `IsLocalUrl()`.</span><span class="sxs-lookup"><span data-stu-id="84921-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="84921-151">Защита MVC 2 и ASP.NET MVC 1.0 приложений</span><span class="sxs-lookup"><span data-stu-id="84921-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="84921-152">Мы можно воспользоваться преимуществами изменения ASP.NET MVC 3 в наши существующие ASP.NET MVC 1.0 и 2 приложения путем добавления вспомогательного метода IsLocalUrl() и выполняется обновление действия входа для проверки параметра returnUrl.</span><span class="sxs-lookup"><span data-stu-id="84921-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="84921-153">Метод UrlHelper IsLocalUrl(), фактически вызов метода в System.Web.WebPages, как эта проверка также используется приложениями веб-страниц ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="84921-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="84921-154">**Листинг 3 – метод IsLocalUrl() из ASP.NET MVC 3 UrlHelper `class`**</span><span class="sxs-lookup"><span data-stu-id="84921-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="84921-155">Метод IsUrlLocalToHost содержит логики проверки, как показано в листинге 4.</span><span class="sxs-lookup"><span data-stu-id="84921-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="84921-156">**Листинг 4 – метод IsUrlLocalToHost() класса System.Web.WebPages RequestExtensions**</span><span class="sxs-lookup"><span data-stu-id="84921-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="84921-157">В нашем ASP.NET MVC 1.0 или 2 приложения мы добавим метод IsLocalUrl() AccountController, но настоятельно рекомендуется, чтобы добавить его в отдельном вспомогательном классе, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="84921-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="84921-158">Мы сделать две небольшие изменения в ASP.NET MVC 3 версию IsLocalUrl(), чтобы он будет работать внутри AccountController.</span><span class="sxs-lookup"><span data-stu-id="84921-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="84921-159">Во-первых мы изменим его из открытого метода в закрытый метод, так как открытые методы в контроллерах доступны в виде действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="84921-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="84921-160">Во-вторых мы изменим проверки узла URL-адрес для узла приложения.</span><span class="sxs-lookup"><span data-stu-id="84921-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="84921-161">Что вызов использует локальный RequestContext в класс UrlHelper.</span><span class="sxs-lookup"><span data-stu-id="84921-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="84921-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span><span class="sxs-lookup"><span data-stu-id="84921-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="84921-163">Ниже приведен измененный метод IsLocalUrl() для использования с классом контроллера в ASP.NET MVC 1.0 и 2 приложения.</span><span class="sxs-lookup"><span data-stu-id="84921-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="84921-164">**В листинге 5 – IsLocalUrl() метод, который изменяется для использования с классом контроллера MVC**</span><span class="sxs-lookup"><span data-stu-id="84921-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="84921-165">Теперь, когда метод IsLocalUrl() находится в месте, можно вызывать его из действии входа для проверки параметра returnUrl, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="84921-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="84921-166">**В листинге 6 – Updated входа, который проверяет параметр returnUrl**</span><span class="sxs-lookup"><span data-stu-id="84921-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="84921-167">Теперь мы можем протестировать атака открытое перенаправление, попытавшись выполнить вход с использованием внешних URL-адрес возврата.</span><span class="sxs-lookup"><span data-stu-id="84921-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="84921-168">Давайте используем /Account/LogOn? ReturnUrl =<http://www.bing.com/> еще раз.</span><span class="sxs-lookup"><span data-stu-id="84921-168">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="84921-169">**Рис. 04**: Тестирование обновление действия входа в систему</span><span class="sxs-lookup"><span data-stu-id="84921-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="84921-170">После успешного входа в систему, мы перенаправляются на действие контроллера Home/Index, а не внешний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="84921-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="84921-171">**05 рис**: Откройте изменило Атака перенаправления</span><span class="sxs-lookup"><span data-stu-id="84921-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="84921-172">Сводка</span><span class="sxs-lookup"><span data-stu-id="84921-172">Summary</span></span>

<span data-ttu-id="84921-173">Открытой переадресацией может произойти при перенаправлении URL-адреса передаются как параметры в URL-адрес для приложения.</span><span class="sxs-lookup"><span data-stu-id="84921-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="84921-174">ASP.NET MVC 3, шаблон включает код для защиты от откройте атак путем перенаправления.</span><span class="sxs-lookup"><span data-stu-id="84921-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="84921-175">Вы можете добавить этот код с некоторыми изменениями в ASP.NET MVC 1.0 и 2 приложения.</span><span class="sxs-lookup"><span data-stu-id="84921-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="84921-176">Для защиты от атак открытое перенаправление, при входе в ASP.NET 1.0 и 2 приложения, добавьте метод IsLocalUrl() и проверить параметр returnUrl в действии входа в систему.</span><span class="sxs-lookup"><span data-stu-id="84921-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>