---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: Разрешение только некоторых символов в текстовом поле (Visual Basic) | Документация Майкрософт
author: wenz
description: Проверяющие элементы управления ASP.NET гарантирует, что вводимые пользователем данные разрешены только некоторых символов. Тем не менее это по-прежнему не позволяет пользователям вводить недопустимые...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0f13140fcafd666a89c27acb829e4e762eff29
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127449"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="f744b-104">Разрешение только некоторых символов в текстовом поле (VB)</span><span class="sxs-lookup"><span data-stu-id="f744b-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>

<span data-ttu-id="f744b-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f744b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f744b-106">[Скачать код](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f744b-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="f744b-107">Проверяющие элементы управления ASP.NET гарантирует, что вводимые пользователем данные разрешены только некоторых символов.</span><span class="sxs-lookup"><span data-stu-id="f744b-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="f744b-108">Тем не менее это по-прежнему не запрещает пользователям вводить недопустимые символы и при попытке отправить форму.</span><span class="sxs-lookup"><span data-stu-id="f744b-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="f744b-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="f744b-109">Overview</span></span>

<span data-ttu-id="f744b-110">Проверяющие элементы управления ASP.NET гарантирует, что вводимые пользователем данные разрешены только некоторых символов.</span><span class="sxs-lookup"><span data-stu-id="f744b-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="f744b-111">Тем не менее это по-прежнему не запрещает пользователям вводить недопустимые символы и при попытке отправить форму.</span><span class="sxs-lookup"><span data-stu-id="f744b-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="f744b-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="f744b-112">Steps</span></span>

<span data-ttu-id="f744b-113">ASP.NET AJAX Control Toolkit содержит `FilteredTextBox` элемента управления, который расширяет текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f744b-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="f744b-114">После активации, можно вводить только определенный набор символов в поле.</span><span class="sxs-lookup"><span data-stu-id="f744b-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="f744b-115">Чтобы это работало, необходимо сначала обычным образом ASP.NET AJAX `ScriptManager` которого загружала библиотеки JavaScript, которые также используется ASP.NET AJAX Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="f744b-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="f744b-116">Затем нам нужно текстового поля:</span><span class="sxs-lookup"><span data-stu-id="f744b-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="f744b-117">Наконец `FilteredTextBoxExtender` берет на себя ограничение символов, пользователь может ввести элемент управления.</span><span class="sxs-lookup"><span data-stu-id="f744b-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="f744b-118">Сначала задайте `TargetControlID` атрибут `ID` из `TextBox` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="f744b-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="f744b-119">Выберите один из доступных `FilterType` значений:</span><span class="sxs-lookup"><span data-stu-id="f744b-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="f744b-120">`Custom` по умолчанию; Вы должны предоставить список допустимых знаков</span><span class="sxs-lookup"><span data-stu-id="f744b-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="f744b-121">`LowercaseLetters` только строчные буквы</span><span class="sxs-lookup"><span data-stu-id="f744b-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="f744b-122">`Numbers` только цифры</span><span class="sxs-lookup"><span data-stu-id="f744b-122">`Numbers` digits only</span></span>
- <span data-ttu-id="f744b-123">`UppercaseLetters` только прописные буквы</span><span class="sxs-lookup"><span data-stu-id="f744b-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="f744b-124">Если `Custom FilterType` используется, `ValidChars` свойство должно быть задано и укажите список символов, которые может ввести.</span><span class="sxs-lookup"><span data-stu-id="f744b-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="f744b-125">Между прочим: при попытке вставить текст в текстовое поле, будут удалены все недопустимые символы.</span><span class="sxs-lookup"><span data-stu-id="f744b-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="f744b-126">Далее приведена разметка для `FilteredTextBoxExtender` элемент управления, который допускает только цифры (то, что также было бы возможным с `FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="f744b-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="f744b-127">Запустите страницу и попробуйте ввести буквы в том случае, если включить JavaScript, он не будет работать; Тем не менее, на странице отображаются цифры.</span><span class="sxs-lookup"><span data-stu-id="f744b-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="f744b-128">Тем не менее Обратите внимание, что защита `FilteredTextBox` предоставляет не пуленепробиваема: Если включен JavaScript, любые данные можно вводить в текстовом поле, поэтому необходимо использовать средства дополнительной проверки, т. е. ASP. NET-элементов управления проверки.</span><span class="sxs-lookup"><span data-stu-id="f744b-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="f744b-129">[![Можно вводить только цифры](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f744b-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="f744b-130">Можно вводить только цифры ([Просмотр полноразмерного изображения](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f744b-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f744b-131">Назад</span><span class="sxs-lookup"><span data-stu-id="f744b-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)
