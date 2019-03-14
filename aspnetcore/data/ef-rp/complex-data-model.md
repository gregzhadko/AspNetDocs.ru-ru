---
title: Razor Pages с EF Core в ASP.NET Core — модель данных— 5 из 8
author: rick-anderson
description: В этом руководстве вы добавите дополнительные сущности и связи, а также настроите модель данных, указав правила форматирования, проверки и сопоставления.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: data/ef-rp/complex-data-model
ms.openlocfilehash: 1dc9f1278e502cd5040e82c18d99e2da6f139568
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052811"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---data-model---5-of-8"></a>Razor Pages с EF Core в ASP.NET Core — модель данных— 5 из 8

[!INCLUDE[2.0 version](~/includes/RP-EF/20-pdf.md)]

::: moniker range=">= aspnetcore-2.1"

Авторы: [Том Дайкстра](https://github.com/tdykstra) (Tom Dykstra) и [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

[!INCLUDE [about the series](~/includes/RP-EF/intro.md)]

Предыдущие руководства работали с базовой моделью данных, состоящей из трех сущностей. В этом руководстве:

* Добавляются дополнительные сущности и связи.
* Настраивается модель данных с помощью указания правил для форматирования, проверки и сопоставления базы данных.

Классы сущностей для готовой модели данных показаны на следующем рисунке:

![Схема сущностей](complex-data-model/_static/diagram.png)

При возникновении проблем, которые вам не удается устранить, скачайте [готовое приложение](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples).

## <a name="customize-the-data-model-with-attributes"></a>Настройка модели данных с использованием атрибутов

В этом разделе модель данных настраивается с помощью атрибутов.

### <a name="the-datatype-attribute"></a>Атрибут DataType

Страницы учащихся сейчас отображают время и дату зачисления. Как правило, поля даты отображают только дату без времени.

Обновите *Models/Student.cs*, используя следующий выделенный код:

[!code-csharp[](intro/samples/cu21/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

Атрибут [DataType](/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) указывает тип данных более точно по сравнению со встроенным типом базы данных. В этом случае следует отображать отобразить только дату, а не дату и время. В [перечислении DataType](/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) представлено множество типов данных, таких как Date, Time, PhoneNumber, Currency, EmailAddress и других. Атрибут `DataType` также обеспечивает автоматическое предоставление функций для определенных типов в приложении. Пример:

* Ссылка `mailto:` для `DataType.EmailAddress` создается автоматически.
* Средство выбора даты предоставляется для `DataType.Date` в большинстве браузеров.

Атрибут `DataType` создает атрибуты HTML 5 `data-`, которые используются браузерами с поддержкой HTML 5. Атрибуты `DataType` не предназначены для проверки.

`DataType.Date` не задает формат отображаемой даты. По умолчанию поле даты отображается с использованием форматов, установленных в [CultureInfo](xref:fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support) сервера.

С помощью атрибута `DisplayFormat` можно явно указать формат даты:

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

Параметр `ApplyFormatInEditMode` указывает, что формат должен применяться к пользовательскому интерфейсу редактирования. Некоторым полям не следует использовать `ApplyFormatInEditMode`. Например, обозначение денежной единицы в общем случае не должно отображаться в поле редактирования текста.

Атрибут `DisplayFormat` можно использовать отдельно. Однако чаще всего `DataType` рекомендуется применять вместе с атрибутом `DisplayFormat`. Атрибут `DataType` передает семантику данных (в отличие от способа их вывода на экран). Атрибут `DataType` дает следующие преимущества, недоступные в `DisplayFormat`:

* Поддержка функций HTML5 в браузере. Например, отображение элемента управления календарем, соответствующего языковому стандарту обозначения денежной единицы, ссылок электронной почты, проверки входных данных на стороне клиента и т. д.
* По умолчанию формат отображения данных в браузере определяется в соответствии с установленным языковым стандартом.

Дополнительные сведения см. в документации по [вспомогательной функции тегов \<input>](xref:mvc/views/working-with-forms#the-input-tag-helper).

Запустите приложение. Перейдите на страницу индекса учащихся. Время больше не отображается. Каждое представление, использующее модель `Student`, отображает дату без времени.

![Страница указателя учащихся с датами без времени](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a>Атрибут StringLength

С помощью атрибутов можно указать правила проверки данных и сообщения об ошибках проверки. Атрибут [StringLength](/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) указывает минимальную и максимальную длину символов, разрешенных в поле данных. Атрибут `StringLength` также обеспечивает проверку на стороне клиента и на стороне сервера. Минимальное значение не оказывает влияния на схему базы данных.

Обновите модель`Student`, используя следующий код:

[!code-csharp[](intro/samples/cu21/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

Предыдущий код задает ограничение длины имен в 50 символов. Атрибут `StringLength` не запрещает пользователю ввести пробел в качестве имени пользователя. Атрибут [RegularExpression](/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) используется для применения ограничений к входным данным. Например, следующий код требует, чтобы первый символ был прописной буквой, а остальные символы были буквенными:

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]
```

Запустите приложение:

* Перейдите на страницу учащихся.
* Выберите **Create New** (Создать) и введите имя длиной более 50 символов.
* Выберите **Create** (Создать), проверка на стороне клиента отображает сообщение об ошибке.

![Страница указателя учащихся с ошибками длины строки](complex-data-model/_static/string-length-errors.png)

В **обозревателе объектов SQL Server** (SSOX) откройте конструктор таблиц учащихся, дважды щелкнув таблицу **Student** (Учащийся).

![Таблица учащихся в SSOX до миграций](complex-data-model/_static/ssox-before-migration.png)

На предыдущем изображении показана схемы для таблицы `Student`. Поля имен имеют тип `nvarchar(MAX)`, так как миграции для базы данных не выполнялись. Когда в дальнейшем миграции будут выполнены, поля имен станут `nvarchar(50)`.

### <a name="the-column-attribute"></a>Атрибут Column

Атрибуты могут управлять, как именно классы и свойства сопоставляются с базой данных. В этом разделе атрибут `Column` используется для сопоставления имени свойства `FirstMidName` с "FirstName" в базе данных.

При создании базы данных имена свойств в модели используются для имен столбцов (кроме случая, когда используется атрибут `Column`).

Модель `Student` использует `FirstMidName` для поля имени, так как это поле также может содержать отчество.

Обновите файл *Student.cs*, используя следующий выделенный код:

[!code-csharp[](intro/samples/cu21/Models/Student.cs?name=snippet_Column&highlight=4,14)]

С учетом предыдущего изменения `Student.FirstMidName` в приложении сопоставляется со столбцом `FirstName` таблицы `Student`.

Добавление атрибута `Column` изменяет модель для поддержки `SchoolContext`. Модель, поддерживающая `SchoolContext`, больше не соответствует базе данных. Если приложение запускается перед применением миграций, возникает следующее исключение:

```SQL
SqlException: Invalid column name 'FirstName'.
```

Для обновления базы данных сделайте следующее:

* Выполните построение проекта.
* Откройте командное окно в папке проекта. Введите следующие команды для создания миграции и обновления базы данных:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

```PMC
Add-Migration ColumnFirstName
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

```console
dotnet ef migrations add ColumnFirstName
dotnet ef database update
```

------

Команда `migrations add ColumnFirstName` выдает следующее предупреждающее сообщение:

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
```

Это предупреждение вызвано тем, что поля имен теперь ограничены 50 символами. Если имя в базе данных имеет больше 50 символов, символы с 51 до последнего будут потеряны.

* Проверьте работу приложения.

Откройте таблицу "Student" (Учащийся) в окне SSOX:

![Таблица учащихся в SSOX после миграций](complex-data-model/_static/ssox-after-migration.png)

До применения миграции столбцы имен имели тип [nvarchar(MAX)](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql). Теперь столбцы имен имеют тип `nvarchar(50)`. Имя столбца изменилось с `FirstMidName` на `FirstName`.

> [!Note]
> В следующем разделе сборка приложения на некоторых этапах приводит к возникновению ошибок компилятора. В инструкциях указано, когда производить сборку приложения.

## <a name="student-entity-update"></a>Обновление сущности Student

![Сущность Student](complex-data-model/_static/student-entity.png)

Обновите *Models/Student.cs*, используя следующий код:

[!code-csharp[](intro/samples/cu21/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a>Атрибут Required

Атрибут `Required` делает свойства имен обязательными полями. Атрибут `Required` не нужен для типов, не допускающих значения null, например для типов значений (`DateTime`, `int`, `double` и т. д.). Типы, которые не могут принимать значение null, автоматически обрабатываются как обязательные поля.

Атрибут `Required` можно заменить параметром минимальной длины в атрибуте `StringLength`:

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a>Атрибут Display

Атрибут `Display` указывает, что заголовки для текстовых полей должны иметь вид "First Name" (Имя), "Last Name" (Фамилия), "Full Name" (Полное имя) и "Enrollment Date" (Дата зачисления). По умолчанию в заголовках не использовался пробел для разделения слов, например "Lastname".

### <a name="the-fullname-calculated-property"></a>Вычисляемое свойство FullName

`FullName` — это вычисляемое свойство, которое возвращает значение, созданное путем объединения двух других свойств. `FullName` не может быть задано, оно имеет только метод доступа get. В базе данных не создается столбец `FullName`.

## <a name="create-the-instructor-entity"></a>Создание сущности Instructor

![Сущность Instructor](complex-data-model/_static/instructor-entity.png)

Создайте файл *Models/Instructor.cs* со следующим кодом:

[!code-csharp[](intro/samples/cu21/Models/Instructor.cs)]

На одной строке могут находиться несколько атрибутов. Атрибуты `HireDate` можно записать следующим образом:

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a>Свойства навигации CourseAssignments и OfficeAssignment

`CourseAssignments` и `OfficeAssignment` — это свойства навигации.

Преподаватель может проводить любое количество курсов, поэтому `CourseAssignments` определен как коллекция.

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

Если свойство навигации содержит несколько сущностей:

* Оно должно быть типом списка, где можно добавлять, удалять и обновлять записи.

К типам свойств навигации относятся следующие:

* `ICollection<T>`
*  `List<T>`
*  `HashSet<T>`

Если указан тип `ICollection<T>`, платформа EF Core по умолчанию создает коллекцию `HashSet<T>`.

Сущность `CourseAssignment` описана в разделе по связям многие ко многим.

Бизнес-правила университета Contoso указывают, что преподаватель может иметь не более одного кабинета. Свойство `OfficeAssignment` содержит отдельную сущность `OfficeAssignment`. `OfficeAssignment` имеет значение null, если кабинет не назначен.

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a>Создание сущности OfficeAssignment

![Сущность OfficeAssignment](complex-data-model/_static/officeassignment-entity.png)

Создайте файл *Models/OfficeAssignment.cs* со следующим кодом:

[!code-csharp[](intro/samples/cu21/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a>Атрибут Key

Атрибут `[Key]` используется для идентификации свойства в качестве первичного ключа (PK), когда имя свойства отличается от classnameID или ID.

Между сущностями `Instructor` и `OfficeAssignment` действует связь один к нулю или к одному. Назначение кабинета существует только в связи с преподавателем, которому оно назначено. Первичный ключ `OfficeAssignment` также является внешним ключом (FK) для сущности `Instructor`. EF Core не распознает автоматически `InstructorID` как первичный ключ объекта `OfficeAssignment` по следующей причине:

* `InstructorID` не соблюдает соглашение об именовании ID или classnameID.

Таким образом, атрибут `Key` используется для определения `InstructorID` в качестве первичного ключа:

```csharp
[Key]
public int InstructorID { get; set; }
```

По умолчанию EF Core считает ключ созданным не базой данных, так как столбец предназначен для идентифицирующего отношения.

### <a name="the-instructor-navigation-property"></a>Свойство навигации Instructor

Свойство навигации `OfficeAssignment` для сущности `Instructor` допускает значение null по следующим причинам:

* Ссылочные типы (например, классы) допускают значение null.
* Преподавателю может быть не назначен кабинет.


Сущность `OfficeAssignment` имеет свойство навигации `Instructor`, не допускающее значение null, по следующим причинам:

* `InstructorID` не допускает значение null.
* Назначение кабинета не может существовать без преподавателя.

Когда сущность `Instructor` имеет связанную сущность `OfficeAssignment`, каждая из них имеет ссылку на другую в своем свойстве навигации.

Атрибут `[Required]` можно применить к свойству навигации `Instructor`:

```csharp
[Required]
public Instructor Instructor { get; set; }
```

Предыдущий код указывает, что должен существовать связанный преподаватель. Этот код не нужен, так как внешний ключ `InstructorID` (который также является первичным) не допускает значение null.

## <a name="modify-the-course-entity"></a>Изменение сущности Course

![Сущность Course](complex-data-model/_static/course-entity.png)

Обновите *Models/Course.cs*, используя следующий код:

[!code-csharp[](intro/samples/cu21/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

Сущность `Course` имеет свойство внешнего ключа (FK) `DepartmentID`. `DepartmentID` указывает на связанную сущность `Department`. Сущность `Course` имеет свойство навигации `Department`.

EF Core не требует свойство внешнего ключа для модели данных, если она имеет свойство навигации для связанной сущности.

EF Core автоматически создает внешние ключи в базе данных по мере необходимости. EF Core создает [теневые свойства](/ef/core/modeling/shadow-properties) для автоматически созданных внешних ключей. Наличие внешнего ключа в модели данных позволяет сделать обновления проще и эффективнее. Например, рассмотрим модель, где свойство внешнего ключа `DepartmentID` *не* включено. При получении сущности курса для редактирования:

* сущность `Department` имеет значение null, если она не загружена явно;
* для обновления сущности курса нужно сначала получить сущность `Department`.

Если свойство внешнего ключа `DepartmentID` включено в модель данных, получать сущность `Department` перед обновлением не нужно.

### <a name="the-databasegenerated-attribute"></a>Атрибут DatabaseGenerated

Атрибут `[DatabaseGenerated(DatabaseGeneratedOption.None)]` указывает, что первичный ключ предоставляется приложением, а не создается базой данных.

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

По умолчанию EF Core предполагает, что значения первичного ключа создаются базой данных. Обычно лучше всего использовать значения первичного ключа, созданные базой данных. Для сущностей `Course` пользователь указывает первичный ключ. Например, номер курса, такой как серия 1000 для кафедры математики и серия 2000 для кафедры английского языка.

Атрибут `DatabaseGenerated` также может использоваться для создания значений по умолчанию. Например, база данных может автоматически создать поле даты для записи даты, когда строка была создана или изменена. Дополнительные сведения см. в разделе [Созданные свойства](/ef/core/modeling/generated-properties).

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа (FK) и свойства навигации в сущности `Course` отражают следующие связи:

Курс назначается одной кафедре, поэтому имеется внешний ключ `DepartmentID` и свойство навигации `Department`.

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

На курс может быть зачислено любое количество учащихся, поэтому свойство навигации `Enrollments` является коллекцией:

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

Курс могут вести несколько преподавателей, поэтому свойство навигации `CourseAssignments` является коллекцией:

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

`CourseAssignment` описано [далее](#many-to-many-relationships).

## <a name="create-the-department-entity"></a>Создание сущности Department

![Сущность Department](complex-data-model/_static/department-entity.png)

Создайте файл *Models/Department.cs* со следующим кодом:

[!code-csharp[](intro/samples/cu21/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a>Атрибут Column

Ранее атрибут `Column` использовался, чтобы изменить сопоставление имени столбца. В коде для сущности `Department` атрибут `Column` можно использовать, чтобы изменить сопоставление типов данных SQL. Столбец `Budget` определяется с помощью типа money SQL Server в базе данных:

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

Сопоставление столбцов обычно не требуется. В общем случае EF Core выбирает соответствующий тип данных SQL Server на основе типа среды CLR для свойства. Тип `decimal` среды CLR сопоставляется с типом `decimal` SQL Server. `Budget` используется для денежных единиц, хотя для этого лучше подходит тип данных money.

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и навигации отражают следующие связи:

* Кафедра может иметь или не иметь администратора.
* Администратор всегда является преподавателем. Поэтому свойство `InstructorID` включается в качестве внешнего ключа в сущность `Instructor`.

Свойство навигации называется `Administrator`, но содержит сущность `Instructor`:

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

Вопросительный знак (?) в приведенном выше коде указывает, что свойство допускает значение null.

Кафедра может иметь несколько курсов, поэтому доступно свойство навигации Courses:

```csharp
public ICollection<Course> Courses { get; set; }
```

Примечание. По соглашению EF Core разрешает каскадное удаление для внешних ключей, не допускающих значение null, и связей "многие ко многим". Каскадное удаление может привести к циклическим правилам каскадного удаления. Такие правила вызывают исключение при добавлении миграции.

Например, если свойство `Department.InstructorID` не было определено как допускающее значение null:

* EF Core настраивает правило каскадного удаления для удаления преподавателя при удалении кафедры.
* Удаление преподавателя при удалении кафедры не является запланированным поведением.

Если бизнес-правила требуют, чтобы свойство `InstructorID` не допускало значение null, используйте следующий оператор текучего API:

 ```csharp
 modelBuilder.Entity<Department>()
    .HasOne(d => d.Administrator)
    .WithMany()
    .OnDelete(DeleteBehavior.Restrict)
 ```

Предыдущий код отключает каскадное удаление для связи кафедры и преподавателя.

## <a name="update-the-enrollment-entity"></a>Обновление сущности Enrollment

Запись зачисления обозначает один курс, который проходит один учащийся.

![Сущность Enrollment](complex-data-model/_static/enrollment-entity.png)

Обновите *Models/Enrollment.cs*, используя следующий код:

[!code-csharp[](intro/samples/cu21/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a>Свойства внешнего ключа и навигации

Свойства внешнего ключа и навигации отражают следующие связи:

Запись зачисления предназначена для одного курса, поэтому доступно свойство первичного ключа `CourseID` и свойство навигации `Course`:

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

Запись зачисления предназначена для одного учащегося, поэтому доступно свойство первичного ключа `StudentID` и свойство навигации `Student`:

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a>Связи многие ко многим

Между сущностями `Student` и `Course` действует связь многие ко многим. Сущности `Enrollment` выступают в качестве таблицы соединения многие ко многим *с полезными данными* в базе данных. Фраза "с полезными данными" означает, что таблица `Enrollment` содержит дополнительные данные, кроме внешних ключей для присоединяемых таблиц (в данном случае — первичный ключ и `Grade`).

На следующем рисунке показано, как выглядят эти связи на схеме сущностей. (Эта схема была создана с помощью [EF Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) для EF 6.x. Создание схемы не является частью руководства.)

![Связь многие ко многим между Student и Course](complex-data-model/_static/student-course.png)

Каждая линия связи имеет 1 на одном конце и звездочку (*) на другом, указывая характер один ко многим.

Если таблица `Enrollment` не включала в себя сведения об оценках, ей потребуется содержать всего два внешних ключа (`CourseID` и `StudentID`). Таблицу соединения многие ко многим без полезных данных иногда называют чистой таблицей соединения (PJT).

Сущности `Instructor` и `Course` имеют связь многие ко многим с использованием чистой таблицы соединения.

Примечание. EF 6.x поддерживает неявные таблицы соединения для связей многие ко многим, но EF Core — нет. Дополнительные сведения см. в статье [Связи многие ко многим в EF Core 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/).

## <a name="the-courseassignment-entity"></a>Сущность CourseAssignment

![Сущность CourseAssignment](complex-data-model/_static/courseassignment-entity.png)

Создайте файл *Models/CourseAssignment.cs* со следующим кодом:

[!code-csharp[](intro/samples/cu21/Models/CourseAssignment.cs)]

### <a name="instructor-to-courses"></a>Связь между Instructor и Courses

![Связь многие ко многим между Instructor и Courses](complex-data-model/_static/courseassignment.png)

Связь многие ко многим между Instructor и Courses:

* Нуждается в таблице соединения, которая должна быть представлена набором сущностей.
* Является чистой таблицей соединения (таблицей без полезных данных).

Обычно для сущности соединения используется имя `EntityName1EntityName2`. Например, таблицей соединения Instructor и Courses, использующей этот шаблон, является `CourseInstructor`. Однако рекомендуется использовать имя, которое описывает эту связь.

Модели данных создаются простыми и разрастаются. Соединения без полезных данных (PJT) часто начинают включать их. Если в начале задать описательное имя сущности, его не нужно менять при изменениях таблицы соединения. Оптимально, если сущность соединения имеет собственное естественное имя (возможно, из одного слова) в бизнес-среде. Например, Books и Customers можно связать с сущностью соединения Ratings. Связь многие ко многим между Instructor и Courses `CourseAssignment` является более предпочтительным вариантом, чем `CourseInstructor`.

### <a name="composite-key"></a>Составной ключ

Внешние ключи не допускают значение null. Два внешних ключа в `CourseAssignment` (`InstructorID` и `CourseID`) совместно однозначно определяют каждую строку таблицы `CourseAssignment`. `CourseAssignment` не требуется выделенный первичный ключ. Свойства `InstructorID` и `CourseID` выступают в качестве составного первичного ключа. Единственным способом указать составные первичные ключи для EF Core является *текучий API*. Следующий раздел описывает, как настроить составной первичный ключ.

Составной ключ обеспечивает следующее:

* Для одного курса допускается несколько строк.
* Для одного преподавателя допускается несколько строк.
* Несколько строк для одного преподавателя и курса недопустимы.

Сущность соединения `Enrollment` определяет собственный первичный ключ, поэтому подобные дубликаты возможны. Для предотвращения подобных дубликатов:

* добавьте уникальный индекс для полей внешнего ключа или
* настройте `Enrollment` с первичным составным ключом аналогично `CourseAssignment`. Дополнительные сведения см. в разделе [Индексы](/ef/core/modeling/indexes).

## <a name="update-the-db-context"></a>Изменение контекста базы данных

Добавьте выделенный ниже код в файл *Data/SchoolContext.cs*:

[!code-csharp[](intro/samples/cu21/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

Предыдущий код добавляет новые сущности и настраивает составной первичный ключ сущности `CourseAssignment`.

## <a name="fluent-api-alternative-to-attributes"></a>Текучий API вместо атрибутов

Метод `OnModelCreating` в предыдущем коде использует для настройки поведения EF Core *текучий API*. Этот API называется "текучим", так как часто используется для объединения серии вызовов методов в один оператор. В [следующем коде](/ef/core/modeling/#methods-of-configuration) показан пример текучего API:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

В этом руководстве текучий API используется только для сопоставления базы данных, которое невозможно выполнить с помощью атрибутов. Однако текучий API позволяет задать большинство правил форматирования, проверки и сопоставления, которые можно указать с помощью атрибутов.

Некоторые атрибуты, такие как `MinimumLength`, невозможно применить с текучим API. `MinimumLength` не изменяет схему, он лишь применяет правило проверки минимальной длины.

Некоторые разработчики предпочитают использовать текучий API монопольно, чтобы оставить свои классы сущностей "чистыми". Атрибуты и текучий API можно смешивать. Существует несколько конфигураций, которые можно реализовать только с помощью текучего API (с указанием составного первичного ключа). Существует несколько конфигураций, которые можно реализовать только с помощью атрибутов (`MinimumLength`). Рекомендации по использованию текучего API и атрибутов:

* Выберите один из двух этих подходов.
* Используйте выбранный подход максимально согласованно.

Некоторые атрибуты из этого руководства используются:

* только для проверки (например, `MinimumLength`);
* только для конфигурации EF Core (например, `HasKey`);
* для проверки и конфигурации EF Core (например, `[StringLength(50)]`).

Дополнительные сведения о сравнении атрибутов и текучего API см. в разделе [Методы конфигурации](/ef/core/modeling/#methods-of-configuration).

## <a name="entity-diagram-showing-relationships"></a>Схема сущностей, показывающая связи

Ниже показана схема, создаваемая средствами EF Power Tools для завершенной модели School.

![Схема сущностей](complex-data-model/_static/diagram.png)

На предыдущей схеме показано следующее:

* Несколько линий связи один ко многим (1 к \*).
* Линия связи один к нулю или одному (1 к 0..1) между сущностями `Instructor` и `OfficeAssignment`.
* Линия связи нуль или один ко многим (0..1 к *) между сущностями `Instructor` и `Department`.

## <a name="seed-the-db-with-test-data"></a>Заполнение базы данных тестовыми данными

Обновите код в файле *Data/DbInitializer.cs*:

[!code-csharp[](intro/samples/cu21/Data/DbInitializer.cs?name=snippet_Final)]

Предыдущий код предоставляет начальные данные для новых сущностей. Основная часть кода создает объекты сущностей и загружает демонстрационные данные. Демонстрационные данные используются для проверки. См. `Enrollments` и `CourseAssignments`, чтобы ознакомиться с примерами заполнения данными таблиц соединения "многие ко многим".

## <a name="add-a-migration"></a>Добавление миграции

Выполните построение проекта.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

```PMC
Add-Migration ComplexDataModel
```

# <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

```console
dotnet ef migrations add ComplexDataModel
```

------

Предыдущая команда отображает предупреждение о возможной потере данных.

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

При выполнении команды `database update` возникает следующая ошибка:

```text
The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in
database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.
```

## <a name="apply-the-migration"></a>Применение миграции

Теперь у вас есть база данных, и пора подумать о том, как применять к ней будущие изменения. В этом руководстве показано два подхода:

* [Удаление и повторное создание базы данных](#drop)
* [Применение миграции к существующей базе данных](#applyexisting). Хотя этот метод является более сложным и трудоемким, в реальной рабочей среде лучше использовать именно его. **Примечание**. Это необязательный раздел руководства. Вы можете выполнить удаление и повторное создание и пропустить этот раздел. Если вы хотите выполнить инструкции в этом разделе, не выполняйте удаление и повторное создание. 

<a name="drop"></a>

### <a name="drop-and-re-create-the-database"></a>Удаление и повторное создание базы данных

Код в обновленном `DbInitializer` предоставляет начальные данные для новых сущностей. Чтобы выполнить в EF Core принудительное создание новой базы данных, удаление и обновление базы данных:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Выполните следующие команды в **консоли диспетчера пакетов** (PMC):

```PMC
Drop-Database
Update-Database
```

Чтобы просмотреть справочную информацию, выполните команду `Get-Help about_EntityFrameworkCore` в PMC.

# <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

Откройте командное окно и перейдите в папку проекта. Папка проекта содержит файл *Startup.cs*.

Введите в командном окне следующее:

 ```console
 dotnet ef database drop
dotnet ef database update
 ```

------

Запустите приложение. При запуске приложения выполняется метод `DbInitializer.Initialize`. `DbInitializer.Initialize` заполняет новую базу данных.

Откройте базу данных в SSOX:

* Если SSOX был открыт ранее, нажмите кнопку **Обновить**.
* Разверните узел **Таблицы**. Отображаются созданные таблицы.

![Таблицы в SSOX](complex-data-model/_static/ssox-tables.png)

Изучите таблицу **CourseAssignment**:

* Щелкните правой кнопкой мыши таблицу **CourseAssignment** и выберите пункт **Просмотреть данные**.
* Убедитесь, что таблица **CourseAssignment** содержит данные.

![Данные CourseAssignment в SSOX](complex-data-model/_static/ssox-ci-data.png)

<a name="applyexisting"></a>

### <a name="apply-the-migration-to-the-existing-database"></a>Применение миграции к существующей базе данных

Этот раздел является необязательным. Эти действия подходят только в том случае, если вы пропустили предыдущий раздел [Удаление и повторное создание базы данных](#drop).

При выполнении миграций с существующими данными могут действовать ограничения внешнего ключа, которым существующие данные не соответствуют. Для рабочих данных нужно предпринять меры по переносу существующих данных. Этот раздел содержит пример того, как устранить нарушения ограничений внешнего ключа. Вносите эти изменения кода только после создания резервной копии. Не вносите эти изменения кода, если вы выполнили инструкции из предыдущего раздела и обновили базу данных.

Файл *{метка_времени}_ComplexDataModel.cs* содержит следующий код:

[!code-csharp[](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_DepartmentID)]

Предыдущий код добавляет в таблицу `Course` внешний ключ `DepartmentID`, не допускающий значение null. База данных из предыдущего руководства содержит строки в `Course`, поэтому эту таблицу невозможно обновить с помощью миграций.

Чтобы заставить миграцию `ComplexDataModel` работать с существующими данными:

* Изменить код, чтобы присвоить новому столбцу (`DepartmentID`) значение по умолчанию.
* Создайте фиктивную кафедру с именем "Temp" для использования по умолчанию.

#### <a name="fix-the-foreign-key-constraints"></a>Устранение ограничений внешнего ключа

Обновите метод `Up` в классах `ComplexDataModel`.

* Откройте файл *{метка_времени}_ComplexDataModel.cs*.
* Закомментируйте строку кода, которая добавляет столбец `DepartmentID` в таблицу `Course`.

[!code-csharp[](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

Добавьте выделенный ниже код. Новый код идет после блока `.CreateTable( name: "Department"`.

 [!code-csharp[](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]

После внесения описанных выше изменений существующие строки `Course` будут связаны с кафедрой "Temp" после выполнения метода `ComplexDataModel` `Up`.

Рабочее приложение:

* включает код или сценарии, чтобы добавить строки `Department` и связанные строки `Course` к новым строкам `Department`;
* не использует кафедру "Temp" или значение по умолчанию для `Course.DepartmentID`.

Следующее руководство посвящено связанным данным.

::: moniker-end

> [!div class="step-by-step"]
> [Назад](xref:data/ef-rp/migrations)
> [Вперед](xref:data/ef-rp/read-related-data)
