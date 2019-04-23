---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: Использование обратных передач с помощью элемента управления ReorderList (VB) | Документация Майкрософт
author: wenz
description: Элемент управления ReorderList в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Каждый раз, когда отображается список po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 22c7eecb841ff67196d21e6efeeda63a3456c5cb
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59409087"
---
# <a name="using-postbacks-with-reorderlist-vb"></a>Использование обратных передач с помощью элемента управления ReorderList (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> Элемент управления ReorderList в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Всякий раз, когда отображается список обратную передачу должны сообщить серверу изменения.


## <a name="overview"></a>Обзор

`ReorderList` Элемент управления в AJAX Control Toolkit предоставляет список, можно ли изменять расположение пользователем с помощью операции перетаскивания. Всякий раз, когда отображается список обратную передачу должны сообщить серверу изменения.

## <a name="steps"></a>Шаги

Существует несколько источников данных для `ReorderList` элемента управления. Одним является использование `XmlDataSource` управления:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

Чтобы привязать этот XML-код для `ReorderList` должно иметь значение управления с обратной передачей, следующие атрибуты:

- `DataSourceID`: Идентификатор источника данных
- `SortOrderField`: Свойство, чтобы выполнить сортировку по
- `AllowReorder`: Следует ли разрешить пользователю изменять порядок элементов списка
- `PostBackOnReorder`: Нужно ли создавать обратной передачи, каждый раз, когда изменяется список

Ниже приведен соответствующий разметки для элемента управления.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

В рамках `ReorderList` может привязать элемент управления, определенных данных из источника данных с помощью `Eval()` метод:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

В случайном положении на странице метку хранения информации, когда произошло последнее изменение порядка:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

Эта метка заполняется с текстом в коде на сервере обработки обратной передачи:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

Наконец, для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления должны быть размещены на странице:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


[![Каждый переупорядочения инициирует обратную передачу](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

Каждый переупорядочения инициирует обратную передачу ([Просмотр полноразмерного изображения](using-postbacks-with-reorderlist-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](drag-and-drop-via-reorderlist-cs.md)
> [Вперед](drag-and-drop-via-reorderlist-vb.md)
