---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: Выполнение нескольких анимаций друг за другом (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Он позволяет выполнять severa...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: 60fb7dacfe59eaafef71fcc9cde61b7840624343
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030971"
---
<a name="executing-several-animations-after-each-other-c"></a>Выполнение нескольких анимаций друг за другом (C#)
====================
по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Он одновременное выполнение нескольких анимаций один за другим.


Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Он одновременное выполнение нескольких анимаций один за другим.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

Анимация будет применяться к панели текста, который выглядит следующим образом:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

В рамках `<Animations>` узла, используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Как правило `<OnLoad>` принимает только одна анимация. Платформа анимации позволяет объединить несколько анимаций в один с помощью `<Sequence>` элемент. Все анимации в `<Sequence>` , выполняются за другим. Вот возможные разметку для `AnimationExtender` элемента управления, сначала внесение панели «ширина» и затем уменьшая высоту:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

При выполнении этого сценария, панели первой получает шире и затем меньшего размера.


[![Сначала увеличивается ширина](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)

Сначала ширина увеличивается ([Просмотр полноразмерного изображения](executing-several-animations-after-each-other-cs/_static/image3.png))


[![Затем уменьшается на высоту](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)

Затем уменьшается на высоту ([Просмотр полноразмерного изображения](executing-several-animations-after-each-other-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Назад](executing-several-animations-at-the-same-time-cs.md)
> [Вперед](animation-depending-on-a-condition-cs.md)
