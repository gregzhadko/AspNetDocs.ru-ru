---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET и веб-инструменты 2012.2 Примечания к выпуску (ru) Документы Майкрософт
author: rick-anderson
description: Выпуск примечаний для ASP.NET и Web Tools 2012.2.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675907"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET и веб-инструменты 2012.2 — заметки о выпуске

> В этом документе описывается выпуск ASP.NET и Web Tools 2012.2. Это обновление для Визуальной студии веб-инструментирования и ASP.NET.

- [Примечания к установке](#_Installation)
- [Документация](#_Documentation)
- [Поддержка](#_Support)
- [Требования к программному обеспечению](#_Software_Requirements)
- [Новые функции в ASP.NET и веб-инструменты 2012.2](#_New_Features_in)

    - [Инструменты](#_Tooling)
    - [Веб-издательство](#_Web_Publishing)
    - [ASP.NET шаблоны MVC](#_Templates)
    - [Веб-API ASP.NET](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET Friendly URLs](#_ASP.NET_Friendly_URLs)
- [Известные проблемы и ломая изменения](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Замечания по установке

ASP.NET и web Tools 2012.2 для Visual Studio 2012 может быть установлен с помощью [установщика веб-платформы.](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2) Это обновление для Visual Studio 2012 или Visual Studio Express 2012 для Интернета, который требуется. Если у вас нет визуальной студии установлен, Visual Studio Express 2012 для Интернета будет установлен.

Вы также можете установить ASP.NET и web Tools 2012.2 вручную. Вы должны иметь Visual Studio 2012 или Visual Studio Express 2012 для веб-установки. Затем используйте следующие инструкции: 

1. Скачать [ASP.NET и веб-рамки 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) установщик из Скачать центр.
2. При нажатии кнопки Run. Вы также можете сохранить файл, чтобы запустить его позже.
3. Проверьте версию Visual Studio вы будете обновлять. Вы можете сделать это, запустив Visual Studio вы хотите обновить. Затем нажмите пункт меню справки.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Если вы видите &quot;пункт меню о Microsoft Visual&quot; Studio 2012 для Интернета, то скачать [Веб-разработчик Инструменты 2012.2 - Visual Studio Express 2012 для Интернета](https://go.microsoft.com/fwlink/?LinkID=282228). В противном случае скачать [веб-разработчик Инструменты 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. При нажатии кнопки Run. Вы также можете сохранить файл, чтобы запустить его позже.

> [!NOTE]
> ASP.NET и Web Tools 2012.2 не включает в себя инструменты для данных серверов S'L. Базы данных S'L Server и Windows Azure S'L предоставляют более богатый набор инструментов баз данных, включая автономные разработки, поддерживаемые проектами, сравнение схем и расширенные возможности развертывания баз данных. Для получения более подробной информации [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)или для установки инструментов данных серверов S'L посетите веб-сайт .

<a id="_Documentation"></a>
## <a name="documentation"></a>Документация

Учебники и другая информация о ASP.NET и Web Tools 2012.2 можно получить на веб-сайте ASP.NET ( . https://www.asp.net)

<a id="_Support"></a>
## <a name="support"></a>Поддержка

ASP.NET и Web Tools 2012.2 официально выпущен и поддерживается. Вы можете использовать свой обычный канал поддержки. Вы также можете отправлять вопросы[https://forums.asp.net/](https://forums.asp.net/)на ASP.NET форумах (), где члены ASP.NET сообщества часто могут оказывать неофициальную поддержку.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Требования к программному обеспечению

ASP.NET и веб-инструменты 2012.2 требует Visual Studio 2012 или Visual Studio Express 2012 для Интернета.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>Новые функции в ASP.NET и веб-инструменты 2012.2

В этом разделе описаны функции, которые были представлены в выпуске ASP.NET и Web Tools 2012.2.

<a id="_Tooling"></a>
### <a name="tooling"></a>Инструменты

- Инспектор страниц 

    - Поддержка отображения выбора JavaScript, позволяющая инспектору страницы отображывать элементы, которые были динамически добавлены на страницу, к соответствующему коду JavaScript.
    - Возможность просмотра обновлений CSS в режиме реального времени.
    - Для получения дополнительной информации, прочитайте [CSS Auto-Sync и JavaScript Выбор Картирование в Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).
- Редактор 

    - Поддержка синтаксиса выделения для CoffeeScript, усы, рулькбар, и JsRender.
    - HTML-редактор предоставляет Intellisense для привязки Knockout.
    - Поддержка редактирования и компилятора LESS для обеспечения динамического CSS с использованием LESS.
    - Вставьте JSON как класс .NET. Используя эту специальную команду Пасты для вставки JSON в файл кода C- или VB.NET, и Visual Studio будет автоматически генерировать классы .NET, выведенные из JSON.
- Поддержка мобильного эмулятора добавляет расширяемость крючков, так что сторонние эмуляторы могут быть установлены в качестве VSIX. Установленные эмуляторы будут отображаться в F5 dropdown, так что разработчики могут просматривать свои веб-сайты на различных мобильных устройствах. Узнайте больше об этой функции в блоге Скотта Hanselman запись о [новой интеграции BrowserStack с Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Веб-издательство

- Проекты веб-узлов теперь имеют тот же опыт публикации, что и проекты Web-приложений, включая публикацию на веб-сайтах Windows Azure.
- Селективное опубликовать &#8211; для одного или нескольких файлов, которые можно выполнить следующие действия (после публикации в конечную точку Web Deploy): 

    - Публикация выбранных файлов.
    - Узнайте разницу между локальным файлом и удаленным файлом.
    - Обновление локального файла с помощью удаленного файла или обновление удаленного файла с помощью локального файла.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET шаблоны MVC

- Новый шаблон приложения Facebook упрощает создание приложений Facebook Canvas. Всего за несколько простых шагов можно создать приложение Facebook, получающее данные от выполнившего вход пользователя и передающего их его друзьям. Шаблон содержит новую библиотеку, предназначенную для выполнения любых операций по проектированию приложений Facebook, включая проверку подлинности, разрешения, доступ к данным Facebook и многое другое. Для получения дополнительной информации об [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)использовании шаблона приложения Facebook см.
- С помощью нового шаблона одностраничного приложения MVC разработчики могут создавать интерактивные клиентские веб-приложения, применяя в веб-API ASP.NET код HTML 5 и CSS 3, а также используя популярные библиотеки Knockout и jQuery JavaScript. Шаблон включает в себя приложение списка "todo", которое демонстрирует общие практики создания приложения JavaScript HTML5, использующему API сервера RESTful. Вы можете прочитать больше на [https://www.asp.net/single-page-application](../../../single-page-application/index.md).
- Теперь можно создать VSIX, который добавляет новые шаблоны в диалог ASP.NET MVC New Project. Узнайте, как здесь:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- Пакет FixedDisplayModes &#8211; шаблоны проектов MVC были обновлены, чтобы включить новый пакет NuGet 'FixedDisplayModes', который содержит обходной путь для ошибки в MVC 4. Для получения дополнительной информации о исправлении, содержащемся в пакете, обратитесь к этому сообщению в блоге ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) от команды MVC.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>Веб-API ASP.NET

ASP.NET Web API был дополнен несколькими новыми функциями:

- ASP.NET Web API OData
- ASP.NET веб-aPI Tracing
- ASP.NET страница справки Web API

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData дает вам гибкость, необходимую для построения конечных точек OData с богатой бизнес-логикой над любым источником данных. С ASP.NET Web API OData вы контролируете количество семантики OData, которую вы хотите разоблачить. ASP.NET Web API OData включен в ASP.NET шаблоны проекта MVC 4, а также доступен в NuGet ().[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)

ASP.NET Web API OData в настоящее время поддерживает следующие функции:

- Включить семантику запроса OData, применяя атрибут «Квирайируемый».
- Легко проверить запросы OData и ограничить набор поддерживаемых параметров запроса, операторов и функций.
- Параметр привязывается к OData-КуэриОпции непосредственно, чтобы получить абстрактное представление дерева синтаксиса запроса, которое затем может быть проверено и применено к I'E'E'eeable или IEnumerable.
- Включите прокладку на основе службы и следующее поколение ссылок страниц, указав ограничения на результат ы на атрибуте «Квирайируемый».
- Запросить подстойное количество общих ресурсов, использующих $inlinecount.
- Контроль нулевого распространения.
- Любые/Все операторы в $filter.
- Вывод модели данных сущности по конвенции или явно настраивайте модель таким же образом, как и Рамочный кодекс сущности-первый.
- Экспонировать наборы сущности, вытекающие из EntitySetController.
- Простые, настраиваемые конвенции для раскрытия навигационных свойств, манипулирования ссылками и реализации действий OData.
- Упрощенная маршрутизм с использованием метода расширения MapODataRoute.
- Поддержка версий путем разоблачения нескольких моделей EDM.
- Выставлять документы службы и $metadata, чтобы вы могли создавать клиентов (.NET, Windows Phone, Магазин Windows и т.д.) для вашего Web API.
- Поддержка многословных форматов OData Atom, JSON и JSON.
- Создавайте, обновляйте, частично обновляйте (PATCH) и удаляйте сущности.
- Запрос и манипулирование отношениями между сущностями.
- Создавайте ссылки на связи, которые подсваивают сява к вашим маршрутам.
- Сложные типы.
- Наследие типа entity.
- Свойства коллекции.
- Перечисления.
- Действия OData.
- Построенный на том же основании, что и[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)WCF Data Services, а именно ODataLib ( ).

Для получения дополнительной информации о [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)ASP.NET Веб API OData см.

#### <a name="aspnet-web-api-tracing"></a>ASP.NET веб-aPI Tracing

ASP.NET Web API Tracing интегрирует отслеживая данные из веб-aPI с помощью .NET Tracing. Теперь он включен по умолчанию в шаблоне проекта Web API. Отслеживание данных для веб-AI отправляется в окно вывода и становится доступным через IntelliTrace. ASP.NET Web API Tracing позволяет отслеживать информацию о вашем Web API при размещении на Windows Azure через интеграцию с [Windows Azure Diagnostics.](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx) Вы также можете установить и включить ASP.NET веб-aPI Tracing в любом[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)приложении с помощью пакета ASP.NET Web API Tracing NuGet ().

Для получения дополнительной информации о настройке и [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)использовании ASP.NET веб-aPI Tracing см.

#### <a name="aspnet-web-api-help-page"></a>ASP.NET страница справки Web API

Страница справки ASP.NET Web API теперь включена по умолчанию в шаблон проекта Web API. Страница справки ASP.NET Web API автоматически генерирует документацию для web-aPI, включая конечные точки HTTP, поддерживаемые методы HTTP, параметры и пример ый запрос и полезную нагрузку сообщения ответа. Документация автоматически извлекается из комментариев в коде. Вы также можете добавить ASP.NET Web API Справка Страница для любого[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)приложения, используя ASP.NET Web API Справка Страница NuGet пакет ( ).

Для получения дополнительной информации о настройке и настройке страницы справки Web API смотрите [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)ASP.NET страницы справки Web API:

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR упрощает добавление веб-возможностей в режиме реального времени в ASP.NET приложение, используя WebSockets при наличии webSockets и автоматически возвращаясь к другим методам, когда это не так.

Для получения дополнительной информации [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)об использовании ASP.NET SignalR см.

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Friendly URLs

ASP.NET FriendlyURL делает его очень легким для веб-форм разработчиков для создания более чистых перспективных URL-адресов (без расширения .aspx). Она требует практически никакой конфигурации и может быть использована с существующими приложениями ASP.NET v4.0. Функция FriendlyURL также упрощает для разработчиков добавление мобильной поддержки в свои приложения, поддерживая переключение между настольными и мобильными представлениями.

Для получения дополнительной информации об установке [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)и использовании ASP.NET дружественных URL-адресов см.

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Известные проблемы и ломая изменения

В этом разделе описаны известные проблемы и изменения, которые есть в ASP.NET и Web Tools 2012.2 релиз.

### <a name="installation-issues"></a>Проблемы с установкой

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Не по заказу устанавливается Visual Studio 2012

Установка дополнительного SKU Visual Studio 2012 после установки ASP.NET и Web Tools 2012.2 потребует ремонта. Рассмотрим следующую последовательность:

1. Установка Визуальной студии 2012 Экспресс для Интернета
2. Установка ASP.NET и веб-инструментов 2012.2
3. Установка Visual Studio 2012 Профессиональная, Премиум или Ultimate

Шаг 2 приведет только к установке обновлений для Express для Интернета. Чтобы убедиться, что дополнительный SKU, установленный во время шага 3, содержит обновление, необходимо отремонтировать ASP.NET и Web Tools 2012.2 для установки обновлений для последнего установленного SKU. Это также применяется, если СКУ в шаге 1 и 3 отменены.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Установка Microsoft ASP.NET и web Tools 2012.2, когда Visual Studio открыта

Если VS открыт во время установки Microsoft ASP.NET и Web Tools 2012.2, Visual Studio может оказаться в плохом состоянии. Рекомендуется, чтобы пользователи закрыли все экземпляры Visual Studio, прежде чем приступить к установке.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Отмена установки ASP.NET и Web Tools 2012.2 в середине установки

Отмена ASP.NET и Web Tools 2012.2 установки в середине установки оставит Visual Studio в плохом состоянии. Для решения этой проблемы следует следующие действия: 

- Нажмите Установка и удаление программ
- Удалите Microsoft ASP.NET и Web Tools 2012.2, если он присутствует.
- Переустановка Microsoft ASP.NET и веб-инструменты 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>После установки ASP.NET и web Tools 2012.2 ASP.NET шаблоны MVC 4 и шаблоны веб-сайта Razor v2 отсутствуют

Установка ASP.NET и Web Tools 2012.2 также удалит все ASP.NET mVC 4 и Razor v2 Web Site шаблонов от Visual Studio 2012.

Обходной путь заключается в ремонте visual Studio 2012 установки для переустановки ASP.NET MVC 4 и Razor v2 веб-сайта шаблонов.

### <a name="tooling-issues"></a>Проблемы с инструментами

#### <a name="nuget-error-reported-during-project-creation"></a>Ошибка NuGet, зарегистрированная при создании проекта

После установки ASP.NET и Web Tools 2012.2 вы можете увидеть следующую ошибку при создании проекта MVC 4

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET и Web Tools 2012.2 корабли NuGet 2.1 и будет модернизировать расширение в Visual Studio 2012. В некоторых случаях установщик VSIX не сможет правильно обновить VSIX. Следующие шаги позволят решить эту проблему:

1. Начало Visual Studio 2012 в качестве администратора
2. Перейти к&gt;инструменты-расширения и обновления и удалить NuGet.
3. Закройте Visual Studio.
4. Перейдите к папке установки ASP.NET и Web Tools 2012.2:

    1. Для визуальной студии 2012: **Файлы программы»Microsoft ASP.NET-ASP.NET Веб Стек-Визуальная студия 2012**
    2. Для Visual Studio 2012 Экспресс для Интернета: **Файлы программы»-Microsoft ASP.NET-ASP.NET Web Stack-Visual Studio Express 2012 для Интернета**
5. Дважды нажмите на NuGet.Tools.vsix, чтобы переустановить NuGet

### <a name="web-api-issues"></a>Проблемы web API

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>Разбор вопросов в $filter и DateTime буквально

OData URI parser не может анализировать частичное время даты буквально правильно. Например, $filter eq datetime'2012-12-31T12:00' не разбор ауто. Обходной путь заключается в использовании полного буквального, $filter-start eq datetime'2012-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData не поддерживает имена нечувствительных свойств.

OData не поддерживает имена нечувствительных свойств в запросах OData и пути odata. Посмотреть рабочие материалы:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Если пользователи имеют различные корпуса на JavaScript стороне клиента и сервера стороны, они, вероятно, столкнется с этой проблемой. Эта проблема является дизайном в протоколе odata. Тем не менее, многие пользователи сообщают об этой проблеме. Чтобы обойти его, пользователи должны исправить свои случаи в URL.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Конвенции по умолчанию OData не поддерживают свойство навигации POST/PUT.

Конвенции по умолчанию OData не поддерживают свойство навигации POST/PUT. Смотрите рабочий пункт [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366). Нам не хватает этой широко используемой конвенции в конвенциях по умолчанию.

Чтобы обойти его, пользователям необходимо расширить новую конвенцию о реукторе, чтобы поддержать его.

### <a name="facebook-template-issues"></a>Вопросы шаблона Facebook

#### <a name="facebook-application-template-only-works-using-net-45"></a>Шаблон приложения Facebook работает только с помощью .NET 4.5

Необходимо выбрать .NET 4.5 в списке отсева из шаблона инфраструктуры в диалоге Нового проекта, чтобы увидеть шаблон приложения Facebook в ASP.NET MVC 4.

#### <a name="real-time-update-controller"></a>Контроллер обновления в реальном времени

Шаблон приложения Facebook позволяет пользователю легко создавать веб-контроллер API для обработки обновлений в режиме реального времени с Facebook. Если машина разработки стоит за NAT, контроллер может не работать без дальнейшей конфигурации сети. Подробности смотрите здесь:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Значения строки запроса противоречат параметрам Facebook OAuth

Следующие поля противоречат URL-адресу диалога Facebook OAuth. Не добавляйте собственные значения строки запроса со следующими\_именами:\_код, ошибка, описание ошибки, причина ошибки.

#### <a name="using-page-inspector-with-facebook-template"></a>Использование Page Inspector с шаблоном Facebook

Вы не можете использовать функцию Page Inspector в Visual Studio 2012 во время отладки приложения Facebook. В настоящее время Инспектор Страницы не поддерживает iframes.

### <a name="single-page-application-template-issues"></a>Вопросы шаблона приложения для одной страницы

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>При обновлении J'ery 1.9/Knockout 2.2.1 при запуске проекта MVC SPA по умолчанию новое элемента Todo не обрабатывается должным образом.

С обновлением J'ery 1.9/Knockout 2.2.1 при запуске проекта MVC SPA по умолчанию новый элемент todo больше не вскакивает сят-к новому пункту Todo после ввода нового элемента Todo в список todo.

Для ссылки [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)обходного решения, и сделать аналогичное исправление следующего кода образца:

Файл todo.model.js  
 функцию тодолист (данные), добавить следующие:  
 **self.isSelected - ko.observable (false);**

функцию todoList.prototype.addTodo, добавьте следующий затемненный текст:  
 **self.isSelected (истинно);**  
 self.newTodoTitle&quot;&quot;();

Файл index.cshtml, добавьте следующий затемненный текст:  
 &lt;форма данных-bind'&quot;представить: addTodo&quot;&gt;  
 &lt;входним&quot;класса "&quot; добавитьTodo типа&quot;" текст&quot; данных-bind"&quot;значение: newTodoTitle, заполнитель: "Введите здесь, чтобы добавить", blurOnEnter: правда, **hasfocus: isSelected**, событие:&quot; /&gt;  
 &lt;/форма&gt;
