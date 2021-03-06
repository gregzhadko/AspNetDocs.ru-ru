---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
title: Восстановление и изменение паролей (C#) | Документация Майкрософт
author: rick-anderson
description: ASP.NET включает два веб-элемента управления для помощи с восстановлением и изменением паролей. Элемент управления Пассвордрековери позволяет посетителю восстановить утерянный PA...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 19c4d042-4e34-4b44-9f1d-6bf2253ba366
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c07b8a3c36e4863c6d2d356b8483544ac4cafeb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457194"
---
# <a name="recovering-and-changing-passwords-c"></a>Восстановление и смена паролей (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.13.zip) или [скачать PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_cs.pdf)

> ASP.NET включает два веб-элемента управления для помощи с восстановлением и изменением паролей. Элемент управления Пассвордрековери позволяет посетителю восстановить потерянный пароль. Элемент управления ChangePassword позволяет пользователю обновить свой пароль. Как и в других веб-элементах управления, связанных с именем входа, которые мы видели в этой серии руководств, элементы управления Пассвордрековери и ChangePassword работают с инфраструктурой членства в фоновом режиме для сброса или изменения паролей пользователей.

## <a name="introduction"></a>Введение

Между веб-сайтами для моего банка, служебной компании, телефонной компании, учетной записи электронной почты и персонализированных веб-порталов я, как и большинство пользователей, должен помнить десятки разных паролей. Благодаря большому количеству учетных данных для запоминания этих дней люди не часто забывают свои пароли. Для этого веб-сайты, которые предлагают учетные записи пользователей, должны включать способ восстановления пароля пользователем. Этот процесс обычно включает создание нового случайного пароля и его отправку по адресу электронной почты пользователя в файле. После получения нового пароля большинство пользователей возвращаются на сайт и изменяют свой пароль, созданный случайным образом, на более запоминающееся.

ASP.NET включает два веб-элемента управления для помощи с восстановлением и изменением паролей. Элемент управления Пассвордрековери позволяет посетителю восстановить потерянный пароль. Элемент управления ChangePassword позволяет пользователю обновить свой пароль. Как и в других веб-элементах управления, связанных с именем входа, которые мы видели в этой серии руководств, элементы управления Пассвордрековери и ChangePassword работают с инфраструктурой членства в фоновом режиме для сброса или изменения паролей пользователей.

В этом учебнике мы рассмотрим использование этих двух элементов управления. Мы также рассмотрим программное изменение и сброс пароля пользователя с помощью методов `ChangePassword` и `ResetPassword` класса `MembershipUser`.

## <a name="step-1-helping-users-recover-lost-passwords"></a>Шаг 1. помощь пользователям в восстановлении потерянных паролей

Все веб-сайты, поддерживающие учетные записи пользователей, должны предоставлять пользователям некоторый механизм восстановления забытых паролей. Хорошая новость заключается в том, что реализация таких функций в ASP.NET очень просто благодаря веб-элементу управления Пассвордрековери. Элемент управления Пассвордрековери визуализирует интерфейс, предлагающий пользователю ввести имя пользователя, и, при необходимости, ответ на контрольный вопрос. Затем он отправляет по электронной почте пароль пользователя.

> [!NOTE]
> Поскольку сообщения электронной почты передаются по сети в виде обычного текста, существуют риски безопасности, связанные с отправкой пароля пользователя по электронной почте.

Элемент управления Пассвордрековери состоит из трех представлений:

- **Username** — запрашивает у посетителя имя пользователя. Это начальное представление.
- **Вопрос**. Отображает имя пользователя и контрольный вопрос как текст, а также текстовое поле для ввода ответа на контрольный вопрос.
- **Успешно**. отображает сообщение, информирующее пользователя о том, что его пароль был отправлен по электронной почте.

Отображаемые представления и действия, выполняемые элементом управления Пассвордрековери, зависят от следующих параметров конфигурации членства:

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

Параметр `RequiresQuestionAndAnswer` платформы членства указывает, должны ли пользователи при регистрации учетной записи указывать контрольный вопрос и ответить на него. Как мы обсуждали в <a id="_msoanchor_1"> </a>учебнике [*Создание учетных записей пользователей*](../membership/creating-user-accounts-cs.md) , если `RequiresQuestionAndAnswer` имеет значение true (по умолчанию), то интерфейс CreateUserWizard включает элементы управления TextBox для контрольного вопроса нового пользователя и ответа на него. Если `RequiresQuestionAndAnswer` имеет значение false, то такая информация не собирается. Аналогично, если `RequiresQuestionAndAnswer` имеет значение true, элемент управления Пассвордрековери отображает представление вопроса после того, как пользователь вводит имя пользователя. пароль восстанавливается только в том случае, если пользователь вводит правильный ответ на контроль. Однако если `RequiresQuestionAndAnswer` имеет значение false, элемент управления Пассвордрековери перемещается непосредственно из представления UserName в представление успешного выполнения.

После того как пользователь предоставил свое имя пользователя или его имя пользователя и ответ на контрольный вопрос, если `RequiresQuestionAndAnswer` имеет значение true, Пассвордрековери по электронной почте пароль пользователя. Если параметр `EnablePasswordRetrieval` имеет значение true, то пользователь по электронной почте отправляет свой текущий пароль. Если задано значение false, а параметру `EnablePasswordReset` присвоено значение true, то элемент управления Пассвордрековери создает новый случайный пароль для пользователя и отправляет ему по электронной почте новый пароль. Если оба `EnablePasswordRetrieval` и `EnablePasswordReset` имеют значение false, элемент управления Пассвордрековери создает исключение.

> [!NOTE]
> Помните, что `SqlMembershipProvider` хранит пароли пользователей в одном из трех форматов: Clear, хэшированный (по умолчанию) или encrypted. Используемый механизм хранения зависит от параметров конфигурации членства. Демонстрационное приложение использует формат хэшированного пароля. При использовании формата хэшированного пароля параметру `EnablePasswordRetrieval` должно быть присвоено значение false, поскольку система не может определить фактический пароль пользователя из хэшированной версии, хранящейся в базе данных.

На рис. 1 показано влияние интерфейса Пассвордрековери и поведения в конфигурации членства.

[![Рекуирескуестионандансвер, Енаблепассвордретриевал и Енаблепассвордресет влияют на внешний вид и поведение элемента управления Пассвордрековери](recovering-and-changing-passwords-cs/_static/image2.png)](recovering-and-changing-passwords-cs/_static/image1.png)

**Рис. 1**. `RequiresQuestionAndAnswer`, `EnablePasswordRetrieval`и `EnablePasswordReset` влияют на внешний вид и поведение элемента управления Пассвордрековери ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image3.png))

