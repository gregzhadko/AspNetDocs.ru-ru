---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
title: Использование полей TemplateField в элементе управления DetailsView (VB) | Документация Майкрософт
author: rick-anderson
description: Те же поля TemplateField возможности, доступные с помощью GridView, также доступны с помощью элемента управления DetailsView. В этом руководстве мы будем отображать продукты...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0b91d5f8-127d-4f6a-b204-f2e2b35ef703
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9a2f500206bbdc09d8007e10c0c7464f1ba384a3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59395073"
---
# <a name="using-templatefields-in-the-detailsview-control-vb"></a>Использование TemplateField в элементе управления DetailsView (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачайте пример приложения](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_13_VB.exe) или [скачать PDF](using-templatefields-in-the-detailsview-control-vb/_static/datatutorial13vb1.pdf)

> Те же поля TemplateField возможности, доступные с помощью GridView, также доступны с помощью элемента управления DetailsView. В этом руководстве мы будем отображать продукты одновременно в элементе управления DetailsView, содержащий поля TemplateField.


## <a name="introduction"></a>Вступление

TemplateField предлагает большую степень гибкости в визуализации данных, чем BoundField, CheckBoxField, HyperLinkField и другие элементы управления полями данных. В [предыдущем учебном курсе](using-templatefields-in-the-gridview-control-vb.md) рассматривалось использование TemplateField в элементе управления GridView для:

- Отображения нескольких значений полей данных в одном столбце. Говоря конкретнее, `FirstName` и `LastName` поля были объединены в один столбец GridView.
- Используйте альтернативный веб-элемент управления для выражения значения поля данных. Мы узнали, как Показать `HiredDate` значение с помощью календаря.
- Показать сведения о состоянии, на основе базовых данных. Хотя `Employees` таблица не содержит столбец, который возвращает число дней, которое сотрудник провел на работе, мы имели возможность отобразить такую информацию в примере GridView в предыдущем учебном курсе использование TemplateField и метода форматирования.

Те же поля TemplateField возможности, доступные с помощью GridView, также доступны с помощью элемента управления DetailsView. В этом руководстве мы будем отображать продукты одновременно в элементе управления DetailsView, содержащий два поля TemplateField. Первый TemplateField объединит `UnitPrice`, `UnitsInStock`, и `UnitsOnOrder` полей данных в одну строку DetailsView. Второй TemplateField будет отображаться значение `Discontinued` , но будет использовать метод форматирования для отображения «Да», если `Discontinued` является `True`и в противном случае — значение «Нет».


[![TWO TemplateField, используемые для настройки отображения](using-templatefields-in-the-detailsview-control-vb/_static/image2.png)](using-templatefields-in-the-detailsview-control-vb/_static/image1.png)

**Рис. 1**: Два TemplateField, используемые для настройки отображения ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image3.png))


Давайте начнем!

## <a name="step-1-binding-the-data-to-the-detailsview"></a>Шаг 1. Привязка данных к элементу управления DetailsView

Как уже говорилось в предыдущем учебном курсе, при работе с поля TemplateField, часто бывает проще всего начать с создания в элементе управления DetailsView, содержащий только поля BoundField, кроме, а затем добавьте нового поля TemplateField или преобразование существующих полей BoundField в поля TemplateField, как требуется . Таким образом что для начала добавление DetailsView на странице через конструктор и привяжите его к элементу ObjectDataSource, который возвращает список продуктов. Эти действия создадут DetailsView с полей BoundField для каждого из полей нелогических значений продукта и по полю CheckBoxField для одного поля логического значения (Discontinued).

Откройте `DetailsViewTemplateField.aspx` страницы и перетащите DetailsView из области элементов в конструктор. Смарт-теге DetailsView выберите Добавление нового элемента управления ObjectDataSource, который вызывает `ProductsBLL` класса `GetProducts()` метод.


[![Aдд новый элемент управления ObjectDataSource, вызывающего метод GetProducts()](using-templatefields-in-the-detailsview-control-vb/_static/image5.png)](using-templatefields-in-the-detailsview-control-vb/_static/image4.png)

**Рис. 2**: Добавить новый элемент управления ObjectDataSource, Invokes `GetProducts()` метод ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image6.png))


