---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Руководство по безопасности для веб-API 2 ASP.NET OData | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/06/2013
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 4ba53e15dab83368097a58ba4d0d2e46d113d1d2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065251"
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="173ae-102">Руководство по безопасности для веб-API 2 ASP.NET OData</span><span class="sxs-lookup"><span data-stu-id="173ae-102">Security Guidance for ASP.NET Web API 2 OData</span></span>
====================
<span data-ttu-id="173ae-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="173ae-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="173ae-104">В этом разделе описываются некоторые проблемы безопасности, которые следует учитывать при предоставлении объект dataset с помощью OData.</span><span class="sxs-lookup"><span data-stu-id="173ae-104">This topic describes some of the security issues that you should consider when exposing a dataset through OData.</span></span>

## <a name="edm-security"></a><span data-ttu-id="173ae-105">Модель EDM безопасности</span><span class="sxs-lookup"><span data-stu-id="173ae-105">EDM Security</span></span>

<span data-ttu-id="173ae-106">Семантики запросов основаны на модели EDM (модель EDM), не базовых типов модели.</span><span class="sxs-lookup"><span data-stu-id="173ae-106">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="173ae-107">Свойство можно исключить из модели EDM, и он не будет видимым для запроса.</span><span class="sxs-lookup"><span data-stu-id="173ae-107">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="173ae-108">Например предположим, что модель включает в себя тип со свойством заработной платы сотрудника.</span><span class="sxs-lookup"><span data-stu-id="173ae-108">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="173ae-109">Может потребоваться исключить это свойство из модели EDM, чтобы скрыть его от клиентов.</span><span class="sxs-lookup"><span data-stu-id="173ae-109">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="173ae-110">Существует два способа исключает свойство из модели EDM.</span><span class="sxs-lookup"><span data-stu-id="173ae-110">There are two ways to exlude a property from the EDM.</span></span> <span data-ttu-id="173ae-111">Можно задать **[IgnoreDataMember]** атрибут на свойство в класс модели:</span><span class="sxs-lookup"><span data-stu-id="173ae-111">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="173ae-112">Можно также удалить свойство из EDM программным способом.</span><span class="sxs-lookup"><span data-stu-id="173ae-112">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="173ae-113">Безопасность запросов</span><span class="sxs-lookup"><span data-stu-id="173ae-113">Query Security</span></span>

