---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
title: Программная установка значений параметров ObjectDataSource (C#) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим добавление метода к DAL и BLL, который принимает один входной параметр и возвращает данные. В примере будет задан этот параметр...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1c4588bb-255d-4088-b319-5208da756f4d
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
msc.type: authoredcontent
ms.openlocfilehash: 8aa57172abcfc779fa74b128ad76d42c41dc5b98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465942"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-c"></a>Программная установка значений параметров ObjectDataSource (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_6_CS.exe) или [Загрузка PDF-файла](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/datatutorial06cs1.pdf)

> В этом учебнике мы рассмотрим добавление метода к DAL и BLL, который принимает один входной параметр и возвращает данные. В этом примере этот параметр будет задан программно.

## <a name="introduction"></a>Введение

Как было показано в [предыдущем учебном курсе](declarative-parameters-cs.md), для декларативной передачи значений параметров в методы ObjectDataSource можно использовать ряд параметров. Если значение параметра жестко запрограммировано, поступает из веб-элемента управления на странице или находится в любом другом источнике, который читается источником данных `Parameter` объектом, например, это значение может быть привязано к входному параметру без написания строки кода.

Однако могут возникнуть случаи, когда значение параметра поступает из некоторого источника, который еще не учитывается одним из встроенных источников данных `Parameter` объектов. Если наш сайт поддерживал учетные записи пользователей, может потребоваться задать параметр на основе идентификатора пользователя, вошедшего в систему в текущий момент. Или может потребоваться настроить значение параметра перед его отправкой в метод базового объекта ObjectDataSource.

Каждый раз, когда вызывается метод `Select` ObjectDataSource, ObjectDataSource сначала создает свое [событие SELECT](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx). Затем вызывается метод базового объекта ObjectDataSource. После этого срабатывает [выбранное событие](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) ObjectDataSource (рис. 1 иллюстрирует эту последовательность событий). Значения параметров, передаваемые в метод базового объекта ObjectDataSource, можно задать или настроить в обработчике событий для события `Selecting`.

[![выбранное событие ObjectDataSource и события выбора вызываются до и после вызова метода базового объекта](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image1.png)

**Рис. 1**. события `Selected` и `Selecting` ObjectDataSource срабатывают до и после вызова метода базового объекта ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image3.png))

В этом учебнике мы рассмотрим добавление метода к DAL и BLL, который принимает один входной параметр `Month`, типа `int` и возвращает объект `EmployeesDataTable`, заполненный такими сотрудниками, годовщина найма которых находится в указанном `Month`. В нашем примере этот параметр будет задан программно на основе текущего месяца, в котором отображается список «годовщины сотрудников в этом месяце».

Приступим.

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>Шаг 1. Добавление метода в`EmployeesTableAdapter`

Для нашего первого примера необходимо добавить средства для получения тех сотрудников, чьи `HireDate` произошли в указанный месяц. Чтобы обеспечить эту функциональность в соответствии с нашей архитектурой, необходимо сначала создать метод в `EmployeesTableAdapter`, который сопоставляется с соответствующей инструкцией SQL. Чтобы выполнить это, сначала откройте типизированный набор данных Northwind. Щелкните правой кнопкой мыши метку `EmployeesTableAdapter` и выберите команду Добавить запрос.

[![добавить новый запрос в Емплойистаблеадаптер](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image4.png)

**Рис. 2**. Добавление нового запроса в `EmployeesTableAdapter` ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image6.png))

Выберите, чтобы добавить инструкцию SQL, которая возвращает строки. Когда вы найдете на экран указание `SELECT` оператора, будет уже загружена инструкция `SELECT` по умолчанию для `EmployeesTableAdapter`. Просто добавьте в предложение `WHERE`: `WHERE DATEPART(m, HireDate) = @Month`. [DatePart](https://msdn.microsoft.com/library/ms174420.aspx) — это функция T-SQL, которая возвращает определенную часть даты типа `datetime`; в этом случае мы используем `DATEPART` для возврата месяца `HireDate` столбца.

[![возвращать только те строки, в которых столбец HireDate меньше или равен параметру @HiredBeforeDate](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image7.png)

**Рис. 3**. возврат только тех строк, в которых столбец `HireDate` меньше или равен параметру `@HiredBeforeDate` ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image9.png))

Наконец, измените имена методов `FillBy` и `GetDataBy` на `FillByHiredDateMonth` и `GetEmployeesByHiredDateMonth`соответственно.

[![выбрать более подходящие имена методов, чем Филлби и Жетдатаби](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image10.png)

**Рис. 4**. выбор более подходящих имен методов, чем `FillBy` и `GetDataBy` ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image12.png))

