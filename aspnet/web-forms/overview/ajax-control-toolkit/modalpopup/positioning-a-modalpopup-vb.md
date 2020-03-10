---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Размещение ModalPopup (VB) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств. Однако элемент управления не предлагает...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: fb79a08a339588ed8adc4b4236911819ea9286b4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496896"
---
# <a name="positioning-a-modalpopup-vb"></a><span data-ttu-id="77be9-104">Размещение ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="77be9-104">Positioning a ModalPopup (VB)</span></span>

<span data-ttu-id="77be9-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="77be9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="77be9-106">[Скачать код](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="77be9-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span></span>

> <span data-ttu-id="77be9-107">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="77be9-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="77be9-108">Однако элемент управления не предоставляет встроенные функции для позиционирования всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="77be9-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="77be9-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="77be9-109">Overview</span></span>

<span data-ttu-id="77be9-110">Элемент управления ModalPopup в наборе средств AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="77be9-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="77be9-111">Однако элемент управления не предоставляет встроенные функции для позиционирования всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="77be9-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="77be9-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="77be9-112">Steps</span></span>

<span data-ttu-id="77be9-113">Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, `ScriptManager`.</span><span class="sxs-lookup"><span data-stu-id="77be9-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="77be9-114">элемент управления должен размещаться в любом месте страницы (но в элементе `<form>`):</span><span class="sxs-lookup"><span data-stu-id="77be9-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="77be9-115">Затем добавьте панель, которая выступает в качестве модального всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="77be9-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="77be9-116">Кнопка используется для закрытия всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="77be9-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="77be9-117">При отображении всплывающего окна оно должно располагаться в определенном месте страницы.</span><span class="sxs-lookup"><span data-stu-id="77be9-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="77be9-118">Для этой задачи создается клиентская функция JavaScript.</span><span class="sxs-lookup"><span data-stu-id="77be9-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="77be9-119">Сначала он пытается получить доступ к панели.</span><span class="sxs-lookup"><span data-stu-id="77be9-119">It first tries to access the panel.</span></span> <span data-ttu-id="77be9-120">В случае успешности положение панели задается с помощью CSS и JavaScript (измените положение всплывающего окна в нем).</span><span class="sxs-lookup"><span data-stu-id="77be9-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="77be9-121">Однако элемент управления `ModalPopupExtender` также пытается расположить всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="77be9-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="77be9-122">Таким образом, код JavaScript многократно помещает всплывающее окно в каждую десятую часть секунды.</span><span class="sxs-lookup"><span data-stu-id="77be9-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

<span data-ttu-id="77be9-123">Как видите, возвращаемое значение метода `setTimeout()` JavaScript сохраняется в глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="77be9-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="77be9-124">Это позволяет предотвратить повторное позиционирование всплывающего окна по запросу с помощью метода `clearTimeout()`:</span><span class="sxs-lookup"><span data-stu-id="77be9-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

<span data-ttu-id="77be9-125">Теперь все, что осталось сделать, — это заставить браузер вызывать эти функции при необходимости.</span><span class="sxs-lookup"><span data-stu-id="77be9-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="77be9-126">Функция `movePanel()` JavaScript должна вызываться при нажатии кнопки, которая активирует панель:</span><span class="sxs-lookup"><span data-stu-id="77be9-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

<span data-ttu-id="77be9-127">При закрытии всплывающего окна функция `stopMoving()` вступает в игру. это может быть вызвано в элементе управления `ModalPopupExtender`:</span><span class="sxs-lookup"><span data-stu-id="77be9-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

<span data-ttu-id="77be9-128">[![модальное всплывающее окно отображается в указанной позиции](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77be9-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="77be9-129">Модальное всплывающее окно отображается в указанной позиции ([щелкните, чтобы просмотреть изображение с полным размером](positioning-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="77be9-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="77be9-130">Назад</span><span class="sxs-lookup"><span data-stu-id="77be9-130">Previous</span></span>](handling-postbacks-from-a-modalpopup-vb.md)
