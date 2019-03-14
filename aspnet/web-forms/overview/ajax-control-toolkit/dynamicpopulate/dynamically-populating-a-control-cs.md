---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: Динамическое заполнение элемента управления (C#) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 1f37a3a41c7b83738f97c0daacd781c52b55abc8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029511"
---
<a name="dynamically-populating-a-control-c"></a><span data-ttu-id="30d95-103">Динамическое заполнение элемента управления (C#)</span><span class="sxs-lookup"><span data-stu-id="30d95-103">Dynamically Populating a Control (C#)</span></span>
====================
<span data-ttu-id="30d95-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="30d95-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="30d95-105">[Скачать код](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="30d95-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)</span></span>

> <span data-ttu-id="30d95-106">Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="30d95-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>


## <a name="overview"></a><span data-ttu-id="30d95-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="30d95-107">Overview</span></span>

<span data-ttu-id="30d95-108">`DynamicPopulate` Элемента управления в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="30d95-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="30d95-109">Этом руководстве показано, как выполнить такую настройку.</span><span class="sxs-lookup"><span data-stu-id="30d95-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="30d95-110">Шаги</span><span class="sxs-lookup"><span data-stu-id="30d95-110">Steps</span></span>

<span data-ttu-id="30d95-111">Во-первых, необходимо, чтобы к веб-службе ASP.NET, который реализует метод, вызываемый `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="30d95-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="30d95-112">Класс веб-службы требует `ScriptService` атрибут, который определен в `Microsoft.Web.Script.Services`; в противном случае AJAX для ASP.NET не удается создать клиентский прокси JavaScript для веб-службы, который в свою очередь, необходим `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="30d95-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="30d95-113">Веб-метода должен ожидать, что один аргумент типа строки, называемой `contextKey`, так как `DynamicPopulate` элемент управления отправляет понимается набор сведений о контексте с каждый вызов веб-службы.</span><span class="sxs-lookup"><span data-stu-id="30d95-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="30d95-114">Следующая веб-служба возвращает текущую дату в формате, представленный `contextKey` аргумент:</span><span class="sxs-lookup"><span data-stu-id="30d95-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="30d95-115">Веб-служба затем сохраняется как `DynamicPopulate.cs.asmx`.</span><span class="sxs-lookup"><span data-stu-id="30d95-115">The web service is then saved as `DynamicPopulate.cs.asmx`.</span></span> <span data-ttu-id="30d95-116">Кроме того, вы можете реализовать `getDate()` метод как метод страницы в фактические страницы ASP.NET с `DynamicPopulate` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="30d95-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="30d95-117">На следующем шаге создайте новый файл ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="30d95-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="30d95-118">Как всегда, первым шагом является включение `ScriptManager` на текущей странице загрузки библиотеки ASP.NET AJAX и разработку набора средств элементов управления:</span><span class="sxs-lookup"><span data-stu-id="30d95-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="30d95-119">Затем добавьте элемент управления label (например с помощью HTML-элемент управления с тем же именем, или &lt; `asp:Label`  / &gt; веб-элемент управления) где позже будет показано, результатом вызова веб-службы.</span><span class="sxs-lookup"><span data-stu-id="30d95-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

<span data-ttu-id="30d95-120">Кнопка HTML (как элемент управления HTML, так как мы не требуют обратную передачу на сервер) будет использоваться для запуска динамического заполнения:</span><span class="sxs-lookup"><span data-stu-id="30d95-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="30d95-121">Наконец, мы должны `DynamicPopulateExtender` управления связывание всех компонентов.</span><span class="sxs-lookup"><span data-stu-id="30d95-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="30d95-122">Устанавливается следующие атрибуты (помимо очевидными, `ID` и `runat` = `"server"`):</span><span class="sxs-lookup"><span data-stu-id="30d95-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="30d95-123">`TargetControlID` куда поместить результат из вызова веб-службы</span><span class="sxs-lookup"><span data-stu-id="30d95-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="30d95-124">`ServicePath` путь к веб-службы (опустить, если вы хотите использовать метод страницы)</span><span class="sxs-lookup"><span data-stu-id="30d95-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="30d95-125">`ServiceMethod` Имя веб-метода или метода страницы</span><span class="sxs-lookup"><span data-stu-id="30d95-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="30d95-126">`ContextKey` сведения о контексте, который должны отправляться веб-службы</span><span class="sxs-lookup"><span data-stu-id="30d95-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="30d95-127">`PopulateTriggerControlID` элемент, который запускает вызов веб-службы</span><span class="sxs-lookup"><span data-stu-id="30d95-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="30d95-128">`ClearContentsDuringUpdate` следует ли очистить целевого элемента во время вызова веб-службы</span><span class="sxs-lookup"><span data-stu-id="30d95-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="30d95-129">Как вы видите, элемент управления требуются некоторые сведения, но размещением всего подряд в месте довольно просто.</span><span class="sxs-lookup"><span data-stu-id="30d95-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="30d95-130">Далее приведена разметка для `DynamicPopulateExtender` элемента управления в текущем сценарии:</span><span class="sxs-lookup"><span data-stu-id="30d95-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="30d95-131">Откройте страницу ASP.NET в браузере и нажмите кнопку ""; Вы получите текущую дату в формате месяц день год.</span><span class="sxs-lookup"><span data-stu-id="30d95-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>


<span data-ttu-id="30d95-132">[![Нажмите кнопку извлекает дату с сервера](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="30d95-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="30d95-133">Нажмите кнопку извлекает дату с сервера ([Просмотр полноразмерного изображения](dynamically-populating-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="30d95-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="30d95-134">Вперед</span><span class="sxs-lookup"><span data-stu-id="30d95-134">Next</span></span>](dynamically-populating-a-control-using-javascript-code-cs.md)
