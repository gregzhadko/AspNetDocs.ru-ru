---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Создание пользовательских маршрутов (СЗ) Документы Майкрософт
author: rick-anderson
description: Узнайте, как добавить пользовательские маршруты в приложение ASP.NET MVC. В этом уроке вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542759"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="d9357-104">Создание пользовательских маршрутов (C#)</span><span class="sxs-lookup"><span data-stu-id="d9357-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="d9357-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d9357-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d9357-106">Узнайте, как добавить пользовательские маршруты в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d9357-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="d9357-107">В этом уроке вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global.asax.</span><span class="sxs-lookup"><span data-stu-id="d9357-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="d9357-108">В этом уроке вы узнаете, как добавить пользовательский маршрут к ASP.NET mVC-приложению.</span><span class="sxs-lookup"><span data-stu-id="d9357-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="d9357-109">Вы узнаете, как изменить таблицу маршрута по умолчанию в файле Global.asax с помощью пользовательского маршрута.</span><span class="sxs-lookup"><span data-stu-id="d9357-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="d9357-110">Для многих простых ASP.NET mVC-приложений таблица маршрутов по умолчанию будет работать нормально.</span><span class="sxs-lookup"><span data-stu-id="d9357-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="d9357-111">Тем не менее, вы можете обнаружить, что у вас есть специализированные потребности в реукторе.</span><span class="sxs-lookup"><span data-stu-id="d9357-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="d9357-112">В этом случае можно создать пользовательский маршрут.</span><span class="sxs-lookup"><span data-stu-id="d9357-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="d9357-113">Представьте себе, например, что вы строите приложение для блога.</span><span class="sxs-lookup"><span data-stu-id="d9357-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="d9357-114">Вы можете обрабатывать входящие запросы, которые выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d9357-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="d9357-115">/Архив/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="d9357-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="d9357-116">Когда пользователь вводит этот запрос, вы хотите вернуть запись в блоге, которая соответствует дате 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="d9357-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="d9357-117">Для обработки такого типа запроса необходимо создать пользовательский маршрут.</span><span class="sxs-lookup"><span data-stu-id="d9357-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="d9357-118">Файл Global.asax в листинге 1 содержит новый пользовательский маршрут под названием Блог, который обрабатывает запросы, которые выглядят как /Archive/*Дата входа.*</span><span class="sxs-lookup"><span data-stu-id="d9357-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="d9357-119">**Список 1 - Global.asax (с пользовательским маршрутом)**</span><span class="sxs-lookup"><span data-stu-id="d9357-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="d9357-120">Важно ею является порядок маршрутов, которые вы добавляете в таблицу маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d9357-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="d9357-121">Наш новый пользовательский маршрут блог добавляется до существующего маршрута по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d9357-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="d9357-122">Если вы отменили заказ, то маршрут по умолчанию всегда будет вызываться вместо пользовательского маршрута.</span><span class="sxs-lookup"><span data-stu-id="d9357-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="d9357-123">Пользовательский маршрут блога соответствует любому запросу, который начинается с /Archive/.</span><span class="sxs-lookup"><span data-stu-id="d9357-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="d9357-124">Таким образом, он соответствует всем следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="d9357-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="d9357-125">/Архив/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="d9357-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="d9357-126">/Архив/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="d9357-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="d9357-127">/Архив/яблоко</span><span class="sxs-lookup"><span data-stu-id="d9357-127">/Archive/apple</span></span>

<span data-ttu-id="d9357-128">Пользовательский маршрут отображает входящий запрос контроллеру под названием Archive и вызывает действие Входа ()</span><span class="sxs-lookup"><span data-stu-id="d9357-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="d9357-129">При вызове метода входа () дата входа передается как параметр, названный entryDate.</span><span class="sxs-lookup"><span data-stu-id="d9357-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="d9357-130">Вы можете использовать блог пользовательский маршрут с контроллером в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="d9357-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="d9357-131">**Список 2 - ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="d9357-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="d9357-132">Обратите внимание, что метод входа () в листинге 2 принимает параметр типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="d9357-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="d9357-133">Платформа MVC достаточно умна, чтобы автоматически преобразовать дату входа из URL в значение DateTime.</span><span class="sxs-lookup"><span data-stu-id="d9357-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="d9357-134">Если параметр даты входа из URL не может быть преобразован в DateTime, возникает ошибка (см. рисунок 1).</span><span class="sxs-lookup"><span data-stu-id="d9357-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="d9357-135">**Рисунок 1 - Ошибка от преобразования параметра**</span><span class="sxs-lookup"><span data-stu-id="d9357-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="d9357-136">[![Диалоговое окно New Project (Новый проект)](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d9357-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="d9357-137">**Рисунок 01**: Ошибка от преобразования параметра ([Нажмите, чтобы просмотреть полноразмерное изображение](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d9357-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="d9357-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="d9357-138">Summary</span></span>

<span data-ttu-id="d9357-139">Цель этого учебника состояла в том, чтобы продемонстрировать, как вы можете создать пользовательский маршрут.</span><span class="sxs-lookup"><span data-stu-id="d9357-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="d9357-140">Вы узнали, как добавить пользовательский маршрут к таблице маршрутов в файле Global.asax, который представляет записи в блоге.</span><span class="sxs-lookup"><span data-stu-id="d9357-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="d9357-141">Мы обсудили, как сопоставить запросы на записи в блоге на контроллер под названием ArchiveController и действие контроллера под названием Entry().</span><span class="sxs-lookup"><span data-stu-id="d9357-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d9357-142">[Назад](aspnet-mvc-controllers-overview-cs.md)
> [Вперед](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d9357-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
