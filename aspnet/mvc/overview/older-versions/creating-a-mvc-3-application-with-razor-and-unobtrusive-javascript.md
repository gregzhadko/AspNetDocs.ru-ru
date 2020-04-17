---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Создание приложения MVC 3 с помощью Razor и ненавязчивого JavaScript (ru) Документы Майкрософт
author: rick-anderson
description: Образец веб-приложения «Список пользователей» демонстрирует, насколько просто создавать ASP.NET приложения MVC 3 с помощью движка представления Razor. Образец применения s. .
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542460"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Создание приложения на MVC 3 с помощью Razor и ненавязчивого JavaScript

[корпорацией Майкрософт](https://github.com/microsoft)

> Образец веб-приложения «Список пользователей» демонстрирует, насколько просто создавать ASP.NET приложения MVC 3 с помощью движка представления Razor. Пример приложения показывает, как использовать новый движок представления Razor с ASP.NET версии MVC 3 и Visual Studio 2010 для создания вымышленного веб-сайта списка пользователей, который включает в себя такие функции, как создание, отображение, редактирование и удаливание пользователей.
> 
> В этом уроке описаны шаги, предпринятые для создания образца списка пользователей ASP.NET приложениеM MVC 3. Проект Visual Studio с исходным кодом C и VB доступен для сопровождения этой темы: [Скачать](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Если у вас есть вопросы об этом учебнике, пожалуйста, разместите их на [форуме MVC](https://forums.asp.net/1146.aspx).

## <a name="overview"></a>Обзор

Приложение, которое вы будете строить простой веб-сайт список пользователей. Пользователи могут вводить, просматривать и обновлять информацию о пользователе.

![Пример сайта](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

Вы можете скачать VB и C е завершенный проект [здесь](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).

## <a name="creating-the-web-application"></a>Создание веб-приложения

Чтобы начать учебник, откройте Visual Studio 2010 и создайте новый проект с использованием *шаблона ASP.NET веб-приложений MVC 3 MVC 3.* Назовите приложение &quot;Mvc3Razor&quot;.

[![Новый проект MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

В **диалоге проекта New ASP.NET MVC 3** выберите **Internet Application,** выберите движок представления Razor, а затем нажмите **OK.**

![Новый диалог проекта mVC 3 ASP.NET](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

В этом учебнике вы не будете использовать ASP.NET поставщика членства, так что вы можете удалить все файлы, связанные с логином и членством. В **Solution Explorer**удалите следующие файлы и каталоги:

- *Контролеры-бухгалтеры*
- *Модели-AccountModels*
- *Просмотр\\_LogOnPartialы*
- *Просмотры (и* все файлы в этом каталоге)

![Солн Эксп](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

Отойдите файл <em> \_Layout.cshtml</em> и замените `<div>` разметку внутри элемента, названного `logindisplay` сообщением <em>&quot;</em>Login Disabled.&quot; Следующий пример показывает новую разметку:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Добавление модели

В **Solution Explorer**, правой кнопкой кнопку *Модели* папку, выберите **Добавить,** а затем нажмите **класс**.

![Новый пользовательский класс Mdl](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Назовите класс `UserModel`. Замените содержимое файла *UserModel* следующим кодом:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

Класс `UserModel` представляет пользователей. Каждый участник класса аннотируется с [требуемым](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) атрибутом из пространства имен [DataAnnotations.](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Атрибуты в пространстве имен [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) обеспечивают автоматическую проверку на стороне клиента и сервера для веб-приложений.

Откройте `HomeController` класс и `using` добавьте директиву, `UserModel` `Users` чтобы вы могли получить доступ к классам:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Сразу после `HomeController` объявления добавьте следующий комментарий `Users` и ссылку на класс:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

Класс `Users` представляет собой упрощенный хранилище данных в памяти, который вы будете использовать в этом учебнике. В реальном приложении вы будете использовать базу данных для хранения информации о пользователе. Первые несколько строк `HomeController` файла отображаются в следующем примере:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Создайте приложение таким образом, чтобы модель пользователя была доступна мастеру строительных лесов на следующем этапе.

## <a name="creating-the-default-view"></a>Создание представления по умолчанию

Следующим шагом является добавление метода действия и представления для отображения пользователей.

Удалите существующий файл *«Домашний индекс».* Вы создадите новый файл *Индекса* для отображения пользователей.

В `HomeController` классе замените содержимое `Index` метода следующим кодом:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Нажмите правой `Index` кнопкой мыши внутри метода, а затем нажмите **Добавить вид**.

![Добавление представления](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Выберите **возможность создания сильно типового представления.** Для **просмотра класса данных,** выберите **Mvc3Razor.Models.UserModel**. (Если вы не видите **Mvc3Razor.Models.UserModel** в поле **класса данных View,** вам необходимо создать проект.) Убедитесь, что движок представления настроен на **Razor.** Установите **содержимое просмотра** в **список,** а затем нажмите **Добавить**.

![Добавление представления индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Новое представление автоматически подмостки пользовательских данных, `Index` которые передаются в представление. Изучите недавно созданный файл *«Домашний индекс».* **Создать новые,** **отсвативайте,** **Детали**и **Удалить** ссылки не работают, но остальная часть страницы является функциональной. Запустите страницу. Вы видите список пользователей.

![Страница индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

Откройте файл *Index.cshtml* `ActionLink` и замените разметку для **Edit,** **Подробности**и **Удалить** со следующим кодом:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Имя пользователя используется в качестве идентификатора для поиска выбранной записи в ссылках **Edit,** **Details**и **Delete.**

## <a name="creating-the-details-view"></a>Создание представления деталей

Следующим шагом является добавление `Details` метода действия и представления для отображения деталей пользователя.

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Добавьте `Details` следующий метод к домашнему контроллеру:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Нажмите правой `Details` кнопкой мыши внутри метода, а затем выберите <strong>Добавить вид</strong>. Убедитесь, что в поле <strong>класса данных View</strong> содержится <strong>Mvc3Razor.Models.UserModel</strong><em>.</em> Установите <strong>содержимое view</strong> для <strong>деталей,</strong> а затем нажмите <strong>Добавить</strong>.

![Добавление представления деталей](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Запустите приложение и выберите ссылку на детали. Автоматические строительные леса показывают каждое свойство в модели.

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Создание представления об отсылке

Добавьте `Edit` следующий метод к домашнему контроллеру.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Добавьте представление, как в предыдущих шагах, но установите **содержимое view** для **edit.**

![Добавление представления edit](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Запустите приложение и отодевать имя и фамилию одного из пользователей. Если вы `DataAnnotation` нарушаете какие-либо `UserModel` ограничения, которые были применены к классу, при отправке формы вы увидите ошибки проверки, которые производятся кодом сервера. Например, если вы измените&quot; &quot;имя&quot; &quot;Ann на A, при отправке формы в форме отображается следующая ошибка:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

В этом уроке вы рассматриваете имя пользователя в качестве основного ключа. Таким образом, свойство имени пользователя не может быть изменено. В файле *Edit.cshtml* сразу `Html.BeginForm` после оператора установите имя пользователя как скрытое поле. Это приводит к тому, что свойство передается в модели. Следующий фрагмент кода показывает `Hidden` размещение оператора:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Замените `TextBoxFor` `ValidationMessageFor` и разметку для `DisplayFor` имени пользователя вызовом. Метод `DisplayFor` отображает свойство как элемент только для чтения. В следующем примере приведена полная разметка. Оригинал `TextBoxFor` и `ValidationMessageFor` звонки комментируются с Razor начать комментарий и конец-комментарий символов (`@* *@`)

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Включение проверки клиента на стороне

Для включения проверки на стороне клиента в ASP.NET MVC 3 необходимо установить два флага и включить три файла JavaScript.

Откройте файл *Web.config* приложения. Проверить `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` и верны в настройках приложения. Следующий фрагмент из корневого файла *Web.config* показывает правильные настройки:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

Установка `UnobtrusiveJavaScriptEnabled` на истину позволяет ненавязчивым Ajax и ненавязчивой проверки клиента. При использовании ненавязчивой проверки правила проверки превращаются в атрибуты HTML5. Имена атрибутов HTML5 могут состоять только из букв, цифр и тире.

Установка `ClientValidationEnabled` на истину позволяет клиентской проверки. Установив эти ключи в файле *web.config* приложения, вы позволяете проверку клиента и ненавязчивый JavaScript для всего приложения. Вы также можете включить или отключить эти параметры в отдельных представлениях или в методах контроллера, используя следующий код:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Также необходимо включить несколько файлов JavaScript в отрисованные представления. Простой способ включить JavaScript во все представления — добавить их в файл *«Общие\\_Layout.cshtml».* Замените `<head>` элемент файла * \_Layout.cshtml* следующим кодом:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

Первые два сценария j'ery размещаются в Microsoft Ajax Content Delivery Network (CDN). Воспользовавшись Microsoft Ajax CDN, вы можете значительно улучшить производительность приложений в первом хите.

Запустите приложение и нажмите ссылку на отодевать. Просмотр источника страницы в браузере. Источник браузера показывает много атрибутов формы `data-val` (для проверки данных). При включении проверки клиента и ненавязчивой JavaScript ввода полей с `data-val="true"` правилом проверки клиента содержат атрибут, чтобы вызвать ненавязчивую проверку клиента. Например, `City` поле в модели было украшено [атрибутом Required,](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) что приводит к html, показанным в следующем примере:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Для каждого правила проверки клиента добавляется атрибут, `data-val-rulename="message"`который имеет форму. Используя `City` приведенный ранее пример поля, требуемое правило `data-val-required` проверки &quot;клиента генерирует атрибут&quot;и требуется поле City. Запустите приложение, отодвите одного `City` из пользователей и очистите поле. При вывозе вкладки из поля вы видите сообщение об ошибке проверки клиента.

![Город требуется](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Аналогичным образом, для каждого параметра в правиле проверки клиента `data-val-rulename-paramname=paramvalue`добавляется атрибут, который имеет форму. Например, `FirstName` свойство аннотировано атрибутом [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) и определяет минимальную длину 3 и максимальную длину 8. Названо `length` правило проверки данных `max` с именем параметра и значением параметра 8. Ниже отображается HTML, который `FirstName` генерируется для поля при отобрасвании одного из пользователей:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Для получения дополнительной информации о ненавязчивой проверки клиента, см запись [Ненавязчивая проверка клиента в ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) в блоге Брэда Уилсона.

> [!NOTE]
> В ASP.NET MVC 3 Beta, иногда необходимо представить форму для того, чтобы начать проверку на стороне клиента. Это может быть изменено для окончательного выпуска.

## <a name="creating-the-create-view"></a>Создание представления о создании

Следующим шагом является добавление `Create` метода действия и представления, чтобы пользователь мог создать нового пользователя. Добавьте `Create` следующий метод к домашнему контроллеру:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Добавьте представление, как в предыдущих шагах, но установите **содержимое view** для **создания.**

![Создание представления](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Запустите приложение, выберите ссылку **«Создать»** и добавьте нового пользователя. Метод `Create` автоматически использует проверку на стороне клиента и сервера. Попробуйте ввести имя пользователя, содержащее белое пространство, например &quot;Бен X&quot;. При выражаемеименно из поля имени пользователя отображается ошибка проверки на стороне клиента ()`White space is not allowed`

## <a name="add-the-delete-method"></a>Добавить метод удаления

Чтобы завершить обучение, добавьте следующий `Delete` метод в домашний контроллер:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Добавьте `Delete` представление, как и в предыдущих шагах, установив **содержимое View** для **удаления.**

![Удалить представление](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Теперь у вас есть простой, но полностью функциональный ASP.NET mVC 3 приложение с проверкой.
