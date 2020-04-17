---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Создание действия (C) Документы Майкрософт
author: rick-anderson
description: Узнайте, как добавить новое действие в ASP.NET контроллер MVC. Узнайте о требованиях к методу, который должен быть действием.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542278"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="bff22-104">Создание действия (C#)</span><span class="sxs-lookup"><span data-stu-id="bff22-104">Creating an Action (C#)</span></span>

<span data-ttu-id="bff22-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bff22-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="bff22-106">Узнайте, как добавить новое действие в ASP.NET контроллер MVC.</span><span class="sxs-lookup"><span data-stu-id="bff22-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="bff22-107">Узнайте о требованиях к методу, который должен быть действием.</span><span class="sxs-lookup"><span data-stu-id="bff22-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="bff22-108">Цель этого учебника состоит в том, чтобы объяснить, как вы можете создать новый контроллер действий.</span><span class="sxs-lookup"><span data-stu-id="bff22-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="bff22-109">Вы узнаете о требованиях метода действия.</span><span class="sxs-lookup"><span data-stu-id="bff22-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="bff22-110">Вы также узнаете, как предотвратить метод от разоблачения в качестве действия.</span><span class="sxs-lookup"><span data-stu-id="bff22-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="bff22-111">Добавление действия в контроллер</span><span class="sxs-lookup"><span data-stu-id="bff22-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="bff22-112">Вы добавляете новое действие контроллеру, добавляя новый метод в контроллер.</span><span class="sxs-lookup"><span data-stu-id="bff22-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="bff22-113">Например, контроллер в листинге 1 содержит действие под названием Индекс () и действие под названием SayHello().</span><span class="sxs-lookup"><span data-stu-id="bff22-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="bff22-114">Оба метода разоблачаются как действия.</span><span class="sxs-lookup"><span data-stu-id="bff22-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="bff22-115">**Список 1 - Контролеры**</span><span class="sxs-lookup"><span data-stu-id="bff22-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="bff22-116">Для того, чтобы подвергаться воздействию Вселенной как действия, метод должен соответствовать определенным требованиям:</span><span class="sxs-lookup"><span data-stu-id="bff22-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="bff22-117">Метод должен быть общедоступным.</span><span class="sxs-lookup"><span data-stu-id="bff22-117">The method must be public.</span></span>
- <span data-ttu-id="bff22-118">Метод не может быть статичным методом.</span><span class="sxs-lookup"><span data-stu-id="bff22-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="bff22-119">Метод не может быть методом расширения.</span><span class="sxs-lookup"><span data-stu-id="bff22-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="bff22-120">Метод не может быть конструктором, геттером или сеттером.</span><span class="sxs-lookup"><span data-stu-id="bff22-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="bff22-121">Метод не может иметь открытые типы общего.</span><span class="sxs-lookup"><span data-stu-id="bff22-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="bff22-122">Метод не является методом базового класса контроллера.</span><span class="sxs-lookup"><span data-stu-id="bff22-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="bff22-123">Метод не может содержать параметры **реф** или **из** них.</span><span class="sxs-lookup"><span data-stu-id="bff22-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="bff22-124">Обратите внимание, что нет никаких ограничений на тип возврата действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="bff22-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="bff22-125">Действие контроллера может вернуть строку, DateTime, экземпляр класса Random или пустоту.</span><span class="sxs-lookup"><span data-stu-id="bff22-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="bff22-126">Платформа ASP.NET MVC преобразует любой тип возврата, который не является результатом действия, в строку и внесет строку в браузер.</span><span class="sxs-lookup"><span data-stu-id="bff22-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="bff22-127">При добавлении любого метода, который не нарушает эти требования, в контроллер, метод подвергается действию контроллера.</span><span class="sxs-lookup"><span data-stu-id="bff22-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="bff22-128">Будь осторожен здесь.</span><span class="sxs-lookup"><span data-stu-id="bff22-128">Be careful here.</span></span> <span data-ttu-id="bff22-129">Действия контроллера могут вызываться любым лицом, подключенным к Интернету.</span><span class="sxs-lookup"><span data-stu-id="bff22-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="bff22-130">Не создавайте, например, действия контроллера DeleteMyWebsite()</span><span class="sxs-lookup"><span data-stu-id="bff22-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="bff22-131">Предотвращение вызова общедоступного метода</span><span class="sxs-lookup"><span data-stu-id="bff22-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="bff22-132">Если вам нужно создать общедоступный метод в классе контроллера, и вы не хотите, чтобы разоблачить метод как действие контроллера, то вы можете предотвратить метод от вызова с помощью атрибута «NonAction».</span><span class="sxs-lookup"><span data-stu-id="bff22-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="bff22-133">Например, контроллер в листинге 2 содержит общедоступный метод под названием CompanySecrets(), который украшен атрибутом «NonAction».</span><span class="sxs-lookup"><span data-stu-id="bff22-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="bff22-134">**Список 2 - Контроллеры/WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="bff22-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="bff22-135">Если вы попытаетесь вызвать CompanySecrets () действие контроллера, введя /Work/CompanySecrets в адресную строку вашего браузера, то вы получите сообщение об ошибке на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="bff22-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="bff22-136">[![Ссылаясь на метод NonAction](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bff22-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="bff22-137">**Рисунок 01**: Ссылка на метод NonAction[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-an-action-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="bff22-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bff22-138">[Назад](creating-a-controller-cs.md)
> [Вперед](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="bff22-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
