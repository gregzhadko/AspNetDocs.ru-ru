---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: Расширенные сценарии Entity Framework для веб-приложения MVC (10 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 85dd59016d904a9f654c438db977b5ae2c0187d2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045056"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>Дополнительные Entity Framework сценарии для веб-приложения MVC (10 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем руководстве вы реализовали шаблоны репозитория и единиц работы. В этом учебнике рассматриваются следующие темы:

- Выполнение необработанных запросов SQL.
- Выполнение запросов без отслеживания.
- Проверка запросов, отправленных в базу данных.
- Работа с классами прокси.
- Отключение автоматического обнаружения изменений.
- Отключение проверки при сохранении изменений.
- [Ошибки и обходные проблемы](#errors)

В большинстве из этих разделов вы будете работать с уже созданными страницами. Чтобы использовать необработанный SQL для выполнения операций с массовыми обновлениями, создайте новую страницу, которая обновляет количество кредитов всех курсов в базе данных:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

Чтобы использовать запрос без отслеживания, добавьте новую логику проверки на страницу редактирования отдела:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>Выполнение необработанных запросов SQL

API Entity Framework Code First содержит методы, позволяющие передавать команды SQL непосредственно в базу данных. Вам доступны следующие варианты:

- Использование метода `DbSet.SqlQuery` для запросов, которые возвращают типы сущностей. Возвращаемые объекты должны иметь тип, ожидаемый `DbSet` объектом, и они автоматически отслеживаются контекстом базы данных, если не отключить отслеживание. (Сведения о методе см. в следующем разделе `AsNoTracking` .)
- Используйте `Database.SqlQuery` метод для запросов, возвращающих типы, которые не являются сущностями. Возвращаемые данные не отслеживаются контекстом базы данных, даже если вы используете этот метод для извлечения типов сущностей.
- Используйте [Database.Exeкутесклкомманд](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) для команд, не относящихся к запросу.

Одним из преимуществ использования платформы Entity Framework является возможность избежать слишком тесной привязки кода к конкретному способу хранения данных. Это достигается путем автоматического создания запросов и команд SQL, что позволяет упростить написание кода. Но существуют исключительные ситуации, когда необходимо выполнить определенные запросы SQL, созданные вручную, и эти методы позволят вам справиться с такими исключениями.

Как и всегда при выполнении команд SQL в веб-приложении, необходимо принимать меры предосторожности для защиты сайта от атак путем внедрения кода SQL. Одним из способов защиты является применение параметризованных запросов, которые гарантируют, что строки, отправляемые веб-страницей, не могут быть интерпретированы как команды SQL. В рамках этого учебника вы будете использовать параметризованные запросы при интеграции вводимых пользователем данных в запрос.

### <a name="calling-a-query-that-returns-entities"></a>Вызов запроса, возвращающего сущности

Предположим, требуется, `GenericRepository` чтобы класс предоставил дополнительные возможности фильтрации и сортировки, не требуя создания производного класса с дополнительными методами. Одним из способов добиться этого является Добавление метода, принимающего SQL-запрос. Затем можно указать любой тип фильтрации или сортировки в контроллере, например `Where` предложение, которое зависит от соединений или вложенного запроса. В этом разделе вы узнаете, как реализовать такой метод.

Создайте `GetWithRawSql` метод, добавив следующий код в *GenericRepository.CS*:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

В *CourseController.CS*вызовите новый метод из `Details` метода, как показано в следующем примере:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

В этом случае можно было бы использовать `GetByID` метод, но вы используете `GetWithRawSql` метод, чтобы убедиться, что `GetWithRawSQL` метод работает.

Запустите страницу сведений, чтобы убедиться в том, что запрос на выборку работает (выберите вкладку **Course (курс** ), а затем **сведения** для одного курса).

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>Вызов запроса, возвращающего другие типы объектов

Ранее вы создали таблицу статистики учащихся на странице сведений, в которой было показано число учащихся на каждую дату регистрации. Код, который делает это в *HomeController.CS* , использует LINQ:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

Предположим, что вам нужно написать код, извлекающий эти данные непосредственно в SQL, а не использовать LINQ. Для этого необходимо выполнить запрос, который возвращает нечто, отличное от объектов сущности, что означает необходимость использования `Database.SqlQuery` метода.

В *HomeController.CS*Замените инструкцию LINQ в `About` методе следующим кодом:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

Запуск страницы About. На экран будут выведены те же данные, что и ранее.

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>Вызов запроса на обновление

Предположим, администраторы университета Contoso хотят иметь возможность выполнять групповые изменения в базе данных, например изменять количество кредитов для каждого курса. Поскольку в университете ведется множество курсов, будет неэффективно извлекать их в виде сущностей и изменять по отдельности. В этом разделе вы реализуете веб-страницу, с помощью которой пользователь сможет указать коэффициент, на который нужно изменить количество кредитов для всех курсов, и внести изменения, выполнив `UPDATE` инструкцию SQL. Веб-страница должна выглядеть так, как показано на следующем рисунке:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

В предыдущем учебнике использовался универсальный репозиторий для чтения и обновления `Course` сущностей в `Course` контроллере. Для этой операции с массовым обновлением необходимо создать новый метод репозитория, который не входит в общий репозиторий. Для этого нужно создать выделенный `CourseRepository` класс, производный от `GenericRepository` класса.

В папке *DAL* создайте *CourseRepository.CS* и замените существующий код следующим кодом:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

В *UnitOfWork.CS*измените `Course` Тип репозитория с `GenericRepository<Course>` на `CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

В *CourseController.CS*добавьте `UpdateCourseCredits` метод:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

Этот метод будет использоваться как для `HttpGet` , так и для `HttpPost` . При `HttpGet` `UpdateCourseCredits` выполнении метода `multiplier` переменная будет иметь значение null, и в представлении отобразится пустое текстовое поле и кнопка отправки, как показано на предыдущем рисунке.

При нажатии кнопки **Обновить** в `HttpPost` `multiplier` текстовом поле будет введено значение. Затем код вызывает `UpdateCourseCredits` метод репозитория, который возвращает количество затронутых строк, и это значение сохраняется в `ViewBag` объекте. Когда представление получает количество затронутых строк в `ViewBag` объекте, оно отображает это число вместо текстового поля и кнопки Отправить, как показано на следующем рисунке:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

Создайте представление в папке *виевс\каурсе* на странице Обновление кредитов для курса:

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

В *виевс\каурсе\упдатекаурсекредитс.кштмл*замените код шаблона следующим кодом:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

Выполните метод `UpdateCourseCredits`, выбрав вкладку **Courses** (Курсы), а затем добавив "/UpdateCourseCredits" в конец URL-адреса в адресной строке браузера (например, `http://localhost:50205/Course/UpdateCourseCredits`). Введите число в текстовое поле:

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

Нажмите кнопку **Обновить**. Отобразится число обработанных строк:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

Нажмите кнопку **Back to List** (Вернуться к списку), чтобы просмотреть список курсов с измененным числом зачетных баллов.

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

Дополнительные сведения о необработанных запросах SQL см. в статье [необработанные запросы SQL](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) в блоге Entity Framework Team.

## <a name="no-tracking-queries"></a>и без отслеживания

Когда контекст базы данных получает строки базы данных и создает объекты сущностей, которые их представляют, по умолчанию он отслеживает, синхронизированы ли сущности в памяти с базой данных. При обновлении сущности данные в памяти выступают в роли кэша. В веб-приложении такое кэширование часто не нужно, поскольку экземпляры контекста, как правило, существуют недолго (для каждого запроса создается и ликвидируется собственный экземпляр), и контекст, считывающий сущность, как правило, ликвидируется до того, как сущность будет использована снова.

Можно указать, будет ли контекст отслеживать объекты сущностей для запроса с помощью `AsNoTracking` метода. Как правило, это требуется в следующих сценариях:

- Запрос получает такой большой объем данных, при котором отключение отслеживания может заметно повысить производительность.
- Вы хотите присоединить сущность, чтобы обновить ее, но вы ранее извлекли ту же сущность для другой цели. Поскольку сущность уже отслеживается контекстом базы данных, присоединить сущность, которую требуется изменить, нельзя. Одним из способов предотвращения этого является использование `AsNoTracking` параметра с предыдущим запросом.

В этом разделе вы реализуете бизнес-логику, которая иллюстрирует второй из этих сценариев. В частности, вы будете применять бизнес-правило, говорящее, что инструктор не может быть администратором более чем одного отдела.

В *DepartmentController.CS*добавьте новый метод, который можно вызвать из `Edit` `Create` методов и, чтобы убедиться, что ни один из двух отделов не имеет одного и того же администратора:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

Добавьте код в `try` блок `HttpPost` `Edit` метода, чтобы вызвать этот новый метод, если нет ошибок проверки. `try`Теперь этот блок выглядит как в следующем примере:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

Запустите страницу редактирования отдела и попробуйте изменить администратора отдела на лектора, который уже является администратором другого отдела. Вы получаете ожидаемое сообщение об ошибке:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

Теперь снова запустите страницу редактирования отдела, и на этот раз измените сумму **бюджета** . При нажатии кнопки **сохранить**отображается страница ошибки.

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

Сообщение об ошибке Exception " `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` " это произошло из-за следующей последовательности событий:

- `Edit`Метод вызывает `ValidateOneAdministratorAssignmentPerInstructor` метод, который извлекает все отделы, имеющие в качестве администратора Kim аберкромбие. Это приводит к считыванию английского Отдела. Так как это редактируемый отдел, сообщения об ошибках не выводятся. Однако в результате этой операции чтения сущность «Отдел по английскому», считанная из базы данных, теперь отслеживается контекстом базы данных.
- `Edit`Метод пытается установить `Modified` флаг для сущности в русском отделе, созданной связывателем модели MVC, но это не удается, так как контекст уже отслеживает сущность для английского Отдела.

Одним из решений этой проблемы является обеспечение контекста от отслеживания сущностей в памяти в подразделении, извлеченных запросом проверки. Это не имеет смысла, так как вы не обновляете эту сущность или не читаете ее повторно, чтобы использовать ее для кэширования в памяти.

В *DepartmentController.CS*в `ValidateOneAdministratorAssignmentPerInstructor` методе укажите параметр без отслеживания, как показано ниже:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

Повторите попытку изменения суммы **бюджета** для отдела. На этот раз операция завершается успешно, и сайт возвращается ожидаемым образом на страницу индекса отделов, отображая пересмотренное значение бюджета.

## <a name="examining-queries-sent-to-the-database"></a>Проверка запросов, отправленных в базу данных

В некоторых случаях полезно иметь возможность просмотреть фактические SQL-запросы, отправляемые в базу данных. Для этого можно проверить переменную запроса в отладчике или вызвать `ToString` метод запроса. Чтобы попробовать это, рассмотрим простой запрос, а затем посмотрим, что происходит с ним при добавлении параметров, таких как упреждающая загрузка, фильтрация и сортировка.

В *Controllers/каурсеконтроллер*замените `Index` метод следующим кодом:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

Теперь установите точку останова в *GenericRepository.CS* в `return query.ToList();` `return orderBy(query).ToList();` инструкциях и для `Get` метода. Запустите проект в режиме отладки и выберите страницу индекса курса. Когда код достигает точки останова, изучите `query` переменную. Отобразится запрос, отправленный в SQL Server. Это простая `Select` Инструкция:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.sql)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

Запросы могут быть слишком длинными для отображения в окнах отладки в Visual Studio. Чтобы просмотреть весь запрос, можно скопировать значение переменной и вставить его в текстовый редактор:

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

Теперь вы добавите раскрывающийся список на страницу индекса курса, чтобы пользователи могли выполнять фильтрацию по определенному отделу. Вы сортируете курсы по названию и указываете безотлагательную загрузку для `Department` Свойства навигации. В *CourseController.CS*замените `Index` метод следующим кодом:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

Метод получает выбранное значение раскрывающегося списка в `SelectedDepartment` параметре. Если ничего не выбрано, этот параметр будет иметь значение null.

`SelectList`Коллекция, содержащая все отделы, передается в представление раскрывающегося списка. Параметры, передаваемые в `SelectList` конструктор, указывают имя поля значения, имя текстового поля и выбранный элемент.

Для `Get` метода `Course` репозитория в коде указывается критерий фильтра, порядок сортировки и упреждающая загрузка для `Department` Свойства навигации. Критерий фильтра всегда возвращает значение, `true` Если в раскрывающемся списке ничего не выбрано (то есть `SelectedDepartment` равно null).

В *виевс\каурсе\индекс.кштмл*непосредственно перед открывающим `table` тегом добавьте следующий код, чтобы создать раскрывающийся список и кнопку отправки:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

Если в классе все еще заданы точки останова `GenericRepository` , запустите страницу индекса курса. Продолжайте первые два раза, когда код достигает точки останова, чтобы страница отображалась в браузере. Выберите отдел в раскрывающемся списке и щелкните **Фильтр**:

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

На этот раз первая точка останова будет относиться к запросу отделов для раскрывающегося списка. Пропустите эту переменную и просмотрите ее в `query` следующий раз, когда код достигнет точки останова, чтобы увидеть, как будет выглядеть `Course` запрос. Вы увидите нечто вроде следующего:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.sql)]

