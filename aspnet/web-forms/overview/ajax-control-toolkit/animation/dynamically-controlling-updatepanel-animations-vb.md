---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: Динамическое управление анимациями UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Для содержимого...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 2a4c01ffdee20f2c7970d999b34bf1374088d4c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053671"
---
<a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="a7932-104">Динамическое управление анимациями UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="a7932-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>
====================
<span data-ttu-id="a7932-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a7932-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a7932-106">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a7932-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="a7932-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="a7932-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a7932-108">Для содержимого элемента управления UpdatePanel специальные расширения существует, во многом полагается на framework анимации: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="a7932-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="a7932-109">Он также может работать вместе с триггерах UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="a7932-109">It can also work together with UpdatePanel triggers.</span></span>


## <a name="overview"></a><span data-ttu-id="a7932-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="a7932-110">Overview</span></span>

<span data-ttu-id="a7932-111">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="a7932-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a7932-112">Для содержимого `UpdatePanel`, существует специальные расширения, которая основывается на использовании framework анимации: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="a7932-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="a7932-113">Он также может работать вместе с `UpdatePanel` триггеров.</span><span class="sxs-lookup"><span data-stu-id="a7932-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="a7932-114">Шаги</span><span class="sxs-lookup"><span data-stu-id="a7932-114">Steps</span></span>

<span data-ttu-id="a7932-115">Первым шагом является обычным образом, чтобы включить `ScriptManager` на странице, ASP.NET AJAX library загружается и может использоваться набор элементов управления:</span><span class="sxs-lookup"><span data-stu-id="a7932-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="a7932-116">Анимация в этом сценарии будет применяться для отображения в виде текущего времени.</span><span class="sxs-lookup"><span data-stu-id="a7932-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="a7932-117">Эти сведения можно записать в метку с помощью `Page_Load()` метод, или (для простоты) используется следующий встроенный код:</span><span class="sxs-lookup"><span data-stu-id="a7932-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="a7932-118">Кроме того создается кнопка для активации, обновляя время:</span><span class="sxs-lookup"><span data-stu-id="a7932-118">Also, a button to trigger updating the time is created:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="a7932-119">Этот код помещается в переменную `<ContentTemplate>` раздел `UpdatePanel` элемент.</span><span class="sxs-lookup"><span data-stu-id="a7932-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="a7932-120">Панели `UpdateMode` атрибута должно быть присвоено `"Conditional"`, поскольку только триггеры могут обновлять содержимое панели.</span><span class="sxs-lookup"><span data-stu-id="a7932-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="a7932-121">В `<Triggers>` раздел `UpdatePanel`, создается триггер асинхронной обратной передачи и привязаны к `Click` события кнопки.</span><span class="sxs-lookup"><span data-stu-id="a7932-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="a7932-122">Таким образом, если пользователь нажимает кнопку, `UpdatePanel` обновляется.</span><span class="sxs-lookup"><span data-stu-id="a7932-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="a7932-123">Далее приведена разметка для `UpdatePanel` управления:</span><span class="sxs-lookup"><span data-stu-id="a7932-123">Here is the markup for the `UpdatePanel` control:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="a7932-124">Наконец `UpdatePanelAnimationExtender` должен быть настроен: Задайте `TargetControlID` атрибут с идентификатором панели и определите анимацию в модуле.</span><span class="sxs-lookup"><span data-stu-id="a7932-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="a7932-125">Плавный переход в делает смысле, который создает удобный визуальное выделение важных фрагментов, на время обновления.</span><span class="sxs-lookup"><span data-stu-id="a7932-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="a7932-126">Расширения разметки может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a7932-126">Your extender markup may then look like this:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="a7932-127">Запустите файл в браузере.</span><span class="sxs-lookup"><span data-stu-id="a7932-127">Run the file in the browser.</span></span> <span data-ttu-id="a7932-128">При каждом нажатии кнопки текущее время отображается на панели, всегда плавный переход течение одной секунды.</span><span class="sxs-lookup"><span data-stu-id="a7932-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>


<span data-ttu-id="a7932-129">[![Текущее время плавный переход](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a7932-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="a7932-130">Текущее время плавный переход ([Просмотр полноразмерного изображения](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a7932-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a7932-131">Назад</span><span class="sxs-lookup"><span data-stu-id="a7932-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