В этом отчете удалить `ProductID`, `SupplierID`, `CategoryID`, и `ReorderLevel` полей BoundField. Далее, изменить порядок полей BoundFields таким образом, чтобы `CategoryName` и `SupplierName` поля BoundField, кроме располагаться сразу после `ProductName` BoundField. Вы можете изменить `HeaderText` свойства и свойства форматирования для поля BoundField, кроме вашему усмотрению. Как и GridView, эти изменения уровня BoundField можно выполнять через поля-диалоговое окно (доступными, щелкнув ссылку Изменить поля в смарт-теге DetailsView) или через декларативный синтаксис. Наконец, очистите DetailsView `Height` и `Width` значения свойств, чтобы разрешить элементу управления DetailsView управления для развертывания на основе отображаемых данных и установите флажок Enable Paging в смарт-тег.

После внесения этих изменений декларативная разметка элемента управления DetailsView должен выглядеть следующим образом:


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample1.aspx)]

Отвлекитесь и просмотрите страницу через обозреватель. На этом этапе вы увидите один продукт (Chai) со строками, показывающими, название продукта, категории, поставщика, цены, единиц на складе, заказанных единиц и его состояние больше не поддерживаются.


[![Tсведения о продукте HE выделяются с помощью серии полей BoundField](using-templatefields-in-the-detailsview-control-vb/_static/image8.png)](using-templatefields-in-the-detailsview-control-vb/_static/image7.png)

**Рис. 3**: Сведения о продукте отображаются с помощью серии полей BoundField ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image9.png))


## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>Шаг 2. Объединение цены, единиц на складе и заказанных единиц в одну строку

DetailsView имеет одну строку для `UnitPrice`, `UnitsInStock`, и `UnitsOnOrder` поля. Можно объединить эти поля данных в одну строку с TemplateField либо путем добавления нового поля TemplateField, либо преобразовав одно из существующих `UnitPrice`, `UnitsInStock`, и `UnitsOnOrder` полей BoundField в поле TemplateField. Хотя лично я предпочитаю, преобразовывать существующие поля BoundFields, давайте потренируемся, путем добавления нового поля TemplateField.

Запустить, щелкнув ссылку Изменить поля в смарт-теге DetailsView, чтобы открыть диалоговое окно "поля". Затем добавьте нового поля TemplateField и задать его `HeaderText` свойство «Цены и инвентаризация» и перемещения нового поля TemplateField, что он находится выше `UnitPrice` BoundField.


[![Aдд нового поля TemplateField в элементе управления DetailsView](using-templatefields-in-the-detailsview-control-vb/_static/image11.png)](using-templatefields-in-the-detailsview-control-vb/_static/image10.png)

**Рис. 4**: Добавление нового поля TemplateField в элементе управления DetailsView ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image12.png))


Так как этого нового поля TemplateField будет содержать значения, отображаемую в данный момент `UnitPrice`, `UnitsInStock`, и `UnitsOnOrder` полей BoundField, давайте удалим их.

Последняя задача для этого шага — для определения `ItemTemplate` разметку для цены и TemplateField инвентаризации, который можно проделать либо через редактирования интерфейса в конструкторе или вручную через декларативный синтаксис серверного элемента управления DetailsView шаблона. Как и в случае с GridView, DetailsView интерфейса изменения шаблонов может осуществляться, щелкнув ссылку Изменить шаблоны смарт-тега. Отсюда можно выбрать шаблон для правки из раскрывающегося списка, а затем добавьте любой веб-элементы управления из панели элементов.

В этом учебнике, начните с добавления элемента управления Label цену и инвентаризации TemplateField `ItemTemplate`. Затем щелкните ссылку Edit DataBindings в смарт-теге элемента управления Label Web и привязать `Text` свойства `UnitPrice` поля.


[![BПоле для свойства Label Text к данным UnitPrice IND](using-templatefields-in-the-detailsview-control-vb/_static/image14.png)](using-templatefields-in-the-detailsview-control-vb/_static/image13.png)

**Рис. 5**: Привязка метки `Text` свойства `UnitPrice` поля данных ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image15.png))


## <a name="formatting-the-price-as-a-currency"></a>Форматирование цены как денежной единицы

В результате этого добавления элемента управления Label Web цены и инвентаризации TemplateField теперь будет отображать только цену для выбранного продукта. Рис. 6 показан снимок экрана ход работы до сих при просмотре через браузер.


[![Tон цены и инвентаризации TemplateField показана цена](using-templatefields-in-the-detailsview-control-vb/_static/image17.png)](using-templatefields-in-the-detailsview-control-vb/_static/image16.png)

**Рис. 6**: Цена и инвентаризации TemplateField показана цена ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image18.png))