<span data-ttu-id="173ae-114">Вредоносный или упрощенный клиент может иметь возможность создайте запрос, который занимает очень много времени для выполнения.</span><span class="sxs-lookup"><span data-stu-id="173ae-114">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="173ae-115">В худшем случае это может нарушить доступ к вашей службе.</span><span class="sxs-lookup"><span data-stu-id="173ae-115">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="173ae-116">**[Queryable]** атрибута является фильтром операции, которая выполняет синтаксический анализ, проверяет и применяет запрос.</span><span class="sxs-lookup"><span data-stu-id="173ae-116">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="173ae-117">Фильтр преобразует параметры запроса в выражении LINQ.</span><span class="sxs-lookup"><span data-stu-id="173ae-117">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="173ae-118">При возвращении контроллер OData **IQueryable** типа, **IQueryable** LINQ поставщик преобразует выражения LINQ в запрос.</span><span class="sxs-lookup"><span data-stu-id="173ae-118">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="173ae-119">Таким образом производительность зависит от поставщика LINQ, который используется, а также от характеристик конкретной схемы набора данных или базы данных.</span><span class="sxs-lookup"><span data-stu-id="173ae-119">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="173ae-120">Дополнительные сведения об использовании параметров запроса OData в веб-API ASP.NET, см. в разделе [поддержки параметров запроса OData](supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="173ae-120">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="173ae-121">Если вы знаете, что все клиенты являются доверенными (например, в корпоративной среде) или небольшой набор данных, производительность запросов может оказаться проблемой.</span><span class="sxs-lookup"><span data-stu-id="173ae-121">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="173ae-122">В противном случае рассмотрите следующие рекомендации.</span><span class="sxs-lookup"><span data-stu-id="173ae-122">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="173ae-123">Тестирование службы с помощью различных запросов и профиля базы данных.</span><span class="sxs-lookup"><span data-stu-id="173ae-123">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="173ae-124">Включение сервера разбиение на страницы избежать возвращения большого набора данных в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="173ae-124">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="173ae-125">Дополнительные сведения см. в разделе [разбиение по страницам Server-Driven](supporting-odata-query-options.md#server-paging).</span><span class="sxs-lookup"><span data-stu-id="173ae-125">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="173ae-126">Требуется $filter и $orderby?</span><span class="sxs-lookup"><span data-stu-id="173ae-126">Do you need $filter and $orderby?</span></span> <span data-ttu-id="173ae-127">Некоторые приложения может разрешить клиентским разбиение по страницам, используя $top и $skip, но отключить другие параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="173ae-127">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="173ae-128">Можно ограничить $orderby к свойствам в кластеризованном индексе.</span><span class="sxs-lookup"><span data-stu-id="173ae-128">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="173ae-129">Сортировка больших объемов данных без кластеризованного индекса выполняется медленно.</span><span class="sxs-lookup"><span data-stu-id="173ae-129">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="173ae-130">Максимальное число узлов: **MaxNodeCount** свойство **[Queryable]** задает максимальное число узлов, разрешенных в синтаксического дерева $filter.</span><span class="sxs-lookup"><span data-stu-id="173ae-130">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="173ae-131">Значение по умолчанию — 100, но вы можете задать более низкое значение, так как большое количество узлов может выполняться медленно для компиляции.</span><span class="sxs-lookup"><span data-stu-id="173ae-131">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="173ae-132">Это особенно верно при использовании LINQ to Objects (т. е. запросы LINQ к коллекции в памяти, без использования промежуточного поставщика LINQ).</span><span class="sxs-lookup"><span data-stu-id="173ae-132">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="173ae-133">Рекомендуется отключить функции any() и all(), так как они могут выполняться медленно.</span><span class="sxs-lookup"><span data-stu-id="173ae-133">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="173ae-134">Если любые свойства строки содержат больших строк&#8212;к примеру, описание продукта или запись в блоге&#8212;рекомендуется отключить строковые функции.</span><span class="sxs-lookup"><span data-stu-id="173ae-134">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="173ae-135">Рассмотрите возможность запрета, фильтрация по свойствам навигации.</span><span class="sxs-lookup"><span data-stu-id="173ae-135">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="173ae-136">Фильтрация по свойствам навигации может привести соединение, которое может быть медленным, в зависимости от схемы базы данных.</span><span class="sxs-lookup"><span data-stu-id="173ae-136">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="173ae-137">В следующем коде показано запроса проверяющий элемент управления, не позволяющая фильтрация по свойствам навигации.</span><span class="sxs-lookup"><span data-stu-id="173ae-137">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="173ae-138">Дополнительные сведения о запросе проверяющие элементы управления, см. в разделе [Проверка запроса](supporting-odata-query-options.md#query-validation).</span><span class="sxs-lookup"><span data-stu-id="173ae-138">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="173ae-139">Можно ограничить запросы $filter, написав проверяющий элемент управления, который настроен для базы данных.</span><span class="sxs-lookup"><span data-stu-id="173ae-139">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="173ae-140">Например рассмотрим следующие два запроса:</span><span class="sxs-lookup"><span data-stu-id="173ae-140">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="173ae-141">Все фильмы с субъектами, чья фамилия начинается с «A».</span><span class="sxs-lookup"><span data-stu-id="173ae-141">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="173ae-142">Все фильмы, выпущенная в 1994 г.</span><span class="sxs-lookup"><span data-stu-id="173ae-142">All movies released in 1994.</span></span>

    <span data-ttu-id="173ae-143">Если субъекты индексированных фильмы, первый запрос может потребоваться ядра СУБД, чтобы проверять весь список фильмов.</span><span class="sxs-lookup"><span data-stu-id="173ae-143">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="173ae-144">В то время как второй запрос может быть приемлемым, если предполагается, что фильмы индексируются год выпуска.</span><span class="sxs-lookup"><span data-stu-id="173ae-144">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="173ae-145">В следующем коде показано проверяющий элемент управления, который позволяет фильтровать свойства «ReleaseYear» и «Title», но не других свойств.</span><span class="sxs-lookup"><span data-stu-id="173ae-145">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="173ae-146">В общем случае рекомендуется какие функции $filter.</span><span class="sxs-lookup"><span data-stu-id="173ae-146">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="173ae-147">Если клиентам не требуется полный выразительность $filter, можно ограничить допустимые функции.</span><span class="sxs-lookup"><span data-stu-id="173ae-147">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>