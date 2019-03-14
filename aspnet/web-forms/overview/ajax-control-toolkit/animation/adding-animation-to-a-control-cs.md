---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Добавление анимации в элемент управления (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. В этом руководстве показано как...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: aa977883af931bb74b791104cf4ee3212079e43a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031341"
---
<a name="adding-animation-to-a-control-c"></a><span data-ttu-id="1066b-104">Добавление анимации в элемент управления (C#)</span><span class="sxs-lookup"><span data-stu-id="1066b-104">Adding Animation to a Control (C#)</span></span>
====================
<span data-ttu-id="1066b-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1066b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1066b-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1066b-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="1066b-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1066b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1066b-108">Этом руководстве показано, как настроить такой анимации.</span><span class="sxs-lookup"><span data-stu-id="1066b-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="1066b-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="1066b-109">Overview</span></span>

<span data-ttu-id="1066b-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="1066b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1066b-111">Этом руководстве показано, как настроить такой анимации.</span><span class="sxs-lookup"><span data-stu-id="1066b-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="1066b-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="1066b-112">Steps</span></span>

<span data-ttu-id="1066b-113">Первым шагом является обычным образом, чтобы включить `ScriptManager` на странице, ASP.NET AJAX library загружается и может использоваться набор элементов управления:</span><span class="sxs-lookup"><span data-stu-id="1066b-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="1066b-114">Анимация в этом сценарии будут применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1066b-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="1066b-115">Связанный класс CSS для панели определяет цвет фона и шириной:</span><span class="sxs-lookup"><span data-stu-id="1066b-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="1066b-116">Далее, необходимо `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="1066b-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="1066b-117">После предоставления `ID` и обычные `runat="server"`, `TargetControlID` атрибута необходимо задать для элемента управления для анимации в нашем случае панели:</span><span class="sxs-lookup"><span data-stu-id="1066b-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="1066b-118">Всего применяется анимация декларативно, используя синтаксис XML, к сожалению в настоящее время не полностью поддерживается технологией IntelliSense в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1066b-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="1066b-119">Корневым узлом является `<Animations>;` в этот узел, несколько событий разрешены определяющие при анимации take(s) месте:</span><span class="sxs-lookup"><span data-stu-id="1066b-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="1066b-120">`OnClick` (щелчка мыши)</span><span class="sxs-lookup"><span data-stu-id="1066b-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="1066b-121">`OnHoverOut` (когда указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="1066b-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="1066b-122">`OnHoverOver` (при наведении указателя мыши над элементом управления, остановка `OnHoverOut` анимации)</span><span class="sxs-lookup"><span data-stu-id="1066b-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="1066b-123">`OnLoad` (когда страницы загрузки)</span><span class="sxs-lookup"><span data-stu-id="1066b-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="1066b-124">`OnMouseOut` (когда указатель мыши покидает элемент управления)</span><span class="sxs-lookup"><span data-stu-id="1066b-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="1066b-125">`OnMouseOver` (при наведении указателя мыши над элементом управления, не останавливает `OnMouseOut` анимации)</span><span class="sxs-lookup"><span data-stu-id="1066b-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="1066b-126">Платформа framework поставляется с набором анимации, каждый из них, представленный собственным XML-элементом.</span><span class="sxs-lookup"><span data-stu-id="1066b-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="1066b-127">Ниже указаны:</span><span class="sxs-lookup"><span data-stu-id="1066b-127">Here is a selection:</span></span>

- <span data-ttu-id="1066b-128">`<Color>` (Изменение цвета)</span><span class="sxs-lookup"><span data-stu-id="1066b-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="1066b-129">`<FadeIn>` (плавный переход)</span><span class="sxs-lookup"><span data-stu-id="1066b-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="1066b-130">`<FadeOut>` (исчезновение)</span><span class="sxs-lookup"><span data-stu-id="1066b-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="1066b-131">`<Property>` (изменение свойства элемента управления)</span><span class="sxs-lookup"><span data-stu-id="1066b-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="1066b-132">`<Pulse>` (pulsating)</span><span class="sxs-lookup"><span data-stu-id="1066b-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="1066b-133">`<Resize>` (изменение размера)</span><span class="sxs-lookup"><span data-stu-id="1066b-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="1066b-134">`<Scale>` (Пропорциональное изменение размера)</span><span class="sxs-lookup"><span data-stu-id="1066b-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="1066b-135">В этом примере панели должны скрывать. Анимация должна осуществляться 1,5 секунды (`Duration` атрибут), отображение 24 (анимации шаги) кадров в секунду (`Fps` attributs).</span><span class="sxs-lookup"><span data-stu-id="1066b-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attributs).</span></span> <span data-ttu-id="1066b-136">Вот полная разметка для `AnimationExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="1066b-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="1066b-137">При выполнении этого скрипта панели отображается и исчезает в один с половиной секунд.</span><span class="sxs-lookup"><span data-stu-id="1066b-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


<span data-ttu-id="1066b-138">[![Исчезновение панели](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1066b-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="1066b-139">Исчезновение панели ([Просмотр полноразмерного изображения](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1066b-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1066b-140">Вперед</span><span class="sxs-lookup"><span data-stu-id="1066b-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
