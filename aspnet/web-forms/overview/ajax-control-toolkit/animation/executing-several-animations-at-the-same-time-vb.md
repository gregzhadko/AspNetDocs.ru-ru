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
ms.openlocfilehash: 02eb078a4fb8fddbbac18e4631214f354388cc2f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133415"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="a79f1-104">Выполнение нескольких анимаций одновременно (VB)</span><span class="sxs-lookup"><span data-stu-id="a79f1-104">Executing Several Animations at The Same Time (VB)</span></span>

<span data-ttu-id="a79f1-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a79f1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a79f1-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a79f1-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="a79f1-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="a79f1-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a79f1-108">Он одновременное выполнение нескольких анимаций параллельно.</span><span class="sxs-lookup"><span data-stu-id="a79f1-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="a79f1-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="a79f1-109">Overview</span></span>

<span data-ttu-id="a79f1-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="a79f1-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a79f1-111">Он одновременное выполнение нескольких анимаций параллельно.</span><span class="sxs-lookup"><span data-stu-id="a79f1-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="a79f1-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="a79f1-112">Steps</span></span>

<span data-ttu-id="a79f1-113">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="a79f1-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="a79f1-114">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a79f1-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="a79f1-115">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="a79f1-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="a79f1-116">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="a79f1-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="a79f1-117">В рамках `<Animations>` узла, используйте `<OnLoad>` для запуска анимации после полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="a79f1-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="a79f1-118">Как правило `<OnLoad>` принимает только одна анимация.</span><span class="sxs-lookup"><span data-stu-id="a79f1-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="a79f1-119">Платформа анимации позволяет объединить несколько анимаций в один с помощью `<Parallel>` элемент.</span><span class="sxs-lookup"><span data-stu-id="a79f1-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="a79f1-120">Все анимации в `<Parallel>` выполняются одновременно.</span><span class="sxs-lookup"><span data-stu-id="a79f1-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="a79f1-121">Вот возможные разметку для `AnimationExtender` элемента управления, исчезновение и изменение размера панели, в то же время:</span><span class="sxs-lookup"><span data-stu-id="a79f1-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="a79f1-122">И действительно: при выполнении этого скрипта панели отображается, затем изменяет размеры (более чем утраивается его ширину и высоту, потребленных в рамках) и исчезает, в то же время.</span><span class="sxs-lookup"><span data-stu-id="a79f1-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="a79f1-123">[![Исчезновение и изменение размера (в том числе его содержимого, благодаря механизм визуализации в браузере) панели](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a79f1-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="a79f1-124">Исчезновение и изменение размера (в том числе его содержимого, благодаря механизм визуализации в браузере) панели ([Просмотр полноразмерного изображения](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a79f1-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a79f1-125">[Назад](adding-animation-to-a-control-vb.md)
> [Вперед](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a79f1-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
