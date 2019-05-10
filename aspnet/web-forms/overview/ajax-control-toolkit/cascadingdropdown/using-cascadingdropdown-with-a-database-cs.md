---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: Использование CascadingDropDown с базой данных (C#) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 706a099042a298f8870f36cb653f1e5d5d156f2a
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125164"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a>Использование CascadingDropDown с базой данных (C#)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList. В порядке, чтобы это работало должны создаваться специальных веб-службы.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList. (К примеру, один список содержит список штатов США, и следующий список заполняется крупнейших городов в этом состоянии.) В порядке, чтобы это работало должны создаваться специальных веб-службы.

## <a name="steps"></a>Шаги

Во-первых источником данных является обязательным. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. Базы данных является необязательной частью установки Visual Studio (включая экспресс-выпуск), а также доступна для загрузки в разделе [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). Базы данных AdventureWorks является частью образцы SQL Server 2005 и образцов баз данных (загрузить в [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базы данных является использование Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединения `AdventureWorks.mdf` файл базы данных.

В этом примере мы предполагаем, что экземпляр SQL Server 2005 Express Edition называется `SQLEXPRESS` и находится на одном компьютере с веб-сервера; это также настройки по умолчанию. Если настройки отличаются, вам нужно адаптировать сведения о соединении для базы данных.

Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в &lt; `form` &gt; элемента):

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

На следующем шаге необходимы два элемента управления DropDownList. В этом примере мы используем поставщику и контактной информации из AdventureWorks, таким образом мы создадим один список доступных поставщиков и доступных контактов:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

Затем необходимо добавить два расширителей CascadingDropDown на страницу. Одно заполняет первый список (поставщики), а другой заполняет второй список (контакты). Необходимо задать следующие атрибуты:

- `ServicePath`: URL-адрес веб-службы, предоставляя элементов списка
- `ServiceMethod`: Веб-метода доставки элементов списка
- `TargetControlID`: Идентификатор списка, раскрывающегося списка
- `Category`: Сведения о категории, которая отправляется при вызове метода веб-
- `PromptText`: Текст, отображаемый при асинхронной загрузкой данных с сервера
- `ParentControlID`: (необязательно) родительского раскрывающемся списке, что загрузка триггеры текущего списка

В зависимости от используемого языка программирования изменяет имя веб-службы в вопросе, но все остальные значения атрибута совпадают. Ниже приведен элемент CascadingDropDown для первого раскрывающегося списка.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

Нужно задать управляющих элементов-расширителей для второй список `ParentControlID` таким образом, выберите соответствующую запись в триггерах списка поставщиков загрузке связанных элементов в списке контактов.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

Фактическая работа осуществляется в веб-службы, который настраивается следующим образом. Обратите внимание, что `[ScriptService]` используется атрибут, в противном случае AJAX для ASP.NET не удается создать прокси JavaScript для доступа к веб-методы из кода клиентского сценария.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

Подпись веб-методов, вызванных CascadingDropDown выглядит следующим образом:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

Поэтому возвращаемое значение должно быть массивом типа `CascadingDropDownNameValue` которого определяется набор элементов управления. `GetVendors()` Метод довольно прост в реализации: Код подключается к базе данных AdventureWorks и запрашивает поставщиков первые 25. Первый параметр в `CascadingDropDownNameValue` конструктор будет ее величина заголовок элемента списка, второй (значение атрибута в формате HTML &lt; `option` &gt; элемент). Ниже приведен код:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

Получение связанных контактов для поставщика (имя метода: `GetContactsForVendor()`) немного сложнее. Во-первых необходимо определить поставщика, который был выбран в первом раскрывающемся списке. Набор средств управления определяет вспомогательный метод для выполнения этой задачи: `ParseKnownCategoryValuesString()` Возвращает `StringDictionary` элемент, содержащий данные раскрывающегося списка:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

По соображениям безопасности необходимо сначала проверить эти данные. Таким образом, если имеется запись поставщика (поскольку `Category` первого элемента CascadingDropDown свойству `"Vendor"`), можно извлечь идентификатор выбранного поставщика:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

Остальная часть метода — довольно очевидно, затем. Идентификатор поставщика используется в качестве параметра для SQL-запрос, который извлекает все связанные контакты для этого поставщика. Опять же, метод возвращает массив объектов типа `CascadingDropDownNameValue`.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

Загрузки страницы ASP.NET, и через некоторое время короткий список поставщиков заполняется 25 записей. Выберите одну запись и обратите внимание на то, каким образом второго раскрывающегося списка заполняется данными.

[![Первый список заполняется автоматически](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

Первый список заполняется автоматически ([Просмотр полноразмерного изображения](using-cascadingdropdown-with-a-database-cs/_static/image3.png))

[![Второй список заполняется согласно выбору, в первом списке](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

Второй список заполняется согласно выбору, в первом списке ([Просмотр полноразмерного изображения](using-cascadingdropdown-with-a-database-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](filling-a-list-using-cascadingdropdown-cs.md)
> [Вперед](presetting-list-entries-with-cascadingdropdown-cs.md)
