---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: Учебник. Добавление сортировки, фильтрации и разбиения на страницы с помощью Entity Framework в приложении MVC ASP.NET | Документация Майкрософт
author: tdykstra
description: В этом руководстве вы добавите функции сортировки, фильтрации и разбиения на страницы для индекса **учащихся** . Вы также создадите простую страницу группирования.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499332"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>Учебник. Добавление сортировки, фильтрации и разбиения на страницы с помощью Entity Framework в приложении ASP.NET MVC

В [предыдущем руководстве](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)вы реализовали набор веб-страниц для базовых операций CRUD для сущностей `Student`. В этом руководстве вы добавите функции сортировки, фильтрации и разбиения на страницы для индекса **учащихся** . Вы также создадите простую страницу группирования.

На следующем рисунке показано, как будет выглядеть страница после завершения. Заголовки столбцов являются ссылками, при нажатии на которые происходит сортировка по этому столбцу. При повторном нажатии на заголовок происходит переключение между сортировкой по возрастанию и убыванию.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

Изучив это руководство, вы:

> [!div class="checklist"]
> * Добавление ссылок для сортировки столбцов
> * Добавление поля поиска
> * Добавление разбиения по страницам
> * Создание страницы сведений

## <a name="prerequisites"></a>Предварительные требования