> [!NOTE]
> <a id="_msoanchor_2"> </a>В учебном курсе [*Создание схемы членства в SQL Server*](../membership/creating-the-membership-schema-in-sql-server-cs.md) мы настроили поставщик членства, установив для `RequiresQuestionAndAnswer` значение true, `EnablePasswordRetrieval` значение false, а `EnablePasswordReset` — значение true.

### <a name="using-the-passwordrecovery-control"></a>Использование элемента управления Пассвордрековери

Рассмотрим использование элемента управления Пассвордрековери на странице ASP.NET. Откройте `RecoverPassword.aspx` и перетащите элемент управления Пассвордрековери из панели элементов в конструктор. Задайте для его `ID` значение `RecoverPwd`. Как и в случае с веб-элементами управления для входа и CreateUserWizard, представления элемента управления Пассвордрековери отображают расширенный составной интерфейс, включающий метки, текстовые поля, кнопки и элементы управления проверки. Внешний вид представлений можно настроить с помощью свойств стиля элемента управления или путем преобразования представлений в шаблоны. Я оставлю это в качестве упражнения для заинтересованного читателя.

Когда пользователь посещает эту страницу, он введет имя пользователя и нажмите кнопку Submit (отправить). Поскольку для свойства `RequiresQuestionAndAnswer` задано значение true в настройках конфигурации членства, элемент управления Пассвордрековери будет отображать представление вопроса. После того как пользователь введет правильный ответ безопасности и нажмет кнопку Отправить, элемент управления Пассвордрековери обновит пароль пользователя на случайный, а затем отправьте его по электронной почте на адрес электронной почты в файле. Все это было возможно без необходимости написания одной строки кода!

