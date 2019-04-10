---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: Выполнение нескольких анимаций одновременно (Visual Basic) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Он позволяет выполнять severa...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: f8bb91de9642814a79d0fddd642928c25c58ebfd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59402847"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a>Выполнение нескольких анимаций одновременно (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Он одновременное выполнение нескольких анимаций параллельно.


## <a name="overview"></a>Обзор

Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Он одновременное выполнение нескольких анимаций параллельно.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

Анимация будет применяться к панели текста, который выглядит следующим образом:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

В рамках `<Animations>` узла, используйте `<OnLoad>` для запуска анимации после полной загрузки страницы. Как правило `<OnLoad>` принимает только одна анимация. Платформа анимации позволяет объединить несколько анимаций в один с помощью `<Parallel>` элемент. Все анимации в `<Parallel>` выполняются одновременно.

Вот возможные разметку для `AnimationExtender` элемента управления, исчезновение и изменение размера панели, в то же время:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

И действительно: при выполнении этого скрипта панели отображается, затем изменяет размеры (более чем утраивается его ширину и высоту, потребленных в рамках) и исчезает, в то же время.


[![Tпанель HE существует исчезновение и изменение размера (в том числе его содержимого, благодаря механизм визуализации в браузере)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

Исчезновение и изменение размера (в том числе его содержимого, благодаря механизм визуализации в браузере) панели ([Просмотр полноразмерного изображения](executing-several-animations-at-the-same-time-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](adding-animation-to-a-control-vb.md)
> [Вперед](executing-several-animations-after-each-other-vb.md)
