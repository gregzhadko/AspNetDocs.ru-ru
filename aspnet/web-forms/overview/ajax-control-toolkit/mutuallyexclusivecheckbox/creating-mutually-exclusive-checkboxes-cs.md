---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: Создание взаимоисключающих флажков (C#) | Документация Майкрософт
author: wenz
description: 'Если можно выбрать только один из наборов параметров, обычно используются переключатели. Однако существует недостаток: один переключатель в группе,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496788"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="64f3d-104">Создание взаимоисключающих флажков (C#)</span><span class="sxs-lookup"><span data-stu-id="64f3d-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>

<span data-ttu-id="64f3d-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="64f3d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="64f3d-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="64f3d-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="64f3d-107">Если можно выбрать только один из наборов параметров, обычно используются переключатели.</span><span class="sxs-lookup"><span data-stu-id="64f3d-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="64f3d-108">Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно.</span><span class="sxs-lookup"><span data-stu-id="64f3d-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="64f3d-109">Флажки в любое время можно снять, но они не являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="64f3d-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="64f3d-110">В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="64f3d-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="64f3d-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="64f3d-111">Overview</span></span>

<span data-ttu-id="64f3d-112">Если можно выбрать только один из наборов параметров, обычно используются переключатели.</span><span class="sxs-lookup"><span data-stu-id="64f3d-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="64f3d-113">Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно.</span><span class="sxs-lookup"><span data-stu-id="64f3d-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="64f3d-114">Флажки в любое время можно снять, но они не являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="64f3d-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="64f3d-115">В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="64f3d-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="64f3d-116">Шаги</span><span class="sxs-lookup"><span data-stu-id="64f3d-116">Steps</span></span>

<span data-ttu-id="64f3d-117">Набор средств управления ASP.NET AJAX содержит расширитель Мутуаллексклусивечеккбокс.</span><span class="sxs-lookup"><span data-stu-id="64f3d-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="64f3d-118">Это позволяет программистам назначать любой флажок имени группы (`Key` атрибут).</span><span class="sxs-lookup"><span data-stu-id="64f3d-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="64f3d-119">Из всех флажков в одной группе можно выбрать только один из них.</span><span class="sxs-lookup"><span data-stu-id="64f3d-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="64f3d-120">Начнем с установки двух флажков на новой странице ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="64f3d-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="64f3d-121">Для демонстрации принципа может быть больше, но два из них достаточно:</span><span class="sxs-lookup"><span data-stu-id="64f3d-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="64f3d-122">Для обоих флажков на странице должен быть размещен элемент управления Мутуаллексклусивечеккбоксекстендер.</span><span class="sxs-lookup"><span data-stu-id="64f3d-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="64f3d-123">Оба ключевых атрибута должны иметь одинаковое значение, так же как атрибуты значений элементов переключателя HTML должны быть идентичны, чтобы обозначить группу, к которой они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="64f3d-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="64f3d-124">Свойство TargetControlID расширителя указывает на идентификатор флажка.</span><span class="sxs-lookup"><span data-stu-id="64f3d-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="64f3d-125">Наконец, включите ASP.NET AJAX `ScriptManager`, необходимый для всех элементов набора средств управления AJAX ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="64f3d-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="64f3d-126">Сохраните и запустите страницу. Вы можете установить флажки и снять флажки, однако в этом случае оба флажка не будут установлены.</span><span class="sxs-lookup"><span data-stu-id="64f3d-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="64f3d-127">[![только один флажок можно проверить за раз](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="64f3d-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="64f3d-128">Только один флажок может быть проверен за раз ([щелкните, чтобы просмотреть изображение с полным размером](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="64f3d-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="64f3d-129">Дальше</span><span class="sxs-lookup"><span data-stu-id="64f3d-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