Вы видите, что запрос теперь является `JOIN` запросом, который загружает `Department` данные вместе с `Course` данными и включает `WHERE` предложение.

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>Работа с классами прокси

Когда Entity Framework создает экземпляры сущности (например, при выполнении запроса), она часто создает их как экземпляры динамически создаваемого производного типа, который выступает в качестве прокси-сервера для сущности. Этот прокси-сервер переопределяет некоторые виртуальные свойства сущности, чтобы вставлять обработчики для выполнения действий автоматически при обращении к свойству. Например, этот механизм используется для поддержки отложенной загрузки связей.

В большинстве случаев вам не нужно знать об использовании прокси-серверов, но существуют исключения.

- В некоторых случаях может потребоваться запретить Entity Framework создавать экземпляры прокси-сервера. Например, сериализация экземпляров, не являющихся прокси-сервером, может оказаться более эффективной, чем сериализация экземпляров прокси-сервера.
- При создании экземпляра класса сущности с помощью `new` оператора вы не получаете экземпляр прокси-сервера. Это означает, что вы не получаете такие функции, как отложенная загрузка и автоматическое отслеживание изменений. Обычно это нормально. обычно отложенная загрузка не требуется, так как создается новая сущность, которая не находится в базе данных, и обычно не требуется отслеживание изменений, если вы явно помечаете сущность как `Added` . Однако, если требуется отложенная загрузка и требуется отслеживание изменений, можно создать новые экземпляры сущностей с прокси-сервером с помощью `Create` метода `DbSet` класса.
- Может потребоваться получить фактический тип сущности из прокси-типа. `GetObjectType` `ObjectContext` Для получения фактического типа сущности экземпляра прокси-типа можно использовать метод класса.

