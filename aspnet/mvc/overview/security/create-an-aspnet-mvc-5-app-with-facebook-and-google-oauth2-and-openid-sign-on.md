---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Создайте приложение MVC 5 с помощью Facebook, Twitter, LinkedIn и Google OAuth2 Всхейно (C) Документы Майкрософт
author: Rick-Anderson
description: Этот учебник показывает вам, как построить ASP.NET MVC 5 веб-приложение, которое позволяет пользователям войти в систему с помощью OAuth 2.0 с полномочиями от внешнего authenti ...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675919"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="21559-103">Создание приложения ASP.NET MVC 5 с единым входом с помощью учетных данных Facebook, Twitter, LinkedIn и Google OAuth2 (C#)</span><span class="sxs-lookup"><span data-stu-id="21559-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="21559-104">[Рик Андерсон](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="21559-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="21559-105">В этом учебнике показано, как создать веб-приложение mVC 5 ASP.NET, которое позволяет пользователям войти в систему с помощью [OAuth 2.0](http://oauth.net/2/) с учетными данными от внешнего поставщика аутентификации, таких как Facebook, Twitter, LinkedIn, Microsoft или Google.</span><span class="sxs-lookup"><span data-stu-id="21559-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="21559-106">Для простоты, этот учебник фокусируется на работе с учетными данными от Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="21559-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="21559-107">Включение этих учетных данных на веб-сайты обеспечивает значительное преимущество, поскольку миллионы пользователей уже имеют учетные записи с этими внешними поставщиками.</span><span class="sxs-lookup"><span data-stu-id="21559-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="21559-108">Эти пользователи могут быть более склонны подписаться на ваш сайт, если они не должны создавать и запоминать новый набор учетных данных.</span><span class="sxs-lookup"><span data-stu-id="21559-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="21559-109">Смотрите также [ASP.NET приложение MVC 5 с SMS и электронной почте Двухфакторная аутентификация](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="21559-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="21559-110">В учебнике также показано, как добавлять данные профиля для пользователя и как использовать API членства для добавления ролей.</span><span class="sxs-lookup"><span data-stu-id="21559-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="21559-111">Этот учебник был написан [Рик Андерсон](https://blogs.msdn.com/rickAndy) ( [@RickAndMSFT](https://twitter.com/RickAndMSFT) Пожалуйста, следуйте за мной по щебетать: ).</span><span class="sxs-lookup"><span data-stu-id="21559-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="21559-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="21559-112">Getting Started</span></span>

<span data-ttu-id="21559-113">Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="21559-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="21559-114">Установите Visual Studio [2013 Обновление 3](https://go.microsoft.com/fwlink/?LinkId=390521) или выше.</span><span class="sxs-lookup"><span data-stu-id="21559-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="21559-115">Для помощи с Dropbox, GitHub, Linkedin, Instagram, Буфер, Salesforce, STEAM, Стек Exchange, Tripit, Twitch, Twitter, Yahoo!, и многое другое, смотрите этот [пример проекта](https://github.com/matthewdunsdon/oauthforaspnet).</span><span class="sxs-lookup"><span data-stu-id="21559-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="21559-116">Вы должны установить Visual Studio [2013 Обновление 3](https://go.microsoft.com/fwlink/?LinkId=390521) или выше, чтобы использовать Google OAuth 2 и отладить локально без SSL предупреждений.</span><span class="sxs-lookup"><span data-stu-id="21559-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="21559-117">Нажмите **Новый проект** со **стартовой** страницы, или вы можете использовать меню и выбрать **файл,** а затем **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="21559-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="21559-118">Создание первого приложения</span><span class="sxs-lookup"><span data-stu-id="21559-118">Creating Your First Application</span></span>

<span data-ttu-id="21559-119">Нажмите **Новый проект**, затем выберите **Visual C "** слева, затем **веб,а** затем выберите **ASP.NET веб-приложений**.</span><span class="sxs-lookup"><span data-stu-id="21559-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="21559-120">Назовите свой проект "MvcAuth", а затем нажмите **OK**.</span><span class="sxs-lookup"><span data-stu-id="21559-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="21559-121">В диалоге **проекта New ASP.NET** щелкните **MVC**.</span><span class="sxs-lookup"><span data-stu-id="21559-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="21559-122">Если проверка подлинности не является **индивидуальными учетными записями пользователей,** нажмите кнопку **«Изменение аутентификации»** и выберите **индивидуальные учетные записи пользователей.**</span><span class="sxs-lookup"><span data-stu-id="21559-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="21559-123">Проверяя **host в облаке,** приложение будет очень легко разместить в Azure.</span><span class="sxs-lookup"><span data-stu-id="21559-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="21559-124">Если вы выбрали **Host в облаке,** заполните диалог настройки.</span><span class="sxs-lookup"><span data-stu-id="21559-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="21559-125">Используйте NuGet для обновления до последних программ OWIN</span><span class="sxs-lookup"><span data-stu-id="21559-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="21559-126">Используйте менеджер пакетов NuGet для обновления [промежуточного посуды OWIN.](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)</span><span class="sxs-lookup"><span data-stu-id="21559-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="21559-127">Выберите **обновления** в левом меню.</span><span class="sxs-lookup"><span data-stu-id="21559-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="21559-128">Вы можете нажать на кнопку **Обновление Все** или вы можете искать только пакеты OWIN (показано на следующем изображении):</span><span class="sxs-lookup"><span data-stu-id="21559-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="21559-129">На рисунке ниже показаны только пакеты OWIN:</span><span class="sxs-lookup"><span data-stu-id="21559-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="21559-130">С консоли менеджера пакетов (PMC) можно ввести `Update-Package` команду, которая будет обновлять все пакеты.</span><span class="sxs-lookup"><span data-stu-id="21559-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="21559-131">Нажмите **F5** или **Ctrl-F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="21559-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="21559-132">На рисунке ниже номер порта 1234.</span><span class="sxs-lookup"><span data-stu-id="21559-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="21559-133">При запуске приложения вы увидите другой номер порта.</span><span class="sxs-lookup"><span data-stu-id="21559-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="21559-134">В зависимости от размера окна браузера, возможно, потребуется нажать значок навигации, чтобы увидеть **"Дом",** **"Контакт",** **Contact** **"Регистрация"** и **"Вход в** ссылки".</span><span class="sxs-lookup"><span data-stu-id="21559-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="21559-135">Настройка SSL в проекте</span><span class="sxs-lookup"><span data-stu-id="21559-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="21559-136">Чтобы подключиться к поставщикам аутентификации, таким как Google и Facebook, необходимо настроить IIS-Express для использования SSL.</span><span class="sxs-lookup"><span data-stu-id="21559-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="21559-137">Важно продолжать использовать SSL после входа и не возвращаться к HTTP, ваш файл cookie-файлов является таким же секретным, как и ваше имя пользователя и пароль, и без использования SSL вы отправляете его в ясном тексте по проводу.</span><span class="sxs-lookup"><span data-stu-id="21559-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="21559-138">Кроме того, вы уже взяли время для выполнения рукопожатия и обеспечения безопасности канала (который является основной частью того, что делает HTTPS медленнее, чем HTTP) до запуска конвейера MVC, поэтому перенаправление обратно в HTTP после ввоза в систему не сделает текущий запрос или будущие запросы гораздо быстрее.</span><span class="sxs-lookup"><span data-stu-id="21559-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="21559-139">В **Solution Explorer**щелкните проект **MvcAuth.**</span><span class="sxs-lookup"><span data-stu-id="21559-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="21559-140">Нажмите на ключ F4, чтобы показать свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="21559-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="21559-141">Кроме того, из меню **View** вы можете выбрать **окно свойств.**</span><span class="sxs-lookup"><span data-stu-id="21559-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="21559-142">Изменение **SSL позволило** true.</span><span class="sxs-lookup"><span data-stu-id="21559-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="21559-143">Копирование URL SSL (который будет, `https://localhost:44300/` если вы не создали другие проекты SSL).</span><span class="sxs-lookup"><span data-stu-id="21559-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="21559-144">В **Solution Explorer**, право нажмите на проект **MvcAuth** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="21559-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="21559-145">Выберите **web-вкладку,** а затем вставьте URL SSL в поле **Project Url.**</span><span class="sxs-lookup"><span data-stu-id="21559-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="21559-146">Сохранить файл (Ctl-S).</span><span class="sxs-lookup"><span data-stu-id="21559-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="21559-147">Этот URL-адрес необходим для настройки приложений для проверки подлинности Facebook и Google.</span><span class="sxs-lookup"><span data-stu-id="21559-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="21559-148">Добавьте атрибут [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) в `Home` контроллер, требующий, чтобы все запросы должны использовать HTTPS.</span><span class="sxs-lookup"><span data-stu-id="21559-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="21559-149">Более безопасный подход заключается в добавлении фильтра [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) в приложение.</span><span class="sxs-lookup"><span data-stu-id="21559-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="21559-150">Смотрите раздел &quot;Защита приложения с SSL и&quot; Авторизовать атрибут в моем учебнике [Создать ASP.NET mVC приложение с auth и S'L DB и развернуть в Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="21559-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="21559-151">Ниже показана часть контроллера Home.</span><span class="sxs-lookup"><span data-stu-id="21559-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="21559-152">Для запуска приложения нажмите сочетание клавиш CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="21559-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="21559-153">Если вы установили сертификат в прошлом, вы можете пропустить остальную часть этого раздела и перейти к [созданию приложения Google для OAuth 2 и подключения приложения к проекту](#goog), в противном случае, следуйте инструкциям доверять самостоятельно подписанному сертификату, который iIS Express создал.</span><span class="sxs-lookup"><span data-stu-id="21559-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="21559-154">Прочитайте диалог **предупреждения о безопасности,** а затем нажмите **«Да»,** если вы хотите установить сертификат, представляющий localhost.</span><span class="sxs-lookup"><span data-stu-id="21559-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="21559-155">В IE откроется *Главная* страница без предупреждений SSL.</span><span class="sxs-lookup"><span data-stu-id="21559-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="21559-156">Google Chrome также принимает сертификат и будет показывать содержимое HTTPS без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="21559-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="21559-157">Firefox использует свой собственный магазин сертификатов, поэтому он будет отображать предупреждение.</span><span class="sxs-lookup"><span data-stu-id="21559-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="21559-158">Для нашего приложения вы можете безопасно нажать **Я понимаю риски**.</span><span class="sxs-lookup"><span data-stu-id="21559-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="21559-159">Создание приложения Google для OAuth 2 и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="21559-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="21559-160">Для текущих инструкций Google OAuth [см. Настройка аутентификации Google в ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="21559-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="21559-161">Перейдите к [Консоли разработчиков Google](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="21559-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="21559-162">Если вы еще не создали проект раньше, выберите **учетные данные** в левой вкладке, а затем выберите **Создать.**</span><span class="sxs-lookup"><span data-stu-id="21559-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="21559-163">В левой вкладке нажмите **«Удостоверения».**</span><span class="sxs-lookup"><span data-stu-id="21559-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="21559-164">Нажмите **Создать учетные данные,** то **OAuth идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="21559-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="21559-165">В диалоге **«Создать идентификатор клиента»** сохраните **web-приложение** по умолчанию для типа приложения.</span><span class="sxs-lookup"><span data-stu-id="21559-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="21559-166">Установите **авторизованные** истоки JavaScript на URL`https://localhost:44300/` SSL, который вы использовали выше (если вы не создали другие SSL-проекты)</span><span class="sxs-lookup"><span data-stu-id="21559-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="21559-167">Установите **авторизованный перенаправить URI** на:</span><span class="sxs-lookup"><span data-stu-id="21559-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="21559-168">Нажмите на пункт меню экрана OAuth Consent, а затем установите адрес электронной почты и название продукта.</span><span class="sxs-lookup"><span data-stu-id="21559-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="21559-169">При заполнении формы нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="21559-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="21559-170">Нажмите на элемент меню библиотеки, поиск **Google ' API**, нажмите на него, а затем нажмите Включить.</span><span class="sxs-lookup"><span data-stu-id="21559-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="21559-171">На рисунке ниже показаны включенные AIS.</span><span class="sxs-lookup"><span data-stu-id="21559-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="21559-172">С помощью API-менеджера Google API посетите вкладку **Credentials** для получения **идентификатора клиента.**</span><span class="sxs-lookup"><span data-stu-id="21559-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="21559-173">Скачать, чтобы сохранить файл JSON с секретами приложения.</span><span class="sxs-lookup"><span data-stu-id="21559-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="21559-174">Копируйте и вставьте **ClientId** и `UseGoogleAuthentication` **ClientSecret** в *метод,* найденный в Startup.Auth.cs файле в *папке App_Start.*</span><span class="sxs-lookup"><span data-stu-id="21559-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="21559-175">Значения **ClientId** и **ClientSecret,** приведенные ниже, являются образцами и не работают.</span><span class="sxs-lookup"><span data-stu-id="21559-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="21559-176">Безопасность - Никогда не храните конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="21559-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="21559-177">Учетная запись и учетные данные добавляются в приведенный выше код, чтобы сохранить образец простым.</span><span class="sxs-lookup"><span data-stu-id="21559-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="21559-178">[Ознакомьтесь с рекомендациями по развертыванию паролей и других конфиденциальных данных в ASP.NET и службе приложений Azure.](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)</span><span class="sxs-lookup"><span data-stu-id="21559-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="21559-179">Нажмите **на CTRL-F5,** чтобы построить и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="21559-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="21559-180">Щелкните ссылку **Войти в систему** .</span><span class="sxs-lookup"><span data-stu-id="21559-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="21559-181">Под **использованием другой службы для входа в систему,** нажмите **Google**.</span><span class="sxs-lookup"><span data-stu-id="21559-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="21559-182">Если вы пропустите любой из вышеперечисленных шагов, вы получите ошибку HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="21559-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="21559-183">Перепроверьте свои шаги выше.</span><span class="sxs-lookup"><span data-stu-id="21559-183">Recheck your steps above.</span></span> <span data-ttu-id="21559-184">Если вы пропустили требуемый параметр (например, **название продукта),** добавьте недостающий элемент и сохраните; проверка подлинности может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="21559-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="21559-185">Вы будете перенаправлены на сайт Google, где вы введете свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="21559-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="21559-186">После ввода учетных данных появится запрос на получение разрешений для веб-приложения, которое было только что создано: </span><span class="sxs-lookup"><span data-stu-id="21559-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="21559-187">Нажмите **Принять**.</span><span class="sxs-lookup"><span data-stu-id="21559-187">Click **Accept**.</span></span> <span data-ttu-id="21559-188">Теперь вы будете перенаправлены обратно на страницу **Регистрации** приложения MvcAuth, где вы можете зарегистрировать свою учетную запись Google.</span><span class="sxs-lookup"><span data-stu-id="21559-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="21559-189">У вас есть возможность изменить локальное имя регистрации электронной почты, используемое для вашей учетной записи Gmail, но вы, как правило, хотите сохранить псевдоним электронной почты по умолчанию (то есть тот, который вы использовали для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="21559-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="21559-190">Щелкните **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="21559-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="21559-191">Создание приложения в Facebook и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="21559-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="21559-192">Для текущих инструкций по аутентификации Facebook OAuth2 [см.](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="21559-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="21559-193">Изучение данных о членстве</span><span class="sxs-lookup"><span data-stu-id="21559-193">Examine the Membership Data</span></span>

<span data-ttu-id="21559-194">В меню **View** нажмите **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="21559-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="21559-195">Расширить **defaultConnection (MvcAuth),** расширить **таблицы**, нажмите право **aspNetUsers** и нажмите **Показать таблицы данных**.</span><span class="sxs-lookup"><span data-stu-id="21559-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![таблицы aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="21559-197">Добавление данных профиля в класс пользователя</span><span class="sxs-lookup"><span data-stu-id="21559-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="21559-198">В этом разделе вы добавите дату рождения и родной город к данным пользователя во время регистрации, как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="21559-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![рег с родным городом и Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="21559-200">Откройте файл *Модели-IdentityModels.cs* и добавьте дату рождения и свойства родного города:</span><span class="sxs-lookup"><span data-stu-id="21559-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="21559-201">Откройте файл *Модели-AccountViewModels.cs* и установленную дату `ExternalLoginConfirmationViewModel`рождения и недвижимость в родном городе.</span><span class="sxs-lookup"><span data-stu-id="21559-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="21559-202">Откройте файл *Controllers-AccountController.cs* и добавьте код для `ExternalLoginConfirmation` даты рождения и родного города в методе действия, как показано на рисунке:</span><span class="sxs-lookup"><span data-stu-id="21559-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="21559-203">Добавить дату рождения и родной город в файл *Views-Account-ExternalLoginConfirmation.cshtml:*</span><span class="sxs-lookup"><span data-stu-id="21559-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="21559-204">Удалите базу данных о членстве, чтобы вы могли снова зарегистрировать свою учетную запись Facebook с вашим приложением и проверить, что вы можете добавить новую дату рождения и информацию профиля родного города.</span><span class="sxs-lookup"><span data-stu-id="21559-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="21559-205">От **разрешения Explorer**, нажмите Показать все **файлы** значок, а затем нажмите нажмите *Нажмите Добавить\_Data'aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* и нажмите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="21559-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="21559-206">Из меню **Инструменты,** нажмите **NuGet пакет яслях**, а затем нажмите **пакет менеджер консоли** (PMC).</span><span class="sxs-lookup"><span data-stu-id="21559-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="21559-207">Введите следующие команды в PMC.</span><span class="sxs-lookup"><span data-stu-id="21559-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="21559-208">Включение-миграция</span><span class="sxs-lookup"><span data-stu-id="21559-208">Enable-Migrations</span></span>
2. <span data-ttu-id="21559-209">Адди-Миграция Init</span><span class="sxs-lookup"><span data-stu-id="21559-209">Add-Migration Init</span></span>
3. <span data-ttu-id="21559-210">Обновление-База данных</span><span class="sxs-lookup"><span data-stu-id="21559-210">Update-Database</span></span>

<span data-ttu-id="21559-211">Запустите приложение и используйте FaceBook и Google для входа и регистрации некоторых пользователей.</span><span class="sxs-lookup"><span data-stu-id="21559-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="21559-212">Изучение данных о членстве</span><span class="sxs-lookup"><span data-stu-id="21559-212">Examine the Membership Data</span></span>

<span data-ttu-id="21559-213">В меню **View** нажмите **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="21559-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="21559-214">Право нажмите **AspNetUsers** и нажмите **Показать Таблица данных**.</span><span class="sxs-lookup"><span data-stu-id="21559-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="21559-215">Поля `HomeTown` `BirthDate` и поля показаны ниже.</span><span class="sxs-lookup"><span data-stu-id="21559-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="21559-216">Запись вашего приложения и регистрация с другой учетной записью</span><span class="sxs-lookup"><span data-stu-id="21559-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="21559-217">Если вы входите в приложение с Facebook, а затем выходите из системы и попытаетесь войти снова с другой учетной записью Facebook (с помощью того же браузера), вы будете немедленно войти в предыдущий аккаунт Facebook, который вы использовали.</span><span class="sxs-lookup"><span data-stu-id="21559-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="21559-218">Для того, чтобы использовать другую учетную запись, вам нужно перейти на Facebook и выйти на Facebook.</span><span class="sxs-lookup"><span data-stu-id="21559-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="21559-219">То же правило применяется к любому другому поставщику аутентификации сторон.</span><span class="sxs-lookup"><span data-stu-id="21559-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="21559-220">Кроме того, вы можете войти в систему с другой учетной записью с помощью другого браузера.</span><span class="sxs-lookup"><span data-stu-id="21559-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21559-221">Next Steps</span><span class="sxs-lookup"><span data-stu-id="21559-221">Next Steps</span></span>

<span data-ttu-id="21559-222">Смотрите [Представляя Yahoo и LinkedIn OAuth поставщиков безопасности для OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Джерри Пелсер для Yahoo и LinkedIn инструкции.</span><span class="sxs-lookup"><span data-stu-id="21559-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="21559-223">Смотрите кнопки входа в социальную систему Jerrie's Pretty для ASP.NET MVC 5, чтобы включить кнопки социального входа.</span><span class="sxs-lookup"><span data-stu-id="21559-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="21559-224">Следуйте [моему учебнику Создайте приложение mVC ASP.NET с auth и S'L DB и разместите в Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), который продолжает этот учебник и показывает следующее:</span><span class="sxs-lookup"><span data-stu-id="21559-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="21559-225">Как развернуть приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="21559-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="21559-226">Как обезопасить приложение ролями.</span><span class="sxs-lookup"><span data-stu-id="21559-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="21559-227">Как обезопасить приложение с помощью [фильтров RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) и [разрешить его.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="21559-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="21559-228">Как использовать API членства для добавления пользователей и ролей.</span><span class="sxs-lookup"><span data-stu-id="21559-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="21559-229">Пожалуйста, оставьте отзыв о том, как вам понравился этот учебник и что мы могли бы улучшить.</span><span class="sxs-lookup"><span data-stu-id="21559-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="21559-230">Вы также можете запросить новые темы на [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="21559-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="21559-231">Вы даже можете попросить и проголосовать за новые функции, которые будут добавлены в ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="21559-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="21559-232">Например, можно проголосовать за инструмент [для создания и управления пользователями и ролями.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="21559-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="21559-233">Для получения хорошего объяснения того, как работают службы [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services)внешней аутентификации ASP.NET, см.</span><span class="sxs-lookup"><span data-stu-id="21559-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="21559-234">Статья Роберта также подробно описывается в возможности проверки подлинности Microsoft и Twitter.</span><span class="sxs-lookup"><span data-stu-id="21559-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="21559-235">Отличный учебник Tom Dykstra [EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) показывает, как работать с Рамочной системой entity.</span><span class="sxs-lookup"><span data-stu-id="21559-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