Прежде чем протестировать эту страницу, можно выполнить одну последнюю настройку: необходимо указать параметры доставки почты в `Web.config`. Элемент управления Пассвордрековери использует эти параметры для отправки сообщения электронной почты.

Конфигурация доставки почты задается с помощью [элемента`<mailSettings>`](https://msdn.microsoft.com/library/w355a94k.aspx) [элемента`<system.net>`](https://msdn.microsoft.com/library/6484zdc1.aspx). Используйте [элемент`<smtp>`](https://msdn.microsoft.com/library/ms164240.aspx) , чтобы указать метод доставки и адрес по умолчанию. Следующая разметка настраивает параметры электронной почты для использования сетевого SMTP-сервера с именем `smtp.example.com` на порту 25 и с учетными данными пользователя и пароля имени пользователя и пароля.

> [!NOTE]
> `<system.net>` является дочерним элементом корневого `<configuration>` элемента и одноуровневый элемент `<system.web>`. Поэтому не помещайте элемент `<system.net>` в элемент `<system.web>`; Вместо этого разместите его на том же уровне.

[!code-xml[Main](recovering-and-changing-passwords-cs/samples/sample1.xml)]

Помимо использования SMTP-сервера в сети, можно также указать каталог подбора, куда должны быть отправлены сообщения электронной почты.

После настройки параметров SMTP посетите страницу `RecoverPassword.aspx` в браузере. Сначала попробуйте ввести имя пользователя, которое не существует в хранилище пользователя. Как показано на рис. 2, элемент управления Пассвордрековери отображает сообщение, указывающее, что не удалось получить доступ к сведениям о пользователе. Текст сообщения можно настроить с помощью [свойства`UserNameFailureText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)элемента управления.

[![отображается сообщение об ошибке, если указано недопустимое имя пользователя](recovering-and-changing-passwords-cs/_static/image5.png)](recovering-and-changing-passwords-cs/_static/image4.png)

**Рис. 2**. сообщение об ошибке при входе в неверное имя пользователя ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image6.png))

Теперь введите имя пользователя. Используйте имя пользователя учетной записи в системе с адресом электронной почты, к которому у вас есть доступ и ответ на который вам известно. После ввода имени пользователя и нажатия кнопки отправить элемент управления Пассвордрековери отображает его представление вопроса. Как и в представлении UserName, при вводе неверного ответа элемент управления Пассвордрековери отображает сообщение об ошибке (см. рис. 3). Чтобы настроить это сообщение об ошибке, используйте [свойство`QuestionFailureText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx) .

[![отображается сообщение об ошибке, если пользователь вводит недопустимый ответ на контроль](recovering-and-changing-passwords-cs/_static/image8.png)](recovering-and-changing-passwords-cs/_static/image7.png)

**Рис. 3**. отображается сообщение об ошибке, если пользователь вводит недопустимый защитный ответ ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image9.png))

Наконец, введите правильный ответ в систему безопасности и нажмите кнопку Отправить. В фоновом режиме элемент управления Пассвордрековери создает случайный пароль, назначает его учетной записи пользователя, отправляет сообщение электронной почты с уведомлением пользователя о новом пароле (см. рис. 4), а затем отображает представление успешного выполнения.

[![пользователь отправляет сообщение электронной почты с новым паролем](recovering-and-changing-passwords-cs/_static/image11.png)](recovering-and-changing-passwords-cs/_static/image10.png)

**Рис. 4**. пользователь отправил сообщение с новым паролем ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image12.png))

### <a name="customizing-the-email"></a>Настройка электронной почты

Электронная почта по умолчанию, отправленная элементом управления Пассвордрековери, довольно тускла (см. рис. 4). Сообщение отправляется из учетной записи, указанной в атрибуте `from` элемента `<smtp>`, с паролем субъекта и текстовым текстом:

