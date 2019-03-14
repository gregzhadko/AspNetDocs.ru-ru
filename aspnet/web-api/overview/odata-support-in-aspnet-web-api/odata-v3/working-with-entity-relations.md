---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Поддержка отношений сущностей в OData v3 с веб-API 2 | Документация Майкрософт
author: MikeWasson
description: 'В большинстве наборов данных определить отношения между сущностями: Клиенты имеют заказы; у книги может быть авторов; продукты, имеют поставщики. С помощью OData, клиенты могут переходить по...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: f78b5cf36789032f90d3d073698f7a439507277f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028711"
---
<a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="a5cc2-104">Поддержка отношений сущностей в OData v3 с веб-API 2</span><span class="sxs-lookup"><span data-stu-id="a5cc2-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>
====================
<span data-ttu-id="a5cc2-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a5cc2-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a5cc2-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="a5cc2-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="a5cc2-107">В большинстве наборов данных определить отношения между сущностями: Клиенты имеют заказы; у книги может быть авторов; продукты, имеют поставщики.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="a5cc2-108">С помощью OData, клиенты можно переходить через отношения сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="a5cc2-109">Учитывая продукта, можно найти поставщика.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="a5cc2-110">Также можно создать или удалить связи.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-110">You can also create or remove relationships.</span></span> <span data-ttu-id="a5cc2-111">Например можно задать поставщик для продукта.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="a5cc2-112">Этом руководстве показано, как для поддержки этих операций в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="a5cc2-113">Учебном курсе руководство [Создание конечной точки OData v3 с веб-API 2](creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a5cc2-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a5cc2-114">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="a5cc2-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a5cc2-115">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="a5cc2-115">Web API 2</span></span>
> - <span data-ttu-id="a5cc2-116">OData версии 3</span><span class="sxs-lookup"><span data-stu-id="a5cc2-116">OData Version 3</span></span>
> - <span data-ttu-id="a5cc2-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="a5cc2-117">Entity Framework 6</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="a5cc2-118">Добавление сущности Supplier</span><span class="sxs-lookup"><span data-stu-id="a5cc2-118">Add a Supplier Entity</span></span>

<span data-ttu-id="a5cc2-119">Во-первых, нам нужно добавить новый тип сущности для наших веб-канала OData.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="a5cc2-120">Мы добавим `Supplier` класса.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="a5cc2-121">Этот класс использует строку для ключа сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="a5cc2-122">На практике, это может быть реже, чем с помощью целочисленного ключа.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="a5cc2-123">Но стоит видеть, как OData обрабатывает другие типы ключей, помимо целых чисел.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="a5cc2-124">Далее, мы создадим связь путем добавления `Supplier` свойства `Product` класса:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="a5cc2-125">Добавьте новый **DbSet** для `ProductServiceContext` класса, таким образом, чтобы платформа Entity Framework будет включать `Supplier` таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="a5cc2-126">В файле WebApiConfig.cs добавьте модель EDM сущности «Поставщики»:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="a5cc2-127">Свойства навигации</span><span class="sxs-lookup"><span data-stu-id="a5cc2-127">Navigation Properties</span></span>

<span data-ttu-id="a5cc2-128">Чтобы получить поставщик для продукта, клиент отправляет запрос GET:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="a5cc2-129">Здесь «Поставщик» является свойством навигации на `Product` типа.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="a5cc2-130">В этом случае `Supplier` ссылается на один элемент, но переход свойство также может возвращать коллекции (отношения один ко многим "или" многие ко многим).</span><span class="sxs-lookup"><span data-stu-id="a5cc2-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="a5cc2-131">Чтобы этот запрос в службу поддержки, добавьте следующий метод в `ProductsController` класса:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="a5cc2-132">*Ключ* параметр — ключ продукта.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="a5cc2-133">Этот метод возвращает связанные сущности&#8212;в этом случае `Supplier` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="a5cc2-134">Имя метода и имени параметра являются важным.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="a5cc2-135">Как правило если свойство навигации называется «X», необходимо добавить метод с именем «GetX».</span><span class="sxs-lookup"><span data-stu-id="a5cc2-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="a5cc2-136">Метод должен принимать параметр с именем "*ключ*", соответствующий тип данных ключа родительского элемента.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="a5cc2-137">Также важно включить **[FromOdataUri]** атрибут в *ключ* параметра.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="a5cc2-138">Этот атрибут сообщает веб-API для использования правилами синтаксиса OData при синтаксическом анализе ключ из URI запроса.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="a5cc2-139">Создание и удаление ссылки</span><span class="sxs-lookup"><span data-stu-id="a5cc2-139">Creating and Deleting Links</span></span>

