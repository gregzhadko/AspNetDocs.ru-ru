---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Анимация элемента управления UpdatePanel (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c403cddd1e3eb5b66f795a2e4032fae63fdb26ca
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130741"
---
# <a name="animating-an-updatepanel-control-c"></a>Анимация элемента управления UpdatePanel (C#)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого элемента управления UpdatePanel специальные расширения существует, во многом полагается на framework анимации: UpdatePanelAnimation. Этом руководстве показано, как настроить такой анимации для элемента управления UpdatePanel.

## <a name="overview"></a>Обзор

Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого `UpdatePanel`, существует специальные расширения, которая основывается на использовании framework анимации: `UpdatePanelAnimation`. Этом руководстве показано, как настроить такой анимацию для `UpdatePanel`.

## <a name="steps"></a>Шаги

Первым шагом является обычным образом, чтобы включить `ScriptManager` на странице, ASP.NET AJAX library загружается и может использоваться набор элементов управления:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

Анимация в этом сценарии будет применяться к ASP.NET `Wizard` веб-элемента управления, находящихся в `UpdatePanel`. Три шага (произвольному) предоставляют достаточно возможности для запуска операций обратной передачи.

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

Разметка, необходимые для `UpdatePanelAnimationExtender` управления очень похож на разметку, используемую для `AnimationExtender`. В `TargetControlID` атрибут, мы предоставляем `ID` из `UpdatePanel` для анимации; в `UpdatePanelAnimationExtender` элемента управления, `<Animations>` элемент содержит XML-разметку для анимации. Однако есть одно различие: Объем события и обработчики событий ограничено по сравнению с `AnimationExtender`. Для `UpdatePanels`, только два из них существует:

- `<OnUpdated>` Когда будет обновлена UpdatePanel
- `<OnUpdating>` Когда UpdatePanel начинает обновление

В этом случае новый содержимое `UpdatePanel` (после обратной отправки) должны появление. Это необходимые средства разметки для этого:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

Теперь всякий раз, когда происходит обратная передача внутри UpdatePanel, новое содержимое панели Плавное.

[![Следующий шаг мастера является плавный переход](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

Следующий шаг мастера является плавный переход ([Просмотр полноразмерного изображения](animating-an-updatepanel-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](changing-an-animation-using-client-side-code-cs.md)
> [Вперед](dynamically-controlling-updatepanel-animations-cs.md)