Вернитесь на сайт и выполните вход с использованием следующих сведений.

Имя *пользователя: имя пользователя*

Пароль: *пароль*

Это сообщение можно настроить программно с помощью обработчика событий [`SendingMail` события](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)элемента управления пассвордрековери или декларативно с помощью [Свойства`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx). Давайте рассмотрим оба этих варианта.

Событие `SendingMail` срабатывает перед отправкой сообщения электронной почты и является последним шансом программной настройки сообщения электронной почты. При возникновении этого события обработчику событий передается объект типа [`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx), свойство `Message` которого содержит ссылку на отправляемое сообщение электронной почты.

Создайте обработчик событий для `SendingMail` события и добавьте следующий код, который программно добавляет `webmaster@example.com` в список копий.

[!code-csharp[Main](recovering-and-changing-passwords-cs/samples/sample2.cs)]

Сообщение электронной почты также можно настроить с помощью декларативных средств. Свойство `MailDefinition` Пассвордрековери является объектом типа [`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx). Класс `MailDefinition` предлагает узел свойств, связанных с электронной почтой, включая `From`, `CC`, `Priority`, `Subject`, `IsBodyHtml`, `BodyFileName`и др. Для начала присвойте [свойству`Subject`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx) значение, более понятное, чем используемое по умолчанию (пароль), например сброс пароля...

Чтобы настроить текст сообщения электронной почты, необходимо создать отдельный файл шаблона электронной почты, содержащий содержимое текста. Начните с создания новой папки на веб-сайте с именем `EmailTemplates`. Затем добавьте новый текстовый файл в эту папку с именем `PasswordRecovery.txt` и добавьте следующее содержимое:

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample3.aspx)]

Обратите внимание на использование заполнителей `<%UserName%>` и `<%Password%>`. Элемент управления Пассвордрековери автоматически заменяет эти два заполнителя именем пользователя и восстановленным паролем перед отправкой сообщения электронной почты.

Наконец, укажите для [свойства`BodyFileName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) `MailDefinition`шаблон электронного сообщения, который мы только что создали (`~/EmailTemplates/PasswordRecovery.txt`).

После внесения этих изменений снова посетите страницу `RecoverPassword.aspx` и введите имя пользователя и ответ на контрольный вопрос. Вы получите сообщение электронной почты, которое будет выглядеть, как показано на рис. 5. Обратите внимание, что `webmaster@example.com` был CC, а тема и текст были обновлены.

[![список "Тема", "текст" и "копия" обновлен](recovering-and-changing-passwords-cs/_static/image14.png)](recovering-and-changing-passwords-cs/_static/image13.png)

**Рис. 5**. обновлен список субъекта, текст и копия (щелкните,[чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image15.png))

Чтобы отправить сообщение электронной почты в формате HTML [`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) значение true (значение по умолчанию — false) и обновите шаблон электронной почты, включив HTML.

Свойство `MailDefinition` не является уникальным для класса Пассвордрековери. Как будет показано на шаге 2, элемент управления ChangePassword также предлагает свойство `MailDefinition`. Более того, элемент управления CreateUserWizard включает такое свойство, которое можно настроить для автоматической отправки приветственного сообщения новым пользователям.

> [!NOTE]
> В настоящее время в левой части навигации нет ссылок для достижения `RecoverPassword.aspx` странице. Пользователю будет интересно посетить эту страницу только в том случае, если ей не удалось успешно войти на сайт. Поэтому обновите страницу `Login.aspx`, чтобы включить ссылку на страницу `RecoverPassword.aspx`.

### <a name="programmatically-resetting-a-users-password"></a>Программный сброс пароля пользователя

При сбросе пароля пользователя элемент управления Пассвордрековери вызывает [метод`ResetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)объекта `MembershipUser`. У этого метода две перегрузки.

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** — сбрасывает пароль пользователя. Используйте эту перегрузку, если `RequiresQuestionAndAnswer` имеет значение false.
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** — сбрасывает пароль пользователя, только если указан правильный *секуритянсвер* . Используйте эту перегрузку, если `RequiresQuestionAndAnswer` имеет значение true.