Нажмите кнопку Готово, чтобы завершить работу мастера и вернуться к области конструктора набора данных. Теперь `EmployeesTableAdapter` должен включать новый набор методов для доступа к сотрудникам, нанятым в течение указанного месяца.

[![новые методы появляются в область конструкторае набора данных.](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image13.png)

**Рис. 5**. новые методы отображаются в область конструкторае набора данных ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image15.png))

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>Шаг 2. Добавление метода`GetEmployeesByHiredDateMonth(month)`к слою бизнес-логики

Так как наша архитектура приложения использует отдельный слой для бизнес-логики и логики доступа к данным, нам нужно добавить к BLL метод, который обращается к DAL для получения сотрудников, нанятых до указанной даты. Откройте файл `EmployeesBLL.cs` и добавьте следующий метод:

[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample1.cs)]

Как и в случае с другими методами в этом классе, `GetEmployeesByHiredDateMonth(month)` просто вызывает DAL и возвращает результаты.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>Шаг 3. Отображение сотрудников, годовщина найма которых находится в этом месяце

Последний шаг в этом примере — отображение сотрудников, годовщина найма которых составляет этот месяц. Начните с добавления элемента управления GridView на страницу `ProgrammaticParams.aspx` в папке `BasicReporting` и добавьте новый элемент управления ObjectDataSource в качестве источника данных. Настройте ObjectDataSource для использования класса `EmployeesBLL`, `SelectMethod` для которого задано значение `GetEmployeesByHiredDateMonth(month)`.

[![использования класса Емплойисблл](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image16.png)

**Рис. 6**. использование класса `EmployeesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image18.png))

[![SELECT из метода Жетемплойисбихиреддатемонс (month)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image19.png)

**Рис. 7**. выбор из метода `GetEmployeesByHiredDateMonth(month)` ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image21.png))

На последнем экране будет предложено указать источник значения параметра `month`. Так как это значение будет задано программно, оставьте параметр Источник параметра значение по умолчанию нет и нажмите кнопку Готово.

[![параметр источнику параметра оставить значение нет](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image22.png)

**Рис. 8**. Оставьте параметр Источник параметра равным None ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image24.png)).

Будет создан объект `Parameter` в коллекции `SelectParameters` ObjectDataSource, для которой не указано значение.

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample2.aspx)]

Чтобы программно задать это значение, необходимо создать обработчик событий для события `Selecting` ObjectDataSource. Чтобы сделать это, перейдите к представление конструирования и дважды щелкните элемент ObjectDataSource. Кроме того, можно выбрать элемент ObjectDataSource, вернуться к окно свойств и щелкнуть значок с молнией. Затем либо дважды щелкните текстовое поле рядом с событием `Selecting`, либо введите имя обработчика событий, который вы хотите использовать.

![Щелкните значок с молнией в окне "Свойства", чтобы получить список событий веб-элемента управления](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image25.png)

**Рис. 9**. Щелкните значок с молнией в окне свойств, чтобы получить список событий веб-элемента управления

Оба подхода добавляют новый обработчик событий для события `Selecting` ObjectDataSource в класс кода программной части страницы. В этом обработчике событий можно выполнять чтение и запись значений параметров с помощью `e.InputParameters[parameterName]`, где *`parameterName`* является значением атрибута `Name` в теге `<asp:Parameter>` (`InputParameters` коллекция также может индексироваться по порядковому номеру, как в `e.InputParameters[index]`). Чтобы задать для параметра `month` текущий месяц, добавьте следующий объект в обработчик событий `Selecting`:

[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample3.cs)]

При просмотре этой страницы в браузере мы видим, что только один сотрудник был нанят в этом месяце (март) Мария Каллахан, которая была в компании с 1994.

[![сотрудников, годовщины которых показаны в этом месяце](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image26.png)

**Рис. 10**. показаны сотрудники, годовщины которых отображаются в этом месяце ([щелкните, чтобы просмотреть изображение с полным размером](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image28.png))

## <a name="summary"></a>Сводка

Хотя значения параметров ObjectDataSource обычно могут быть заданы декларативно, не требуя строки кода, можно легко задать значения параметров программным способом. Все, что нам нужно сделать, — это создать обработчик событий для события `Selecting` ObjectDataSource, который срабатывает перед вызовом метода базового объекта, и вручную задать значения для одного или нескольких параметров через коллекцию `InputParameters`.

В этом руководстве заканчивается раздел "основные отчеты". В [следующем учебнике](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) описывается раздел сценарии фильтрации и основной информации, в котором мы рассмотрим методы, позволяющие посетителям фильтровать данные и переходить от главного отчета к подробному отчету.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](declarative-parameters-cs.md)
> [Вперед](displaying-data-with-the-objectdatasource-vb.md)
