---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Динамические и Строго типизированные представления | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702950"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="aeb0c-103">Динамические и</span><span class="sxs-lookup"><span data-stu-id="aeb0c-103">Dynamic v.</span></span> <span data-ttu-id="aeb0c-104">строго типизированные представления</span><span class="sxs-lookup"><span data-stu-id="aeb0c-104">Strongly Typed Views</span></span>

<span data-ttu-id="aeb0c-105">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="aeb0c-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="aeb0c-106">Существует три способа передачи информации из контроллера в представление в ASP.NET MVC 3:</span><span class="sxs-lookup"><span data-stu-id="aeb0c-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="aeb0c-107">Как объект модели со строгой типизацией.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="aeb0c-108">Как динамический тип (с использованием @model dynamic)</span><span class="sxs-lookup"><span data-stu-id="aeb0c-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="aeb0c-109">Использование ViewBag</span><span class="sxs-lookup"><span data-stu-id="aeb0c-109">Using the ViewBag</span></span>

<span data-ttu-id="aeb0c-110">Я написал простое приложение блогов MVC третьего уровня для сравнения динамических и строго типизированных представлений.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="aeb0c-111">Контроллер начинается с простого списка блогов:</span><span class="sxs-lookup"><span data-stu-id="aeb0c-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="aeb0c-112">Щелкните правой кнопкой мыши метод Индекснотстонглитипед () и добавьте представление Razor.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="aeb0c-113">[![8475. Нотстронглитипедвиев [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="aeb0c-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="aeb0c-114">Убедитесь, что флажок **создать строго типизированное представление** не установлен.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="aeb0c-115">Результирующее представление не содержит много:</span><span class="sxs-lookup"><span data-stu-id="aeb0c-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="aeb0c-116">Так как мы используем динамическое, а не строго типизированное представление, IntelliSense не помогает нам.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="aeb0c-117">Завершенный код показан ниже:</span><span class="sxs-lookup"><span data-stu-id="aeb0c-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="aeb0c-118">[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="aeb0c-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="aeb0c-119">Теперь мы добавим строго типизированное представление.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="aeb0c-120">Добавьте следующий код в контроллер:</span><span class="sxs-lookup"><span data-stu-id="aeb0c-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="aeb0c-121">Обратите внимание, что это точно такое же возвращаемое представление (Топблогс); Вызовите метод как нестрого типизированное представление.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="aeb0c-122">Щелкните правой кнопкой мыши внутри *стонглитипединдекс ()* и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="aeb0c-123">На этот раз выберите класс модель **блога** и выберите **список** в качестве шаблона шаблонов.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="aeb0c-124">[![5658. Стронгвиев [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="aeb0c-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="aeb0c-125">В новом шаблоне представления мы получаем поддержку IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="aeb0c-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="aeb0c-126">[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="aeb0c-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>
