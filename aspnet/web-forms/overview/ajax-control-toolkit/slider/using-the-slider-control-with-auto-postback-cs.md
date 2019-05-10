---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: С помощью элемента управления Slider с автоматической обратной передачей (C#) | Документация Майкрософт
author: wenz
description: Элемент управления "ползунок" в AJAX Control Toolkit предоставляет графическим ползунком, которые могут контролироваться с помощью мыши. Это можно делать Автоматическая разноска "ползунок"...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 2b1e7c2e62438876343987917ffc8f792c755186
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124637"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="be714-104">С помощью элемента управления Slider с автоматической обратной передачей (C#)</span><span class="sxs-lookup"><span data-stu-id="be714-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="be714-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="be714-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="be714-106">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="be714-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="be714-107">Элемент управления "ползунок" в AJAX Control Toolkit предоставляет графическим ползунком, которые могут контролироваться с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="be714-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="be714-108">Это можно делать autopostback ползунок один раз изменении ее значения.</span><span class="sxs-lookup"><span data-stu-id="be714-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="be714-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="be714-109">Overview</span></span>

<span data-ttu-id="be714-110">Элемент управления "ползунок" в AJAX Control Toolkit предоставляет графическим ползунком, которые могут контролироваться с помощью мыши.</span><span class="sxs-lookup"><span data-stu-id="be714-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="be714-111">Это можно делать autopostback ползунок один раз изменении ее значения.</span><span class="sxs-lookup"><span data-stu-id="be714-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="be714-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="be714-112">Steps</span></span>

<span data-ttu-id="be714-113">Чтобы сделать ползунок автоматически обратной передачи, при изменении, оба поля атрибут должен быть добавлен `AutoPostBack="true"`: Текстовое поле, которое станет самой ползунок и текстовое поле, которое содержит положение ползунка.</span><span class="sxs-lookup"><span data-stu-id="be714-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="be714-114">Далее приведена разметка необходимые для этого:</span><span class="sxs-lookup"><span data-stu-id="be714-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="be714-115">`SliderExtender` Элемента управления ASP.NET AJAX Control Toolkit назначает функциональные возможности "ползунок" для двух текстовых полях:</span><span class="sxs-lookup"><span data-stu-id="be714-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="be714-116">Дополнительные метки элемента будет использоваться позже для информирования пользователей обратной передачи:</span><span class="sxs-lookup"><span data-stu-id="be714-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="be714-117">Наконец `ScriptManager` элемент управления AJAX для ASP.NET загружает требуемого кода JavaScript для набора средств управления для работы:</span><span class="sxs-lookup"><span data-stu-id="be714-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="be714-118">Теперь ползунок обратной передаче; на стороне сервера это событие может быть перехвачено и обрабатываемое:</span><span class="sxs-lookup"><span data-stu-id="be714-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="be714-119">[![Перемещая ползунок инициирует обратную передачу](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="be714-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="be714-120">Перемещая ползунок инициирует обратную передачу ([Просмотр полноразмерного изображения](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="be714-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="be714-121">[![После этого дата это изменение записывается в метке](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="be714-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="be714-122">После этого дата это изменение записывается в метке ([Просмотр полноразмерного изображения](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="be714-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="be714-123">Вперед</span><span class="sxs-lookup"><span data-stu-id="be714-123">Next</span></span>](databinding-the-slider-control-cs.md)
