---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: С помощью автоматической обратной передачи с помощью с CascadingDropDown (C#) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 7c84951691935d9976f961f65f96fa70633ecbce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061331"
---
<a name="using-auto-postback-with-cascadingdropdown-c"></a>Использование автоматической обратной передачи с помощью CascadingDropDown (C#)
====================
по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)

> Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList. Тем не менее при использовании элемента управления CascadingDropDown, ASP. Элемент управления DropDownList NET AutoPostBack функция работает, поскольку асинхронно загрузки данных в списке создает (ненужные) обратную передачу, сам. Этот эффект можно избежать с помощью кода JavaScript.


## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в AJAX Control Toolkit расширяет элемент управления DropDownList, что изменения в одной загрузке DropDownList соответствующих значений в другой DropDownList. (К примеру, один список содержит список штатов США, и следующий список заполняется крупнейших городов в этом состоянии.) Тем не менее при использовании элемента управления CascadingDropDown, ASP. Элемент управления DropDownList NET AutoPostBack функция работает, поскольку асинхронно загрузки данных в списке создает (ненужные) обратную передачу, сам. Этот эффект можно избежать с помощью кода JavaScript.

## <a name="steps"></a>Шаги

Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в &lt; `form` &gt; элемента):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

Затем необходим элемент управления DropDownList:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

Для этого списка добавляется расширитель CascadingDropDown, предоставляя данные веб-службы URL-адрес и метод:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

Расширитель CascadingDropDown затем производит асинхронный вызов веб-службы со следующей сигнатурой метода:

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

Метод возвращает массив объектов типа CascadingDropDown значение. Конструктор типа сначала ожидает заголовок элемента списка, а затем значение (HTML `value` атрибут).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

Загрузку страницы в браузере будет заполнить раскрывающийся список с тремя поставщиками второй выбраны заранее. Кроме того, ASP.NET определяет `__doPostBack()` метод JavaScript. После загрузки страницы, этот вызов JavaScript добавляется к раскрывающемуся списку, но только при наличии элементов в нем. Если в списке нет элементов, набор элементов управления в процессе загрузки, поэтому в коде JavaScript используется время ожидания и предпринимает попытку через половины секунды.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

Таким образом, обратная передача выполняется только при наличии фактически элементы в списке, и пользователь выбирает запись.


[![Выбор элемента списка вызывает обратную передачу](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)

Выбор элемента списка вызывает обратную передачу ([Просмотр полноразмерного изображения](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](presetting-list-entries-with-cascadingdropdown-cs.md)
> [Вперед](filling-a-list-using-cascadingdropdown-vb.md)
