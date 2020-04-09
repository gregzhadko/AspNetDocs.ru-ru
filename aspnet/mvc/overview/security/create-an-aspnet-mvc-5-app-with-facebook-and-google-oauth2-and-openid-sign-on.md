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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Создание приложения ASP.NET MVC 5 с единым входом с помощью учетных данных Facebook, Twitter, LinkedIn и Google OAuth2 (C#)

[Рик Андерсон](https://twitter.com/RickAndMSFT)

> В этом учебнике показано, как создать веб-приложение mVC 5 ASP.NET, которое позволяет пользователям войти в систему с помощью [OAuth 2.0](http://oauth.net/2/) с учетными данными от внешнего поставщика аутентификации, таких как Facebook, Twitter, LinkedIn, Microsoft или Google. Для простоты, этот учебник фокусируется на работе с учетными данными от Facebook и Google.
> 
> Включение этих учетных данных на веб-сайты обеспечивает значительное преимущество, поскольку миллионы пользователей уже имеют учетные записи с этими внешними поставщиками. Эти пользователи могут быть более склонны подписаться на ваш сайт, если они не должны создавать и запоминать новый набор учетных данных.
> 
> Смотрите также [ASP.NET приложение MVC 5 с SMS и электронной почте Двухфакторная аутентификация](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).
> 
> В учебнике также показано, как добавлять данные профиля для пользователя и как использовать API членства для добавления ролей. Этот учебник был написан [Рик Андерсон](https://blogs.msdn.com/rickAndy) ( [@RickAndMSFT](https://twitter.com/RickAndMSFT) Пожалуйста, следуйте за мной по щебетать: ).

<a id="start"></a>
## <a name="getting-started"></a>Приступая к работе

Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566). Установите Visual Studio [2013 Обновление 3](https://go.microsoft.com/fwlink/?LinkId=390521) или выше. Для помощи с Dropbox, GitHub, Linkedin, Instagram, Буфер, Salesforce, STEAM, Стек Exchange, Tripit, Twitch, Twitter, Yahoo!, и многое другое, смотрите этот [пример проекта](https://github.com/matthewdunsdon/oauthforaspnet).

> [!NOTE]
> Вы должны установить Visual Studio [2013 Обновление 3](https://go.microsoft.com/fwlink/?LinkId=390521) или выше, чтобы использовать Google OAuth 2 и отладить локально без SSL предупреждений.

Нажмите **Новый проект** со **стартовой** страницы, или вы можете использовать меню и выбрать **файл,** а затем **новый проект**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Создание первого приложения

Нажмите **Новый проект**, затем выберите **Visual C "** слева, затем **веб,а** затем выберите **ASP.NET веб-приложений**. Назовите свой проект "MvcAuth", а затем нажмите **OK**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

В диалоге **проекта New ASP.NET** щелкните **MVC**. Если проверка подлинности не является **индивидуальными учетными записями пользователей,** нажмите кнопку **«Изменение аутентификации»** и выберите **индивидуальные учетные записи пользователей.** Проверяя **host в облаке,** приложение будет очень легко разместить в Azure.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

Если вы выбрали **Host в облаке,** заполните диалог настройки.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>Используйте NuGet для обновления до последних программ OWIN

Используйте менеджер пакетов NuGet для обновления [промежуточного посуды OWIN.](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md) Выберите **обновления** в левом меню. Вы можете нажать на кнопку **Обновление Все** или вы можете искать только пакеты OWIN (показано на следующем изображении):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

На рисунке ниже показаны только пакеты OWIN:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

С консоли менеджера пакетов (PMC) можно ввести `Update-Package` команду, которая будет обновлять все пакеты.

Нажмите **F5** или **Ctrl-F5** для запуска приложения. На рисунке ниже номер порта 1234. При запуске приложения вы увидите другой номер порта.

В зависимости от размера окна браузера, возможно, потребуется нажать значок навигации, чтобы увидеть **"Дом",** **"Контакт",** **Contact** **"Регистрация"** и **"Вход в** ссылки".

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Настройка SSL в проекте

Чтобы подключиться к поставщикам аутентификации, таким как Google и Facebook, необходимо настроить IIS-Express для использования SSL. Важно продолжать использовать SSL после входа и не возвращаться к HTTP, ваш файл cookie-файлов является таким же секретным, как и ваше имя пользователя и пароль, и без использования SSL вы отправляете его в ясном тексте по проводу. Кроме того, вы уже взяли время для выполнения рукопожатия и обеспечения безопасности канала (который является основной частью того, что делает HTTPS медленнее, чем HTTP) до запуска конвейера MVC, поэтому перенаправление обратно в HTTP после ввоза в систему не сделает текущий запрос или будущие запросы гораздо быстрее.

1. В **Solution Explorer**щелкните проект **MvcAuth.**
2. Нажмите на ключ F4, чтобы показать свойства проекта. Кроме того, из меню **View** вы можете выбрать **окно свойств.**
3. Изменение **SSL позволило** true.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. Копирование URL SSL (который будет, `https://localhost:44300/` если вы не создали другие проекты SSL).
5. В **Solution Explorer**, право нажмите на проект **MvcAuth** и выберите **Свойства**.
6. Выберите **web-вкладку,** а затем вставьте URL SSL в поле **Project Url.** Сохранить файл (Ctl-S). Этот URL-адрес необходим для настройки приложений для проверки подлинности Facebook и Google.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Добавьте атрибут [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) в `Home` контроллер, требующий, чтобы все запросы должны использовать HTTPS. Более безопасный подход заключается в добавлении фильтра [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) в приложение. Смотрите раздел &quot;Защита приложения с SSL и&quot; Авторизовать атрибут в моем учебнике [Создать ASP.NET mVC приложение с auth и S'L DB и развернуть в Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Ниже показана часть контроллера Home.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Для запуска приложения нажмите сочетание клавиш CTRL+F5. Если вы установили сертификат в прошлом, вы можете пропустить остальную часть этого раздела и перейти к [созданию приложения Google для OAuth 2 и подключения приложения к проекту](#goog), в противном случае, следуйте инструкциям доверять самостоятельно подписанному сертификату, который iIS Express создал.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Прочитайте диалог **предупреждения о безопасности,** а затем нажмите **«Да»,** если вы хотите установить сертификат, представляющий localhost.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. В IE откроется *Главная* страница без предупреждений SSL.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome также принимает сертификат и будет показывать содержимое HTTPS без предупреждения. Firefox использует свой собственный магазин сертификатов, поэтому он будет отображать предупреждение. Для нашего приложения вы можете безопасно нажать **Я понимаю риски**.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>Создание приложения Google для OAuth 2 и подключение приложения к проекту

> [!WARNING]
> Для текущих инструкций Google OAuth [см. Настройка аутентификации Google в ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).

1. Перейдите к [Консоли разработчиков Google](https://console.developers.google.com/).
2. Если вы еще не создали проект раньше, выберите **учетные данные** в левой вкладке, а затем выберите **Создать.**
3. В левой вкладке нажмите **«Удостоверения».**
4. Нажмите **Создать учетные данные,** то **OAuth идентификатор клиента**. 

    1. В диалоге **«Создать идентификатор клиента»** сохраните **web-приложение** по умолчанию для типа приложения.
    2. Установите **авторизованные** истоки JavaScript на URL`https://localhost:44300/` SSL, который вы использовали выше (если вы не создали другие SSL-проекты)
    3. Установите **авторизованный перенаправить URI** на:  
         `https://localhost:44300/signin-google`
5. Нажмите на пункт меню экрана OAuth Consent, а затем установите адрес электронной почты и название продукта. При заполнении формы нажмите **Сохранить**.
6. Нажмите на элемент меню библиотеки, поиск **Google ' API**, нажмите на него, а затем нажмите Включить.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   На рисунке ниже показаны включенные AIS.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. С помощью API-менеджера Google API посетите вкладку **Credentials** для получения **идентификатора клиента.** Скачать, чтобы сохранить файл JSON с секретами приложения. Копируйте и вставьте **ClientId** и `UseGoogleAuthentication` **ClientSecret** в *метод,* найденный в Startup.Auth.cs файле в *папке App_Start.* Значения **ClientId** и **ClientSecret,** приведенные ниже, являются образцами и не работают.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Безопасность - Никогда не храните конфиденциальные данные в исходном коде. Учетная запись и учетные данные добавляются в приведенный выше код, чтобы сохранить образец простым. [Ознакомьтесь с рекомендациями по развертыванию паролей и других конфиденциальных данных в ASP.NET и службе приложений Azure.](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
8. Нажмите **на CTRL-F5,** чтобы построить и запустить приложение. Щелкните ссылку **Войти в систему** .  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. Под **использованием другой службы для входа в систему,** нажмите **Google**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Если вы пропустите любой из вышеперечисленных шагов, вы получите ошибку HTTP 401. Перепроверьте свои шаги выше. Если вы пропустили требуемый параметр (например, **название продукта),** добавьте недостающий элемент и сохраните; проверка подлинности может занять несколько минут.
10. Вы будете перенаправлены на сайт Google, где вы введете свои учетные данные.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. После ввода учетных данных появится запрос на получение разрешений для веб-приложения, которое было только что создано: 
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. Нажмите **Принять**. Теперь вы будете перенаправлены обратно на страницу **Регистрации** приложения MvcAuth, где вы можете зарегистрировать свою учетную запись Google. У вас есть возможность изменить локальное имя регистрации электронной почты, используемое для вашей учетной записи Gmail, но вы, как правило, хотите сохранить псевдоним электронной почты по умолчанию (то есть тот, который вы использовали для проверки подлинности). Щелкните **Зарегистрировать**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Создание приложения в Facebook и подключение приложения к проекту

> [!WARNING]
> Для текущих инструкций по аутентификации Facebook OAuth2 [см.](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Изучение данных о членстве

В меню **View** нажмите **Server Explorer**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

Расширить **defaultConnection (MvcAuth),** расширить **таблицы**, нажмите право **aspNetUsers** и нажмите **Показать таблицы данных**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![таблицы aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Добавление данных профиля в класс пользователя

В этом разделе вы добавите дату рождения и родной город к данным пользователя во время регистрации, как показано на следующем изображении.

![рег с родным городом и Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

Откройте файл *Модели-IdentityModels.cs* и добавьте дату рождения и свойства родного города:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

Откройте файл *Модели-AccountViewModels.cs* и установленную дату `ExternalLoginConfirmationViewModel`рождения и недвижимость в родном городе.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

Откройте файл *Controllers-AccountController.cs* и добавьте код для `ExternalLoginConfirmation` даты рождения и родного города в методе действия, как показано на рисунке:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

Добавить дату рождения и родной город в файл *Views-Account-ExternalLoginConfirmation.cshtml:*

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Удалите базу данных о членстве, чтобы вы могли снова зарегистрировать свою учетную запись Facebook с вашим приложением и проверить, что вы можете добавить новую дату рождения и информацию профиля родного города.

От **разрешения Explorer**, нажмите Показать все **файлы** значок, а затем нажмите нажмите *Нажмите Добавить\_Data'aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* и нажмите **Удалить**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

Из меню **Инструменты,** нажмите **NuGet пакет яслях**, а затем нажмите **пакет менеджер консоли** (PMC). Введите следующие команды в PMC.

1. Включение-миграция
2. Адди-Миграция Init
3. Обновление-База данных

Запустите приложение и используйте FaceBook и Google для входа и регистрации некоторых пользователей.

## <a name="examine-the-membership-data"></a>Изучение данных о членстве

В меню **View** нажмите **Server Explorer**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

Право нажмите **AspNetUsers** и нажмите **Показать Таблица данных**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Поля `HomeTown` `BirthDate` и поля показаны ниже.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Запись вашего приложения и регистрация с другой учетной записью

Если вы входите в приложение с Facebook, а затем выходите из системы и попытаетесь войти снова с другой учетной записью Facebook (с помощью того же браузера), вы будете немедленно войти в предыдущий аккаунт Facebook, который вы использовали. Для того, чтобы использовать другую учетную запись, вам нужно перейти на Facebook и выйти на Facebook. То же правило применяется к любому другому поставщику аутентификации сторон. Кроме того, вы можете войти в систему с другой учетной записью с помощью другого браузера.

## <a name="next-steps"></a>Next Steps

Смотрите [Представляя Yahoo и LinkedIn OAuth поставщиков безопасности для OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Джерри Пелсер для Yahoo и LinkedIn инструкции. Смотрите кнопки входа в социальную систему Jerrie's Pretty для ASP.NET MVC 5, чтобы включить кнопки социального входа.

Следуйте [моему учебнику Создайте приложение mVC ASP.NET с auth и S'L DB и разместите в Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), который продолжает этот учебник и показывает следующее:

1. Как развернуть приложение в Azure.
2. Как обезопасить приложение ролями.
3. Как обезопасить приложение с помощью [фильтров RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) и [разрешить его.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)
4. Как использовать API членства для добавления пользователей и ролей.

Пожалуйста, оставьте отзыв о том, как вам понравился этот учебник и что мы могли бы улучшить. Вы также можете запросить новые темы на [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code). Вы даже можете попросить и проголосовать за новые функции, которые будут добавлены в ASP.NET. Например, можно проголосовать за инструмент [для создания и управления пользователями и ролями.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

Для получения хорошего объяснения того, как работают службы [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services)внешней аутентификации ASP.NET, см. Статья Роберта также подробно описывается в возможности проверки подлинности Microsoft и Twitter. Отличный учебник Tom Dykstra [EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) показывает, как работать с Рамочной системой entity.
