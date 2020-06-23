---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Проверка подлинности Windows Azure | Документация Майкрософт
author: Rick-Anderson
description: Средства Microsoft ASP.NET для Windows Azure Active Directory упрощают проверку подлинности для веб-приложений, размещенных на веб-сайтах Windows Azure...
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: ab75218cbe3817c14a064e9816388aebc7e431f7
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240568"
---
# <a name="windows-azure-authentication"></a>Проверка подлинности Microsoft Azure

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> Средства Microsoft ASP.NET для Windows Azure Active Directory упрощают проверку подлинности для веб-приложений, размещенных на [веб-сайтах Windows Azure](https://www.windowsazure.com/home/features/web-sites/). Для проверки подлинности пользователей Office 365 в Организации можно использовать проверку подлинности Windows Azure. корпоративные учетные записи синхронизируются с локальными Active Directory или пользователями, созданными в пользовательском домене Windows Azure Active Directory. Включение проверки подлинности Windows Azure настраивает приложение для проверки подлинности пользователей с помощью одного клиента [Azure Active Directory Windows](https://docs.microsoft.com/azure/active-directory/) .
>
> Средство проверки подлинности Windows Azure ASP.NET не поддерживается для веб-ролей в облачной службе, но мы планируем сделать это в будущем выпуске. [Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) поддерживается в веб-ролях Windows Azure.
>
> Дополнительные сведения о настройке синхронизации между локальными Active Directory и клиентом Windows Azure Active Directory см. в статье [использование AD FS 2,0 для реализации единого входа и управления им](https://technet.microsoft.com/library/jj205462.aspx).
>
> Windows Azure Active Directory в настоящее время доступна в качестве [бесплатной предварительной версии службы](https://azure.microsoft.com/free/dotnet/).

## <a name="requirements"></a>Требования

- Visual Studio 2012 или [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- [Расширения веб-инструментов для расширений Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) или [Web tools для Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)
- [Средства Microsoft ASP.NET для windows Azure Active Directory — Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) или [Microsoft ASP.NET Tools for windows Azure Active Directory – Visual Studio Express 2012 для Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>Создание веб-приложения ASP.NET с помощью Visual Studio 2012

Вы можете создать любое веб-приложение с помощью Visual Studio 2012. в этом руководстве используется шаблон интрасети ASP.NET MVC.

1. Создайте новое приложение интрасети ASP.NET MVC 4 и примите все значения по умолчанию. (Он должен быть в **тра** NET, а не в проекте **заве** NET).
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>Включить проверку подлинности Windows Azure (если вы являетесь глобальным администратором этого принципа)

Если у вас нет существующего клиента Windows Azure Active Directory (например, с помощью существующей учетной записи Office 365), можно создать новый клиент, зарегистрировавшись на [новую учетную запись Azure Active Directory Windows](https://g.microsoftonline.com/0AX00en/5).

1. В меню Проект выберите **включить проверку подлинности Windows Azure**:

   ![](windows-azure-authentication/_static/image2.png)

2. Введите домен для клиента Windows Azure Active Directory (например, contoso.onmicrosoft.com) и щелкните **включить**.

![](windows-azure-authentication/_static/image3.png)

3. В диалоговом окне веб-аутентификации Войдите в систему как администратор для вашего клиента Windows Azure Active Directory:

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>Включение Windows Azure не администратором этого принципа

Если у вас нет прав глобального администратора для клиента Windows Azure Active Directory, можно снять флажок для подготовки приложения.

![](windows-azure-authentication/_static/image6.png)

В диалоговом окне отобразится **домен**, **идентификатор субъекта приложения** и **URL-адрес ответа** , необходимые для подготовки приложения с помощью Azure Active Directoryного принципа. Эти сведения необходимо предоставить пользователю, имеющему достаточные права для предоставления приложения. Сведения о том, как использовать командлет для создания субъекта-службы вручную, см. в статье[Реализация единого входа с помощью приложения Windows Azure Active Directory ASP.NET](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) .
После успешной подготовки приложения можно нажать кнопку **продолжить обновление web.config с выбранными параметрами**. Если вы хотите продолжить разработку приложения во время ожидания подготовки, можно нажать кнопку **Закрыть, чтобы запомнить параметры в файле проекта**. При следующем вызове параметра включить проверку подлинности Windows Azure и снять флажок подготовить можно увидеть те же параметры и нажать кнопку **продолжить**, а затем **применить эти параметры в web.config**.

1. Подождите, пока приложение настроено для проверки подлинности Windows Azure и подготовлено с помощью Azure Active Directory Windows.
2. После включения проверки подлинности Windows Azure для приложения нажмите кнопку **Закрыть:**

    ![](windows-azure-authentication/_static/image7.png)
3. Нажмите клавишу F5, чтобы запустить приложение. Вы должны автоматически перенаправлены на страницу входа. Для входа в приложение используйте учетные данные пользователя, предназначенного для доступа к каталогу.

    ![](windows-azure-authentication/_static/image1.jpg)
4. Так как приложение в настоящее время использует самозаверяющий тестовый сертификат, вы получите от браузера предупреждение о том, что сертификат не был выдан доверенным центром сертификации.

    Это предупреждение можно спокойно игнорировать во время локальной разработки, нажав кнопку **"продолжить" для этого веб-сайта:**

    ![](windows-azure-authentication/_static/image8.png)
5. Вы успешно выполнили вход в приложение с помощью проверки подлинности Windows Azure!

    ![](windows-azure-authentication/_static/image2.jpg)

Включение проверки подлинности Windows Azure вносит в приложение следующие изменения:

- В проект добавляется класс подделки межсайтовых запросов ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) ( *app \_ старт\антикссрфконфиг.КС* ).
- Пакеты NuGet `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` добавляются в проект.
- Параметры Windows Identity Foundation в приложении будут настроены на прием маркеров безопасности от клиента Windows Azure Active Directory. Щелкните изображение ниже, чтобы просмотреть развернутое представление изменений, внесенных в файл *Web.config* .

     ![](windows-azure-authentication/_static/image9.png)
- Будет подготовлен субъект-служба для приложения в клиенте Windows Azure Active Directory.
- HTTPS включен.

## <a name="deploy-the-application-to-windows-azure"></a>Развертывание приложения в Windows Azure

Полные инструкции см. [в статье Развертывание веб-приложения ASP.NET на веб-сайте Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).

Чтобы опубликовать приложение с помощью проверки подлинности Windows Azure на веб-сайте Azure, выполните следующие действия.

1. Щелкните приложение правой кнопкой мыши и выберите **Опубликовать:**

    ![](windows-azure-authentication/_static/image3.jpg)
2. В диалоговом окне Опубликовать веб-сайт Скачайте и импортируйте профиль публикации для веб-сайта Azure.

    ![](windows-azure-authentication/_static/image4.jpg)
3. На вкладке **Подключение** отображается **URL-адрес назначения** (общедоступный URL-адрес приложения). Щелкните **проверить подключение** , чтобы проверить подключение.

    ![](windows-azure-authentication/_static/image5.jpg)
4. Если вы уже опубликовали на этом веб-сайте Azure, рекомендуется проверить параметр **удалить дополнительные файлы в месте назначения** , чтобы убедиться, что приложение публикуется аккуратно. Обратите внимание, что флажок **включить проверку подлинности Windows Azure** установлен.

    ![](windows-azure-authentication/_static/image10.png)
5. Необязательно. на вкладке **Предварительный просмотр** нажмите кнопку **запустить предварительный просмотр** , чтобы просмотреть развернутые файлы.

    ![](windows-azure-authentication/_static/image6.jpg)
6. Нажмите кнопку **Опубликовать.**

    Вам будет предложено включить проверку подлинности Windows Azure для целевого узла. Чтобы продолжить, нажмите кнопку **включить** .

    ![](windows-azure-authentication/_static/image11.png)
7. Введите учетные данные администратора для клиента Windows Azure Active Directory:

    ![](windows-azure-authentication/_static/image7.jpg)
8. После успешной публикации приложения браузер откроется на опубликованном веб-узле.

    > [!NOTE]
    > Полная подготовка приложения с помощью Windows Azure Active Directory после включения проверки подлинности Windows Azure для целевого узла может занять до пяти минут (обычно меньше). При первом запуске приложения при появлении ошибки ACS50001: не удалось найти проверяющую сторону с именем "[realm]", подождите несколько минут и попробуйте запустить приложение еще раз.
9. При появлении запроса войдите в систему как пользователь в каталоге:

    ![](windows-azure-authentication/_static/image8.jpg)
10. Вы успешно выполнили вход в приложение, размещенное в Azure, с использованием проверки подлинности Windows Azure.

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>Известные проблемы

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>Сбой авторизации на основе ролей при использовании проверки подлинности Windows Azure

В настоящее время проверка подлинности Windows Azure не предоставляет необходимое утверждение роли, чтобы можно было выполнить авторизацию на основе ролей. Роль пользователя, прошедшего проверку подлинности, необходимо вручную получить из Azure Active Directory Windows.

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>При переходе к приложению с проверкой подлинности Windows Azure возникает ошибка "ACS20016 домен пользователя, вошедшего в систему (live.com), не соответствует ни одному домену этой STS"

Если вы уже вошли в учетную запись Майкрософт (например, hotmail.com, live.com, outlook.com) и пытаетесь получить доступ к приложению, в котором включена проверка подлинности Windows Azure, вы можете получить ответ об ошибке 400, так как домен вашей учетной записи Майкрософт не распознается Azure Active Directory Windows. Чтобы войти в приложение, сначала выйдите из своей учетной записи Майкрософт.

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>Вход в приложение с включенной проверкой подлинности Windows Azure и X509CertificateValidationMode, отличное от None, приводит к ошибкам проверки сертификата для сертификата accounts.accesscontrol.windows.net.

Проверка сертификата не является обязательной и должна быть отключена. Отпечаток сертификата издателя проверяется модулем WSFederationAuthenticationModule.

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>При попытке включить проверку подлинности Windows Azure в диалоговом окне веб-аутентификации отображается ошибка "ACS20016: домен пользователя, выполнившего вход (contoso.onmicrosoft.com), не соответствует ни одному из разрешенных доменов этой STS".

Эта ошибка может возникать, если ранее вы успешно выполнили вход с помощью другой учетной записи Azure Active Directory Windows в рамках того же процесса Visual Studio. Выйдите из указанной учетной записи или перезапустите Visual Studio. Если вы ранее вошли в систему и выбрали параметр "оставаться в системе", вам может потребоваться очистить файлы cookie браузера.

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012: запрос не является допустимым сообщением протокола WS-Federation

Это может произойти, если вы уже выполнили вход с другим ИДЕНТИФИКАТОРом Майкрософт в одну из служб Azure. Используйте закрытое окно браузера, например InPrivate в IE или режиме инкогнито в Chrome, или очистите все файлы cookie.

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Средства Microsoft ASP.NET для Windows Azure Active Directory — Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Витторио Берточчи
- [Функции Windows Azure: удостоверение](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Azure Active Directory Windows](https://technet.microsoft.com/library/hh967619.aspx)
- [Azure Active Directory Windows: Разработка приложений для Организации](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Azure Active Directory Windows: Разработка приложений для нескольких организаций](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [Как реализовать единый вход с помощью Windows Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Единый вход с Windows Azure Active Directory: подробный](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) обзор – Витторио Берточчи
- [Использование AD FS 2,0 для реализации единого входа и управления им](https://technet.microsoft.com/library/jj205462.aspx)