Дополнительные сведения см. в разделе [Работа с прокси-серверами](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) в блоге Entity Framework Team.

## <a name="disabling-automatic-detection-of-changes"></a>Отключение автоматического обнаружения изменений

Платформа Entity Framework определяет, как была изменена сущность (и, соответственно, какие обновления требуется отправить в базу данных), сравнивая текущие значения сущности с исходными. Исходные значения сохраняются при запросе или присоединении сущности. Ниже перечислены некоторые из методов, которые приводят к автоматическому обнаружению изменений:

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

Если вы отслеживаете большое количество сущностей и вызываете один из этих методов несколько раз в цикле, вы можете значительно повысить производительность, временно отключив автоматическое обнаружение изменений с помощью свойства [аутодетектчанжесенаблед](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) . Дополнительные сведения см. в разделе [Автоматическое обнаружение изменений](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).

## <a name="disabling-validation-when-saving-changes"></a>Отключение проверки при сохранении изменений

При вызове `SaveChanges` метода по умолчанию Entity Framework проверяет данные во всех свойствах всех измененных сущностей перед обновлением базы данных. Если вы обновили большое количество сущностей и уже проверили данные, эта работа не требуется, и процесс сохранения изменений займет меньше времени, временно отключив проверку. Это можно сделать с помощью свойства [валидатеонсавинаблед](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) . Дополнительные сведения см. в разделе [Проверка](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).

