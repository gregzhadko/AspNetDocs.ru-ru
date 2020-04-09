---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET доступ к данным - Рекомендуемые ресурсы Документы Майкрософт
author: rick-anderson
description: Эта тема содержит ссылки на ресурсы документации о том, как получить доступ к данным в ASP.NET веб-приложений, в первую очередь с помощью рамочной системы сущности и S'L Se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675787"
---
# <a name="aspnet-data-access---recommended-resources"></a>Доступ к данным ASP.NET. Рекомендуемые ресурсы

> Эта тема содержит ссылки на ресурсы документации о том, как получить доступ к данным в ASP.NET веб-приложений, в первую очередь с помощью рамочной системы сущности и сервера S'L.
> 
> Если вы знаете большой блог, [stackoverflow](http://stackoverflow.com) поток, или любой другой ссылке, которая была бы полезна, [пришлите нам по электронной почте](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) со ссылкой.
> 
> Последнее обновление 4/3/2014

В нем содержатся следующие подразделы:

- [Начало работы с доступом к данным в ASP.NET](#gettingstarted)
- [Использование рамочной системы сущности](#ef)

    - [Использование Рамочного кода сущности во-первых](#cf)
    - [Использование Рамочного кода сущности первых миграций](#efcfmigrations)
    - [Использование базы данных Entity Framework First или Model First (дизайнер EF)](#efdbf)
    - [Загрузка связанных данных в рамках сущности (Ленивая загрузка, загрузка и явная загрузка)](#efrelateddata)
    - [Оптимизация эффективности рамочной системы entity](#optimizingef)
    - [Обработка параллелизма в рамочном приложении Entity](#efconcurrency)
    - [Книги о рамочной системе образований](#efbooks)
    - [Дополнительные ресурсы системы сущностей](#otherefresources)
- [Связывание данных в ASP.NET приложениях web-форм](#wfdatabinding)

    - [Использование Web Форм Модель Связывание](#wfmodelbinding)
    - [Использование управления исходом исходных данных веб-форм](#wfdsc)
    - [Использование web-форм управления на основе связывания данных и привязки к данным](#wfdbc)
- [Работа с базами данных серверов S'L](#sqlserver)

    - [Работа с базами данных S'L Server Express LocalDB](#sslocaldb)
    - [Работа с базами данных серверного экспресса S'L](#sse)
    - [Работа с базой данных Windows Azure S'L](#ssdb)
    - [Выбор между сервером S'L и базой данных Windows Azure S'L](#ssdbchoosing)
- [Работа с системами управления базами данных НоСЗЛ](#nosql)
- [Использование запросов В ASP.NET приложениях](#linq)
- [Использование подмостков динамических данных](#dd)
- [Обеспечение доступа к данным](#securing)
- [Оптимизация производительности доступа к данным](#optimizingdataaccess)
- [Развертывание базы данных](#deploying)
- [Доступ к данным через веб-службу](#webservice)
- [Дополнительные ресурсы](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Начало работы с доступом к данным в ASP.NET

- [Параметры хранения данных (создание облачных приложений в реальном мире с помощью Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Глава электронной книги о разработке для облака. Вводит базы данных NoS'L в качестве альтернативы, которую многие разработчики, знакомые с реляционными базами данных, как правило, упускать из виду. Представляет рекомендации о том, о чем думать при выборе реляционного или НоСЗЛ, или выборе конкретной платформы.
- [ASP.NET параметры доступа к данным](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). Введение в параметры доступа к данным для реляционных баз данных для ASP.NET и рекомендации по выбору платформ и методов доступа, подходящих для вашего сценария.
- [Реляционные базы данных](http://en.wikipedia.org/wiki/Relational_database). Википедия). Если вы не работали с реляционными базами данных, смотрите на этой странице для введения в реляционные термины базы данных и концепций. Для введения в S'L Server, в частности, [см. Работа с базами данных сервера S'L](#sqlserver) позже в этой теме.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Использование рамочной системы сущности

- [Подходы к разработке рамочных систем](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Руководство по выбору подхода к разработке системentity «Первая база данных», «Первая модель» или «Код первый».

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Использование Рамочного кода сущности во-первых

Следующие учебники предлагают загружаемые примеры приложений:

- [Начало работы с EF 6 с использованием MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Охватывает широкий спектр сценариев Рамочного кода сущности, включая миграцию и функции EF 6, такие как устойчивость соединения, перехват команд и асин. Это обновленная версия [серии EF 5 / MVC 4](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Предыдущая серия включает в себя учебник по репозиторию и шаблонам единицы работы, который не включен в новую серию.
- [Введение в ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md). Охватывает более узкий диапазон сценариев Рамочного кода сущности, но выполняет более всеобъемлющую работу по внедрению функций MVC.
- [Привязка модели и веб-формы](https://go.microsoft.com/fwlink/?LinkId=286117). Использует Код Первый в приложении Web Forms.
- [Начало работы с ASP.NET 4.5 веб-форм](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Введение в веб-формы с некоторым освещением Кода во-первых. Использует привязку к модели.
- [Музыкальный магазин MVC](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). Использует Code First в приложении mVC 3 электронной коммерции, которое также реализует членство и авторизацию. Версия MVC и ASP.NET членство (аутентификация и авторизация), используемые здесь, устарели; для получения более актуальной информации о [https://asp.net/identity](https://asp.net/identity)ASP.NET членстве, см.

Другие ресурсы:

- [Система сущности - Код сначала к существующей базе данных](https://msdn.microsoft.com/data/jj200620). Msdn. Видео и пошаговое походе, которые показывают, как использовать Code First с существующей базой данных.
- [Центр разработчиков данных - Система entity](https://msdn.microsoft.com/data/ef). Msdn. В руководстве по документации Entity Framework, созданной и обслуживаемых группой Entity Framework, можно ознакомиться на ссылке [Get Started.](https://msdn.microsoft.com/data/ee712907)

Поэтой те также [книги о рамочной системе и](#efbooks) [дополнительных ресурсах сущности](#otherefresources) позже смотрите в этой теме.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Использование Рамочного кода сущности первых миграций

Большинство учебников Code First, перечисленных выше, охватывают миграции. Смотрите также следующие ресурсы.

- [Веб-развертывание ASP.NET с помощью Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Серия учебников из 2 частей, в рамках которого показано, как использовать code First Migrations для развертывания базы данных.
- [Развертывание приложения «Безопасный ASP.NET MVC 5» с членством, Базой данных OAuth и S'L на веб-узел Windows Azure.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) Microsoft Azure). Как использовать миграции для развертывания данных о членстве и приложениях в Azure.
- [Обзор веб-развертывания для визуальной студии и ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). В разделе **«Настройка развертывания базы данных в визуальной студии» смотрите раздел «Настройка базы данных» (Configuring Database Deployment in Visual Studio),** где можно понять, как код First Migrations интегрирован в функции веб-развертывания Visual Studio.
- [Центр разработчиков данных - Код первых миграций](https://msdn.microsoft.com/data/jj591621) (MSDN). Документация группы по миграции группы «Образование фреймворк».
- [Миграция Screencast серии](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). Блог EF). Три видеона продвинутые темы в Code First Migrations.
- [Код первый миграции с ASP.NET веб-страниц.](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites) Mikesdotnetting блог). Показывает, как использовать миграцию Code First с ASP.NET веб-страниц, поместив контекст данных в проект библиотеки класса Visual Studio.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Использование базы данных Entity Framework First или Model First (дизайнер EF)

- [Начало работы с базой данных Entity Framework 6 Сначала с помощью MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Выполнить скрипт в Server Explorer для создания базы данных, а затем использовать конструктор АСВ для создания модели данных. Показывает, как создавать простые веб-страницы CRUD, а для других функций обработки данных можно следить за одним из учебников Code First, так как все рабочие процессы EF используют тот же API DbContext.

Следующие ресурсы старше. Они полезны, если вы хотите использовать версию 4.0 рамочной системы entity, и вы хотите использовать элемент управления источниками данных для связывания данных в приложении Web Forms.

- [Начало работы с Рамочной системой сущности 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). Показывает, как использовать элемент управления **EntityDataSource.**
- [Продолжение рамочной программы entity](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(показывает, как использовать элемент управления **ObjectDataSource.** Включает в себя учебник по обработке параллелизма, учебник по производительности EF и учебник о том, что нового в EF 4.0.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Обработка связанных данных в рамках сущности (Ленивая загрузка, стремящаяся загрузка и явная загрузка)

- [Чтение соответствующих данных с рамочной системой entity в ASP.NET mVC Application.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) Код во-первых, MVC образца приложения. Показанные методы применяются также к привязке модели Web Forms и рабочему процессу Базы данных.
- [Центр разработчиков данных - Загрузка связанных объектов](https://msdn.microsoft.com/data/jj574232) (MSDN). Документация группы «Система сущности» о загрузке соответствующих данных.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Оптимизация производительности рамочной системы сущности

- [Расширенные рамочные сценарии сущности для ASP.NET приложения.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md) Показывает, как выполнять свои собственные операторы S'L или вызывать собственные сохраненные процедуры, как отключить обнаружение изменений и как отключить проверку при сохранении изменений.
- [Соображения производительности для рамочной структуры 5](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [Соображения производительности (Система entity)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Максимизация производительности с помощью рамочной системы entity в ASP.NET веб-приложении.](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md) Применяется к Рамочной системе 4.0.
- Подробнее об [ASP.NET этом](#optimizingdataaccess) читайте в этой теме.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Обработка параллелизма в рамочном приложении Entity

- [Обработка параллелизма с рамочной системой entity в ASP.NET mVC Application.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) Code First, DbContext API, используя применение образца MVC.
- [Центр разработчиков данных - Оптимистичные шаблоны параллелизма](https://msdn.microsoft.com/data/jj592904) (MSDN). Параллельная документация группы «Система сущности».
- [Обработка параллелизма с рамочной системой entity в ASP.NET веб-приложении.](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md) Применяется к Рамочной системе 4.0. Во-первых, ObjectContext API, используя пример приложения Web Forms.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Книги о рамочной системе образований

- [Программирование Entity Framework: DbContext](http://shop.oreilly.com/product/0636920022237.do) Джули Лерман и Роуэн Миллер.
- [Рамки программирования: Код Первый](http://shop.oreilly.com/product/0636920022220.do) Джули Лерман и Роуэн Миллер.

Обе эти книги обновлены с современными рекомендуемыми методами. Они обеспечивают более всеобъемлющее, но легкое введение в Рамочной системе образований, чем все, что доступно в Интернете. Другая книга, [Программирование Entity Framework](http://shop.oreilly.com/product/9780596807252.do) Джули Лерман, больше и более всеобъемлющим, но она старше, и многие из методов, она охватывает уже не рекомендуемый способ использования Entity Framework. Смотрите также список книг, рекомендованных группой Entity Framework в [Центре разработчиков данных - Книги](https://msdn.microsoft.com/data/aa937716) на сайте MSDN.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Другие ресурсы, налажете образование

- [Сущность Рамочной (ADO.NET) блог команды](https://blogs.msdn.com/b/adonet/). Один из лучших ресурсов для наиболее актуальной информации и объявления о новых усовершенствованиях. Для других связанных с EF блогов, см. Blogroll на [Получить начало с entity Framework](https://msdn.microsoft.com/data/ee712907).
- [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx). Просмотрите столбец **«Точки данных»,** который часто посвящен темам, связанным с рамочной системой сущности.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>Связывание данных в ASP.NET приложениях web-форм

- [ASP.NET веб-формы вариантов доступа](https://msdn.microsoft.com/library/jj822927.aspx) <a id="wfmodelbinding"></a>к данным (MSDN) .

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Использование Web Форм Модель Связывание

- [Привязка модели и веб-формы](https://go.microsoft.com/fwlink/?LinkId=286117). Учебные серии с использованием EF Code First.
- [Веб-формы модели Связывание Часть 1: Выбор данных](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Скотт Гатри в блоге). В этих старых блогах свойство, которое в настоящее время называется ItemType, получило название ModelType, но в противном случае информация, которую они содержат, действительна.
- [Веб-формы Модели Связывание Часть 2: Фильтрация данных](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Скотт Гатри в блоге).
- [Веб-формы Модели Связывание Часть 3: Обновление и проверка](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Скотт Гатри блог).
- [ASP.NET 4.5 Web Форм Астыковая](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (видео).
- [Модель Связывание Часть 1 - Выбор данных](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (видео).
- [Модель Связывание Часть 2 - Фильтрация](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (видео).
- [Начало работы с ASP.NET 4.5 веб-формы - Отображение элементов данных и подробная информация](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Использование управления исходом исходных данных веб-форм

- [Управление веб-сервером источника данных](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- [Объявление о выпуске поставщика динамических данных и управления EntityDataSource для Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (блог веб-разработки Microsoft Web).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Использование web-форм управления на основе связывания данных и привязки к данным

- [Привязка модели и веб-формы](https://go.microsoft.com/fwlink/?LinkId=286117). Учебник серии, которая использует EF код первый.
- [Начало работы с ASP.NET 4.5 веб-формы - Отображение элементов данных и подробная информация](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).
- [Сильно Набранные управления данными](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Скотт Гатри в блоге).
- [Сильно набранные элементы управления данными](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (видео).
- [ASP.NET 4.5 Веб-формы сильных типированных элементов управления данными](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (видео).
- [Управление веб-сервером](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN) связано с данными.
- [Обзор привязки к данным](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Эта страница охватывает только **Эвал** и **Bind**; он не был обновлен, чтобы включить **пункт** и **BindItem**.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>Работа с базами данных серверов S'L

- [Функции базы данных серверов S'L](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Для общего введения в самые разнообразные темы Сервера S'L, см.
- [Выпуски серверов S'L](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Резюме доступных выпусков s'L Server со ссылками на более подробную информацию о каждом из них.)
- [Строки подключения сервера для ASP.NET web-приложений](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Использование компактного сервера s'L для ASP.NET веб-приложений](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Сервер Microsoft S'L: Образцы продуктов базы данных](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Пример ы на базе данных AdventureWorks.
- [Установка выборочных баз данных](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). В дополнение к приведенным здесь методам можно также загрузить один из файлов\_.mdf в папку App Data веб-проекта, преобразовать базу данных в LocalDB и создать строку подключения LocalDB. Для получения информации о том, как это сделать, [см. Как: Обновление до LocalDB](https://msdn.microsoft.com/library/hh873188.aspx).

Также можно ознакомиться с следующими разделами, в которых можно ознакомиться с системой «Сервер экспресс» и «Локальный сервер» и базой данных«СЗЛ».

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>Работа с базами данных S'L Server Express LocalDB

- [СЗЛ Сервер Экспресс 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). Официальное введение MSDN к LocalDB.
- [Строки подключения сервера для ASP.NET web-приложений](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Как: Обновление до LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Как перенести файл .mdf из более ранней версии S'L Server Express в LocalDB. Вы также должны пройти через этот процесс, если вы загрузите одну из [выборочных баз данных S'L Server 2012.](https://go.microsoft.com/fwlink/?linkid=117483)
- [Представляем LocalDB, улучшенный экспресс S'L](https://go.microsoft.com/fwlink/?LinkId=234375) (блог Сервер-Экспресс). Имеет больше информации о том, почему был создан LocalDB, чем входит в MSDN.
- [LocalDB: Где моя база данных?](https://go.microsoft.com/fwlink/?LinkId=234376) (Блог Сервер Аосервер Экспресс). Информация о том, где создаются файлы базы данных LocalDB.
- [Использование LocalDB с полным IIS, часть 1: Профиль пользователя](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (блог S'L Server Express). LocalDB не предназначен для работы с IIS. Эта серия сообщений в блоге объясняет проблемы и некоторые обходные пути.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>Работа с базами данных серверного экспресса S'L

- [Строки подключения сервера для ASP.NET web-приложений](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). Если вы используете настройки строки подключения AttachDBFileName с s'L Server Express, обратитесь в раздел "Пользовательский экземпляр" на этой странице.
- Как взять на себя ответственность за [ваш местный S'L Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (блог S'L Server Express). Распространенной проблемой является невозможность работы с базами данных S'L Server Express, поскольку вы не являетесь администратором в экземпляре S'L Server Express. По умолчанию администратором является только тот, кто установил S'L Server Express. В этом блоге объясняется, как сделать себя администратором сервера S'L, если вы администратор на компьютере.
- [Может ли мое ASP.NET веб-приложение использовать в производственном производстве базу данных S'L Server Express?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Работа с базой данных Windows Azure S'L

- [Развертывание приложения Secure ASP.NET MVC с членством, OAuth и базой данных S'L на веб-узел Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (сайт Microsoft Azure).
- [Базы данных S'L](https://docs.microsoft.com/azure/sql-database/) (сайт Microsoft Azure). Начало начал учебники и как-к руководствам.
- [База данных Windows Azure S'L](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). Узл верхнего уровня таблицы содержимого для базы данных S'L в MSDN.
- [Windows Azure S'L База данных TechNet Вики Индекс статей (сайт](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) Microsoft TechNet).
- [Переходный блок обработки неисправностей](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Платформа, позволяющая обрабатывать временные ошибки сети и ошибки соединения, которые возникают в результате регулирования. Доступно в пакете NuGet: [Корпоративная библиотека 5.0 - Переходный блок обработки неисправностей.](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)
- [Начало работы с базой данных и рамочной базой данных](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Комплект обучения Windows Azure](https://www.microsoft.com/download/details.aspx?id=8396) (Центр загрузки Microsoft). Включает в себя практические лаборатории для базы данных S'L.
- [Форум сообщества баз данных Windows Azure S'L](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Переход на базу данных Windows Azure S'L](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Одна глава всеобъемлющего комплексного сценария группы Microsoft Patterns and Practices. Рассказывается о том, почему может потребоваться миграция и как перейти из сервера S'L в базу данных S'L.
- [Миграция баз данных серверов S'L в базу данных Windows Azure S'L](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).
- [Мастер миграции базы данных S'L](http://sqlazuremw.codeplex.com/). Инструмент с открытым исходным кодом для переноса баз данных в базу данных и из базы данных S'L.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>Выбор между сервером S'L и базой данных Windows Azure S'L

- [Сравните сервер S'L с базой данных Windows Azure S'L](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (сайт Microsoft TechNet).
- [Миграция данных в базу данных Windows Azure S'L: инструменты и методы](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). Включает разделы, которые сравнивают сервер S'L с базой данных S'L и предоставляют рекомендации о том, когда происходит переход от сервера S'L к базе данных S'L.
- [Руководство по доставке данных Windows Azure S'L (сайт](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) Microsoft TechNet).
- [Ограничения функций серверов сервера S'L (База данных Windows Azure S'L)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Windows Azure Хранилище таблицы и Windows Azure S'L база данных - Сравнение и контрастные](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Для приложения, развернутого в Windows Azure, хранилище таблиц Windows Azure может быть альтернативой базе данных Windows Azure S'L. Эта тема поможет вам выбрать между этими альтернативами.
- [База данных Windows Azure S'L](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Рекомендации и ограничения (база данных SQL Windows Azure)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>Работа с системами управления базами данных НоСЗЛ

- [Службы данных Windows Azure](https://www.windowsazure.com/develop/net/data/) (сайт Microsoft Azure). Смотрите [руководство по функции службы таблицы](https://docs.microsoft.com/azure/) и раздел **больших данных** страницы.
- [ASP.NET многоуровневое приложение с использованием таблиц хранения данных, очередей и blobs](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (сайт Microsoft Azure). Сквозной учебник с загружаемым примером приложения, которое использует таблицы хранения Данных Windows Azure.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>Использование запросов в ASP.NET приложениях

- [ASP.NET параметры доступа к данным](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). Включает в себя введение в LIN'.
- [Видео обучения (блог](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) Джо Стагнера).
- [ASP.NET форуме поток со ссылками на динамические ресурсы LIN .](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Использование динамических данных Scaffolding

- [Шаблоны динамических данных](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) проекта (MSDN). Руководство по использованию проектов Динамических Данных.
- [ASP.NET динамические данные](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Обеспечение доступа к данным

- [Обеспечение доступа к данным в ASP.NET](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Соображения безопасности (Система сущности)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Как: Безопасные строки подключения при использовании управления исходным элементом данных](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Оптимизация производительности доступа к данным

- [обзор производительности ASP.NET](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET Кэшинг](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [Повышение производительности ASP.NET](https://msdn.microsoft.com/library/ff647787) (MSDN). В верхней части этой страницы имеется предупреждение «Утвлядское содержимое», но большая часть информации по-прежнему актуальна и нет сопоставимого обновленного ресурса.
- [Улучшение производительности серверов S'L](https://msdn.microsoft.com/library/ff647793) (MSDN). Тот же комментарий, что и предыдущая ссылка.

Смотрите также [Оптимизация производительности рамочной системы сущности](#optimizingef) ранее в этой теме.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Развертывание базы данных

- [ASP.NET веб-развертывание - Рекомендуемые ресурсы](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Доступ к данным через веб-службу

- [Доступ к данным через веб-службу](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN). Руководство о том, когда использовать Web API по сравнению с WCF.
- [Начало работы с ASP.NET Web API](../web-api/index.md).
- [Службы данных WCF](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Дополнительные ресурсы

- [ASP.NET часто задаваемые вопросы доступа к данным](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [ASP.NET веб-формы Учебники - Данные](../web-forms/overview/data-access/index.md). Большинство из этих учебников являются относительно старыми; Убедитесь, что вы сначала прочитали [ASP.NET параметры доступа к данным](https://msdn.microsoft.com/library/ms178359.aspx) и параметры хранения [данных (создание облачных приложений с помощью Windows Azure),](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) чтобы не зайти слишком далеко в метод доступа к данным, который не подходит для вашего сценария.
- [ASP.NET Карта контента MVC](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [ASP.NET веб-страниц учебники - Данные](../web-pages/overview/data/index.md).
- [Доступ к данным в визуальной студии](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Предоставляет список ссылок, похожих на эту карту контента, но с акцентом на Visual Studio, а не ASP.NET.
