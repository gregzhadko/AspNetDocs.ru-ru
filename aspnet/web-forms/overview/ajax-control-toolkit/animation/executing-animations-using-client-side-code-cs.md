---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Выполнение анимаций с помощью клиентского кода (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Выполнение анимации...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: a8812b3b9f9a34b34a579d6f5595b9ffc175caa4
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2019
ms.locfileid: "58420990"
---
<a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="e59f7-104">Выполнение анимаций с помощью клиентского кода (C#)</span><span class="sxs-lookup"><span data-stu-id="e59f7-104">Executing Animations Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="e59f7-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e59f7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e59f7-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e59f7-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="e59f7-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="e59f7-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e59f7-108">Выполнение анимации могут также инициироваться с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e59f7-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="e59f7-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="e59f7-109">Overview</span></span>

<span data-ttu-id="e59f7-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="e59f7-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e59f7-111">Выполнение анимации могут также инициироваться с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e59f7-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="e59f7-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="e59f7-112">Steps</span></span>

<span data-ttu-id="e59f7-113">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="e59f7-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="e59f7-114">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e59f7-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="e59f7-115">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="e59f7-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="e59f7-116">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="e59f7-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="e59f7-117">В рамках `<Animations>` узла, используйте `<OnClick>` для запуска анимации один раз пользователь нажимает кнопку на панели.</span><span class="sxs-lookup"><span data-stu-id="e59f7-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="e59f7-118">Добавьте две анимации, выполняемый в параллельном режиме:</span><span class="sxs-lookup"><span data-stu-id="e59f7-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="e59f7-119">Для целей демонстрации этой анимации (и другие анимации, созданные с помощью набора средств элементов управления) выполняется с помощью кода JavaScript, когда страница выполняется.</span><span class="sxs-lookup"><span data-stu-id="e59f7-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="e59f7-120">Во-первых, нам нужен доступ к `AnimationExtender` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="e59f7-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="e59f7-121">Библиотека ASP.NET AJAX предоставляет `$find()` функции для выполнения этой задачи:</span><span class="sxs-lookup"><span data-stu-id="e59f7-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="e59f7-122">`AnimationExtender` Элемент управления предоставляет Интерфейс с широкими возможностями, включая методы с именами, идентичными обработчики событий, используемые в XML-разметку: `OnClick()`, `OnLoad()`, и т. д.</span><span class="sxs-lookup"><span data-stu-id="e59f7-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="e59f7-123">Например, вызов `OnClick()` анимации в выполнении метода `<OnClick>` элемент `AnimationExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="e59f7-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="e59f7-124">Ниже приведен полный код клиентского JavaScript, который эмулирует щелкните на панели после полной загрузки страницы Обратите внимание, что `pageLoad()` вызываемый ASP.NET AJAX один раз страницы используется имя функции и все включены библиотеки были JavaScript загрузить.</span><span class="sxs-lookup"><span data-stu-id="e59f7-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]


<span data-ttu-id="e59f7-125">[![Анимация запускается немедленно, без щелчка мыши](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e59f7-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="e59f7-126">Анимация запускается немедленно, без щелчка мышью ([Просмотр полноразмерного изображения](executing-animations-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e59f7-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e59f7-127">[Назад](modifying-animations-from-the-server-side-cs.md)
> [Вперед](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e59f7-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>