Обратите внимание на то, что цена продукта отформатировано как денежная единица. С BoundField, форматирование возможна, задав `HtmlEncode` свойства `False` и `DataFormatString` свойства `{0:formatSpecifier}`. Для TemplateField тем не менее любые инструкции по форматированию должен быть указан в синтаксис привязки данных либо с помощью метода форматирования, определенного где-нибудь в код приложения (например, в классе фонового кода страницы ASP.NET).

Чтобы указать форматирование для синтаксиса привязки данных, используемого в элементе управления Label Web, вернитесь в диалоговое окно привязки данных, щелкнув ссылку Edit DataBindings в смарт-теге метки. Можно ввести инструкции форматирования непосредственно в раскрывающемся списке формат, или выберите один из определенных строк формата. Как и в поле типа BoundField `DataFormatString` свойство, форматирование указывается с помощью `{0:formatSpecifier}`.

Для `UnitPrice` используйте форматирование денежной единицы, указано, выбрав значение соответствующего раскрывающегося списка или введя в поле `{0:C}` вручную.


[![FФормат цены как денежной единицы](using-templatefields-in-the-detailsview-control-vb/_static/image20.png)](using-templatefields-in-the-detailsview-control-vb/_static/image19.png)

**Рис. 7**: Форматирование цены как денежной единицы ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image21.png))


Декларативно спецификация форматирования указывается как второй параметр в `Bind` или `Eval` методы. Параметры, только что созданные в конструкторе, приводят следующее выражение привязки данных в декларативной разметке:


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>Добавление остающихся полей данных к TemplateField

К этому моменту мы отобразили и `UnitPrice` данные полей в цену и TemplateField инвентаризации, но по-прежнему требуется отображать `UnitsInStock` и `UnitsOnOrder` поля. Давайте отобразим их в строке под ценой заключенными в скобки. Из интерфейса изменения шаблонов в конструкторе подобную разметку можно добавить, поместив курсор внутри шаблона и просто введя текст для отображения. Кроме того эту разметку можно ввести напрямую в декларативном синтаксисе.

Добавьте статическую разметку, элементы управления Label Web и синтаксис привязки данных, таким образом, цены и TemplateField инвентаризации сведения о цене и складских следующим образом:

*Цена*  
(**На складе / Заказано:** *UnitsInStock* / *UnitsOnOrder*)

После выполнения этой задачи декларативная разметка вашей DetailsView должен выглядеть следующим образом:


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample3.aspx)]

С этими изменениями мы объединили информация о цене и инвентаризации в одну строку DetailsView.


[![Tон цены и данные инвентаризации отображается на одной строки](using-templatefields-in-the-detailsview-control-vb/_static/image23.png)](using-templatefields-in-the-detailsview-control-vb/_static/image22.png)

**Рис. 8**: Цена и данные инвентаризации отображается на одной строки ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image24.png))


## <a name="step-3-customizing-the-discontinued-field-information"></a>Шаг 3. Настройка сведений неподдерживаемые поля

`Products` Таблицы `Discontinued` столбец имеет значение бита, указывает ли продукт был снят с производства. При привязке к элементу управления источником данных DetailsView (или GridView), логическое значение поля, такие как `Discontinued`, реализованы в виде CheckBoxFields, тогда как поля нелогических значений, такие как `ProductID`, `ProductName`, и т. д., реализованы в виде Поля BoundFields. Выполняет визуализацию CheckBoxField как снятый флажок, проверяется, если значение поля данных является True или не помеченный в противном случае.

Вместо отображения CheckBoxField, нужно вместо отображения текста, указывающее, является ли продукт снят с производства. Для выполнения этой задачи мы могли бы удалить CheckBoxField из элемента управления DetailsView и затем добавьте поле BoundField которого `DataField` было установлено на `Discontinued`. Отвлекитесь и это сделать. После этого изменения DetailsView отображается текст «True» для снятых с производства продуктов и «False» для продуктов, которые по-прежнему активны.


[![Tон строки True и False используются для отображения состояния снят с продажи](using-templatefields-in-the-detailsview-control-vb/_static/image26.png)](using-templatefields-in-the-detailsview-control-vb/_static/image25.png)

**Рис. 9**: Строки True и False используются для отображения состояния Discontinued ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image27.png))


Представьте себе, что мы не хотим видеть строки «True» или «False» для использования, но «Да» и «NO», вместо этого. Такая настройка может выполняться с помощью TemplateField и метода форматирования. Метод форматирования может занять в любое количество входных параметров, но должна возвратить код HTML (в виде строки) для введения в шаблон.

