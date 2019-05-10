---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: Отключение действий во время анимации (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Она также поддерживает действия...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: dd69317c4a9b5a98302683766e6bc699d3b6396d
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108653"
---
# <a name="disabling-actions-during-animation-c"></a><span data-ttu-id="ee42b-104">Отключение действий во время анимации (C#)</span><span class="sxs-lookup"><span data-stu-id="ee42b-104">Disabling Actions during Animation (C#)</span></span>

<span data-ttu-id="ee42b-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ee42b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ee42b-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ee42b-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span></span>

> <span data-ttu-id="ee42b-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="ee42b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ee42b-108">Она также поддерживает действия, например, щелчки мышью.</span><span class="sxs-lookup"><span data-stu-id="ee42b-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="ee42b-109">Тем не менее при щелчка кнопкой мыши запускает анимацию, желательно отключить щелчки мыши во время анимации.</span><span class="sxs-lookup"><span data-stu-id="ee42b-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="ee42b-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="ee42b-110">Overview</span></span>

<span data-ttu-id="ee42b-111">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="ee42b-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ee42b-112">Она также поддерживает действия, например, щелчки мышью.</span><span class="sxs-lookup"><span data-stu-id="ee42b-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="ee42b-113">Тем не менее при щелчка кнопкой мыши запускает анимацию, желательно отключить щелчки мыши во время анимации.</span><span class="sxs-lookup"><span data-stu-id="ee42b-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="ee42b-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="ee42b-114">Steps</span></span>

<span data-ttu-id="ee42b-115">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="ee42b-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

<span data-ttu-id="ee42b-116">Анимация будет применяться к HTML-кнопка следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ee42b-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

<span data-ttu-id="ee42b-117">Обратите внимание, что элемент управления HTML используется вместо веб-элемент управления, поскольку мы не хотим, кнопку, чтобы создать обратной передачи; он просто должен запустить клиентские анимации для нас.</span><span class="sxs-lookup"><span data-stu-id="ee42b-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="ee42b-118">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="ee42b-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

<span data-ttu-id="ee42b-119">В рамках `<Animations>` узел, `<OnClick>` является правильного элемента для обработки щелчка мыши.</span><span class="sxs-lookup"><span data-stu-id="ee42b-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="ee42b-120">Тем не менее во время анимации, а также может быть нажата кнопка.</span><span class="sxs-lookup"><span data-stu-id="ee42b-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="ee42b-121">`<EnableAction>` Элемент заняться.</span><span class="sxs-lookup"><span data-stu-id="ee42b-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="ee42b-122">Параметр `Enabled="false"` отключает кнопку как часть анимации.</span><span class="sxs-lookup"><span data-stu-id="ee42b-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="ee42b-123">Так как мы используем несколько отдельных анимаций, (Отключение кнопки и фактическое анимации), `<Parallel>` элемент является обязательным для объединения одной анимации вместе в одну.</span><span class="sxs-lookup"><span data-stu-id="ee42b-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="ee42b-124">Вот полная разметка для `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="ee42b-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

<span data-ttu-id="ee42b-125">Также возможно включить кнопку после анимации, используя следующий XML-элемент в конец списка:</span><span class="sxs-lookup"><span data-stu-id="ee42b-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

<span data-ttu-id="ee42b-126">Однако в данном сценарии это окажется бесполезной после кнопки исчезает и остается невидимым в конце анимации.</span><span class="sxs-lookup"><span data-stu-id="ee42b-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="ee42b-127">[![Кнопка отключена, а анимация](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ee42b-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span></span>

<span data-ttu-id="ee42b-128">Кнопка отключена, а анимация ([Просмотр полноразмерного изображения](disabling-actions-during-animation-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ee42b-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ee42b-129">[Назад](animating-in-response-to-user-interaction-cs.md)
> [Вперед](triggering-an-animation-in-another-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ee42b-129">[Previous](animating-in-response-to-user-interaction-cs.md)
[Next](triggering-an-animation-in-another-control-cs.md)</span></span>
