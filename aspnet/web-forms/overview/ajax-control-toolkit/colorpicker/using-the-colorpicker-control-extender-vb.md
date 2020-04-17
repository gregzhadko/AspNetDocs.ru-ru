---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: Использование расширителя управления ColorPicker (VB) Документы Майкрософт
author: rick-anderson
description: ColorPicker — это ASP.NET удлинитель AJAX, который обеспечивает функциональность выбора цвета со стороны клиента с помощью uI в элементе управления всплывающими окном. Его можно прикрепить к любому ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542850"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>Использование расширителя управления ColorPicker (VB)

[корпорацией Майкрософт](https://github.com/microsoft)

> ColorPicker — это ASP.NET удлинитель AJAX, который обеспечивает функциональность выбора цвета со стороны клиента с помощью uI в элементе управления всплывающими окном. Он может быть прикреплен к любому ASP.NET управления TextBox. Это.

Цель этого учебника состоит в том, чтобы объяснить, как вы можете использовать AJAX Управления Toolkit ColorPicker управления удлинитель. Удлинитель управления ColorPicker отображает всплывающий диалог, который позволяет выбрать цвет. ColorPicker полезен всякий раз, когда вы хотите предоставить интуитивно понятный пользовательский интерфейс для пользователя, чтобы выбрать цвет.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>Расширение управления TextBox с помощью расширителя управления ColorPicker

Представьте себе, например, что вы хотите создать веб-сайт, который позволяет посетителям создавать индивидуальные визитные карточки. Посетители могут ввести текст для визитной карточки и выбрать цвет. Страница ASP.NET в листинге 1 содержит два элемента управления TextBox под названием txtCardText и txtCardColor. При отправке формы отображаются выбранные значения (см. рисунок 1).

[![Простая форма для создания бизнес-карты](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**Рисунок 01**: Простая форма для создания визитной карточки ([Нажмите, чтобы просмотреть полноразмерное изображение](using-the-colorpicker-control-extender-vb/_static/image2.png))

**Листинг 1 - CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

Форма в листинге 1 работает, но она не обеспечивает большой пользовательский опыт. Пользователь должен ввести цвет в текстовый ящик. Если пользователь хочет специализированный цвет - например, только правильный оттенок гороха зеленый - то пользователь должен выяснить HTML цветовой код без какой-либо помощи.

Вы можете использовать удлинитель управления ColorPicker для создания лучшего пользовательского интерфейса. ColorPicker отображает цветовой диалог при перемещении фокуса на элемент управления TextBox (см. рисунок 2).

[![Расширитель управления ColorPicker](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**Рисунок 02**: Расширитель управления ColorPicker ([Нажмите, чтобы просмотреть полноразмерное изображение](using-the-colorpicker-control-extender-vb/_static/image4.png))

Вам нужно выполнить два шага, чтобы использовать удлинитель управления ColorPicker с формой в листинге 1:

1. Добавление элемента управления ScriptManager на страницу
2. Добавьте на страницу расширитель управления ColorPicker

Прежде чем использовать ColorPicker, вы должны добавить scriptManager на вашу страницу. Хорошее место, чтобы добавить ScriptManager находится &lt;прямо&gt; под открытием сервера стороне формы тега. Вы можете перетащить ScriptManager на страницу из инструментария (менеджер scriptManager находится под вкладкой AJAX Extensions). Кроме того, можно ввести следующий тег в Source View под тегом формы сервера:

&lt;asp:ScriptManager ID "ScriptManager1" runat'"server" /&gt;

Самый простой способ добавить удлинитель управления ColorPicker на страницу — в Design View. Если вы нависнете над мышью над txtCardColor TextBox, появляется опция «умного» — это позволяет добавить расширитель (см. рисунок 3). Если вы выберете эту опцию, появится мастер-расширитель (см. рисунок 4).

[![Добавление расширителя](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**Рисунок 03**: Добавление расширителя[(Нажмите, чтобы просмотреть полноразмерное изображение)](using-the-colorpicker-control-extender-vb/_static/image6.png)

[![Выбор расширителя управления с мастером расширения](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**Рисунок 04**: Выбор удлинителя управления с мастером расширения ([Нажмите, чтобы просмотреть полноразмерное изображение](using-the-colorpicker-control-extender-vb/_static/image8.png))

Вы можете выбрать удлинитель ColorPicker, чтобы расширить TxtCardColor TextBox с удлинителем ColorPicker. Нажмите кнопку ОК, чтобы закрыть диалоговое окно.

После внесения этих изменений источник страницы выглядит как листинг 2.

**Список 2 - CreateCard.aspx (с ColorPicker)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

Обратите внимание, что страница теперь содержит управление ColorPickerExtender, которое появляется непосредственно под контролем txtCardColor TextBox. Управление ColorPickerExtender расширяет управление txtCardColor так, что он отображает диалог сборщика цветов.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Использование кнопки для запуска Color Picker Dialog

Удлинитель ColorPicker поддерживает следующие свойства:

- PopupButtonId - Идентификатор кнопки на странице, которая вызывает диалог сборщика цветов.
- PopupPosition - Положение, относительно элемента управления мишеней, диалога сборщика цветов. Возможные значения: Абсолют, Центр, БоттомЛевое, ДноПраво, TopLeft, TopRight, Right, Вправо и Левое (по умолчанию является BottomLeft).
- SampleControlId - Идентификатор элемента управления, отображаемого выбранного цвета.
- ВыбранныйЦвет - Первоначальный цвет, выбранный ColorPicker.

Эти свойства можно использовать для настройки того, как отображается диалог сборщика цветов и как отображается выбранный цвет. Страница в листинге 3 иллюстрирует, как можно использовать некоторые из этих свойств.

**Листинг 3 - CreateCardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

Страница в листинге 3 включает кнопку «Выбор цвета» (см. рисунок 5). При нажатии на эту кнопку диалог сборщика цветов отображается выше TextBox. Если вы выберете цвет из диалога, то выбранный цвет отображается в виде фонового цвета управления этикетки lblSample.

Свойство ColorPicker PopupButtonID используется для ассоциируется с кнопкой Pick Color с расширителем ColorPicker. При предоставлении значения для свойства PopupButtonID диалог сборщика цветов больше не отображается, когда целевой элемент управления фокусируется. Вы должны нажать на кнопку, чтобы отобразить диалог.

Свойство SampleControlID используется для ассоциации элемента управления, отображаемого выбранного цвета, с ColorPicker. ColorPicker изменяет цвет фона этого элемента управления на выбранный в настоящее время цвет.

[![Отображение диалога сборщика цветов с помощью кнопки](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**Рисунок 05**: Отображение диалога сборщика цветов с помощью кнопки ([Нажмите, чтобы просмотреть полноразмерное изображение](using-the-colorpicker-control-extender-vb/_static/image10.png))

## <a name="summary"></a>Сводка

В этом учебнике вы узнали, как использовать удлинитель управления ColorPicker для отображения всплывающих цветсборщик диалог. Во-первых, мы рассмотрели, как можно отображать диалог, когда фокус перемещается в управление TextBox. Затем вы узнали, как создать кнопку, которая отображает диалог сборщика цветов при нажатии кнопки.

> [!div class="step-by-step"]
> [Назад](using-the-colorpicker-control-extender-cs.md)
