---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Изменение анимаций с помощью клиентского кода (C#) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Можно также анимации...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bdee58aa04e1c8217c2a727b96aa8b239fe1aca
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395612"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="dd37b-104">Изменение анимаций с помощью клиентского кода (C#)</span><span class="sxs-lookup"><span data-stu-id="dd37b-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="dd37b-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="dd37b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="dd37b-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="dd37b-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="dd37b-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="dd37b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dd37b-108">Также можно изменить анимации с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="dd37b-108">The animation can also be changed using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="dd37b-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="dd37b-109">Overview</span></span>

<span data-ttu-id="dd37b-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="dd37b-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dd37b-111">Также можно изменить анимации с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="dd37b-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="dd37b-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="dd37b-112">Steps</span></span>

<span data-ttu-id="dd37b-113">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="dd37b-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="dd37b-114">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dd37b-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="dd37b-115">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="dd37b-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="dd37b-116">Фактический анимация запускается с HTML-кнопок:</span><span class="sxs-lookup"><span data-stu-id="dd37b-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="dd37b-117">Затем добавьте `AnimationExtender` на страницу, предоставляя `ID`, `TargetControlID` атрибут и обязательным `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="dd37b-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="dd37b-118">Следует отметить, что не `<Animations>` узел в `AnimationExtender` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="dd37b-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="dd37b-119">Пользовательский код JavaScript используется для предоставления анимации для использования с элементом управления.</span><span class="sxs-lookup"><span data-stu-id="dd37b-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="dd37b-120">Как и в API сервера из `AnimationExtender`, нет простого способа еще назначить анимации расширителя.</span><span class="sxs-lookup"><span data-stu-id="dd37b-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="dd37b-121">Тем не менее расширителя предоставляют несколько методов для чтения и записи анимации зарегистрировано различные события (`OnClick`, `OnLoad`, и так далее).</span><span class="sxs-lookup"><span data-stu-id="dd37b-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="dd37b-122">Далее приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="dd37b-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="dd37b-123">Формат возвращаемого значения `get_*()` функции и формат аргумента для `set_*()` функции представляет собой строку JSON, предоставляя объектное представление XML-разметку, которые бы.</span><span class="sxs-lookup"><span data-stu-id="dd37b-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="dd37b-124">В настоящее время невозможно передать объект в, но можно считать объект из данной анимации (`get_OnXXXBehavior()` методов).</span><span class="sxs-lookup"><span data-stu-id="dd37b-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="dd37b-125">Здесь представляет собой строку JSON (без кавычек разделителя и форматировать хорошо) представляющий анимацию, инициируемой этой кнопкой, но анимации на панели, изменяя его размер и исчезновение в то же время:</span><span class="sxs-lookup"><span data-stu-id="dd37b-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="dd37b-126">Следующий код JavaScript назначает этот descripting JSON для `OnClick` анимации текущего расширителя и запускает его:</span><span class="sxs-lookup"><span data-stu-id="dd37b-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]


<span data-ttu-id="dd37b-127">[![Анимация запускается немедленно, без щелчка мыши (и с очень небольшой разметкой)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dd37b-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="dd37b-128">Анимация запускается немедленно, без щелчка мышью (и с очень небольшой разметкой) ([Просмотр полноразмерного изображения](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="dd37b-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dd37b-129">[Назад](executing-animations-using-client-side-code-cs.md)
> [Вперед](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="dd37b-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
