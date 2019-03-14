---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: Анимация в ответ на взаимодействие пользователя (Visual Basic) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Анимацию можно star...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 0d9a3bf853afdbde0a419b90d1563fc06d3f9979
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057851"
---
<a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="c251c-104">Анимация в ответ на взаимодействие пользователя (VB)</span><span class="sxs-lookup"><span data-stu-id="c251c-104">Animating in Response To User Interaction (VB)</span></span>
====================
<span data-ttu-id="c251c-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c251c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c251c-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c251c-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="c251c-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c251c-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c251c-108">Анимации могут запускаться автоматически или могут быть предприняты взаимодействием с пользователем, например, щелкнув мышью.</span><span class="sxs-lookup"><span data-stu-id="c251c-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>


## <a name="overview"></a><span data-ttu-id="c251c-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="c251c-109">Overview</span></span>

<span data-ttu-id="c251c-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c251c-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c251c-111">Анимации могут запускаться автоматически или могут быть предприняты взаимодействием с пользователем, например, щелкнув мышью.</span><span class="sxs-lookup"><span data-stu-id="c251c-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="c251c-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="c251c-112">Steps</span></span>

<span data-ttu-id="c251c-113">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="c251c-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="c251c-114">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c251c-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="c251c-115">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="c251c-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="c251c-116">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="c251c-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="c251c-117">В рамках `<Animations>` узел, существует пять способов для запуска анимации с помощью взаимодействия с пользователем (неотображаемый элемент является `<OnLoad>` которого будет выполнена после полной загрузки страницы в целом):</span><span class="sxs-lookup"><span data-stu-id="c251c-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="c251c-118">`<OnClick>` (щелчка мыши на элементе управления)</span><span class="sxs-lookup"><span data-stu-id="c251c-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="c251c-119">`<OnHoverOut>` (указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="c251c-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="c251c-120">`<OnHoverOver>` (указатель мыши находится над элементом управления, остановка `<OnHoverOut>` анимации)</span><span class="sxs-lookup"><span data-stu-id="c251c-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="c251c-121">`<OnMouseOut>` (указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="c251c-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="c251c-122">`<OnMouseOver>` (указатель мыши находится над элементом управления, не останавливает `<OnMouseOut>` анимации)</span><span class="sxs-lookup"><span data-stu-id="c251c-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="c251c-123">В этом случае `<OnClick>` используется.</span><span class="sxs-lookup"><span data-stu-id="c251c-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="c251c-124">При нажатии на панели, он изменяется и исчезает, в то же время.</span><span class="sxs-lookup"><span data-stu-id="c251c-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


<span data-ttu-id="c251c-125">[![Нажатие клавиши мыши запускает анимацию](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c251c-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="c251c-126">Нажатие клавиши мыши запускает анимацию ([Просмотр полноразмерного изображения](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c251c-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c251c-127">[Назад](picking-one-animation-out-of-a-list-vb.md)
> [Вперед](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c251c-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