Обе перегрузки возвращают новый, создаваемый случайным образом пароль.

Как и в случае с другими методами в инфраструктуре членства, метод `ResetPassword` делегирует настроенному поставщику. `SqlMembershipProvider` вызывает `aspnet_Membership_ResetPassword` хранимую процедуру, передавая пользователю имя пользователя, новый пароль и ответ на него, помимо других полей. Хранимая процедура гарантирует, что ответ пароля совпадает с паролем пользователя, а затем обновляет его.

Пара заметок по реализации низкого уровня:

- Заблокированный пользователь не может сбросить свой пароль. Однако неодобренный пользователь может. Сведения о заблокированных и утвержденных состояниях см. в руководстве по <a id="_msoanchor_3"> </a> [*разблокировке и*](unlocking-and-approving-user-accounts-cs.md) утверждению учетных записей пользователей.
- Если ответ на пароль неверный, то число попыток ответа на пароль не удалось увеличить. Если указанное число недопустимых попыток обеспечения безопасности происходит в течение заданного временного интервала, пользователь блокируется.

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>Слово о том, как создаются случайные пароли

Созданные случайным образом пароли, показанные в сообщениях электронной почты на рис. 4 и 5, создаются с помощью [метода`GeneratePassword`](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)класса членства. Этот метод принимает два целочисленных входных значения примечанием- *length* и *нумберофноналфанумерикчарактерс* -и возвращает строку длиной не менее *нумберофноналфанумерикчарактерс* *символов,* если не меньше букв и не больше, чем для знаков. При вызове этого метода из классов членства или веб-элементов управления, связанных с входом, значения этих двух параметров определяются свойствами `MinRequiredPasswordLength` и `MinRequiredNonalphanumericCharacters` конфигурации членства, которые устанавливаются в 7 и 1 соответственно.

Метод `GeneratePassword` использует криптографически надежный генератор случайных чисел, чтобы гарантировать, что не будет выбрано смещение случайных символов. Более того, `GeneratePassword` является `public`, что позволяет использовать его непосредственно из приложения ASP.NET, если необходимо создать случайные строки или пароли.

> [!NOTE]
> Класс `SqlMembershipProvider` всегда создает случайный пароль длиной не менее 14 символов, поэтому, если `MinRequiredPasswordLength` меньше 14, его значение игнорируется.

## <a name="step-2-changing-passwords"></a>Шаг 2. изменение паролей

Пароли, созданные случайным образом, трудно запомнить. Рассмотрим пароль, показанный на рис. 4. `WWGUZv(f2yM:Bd`. Попробуйте зафиксировать это в памяти! Нет нужды говорить, что после того, как пользователь отправил случайный пароль для этой сортировки, ему потребуется изменить пароль на что-то более запоминающееся.

Используйте элемент управления ChangePassword, чтобы создать интерфейс для изменения пароля пользователя. Как и элемент управления Пассвордрековери, элемент управления ChangePassword состоит из двух представлений: изменить пароль и успешное выполнение. В представлении смена пароля пользователю предлагается ввести старый и новый пароли. При указании правильного старого пароля и нового пароля, который соответствует требованиям к минимальной длине и не алфавитно-цифровым символам, элемент управления ChangePassword обновляет пароль пользователя и отображает представление успешного выполнения.

