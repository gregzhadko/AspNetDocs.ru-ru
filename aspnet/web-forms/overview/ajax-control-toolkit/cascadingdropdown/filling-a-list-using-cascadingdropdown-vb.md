---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Заполнение списка с помощью CascadingDropDown (VB) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 663dfc76dc3d07dbe9ddca002dc07cb3f9acdb1c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419344"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a>Заполнение списка с помощью CascadingDropDown (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList. (К примеру, один список содержит список штатов США, и следующий список заполняется крупнейших городов в этом состоянии.) Первая трудность заключается для решения — фактически заполнение раскрывающегося списка, с помощью этого элемента управления.


## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList. (К примеру, один список содержит список штатов США, и следующий список заполняется крупнейших городов в этом состоянии.) Первая трудность заключается для решения — фактически заполнение раскрывающегося списка, с помощью этого элемента управления.

## <a name="steps"></a>Шаги

Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в `<form>` элемента):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

Затем необходим элемент управления DropDownList:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

Для этого списка расширитель CascadingDropDown добавляется. Он отправит асинхронный запрос к веб-службу, которая будет возвращать список записей для отображения в списке. Чтобы это работало должны быть заданы следующие атрибуты CascadingDropDown:

- `ServicePath`: URL-адрес веб-службы, предоставляя элементов списка
- `ServiceMethod`: Веб-метода доставки элементов списка
- `TargetControlID`: Идентификатор списка, раскрывающегося списка
- `Category`: Сведения о категории, которая отправляется при вызове метода веб-
- `PromptText`: Текст, отображаемый при асинхронной загрузкой данных с сервера

Далее приведена разметка для `CascadingDropDown` элемент. Единственное различие между C# и VB — имя связанного веб-службы:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

Код JavaScript, поступающие от `CascadingDropDown` расширения вызывает метод веб-службы со следующей сигнатурой:

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

Это важный аспект, метод должен возвращать массив объектов типа `CascadingDropDownNameValue` (определяется по ASP.NET AJAX Control Toolkit). В `CascadingDropDownNameValue` конструктор, первый текстовый элемент списка, а затем его значение должно быть указано, так же, как `<option value="VALUE">NAME</option>` в HTML. Вот некоторые примеры данных:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

Загрузку страницы в браузере будет активировать списка, чтобы заполнить трех поставщиков.


[![TСписок он заполняется автоматически](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

Список заполняется автоматически ([Просмотр полноразмерного изображения](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-auto-postback-with-cascadingdropdown-cs.md)
> [Вперед](using-cascadingdropdown-with-a-database-vb.md)
