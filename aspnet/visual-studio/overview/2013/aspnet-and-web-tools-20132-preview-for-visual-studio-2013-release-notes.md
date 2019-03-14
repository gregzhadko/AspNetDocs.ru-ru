---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET и Web Tools 2013.2 для заметки о выпуске Visual Studio 2013 | Документация Майкрософт
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 2a22c5b686cb8e02054f421f78a8fc910af7ce28
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062741"
---
<a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Заметки о выпуске ASP.NET and Web Tools 2013.2 для Visual Studio 2013
====================
по [Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>Замечания по установке

ASP.NET and Web Tools для Visual Studio 2013.2 объединяются в основной установки и можно загрузить как часть [Visual Studio 2013 с обновлением 2](https://go.microsoft.com/fwlink/?LinkId=390521).

## <a name="documentation"></a>Документация

Учебники и другие сведения о ASP.NET and Web Tools для Visual Studio 2013.2 доступны из [веб-сайт ASP.NET](https://www.asp.net/).

## <a name="software-requirements"></a>Требования к программному обеспечению

ASP.NET and Web Tools для Visual Studio 2013.2 требуется Visual Studio 2013.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Новые возможности в ASP.NET and Web Tools для Visual Studio 2013.2

Ниже описаны возможности, представленные в выпуске.

- [Шаблоны одного проекта ASP.NET](#oneaspnet)
- [Поддерживает SSL, при запуске веб-приложений на IIS Express](#ssl)
- [Усовершенствования редактора Visual Studio Web](#vswebeditor)
- [Привязывание к браузеру](#browserlink)
- [Поддержка веб-приложений службы приложений Azure в Visual Studio](#waws)
- [Создать удаленные ресурсы Azure, при создании нового веб-проекта](#AzureResources)
- [Веб-публикация усовершенствования](#webpublish)
- [Формирование шаблонов ASP.NET](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [Веб-форм ASP.NET](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [Веб-API 2.1.2 ASP.NET](#webapi)
- [ASP.NET Web Pages 3.1.2](#webpages)
- [Платформа Entity Framework 6.1](#ef)
- [Удостоверение ASP.NET 2.0.0](#identity)
- [Компоненты Microsoft OWIN](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Шаблоны одного проекта ASP.NET

- Обновления для шаблонов проекта ASP.NET для поддержки подтверждение учетной записи и сброса пароля.
- Обновите шаблон веб-API ASP.NET для поддержки проверки подлинности с помощью на локальных учетных записей организации.
- Шаблон ASP.NET SPA теперь содержит проверку подлинности, основанный на стороне представлений MVC и сервера. Шаблон содержит контроллер веб-API, который может осуществляться только прошедших проверку подлинности пользователей.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>Поддерживает SSL, при запуске веб-приложений на IIS Express

Чтобы устранить предупреждение безопасности при просмотре и отладке HTTPS на локальном узле, мы добавили диалоговое окно, чтобы разрешить Internet Explorer и Chrome доверенным самозаверяющий IIS express SSL-сертификат.

Например свойство проекта web можно задать использование протокола SSL. Нажмите клавишу F4, чтобы открыть диалоговое окно свойств. Изменение **протокол SSL включен** значение true. Скопируйте URL-адрес SSL.

![Протокол SSL включен, свойство](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

Набор web проекта страницы web вкладки со свойствами для использования протокола HTTPS на основе URL-адрес (URL-адрес SSL будет `https://localhost:44300/` Если вы уже создали веб-сайтов SSL.)

![Задать URL-адрес проекта (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Нажмите CTRL+F5, чтобы запустить приложение. Следуйте инструкциям, чтобы доверять самозаверяющий сертификат, созданный IIS Express.

![Предупреждение о SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Чтение **предупреждение системы безопасности** диалоговое окно, а затем нажмите кнопку **Да** Если вы хотите установить сертификат, представляющий localhost.

![Предупреждение системы безопасности](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

Узел будет отображен в IE или Chrome без предупреждения о сертификате в браузере.

![Страницы HTTPS без предупреждения](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox использует собственное хранилище сертификатов, поэтому он будет отображаться предупреждение.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Усовершенствования редактора Visual Studio Web

- **Новые элементы JSON и редактор**: Мы добавили элемент проекта JSON и редактора Visual Studio. Актуальные функции редактора JSON включают выделение цветом, проверки синтаксиса, завершение скобок, структурирование, параметр средства и многое другое.

    ![Редактор JSON](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    Теперь поддерживает IntelliSense [схему JSON](http://json-schema.org/) v3 и v4. Нет схемы поле со списком для выбора существующих схем, изменить путь локальной схемы, или просто перетаскивании JSON в файл проекта его, чтобы получить относительный путь.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![Редактор схем JSON](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Новый редактор Sass (SCSS)**: Мы добавили меньше в VS2013 RTM, и теперь у нас есть элемент проекта Sass и редактор. Редактор sass функции сравнимы для редактора LESS и включают в себя раскраску, переменной и Примеси IntelliSense, закомментируйте или раскомментируйте код, краткие сведения, форматирование, проверки синтаксиса, структурирование, перейти к определению, палитра цветов "Сервис" параметр д.

    ![Добавление нового элемента: Таблица стилей SCSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Редактор таблиц стилей.](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **Новое средство выбора URL-адрес в формате HTML, Razor, CSS, LESS и Sass документов:** Visual STUDIO 2013, поставляемых с не Выбор URL-адреса за пределами страницы веб-форм. Новое средство выбора URL-адрес для HTML, Razor, CSS, LESS и Sass редакторы — это бесплатный диалоговое окно, fluent выбора ввода, которое понимает ".." и файл фильтров соответствующим образом список тегов img и ссылки.

    ![Выбор URL-адреса для тега изображения](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Выбор URL-адреса для представлений](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![Выбор URL-адреса для CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Обновления для редактора LESS, добавляя дополнительные возможности**
- **Обновление маскирования Intellisense**: Мы добавили нестандартный синтаксис KnockOut для VS intelliSense «ko-vs редактор viewModel:» синтаксис. Его можно использовать для привязки к несколько моделей представления на странице с помощью комментариев в форме.

    ![Knockout Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    Мы также добавили поддержку для IntelliSense, вложенные ViewModel, поэтому вы можете более подробно глубоко вложенных объектов в модели представления.

    `<div data-bind="text: foo.bar.baz.etc" />`

    IntelilSense отображается имеет полную поддержку технологии IntelliSense JavaScript-объекта.

    ![IntelliSense, отображение полный объект JavaScript](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **Новое средство выбора URL-адрес в формате HTML, Razor, CSS, LESS и Sass документов**: Visual STUDIO 2013, поставляемых с не Выбор URL-адреса за пределами страницы веб-форм. Новое средство выбора URL-адрес для HTML, Razor, CSS, LESS и Sass редакторы — это бесплатный диалоговое окно, fluent выбора ввода, которое понимает ".." и файл фильтров соответствующим образом список тегов img и ссылки.

    ![Выбор URL-адреса для тега изображения](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Выбор URL-адреса для представлений](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![Выбор URL-адреса для CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Привязывание к браузеру

- Связь с браузером теперь поддерживает подключения по протоколу HTTPS и будут отображаться, на панели мониторинга вместе с другими подключениями до тех пор, пока сертификат является доверенным для браузера.
- Сопоставление источника статический HTML
- SPA поддерживает сопоставление данных
- Сопоставление автоматического обновления данных

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Поддержка веб-приложений службы приложений Azure в Visual Studio

- **Поддержка Azure войдите.**
- **Удаленная отладка и удаленное представление для веб-приложений**: Теперь мы поддерживаем [удаленной отладки для веб-приложений в службе приложений Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) и удаленное представление содержимого файлов веб-приложения в обозревателе серверов.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Создать удаленные ресурсы Azure, при создании нового веб-проекта

Мы добавили Azure [«Создать удаленные ресурсы»](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) флажок на диалоговое окно создания веб-приложения. Выбрав его, можно интегрировать возможности создания нового веб-приложения Azure публикации узла для тестирования и создания профиля публикации, выполнив несколько простых шагов.

![Новый проект с ресурсами Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Публикация в Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Веб-публикация усовершенствования

- Улучшить взаимодействие с пользователем для публикации.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>Формирование шаблонов ASP.NET

- **Поддержка перечисления:** Если модель использует перечисления, шаблон MVC создаст раскрывающийся список для перечисления. При этом используются методы перечисления, помеченные в MVC.
- **Начальная загрузка поддержки**: Обновили шаблоны EditorFor в формирование шаблонов MVC, чтобы они используют классы начальной загрузки.
- **Пакет поддержки**: MVC и средств формирования шаблонов Web API добавляются 5.1 пакеты для MVC и веб-API

Далее на снимках экрана показано формирование шаблонов моделей.

- Код модели:

     ![Модель кода](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Скомпилируйте код модели, щелкните правой кнопкой мыши и выберите **добавить**, **создать шаблонный элемент**.

     ![Добавить новый шаблонный элемент](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- Выберите **контроллер MVC 5 с представлениями, использующий Entity Framework**:

     ![Добавить новый контроллер MVC 5 с представлениями](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **Добавление контроллера** с помощью модели:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Проверьте созданный код, например, содержит Views/WeekdayModels/Edit.cshtml `@Html.EnumDropDownListFor`: ![Представление, содержащее EnumDropDownListFor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- Запустите эту страницу, чтобы просмотреть созданные поля со списком перечисления, обратите внимание на то, что если значение может иметь значение null, пустую строку можно выбрать для поля со списком. Например **создать** странице отображаются следующие:

    ![Поле со списком, позволяя пустая строка](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1, RTM будет выпущена в апреле 2014 г. Ниже приведены ключевые моменты в заметках о выпуске, но проверьте [заметки о полном выпуске](http://docs.nuget.org/docs/release-notes/nuget-2.8) Дополнительные сведения об этих изменениях.

- **Целевой объект Windows Phone 8.1 приложений**: NuGet 2.8.1 теперь поддерживает, предназначенных для Windows Phone 8.1 приложений, с помощью моникеров целевой платформы «WindowsPhoneApp», «WPA», «WindowsPhoneApp81» и «WPA81».
- **Исправление разрешения для зависимостей**: При разрешении зависимостей пакета, NuGet Исторически реализовала стратегии выбора самую раннюю версию основной и дополнительный пакет, который удовлетворяет зависимостям для пакета. В отличие от основной и вспомогательной версии Однако версия исправления всегда разрешения до последней версии. На то, что поведение было намерениями, он создан отсутствия детерминизм для установки пакетов с зависимостями.
- **Коммутатор DependencyVersion**: Хотя изменяет NuGet 2.8 *по умолчанию* поведение для разрешения зависимостей, он также добавляет более точно контролировать процесс разрешения зависимостей с помощью параметра - DependencyVersion в консоли диспетчера пакетов. Параметр включает разрешение зависимостей для возможных самую раннюю версию (поведение по умолчанию), максимально возможный номер версии, или наивысший minor или версию исправления. Этот параметр работает только для install-package в команду powershell.
- **Атрибут DependencyVersion**: Помимо параметра - DependencyVersion, рассмотренных в выше, NuGet также разрешил для возможности, чтобы задать новый атрибут в файле nuget.config определение что такое значение по умолчанию, если не указан параметр - DependencyVersion при вызове install-package. Это значение будет соблюдаться также в диалоговом окне диспетчера пакетов NuGet для всех операций установки пакета. Чтобы задать это значение, добавьте атрибут ниже в файл nuget.config.

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **Просмотр операций NuGet с помощью - whatif**: Некоторые пакеты NuGet могут иметь графами глубокой зависимости, и таким образом, он может пригодиться во время установки, удалить или обновить операцию, чтобы сначала посмотреть, что произойдет. NuGet 2.8 добавляет стандартный интерфейс PowerShell — что делать, если переключиться в режим команды install-package, удалите пакет и пакет обновления для включения визуализации всей замыкание пакетов, к которым применяется команда.
- **Понизить версию пакета**: Нередко установить предварительную версию пакета, чтобы изучить новые функции, а затем решить выполнить откат до последней стабильной версии. До NuGet 2.8 это было многоэтапный процесс, при удалении предварительной пакет и его зависимости, и последующая установка более ранней версии. С помощью NuGet 2.8 тем не менее, пакет обновления теперь откатит замыкание весь пакет (например дерево зависимостей пакета) к предыдущей версии.
- **Зависимости разработки**: Множество различных возможностей могут доставляться в виде пакетов NuGet - в том числе средства, которые используются для оптимизации процесса разработки. Эти компоненты, хотя они могут быть очень важна при разработке нового пакета, не должен считаться опубликованные зависимость нового пакета, находящегося в более поздней версии. NuGet 2.8 позволяет пакету для собственной идентификации в качестве developmentDependency файла nuspec. При установке, эти метаданные также будут добавляться в файл packages.config проекта, в которую был установлен пакет. Если этот файл packages.config позже проанализировать зависимости NuGet во время пакет nuget.exe, исключает эти зависимости, которые помечены как зависимости разработки.
- **Файлы отдельных packages.config для различных платформ**: При разработке приложений для нескольких целевых платформ, это часто используются для каждой из сред сборки в соответствующих файлах разных проектов. Также часто бывает для получения различных пакетов NuGet в разных файлах проекта, так как пакеты имеют различные уровни поддержки для различных платформ. NuGet 2.8 обеспечивает улучшенную поддержку для этого сценария, создавая другой packages.config файлов для файлов разных проекта под конкретную платформу.
- **Откат к локальным кэшем**: Хотя пакеты NuGet обычно используются такие как из удаленной коллекции [коллекции NuGet](http://www.nuget.org) использования сетевого подключения, существует множество сценариев, где клиент не подключен. Без подключения к сети клиент NuGet не удалось успешно установить пакеты - даже в том случае, если эти пакеты уже были на клиентском компьютере в локальном кэше NuGet. NuGet 2.8 добавляет автоматического Резервный кэш консоли диспетчера пакетов.

    Функции резервного кэша не требуют аргументов определенную команду. Кроме того резервный кэш в настоящее время работает только в консоли диспетчера пакетов - поведение не работает в данный момент в диалоговом окне диспетчера пакетов.
- **Исправления ошибок**: Одним из основных ошибок исправления, внесенные было улучшение производительности в пакете обновления-переустановить команды.

    Помимо этих возможностей и исправления производительности, упомянутых выше этот выпуск NuGet также включает много исправлений ошибок. Возникали 181 общее проблемы, описанной в выпуске. Полный список рабочих элементов исправленные в NuGet 2.8 обратитесь представление [NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) для этого выпуска.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>Веб-формы ASP.NET

- Шаблоны Web Forms теперь Показать инструкции по выполнению подтверждение учетной записи и сброса пароля для ASP.NET Identity.
- Элемент управления источника данных Entity и динамических данных поставщик Entity Framework 6. Дополнительные сведения см. в блоге MSDN: [Поставщик динамических данных и управления EntityDataSource для Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Атрибут улучшения маршрутизации](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Поддержка начальной загрузки для редактора шаблонов](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Поддержке нумераций в представлениях](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Поддержка Unobstrusive MinLength / MaxLength атрибуты](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Поддержка «this» контекст в ненавязчивого Ajax](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Различные [исправления ошибок](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>Веб-API 2.1.2 ASP.NET

- [Обработки глобальных ошибок](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Атрибут расширения маршрутизации](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Усовершенствования на странице справки](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [Поддержка IgnoreRoute](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [Модуль форматирования типа мультимедиа BSON](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Улучшенная поддержка async фильтры](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [Синтаксический анализ для клиента форматирование библиотеки запроса](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Различные [исправления ошибок](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web Pages 3.1.2

- Различные [исправления ошибок](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Платформа Entity Framework 6.1

Платформа Entity Framework был обновлен до версии 6.1 для среды выполнения и инструментов. Entity Framework (EF) 6.1 представляет собой незначительное обновление для платформы Entity Framework 6 и включает ряд исправлений и новых функций. Подробные сведения о EF6.1, включая ссылки на документацию для новых функций, см. в разделе [журнал версий Entity Framework](https://msdn.microsoft.com/data/jj574253). Новые возможности в этом выпуске:

- **Средства консолидации** предоставляет согласованный способ создания новой модели EF. Эта функция расширяет мастер модели EDM ADO.NET для поддержки создания моделей Code First, включая реконструирование из существующей базы данных. Эти функции ранее были доступны в бета-версии качества в EF Power Tools.
- **Обработка сбоев фиксации транзакции** предоставляет новые [System.Data.Entity.Infrastructure.CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) использующий новых способность перехватывать операции транзакции. **CommitFailureHandler** обеспечивает автоматическое восстановление после сбоев подключения во время фиксации транзакции.
- **IndexAttribute** позволяет индексы, чтобы указать, разместив атрибут в свойство (или свойства) в модели Code First. Код сначала создаст соответствующий индекс в базе данных.
- **Сопоставление общедоступного API** предоставляет доступ к сведениям, имеет EF в сопоставлении свойств и типов, со столбцами и таблицами в базе данных. В предыдущих версиях этот API был внутренней.
- **Возможность настройки перехватчики посредством файла App/Web.config**(позволяя перехватчики должен быть добавлен без повторной компиляции приложения).
- **DatabaseLogger** — это новый interceptor, который упрощает процесс в журнал всех операций базы данных в файл. В сочетании с предыдущей функции это позволяет легко переключаться на протоколирование операций базы данных для развернутого приложения, без необходимости повторной компиляции.
- **Обнаружение изменений модели миграций** была улучшена так, чтобы точнее; производительность процесса обнаружения изменений также была значительно улучшена шаблонный миграций.
- **Повышение производительности** включая операции ограниченной базы данных во время инициализации, оптимизации для сравнения на равенство null в запросах LINQ, быстрее Просмотр поколения (Создание модели) в различных сценариях и эффективнее Материализация отслеживаемые сущности с несколькими связями.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>Удостоверение ASP.NET 2.0.0

- **Двухфакторная проверка подлинности**: ASP.NET Identity теперь поддерживает двухфакторную проверку подлинности. Двухфакторная проверка подлинности обеспечивает дополнительный уровень безопасности, учетных записей пользователей в случае, когда пароль будет нарушена. Имеется также защиту для подбора против двухфакторные коды.
- **Блокировка учетной записи:** Предоставляет способ блокировки записи пользователя, если пользователь вводит свой пароль или коды двухфакторной неправильно. Число попыток и интервал времени для заблокированных пользователей можно настроить. Разработчик может при необходимости отключить блокировку учетных записей для определенных учетных записей пользователей они нужно.
- **Подтверждение учетной записи:** Системы удостоверений ASP.NET теперь поддерживает подтверждение учетной записи. Это довольно распространенный сценарий в большинстве веб-сайты уже сегодня, where, при регистрации новой учетной записи на веб-сайт, необходимо подтвердить свой адрес электронной почты, перед выполнением любого элемента в веб-сайта. Подтверждение по электронной почте полезен, так как он предотвращает создание фиктивный учетных записей. Это очень полезно в том случае, если вы используете адрес электронной почты как метод взаимодействия с пользователями вашего веб-сайта, таких как форум сайтов банковских операций, электронной коммерции и социальных веб-сайтов.
- **Сброс пароля:** Пароль сброса — это компонент, где пользователь может сбрасывать свои пароли, если они забыли свой пароль.
- **Метка безопасности (вход, выход на всех устройствах):** Поддерживает способ повторно создать маркера безопасности для пользователя в случаях, когда пользователь изменяет пароль или любые другие безопасности связанные сведения, такие как удаление связанного имени для входа (например, Facebook, Google, учетной записи Майкрософт и т. д.). Это необходимо, чтобы убедиться, что делает недействительными все токены, созданные с помощью старого пароля. В образце проекта при изменении пароля для пользователя будет создан новый маркер затем становятся недействительными все предыдущие токены. Эта функция обеспечивает дополнительный уровень безопасности для приложения с момента при изменении пароля, вы выйдете из everywhere (для всех остальных браузерах) где был выполнен вход в это приложение.
- **Сделайте тип первичного ключа, с возможностью расширения для пользователей и ролей**: В ASP.NET 1.0 удостоверений тип первичного ключа таблицы пользователям и ролям была строк. Это значит, что системы удостоверений ASP.NET был сохранен в SQL Server с помощью Entity Framework, мы использовали nvarchar. Было много групповых обсуждениях на тему Эта реализация по умолчанию на сайте Stack Overflow и на основе входящих отзывов. Мы предоставили обработчик расширений, где можно указать, что должен быть первичный ключ таблицы пользователей и ролей. Этот обработчик расширения особенно полезен, если вы переносите приложение и приложение было хранение недопустимость являются идентификаторами GUID или целых чисел.
- **Поддерживает IQueryable о пользователях и ролях**: Добавлена поддержка для IQueryable UsersStore и RolesStore можно легко получить список пользователей и ролей.
- **Поддерживает операции удаления с помощью UserManager**
- **Индексирование на имя пользователя**: В реализации ASP.NET Identity Entity Framework мы добавили уникальный индекс на имя пользователя с помощью нового IndexAttribute в EF 6.1.0. Это гарантирует, что имена пользователей всегда уникальны и возникла не гонки, в котором вы может получиться повторяющихся имен пользователей.
- **Проверяющий элемент управления улучшенные паролей:** Пароль проверяющий элемент управления, который отправлен в ASP.NET Identity 1.0 был одну функцию пароль проверяющий элемент управления, который только проверка Минимальная длина. Имеется новый пароль проверяющий элемент управления, дает больший контроль над сложность пароля. Обратите внимание на то, что даже если вы включите все параметры в этот пароль, мы рекомендуем включить двухфакторную проверку подлинности для учетных записей пользователей.
- **По промежуточного слоя IdentityFactory / CreatePerOwinContext**:

    - **Диспетчер пользователей**: Реализация фабрики можно использовать для получения экземпляра UserManager из контекст OWIN. Этот шаблон похож на использование по получению AuthenticationManager из контекст OWIN для SignIn и SignOut. Это рекомендуемый способ получения экземпляра UserManager каждого запроса для приложения.
    - **DbContextFactory**: ASP.NET Identity использует Entity Framework для сохранения системы идентификации в SQL Server. Для этого система идентификации содержит ссылку на ApplicationDbContext. По промежуточного слоя DbContextFactory возвращает экземпляр ApplicationDbContext каждого запроса, который можно использовать в приложении.
- **Пакет NuGet примеры удостоверения ASP.NET**: Пакет NuGet примеры можно упростить его установки и выполнение примеров для ASP.NET Identity и следуйте этим рекомендациям. Ниже приведен пример приложения ASP.NET MVC. Измените код в соответствии с приложения, перед ее развертыванием в рабочей среде. Образец должен быть установлен в пустое приложение ASP.NET. Дополнительные сведения о пакете перейдите к следующей записи блога: [Объявление о выпуске RTM удостоверения ASP.NET 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Компоненты Microsoft OWIN

Было много ошибок, исправленных в этом выпуске. См. в разделе [заметки о выпуске для 2.1.0 выпуска](https://katanaproject.codeplex.com/releases/view/113281) более подробные сведения.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

Было много ошибок, исправленных в этом выпуске. См. в разделе [заметки о выпуске для 2.0.2 выпуска](https://github.com/SignalR/SignalR/releases/tag/2.0.2) более подробные сведения.