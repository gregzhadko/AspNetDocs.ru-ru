---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Обработка обратных передач из элемента управления Popup без UpdatePanel (VB) | Документация Майкрософт
author: wenz
description: Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления. Когда обратная передача происходит в SU...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446142"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="362aa-104">Обработка операций обратной передачи из элемента управления Popup без использования элемента управления UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="362aa-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="362aa-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="362aa-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="362aa-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="362aa-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="362aa-107">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="362aa-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="362aa-108">Если обратная передача происходит на такой панели и на странице есть несколько панелей, трудно определить, какая панель была нажата.</span><span class="sxs-lookup"><span data-stu-id="362aa-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="362aa-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="362aa-109">Overview</span></span>

<span data-ttu-id="362aa-110">Расширитель Попупконтрол в наборе средств AJAX Control Toolkit предоставляет простой способ активации всплывающего окна при активации любого другого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="362aa-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="362aa-111">Если обратная передача происходит на такой панели и на странице есть несколько панелей, трудно определить, какая панель была нажата.</span><span class="sxs-lookup"><span data-stu-id="362aa-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="362aa-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="362aa-112">Steps</span></span>

<span data-ttu-id="362aa-113">При использовании `PopupControl` с обратной передачей, но без `UpdatePanel` на странице, набор элементов управления не предлагает способ определить, какой клиентский элемент инициировал всплывающее окно, которое, в свою очередь, вызвало обратную передачу.</span><span class="sxs-lookup"><span data-stu-id="362aa-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="362aa-114">Но небольшой хитростью является обходной путь для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="362aa-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="362aa-115">Во-первых, вот основная настройка: два текстовых поля, которые вызывают одно и то же всплывающее окно, календарь.</span><span class="sxs-lookup"><span data-stu-id="362aa-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="362aa-116">Два `PopupControlExtenders` поместит текстовые поля и всплывающее окно вместе.</span><span class="sxs-lookup"><span data-stu-id="362aa-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="362aa-117">Основная идея состоит в том, чтобы добавить скрытое поле формы в элемент &lt;`form`&gt;, содержащий текстовое поле, которое запустило всплывающее окно:</span><span class="sxs-lookup"><span data-stu-id="362aa-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="362aa-118">При загрузке страницы код JavaScript добавляет обработчик событий в оба текстовых поля: каждый раз, когда пользователь щелкает текстовое поле, его имя записывается в скрытое поле формы:</span><span class="sxs-lookup"><span data-stu-id="362aa-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="362aa-119">В коде на стороне сервера значение скрытого поля должно быть считано.</span><span class="sxs-lookup"><span data-stu-id="362aa-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="362aa-120">Поскольку скрытые поля формы просты для управления, утвержденный список способов проверки скрытые значения является обязательным.</span><span class="sxs-lookup"><span data-stu-id="362aa-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="362aa-121">После определения правильного текстового поля в него записывается дата из календаря.</span><span class="sxs-lookup"><span data-stu-id="362aa-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="362aa-122">[![календарь появляется, когда пользователь щелкает текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="362aa-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="362aa-123">Календарь появляется, когда пользователь щелкает текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="362aa-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="362aa-124">[![, щелкнув дату, помещает ее в текстовое поле](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="362aa-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="362aa-125">Если щелкнуть дату, она помещается в текстовое поле ([щелкните, чтобы просмотреть изображение с полным размером](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="362aa-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="362aa-126">Назад</span><span class="sxs-lookup"><span data-stu-id="362aa-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
