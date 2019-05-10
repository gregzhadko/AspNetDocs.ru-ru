---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: Обработка операций обратной передачи из элемента управления всплывающего окна с помощью UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Расширитель PopupControl в AJAX Control Toolkit предлагает простой способ активации всплывающего окна при активации любого другого элемента управления. Особое внимание не надо...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f7d35035e70c04a1a14213e79bb140c5476bf60
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115289"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a>Обработка операций обратной передачи из элемента управления Popup с помощью элемента управления UpdatePanel (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)

> Расширитель PopupControl в AJAX Control Toolkit предлагает простой способ активации всплывающего окна при активации любого другого элемента управления. Особое внимание приходится принимать при обратной передаче в таких всплывающего окна.

## <a name="overview"></a>Обзор

Расширитель PopupControl в AJAX Control Toolkit предлагает простой способ активации всплывающего окна при активации любого другого элемента управления. Особое внимание приходится принимать при обратной передаче в таких всплывающего окна.

## <a name="steps"></a>Шаги

При использовании `PopupControl` при обратной передаче, `UpdatePanel` можно предотвратить обновление страницы, из-за обратной передачи. Следующая разметка определяет несколько важных элементов:

- Объект `ScriptManager` управления, чтобы обеспечить работу ASP.NET AJAX Control Toolkit
- Два `TextBox` элементов управления, которые будут активировать всплывающее окно
- Объект `Panel` элемент управления, который будет использоваться в качестве всплывающего окна
- На панели `Calendar` управления, встроенный в `UpdatePanel` элемента управления
- Два `PopupControlExtender` элементов управления, назначить панель текстовые поля

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

Обратите внимание, что `OnSelectionChanged` атрибут `Calendar` элемента управления задано значение. Поэтому когда пользователь выбирает дату в календаре, происходит обратная передача и серверного метода `c1_SelectionChanged()` выполняется. В этом методе необходимо извлечь текущую дату и записана в текстовом поле.

Синтаксис, выглядит следующим образом: Во-первых, прокси-сервер для объекта `PopupControlExtender` на странице должен быть создан. ASP.NET AJAX Control Toolkit предлагает `GetProxyForCurrentPopup()` метод. Этот метод возвращает объект поддерживает `Commit()` метод, который отправляет значение элемента управления, являющегося всплывающее окно (не элемента управления, являющегося вызова метода!). В следующем коде представлен выбранную дату в качестве аргумента для `Commit()` методом, выполняемым кодом для обратной записи выбранную дату в текстовом поле:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

Теперь всякий раз при нажатии на дату, отображается выбранную дату в соответствующем текстовом поле, создание элемента выбора даты, в настоящее время находятся на многих веб-сайтах.

[![Календарь появляется, когда пользователь нажимает кнопку в текстовое поле](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)

Календарь появляется, когда пользователь нажимает кнопку в текстовое поле ([Просмотр полноразмерного изображения](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))

[![Щелкните дату помещает его в текстовое поле](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)

Щелкните дату помещает его в текстовое поле ([Просмотр полноразмерного изображения](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](using-multiple-popup-controls-vb.md)
> [Вперед](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)