> [!NOTE]
> Элемент управления ChangePassword изменяет пароль пользователя, вызывая [метод`ChangePassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)объекта `MembershipUser`. Метод ChangePassword принимает два `string` входных параметра — *oldPassword* и *newPassword*— и обновляет учетную запись пользователя с помощью *newPassword*, предполагая, что указанный *oldPassword* является верным.

Откройте страницу `ChangePassword.aspx` и добавьте на страницу элемент управления ChangePassword, назвав его `ChangePwd`. На этом этапе представление конструирования должен отобразить представление смена пароля (см. рис. 6). Как и с элементом управления Пассвордрековери, можно переключаться между представлениями через смарт-тег элемента управления. Более того, эти представления можно настраивать с помощью свойств стиля ассортимента или путем их преобразования в шаблон.

[![добавить на страницу элемент управления ChangePassword](recovering-and-changing-passwords-cs/_static/image17.png)](recovering-and-changing-passwords-cs/_static/image16.png)

**Рис. 6**. Добавление элемента управления ChangePassword на страницу ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image18.png))

Элемент управления ChangePassword может обновить пароль текущего пользователя, вошедшего в систему, *или* пароль другого указанного пользователя. Как показано на рис. 6, представление изменения пароля по умолчанию визуализирует только три элемента управления TextBox: одно для старого пароля и два — для нового пароля. Этот интерфейс по умолчанию используется для обновления пароля пользователя, вошедшего в систему.

Чтобы использовать элемент управления ChangePassword для обновления пароля другого пользователя, установите для [свойства`DisplayUserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx) элемента управления значение true. Это приводит к добавлению четвертого текстового поля на страницу с запросом имени пользователя, чей пароль нужно изменить.

Если вы хотите, чтобы пользователь мог изменить свой пароль без входа в систему, можно задать для параметра `DisplayUserName` значение true. Лично я думаю, что нет ничего плохого в том, что для входа пользователь должен будет изменить его пароль. Поэтому оставьте `DisplayUserName` значением false (значение по умолчанию). Тем не менее, при принятии этого решения мы по сути запрещаю анонимным пользователям обращаться к этой странице. Обновите правила авторизации URL-адресов сайта, чтобы запретить анонимным пользователям посещение `ChangePassword.aspx`. Если вам нужно обновить память по синтаксису правила авторизации URL-адреса, ознакомьтесь с руководством по <a id="_msoanchor_4"> </a> [*авторизации на основе пользователей*](../membership/user-based-authorization-cs.md) .

> [!NOTE]
> Может показаться, что свойство `DisplayUserName` полезно, чтобы позволить администраторам изменять пароли других пользователей. Однако даже если `DisplayUserName` имеет значение true, необходимо знать и указать правильный старый пароль. Мы поговорим о методах, позволяющих администраторам изменять пароли пользователей на шаге 3.

Откройте страницу `ChangePassword.aspx` в браузере и измените свой пароль. Обратите внимание, что при вводе нового пароля, который не соответствует требованиям к длине пароля и не алфавитно-цифровым символам, указанным в конфигурации членства (см. рис. 7), отображается сообщение об ошибке.

[![добавить на страницу элемент управления ChangePassword](recovering-and-changing-passwords-cs/_static/image20.png)](recovering-and-changing-passwords-cs/_static/image19.png)

**Рис. 7**. Добавление элемента управления ChangePassword на страницу ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image21.png))

При вводе правильного старого пароля и допустимого нового пароля пароль пользователя, вошедшего в систему, изменяется, и отображается представление успешного выполнения.

### <a name="sending-a-confirmation-email"></a>Отправка сообщения электронной почты с подтверждением

По умолчанию элемент управления ChangePassword не отправляет пользователю сообщение электронной почты, чей пароль был только что обновлен. Если вы хотите отправить сообщение электронной почты, просто настройте свойство `MailDefinition` элемента управления. Настроим элемент управления ChangePassword таким образом, чтобы пользователь отправлял сообщение электронной почты в формате HTML, содержащее новый пароль.

Начните с создания нового файла в папке `EmailTemplates` с именем `ChangePassword.htm`. Добавьте следующую разметку:

[!code-html[Main](recovering-and-changing-passwords-cs/samples/sample4.html)]

Затем задайте для свойств `BodyFileName`, `IsBodyHtml`и `Subject` `MailDefinition` элемента управления ChangePassword значение ~/EmailTemplates/ChangePassword.htm, true, и ваш пароль изменился! соответственно.

После внесения этих изменений снова перейдите на страницу и снова смените пароль. На этот раз элемент управления ChangePassword отправляет настраиваемое сообщение электронной почты в формате HTML на адрес электронной почты пользователя в файле (см. рис. 8).

