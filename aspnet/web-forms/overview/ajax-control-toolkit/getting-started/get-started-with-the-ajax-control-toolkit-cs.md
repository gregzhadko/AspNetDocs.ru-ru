---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Начало работы с ajax управления Toolkit (C) Документы Майкрософт
author: rick-anderson
description: Узнайте все, что вам нужно знать, чтобы начать работу с помощью ajax Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543591"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>Начало работы с набором элементов управления AJAX (C#)

[корпорацией Майкрософт](https://github.com/microsoft)

> Узнайте все, что вам нужно знать, чтобы начать работу с помощью ajax Control Toolkit.

Инструмент ajax Control Toolkit содержит более 30 бесплатных элементов управления, которые можно использовать в ASP.NET приложениях. В этом учебнике вы узнаете, как загрузить набор инструментов управления AJAX и добавить набор инструментов в набор инструментов в набор инструментов в набор инструментов Visual Studio/Visual Web Developer Express.

## <a name="downloading-the-ajax-control-toolkit"></a>Загрузка инструментария управления AJAX

[AJAX Control Toolkit](http://devexpress.com/act) — это проект с открытым исходным кодом, разработанный членами ASP.NET сообщества и командой ASP.NET. 

[![Загрузка инструментария управления AJAX](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**Рисунок 01**: Загрузка ajax Инструмент управления[(Нажмите, чтобы посмотреть полноразмерное изображение](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))

После загрузки файла необходимо разблокировать файл. Нажмите правой кнопкой мыши, выберите Свойства и нажмите кнопку **«Разблокировать»** (см. рисунок 2).

[![Разблокирование файла AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**Рисунок 02**: Разблокировка AJAX Контроль инструмент инструментальный файл[»(Нажмите, чтобы посмотреть полноразмерное изображение](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))

После разблокировки файла можно распаковать файл: нажмите на файл вправо и выберите опцию **«Выдвилость все** меню». Теперь мы готовы добавить набор инструментов в набор инструментов Visual Studio/Visual Web Developer.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Добавление инструментария управления AJAX в набор инструментов для инструментов

Самый простой способ использовать набор инструментов управления AJAX — добавить набор инструментов в набор инструментов Visual Studio/Visual Web Developer (см. рисунок 3). Таким образом, вы можете просто перетащить элемент управления набором инструментов на страницу, когда вы хотите его использовать.

[![Набор инструментов управления AJAX появляется в наборе инструментов](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**Рисунок 03**: Ajax Control Toolkit появляется в наборе инструментов[(Нажмите, чтобы просмотреть полноразмерное изображение)](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)

Во-первых, необходимо добавить вкладку AJAX Control Toolkit в набор инструментов. Выполните следующие действия.

1. Создайте новый веб-сайт ASP.NET, выбрав вариант меню Файл, Новый веб-сайт. Дважды щелкните по умолчанию.aspx в окне Solution Explorer, чтобы открыть файл в редакторе.
2. Нажмите правой кнопкой кнопку Toolbox под общей вкладкой и выберите вариант меню **Добавить вкладку** (см. Рисунок 4).
3. Введите новую вкладку под названием AJAX Control Toolkit.

[![Добавление новой вкладки](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**Рисунок 04**: Добавление новой вкладки[(Нажмите, чтобы просмотреть полноразмерное изображение)](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)

Далее необходимо добавить элементы управления AJAX Toolkit в новую вкладку.

- Нажмите правой кнопкой мыши под вкладкой AJAX Control Toolkit и выберите вариант меню **Выберите элементы (см. рисунок 5).**
- Просмотрите место, где вы расстегнули инструмент управления AJAX и выберите сборку AjaxControlToolkit.dll.

[![Выберите элементы для добавления в набор инструментов](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**Рисунок 05**: Выберите элементы для добавления в набор инструментов[(Нажмите, чтобы просмотреть полноразмерное изображение)](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)

После завершения этих шагов все элементы управления набором инструментов будут отображаться в вашем наборе инструментов.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Обновление до новой версии инструментария

Если вы использовали старый выпуск Toolkit и теперь должны перейти к более поздней версии вот рекомендуемые шаги:

- Binaries - Удалите старую версию сборки AjaxControlToolkit.dll из папки Bin.
- Элементы Toolbox - Удалите вкладку AJAX Control Toolkit и выполните вышеуказанные шаги, чтобы воссоздать вкладку с новой версией сборки AjaxControlToolkit.dll.

> [!div class="step-by-step"]
> [Вперед](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
