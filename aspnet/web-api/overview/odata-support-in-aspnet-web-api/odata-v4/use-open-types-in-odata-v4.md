---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Открытые типы в OData v4 с ASP.NET Web API Документы Майкрософт
author: rick-anderson
description: В OData v4 открытый тип представляет собой структурированный тип, содержащий динамические свойства, в дополнение к любым свойствам, заявленным в определении типа. Открыть...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543734"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="4ef37-104">Открытые типы в OData v4 с ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="4ef37-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="4ef37-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4ef37-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4ef37-106">В OData v4 *открытый тип* представляет собой структурированный тип, содержащий динамические свойства, в дополнение к любым свойствам, заявленным в определении типа.</span><span class="sxs-lookup"><span data-stu-id="4ef37-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="4ef37-107">Открытые типы позволяют повысить гибкость моделей данных.</span><span class="sxs-lookup"><span data-stu-id="4ef37-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="4ef37-108">В этом уроке показано, как использовать открытые типы в ASP.NET Web API OData.</span><span class="sxs-lookup"><span data-stu-id="4ef37-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="4ef37-109">Этот учебник предполагает, что вы уже знаете, как создать конечную точку OData в ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="4ef37-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="4ef37-110">Если нет, начните с чтения [Создайте OData v4 Конечная точка](create-an-odata-v4-endpoint.md) в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="4ef37-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4ef37-111">Версии программного обеспечения, используемые в учебнике</span><span class="sxs-lookup"><span data-stu-id="4ef37-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4ef37-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="4ef37-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="4ef37-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="4ef37-113">OData v4</span></span>

<span data-ttu-id="4ef37-114">Во-первых, некоторые терминологии OData:</span><span class="sxs-lookup"><span data-stu-id="4ef37-114">First, some OData terminology:</span></span>

- <span data-ttu-id="4ef37-115">Тип сущности: структурированный тип с ключом.</span><span class="sxs-lookup"><span data-stu-id="4ef37-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="4ef37-116">Сложный тип: структурированный тип без ключа.</span><span class="sxs-lookup"><span data-stu-id="4ef37-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="4ef37-117">Открытый тип: Тип с динамическими свойствами.</span><span class="sxs-lookup"><span data-stu-id="4ef37-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="4ef37-118">Могут быть открыты как типы сущностей, так и сложные.</span><span class="sxs-lookup"><span data-stu-id="4ef37-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="4ef37-119">Значение динамического свойства может быть примитивным типом, сложным типом или типом перечисления; или коллекция любого из этих типов.</span><span class="sxs-lookup"><span data-stu-id="4ef37-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="4ef37-120">Для получения дополнительной информации [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/)об открытых типах см.</span><span class="sxs-lookup"><span data-stu-id="4ef37-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="4ef37-121">Установка веб-библиотеки OData</span><span class="sxs-lookup"><span data-stu-id="4ef37-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="4ef37-122">Используйте nuGet Package Manager для установки новейших библиотек Web API OData.</span><span class="sxs-lookup"><span data-stu-id="4ef37-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="4ef37-123">В окне Консоль диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="4ef37-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="4ef37-124">Определение типов CLR</span><span class="sxs-lookup"><span data-stu-id="4ef37-124">Define the CLR Types</span></span>

<span data-ttu-id="4ef37-125">Начните с определения моделей EDM как типов CLR.</span><span class="sxs-lookup"><span data-stu-id="4ef37-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="4ef37-126">При создании модели данных сущности (EDM)</span><span class="sxs-lookup"><span data-stu-id="4ef37-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="4ef37-127">`Category`является типом перечисления.</span><span class="sxs-lookup"><span data-stu-id="4ef37-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="4ef37-128">`Address`является сложным типом.</span><span class="sxs-lookup"><span data-stu-id="4ef37-128">`Address` is a complex type.</span></span> <span data-ttu-id="4ef37-129">(Он не имеет ключа, поэтому он не является типом сущности.)</span><span class="sxs-lookup"><span data-stu-id="4ef37-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="4ef37-130">`Customer`— это тип сущности.</span><span class="sxs-lookup"><span data-stu-id="4ef37-130">`Customer` is an entity type.</span></span> <span data-ttu-id="4ef37-131">(У него есть ключ.)</span><span class="sxs-lookup"><span data-stu-id="4ef37-131">(It has a key.)</span></span>
- <span data-ttu-id="4ef37-132">`Press`является открытым сложным типом.</span><span class="sxs-lookup"><span data-stu-id="4ef37-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="4ef37-133">`Book`— это открытый тип сущности.</span><span class="sxs-lookup"><span data-stu-id="4ef37-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="4ef37-134">Для создания открытого типа тип CLR должен `IDictionary<string, object>`иметь свойство типа, которое содержит динамические свойства.</span><span class="sxs-lookup"><span data-stu-id="4ef37-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="4ef37-135">Создание модели EDM</span><span class="sxs-lookup"><span data-stu-id="4ef37-135">Build the EDM Model</span></span>

<span data-ttu-id="4ef37-136">Если вы используете **ODataConventionModelBuilder** для `Press` `Book` создания EDM, и автоматически добавляются `IDictionary<string, object>` в качестве открытых типов, в зависимости от наличия свойства.</span><span class="sxs-lookup"><span data-stu-id="4ef37-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="4ef37-137">Вы также можете построить EDM явно, используя **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="4ef37-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="4ef37-138">Добавление контроллера OData</span><span class="sxs-lookup"><span data-stu-id="4ef37-138">Add an OData Controller</span></span>

