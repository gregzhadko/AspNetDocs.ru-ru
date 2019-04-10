---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: Динамическое добавление области Accordion (C#) | Документация Майкрософт
author: wenz
description: Элемент управления Accordion в AJAX Control Toolkit предоставляет несколько областей и пользователь может одновременно отобразить один из них. Панели обычно объявляются w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: ea526ce8abdf6f7013e8dd832824c21448878e0b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59416848"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="4a1e3-104">Динамическое добавление области Accordion (C#)</span><span class="sxs-lookup"><span data-stu-id="4a1e3-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="4a1e3-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4a1e3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4a1e3-106">[Скачать код](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4a1e3-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="4a1e3-107">Элемент управления Accordion в AJAX Control Toolkit предоставляет несколько областей и пользователь может одновременно отобразить один из них.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="4a1e3-108">Обычно панелей объявлены внутри самой страницы, но серверный код может использоваться для достижения того же результата.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>


## <a name="overview"></a><span data-ttu-id="4a1e3-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="4a1e3-109">Overview</span></span>

<span data-ttu-id="4a1e3-110">Элемент управления Accordion в AJAX Control Toolkit предоставляет несколько областей и пользователь может одновременно отобразить один из них.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="4a1e3-111">Обычно панелей объявлены внутри самой страницы, но серверный код может использоваться для достижения того же результата.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="4a1e3-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="4a1e3-112">Steps</span></span>

<span data-ttu-id="4a1e3-113">Элемент управления Accordion предоставляет все важные свойства серверного кода.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="4a1e3-114">Помимо прочего `Panes` свойство предоставляет доступ к коллекции областей, которые составляют Accordion.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="4a1e3-115">Каждой области есть типа `AccordionPane`.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="4a1e3-116">Таким образом, это просто создание такой области:</span><span class="sxs-lookup"><span data-stu-id="4a1e3-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="4a1e3-117">`HeaderContainer` Свойство `AccordionPane` предоставляет доступ к элементам управления ASP.NET, в разделе заголовка области; `ContentContainer` свойство `AccordionPane` делает то же самое для содержимого части области.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="4a1e3-118">Благодаря этому код ASP.NET для добавления содержимого в области:</span><span class="sxs-lookup"><span data-stu-id="4a1e3-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="4a1e3-119">Наконец, необходимо добавить pane(s) `Panes` коллекцию Гармошка:</span><span class="sxs-lookup"><span data-stu-id="4a1e3-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="4a1e3-120">Ниже приведен полный код на стороне сервера, который добавляет две панели в элемент управления Accordion.</span><span class="sxs-lookup"><span data-stu-id="4a1e3-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="4a1e3-121">Единственный отсутствующий элемент является Accordion, который зависит от наличия ASP.NET `ScriptManager` управления:</span><span class="sxs-lookup"><span data-stu-id="4a1e3-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="4a1e3-122">Чтобы завершить работу в примере, эти два класса CSS, на который ссылается элемент управления Accordion предоставляют сведения о стиле для браузера:</span><span class="sxs-lookup"><span data-stu-id="4a1e3-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]


[![T<span data-ttu-id="4a1e3-123">данные в Гармошка динамически была добавлена, серверный код]</span><span class="sxs-lookup"><span data-stu-id="4a1e3-123">he data in the accordion was dynamically added by server-side code]</span></span>(dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

<span data-ttu-id="4a1e3-124">Данные в Гармошка динамически добавленные серверного кода ([Просмотр полноразмерного изображения](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4a1e3-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4a1e3-125">[Назад](databinding-to-an-accordion-cs.md)
> [Вперед](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4a1e3-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
