---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Обработка операций обратной передачи из элемента управления всплывающего окна без элемента управления UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Расширитель PopupControl в AJAX Control Toolkit предлагает простой способ активации всплывающего окна при активации любого другого элемента управления. При обратной передаче в единицах поиска...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: c0535ee78bf3ee5133d73749e8376f4b771f4d3c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115113"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a>Обработка операций обратной передачи из элемента управления Popup без использования элемента управления UpdatePanel (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)

> Расширитель PopupControl в AJAX Control Toolkit предлагает простой способ активации всплывающего окна при активации любого другого элемента управления. При обратной передаче такие панели и на странице имеется несколько панелей трудно определить, какая из панелей был выполнен щелчок.

## <a name="overview"></a>Обзор

Расширитель PopupControl в AJAX Control Toolkit предлагает простой способ активации всплывающего окна при активации любого другого элемента управления. При обратной передаче такие панели и на странице имеется несколько панелей трудно определить, какая из панелей был выполнен щелчок.

## <a name="steps"></a>Шаги

При использовании `PopupControl` при обратной передаче, но без `UpdatePanel` набор элементов управления на странице не предлагает способ определить, какой элемент клиент активировал всплывающее окно, которое в свою очередь вызвало обратной передачи. Тем не менее небольшую хитрость предоставляет обходной путь для этого сценария.

Во-первых, вот базовую настройку: два текстовых поля, оба способа активации же всплывающего окна календаря. Два `PopupControlExtenders` объединяйте текстовые поля и всплывающего окна.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

Основная идея заключается в том, чтобы добавить скрытого поля формы в &lt; `form` &gt; элемент, который содержит текстовое поле, которое запускается всплывающее окно:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

При загрузке страницы, кода JavaScript добавляет обработчик событий, чтобы оба поля: Каждый раз, когда пользователь нажимает на текстовое поле, его имя записывается в скрытое поле формы:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

В коде на стороне сервера необходимо считать значение скрытого поля. Поскольку скрытые поля формы просты для управления, утвержденный список способов проверки скрытые значения является обязательным. После определения правильного текстовое поле, в него записывается дату из календаря.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

[![Календарь появляется, когда пользователь нажимает кнопку в текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

Календарь появляется, когда пользователь нажимает кнопку в текстовое поле ([Просмотр полноразмерного изображения](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))

[![Щелкните дату помещает его в текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

Щелкните дату помещает его в текстовое поле ([Просмотр полноразмерного изображения](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