<span data-ttu-id="4ef37-139">Затем добавьте контроллер OData.</span><span class="sxs-lookup"><span data-stu-id="4ef37-139">Next, add an OData controller.</span></span> <span data-ttu-id="4ef37-140">Для этого руководства мы будем использовать упрощенный контроллер, который просто поддерживает запросы GET и POST, а также использует список в памяти для хранения сущностей.</span><span class="sxs-lookup"><span data-stu-id="4ef37-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="4ef37-141">Обратите внимание, `Book` что первая инстанция не имеет динамических свойств.</span><span class="sxs-lookup"><span data-stu-id="4ef37-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="4ef37-142">Второй `Book` экземпляр имеет следующие динамические свойства:</span><span class="sxs-lookup"><span data-stu-id="4ef37-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="4ef37-143">"Опубликовано": Примитивный тип</span><span class="sxs-lookup"><span data-stu-id="4ef37-143">"Published": Primitive type</span></span>
- <span data-ttu-id="4ef37-144">"Авторы": Коллекция примитивных типов</span><span class="sxs-lookup"><span data-stu-id="4ef37-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="4ef37-145">"Другие категории": Коллекция типов перечислений.</span><span class="sxs-lookup"><span data-stu-id="4ef37-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="4ef37-146">Кроме того, свойство `Press` этого `Book` экземпляра имеет следующие динамические свойства:</span><span class="sxs-lookup"><span data-stu-id="4ef37-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="4ef37-147">"Блог": Примитивный тип</span><span class="sxs-lookup"><span data-stu-id="4ef37-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="4ef37-148">"Адрес": Комплексный тип</span><span class="sxs-lookup"><span data-stu-id="4ef37-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="4ef37-149">Запрос метаданных</span><span class="sxs-lookup"><span data-stu-id="4ef37-149">Query the Metadata</span></span>

<span data-ttu-id="4ef37-150">Чтобы получить документ метаданных OData, отправьте запрос `~/$metadata`GET.</span><span class="sxs-lookup"><span data-stu-id="4ef37-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="4ef37-151">Ответный орган должен выглядеть так же, как это:</span><span class="sxs-lookup"><span data-stu-id="4ef37-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="4ef37-152">Из документа метаданных можно увидеть:</span><span class="sxs-lookup"><span data-stu-id="4ef37-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="4ef37-153">Для `Book` типов `Press` и типов значение `OpenType` атрибута верно.</span><span class="sxs-lookup"><span data-stu-id="4ef37-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="4ef37-154">`Customer` Типы `Address` и типы не имеют этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="4ef37-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="4ef37-155">Тип `Book` сущности имеет три заявленных свойства: ISBN, Название и Пресс.</span><span class="sxs-lookup"><span data-stu-id="4ef37-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="4ef37-156">Метаданные OData не включают `Book.Properties` свойство из класса CLR.</span><span class="sxs-lookup"><span data-stu-id="4ef37-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="4ef37-157">Аналогичным образом, сложный `Press` тип имеет только два заявленных свойства: имя и категория.</span><span class="sxs-lookup"><span data-stu-id="4ef37-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="4ef37-158">Метаданные не включают `Press.DynamicProperties` свойство из класса CLR.</span><span class="sxs-lookup"><span data-stu-id="4ef37-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="4ef37-159">Запрос Сущность</span><span class="sxs-lookup"><span data-stu-id="4ef37-159">Query an Entity</span></span>

<span data-ttu-id="4ef37-160">Чтобы получить книгу с ISBN равна "978-0-7356-7942-9", отправить запрос GET `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="4ef37-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="4ef37-161">Ответный орган должен выглядеть так же, как и следующие.</span><span class="sxs-lookup"><span data-stu-id="4ef37-161">The response body should look similar to the following.</span></span> <span data-ttu-id="4ef37-162">(Отступ, чтобы сделать его более читаемым.)</span><span class="sxs-lookup"><span data-stu-id="4ef37-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="4ef37-163">Обратите внимание, что динамические свойства включены в соответствие с заявленными свойствами.</span><span class="sxs-lookup"><span data-stu-id="4ef37-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="4ef37-164">POST Сущность</span><span class="sxs-lookup"><span data-stu-id="4ef37-164">POST an Entity</span></span>

<span data-ttu-id="4ef37-165">Чтобы добавить объект Book, отправьте запрос `~/Books`POST.</span><span class="sxs-lookup"><span data-stu-id="4ef37-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="4ef37-166">Клиент может установить динамические свойства в полезной нагрузке запроса.</span><span class="sxs-lookup"><span data-stu-id="4ef37-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="4ef37-167">Вот пример запроса.</span><span class="sxs-lookup"><span data-stu-id="4ef37-167">Here is an example request.</span></span> <span data-ttu-id="4ef37-168">Обратите внимание на свойства "Цена" и "Опубликовано".</span><span class="sxs-lookup"><span data-stu-id="4ef37-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="4ef37-169">Если вы установите точку разрыва в методе контроллера, можно `Properties` увидеть, что Web API добавил эти свойства в словарь.</span><span class="sxs-lookup"><span data-stu-id="4ef37-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="4ef37-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4ef37-170">Additional Resources</span></span>

[<span data-ttu-id="4ef37-171">Пример открытого типа OData</span><span class="sxs-lookup"><span data-stu-id="4ef37-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
