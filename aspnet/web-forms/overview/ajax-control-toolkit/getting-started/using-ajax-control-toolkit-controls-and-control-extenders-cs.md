---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: Использование ajax Управления инструментарий Управления и расширения управления (C) Документы Майкрософт
author: rick-anderson
description: Узнайте, как добавить элементы управления AJAX И удлинители на ASP.NET страницы.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543721"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Использование элементов управления из набора элементов AJAX и управляющих элементов-расширителей (C#)

[корпорацией Майкрософт](https://github.com/microsoft)

> Узнайте, как добавить элементы управления AJAX И удлинители на ASP.NET страницы.

Инструмент ajax Control Toolkit содержит набор элементов управления и удлинителей управления. В этом кратком учебнике вы узнаете, как добавить как элементы управления, так и удлинители управления на страницу ASP.NET.

> [!NOTE] 
> 
> Для получения инструкций по установке ajax Control Toolkit и добавлению инструментария управления AJAX в набор инструментов Visual Studio/Visual Web Developer смотрите учебник [Get Started с помощью инструментария управления AJAX.](get-started-with-the-ajax-control-toolkit-cs.md)

## <a name="using-ajax-control-toolkit-controls"></a>Использование элементов управления AJAX Toolkit Control

Управление инструментарием AJAX Control Toolkit работает так же, как обычное управление ASP.NET. Вы можете перетащить элемент управления из ящика инструментов на ASP.NET страницу. Можно добавить элемент управления на страницу в представлении Design или Source view.

При использовании элементов управления из набора ajax Control Toolkit существует одно специальное требование. Страница должна содержать элемент управления ScriptManager. Контроль ScriptManager отвечает за включение всех необходимых JavaScript, требуемых контролем AJAX Control Toolkit.

Например, вкладка AJAX Control Toolkit включает элемент управления с названием «Управление редактором». Этот элемент управления отображает богатый HTML-редактор. Выполните следующие действия, чтобы добавить элемент управления редактора на страницу:

1. Создайте новую страницу ASP.NET под названием ShowEditor.aspx
2. Выберите элемент управления ScriptManager из-под вкладки AJAX Extensions в наборе инструментов и перетащите элемент управления на страницу.
3. Выберите элемент управления редактором из-под вкладки AJAX Control Toolkit в наборе инструментов и перетащите элемент управления на страницу (см. рисунок 1). Дизайнер должен выглядеть как рисунок 2.
4. Запустите веб-сайт, выбрав вариант меню **Debug, начать отладку** или нажатие клавиши F5.
5. Вы должны увидеть страницу на рисунке 3.

[![Выбор элемента управления HTML-редактором](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**Рисунок 01**: Выбор управления редактором HTML[(Нажмите, чтобы просмотреть полноразмерное изображение)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)

[![Дизайнер визуальной студии с менеджером-сценарием и управлением edit](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**Рисунок 02**: Visual Studio Designer с ScriptManager и управлением edit[(Нажмите, чтобы просмотреть полноразмерное изображение](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))

[![Страница DisplayEditor.aspx](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**Рисунок 03**: Страница DisplayEditor.aspx[(Нажмите, чтобы просмотреть полноразмерное изображение](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>Использование расширителей управления инструментами управления AJAX

Инструмент ajax Control Toolkit также содержит удлинители управления. Как следует из названия, расширитель управления расширяет функциональность существующего элемента управления. Например, расширитель управления Подтверждения Кнопки расширяет стандартный ASP.NET управления кнопкой. Расширитель изменяет поведение управления кнопкой так, чтобы кнопка отображала диалог подтверждения при нажатии на него.

Расширитель управления, как и элементуправления AJAX Control Toolkit, требует управления ScriptManager. Прежде чем начать использовать удлинители управления на странице, необходимо добавить элемент управления ScriptManager на страницу.

Выполните следующие действия, чтобы использовать расширитель управления Подтверждения Кнопки:

1. Создайте новую страницу ASP.NET под названием ShowConfirmButton.aspx
2. Добавьте элемент управления ScriptManager на страницу, перетащив элемент управления на страницу из-под вкладки AJAX Extensions.
3. Добавьте стандартный элемент управления кнопкой на страницу, перетащив кнопку из-под вкладки Standard в панели инструментов на поверхность конструктора.
4. Нажмите на опцию задачи **Add Extender** (см. рисунок 4).
5. В диалоге Выберите Расширитель выберите ConfirmButtonExtender (см. рисунок 5) и нажмите кнопку OK.
6. Выберите элемент управления кнопками в конструкторе\_и расширьте расширители, кнопку1 ConfirmButtonExtender узла в окне свойства (см. Рисунок 6). Присвоить значение *Действительно?* к свойству ConfirmText.
7. Выполнить страницу, выбрав вариант меню **Debug, начать отладку** или нажмите клавишу F5.

[![Опция задачи Add Extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**Рисунок 04**: Опция задачи Добавить Extender[(Нажмите, чтобы просмотреть полноразмерное изображение)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)

[![Выбор расширителя управления Подтверждения Кнопки](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**Рисунок 05**: Выбор расширителя управления Подтверждения Кнопки[(Нажмите, чтобы просмотреть полноразмерное изображение)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)

[![Установка свойства подтверждения кнопки](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**Рисунок 06**: Установка свойства Подтверждения Кнопки[(Нажмите, чтобы просмотреть полноразмерное изображение)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)

Когда страница открывается, вы должны увидеть кнопку. При нажатии кнопки вы получаете диалог подтверждения на рисунке 7.

[![Отображение диалога подтверждения](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**Рисунок 07**: Отображение диалога подтверждения[(Нажмите, чтобы просмотреть полноразмерное изображение)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)

Обратите внимание, что обычно вы не перетаскиваете удлинитель управления на страницу. Вместо этого используется опция задачи **Add Extender** для добавления расширителя к элементу управления, который вы уже добавили на страницу. Кроме того, обратите внимание на то, что вы устанавливаете свойства расширителя управления, открывая лист свойства для расширения элемента управления.

Один ASP.NET управления может быть расширен несколькими удлинителями управления. В листе свойства для расширения элемента управления будут указаны все расширители управления, связанные с управлением.

> [!div class="step-by-step"]
> [Назад](get-started-with-the-ajax-control-toolkit-cs.md)
> [Вперед](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
