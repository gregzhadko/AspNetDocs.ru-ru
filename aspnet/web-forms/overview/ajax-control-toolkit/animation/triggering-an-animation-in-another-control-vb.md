---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Запуск анимации в другой элемент управления (Visual Basic) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Как правило, запуск...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: cc27e44ae42865eebbf67da69dbe1aa43a57a4d7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128167"
---
# <a name="triggering-an-animation-in-another-control-vb"></a>Запуск анимации в другом элементе управления (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Как правило запуск анимации активируется взаимодействие пользователя с одного элемента управления. Тем не менее также возможность взаимодействия с одного элемента управления, а затем анимации другого элемента управления.

## <a name="overview"></a>Обзор

Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Как правило запуск анимации активируется взаимодействие пользователя с одного элемента управления. Тем не менее также возможность взаимодействия с одного элемента управления, а затем анимации другого элемента управления.

## <a name="steps"></a>Шаги

Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

Анимация будет применяться к панели текста, который выглядит следующим образом:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

Для запуска анимации на панели, используется как кнопка HTML. Обратите внимание, что `<input type="button" />` favoured через `<asp:Button />` поскольку мы не хотим обратную передачу при нажатии этой кнопки.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`. Очень важно задать `TargetControlID` для ИД кнопки (элемент триггера в анимации), не идентификатору панели (элемент, выполняется анимация)

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

В рамках `<Animations>` узел, анимации месте как обычно. Чтобы сделать их изменить на панели, не нажатием кнопки, задайте `AnimationTarget` атрибут для каждого элемента анимации в `AnimationExtender`. Значение для `AnimationTarget` — это идентификатор панели, конечно. Таким образом, анимации, которые происходят с панелью, не с помощью активации кнопки. Вот `AnimationExtender` разметки для этого сценария:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Обратите внимание, специальный заказ, в котором отображаются отдельные анимации. Во-первых кнопки получает отключена после выполнения анимации. Так как она не `AnimationTarget` атрибут в `<EnableAction>` элемент, эта анимация применяется к исходного управления: кнопки. Следующие две анимации действия должны выполняться в параллельном режиме (`<Parallel>` элемент). Оба имеют свои `AnimationTarget` атрибуты значения `"Panel1"`, таким образом анимации на панели, а не кнопки.

[![Нажмите кнопку мыши запускает анимацию панели](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

Нажмите кнопку мыши запускает анимацию панели ([Просмотр полноразмерного изображения](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](disabling-actions-during-animation-vb.md)
> [Вперед](modifying-animations-from-the-server-side-vb.md)
