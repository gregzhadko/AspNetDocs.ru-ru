---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: Сортировка, фильтрация и разбиение на страницы с помощью Entity Framework в приложении ASP.NET MVC (3 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 48938b378a741a0f1c351c2cb1d33b5140c6cf93
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484702"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>Сортировка, фильтрация и разбиение на страницы с помощью Entity Framework в приложении ASP.NET MVC (3 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем руководстве вы реализовали набор веб-страниц для базовых операций CRUD для `Student` сущностей. В этом учебнике вы добавите функции сортировки, фильтрации и разбиения на страницы для индекса **учащихся** . Здесь также описывается создание страницы с простой группировкой.

На следующем рисунке изображен вид страницы после выполнения задания. Заголовки столбцов являются ссылками, при нажатии на которые происходит сортировка по этому столбцу. При повторном нажатии на заголовок происходит переключение между сортировкой по возрастанию и убыванию.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>Добавление ссылок для сортировки в заголовки столбцов на странице указателя учащихся

Чтобы добавить сортировку на страницу индекса учащихся, измените `Index` метод `Student` контроллера и добавьте код в `Student` представление индекса.

### <a name="add-sorting-functionality-to-the-index-method"></a>Добавление функции сортировки в метод Index

В *контроллерс\студентконтроллер.КС*замените `Index` метод следующим кодом:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Этот код принимает параметр `sortOrder` из строки запроса в URL. Значение строки запроса предоставляется ASP.NET MVC в качестве параметра метода действия. Имя параметра представляет собой строку, состоящую из "Name" или "Date" с возможным добавлением знака подчеркивания и строки "desc" для указания убывающего порядка сортировки. По умолчанию используется порядок сортировки по возрастанию.

При первом запросе страницы Index строка запроса отсутствует. Студенты отображаются в порядке возрастания по `LastName` , который является значением по умолчанию, установленным в `switch` операторе перебора. Когда пользователь щелкает гиперссылку заголовка столбца, в строку запроса подставляется соответствующее значение параметра `sortOrder`.

Эти две `ViewBag` переменные используются, чтобы представление могли настроить гиперссылки заголовка столбца с соответствующими значениями строки запроса:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Это тернарные условные операторы. Первый указывает, что если `sortOrder` параметр имеет значение null или пуст, то `ViewBag.NameSortParm` для него должно быть задано имя \_ DESC; в противном случае ему следует присвоить пустую строку. Следующие два оператора устанавливают гиперссылки в заголовках столбцов в представлении следующим образом:

| Текущий порядок сортировки | Гиперссылка "Last Name" (Фамилия) | Гиперссылка "Date" (Дата) |
| --- | --- | --- |
| "Last Name" (Фамилия) по возрастанию | descending | ascending |
| "Last Name" (Фамилия) по убыванию | ascending | ascending |
| "Date" (Дата) по возрастанию | ascending | descending |
| "Date" (Дата) по убыванию | ascending | ascending |

Метод использует [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) , чтобы указать столбец для сортировки. Код создает переменную [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) перед `switch` инструкцией, изменяет ее в `switch` операторе и вызывает `ToList` метод после `switch` инструкции. После создания и изменения переменных `IQueryable` запрос в базу данных не отправляется. Запрос не выполняется до тех пор, пока объект не будет преобразован `IQueryable` в коллекцию путем вызова метода, такого как `ToList` . Таким образом, этот код приводит к выполнению одного запроса, который не выполняется до `return View` инструкции.

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>Добавление гиперссылок заголовка столбца в представление индекса учащихся

В *виевс\студент\индекс.кштмл*замените `<tr>` `<th>` элементы и для строки заголовка выделенным кодом:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

Этот код использует сведения в `ViewBag` свойствах для настройки гиперссылок с соответствующими значениями строки запроса.

Чтобы проверить, работает ли сортировка, запустите страницу и щелкните заголовки столбцов **Last Name** и **Date регистрации** .

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

После того как вы щелкните заголовок **Last Name (фамилия** ), учащиеся будут отображаться в порядке убывания фамилий.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>Добавление поля поиска на страницу индекса учащихся

Для добавления фильтра на страницу указателя учащихся необходимо добавить в представление текстовое поле и кнопку отправки и внести изменения в метод `Index`. Текстовое поле необходимо для ввода строки для поиска в полях имени и фамилии.

### <a name="add-filtering-functionality-to-the-index-method"></a>Добавление функций фильтрации в метод Index

В *контроллерс\студентконтроллер.КС*замените `Index` метод следующим кодом (изменения выделены):

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

Мы добавили в метод `Index` параметр `searchString`. Вы также добавили в Оператор LINQ `where` предложение, которое выбирает только учащихся, чье имя или фамилия содержат строку поиска. Значение строки поиска получено из текстового поля, которое будет добавлено в представление индекса. Инструкция, которая добавляет предложение [WHERE](https://msdn.microsoft.com/library/bb535040.aspx) , выполняется только в том случае, если имеется искомое значение.

> [!NOTE]
> Во многих случаях один и тот же метод можно вызвать либо в Entity Framework наборе сущностей, либо в виде метода расширения для коллекции в памяти. Результаты обычно одинаковы, но в некоторых случаях они могут отличаться. Например, .NET Framework реализация `Contains` метода возвращает все строки, когда в нее передается пустая строка, но поставщик Entity Framework для SQL Server Compact 4,0 возвращает нулевые строки для пустых строк. Поэтому код в примере (поместив `Where` инструкцию внутри `if` инструкции) гарантирует получение одинаковых результатов для всех версий SQL Server. Кроме того, .NET Frameworkная реализация `Contains` метода выполняет сравнение с учетом регистра по умолчанию, но Entity Framework поставщики SQL Server по умолчанию выполняют сравнения без учета регистра. Поэтому вызов `ToUpper` метода для явного учета регистра гарантирует, что результаты не изменяются при следующем изменении кода для использования репозитория, который вернет `IEnumerable` коллекцию вместо `IQueryable` объекта. (При вызове метода `Contains` коллекции `IEnumerable` выполняется реализация .NET Framework; при вызове этого же метода у объекта `IQueryable` выполняется реализация поставщика базы данных.)

### <a name="add-a-search-box-to-the-student-index-view"></a>Добавление поля поиска на страницу индекса учащихся

В *виевс\студент\индекс.кштмл*Добавьте выделенный код непосредственно перед открывающим `table` тегом, чтобы создать заголовок, текстовое поле и кнопку **поиска** .

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

Запустите страницу, введите строку поиска и нажмите кнопку **Поиск** , чтобы убедиться, что фильтрация работает.

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Обратите внимание, что URL-адрес не содержит строку поиска "a". Это означает, что если вы заметите эту страницу в закладки, отфильтрованный список не будет получен при использовании закладки. Вы измените кнопку **поиска** , чтобы в дальнейшем использовать строки запросов для критериев фильтрации.

## <a name="add-paging-to-the-students-index-page"></a>Добавление разбиения на страницы индекса учащихся

Чтобы добавить подкачку на страницу индекса учащихся, начните с установки пакета NuGet **пажедлист. MVC** . Затем вы вносите дополнительные изменения в `Index` метод и добавляете в представление ссылки для разбиения на страницы `Index` . **Пажедлист. MVC** — это один из многих хороших пакетов разбиения по страницам и сортировки для ASP.NET MVC, и его использование здесь предназначено только в качестве примера, а не в качестве рекомендации по сравнению с другими вариантами. На следующем рисунке показаны ссылки на подкачку.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>Установка пакета NuGet Пажедлист. MVC

Пакет NuGet **пажедлист. MVC** автоматически устанавливает пакет **пажедлист** в качестве зависимости. Пакет **пажедлист** устанавливает `PagedList` тип коллекции и методы расширения для `IQueryable` `IEnumerable` коллекций и. Методы расширения создают одну страницу данных в `PagedList` коллекции вне `IQueryable` или `IEnumerable` , а `PagedList` Коллекция предоставляет несколько свойств и методов, которые упрощают разбиение на страницы. Пакет **пажедлист. MVC** устанавливает вспомогательный метод разбиения на страницы, который отображает кнопки разбиения на страницы.

В меню **Сервис** выберите **Диспетчер пакетов NuGet** , а затем — **Управление пакетами NuGet для решения**.

В диалоговом окне **Управление пакетами NuGet** перейдите на вкладку в **Интернете** слева и в поле поиска введите "с постраничным переходом". Когда появится пакет **пажедлист. MVC** , нажмите кнопку **установить**.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

В поле **Выбор проектов** нажмите кнопку **ОК**.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>Добавление функции разбиения по страницам в метод Index

В *контроллерс\студентконтроллер.КС*добавьте `using` инструкцию для `PagedList` пространства имен:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Замените метод `Index` следующим кодом:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Этот код добавляет `page` параметр, текущий параметр порядка сортировки и текущий параметр фильтра в сигнатуру метода, как показано ниже:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

При первом отображении страницы или если пользователь еще не нажимал на ссылки сортировки и перелистывания, все параметры будут иметь значение null. Если щелкнуть ссылку подкачки, `page` переменная будет содержать номер отображаемой страницы.

`A ViewBag`свойство предоставляет представление с текущим порядком сортировки, поскольку оно должно быть включено в ссылки подкачки, чтобы порядок сортировки совпадал с тем, что при разбиении на страницы:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Другое свойство, `ViewBag.CurrentFilter` предоставляет представление с текущей строкой фильтра. Это значение необходимо включить в ссылки для перелистывания, чтобы при смене страницы сохранить настройки фильтра, кроме того, необходимо восстановить значение фильтра в текстовом поле после обновления страницы. Если строка поиска изменяется во время перелистывания, то номер страницы должен быть сброшен на 1, так как с новым фильтром изменится состав отображаемых данных. Строка поиска изменяется при вводе значения в текстовое поле и нажатии кнопки Submit (отправить). В этом случае параметр не `searchString` равен null.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

В конце метода `ToPagedList` метод расширения объекта Students `IQueryable` преобразует запрос Student на одну страницу учащихся в типе коллекции, который поддерживает разбиение на страницы. После этого одна страница учащихся передается в представление:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Метод `ToPagedList` принимает номер страницы. Два знака вопроса представляют [оператор объединения со значением NULL](https://msdn.microsoft.com/library/ms173224.aspx). Этот оператор определяет значение по умолчанию для значения null; выражение `(page ?? 1)` возвращает значение переменной `page`, если она имеет значение, и возвращает 1, если переменная `page` имеет значение null.

### <a name="add-paging-links-to-the-student-index-view"></a>Добавление ссылок на подкачку в представление индекса учащихся

В *виевс\студент\индекс.кштмл*замените существующий код следующим кодом:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

Оператор `@model` в начале страницы указывает на то, что теперь представление принимает объект `PagedList`, а не объект `List`.

`using`Инструкция для `PagedList.Mvc` предоставляет доступ к вспомогательному модулю MVC для кнопок разбиения на страницы.

Код использует перегрузку [бегинформ](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) , которая позволяет ему указать [форммесод. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

[Бегинформ](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) по умолчанию отправляет данные формы с помощью записи, что означает, что параметры передаются в тексте сообщения HTTP, а не в URL-адресе в виде строк запроса. При указании метода HTTP GET данные формы передаются в URL-адресе в виде строк запроса, что позволяет добавлять URL-адреса в закладки. [Рекомендации консорциума W3C по использованию HTTP Get](http://www.w3.org/2001/tag/doc/whenToUseGet.html) указывают, что следует использовать GET, если действие не приводит к обновлению.

Текстовое поле инициализируется текущей строкой поиска, поэтому при щелчке на новой странице можно увидеть текущую строку поиска.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

Ссылки в заголовках столбцов передают в контроллер при помощи строки запроса текущее значение строки поиска, чтобы пользователь мог сортировать отфильтрованные данные:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

Отобразится текущая страница и общее количество страниц.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

Если нет страниц для отображения, отображается страница 0 из 0. (В этом случае номер страницы больше, чем число страниц, так как `Model.PageNumber` значение равно 1, а `Model.PageCount` равно 0.)

Вспомогательная функция отображает кнопки разбиения по страницам `PagedListPager` :

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager`Вспомогательное приложение предоставляет ряд параметров, которые можно настраивать, включая URL-адреса и стили. Дополнительные сведения см. в разделе [тройгуде/пажедлист](https://github.com/TroyGoode/PagedList) на сайте GitHub.

Запустите страницу.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Чтобы убедиться, что постраничный просмотр работает, нажимайте кнопки перелистывания при различном порядке сортировки. Затем введите строку поиска и повторите перелистывание, чтобы убедиться, что разбиение на страницы работает корректно вместе с сортировкой и фильтрацией.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>Создание страницы "о программе" с отображением статистики учащихся

На странице About веб-сайта "Университет Contoso" будет отображаться количество зачисленных студентов по дням. Для этого понадобится группировка и выполнение простых расчетов в группах. Для выполнения этой задачи нам потребуется следующее:

- Создать класс модели представления для данных, которые необходимо передать в представление.
- Измените `About` метод в `Home` контроллере.
- Измените `About` представление.

### <a name="create-the-view-model"></a>Создание модели представления

Создайте папку *ViewModels* . В этой папке добавьте файл класса *EnrollmentDateGroup.CS* и замените существующий код следующим кодом:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Изменение контроллера Home

В *HomeController.CS*добавьте следующие инструкции в `using` начало файла:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

Добавьте переменную класса для контекста базы данных сразу после открывающей фигурной скобки для класса:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

Замените метод `About` следующим кодом:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

Запрос LINQ группирует записи из таблицы студентов по дате зачисления, вычисляет число записей в каждой группе и сохраняет результаты в коллекцию объектов моделей представления `EnrollmentDateGroup`.

Добавьте `Dispose` метод:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>Изменение представления About

Замените код в файле *виевс\хоме\абаут.кштмл* следующим кодом:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

Запустите приложение и щелкните ссылку **About (о программе** ). Количество зачисленных студентов по дням отображается в таблице.

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>Необязательно: развертывание приложения в Windows Azure

Пока приложение запущено локально в IIS Express на компьютере разработчика. Чтобы сделать его доступным для других пользователей через Интернет, необходимо развернуть его для поставщика услуг размещения веб-сайтов. В этом необязательном разделе учебника вы развернете его на веб-сайте Windows Azure.

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Развертывание базы данных с помощью Code First Migrations

Чтобы развернуть базу данных, используйте Code First Migrations. При создании профиля публикации, который используется для настройки параметров развертывания из Visual Studio, необходимо установить флажок " **выполнить Code First migrations" (выполняется при запуске приложения)**. Этот параметр заставляет процесс развертывания автоматически настраивать файл *Web.config* приложения на целевом сервере, чтобы Code First использовал `MigrateDatabaseToLatestVersion` класс инициализатора.

Visual Studio не выполняет никаких действий с базой данных в процессе развертывания. Когда развернутое приложение обращается к базе данных в первый раз после развертывания, Code First автоматически создает базу данных или обновляет схему базы данных до последней версии. Если приложение реализует `Seed` метод миграции, метод выполняется после создания базы данных или обновления схемы.

`Seed`Метод миграции вставляет тестовые данные. При развертывании в рабочей среде необходимо изменить `Seed` метод так, чтобы он вставил только те данные, которые необходимо вставить в рабочую базу данных. Например, в текущей модели данных может возникнуть необходимость в реальных курсах, но вымышленных учащихся в базе данных разработки. Можно написать `Seed` метод для загрузки в процессе разработки, а затем закомментировать вымышленные учащиеся перед развертыванием в рабочей среде. Кроме того, можно написать `Seed` метод для загрузки только курсов и ввести вымышленные учащиеся в тестовой базе данных вручную с помощью пользовательского интерфейса приложения.

### <a name="get-a-windows-azure-account"></a>Получение учетной записи Windows Azure

Вам потребуется учетная запись Windows Azure. Если у вас ее еще нет, вы можете создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье [Бесплатная пробная версия Windows Azure](https://azure.microsoft.com/free/dotnet/).

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>Создание веб-сайта и базы данных SQL в Windows Azure

Веб-сайт Windows Azure будет работать в общей среде размещения. Это означает, что она выполняется на виртуальных машинах, которые являются общими для других клиентов Windows Azure. Общая среда внешнего размещения – это недорогой способ начать работу в облачной среде. Если позднее ваш веб-трафик увеличится, приложение можно масштабировать по необходимости, запуская его на выделенных виртуальных машинах. Если вам нужна более сложная архитектура, можно выполнить миграцию в облачную службу Windows Azure. Облачные службы работают на выделенных виртуальных машинах, которые можно настроить в соответствии с конкретными потребностями.

База данных SQL Windows Azure — это облачная служба реляционных баз данных, созданная на основе технологий SQL Server. Средства и приложения, работающие с SQL Server также работают с базой данных SQL.

1. В [портал управления Windows Azure](https://manage.windowsazure.com/)щелкните **веб-сайты** на вкладке слева и нажмите кнопку **создать**.

    ![Кнопка "создать" в портал управления](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. Щелкните **настраиваемое создание**.

    ![Создание с помощью канала связи базы данных в портал управления](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   Откроется **новый веб-сайт — настраиваемый мастер создания** .
3. На шаге **новый веб-сайт** мастера введите строку в поле **URL-адрес** , чтобы использовать его в качестве уникального URL-адреса для приложения. Полный URL-адрес будет состоять из введенной здесь строки и суффикса, который отображается рядом с текстовым полем. На рисунке показан «кону», но этот URL-адрес, вероятно, будет создан, поэтому необходимо выбрать другой.

    ![Создание с помощью канала связи базы данных в портал управления](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. В раскрывающемся списке **регион** выберите область, близкую к вам. Этот параметр указывает центр обработки данных, в котором будет выполняться веб-сайт.
5. В раскрывающемся списке **база данных** выберите **создать свободную базу данных SQL объемом 20 МБ**.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. В поле **имя строки подключения к базе данных**введите *SchoolContext*.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. Щелкните стрелку, расположенную справа внизу окна. Мастер переходит к шагу **Параметры базы данных** .
8. В поле **имя** введите *контосауниверситидб*.
9. В поле **сервер** выберите **новый сервер базы данных SQL**. Кроме того, если ранее был создан сервер, можно выбрать его в раскрывающемся списке.
10. Введите имя для **входа** и **пароль**администратора. Если выбрано действие **Создать сервер базы данных SQL** , не используйте здесь существующие имя и пароль, введите новые, которые в дальнейшем будут использоваться при обращении к базе данных. Если вы выбрали ранее созданный сервер, введите учетные данные для этого сервера. В этом учебнике не будет установлен флажок ***Дополнительно*** . ***Дополнительные*** параметры позволяют задать [Параметры сортировки](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)базы данных.
11. Выберите тот же **регион** , который вы выбрали для веб-сайта.
12. Щелкните галочку в правом нижнем углу окна, чтобы указать, что вы завершили работу.   
  
    ![Шаг "Параметры базы данных" для создания веб-сайта — мастер создания базы данных](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    На следующем рисунке показано использование существующего SQL Server и имени входа.   
  
    ![Шаг "Параметры базы данных" для создания веб-сайта — мастер создания базы данных](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    Портал управления возвращается на страницу веб-сайтов, а в столбце **состояние** указывается, что сайт создается. Через некоторое время (обычно меньше минуты) в столбце **состояние** указывается, что сайт был успешно создан. На панели навигации слева отображается число сайтов в вашей учетной записи рядом со значком **веб-сайтов** , а рядом со значком **базы данных SQL** отображается число баз данных.

## <a name="deploy-the-application-to-windows-azure"></a>Развертывание приложения в Windows Azure

1. В Visual Studio щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать** в контекстном меню.  
  
    !["Опубликовать" в контекстном меню проекта](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. На вкладке **профиль** в мастере **публикации веб-сайта** нажмите кнопку **Импорт**.  
  
    ![Параметры импорта публикации](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. Если вы ранее не добавили подписку Windows Azure в Visual Studio, выполните следующие действия. На этих шагах вы добавите подписку, чтобы в раскрывающемся списке в разделе **Импорт из веб-сайта Windows Azure** содержался ваш веб-сайт.

    а. В диалоговом окне **Импорт профиля публикации** щелкните **Импорт на веб-сайте Windows Azure**, а затем щелкните **Добавить подписку Windows Azure**.

    ![Добавить подписку Windows Azure](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. В диалоговом окне **Импорт подписок Windows Azure** нажмите кнопку **скачать файл подписки**.

    ![Скачать файл подписки](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. В окне браузера сохраните файл *publishsettings* .

    ![Скачать файл publishsettings](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > Безопасность. файл *publishsettings* содержит ваши учетные данные (незакодированные), которые используются для администрирования подписок и служб Windows Azure. Для этого файла рекомендуется временно сохранить его за пределами исходных каталогов (например, в папке *Libraries\Documents* ), а затем удалить его после завершения импорта. Злонамеренный пользователь, получивший доступ к `.publishsettings` файлу, может изменять, создавать и удалять службы Windows Azure.

    d. В диалоговом окне **Импорт подписок Windows Azure** нажмите кнопку **Обзор** и перейдите к файлу *publishsettings* .

    ![Скачать подписку](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    д) Щелкните **Импорт**.

    ![импорт](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. В диалоговом окне **Импорт профиля публикации** выберите **Импорт на веб-сайте Windows Azure**, выберите веб-сайт из раскрывающегося списка и нажмите кнопку **ОК**.  
  
    ![Импорт профиля публикации](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. На вкладке **Подключение** щелкните **проверить подключение** , чтобы убедиться в правильности параметров.  
  
    ![Проверить подключение](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. После проверки соединения рядом с кнопкой **проверить подключение** отображается зеленая галочка. Щелкните **Далее**.  
  
    ![Успешно проверено подключение](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. Откройте раскрывающийся список **удаленная строка подключения** в разделе **SchoolContext** и выберите строку подключения для созданной базы данных.
8. Выберите **выполнить Code First migrations (выполняется при запуске приложения)**.
9. Снимите флажок **использовать эту строку подключения во время выполнения** для **UserContext (DefaultConnection)**, так как это приложение не использует базу данных членства.   
  
    ![Вкладка "Параметры"](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. Щелкните **Далее**.
11. На вкладке **Предварительный просмотр** нажмите кнопку **начать предварительный просмотр**.  
  
    ![Кнопка Стартпревиев на вкладке предварительного просмотра](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    На вкладке отображается список файлов, которые будут скопированы на сервер. Отображение предварительной версии не требуется для публикации приложения, но это полезная функция, о которой следует помнить. В этом случае вам не нужно ничего делать со списком отображаемых файлов. При следующем развертывании этого приложения в этом списке будут отображаться только измененные файлы.  
  
    ![Вывод файла Стартпревиев](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. Нажмите кнопку **Опубликовать**.  
    Visual Studio начнет процесс копирования файлов на сервер Windows Azure.
13. В окне **Вывод** указывается, какие действия по развертыванию были выполнены, а также сообщается об успешном завершении развертывания.  
  
    ![Окно вывода с сообщением об успешном развертывании](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. После успешного развертывания браузер по умолчанию автоматически открывается по URL-адресу развернутого сайта.  
    Созданное вами приложение теперь выполняется в облаке. Перейдите на вкладку учащиеся.  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

На этом этапе база данных *SchoolContext* была создана в базе данных SQL Windows Azure, так как вы выбрали **Execute Code First migrations (выполняется при запуске приложения)**. Файл *Web.config* на развернутом веб-сайте был изменен таким образом, чтобы инициализатор [мигратедатабасетолатестверсион](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) выполнялся в первый раз, когда код считывает или записывает данные в базе данных (что происходит при выборе вкладки **students** ):

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

В процессе развертывания также создается новая строка подключения *(SchoolContext \_ датабасепублиш*) для Code First migrations, используемая для обновления схемы базы данных и заполнения базы данных.

![Строка подключения Database_Publish](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

Строка подключения *DefaultConnection* предназначена для базы данных членства (которая не используется в этом руководстве). Строка подключения *SchoolContext* для базы данных ContosoUniversity.

Развернутую версию Web.config файла можно найти на своем компьютере в *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. Доступ к развернутому файлу *Web.config* можно получить с помощью FTP. Инструкции см. в статье [развертывание кода с помощью Visual Studio в ASP.NET Web Deployment](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). Следуйте инструкциям, которые начинаются с "для использования средства FTP, требуются три вещи: URL-адрес FTP, имя пользователя и пароль".

> [!NOTE]
> Веб-приложение не реализует безопасность, поэтому любой пользователь, который найдет URL-адрес, может изменить данные. Инструкции по обеспечению безопасности веб-сайта см. в статье [развертывание безопасного приложения MVC ASP.NET с членством, OAuth и база данных SQL на веб-сайте Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Вы можете запретить другим пользователям использовать сайт с помощью портал управления Windows Azure или **Обозреватель сервера** в Visual Studio, чтобы отключить сайт.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Инициализаторы Code First

В разделе Deployment (развертывание) вы видели используемый инициализатор [мигратедатабасетолатестверсион](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) . Code First также предоставляет другие инициализаторы, которые можно использовать, включая [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (по умолчанию), [дропкреатедатабасеифмоделчанжес](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) и [дропкреатедатабасеалвайс](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx). `DropCreateAlways`Инициализатор может быть полезен для настройки условий для модульных тестов. Можно также написать собственные инициализаторы, и вы можете вызвать инициализатор явным образом, если вы не хотите ждать, пока приложение не закончит чтение или запись в базу данных. Подробное описание инициализаторов см. в главе 6 руководства по [программированию Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) от Джулия Лерман и Роуэн Миллер.

## <a name="summary"></a>Сводка

В этом учебнике вы узнали, как создать модель данных и реализовать базовые функции CRUD, сортировки, фильтрации, разбиения на страницы и группировки. В следующем учебном курсе вы начнете изучение более сложных тем, развернув модель данных.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [Вперед](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
