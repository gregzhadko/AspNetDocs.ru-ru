---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: Анимация в зависимости от условия (VB) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Является ли анимация...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 78140f56184e88fb4dbe29f234aebd5732b69ad9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418876"
---
# <a name="animation-depending-on-a-condition-vb"></a>Анимация в зависимости от условия (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Запускается ли анимация или не может также зависеть условие в виде кода JavaScript.


## <a name="overview"></a>Обзор

Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Запускается ли анимация или не может также зависеть условие в виде кода JavaScript.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

Анимация будет применяться к панели текста, который выглядит следующим образом:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

В рамках `<Animations>` узла, используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Вместо одного из обычных анимаций `<Condition>` элемент вступает в действие. Код JavaScript, предоставленных в качестве значения из `ConditionScript` атрибут выполняется во время выполнения. Если значение равно true, анимация выполняется, в противном случае не. Следующая разметка предоставляет две анимации, каждый из них выполняется в 50% случаев после случайных. Так как может существовать только одна анимация в `<OnLoad>`, два `<Condition>` анимации соединяются друг с другом с использованием `<Sequence>` элемент:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

Обратите внимание, что знак «меньше» (`<`) в `ConditionScript` атрибут должен быть escape-(). При запуске этого скрипта, либо нет запусков анимации, один из двух или для обоих сделать.


[![Tпанель HE исчезновение без изменения размера, поэтому второй анимации запуски, первый из них не](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

Панели исчезновение без изменения размера, поэтому второй анимации запуски, первый из них не ([Просмотр полноразмерного изображения](animation-depending-on-a-condition-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](executing-several-animations-after-each-other-vb.md)
> [Вперед](picking-one-animation-out-of-a-list-vb.md)
