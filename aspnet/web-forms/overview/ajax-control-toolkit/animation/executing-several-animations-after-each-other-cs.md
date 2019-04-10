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
ms.openlocfilehash: 644af2485c1a51f2de209e968ba1b3475350fa47
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59394072"
---
# <a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="e32ce-104">Выполнение нескольких анимаций друг за другом (C#)</span><span class="sxs-lookup"><span data-stu-id="e32ce-104">Executing Several Animations after Each Other (C#)</span></span>

<span data-ttu-id="e32ce-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e32ce-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e32ce-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e32ce-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="e32ce-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="e32ce-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e32ce-108">Он одновременное выполнение нескольких анимаций один за другим.</span><span class="sxs-lookup"><span data-stu-id="e32ce-108">It allows to run several animations one after the other.</span></span>


<span data-ttu-id="e32ce-109">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="e32ce-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e32ce-110">Он одновременное выполнение нескольких анимаций один за другим.</span><span class="sxs-lookup"><span data-stu-id="e32ce-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="e32ce-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="e32ce-111">Steps</span></span>

<span data-ttu-id="e32ce-112">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="e32ce-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="e32ce-113">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e32ce-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="e32ce-114">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="e32ce-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="e32ce-115">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным</span><span class="sxs-lookup"><span data-stu-id="e32ce-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory</span></span> `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="e32ce-116">В рамках `<Animations>` узла, используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="e32ce-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="e32ce-117">Как правило `<OnLoad>` принимает только одна анимация.</span><span class="sxs-lookup"><span data-stu-id="e32ce-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="e32ce-118">Платформа анимации позволяет объединить несколько анимаций в один с помощью `<Sequence>` элемент.</span><span class="sxs-lookup"><span data-stu-id="e32ce-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="e32ce-119">Все анимации в `<Sequence>` , выполняются за другим.</span><span class="sxs-lookup"><span data-stu-id="e32ce-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="e32ce-120">Вот возможные разметку для `AnimationExtender` элемента управления, сначала внесение панели «ширина» и затем уменьшая высоту:</span><span class="sxs-lookup"><span data-stu-id="e32ce-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="e32ce-121">При выполнении этого сценария, панели первой получает шире и затем меньшего размера.</span><span class="sxs-lookup"><span data-stu-id="e32ce-121">When you run this script, the panel first gets wider and then smaller.</span></span>


[![F<span data-ttu-id="e32ce-122">ервый ширина будет увеличена]</span><span class="sxs-lookup"><span data-stu-id="e32ce-122">irst the width is increased]</span></span>(executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)

<span data-ttu-id="e32ce-123">Сначала ширина увеличивается ([Просмотр полноразмерного изображения](executing-several-animations-after-each-other-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e32ce-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>


[![T<span data-ttu-id="e32ce-124">ри высота уменьшается]</span><span class="sxs-lookup"><span data-stu-id="e32ce-124">hen the height is decreased]</span></span>(executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)

<span data-ttu-id="e32ce-125">Затем уменьшается на высоту ([Просмотр полноразмерного изображения](executing-several-animations-after-each-other-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e32ce-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e32ce-126">[Назад](executing-several-animations-at-the-same-time-cs.md)
> [Вперед](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e32ce-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