<span data-ttu-id="a5cc2-140">OData поддерживает создание или удаление связи между двумя сущностями.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="a5cc2-141">В терминологии OData связь является «ссылку».</span><span class="sxs-lookup"><span data-stu-id="a5cc2-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="a5cc2-142">Каждая ссылка имеет URI с формой *сущности*/$links /*сущности*.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="a5cc2-143">Например ссылка продукта поставщика выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="a5cc2-144">Чтобы создать новую ссылку, клиент отправляет запрос POST к URI ссылки.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="a5cc2-145">Текст запроса является URI целевой сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="a5cc2-146">Например предположим, что имеется поставщик с ключом «CTSO».</span><span class="sxs-lookup"><span data-stu-id="a5cc2-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="a5cc2-147">Чтобы создать ссылку из «Product(1)» на «Supplier('CTSO')», клиент отправляет запрос следующего вида:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="a5cc2-148">Чтобы удалить ссылку, клиент отправляет запрос DELETE к URI ссылки.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="a5cc2-149">**Создание связей между элементами**</span><span class="sxs-lookup"><span data-stu-id="a5cc2-149">**Creating Links**</span></span>

<span data-ttu-id="a5cc2-150">Чтобы включить клиента для создания ссылок на поставщика продукта, добавьте следующий код, чтобы `ProductsController` класса:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="a5cc2-151">Этот метод принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-151">This method takes three parameters:</span></span>

- <span data-ttu-id="a5cc2-152">*Ключ*: Ключ на родительскую сущность (продукт)</span><span class="sxs-lookup"><span data-stu-id="a5cc2-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="a5cc2-153">*navigationProperty*: Имя свойства навигации.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="a5cc2-154">В этом примере свойство навигации, единственным допустимым является «Поставщик».</span><span class="sxs-lookup"><span data-stu-id="a5cc2-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="a5cc2-155">*ссылка*: URI OData связанной сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="a5cc2-156">Это значение берется из текста запроса.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-156">This value is taken from the request body.</span></span> <span data-ttu-id="a5cc2-157">Например, ссылка URI может быть "`http://localhost/odata/Suppliers('CTSO')`, то есть поставщика с Идентификатором = «CTSO».</span><span class="sxs-lookup"><span data-stu-id="a5cc2-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="a5cc2-158">Данный метод использует ссылку для поиска поставщика.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="a5cc2-159">Если найден соответствующий поставщик, метод устанавливает `Product.Supplier` свойство и сохраняет результат в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="a5cc2-160">Самая важная часть синтаксического анализа URI ссылки.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="a5cc2-161">По сути вам нужно имитировать результат при отправке запроса GET к этому URI.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="a5cc2-162">Следующий вспомогательный метод показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="a5cc2-163">Метод вызывает процесс маршрутизации веб-API, а затем возвращает **ODataPath** экземпляр, представляющий проанализированный пути OData.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="a5cc2-164">Для URI ссылки один из сегментов должно быть ключом сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="a5cc2-165">(В противном случае клиент отправил недопустимый URI.)</span><span class="sxs-lookup"><span data-stu-id="a5cc2-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="a5cc2-166">**Удаление ссылки**</span><span class="sxs-lookup"><span data-stu-id="a5cc2-166">**Deleting Links**</span></span>

<span data-ttu-id="a5cc2-167">Чтобы удалить ссылку, добавьте следующий код, чтобы `ProductsController` класса:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="a5cc2-168">В этом примере свойство навигации представляет собой одну `Supplier` сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="a5cc2-169">Если свойство навигации является коллекцией, URI, чтобы удалить ссылку необходимо включить ключ для связанной сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="a5cc2-170">Пример:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="a5cc2-171">Этот запрос удаляет порядка 1 из клиента 1.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="a5cc2-172">В этом случае метод DeleteLink будут иметь следующую сигнатуру:</span><span class="sxs-lookup"><span data-stu-id="a5cc2-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="a5cc2-173">*RelatedKey* параметр предоставляет ключ для связанной сущности.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="a5cc2-174">Таким образом, в вашей `DeleteLink` метод, для поиска основной сущностью, *ключ* параметра, найти связанные сущности, *relatedKey* параметра, а затем удалите связь.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="a5cc2-175">В зависимости от вашей модели данных, может потребоваться реализовать обе версии `DeleteLink`.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="a5cc2-176">Веб-API вызовет правильную версию, в зависимости от URI запроса.</span><span class="sxs-lookup"><span data-stu-id="a5cc2-176">Web API will call the correct version based on the request URI.</span></span>
