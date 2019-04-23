---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: Анимация в ответ на взаимодействие пользователя (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Анимацию можно star...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: c0e2888207e4fa0363fc3b357ae00108ffe817f5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59415223"
---
# <a name="animating-in-response-to-user-interaction-c"></a>Анимация в ответ на взаимодействие пользователя (C#)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Анимации могут запускаться автоматически или могут быть предприняты взаимодействием с пользователем, например, щелкнув мышью.


## <a name="overview"></a>Обзор

Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Анимации могут запускаться автоматически или могут быть предприняты взаимодействием с пользователем, например, щелкнув мышью.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

Анимация будет применяться к панели текста, который выглядит следующим образом:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

В рамках `<Animations>` узел, существует пять способов для запуска анимации с помощью взаимодействия с пользователем (неотображаемый элемент является `<OnLoad>` которого будет выполнена после полной загрузки страницы в целом):

- `<OnClick>` (щелчка мыши на элементе управления)
- `<OnHoverOut>` (указатель мыши покидает элемент управления)
- `<OnHoverOver>` (указатель мыши находится над элементом управления, остановка `<OnHoverOut>` анимации)
- `<OnMouseOut>` (указатель мыши покидает элемент управления)
- `<OnMouseOver>` (указатель мыши находится над элементом управления, не останавливает `<OnMouseOut>` анимации)

В этом случае `<OnClick>` используется. При нажатии на панели, он изменяется и исчезает, в то же время.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]


[![Нажатие клавиши мыши запускает анимацию](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

Нажатие клавиши мыши запускает анимацию ([Просмотр полноразмерного изображения](animating-in-response-to-user-interaction-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](picking-one-animation-out-of-a-list-cs.md)
> [Вперед](disabling-actions-during-animation-cs.md)
