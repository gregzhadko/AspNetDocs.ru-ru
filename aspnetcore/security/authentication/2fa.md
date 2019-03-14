---
title: Двухфакторная проверка подлинности с помощью SMS в ASP.NET Core
author: rick-anderson
description: Узнайте, как настроить двухфакторную проверку подлинности (2FA) с помощью приложения ASP.NET Core.
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 09/22/2018
ms.custom: seodec18
uid: security/authentication/2fa
ms.openlocfilehash: 48bfc50378fc0ec212f5b9d4e7ce05bb4fc97b9d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052761"
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a>Двухфакторная проверка подлинности с помощью SMS в ASP.NET Core

По [Рик Андерсон](https://twitter.com/RickAndMSFT) и [разработчики Швейцария](https://github.com/Swiss-Devs)

>[!WARNING]
> Два фактора проверки подлинности (2FA) проверки подлинности приложения с помощью по времени одноразовый пароль алгоритм (TOTP), являются отрасли, рекомендуемый подход для 2FA. 2FA с помощью TOTP предпочтительнее SMS 2FA. Дополнительные сведения см. в разделе [создания включить QR-кода для приложений TOTP проверки подлинности в ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) ASP.NET Core 2.0 и более поздних версий.

Этом руководстве показано, как настроить двухфакторную проверку подлинности (2FA) с помощью SMS. Инструкции, приведенные для [twilio](https://www.twilio.com/) и [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), но вы можете использовать любой другой поставщик SMS. Мы рекомендуем вам выполнить [подтверждение учетной записи и восстановление пароля](xref:security/authentication/accconfirm) этим руководством.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA). [Как скачать](xref:index#how-to-download-a-sample).

## <a name="create-a-new-aspnet-core-project"></a>Создание проекта ASP.NET Core

Создание нового веб-приложения ASP.NET Core с именем `Web2FA` с учетными записями отдельных пользователей. Следуйте инструкциям в <xref:security/enforcing-ssl> для настройки и обязательного использования протокола HTTPS.

### <a name="create-an-sms-account"></a>Создание учетной записи SMS

Создание учетной записи SMS, например, из [twilio](https://www.twilio.com/) или [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/). Запишите учетные данные проверки подлинности (для twilio: accountSid и authToken для ASPSMS: Userkey и пароль).

#### <a name="figuring-out-sms-provider-credentials"></a>Выяснение учетные данные поставщика SMS

**Twilio:** На вкладке панели мониторинга учетной записи Twilio, скопируйте **ИД безопасности учетной записи** и **маркер проверки подлинности**.

**ASPSMS:** Параметры учетной записи, перейдите к **Userkey** и скопируйте его вместе с вашей **пароль**.

Позже мы сохраним эти значения с помощью диспетчера секретов, в ключи `SMSAccountIdentification` и `SMSAccountPassword`.

#### <a name="specifying-senderid--originator"></a>Указав идентификатор SenderID / инициатора

**Twilio:** На вкладке «числа» скопируйте twilio и значениями **номер телефона**.

**ASPSMS:** Меню разблокирования инициаторы разблокировать один или несколько авторства или выберите инициатор буквенно-цифровых (не поддерживается всех сетей).

Позже мы Сохраним это значение с помощью диспетчера секретов, раздел `SMSAccountFrom`.


### <a name="provide-credentials-for-the-sms-service"></a>Укажите учетные данные для службы SMS

Мы будем использовать [шаблон параметров](xref:fundamentals/configuration/options) для доступа к параметрам и ключ учетной записи пользователя.

   * Создание класса для извлечения ключа безопасности SMS. В этом примере `SMSoptions` класс создается в *Services/SMSoptions.cs* файла.

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

Задайте `SMSAccountIdentification`, `SMSAccountPassword` и `SMSAccountFrom` с [средство secret manager](xref:security/app-secrets). Пример:

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* Добавьте пакет NuGet для поставщика SMS. Из консоли диспетчера пакетов (PMC) выполните:

**Twilio:**
`Install-Package Twilio`

**ASPSMS:**
`Install-Package ASPSMS`


* Добавьте код в *Services/MessageServices.cs* файл, чтобы включить SMS. Использование Twilio или разделе ASPSMS:


**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]

**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]

### <a name="configure-startup-to-use-smsoptions"></a>Настройка запуска для использования `SMSoptions`

Добавить `SMSoptions` в контейнер службы в `ConfigureServices` метод в *Startup.cs*:

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a>Включение двухфакторной проверки подлинности

Откройте *Views/Manage/Index.cshtml* файл представления Razor и удалите символы комментария (поэтому разметка не закомментированного).

## <a name="log-in-with-two-factor-authentication"></a>Войдите с помощью двухфакторной проверки подлинности

* Запустите приложение и зарегистрируйте нового пользователя

![Веб-приложение Register, откройте представление в Microsoft Edge](2fa/_static/login2fa1.png)

* Выберите свое имя пользователя, который активирует `Index` метода действия в контроллере управление. Выберите номер телефона **добавить** ссылку.

![Управление представления – нажать ссылку «Добавить»](2fa/_static/login2fa2.png)

* Добавить номер телефона, который будет получать код проверки и коснитесь **отправить проверочный код**.

![Добавить страницу номер телефона](2fa/_static/login2fa3.png)

* Вы получите текстовое сообщение с кодом проверки. Введите его и коснитесь **отправки**

![Проверить номер телефона страницу](2fa/_static/login2fa4.png)

Если вы не получили текстовое сообщение, см. в разделе страницы журнала twilio.

* Представления управление показывает, что ваш номер телефона успешно добавлен.

![Управление представление — номер телефона успешно добавлен](2fa/_static/login2fa5.png)

* Коснитесь **включить** включить двухфакторную проверку подлинности.

![Управления представлением — Включение двухфакторной проверки подлинности](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a>Тестирование двухфакторной проверки подлинности

* Выйдите из системы.

* Вход.

* Учетной записи пользователя включена двухфакторная проверка подлинности, поэтому вы должны предоставить второй фактор проверки подлинности. В этом руководстве вы включили Проверка номера телефона. Встроенные шаблоны позволяют настроить почту в качестве второго фактора. Можно настроить дополнительные факторы проверки подлинности, например QR-коды, второй. Коснитесь **отправить**.

![Отправить код проверки представления](2fa/_static/login2fa7.png)

* Введите код, полученный в SMS-сообщения.

* Щелкнув **запомнить браузер** флажок будет исключить от необходимости использовать 2FA для входа при использовании же устройства и браузера. Включение 2FA и щелкнув **запомнить браузер** предоставит вам строгого 2FA защиты от злоумышленников, пытается получить доступ к вашей учетной записи, до тех пор, пока они не имеют доступа к устройству. Это можно сделать на любом устройстве закрытого, которые регулярно использовать. Установив **запомнить браузер**, вы получаете дополнительную защиту 2FA с устройств, вы не используете регулярно, и вы получаете удобства на не нужно изучать через 2FA на собственных устройствах.

![Проверить представление](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a>Блокировка учетной записи, обеспечивающие защиту от атак методом подбора

Блокировка учетной записи рекомендуется с 2FA. Когда пользователь войдет в приложение через локальную учетную запись или учетную запись социальной сети, каждая неудачная попытка 2FA хранится. После достижения максимального неудачных попыток доступа пользователя блокируется (по умолчанию: 5-минутный блокировки после 5 неудачных попыток доступа). Сбрасывает счетчик попыток неудачные попытки доступа успешной проверки подлинности и сбрасывает часы. Максимально неудачных попыток доступа и время блокировки может быть задано с помощью [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) и [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan). Следующие настраивает блокировки учетных записей для 10 минут после десяти неудачных попыток доступа:

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

Убедитесь, что [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) задает `lockoutOnFailure` для `true`:

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
