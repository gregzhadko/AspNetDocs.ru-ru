---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: Вход с помощью внешних сайтов на веб-ASP.NET страниц узла (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье объясняется, как выполнить вход на сайт веб-страниц ASP.NET (Razor), с помощью Facebook, Google, Twitter, Yahoo и других сайтов, то есть, как обеспечить поддержку...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: a93835e685716b3be59023b9f84a006e38f48e89
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59380459"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="395ff-103">Вход с помощью внешних сайтов на сайте ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="395ff-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="395ff-104">по [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="395ff-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="395ff-105">В этой статье объясняется, как выполнить вход на сайт веб-страниц ASP.NET (Razor), с помощью Facebook, Google, Twitter, Yahoo и других сайтов, то есть как для поддержки OAuth и OpenID в веб-узла.</span><span class="sxs-lookup"><span data-stu-id="395ff-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="395ff-106">Вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="395ff-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="395ff-107">Выполнение входа с другого сайта, если вы используете шаблон начального сайта WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="395ff-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="395ff-108">Это функция ASP.NET, впервые представленная в этой статье:</span><span class="sxs-lookup"><span data-stu-id="395ff-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="395ff-109">`OAuthWebSecurity` Вспомогательный.</span><span class="sxs-lookup"><span data-stu-id="395ff-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="395ff-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="395ff-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="395ff-111">Веб-страниц ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="395ff-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="395ff-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="395ff-112">WebMatrix 3</span></span>

<span data-ttu-id="395ff-113">Веб-страниц ASP.NET включает в себя поддержку [OAuth](http://oauth.net/) и [OpenID](http://openid.net/) поставщиков.</span><span class="sxs-lookup"><span data-stu-id="395ff-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="395ff-114">С помощью этих поставщиков, вы можете разрешить пользователям входить на сайт, с помощью существующих учетных данных из Facebook, Twitter, Майкрософт и Google.</span><span class="sxs-lookup"><span data-stu-id="395ff-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="395ff-115">Например чтобы войти с использованием учетной записи Facebook, пользователей можно выбрать значок Facebook, который перенаправляет их на страницу входа Facebook, где они ввести учетные данные.</span><span class="sxs-lookup"><span data-stu-id="395ff-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="395ff-116">Они затем можно связать имя входа Facebook со своей учетной записью на узле.</span><span class="sxs-lookup"><span data-stu-id="395ff-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="395ff-117">Улучшение функций членства веб-страницы – что пользователи могут связать несколько попыток входа (в том числе имена входа из сетевых сообществ) с одной учетной записи на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="395ff-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="395ff-118">На этом изображении показаны на страницу входа из **начального сайта** шаблон, где пользователь может выбрать значок, Facebook, Twitter, Google или Microsoft, чтобы включить ведение журнала с помощью учетной записи внешнего:</span><span class="sxs-lookup"><span data-stu-id="395ff-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![внешних поставщиков](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="395ff-120">Вы можете включить членством, OAuth и OpenID, раскомментировав несколько строк кода в **начального сайта** шаблона.</span><span class="sxs-lookup"><span data-stu-id="395ff-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="395ff-121">Методы и свойства, которые позволяют работать с OAuth и OpenID поставщики находятся в `WebMatrix.Security.OAuthWebSecurity` класса.</span><span class="sxs-lookup"><span data-stu-id="395ff-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="395ff-122">**Начального сайта** шаблон включает инфраструктуру полнофункционального членства, дополненный страницу входа, базы данных членства и весь код, вам нужно разрешить пользователям входить на сайт, с помощью локальных учетных данных или из другого сайта .</span><span class="sxs-lookup"><span data-stu-id="395ff-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="395ff-123">В этом разделе приведен пример того, как для входа с внешних сайтов с сайтом на основе пользователей **начального сайта** шаблона.</span><span class="sxs-lookup"><span data-stu-id="395ff-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="395ff-124">После создания начального сайта, это сделать (выполните сведения):</span><span class="sxs-lookup"><span data-stu-id="395ff-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="395ff-125">Для узлов, которые используют поставщик OAuth (Facebook, Twitter и Майкрософт) создать приложение на внешний сайт.</span><span class="sxs-lookup"><span data-stu-id="395ff-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="395ff-126">Это дает ключи приложений, которая потребуется для вызова функции login для этих сайтов.</span><span class="sxs-lookup"><span data-stu-id="395ff-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="395ff-127">Для сайтов, использующих поставщик OpenID (Google) у вас нет для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="395ff-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="395ff-128">Для всех этих узлов необходимо настроить учетную запись для входа в систему и создавать приложения для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="395ff-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="395ff-129">Приложения Майкрософт принимать динамический URL-адрес для работающего веб-сайта, только в том случае, поэтому ее невозможно использовать URL-адрес локального веб-сайта для тестирования имен входа.</span><span class="sxs-lookup"><span data-stu-id="395ff-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="395ff-130">Измените несколько файлов в веб-сайта, чтобы указать поставщика проверки подлинности и для отправки имени входа на сайт, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="395ff-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="395ff-131">В этой статье приведены отдельные инструкции для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="395ff-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="395ff-132">Включение имен входа Google</span><span class="sxs-lookup"><span data-stu-id="395ff-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="395ff-133">Включение имен входа Facebook</span><span class="sxs-lookup"><span data-stu-id="395ff-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="395ff-134">Включение имен входа Twitter</span><span class="sxs-lookup"><span data-stu-id="395ff-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="395ff-135">Включение имен входа Google</span><span class="sxs-lookup"><span data-stu-id="395ff-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="395ff-136">Создайте или откройте узел веб-страниц ASP.NET, основанный на шаблоне начального сайта WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="395ff-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="395ff-137">Откройте  *\_AppStart.cshtml* странице и раскомментируйте следующую строку кода.</span><span class="sxs-lookup"><span data-stu-id="395ff-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="395ff-138">Тестирование входа Google</span><span class="sxs-lookup"><span data-stu-id="395ff-138">Testing Google login</span></span>

1. <span data-ttu-id="395ff-139">Запустите *default.cshtml* страницы веб-сайта и выберите **вход** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="395ff-140">На *входа* странице **вход с помощью другой службы** выберите либо **Google** или **Yahoo** кнопка "Отправить".</span><span class="sxs-lookup"><span data-stu-id="395ff-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="395ff-141">В этом примере используется имя входа Google.</span><span class="sxs-lookup"><span data-stu-id="395ff-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="395ff-142">Веб-страницы перенаправляет запрос на страницу входа Google.</span><span class="sxs-lookup"><span data-stu-id="395ff-142">The web page redirects the request to the Google login page.</span></span>

    ![Вход Google](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="395ff-144">Введите учетные данные для существующей учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="395ff-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="395ff-145">Если Google спрашивает, хотите ли вы разрешить *Localhost* использовать информацию из учетной записи, нажмите кнопку **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="395ff-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="395ff-146">Код использует маркер Google для проверки подлинности пользователя и возвращает на эту страницу на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="395ff-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="395ff-147">Эта страница позволяет связать их имени для входа Google с существующей учетной записи на веб-сайте, или они могут зарегистрировать новую учетную запись на сайте, чтобы связать внешней учетной записи с.</span><span class="sxs-lookup"><span data-stu-id="395ff-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="395ff-149">Выберите **связать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-149">Choose the **Associate** button.</span></span> <span data-ttu-id="395ff-150">Браузер возвращается на домашнюю страницу приложения.</span><span class="sxs-lookup"><span data-stu-id="395ff-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="395ff-151">Включение имен входа Facebook</span><span class="sxs-lookup"><span data-stu-id="395ff-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="395ff-152">Перейдите к [сайт разработчиков Facebook](https://developers.facebook.com/apps) (вход, если вы еще не вошли).</span><span class="sxs-lookup"><span data-stu-id="395ff-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="395ff-153">Выберите **создать новое приложение** кнопку, а затем следуйте инструкциям на экране, чтобы задать имя и создать новое приложение.</span><span class="sxs-lookup"><span data-stu-id="395ff-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="395ff-154">В разделе **выберите, каким образом ваше приложение будет интегрировано с Facebook**, выберите **веб-сайт** раздел.</span><span class="sxs-lookup"><span data-stu-id="395ff-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="395ff-155">Заполните **URL-адрес сайта** с URL-адрес веб-сайта (например, `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="395ff-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="395ff-156">**Домена** поле является необязательным; это можно использовать для проверки подлинности для всего домена (такие как *example.com*).</span><span class="sxs-lookup"><span data-stu-id="395ff-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="395ff-157">При запуске на локальном компьютере с URL-адрес сайта, такие как `http://localhost:12345` (где номер является номером локального порта), можно добавить это значение, чтобы **URL-адрес сайта** для тестирования веб-узла.</span><span class="sxs-lookup"><span data-stu-id="395ff-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="395ff-158">Тем не менее, номер порта изменений локального сайта в любое время, вам потребуется обновить **URL-адрес сайта** поле приложения.</span><span class="sxs-lookup"><span data-stu-id="395ff-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="395ff-159">Выберите **сохранить изменения** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="395ff-160">Выберите **приложений** снова откройте вкладку, а затем просмотрите начальной страницы в приложении.</span><span class="sxs-lookup"><span data-stu-id="395ff-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="395ff-161">Копировать **идентификатор приложения** и **секрет приложения** значения для вашего приложения и вставьте их в текстовый временный файл.</span><span class="sxs-lookup"><span data-stu-id="395ff-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="395ff-162">Эти значения к поставщику Facebook передаст в код веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="395ff-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="395ff-163">Выйдите из сайта разработчика Facebook.</span><span class="sxs-lookup"><span data-stu-id="395ff-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="395ff-164">Теперь вы внести изменения две страницы в веб-сайта, чтобы пользователи будут возможность войти на сайт, используя учетные записи Facebook.</span><span class="sxs-lookup"><span data-stu-id="395ff-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="395ff-165">Создайте или откройте узел веб-страниц ASP.NET, основанный на шаблоне начального сайта WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="395ff-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="395ff-166">Откройте  *\_AppStart.cshtml* странице и раскомментируйте код для поставщика Facebook OAuth.</span><span class="sxs-lookup"><span data-stu-id="395ff-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="395ff-167">Блок кода Раскомментировать области кода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="395ff-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="395ff-168">Копировать **идентификатор приложения** значение из приложения Facebook в качестве значения `appId` параметра (внутри кавычек).</span><span class="sxs-lookup"><span data-stu-id="395ff-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="395ff-169">Копировать **секрет приложения** значение из приложения Facebook в качестве `appSecret` значение параметра.</span><span class="sxs-lookup"><span data-stu-id="395ff-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="395ff-170">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="395ff-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="395ff-171">Тестирование входа в Facebook</span><span class="sxs-lookup"><span data-stu-id="395ff-171">Testing Facebook login</span></span>

1. <span data-ttu-id="395ff-172">Запустите веб-узла *default.cshtml* странице и выбрать **входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="395ff-173">На *входа* странице **вход с помощью другой службы** выберите **Facebook** значок.</span><span class="sxs-lookup"><span data-stu-id="395ff-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="395ff-174">Веб-страницы перенаправляет запрос на страницу входа в Facebook.</span><span class="sxs-lookup"><span data-stu-id="395ff-174">The web page redirects the request to the Facebook login page.</span></span>

    ![OAuth 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="395ff-176">Войдите в учетную запись Facebook.</span><span class="sxs-lookup"><span data-stu-id="395ff-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="395ff-177">Код использует маркер Facebook для проверки подлинности и затем возвращается на страницу, где можно связать имя входа Facebook с именем входа веб сайта.</span><span class="sxs-lookup"><span data-stu-id="395ff-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="395ff-178">Адрес имя или адрес электронной почты пользователя заполняется в **электронной почты** поле в форме.</span><span class="sxs-lookup"><span data-stu-id="395ff-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="395ff-180">Выберите **связать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="395ff-181">Браузер возвращается на домашнюю страницу, и вы вошли.</span><span class="sxs-lookup"><span data-stu-id="395ff-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="395ff-182">Включение имен входа Twitter</span><span class="sxs-lookup"><span data-stu-id="395ff-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="395ff-183">Перейдите к [сайте разработчиков Twitter](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="395ff-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="395ff-184">Выберите **Создание приложения** ссылку и затем войти на сайт.</span><span class="sxs-lookup"><span data-stu-id="395ff-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="395ff-185">На **создать приложение** форме, заполните **имя** и **описание** поля.</span><span class="sxs-lookup"><span data-stu-id="395ff-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="395ff-186">В **веб-сайт** введите URL-адрес веб-сайта (например, `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="395ff-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="395ff-187">Если вы тестируете свой сайт локально (с помощью URL-адресу вида `http://localhost:12345`), URL-адрес может не поддерживать в Twitter.</span><span class="sxs-lookup"><span data-stu-id="395ff-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="395ff-188">Тем не менее, можно использовать локальный петлевой IP-адрес (например `http://127.0.0.1:12345`).</span><span class="sxs-lookup"><span data-stu-id="395ff-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="395ff-189">Это упрощает процесс тестирования приложения локально.</span><span class="sxs-lookup"><span data-stu-id="395ff-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="395ff-190">Тем не менее, при каждом изменении номер порта на локальный сайт, вам потребуется обновить **веб-сайт** поле приложения.</span><span class="sxs-lookup"><span data-stu-id="395ff-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="395ff-191">В **URL-адрес обратного вызова** введите URL-адрес для страницы в веб-сайта, нужно вернуться после входа в Twitter.</span><span class="sxs-lookup"><span data-stu-id="395ff-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="395ff-192">Например, чтобы отправить пользователей на домашнюю страницу сайта Starter (который будет распознавать их состояние вошедшего в систему), введите же URL-адрес, введенный в **веб-сайт** поля.</span><span class="sxs-lookup"><span data-stu-id="395ff-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="395ff-193">Примите условия и выберите **создать приложение Twitter** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="395ff-194">На **Мои приложения** целевой страницы, выберите созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="395ff-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="395ff-195">На **сведения** вкладке, прокрутите вниз и выберите пункт **создать My Access Token** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="395ff-196">На **сведения** вкладке, скопируйте **ключ потребителя** и **секретный ключ потребителя** значения для вашего приложения и вставьте их в текстовый временный файл.</span><span class="sxs-lookup"><span data-stu-id="395ff-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="395ff-197">Вы передадите эти значения к поставщику Twitter в коде веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="395ff-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="395ff-198">Выход на сайте Twitter.</span><span class="sxs-lookup"><span data-stu-id="395ff-198">Exit the Twitter site.</span></span>

<span data-ttu-id="395ff-199">Теперь можно внести изменения две страницы в веб-сайта таким образом, пользователи смогут войти на сайт, с помощью учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="395ff-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="395ff-200">Создайте или откройте узел веб-страниц ASP.NET, основанный на шаблоне начального сайта WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="395ff-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="395ff-201">Откройте  *\_AppStart.cshtml* странице и раскомментируйте код для поставщика Twitter OAuth.</span><span class="sxs-lookup"><span data-stu-id="395ff-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="395ff-202">Блок кода Раскомментировать области кода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="395ff-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="395ff-203">Копировать **ключ потребителя** значение из приложения Twitter для параметра `consumerKey` параметр (внутри кавычек).</span><span class="sxs-lookup"><span data-stu-id="395ff-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="395ff-204">Копировать **секретный ключ потребителя** значение из приложения Twitter для параметра `consumerSecret` параметр.</span><span class="sxs-lookup"><span data-stu-id="395ff-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="395ff-205">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="395ff-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="395ff-206">Тестирование входа в Twitter</span><span class="sxs-lookup"><span data-stu-id="395ff-206">Testing Twitter login</span></span>

1. <span data-ttu-id="395ff-207">Запустите *default.cshtml* страницы веб-сайта и выберите **входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="395ff-208">На *входа* странице **вход с помощью другой службы** выберите **Twitter** значок.</span><span class="sxs-lookup"><span data-stu-id="395ff-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="395ff-209">Веб-страницы перенаправляет запрос на страницу входа Twitter для приложения, которое вы создали.</span><span class="sxs-lookup"><span data-stu-id="395ff-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![OAuth — 4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="395ff-211">Войдите в учетную запись Twitter.</span><span class="sxs-lookup"><span data-stu-id="395ff-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="395ff-212">Код использует маркер Twitter для проверки подлинности пользователя и последующий возврат к странице где можно связать имя входа с учетной записью веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="395ff-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="395ff-213">Имя или адрес электронной почты адрес заполняется в **электронной почты** поле в форме.</span><span class="sxs-lookup"><span data-stu-id="395ff-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="395ff-215">Выберите **связать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="395ff-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="395ff-216">Браузер возвращается на домашнюю страницу, и вы вошли.</span><span class="sxs-lookup"><span data-stu-id="395ff-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="395ff-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="395ff-217">Additional Resources</span></span>


- [<span data-ttu-id="395ff-218">Настройка поведения в масштабах сайта</span><span class="sxs-lookup"><span data-stu-id="395ff-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="395ff-219">Добавление безопасности и членства ASP.NET веб-узел страницы</span><span class="sxs-lookup"><span data-stu-id="395ff-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
