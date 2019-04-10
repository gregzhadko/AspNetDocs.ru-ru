---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Создание действия (C#) | Документация Майкрософт
author: microsoft
description: Узнайте, как добавить новое действие контроллера ASP.NET MVC. Дополнительные сведения о требованиях для метода для действия.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: c66e066bd3e241e667924dacc114f57151df822a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59389561"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="127aa-104">Создание действия (C#)</span><span class="sxs-lookup"><span data-stu-id="127aa-104">Creating an Action (C#)</span></span>

<span data-ttu-id="127aa-105">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="127aa-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="127aa-106">Узнайте, как добавить новое действие контроллера ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="127aa-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="127aa-107">Дополнительные сведения о требованиях для метода для действия.</span><span class="sxs-lookup"><span data-stu-id="127aa-107">Learn about the requirements for a method to be an action.</span></span>


<span data-ttu-id="127aa-108">Чтобы объяснить, как можно создать новое действие контроллера является целью данного учебника.</span><span class="sxs-lookup"><span data-stu-id="127aa-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="127aa-109">Дополнительные сведения о требованиях к методу действия.</span><span class="sxs-lookup"><span data-stu-id="127aa-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="127aa-110">Вы также узнаете, как предотвратить раскрытие как действие метода.</span><span class="sxs-lookup"><span data-stu-id="127aa-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="127aa-111">Добавление действия к контроллеру</span><span class="sxs-lookup"><span data-stu-id="127aa-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="127aa-112">Добавьте новое действие к контроллеру, добавив новый метод к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="127aa-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="127aa-113">Например контроллер в листинге 1 содержит действия с именем Index() и действие с именем SayHello().</span><span class="sxs-lookup"><span data-stu-id="127aa-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="127aa-114">Оба метода доступны как действия.</span><span class="sxs-lookup"><span data-stu-id="127aa-114">Both methods are exposed as actions.</span></span>

**<span data-ttu-id="127aa-115">Listing 1 - Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="127aa-115">Listing 1 - Controllers\HomeController.cs</span></span>**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="127aa-116">Чтобы предоставить вселенной как действие, метод должны соответствовать определенным требованиям:</span><span class="sxs-lookup"><span data-stu-id="127aa-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="127aa-117">Метод должен быть открытым.</span><span class="sxs-lookup"><span data-stu-id="127aa-117">The method must be public.</span></span>
- <span data-ttu-id="127aa-118">Метод не может быть статический метод.</span><span class="sxs-lookup"><span data-stu-id="127aa-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="127aa-119">Метод не может быть методом расширения.</span><span class="sxs-lookup"><span data-stu-id="127aa-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="127aa-120">Метод не может быть конструктор, метод получения или задания.</span><span class="sxs-lookup"><span data-stu-id="127aa-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="127aa-121">Метод не может иметь открытые универсальные типы.</span><span class="sxs-lookup"><span data-stu-id="127aa-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="127aa-122">Метод не является методом базового класса контроллера.</span><span class="sxs-lookup"><span data-stu-id="127aa-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="127aa-123">Этот метод не может содержать **ref** или **out** параметров.</span><span class="sxs-lookup"><span data-stu-id="127aa-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="127aa-124">Обратите внимание на то, что не существует ограничений на тип возвращаемого значения действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="127aa-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="127aa-125">Действие контроллера может вернуть строку, DateTime, экземпляр класса Random, или void.</span><span class="sxs-lookup"><span data-stu-id="127aa-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="127aa-126">Платформа ASP.NET MVC преобразует любой возвращаемый тип, который не является результат действия в строку и просмотру строки в браузере.</span><span class="sxs-lookup"><span data-stu-id="127aa-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="127aa-127">При добавлении любого метода, который не нарушает эти требования к контроллеру, метод указывается в виде действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="127aa-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="127aa-128">Следите за здесь.</span><span class="sxs-lookup"><span data-stu-id="127aa-128">Be careful here.</span></span> <span data-ttu-id="127aa-129">Действие контроллера может вызываться кем-либо подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="127aa-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="127aa-130">Не так, например, создать действие контроллера DeleteMyWebsite().</span><span class="sxs-lookup"><span data-stu-id="127aa-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="127aa-131">Предотвращение вызов открытого метода</span><span class="sxs-lookup"><span data-stu-id="127aa-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="127aa-132">Если вам нужно создать открытый метод в класс контроллера, и вы не хотите предоставлять метод как действие контроллера можно предотвратить метода вызова модуля с помощью атрибута [NonAction].</span><span class="sxs-lookup"><span data-stu-id="127aa-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="127aa-133">Например контроллер в листинге 2 содержит открытый метод с именем CompanySecrets(), дополнен атрибутом [NonAction].</span><span class="sxs-lookup"><span data-stu-id="127aa-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

**<span data-ttu-id="127aa-134">В листинге 2 - Controllers\WorkController.cs</span><span class="sxs-lookup"><span data-stu-id="127aa-134">Listing 2 - Controllers\WorkController.cs</span></span>**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="127aa-135">При попытке вызвать действие контроллера CompanySecrets(), введя в адресной строке браузера /Work/CompanySecrets затем вы получите сообщение об ошибке на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="127aa-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>


[![I<span data-ttu-id="127aa-136">nvoking метод NonAction]</span><span class="sxs-lookup"><span data-stu-id="127aa-136">nvoking a NonAction method]</span></span>(creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

<span data-ttu-id="127aa-137">**Рис 01**: Вызов метода NonAction ([Просмотр полноразмерного изображения](creating-an-action-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="127aa-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="127aa-138">[Назад](creating-a-controller-cs.md)
> [Вперед](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="127aa-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