Добавьте метод форматирования к `DetailsViewTemplateField.aspx` класс фонового кода страницы с именем `DisplayDiscontinuedAsYESorNO` , принимающий `Northwind.ProductsRow` объект в качестве входного параметра и возвращает строку. Как уже говорилось в предыдущем учебном курсе, этот метод *необходимо* быть помечен как `Protected` или `Public` чтобы быть доступным из шаблона.


[!code-vb[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample4.vb)]

Этот метод проверяет входной параметр (`discontinued`) и возвращает «Да», если это `True`, в противном случае — значение «Нет».

> [!NOTE]
> В метод форматирования, проверяются в предыдущего учебника Вспомним, что передавался поля данных, которое может содержать `NULL` s и поэтому требуется проверить, если сотрудника `HiredDate` значение свойства было базу данных `NULL` значение до доступ к `EmployeesRow`в `HiredDate` свойство. Такая проверка не требуется здесь с момента `Discontinued` столбец никогда не может иметь базу данных `NULL` присвоенные значения. Кроме того, именно поэтому метод принимает логическое значение входного параметра, вместо того чтобы принимать `ProductsRow` экземпляра или параметр типа `Object`.


Этот метод форматирования завершен, все, что остается лишь вызвать его из TemplateField `ItemTemplate`. Чтобы создать TemplateField либо удалите `Discontinued` BoundField и Добавление нового поля TemplateField или преобразовать `Discontinued` BoundField в поле TemplateField. Затем из представления декларативной разметки, измените TemplateField, чтобы он содержал только ItemTemplate, вызывающий `DisplayDiscontinuedAsYESorNO` метод, передавая значение текущего `ProductRow` экземпляра `Discontinued` свойство. Это может осуществляться через `Eval` метод. В частности TemplateField разметки должен выглядеть так:


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample5.aspx)]

Это приведет к `DisplayDiscontinuedAsYESorNO` метод, вызываемый при отрисовке элемента управления DetailsView, передавая `ProductRow` экземпляра `Discontinued` значение. Так как `Eval` метод возвращает значение типа `Object`, но `DisplayDiscontinuedAsYESorNO` метод ожидает входной параметр типа `Boolean`, мы приводим `Eval` методы возвращают значение `Boolean`. `DisplayDiscontinuedAsYESorNO` Метод вернет «YES» или «NO» в зависимости от значения при получении. Возвращаемое значение равно, что должно отображаться в этом DetailsView строк (см. рис. 10).


[![YES или нет значения, теперь отображаются в строке снят с продажи](using-templatefields-in-the-detailsview-control-vb/_static/image29.png)](using-templatefields-in-the-detailsview-control-vb/_static/image28.png)

**Рис. 10**: Да или нет значения: теперь отображаются в строке Discontinued ([Просмотр полноразмерного изображения](using-templatefields-in-the-detailsview-control-vb/_static/image30.png))


## <a name="summary"></a>Сводка

TemplateField в элементе управления DetailsView обеспечивает более высокий уровень гибкости в отображении данных, чем другие элементы управления полями и идеально подходят для ситуаций, где:

- Несколько полей данных должны отображаться в одном столбце GridView
- Данные удобнее представить в веб-элемента управления, а не обычный текст
- Результат зависит от базовых данных, такие как отображение метаданных или переформатирования данных

Если поля TemplateField необходимы для большую степень гибкости в визуализации базовых данных DetailsView, выходные данные DetailsView сыроватой угловат как каждое поле визуализируется как строка в HTML- `<table>`.

Элемент управления FormView предоставляет большую степень гибкости в настройке выводимых данных. FormView не содержит полей, но вместо этого он только серию шаблонов (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`, и так далее). Узнаете, как использование FormView для достижения еще большей степени контроля над визуализируемой компоновкой в нашем следующем учебном курсе.

Счастливого вам программирования!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP.NET и основатель веб- [4GuysFromRolla.com](http://www.4guysfromrolla.com), работает с веб-технологиями Microsoft с 1998 года. Скотт — независимый консультант, преподаватель и автор. Его последняя книга — [ *Sams Teach ASP.NET 2.0 in 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ним можно связаться по адресу [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти в [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Особая благодарность

В этой серии руководств пособий рецензировалась многими компетентными редакторами. Основной рецензент этого учебного был (Dan Jagers). Хотите поработать с моих последующих статей для MSDN? Если Да, напишите мне [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](using-templatefields-in-the-gridview-control-vb.md)
> [Вперед](using-the-formview-s-templates-vb.md)
