---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Создание ограничения маршрута (Visual Basic) | Документация Майкрософт
author: StephenWalther
description: В этом руководстве Стивен Вальтер демонстрирует, как можно контролировать, как браузер запрашивает маршруты соответствия путем создания ограничения маршрута с помощью регулярных выражений.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 0a8e540a00d852d5b710bfdbf63a68f6e6d280ee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032191"
---
<a name="creating-a-route-constraint-vb"></a><span data-ttu-id="98079-103">Создание ограничения маршрута (VB)</span><span class="sxs-lookup"><span data-stu-id="98079-103">Creating a Route Constraint (VB)</span></span>
====================
<span data-ttu-id="98079-104">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="98079-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="98079-105">В этом руководстве Стивен Вальтер демонстрирует, как можно контролировать, как браузер запрашивает маршруты соответствия путем создания ограничения маршрута с помощью регулярных выражений.</span><span class="sxs-lookup"><span data-stu-id="98079-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>


<span data-ttu-id="98079-106">Использовать ограничения маршрута для ограничения браузер запросы, которые соответствуют определенным маршрутом.</span><span class="sxs-lookup"><span data-stu-id="98079-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="98079-107">Регулярное выражение можно использовать для указания ограничения маршрута.</span><span class="sxs-lookup"><span data-stu-id="98079-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="98079-108">Например представьте, что вы определили маршрута в листинге 1 в файле Global.asax.</span><span class="sxs-lookup"><span data-stu-id="98079-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="98079-109">**В листинге 1 - Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="98079-109">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="98079-110">В листинге 1 содержит маршрут с именем продукта.</span><span class="sxs-lookup"><span data-stu-id="98079-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="98079-111">Маршрут продукта можно использовать для сопоставления запросов браузера ProductController, содержащихся в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="98079-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="98079-112">**В листинге 2 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="98079-112">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="98079-113">Обратите внимание на то, что Details() действию, предоставляемым продукта контроллер принимает один параметр с именем productId.</span><span class="sxs-lookup"><span data-stu-id="98079-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="98079-114">Этот параметр является параметром целое число.</span><span class="sxs-lookup"><span data-stu-id="98079-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="98079-115">Маршрут, определенный в листинге 1 будет соответствовать любой из следующих URL-адресов:</span><span class="sxs-lookup"><span data-stu-id="98079-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="98079-116">/ Продукта/23</span><span class="sxs-lookup"><span data-stu-id="98079-116">/Product/23</span></span>
- <span data-ttu-id="98079-117">/ Продукта/7</span><span class="sxs-lookup"><span data-stu-id="98079-117">/Product/7</span></span>

<span data-ttu-id="98079-118">К сожалению маршрут будет соответствовать следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="98079-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="98079-119">/ Продукта/сведения</span><span class="sxs-lookup"><span data-stu-id="98079-119">/Product/blah</span></span>
- <span data-ttu-id="98079-120">/ Продукта/apple</span><span class="sxs-lookup"><span data-stu-id="98079-120">/Product/apple</span></span>

<span data-ttu-id="98079-121">Поскольку действие Details() ожидает целочисленный параметр, выполняющего запрос, содержащий отличные от целочисленное значение приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="98079-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="98079-122">Например при вводе /Product/apple URL-адрес в адресную строку браузера на страницу ошибки будет получить на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="98079-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>


<span data-ttu-id="98079-123">[![В диалоговом окне нового проекта](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="98079-123">[![The New Project dialog box](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span></span>

<span data-ttu-id="98079-124">**Рис 01**: Просмотр страницы развернуть ([Просмотр полноразмерного изображения](creating-a-route-constraint-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="98079-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>


<span data-ttu-id="98079-125">Что Вы действительно хотите сделать — соответствовать только URL-адреса, содержащие productId правильное целое число.</span><span class="sxs-lookup"><span data-stu-id="98079-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="98079-126">Ограничение можно использовать при определении маршрута для ограничения URL-адреса, которые соответствуют маршруту.</span><span class="sxs-lookup"><span data-stu-id="98079-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="98079-127">Измененный маршрут продукта в листинге 3 содержит ограничение регулярное выражение, которое соответствует только целые числа.</span><span class="sxs-lookup"><span data-stu-id="98079-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="98079-128">**Листинг 3 - Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="98079-128">**Listing 3 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="98079-129">Регулярное выражение \d+ соответствует один или несколько целых чисел.</span><span class="sxs-lookup"><span data-stu-id="98079-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="98079-130">Этим ограничением обусловлены сопоставления следующие URL-адреса маршрута продукта:</span><span class="sxs-lookup"><span data-stu-id="98079-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="98079-131">/ Продукта/3</span><span class="sxs-lookup"><span data-stu-id="98079-131">/Product/3</span></span>
- <span data-ttu-id="98079-132">/ Продукта/8999</span><span class="sxs-lookup"><span data-stu-id="98079-132">/Product/8999</span></span>

<span data-ttu-id="98079-133">Но не следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="98079-133">But not the following URLs:</span></span>

- <span data-ttu-id="98079-134">/ Продукта/apple</span><span class="sxs-lookup"><span data-stu-id="98079-134">/Product/apple</span></span>
- <span data-ttu-id="98079-135">/ Продукта</span><span class="sxs-lookup"><span data-stu-id="98079-135">/Product</span></span>

<span data-ttu-id="98079-136">Эти запросы браузера будут обрабатываться другой маршрут или, если отсутствуют соответствующие маршруты *не удалось найти ресурс* будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="98079-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="98079-137">[Назад](creating-custom-routes-vb.md)
> [Вперед](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="98079-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>
