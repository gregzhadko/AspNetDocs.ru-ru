---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: Основной/подробности Фильтрация с помощью элемента управления DropDownList (C#) | Документация Майкрософт
author: rick-anderson
description: В этом руководстве будет показано, как отображение основных записей в элемент управления DropDownList и сведений выбранного элемента списка в элементе управления GridView.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 8edc18968625036964c0120b83f8ebb149dbf87a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393435"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-c"></a>Фильтрация "Основной/подробности" с помощью элемента управления DropDownList (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачайте пример приложения](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe) или [скачать PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> В этом руководстве будет показано, как отображение основных записей в элемент управления DropDownList и сведений выбранного элемента списка в элементе управления GridView.


## <a name="introduction"></a>Вступление

Распространенным типом отчета является *отчет "основной/подробности"*, в который начинается с демонстрации определенного набора «основных» записей. Пользователь может затем перейти к одной из основных записей, таким образом просматривая основной записи «подробности». «Основной/подробности» сообщает являются идеальным выбором для визуализации отношений «один ко многим», например отчет все категории и позволяющего пользователю выбрать определенную категорию и отобразить соответствующие продукты. Кроме того отчеты «основной/подробности» полезны для отображения подробных сведений из чрезвычайно «широких» таблиц (таблиц со множеством столбцов). Например, уровень «основной» отчета «основной/подробности» могут отображаться только продукта имя и цену за единицу продуктов в базе данных, и подробное изучение конкретного продукта будет отображать дополнительные поля продукта (категория, поставщик, количество в единицах измерения, и т. д).

Существует много способов, с помощью которых можно реализовать отчета «основной/подробности». В этом и трех следующих руководствах мы рассмотрим различные отчеты «основной/подробности». В этом руководстве мы рассмотрим отображение основных записей в [управления DropDownList](https://msdn.microsoft.com/library/dtx91y0z.aspx) и сведений выбранного элемента списка в элементе управления GridView. В частности отчет «основной/подробности» этого руководства будут перечислены категории и сведения о продукте.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>Шаг 1. Отображение категорий в элементе управления DropDownList

Категории в элементе управления DropDownList, перечислит нашего отчета «основной/подробности» с продуктами выбранного элемента списка отображаются ниже на странице в элементе управления GridView. Первой задачей, то категорий, отображаемых в элементе управления DropDownList. Откройте `FilterByDropDownList.aspx` странице в `Filtering` папки, перетащите DropDownList с панели элементов в конструктор страницы и задать его `ID` свойства `Categories`. Затем щелкните ссылку выберите источник данных смарт-теге DropDownList. Откроется мастер настройки источника данных.


[![SУкажите источник данных DropDownList](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**Рис. 1**: Укажите источник данных DropDownList ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))


Добавить новый ObjectDataSource, именуемый `CategoriesDataSource` , вызывающий `CategoriesBLL` класса `GetCategories()` метод.


[![Aдд новый ObjectDataSource с именем CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**Рис. 2**: Добавить новый элемент управления ObjectDataSource с именем `CategoriesDataSource` ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))


[![CВыберите для использования класса CategoriesBLL](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**Рис. 3**: Выбор `CategoriesBLL` класс ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))


[![CНастройка ObjectDataSource на использование метода GetCategories()](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**Рис. 4**: Настройка ObjectDataSource для использования `GetCategories()` метод ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))


После настройки ObjectDataSource все равно небходимо указать поле источника данных, которые должны отображаться в DropDownList, а какие должно быть связано в качестве значения для элемента списка. У `CategoryName` как отображение и `CategoryID` как значение для каждого элемента списка.


[![Hсохранить элемент управления DropDownList отображает поле «Категория» и CategoryID использовать как значение](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**Рис. 5**: Иметь элемент управления DropDownList отображает `CategoryName` и использует `CategoryID` как значение ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))


На этом этапе у нас есть элемент управления DropDownList, заполненный записями из `Categories` (все действия выполняются приблизительно за шесть секунд). Рис. 6 показаны до сих при просмотре через браузер.


[![A Раскрывающийся список текущих категорий](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**Рис. 6**: Раскрывающийся список текущих категорий ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))


## <a name="step-2-adding-the-products-gridview"></a>Шаг 2. Добавление элемента GridView с продуктами

Последним шагом создания отчета «основной/подробности» является отображение списка продуктов, связанных с выбранной категорией. Для этого добавьте на страницу GridView и создайте новый ObjectDataSource, именуемый `productsDataSource`. У `productsDataSource` должен получать данные от `ProductsBLL` класса `GetProductsByCategoryID(categoryID)` метод.


[![SВыберите метод GetProductsByCategoryID(categoryID)](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**Рис. 7**: Выберите `GetProductsByCategoryID(categoryID)` метод ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))


После выбора этого метода мастер ObjectDataSource запрашивает значения для метода *`categoryID`* параметра. Чтобы использовать значение выбранного `categories` элемент DropDownList источника параметра установите для элемента управления, а для ControlID – `Categories`.


[![SET categoryID параметр со значением элемента управления DropDownList категории](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**Рис. 8**: Задайте *`categoryID`* параметр значению `Categories` DropDownList ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))


Отвлекитесь и просмотрите ход работы в браузере. При первом просмотре страницы, продукты, принадлежащие выбранной категории (Напитки) отображаются (как показано на рис. 9), но изменения в элемент управления DropDownList данные не обновляются. Это обусловлено тем, для обновления GridView необходимо осуществление обратной передачи. Для этого у нас есть два варианта (ни один из которых требует написания кода):

- **Задайте свойства AutoPostBack**[свойство AutoPostBack](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**значение true.** (Это можно сделать, выбрав вариант включить AutoPostBack в смарт-теге DropDownList.) Это приведет к запуску обратную передачу при выборе DropDownList элемент изменен пользователем. Таким образом когда пользователь выбирает новую категорию в элементе управления DropDownList произойдет обратная передача и GridView будет обновлен продуктами для новой выбранной категории. (Это подход, который я использовал в этом руководстве).
- **Добавьте кнопку веб-элемент управления рядом с DropDownList.** Задайте его `Text` свойство для обновления или что-то подобное. При таком подходе пользователь потребуется выбрать новую категорию и нажмите кнопку. Нажмите кнопку вызывает обратную передачу и обновление GridView отображены продукты выбранной категории.

На рис. 9 и 10 показана работа отчета «основной/подробности» в действии.


[![Wри первом просмотре страницы, отображаются продукты отображаются](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**Рис. 9**: При первом просмотре странице отображаются продукты отображаются ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))


[![SОтказ от нового продукта (Produce) автоматически вызывает обратную передачу, обновляется GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**Рис. 10**: Выбор нового продукта (Produce) автоматически вызывает обратную передачу, обновляется GridView ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))


## <a name="adding-a----choose-a-category----list-item"></a>Добавление элемента списка «--выберите категорию--»

При первом просмотре `FilterByDropDownList.aspx` странице категорий, по умолчанию, показывающие отображаются продукты в GridView выбран первый элемент списка DropDownList (Напитки). Вместо отображения продуктов первой категории, нам может потребоваться вместо этого элемент DropDownList выбран, — говорит нечто вроде: «--выберите категорию--».

Чтобы добавить новый элемент списка DropDownList, перейдите в окно свойств и щелкните эллипсы в `Items` свойство. Добавить новый элемент списка с `Text` «--выберите категорию--» и `Value` `-1`.


[![Aдд выберите категорию--элемента списка](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**Рис. 11**: Добавление выберите категорию--элемент списка ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))


Кроме того можно добавить элемент списка, добавив следующую разметку в элемент управления DropDownList:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

Кроме того, нам нужно установить элемент управления DropDownList `AppendDataBoundItems` значение True, так как при привязке категорий к DropDownList из ObjectDataSource они будут перезаписывать все элементы списка, добавленные вручную, если `AppendDataBoundItems` не установлено значение True.


![Установите для свойства AppendDataBoundItems значение true](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**Рис. 12**: Задайте `AppendDataBoundItems` присваивается значение True


После внесения этих изменений при первом просмотре страницы выбран параметр «--выберите категорию--» и продукты не отображаются.


[![On начальной странице нагрузки нет Товары показываются](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**Рис. 13**: На начальной странице продукты нет нагрузки отображаются ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))


Поскольку выбран элемент списка «--выберите категорию--» продукты не отображаются при, так как его значение равно `-1` и нет ни одного продукта в базе данных с помощью `CategoryID` из `-1`. Если это поведение необходимо, то дело сделано на этом этапе! Если, однако будет отображаться *все* категорий при выборе элемента списка «--выберите категорию--» вернитесь `ProductsBLL` и настройте `GetProductsByCategoryID(categoryID)` метод, чтобы он вызывал `GetProducts()` метод Если переданный в *`categoryID`* меньше нуля:

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

Используемый прием аналогичен приемом, использованным для отображения всех поставщиков в [декларативные параметры](../basic-reporting/declarative-parameters-cs.md) учебника, несмотря на то, что в этом примере мы используем значение `-1` для указания, что все записи должны быть извлечь в отличие от `null`. Это обусловлено *`categoryID`* параметр `GetProductsByCategoryID(categoryID)` метод ожидает в качестве целочисленное значение, переданное в, тогда как в этом руководстве декларативным параметрам передавался входной строковой параметр.

Рис. 14 показан снимок экрана `FilterByDropDownList.aspx` при выборе параметра «--выберите категорию--». Здесь по умолчанию отображаются все продукты, и пользователь может сузить отображаемые, выбрав определенную категорию.


[![ALl продуктов — теперь в списке по умолчанию](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**Рис. 14**: Все продукты, теперь в списке по умолчанию ([Просмотр полноразмерного изображения](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))


## <a name="summary"></a>Сводка

При отображении иерархически связанных данных часто полезно представлять данные с помощью отчетов «основной/подробности», из которых пользователь может начать изучение данных в верхней части иерархии и перейти к подробным сведениям. В этом руководстве было рассмотрено создание "основной/подробности" простой отчет, показывающий продукты выбранной категории. Это осуществлялось с помощью элемента управления DropDownList для списка категорий и GridView для продуктов, принадлежащих выбранной категории.

В [следующему руководству](master-detail-filtering-with-two-dropdownlists-cs.md) мы рассмотрим один шаг интерфейс DropDownList, с помощью двух элементов управления DropDownList.

Счастливого вам программирования!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP.NET и основатель веб- [4GuysFromRolla.com](http://www.4guysfromrolla.com), работает с веб-технологиями Microsoft с 1998 года. Скотт — независимый консультант, преподаватель и автор. Его последняя книга — [ *Sams Teach ASP.NET 2.0 in 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ним можно связаться по адресу [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти в [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Далее](master-detail-filtering-with-two-dropdownlists-cs.md)