[![сообщение электронной почты информирует пользователя об изменении его пароля](recovering-and-changing-passwords-cs/_static/image23.png)](recovering-and-changing-passwords-cs/_static/image22.png)

**Рис. 8**. сообщение электронной почты информирует пользователя о том, что пароль был изменен ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image24.png))

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>Шаг 3. разрешение администраторам изменять пароли пользователей

Общей возможностью в приложениях, поддерживающих учетные записи пользователей, является возможность изменять пароли других пользователей с правами администратора. Иногда эта функция необходима, поскольку системе не хватает возможности изменять свои пароли для пользователей. В этом случае пользователю может потребоваться восстановить забытый пароль, чтобы администратор мог назначить им новый пароль. Однако при использовании элементов управления Пассвордрековери и ChangePassword пользователи с правами администратора должны не заявить себя при изменении паролей пользователей, так как пользователи могут выполнять эти действия.

Но что делать, если клиент настаивает, что пользователи должны иметь возможность изменять пароли других пользователей? К сожалению, добавление этой функции может быть небольшой работой. Чтобы изменить пароль пользователя, необходимо предоставить старый и новый пароль для метода `ChangePassword` объекта `MembershipUser`, но администратору не нужно будет указывать пароль пользователя, чтобы изменить его.

Одно из возможных решений — сначала сбросить пароль пользователя, а затем изменить его на новый, используя код следующего вида:

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample5.aspx)]

Этот код начинается с получения сведений об *имени пользователя*, который является пользователем, чей пароль должен изменить администратор. Далее вызывается метод `ResetPassword`, который присваивает и пользователю новый случайный пароль. Этот пароль, созданный случайным образом, возвращается методом и сохраняется в переменной `resetPwd`. Теперь, когда вы узнали пароль пользователя, мы можем изменить его с помощью вызова `ChangePassword`.

Проблема заключается в том, что этот код работает только в том случае, если конфигурация системы членства настроена так, что `RequiresQuestionAndAnswer` имеет значение false. Если `RequiresQuestionAndAnswer` имеет значение true, как это касается нашего приложения, методу `ResetPassword` должен быть передан ответ на контрольный вопрос, в противном случае будет выдано исключение.

Если платформа членства настроена так, что требуется контрольный вопрос и ответ, и клиент настаивает, что администраторы смогут изменять пароли пользователей, у вас есть три варианта:

- Создавайте руки в воздухе и сообщайте клиенту, что это только одно, что не может быть сделано.
- Задайте для `RequiresQuestionAndAnswer` значение false. Это приводит к снижению безопасности приложения. Представьте себе, что пользователь злостный получил доступ к папке "Входящие" электронной почты другого пользователя. Возможно, скомпрометированный пользователь покинул свой рабочий стол и не блокировал свою рабочую станцию, или если у него есть доступ к электронной почте из общедоступного терминала, а не выход из него. В любом случае пользователь злостный может посетить страницу `RecoverPassword.aspx` и ввести имя пользователя. Затем система отправит восстановленный пароль по электронной почте, не выполняя запрос на контрольный вопрос.
- Обходить слой абстракции, созданный платформой членства, и работать непосредственно с базой данных SQL Server. Схема членства включает хранимую процедуру с именем `aspnet_Membership_SetPassword`, которая задает пароль пользователя и не требует ответа на контрольный вопрос или старый пароль для выполнения задачи.

Ни один из этих вариантов не является особенно привлекательным, но в этом заключается в том, что жизнь разработчика иногда бывает.

Я приступил к реализации третьего подхода, написанию кода, который обходит классы `Membership` и `MembershipUser` и работает непосредственно с базой данных `SecurityTutorials`.

> [!NOTE]
> При работе непосредственно с базой данных инкапсуляция, предоставляемая платформой членства, — это разбит. Это решение связывает нас с `SqlMembershipProvider`, делая код менее переносимым. Кроме того, этот код может работать не так, как ожидалось в будущих версиях ASP.NET при изменении схемы членства. Этот подход является обходным путем, и, как и большинство обходных путей, не является примером рекомендаций.