* [Реализация базовой функциональности CRUD](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>Добавление ссылок для сортировки столбцов

Чтобы добавить сортировку на страницу индекса учащихся, измените метод `Index` контроллера `Student` и добавьте код в `Student` представление индекса.

### <a name="add-sorting-functionality-to-the-index-method"></a>Добавление функции сортировки в метод Index

- В *Conrollers\StudentController.cs*замените метод `Index` следующим кодом:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Этот код принимает параметр `sortOrder` из строки запроса в URL. Значение строки запроса предоставляется ASP.NET MVC в качестве параметра метода действия. Параметр представляет собой строку, которая имеет значение "Name" или "Date", при необходимости за которой следует символ подчеркивания и строка "DESC" для указания порядка убывания. По умолчанию задан порядок сортировки по возрастанию.

При первом запросе страницы Index строка запроса отсутствует. Студенты отображаются в возрастающем порядке по `LastName`, который является значением по умолчанию, установленным в операторе `switch`. Когда пользователь щелкает гиперссылку заголовка столбца, в строку запроса подставляется соответствующее значение параметра `sortOrder`.

Используются две переменные `ViewBag`, чтобы представление могли настроить гиперссылки заголовка столбца с соответствующими значениями строки запроса:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Это тернарные условные операторы. Первый указывает, что если параметр `sortOrder` имеет значение null или пуст, `ViewBag.NameSortParm` должен иметь значение "Name\_DESC"; в противном случае необходимо установить пустую строку. Следующие два оператора устанавливают гиперссылки в заголовках столбцов в представлении следующим образом:

| Текущий порядок сортировки | Гиперссылка "Last Name" (Фамилия) | Гиперссылка "Date" (Дата) |
| --- | --- | --- |
| "Last Name" (Фамилия) по возрастанию | descending | ascending |
| "Last Name" (Фамилия) по убыванию | ascending | ascending |
| "Date" (Дата) по возрастанию | ascending | descending |
| "Date" (Дата) по убыванию | ascending | ascending |

Метод использует [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) , чтобы указать столбец для сортировки. Код создает переменную <xref:System.Linq.IQueryable%601> перед инструкцией `switch`, изменяет ее в операторе `switch` и вызывает метод `ToList` после инструкции `switch`. После создания и изменения переменных `IQueryable` запрос в базу данных не отправляется. Запрос не выполняется до тех пор, пока не будет преобразован объект `IQueryable` в коллекцию путем вызова метода, такого как `ToList`. Таким образом, этот код приводит к выполнению одного запроса, который не выполняется до оператора `return View`.

В качестве альтернативы написанию различных операторов LINQ для каждого порядка сортировки можно динамически создать инструкцию LINQ. Дополнительные сведения о динамическом LINQ см. в разделе [dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>Добавление гиперссылок заголовка столбца в представление индекса учащихся

1. В *виевс\студент\индекс.кштмл*замените элементы `<tr>` и `<th>` для строки заголовка выделенным кодом:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   Этот код использует сведения в свойствах `ViewBag` для настройки гиперссылок с соответствующими значениями строки запроса.

2. Чтобы проверить, работает ли сортировка, запустите страницу и щелкните заголовки столбцов **Last Name** и **Date регистрации** .

   После того как вы щелкните заголовок **Last Name (фамилия** ), учащиеся будут отображаться в порядке убывания фамилий.

## <a name="add-a-search-box"></a>Добавление поля поиска

Чтобы добавить фильтрацию на страницу индекса учащихся, добавьте в представление текстовое поле и кнопку Submit и внесите соответствующие изменения в метод `Index`. Текстовое поле позволяет ввести строку для поиска в полях Name и Last Name.

### <a name="add-filtering-functionality-to-the-index-method"></a>Добавление функций фильтрации в метод Index

- В *контроллерс\студентконтроллер.КС*замените метод `Index` следующим кодом (изменения выделены):

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

Код добавляет параметр `searchString` в метод `Index`. Значение строки поиска получается из текстового поля, которое мы добавили в представление Index. Он также добавляет к инструкции LINQ предложение `where`, которое выбирает только учащихся, чье имя или фамилия содержат строку поиска. Инструкция, которая добавляет предложение <xref:System.Linq.Queryable.Where%2A>, выполняется только в том случае, если имеется искомое значение.

> [!NOTE]
> Во многих случаях один и тот же метод можно вызвать либо в Entity Framework наборе сущностей, либо в виде метода расширения для коллекции в памяти. Результаты обычно одинаковы, но в некоторых случаях они могут отличаться.
>
> Например, .NET Framework реализация метода `Contains` возвращает все строки, когда в нее передается пустая строка, но поставщик Entity Framework для SQL Server Compact 4,0 возвращает нулевые строки для пустых строк. Поэтому код в примере (поместив оператор `Where` в инструкцию `if`) гарантирует получение одинаковых результатов для всех версий SQL Server. Кроме того, .NET Frameworkная реализация метода `Contains` выполняет сравнение с учетом регистра по умолчанию, но Entity Framework SQL Server поставщики выполняют сравнения без учета регистра по умолчанию. Таким образом, вызов метода `ToUpper` для проверки явного нечувствительного к регистру регистра гарантирует, что результаты не изменяются при последующем изменении кода для использования репозитория, который вернет коллекцию `IEnumerable` вместо объекта `IQueryable`. (При вызове метода `Contains` коллекции `IEnumerable` выполняется реализация .NET Framework; при вызове этого же метода у объекта `IQueryable` выполняется реализация поставщика базы данных.)
>
> Обработка значений NULL может также отличаться для разных поставщиков баз данных или при использовании объекта `IQueryable` по сравнению с `IEnumerable` коллекцией. Например, в некоторых сценариях `Where` условие, например `table.Column != 0`, может не возвращать столбцы, которые имеют `null` в качестве значения. По умолчанию EF создает дополнительные операторы SQL, чтобы обеспечить равенство значений NULL в базе данных, подобной работе в памяти, но можно установить флаг [уседатабасенуллсемантикс](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) в EF6 или вызвать метод [усерелатионалнуллс](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) в EF Core, чтобы настроить это поведение.

### <a name="add-a-search-box-to-the-student-index-view"></a>Добавление поля поиска в представление индекса учащихся

1. В *виевс\студент\индекс.кштмл*Добавьте выделенный код непосредственно перед открывающим тегом `table`, чтобы создать заголовок, текстовое поле и кнопку **поиска** .

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. Запустите страницу, введите строку поиска и нажмите кнопку **Поиск** , чтобы убедиться, что фильтрация работает.

   Обратите внимание, что URL-адрес не содержит строку поиска "a". Это означает, что если вы заметите эту страницу в закладки, отфильтрованный список не будет получен при использовании закладки. Это также относится к ссылкам сортировки столбцов, так как они будут сортировать весь список. Вы измените кнопку **поиска** , чтобы в дальнейшем использовать строки запросов для критериев фильтрации.

## <a name="add-paging"></a>Добавление разбиения по страницам

Чтобы добавить подкачку на страницу индекса учащихся, начните с установки пакета NuGet **пажедлист. MVC** . Затем вы вносите дополнительные изменения в метод `Index` и добавляете ссылки подкачки в представление `Index`. **Пажедлист. MVC** — это один из многих хороших пакетов разбиения по страницам и сортировки для ASP.NET MVC, и его использование здесь предназначено только в качестве примера, а не в качестве рекомендации по сравнению с другими вариантами.

### <a name="install-the-pagedlistmvc-nuget-package"></a>Установка пакета NuGet Пажедлист. MVC

Пакет NuGet **пажедлист. MVC** автоматически устанавливает пакет **пажедлист** в качестве зависимости. Пакет **пажедлист** устанавливает тип коллекции `PagedList` и методы расширения для коллекций `IQueryable` и `IEnumerable`. Методы расширения создают одну страницу данных в коллекции `PagedList` из `IQueryable` или `IEnumerable`, а коллекция `PagedList` предоставляет несколько свойств и методов, которые упрощают разбиение на страницы. Пакет **пажедлист. MVC** устанавливает вспомогательный метод разбиения на страницы, который отображает кнопки разбиения на страницы.

1. В меню **Сервис** выберите **Диспетчер пакетов NuGet** , а затем — **консоль диспетчера пакетов**.

2. В окне **консоли диспетчера пакетов** убедитесь, что **источник пакета** имеет значение **NuGet.org** , а **проект по умолчанию** — **ContosoUniversity**, а затем введите следующую команду:

   ```text
   Install-Package PagedList.Mvc
   ```

3. Создайте проект.

### <a name="add-paging-functionality-to-the-index-method"></a>Добавление разбиения на страницы в метод Index

1. В *контроллерс\студентконтроллер.КС*добавьте оператор `using` для пространства имен `PagedList`.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. Замените метод `Index` следующим кодом:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   Этот код добавляет параметр `page`, текущий параметр порядка сортировки и текущий параметр фильтра в сигнатуру метода:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   При первом отображении страницы или если пользователь не щелкнул ссылку на подкачку или сортировку, все параметры имеют значение null. При нажатии ссылки на подкачку переменная `page` содержит номер отображаемой страницы.

   Свойство `ViewBag` предоставляет представление с текущим порядком сортировки, поскольку оно должно быть включено в ссылки разбиения на страницы, чтобы порядок сортировки совпадал с порядком разбиения на страницы:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   Другое свойство, `ViewBag.CurrentFilter`, предоставляет представление с текущей строкой фильтра. Это значение необходимо включить в ссылки для перелистывания, чтобы при смене страницы сохранить настройки фильтра, кроме того, необходимо восстановить значение фильтра в текстовом поле после обновления страницы. Если строка поиска изменяется во время перелистывания, то номер страницы должен быть сброшен на 1, так как с новым фильтром изменится состав отображаемых данных. Строка поиска изменяется при вводе значения в текстовое поле и нажатии кнопки Submit (отправить). В этом случае параметр `searchString` не равен null.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   В конце метода метод расширения `ToPagedList` объекта Students `IQueryable` преобразует запрос учащегося на одну страницу учащихся в типе коллекции, который поддерживает разбиение на страницы. После этого одна страница учащихся передается в представление:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   Метод `ToPagedList` принимает номер страницы. Два знака вопроса представляют [оператор объединения со значением NULL](/dotnet/csharp/language-reference/operators/null-coalescing-operator). Этот оператор определяет значение по умолчанию для значения null; выражение `(page ?? 1)` возвращает значение переменной `page`, если она имеет значение, и возвращает 1, если переменная `page` имеет значение null.

### <a name="add-paging-links-to-the-student-index-view"></a>Добавление ссылок на подкачку в представление индекса учащихся

1. В *виевс\студент\индекс.кштмл*замените существующий код следующим кодом. Изменения выделены.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   Оператор `@model` в начале страницы указывает на то, что теперь представление принимает объект `PagedList`, а не объект `List`.

   Инструкция `using` для `PagedList.Mvc` предоставляет доступ к вспомогательному модулю MVC для кнопок разбиения на страницы.

   Код использует перегрузку [бегинформ](/previous-versions/aspnet/dd492719(v=vs.108)) , которая позволяет ему указать [форммесод. Get](/previous-versions/aspnet/dd460179(v=vs.100)).

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   [Бегинформ](/previous-versions/aspnet/dd492719(v=vs.108)) по умолчанию отправляет данные формы с помощью записи, что означает, что параметры передаются в тексте сообщения HTTP, а не в URL-адресе в виде строк запроса. При указании метода HTTP GET данные формы передаются в URL-адресе в виде строк запроса, что позволяет добавлять URL-адреса в закладки. [Рекомендации консорциума W3C по использованию протокола HTTP Get рекомендуют использовать инструкцию](http://www.w3.org/2001/tag/doc/whenToUseGet.html) Get, если действие не приводит к обновлению.

   Текстовое поле инициализируется текущей строкой поиска, поэтому при щелчке на новой странице можно увидеть текущую строку поиска.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   Ссылки в заголовках столбцов передают в контроллер при помощи строки запроса текущее значение строки поиска, чтобы пользователь мог сортировать отфильтрованные данные:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   Отобразится текущая страница и общее количество страниц.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   Если нет страниц для отображения, отображается страница 0 из 0. (В этом случае номер страницы больше, чем число страниц, поскольку `Model.PageNumber` равно 1, а `Model.PageCount` — 0.)

   Кнопки разбиения на страницы отображаются `PagedListPager` вспомогательным модулем:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   Модуль поддержки `PagedListPager` предоставляет ряд параметров, которые можно настраивать, включая URL-адреса и стили. Дополнительные сведения см. в разделе [тройгуде/пажедлист](https://github.com/TroyGoode/PagedList) на сайте GitHub.

2. Запустите страницу.

   Чтобы убедиться, что постраничный просмотр работает, нажимайте кнопки перелистывания при различном порядке сортировки. Затем введите строку поиска и повторите перелистывание, чтобы убедиться, что разбиение на страницы работает корректно вместе с сортировкой и фильтрацией.

## <a name="create-an-about-page"></a>Создание страницы сведений

На странице со сведениями о веб-сайте университета Contoso вы увидите, сколько учащихся зарегистрировано для каждой даты регистрации. Для этого понадобится группировка и выполнение простых расчетов в группах. Для выполнения этой задачи нам потребуется следующее:

- Создать класс модели представления для данных, которые необходимо передать в представление.
- Измените метод `About` в контроллере `Home`.
- Измените представление `About`.

### <a name="create-the-view-model"></a>Создание модели представления

Создайте папку *ViewModels* в папке проекта. В этой папке добавьте файл класса *EnrollmentDateGroup.CS* и замените код шаблона следующим кодом:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Изменение контроллера Home

1. В *HomeController.CS*добавьте в начало файла следующие инструкции `using`:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. Добавьте переменную класса для контекста базы данных сразу после открывающей фигурной скобки для класса:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. Замените метод `About` следующим кодом:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   Запрос LINQ группирует записи из таблицы студентов по дате зачисления, вычисляет число записей в каждой группе и сохраняет результаты в коллекцию объектов моделей представления `EnrollmentDateGroup`.

4. Добавьте метод `Dispose`:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>Изменение представления About

1. Замените код в файле *виевс\хоме\абаут.кштмл* следующим кодом:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. Запустите приложение и щелкните ссылку **About (о программе** ).

   Число учащихся для каждой даты регистрации отображается в таблице.

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>Получение кода

[Скачать завершенный проект](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Дополнительные ресурсы

Ссылки на другие ресурсы Entity Framework можно найти в [материалах, рекомендуемых для доступа к данным ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Дальнейшие действия

Изучив это руководство, вы:

> [!div class="checklist"]
> * Добавление ссылок для сортировки столбцов
> * Добавление поля поиска
> * Добавление разбиения по страницам
> * Создание страницы сведений

Перейдите к следующей статье, чтобы узнать, как использовать устойчивость подключений и перехват команд.
> [!div class="nextstepaction"]
> [Устойчивость подключений и перехват команд](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