## <a name="summary"></a>Сводка

Эта серия руководств по использованию Entity Framework в приложении MVC ASP.NET. Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

Дополнительные сведения о том, как развернуть веб-приложение после его создания, см. в статье [Схема содержимого ASP.NET Deployment](https://msdn.microsoft.com/library/bb386521.aspx) в библиотеке MSDN.

Сведения о других темах, связанных с MVC, таких как проверка подлинности и авторизация, см. в разделе [Рекомендуемые ресурсы MVC](../../getting-started/recommended-resources-for-mvc.md).

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>Благодарности

- Tom Dykstra) написал первоначальную версию этого учебника и является старшим руководством по программированию для веб-платформы Майкрософт и разработчиков содержимого инструментов.
- [Рик Андерсон (](https://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) соавторство этого руководства и выполнил большую часть работы по обновлению для EF 5 и MVC 4. Рик — старший специалист по программированию для Microsoft, сосредоточенный на Azure и MVC.
- [Роуэн Миллер](http://www.romiller.com) и другие члены группы разработчиков Entity Framework, которые были полезны при проверке кода, и помогли отладить многие проблемы с миграциями, возник при обновлении руководства по EF 5.

## <a name="vb"></a>VB

Когда учебник был изначально создан, мы предоставили версии C# и VB завершенного проекта загрузки. В этом обновлении мы предоставляем загружаемый по C# проект для каждой главы, чтобы упростить начало работы в любом месте в ряде, но из-за ограничений по времени и других приоритетов, которые мы не сделали для VB. Если вы создаете проект VB, используя эти учебники, и хотите поделиться им с другими пользователями, сообщите нам о них.

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>Ошибки и способы их решения

### <a name="cannot-createshadow-copy"></a>Не удается создать или теневую копию

Сообщение об ошибке:

*Невозможно создать или теневую копию "Дотнетопенаус. OpenID Connect", если этот файл уже существует.*

Решение:

Подождите несколько секунд и обновите страницу.

### <a name="update-database-not-recognized"></a>Обновление-база данных не распознана

Сообщение об ошибке:

*Термин "обновление базы данных" не распознается как имя командлета, функции, файла сценария или исполняемой программы. Проверьте правильность написания имени или, если путь включен, проверьте правильность пути и повторите* попытку. (Из *`Update-Database`* команды в PMC.)

Решение:

Закройте Visual Studio. Повторно откройте проект и повторите попытку.

### <a name="validation-failed"></a>Проверка завершена с ошибкой

Сообщение об ошибке:

*Проверка не пройдена для одной или нескольких сущностей. Дополнительные сведения см. в свойстве "Ентитивалидатионеррорс".* (Из *`Update-Database`* команды в PMC.)

Решение:

Одной из причин этой проблемы являются ошибки проверки при `Seed` выполнении метода. Советы по отладке метода см. в разделе [Заполнение и отладка Entity Framework (EF) баз данных](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` .

### <a name="http-50019-error"></a>Ошибка HTTP 500,19

Сообщение об ошибке:

*Ошибка HTTP 500,19-Внутренняя ошибка сервера запрошенная страница недоступна из-за недопустимых данных конфигурации для этой страницы.*

Решение:

Одним из способов получения этой ошибки может быть наличие нескольких копий решения, каждый из которых использует один и тот же номер порта. Обычно эту проблему можно решить, выполнив все экземпляры Visual Studio, а затем перезапустив проект, над которым вы работаете. Если это не поможет, попробуйте изменить номер порта. Щелкните правой кнопкой мыши файл проекта и выберите пункт Свойства. Перейдите на вкладку **веб** и измените номер порта в текстовом поле **URL-адрес проекта** .

### <a name="error-locating-sql-server-instance"></a>Ошибка при обнаружении экземпляра SQL Server

Сообщение об ошибке:

*При установлении соединения с SQL Server возникла ошибка, связанная с сетью или экземпляром. Сервер не найден или недоступен. Убедитесь, что имя экземпляра указано правильно и что SQL Server настроено для разрешения удаленных подключений. (поставщик: Сетевые интерфейсы SQL, ошибка: 26-ошибка при поиске указанного сервера или экземпляра)*

Решение:

Проверьте строку подключения. Если вы вручную удалили базу данных, измените имя базы данных в строке конструирования.

> [!div class="step-by-step"]
> [Назад](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [Вперед](building-the-ef5-mvc4-chapter-downloads.md)
