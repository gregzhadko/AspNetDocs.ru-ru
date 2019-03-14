---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Настройка Z-индекса DropShadow (C#) | Документация Майкрософт
author: wenz
description: Элемент управления DropShadow в AJAX Control Toolkit расширяет панель с эффектом отбрасывания тени. Тем не менее Эта теневая иногда конфликтует с другими элементами управления, для пап...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 5cee2acfac74c0790a7ad82bbfb503a8a16f6b47
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024611"
---
<a name="adjusting-the-z-index-of-a-dropshadow-c"></a>Настройка Z-индекса DropShadow (C#)
====================
по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> Элемент управления DropShadow в AJAX Control Toolkit расширяет панель с эффектом отбрасывания тени. Тем не менее Эта теневая иногда конфликтует с другими элементами управления, например элемент управления ASP.NET Menu. Когда запись меню появляется его фоне тени.


## <a name="overview"></a>Обзор

Элемент управления DropShadow в AJAX Control Toolkit расширяет панель с эффектом отбрасывания тени. Тем не менее Эта теневая иногда конфликтует с другими элементами управления, например элемент управления ASP.NET Menu. Когда запись меню появляется его фоне тени.

## <a name="steps"></a>Шаги

Код начинается с элемента управления, содержащий достаточного объема текста, чтобы панель содержит достаточного объема текста для эффекта, который должен отображаться:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

Другую панель помещается непосредственно перед `panelShadow` панели. Она включает меню в горизонтальном направлении, чтобы пункты меню отображаются над (вернее: в разделе) `dropShadow` панель):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

Затем `DropShadowExtender` добавляется расширение `panelShadow` панели с помощью эффекта тени:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

Наконец, AJAX ASP.NET `ScriptManager` управления включает набор средств управления для работы:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

При выполнении этого скрипта, пункты меню отображаются под панели. Тем не менее меню используется класс CSS `panel` где вам просто нужно определить два действия, чтобы сделать элементы отображаются перед элементами на другие панели:

- Относительное расположение
- Положительное значение z индекса

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

Затем `DropShadowExtender` управления больше не конфликтуют с меню элемента управления.


[![Ранее: Элемент меню не отображается](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

До: Элемент меню не отображается ([Просмотр полноразмерного изображения](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))


[![После: Запись меню](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

После: Запись меню ([Просмотр полноразмерного изображения](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Вперед](manipulating-dropshadow-properties-from-client-code-cs.md)
