---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: Часть 6. Создание контроллеров продуктов и заказов | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: 21cfbd0bf691ea033e9a5a873ab49c83507750d5
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425968"
---
<a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="6ea2c-102">Часть 6. Создание контроллеров продуктов и заказов</span><span class="sxs-lookup"><span data-stu-id="6ea2c-102">Part 6: Creating Product and Order Controllers</span></span>
====================
<span data-ttu-id="6ea2c-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6ea2c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6ea2c-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="6ea2c-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="6ea2c-105">Добавить контроллер продуктов</span><span class="sxs-lookup"><span data-stu-id="6ea2c-105">Add a Products Controller</span></span>

<span data-ttu-id="6ea2c-106">Контроллера администрирования является для пользователей с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="6ea2c-107">Клиенты, с другой стороны, можно Просмотр продуктов, но нельзя создать, обновить или удалить их.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="6ea2c-108">Мы можно легко ограничить доступ к методам Post, Put и Delete, не закрывая методы Get.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="6ea2c-109">Но посмотрите на данные, возвращаемые для продукта:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="6ea2c-110">`ActualCost` Свойства не должны быть видимыми для клиентов!</span><span class="sxs-lookup"><span data-stu-id="6ea2c-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="6ea2c-111">Решением является определение *объект передачи данных* (DTO), которая включает подмножество свойств, которые должны отображаться для клиентов.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="6ea2c-112">Мы будем использовать LINQ для проекта `Product` экземпляры `ProductDTO` экземпляров.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="6ea2c-113">Добавьте класс с именем `ProductDTO` папке «модели».</span><span class="sxs-lookup"><span data-stu-id="6ea2c-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="6ea2c-114">Теперь добавьте контроллер.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-114">Now add the controller.</span></span> <span data-ttu-id="6ea2c-115">В обозревателе решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6ea2c-116">Выберите **добавить**, а затем выберите **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="6ea2c-117">В **Добавление контроллера** диалоговое окно, назовите контроллер &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="6ea2c-118">В разделе **шаблона**выберите **контроллер пустой API**.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="6ea2c-119">Замените весь код в исходном файле следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="6ea2c-120">Контроллер по-прежнему использует `OrdersContext` для запроса к базе данных.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="6ea2c-121">Но вместо возвращения `Product` экземпляры напрямую, мы называем `MapProducts` проецировать их на `ProductDTO` экземпляров:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="6ea2c-122">`MapProducts` Возвращает **IQueryable**, поэтому составляется результат с другими параметрами запроса.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="6ea2c-123">Это можно увидеть в `GetProduct` метод, который добавляет **где** к запросу выражение WHERE:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="6ea2c-124">Добавить контроллер заказов</span><span class="sxs-lookup"><span data-stu-id="6ea2c-124">Add an Orders Controller</span></span>

<span data-ttu-id="6ea2c-125">Добавьте контроллер, который позволяет пользователям создавать и просматривать заказы.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="6ea2c-126">Мы начнем с другой DTO.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-126">We'll start with another DTO.</span></span> <span data-ttu-id="6ea2c-127">В обозревателе решений щелкните правой кнопкой мыши папку Models и добавьте класс с именем `OrderDTO` использовать следующую реализацию:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="6ea2c-128">Теперь добавьте контроллер.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-128">Now add the controller.</span></span> <span data-ttu-id="6ea2c-129">В обозревателе решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6ea2c-130">Выберите **добавить**, а затем выберите **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="6ea2c-131">В **Добавление контроллера** диалоговое окно, задайте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="6ea2c-132">В разделе **имя контроллера**, введите «Orderscontroller, который».</span><span class="sxs-lookup"><span data-stu-id="6ea2c-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="6ea2c-133">В разделе **шаблона**, выберите «Контроллер API с действиями чтения и записи, с помощью Entity Framework».</span><span class="sxs-lookup"><span data-stu-id="6ea2c-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="6ea2c-134">В разделе **класс модели**выберите &quot;порядке (ProductStore.Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="6ea2c-135">В разделе **класс контекста данных**выберите &quot;OrdersContext (ProductStore.Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="6ea2c-136">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-136">Click **Add**.</span></span> <span data-ttu-id="6ea2c-137">Добавляется файл с именем OrdersController.cs.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="6ea2c-138">Далее нам нужно изменить реализацию контроллера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="6ea2c-139">Сначала удалите `PutOrder` и `DeleteOrder` методы.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="6ea2c-140">В этом примере клиенты нельзя изменить или удалить существующие заказы.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="6ea2c-141">В реальном приложении вам потребуется логика серверной части для обработки таких случаев.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="6ea2c-142">(Например, порядок уже отправлен?)</span><span class="sxs-lookup"><span data-stu-id="6ea2c-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="6ea2c-143">Изменение `GetOrders` метод для возврата только заказы, принадлежащие пользователю:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="6ea2c-144">Изменение `GetOrder` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="6ea2c-145">Ниже перечислены изменения, которые мы внесли в метод.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="6ea2c-146">Возвращает значение `OrderDTO` экземпляра, а не `Order`.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="6ea2c-147">Когда мы запросим базы данных для заказа, мы используем [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) метод для получения связанных `OrderDetail` и `Product` сущностей.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="6ea2c-148">Мы преобразовать результат с помощью проекции.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="6ea2c-149">HTTP-ответа будет содержать массив продуктов с количества:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="6ea2c-150">Этот формат не облегчает клиентам использовать, чем исходный объект графа, который содержит вложенные сущности (порядок, подробности и продуктах).</span><span class="sxs-lookup"><span data-stu-id="6ea2c-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="6ea2c-151">Последний метод рассматривать ее `PostOrder`.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="6ea2c-152">Прямо сейчас, этот метод принимает `Order` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="6ea2c-153">Но что произойдет, если клиент отправляет текст запроса следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="6ea2c-154">Это хорошо структурированный заказ, и платформа Entity Framework к счастью вставит его в базу данных.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="6ea2c-155">Но он содержит сущности Product, которая раньше не было.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="6ea2c-156">Клиент только что создали новый продукт в базе данных!</span><span class="sxs-lookup"><span data-stu-id="6ea2c-156">The client just created a new product in our database!</span></span> <span data-ttu-id="6ea2c-157">Это будет предусмотрена отдел исполнения заказов, при просмотре заказ koala медведей.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="6ea2c-158">Мораль, необходимо быть очень внимательным, о данных, которые вы принимаете в запросе POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="6ea2c-159">Чтобы избежать этой проблемы, измените `PostOrder` метод, чтобы использовать `OrderDTO` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="6ea2c-160">Используйте `OrderDTO` для создания `Order`.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="6ea2c-161">Обратите внимание, что мы используем `ProductID` и `Quantity` свойства и мы игнорировать любые значения, которые клиент отправил название продукта и цену.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="6ea2c-162">Если код продукта не является допустимым, он будет нарушать ограничение внешнего ключа в базе данных и вставки завершится ошибкой, как должно.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="6ea2c-163">Ниже приведен полный `PostOrder` метод:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="6ea2c-164">Наконец, добавьте **Authorize** атрибута к контроллеру:</span><span class="sxs-lookup"><span data-stu-id="6ea2c-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="6ea2c-165">Теперь только зарегистрированные пользователи могут создавать или Просмотр заказов.</span><span class="sxs-lookup"><span data-stu-id="6ea2c-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6ea2c-166">[Назад](using-web-api-with-entity-framework-part-5.md)
> [Вперед](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="6ea2c-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