Код имеет несколько непривлекательных разрядов и довольно длинный. Поэтому я не хочу перегружать этот учебник с углубленным исследованием. Если вы заинтересованы в изучении, скачайте код для этого руководства и посетите страницу `~/Administration/ManageUsers.aspx`. Эта страница, созданная в <a id="_msoanchor_5"> </a> [предыдущем руководстве](building-an-interface-to-select-one-user-account-from-many-cs.md), содержит список всех пользователей. Я обновил GridView, включив ссылку на страницу `UserInformation.aspx`, передав имя пользователя выбранного пользователя через строку запроса. На странице `UserInformation.aspx` отображаются сведения о выбранном пользователе и полях для изменения их пароля (см. рис. 9).

После ввода нового пароля, его подтверждения во втором текстовом поле и нажатия кнопки Обновить пользователя происходит обратная передача и вызывается `aspnet_Membership_SetPassword` хранимая процедура, которая обновляет пароль пользователя. Я рекомендую пользователям, заинтересованным в этой функции, ознакомиться с кодом и попытаться расширить функциональные возможности, включив отправку сообщения электронной почты пользователю, чей пароль был изменен.

[![администратор может изменить пароль пользователя](recovering-and-changing-passwords-cs/_static/image26.png)](recovering-and-changing-passwords-cs/_static/image25.png)

**Рис. 9**. Администратор может изменить пароль пользователя ([щелкните, чтобы просмотреть изображение с полным размером](recovering-and-changing-passwords-cs/_static/image27.png))

> [!NOTE]
> `UserInformation.aspx`ная страница работает в данный момент только в том случае, если платформа членства настроена для хранения паролей в формате с открытым или хэшированным форматом. В нем отсутствует код для шифрования нового пароля, хотя вы приглашаетесь добавить эту функцию. Я рекомендую добавить необходимый код, чтобы проанализировать исходный код методов в .NET Framework, используя декомпилятор, например [Reflector](http://www.aisto.com/roeder/dotnet/) . Начните с изучения метода `ChangePassword` класса `SqlMembershipProvider`. Это методика, которую я использовал для написания кода для создания хэша пароля.

## <a name="summary"></a>Сводка

ASP.NET предлагает два элемента управления, помогающие пользователям управлять своим паролем. Элемент управления Пассвордрековери полезен для тех, кто забыл свои пароли. В зависимости от конфигурации платформы членства пользователь либо отправляет по электронной почте свой существующий пароль, либо создает новый случайный пароль. Элемент управления ChangePassword позволяет пользователю обновить свой пароль.

Как и элементы управления Login и CreateUserWizard, элементы управления Пассвордрековери и ChangePassword отображают богатый пользовательский интерфейс без необходимости написания декларативной разметки или строки кода. Если пользовательский интерфейс по умолчанию не соответствует вашим потребностям, его можно настроить с помощью различных свойств стиля. Кроме того, интерфейсы элементов управления могут быть преобразованы в шаблоны для более тонкой степени контроля. В фоновом режиме эти элементы управления используют API членства, вызывая методы `ResetPassword` и `ChangePassword` объекта `MembershipUser`.

Поздравляем с программированием!

### <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Краткие руководства по элементу управления ChangePassword](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [Краткие руководства по элементу управления Пассвордрековери](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [Отправка электронной почты в ASP.NET](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` часто задаваемые вопросы](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>Об авторе

Скотт Митчелл, автор нескольких книг по ASP/ASP. NET и основатель 4GuysFromRolla.com, работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — *[Sams обучать себя ASP.NET 2,0 за 24 часа](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Скотт можно получить по адресу [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) или через свой блог по адресу [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства включают Майкл Еммингс и Сучи Банержи. Хотите ознакомиться с моими будущими статьями MSDN? Если да, расположите строку в [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](building-an-interface-to-select-one-user-account-from-many-cs.md)
> [Вперед](unlocking-and-approving-user-accounts-cs.md)
