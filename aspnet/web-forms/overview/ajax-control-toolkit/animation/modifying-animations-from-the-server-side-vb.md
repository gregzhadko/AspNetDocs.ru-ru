---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Изменение анимации со стороны сервера (Visual Basic) | Документация Майкрософт
author: wenz
description: Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления. Анимации могут также...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: fb7e992246b9c630d99a1493f344c4089540d67e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59398089"
---
# <a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="38fc5-104">Изменение анимации со стороны сервера (VB)</span><span class="sxs-lookup"><span data-stu-id="38fc5-104">Modifying Animations From The Server Side (VB)</span></span>

<span data-ttu-id="38fc5-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="38fc5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="38fc5-106">[Скачать код](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) или [скачать PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="38fc5-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="38fc5-107">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="38fc5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="38fc5-108">Также может измениться анимации на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="38fc5-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="38fc5-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="38fc5-109">Overview</span></span>

<span data-ttu-id="38fc5-110">Отображается этот элемент управления в ASP.NET AJAX Control Toolkit не только элемент управления, но всю платформу для добавления анимации в элемент управления.</span><span class="sxs-lookup"><span data-stu-id="38fc5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="38fc5-111">Также может измениться анимации на стороне сервера</span><span class="sxs-lookup"><span data-stu-id="38fc5-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="38fc5-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="38fc5-112">Steps</span></span>

<span data-ttu-id="38fc5-113">Во-первых, включите `ScriptManager` страницы; затем ASP.NET AJAX library загружена, что позволяет использовать набор средств управления:</span><span class="sxs-lookup"><span data-stu-id="38fc5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="38fc5-114">Анимация будет применяться к панели текста, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="38fc5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="38fc5-115">В связанный класс CSS для панели определить цвет фона, удобная и также установить фиксированную ширину для панели:</span><span class="sxs-lookup"><span data-stu-id="38fc5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="38fc5-116">Остальная часть кода выполняется на стороне сервера и не использует разметки; Вместо этого он использует код для создания `AnimationExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="38fc5-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="38fc5-117">Тем не менее набор элементов управления в настоящее время не предоставляет доступ к API для создания отдельных анимаций.</span><span class="sxs-lookup"><span data-stu-id="38fc5-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="38fc5-118">Тем не менее можно задать `AnimationExtender`свойство Animations в строку содержащего XML-разметку, при назначении анимации декларативно.</span><span class="sxs-lookup"><span data-stu-id="38fc5-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="38fc5-119">Чтобы создать XML, который не может содержать `<Animations>` элемент, можно использовать XML платформы .NET Framework поддерживает или, как в следующем коде, просто укажите строку:</span><span class="sxs-lookup"><span data-stu-id="38fc5-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="38fc5-120">Наконец, добавьте `AnimationExtender` управления в текущую страницу в `<form runat="server">` элемент, убедившись, что анимация включена и выполняется:</span><span class="sxs-lookup"><span data-stu-id="38fc5-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


<span data-ttu-id="38fc5-121">[![Анимация создается с использованием серверного C# и Visual Basic кода](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="38fc5-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="38fc5-122">Анимация создается с использованием серверного C# и Visual Basic кода ([Просмотр полноразмерного изображения](modifying-animations-from-the-server-side-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="38fc5-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="38fc5-123">[Назад](triggering-an-animation-in-another-control-vb.md)
> [Вперед](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="38fc5-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
