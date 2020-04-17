---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Наследовать с комплексом типа в OData v4 с ASP.NET Web API Документы Майкрософт
author: rick-anderson
description: Согласно спецификации OData v4, сложный тип может наследоваться от другого сложного типа. (Сложный тип представляет собой структурированный тип без ключа.) Веб-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543604"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="6f8b8-104">Наследовать сложный тип в OData v4 с ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6f8b8-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="6f8b8-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6f8b8-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6f8b8-106">Согласно [спецификации](http://www.odata.org/documentation/odata-version-4-0/)OData v4, сложный тип может наследовать от другого сложного типа.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="6f8b8-107">*(Сложный* тип представляет собой структурированный тип без ключа.) Web API OData 5.3 поддерживает наследование сложного типа.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="6f8b8-108">В этой теме показано, как построить модель данных сущности (EDM) со сложными типами наследования.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="6f8b8-109">Для полного исходного [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)кода см.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6f8b8-110">Версии программного обеспечения, используемые в учебнике</span><span class="sxs-lookup"><span data-stu-id="6f8b8-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6f8b8-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="6f8b8-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="6f8b8-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="6f8b8-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="6f8b8-113">Типовая иерархия</span><span class="sxs-lookup"><span data-stu-id="6f8b8-113">Model Hierarchy</span></span>

<span data-ttu-id="6f8b8-114">Чтобы проиллюстрировать сложное наследование типа, мы используем следующую иерархию классов.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="6f8b8-115">`Shape`является абстрактным сложным типом.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="6f8b8-116">`Rectangle`, `Triangle`, `Circle` и являются сложными `RoundRectangle` типами, `Rectangle`полученными из `Shape`, и происходит от .</span><span class="sxs-lookup"><span data-stu-id="6f8b8-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="6f8b8-117">`Window`— тип сущности `Shape` и содержит экземпляр.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="6f8b8-118">Вот классы CLR, которые определяют эти типы.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="6f8b8-119">Создание модели EDM</span><span class="sxs-lookup"><span data-stu-id="6f8b8-119">Build the EDM Model</span></span>

<span data-ttu-id="6f8b8-120">Для создания EDM можно использовать **ODataConventionModelBuilder,** который выводит отношения наследования из типов CLR.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="6f8b8-121">Вы также можете построить EDM явно, используя **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="6f8b8-122">Это требует больше кода, но дает вам больше контроля над EDM.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="6f8b8-123">Эти два примера создают одну и ту же схему EDM.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="6f8b8-124">Метаданный документ</span><span class="sxs-lookup"><span data-stu-id="6f8b8-124">Metadata Document</span></span>

<span data-ttu-id="6f8b8-125">Вот документ метаданных OData, показывающий наследование сложного типа.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="6f8b8-126">Из документа метаданных можно увидеть:</span><span class="sxs-lookup"><span data-stu-id="6f8b8-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="6f8b8-127">Сложный `Shape` тип абстрактный.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="6f8b8-128">В `Rectangle` `Triangle`, `Circle` и сложный тип `Shape`имеют базовый тип .</span><span class="sxs-lookup"><span data-stu-id="6f8b8-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="6f8b8-129">Тип `RoundRectangle` имеет базовый `Rectangle`тип.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="6f8b8-130">Типы кастинг-комплексов</span><span class="sxs-lookup"><span data-stu-id="6f8b8-130">Casting Complex Types</span></span>

<span data-ttu-id="6f8b8-131">Кастинг на сложных типах теперь поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6f8b8-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="6f8b8-132">Например, следующий запрос отбрасывает `Shape` `Rectangle`a к .</span><span class="sxs-lookup"><span data-stu-id="6f8b8-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="6f8b8-133">Вот полезная нагрузка ответа:</span><span class="sxs-lookup"><span data-stu-id="6f8b8-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
