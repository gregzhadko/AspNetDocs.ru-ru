---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: Поддержка параметров запроса OData в веб-API ASP.NET 2 — ASP.NET 4. x
author: MikeWasson
description: В статье Общие сведения о примерах кода показаны поддерживаемые параметры запроса OData в веб-API ASP.NET 2 для ASP.NET 4. x.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188641"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="61f01-103">Поддержка параметров запроса OData в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="61f01-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="61f01-104">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="61f01-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="61f01-105">В этом обзоре с примерами кода демонстрируется поддержка параметров запроса OData в веб-API ASP.NET 2 для ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="61f01-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="61f01-106">OData определяет параметры, которые могут быть использованы для изменения запроса OData.</span><span class="sxs-lookup"><span data-stu-id="61f01-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="61f01-107">Клиент отправляет эти параметры в строку запроса URI запроса.</span><span class="sxs-lookup"><span data-stu-id="61f01-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="61f01-108">Например, чтобы отсортировать результаты, клиент использует параметр $orderby:</span><span class="sxs-lookup"><span data-stu-id="61f01-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="61f01-109">Спецификация OData вызывает эти параметры *запроса*.</span><span class="sxs-lookup"><span data-stu-id="61f01-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="61f01-110">Вы можете включить параметры запроса OData для любого контроллера веб-API в проекте &#8212; контроллер не должен быть конечной точкой OData.</span><span class="sxs-lookup"><span data-stu-id="61f01-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="61f01-111">Это предоставляет удобный способ добавления таких функций, как фильтрация и сортировка, в любое приложение веб-API.</span><span class="sxs-lookup"><span data-stu-id="61f01-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="61f01-112">Перед включением параметров запроса ознакомьтесь с разделом [руководство по безопасности OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="61f01-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="61f01-113">Включение параметров запроса OData</span><span class="sxs-lookup"><span data-stu-id="61f01-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="61f01-114">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="61f01-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="61f01-115">Подкачка, управляемая сервером</span><span class="sxs-lookup"><span data-stu-id="61f01-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="61f01-116">Ограничение параметров запроса</span><span class="sxs-lookup"><span data-stu-id="61f01-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="61f01-117">Прямой вызов параметров запроса</span><span class="sxs-lookup"><span data-stu-id="61f01-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="61f01-118">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="61f01-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="61f01-119">Включение параметров запроса OData</span><span class="sxs-lookup"><span data-stu-id="61f01-119">Enabling OData Query Options</span></span>

<span data-ttu-id="61f01-120">Веб-API поддерживает следующие параметры запроса OData:</span><span class="sxs-lookup"><span data-stu-id="61f01-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="61f01-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="61f01-121">Option</span></span> | <span data-ttu-id="61f01-122">Описание</span><span class="sxs-lookup"><span data-stu-id="61f01-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61f01-123">$expand</span><span class="sxs-lookup"><span data-stu-id="61f01-123">$expand</span></span> | <span data-ttu-id="61f01-124">Разворачивает связанные сущности в строке.</span><span class="sxs-lookup"><span data-stu-id="61f01-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="61f01-125">$filter</span><span class="sxs-lookup"><span data-stu-id="61f01-125">$filter</span></span> | <span data-ttu-id="61f01-126">Фильтрует результаты на основе логического условия.</span><span class="sxs-lookup"><span data-stu-id="61f01-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="61f01-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="61f01-127">$inlinecount</span></span> | <span data-ttu-id="61f01-128">Указывает серверу включить общее число совпадающих сущностей в ответе.</span><span class="sxs-lookup"><span data-stu-id="61f01-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="61f01-129">(Полезно для разбиения на страницы на стороне сервера.)</span><span class="sxs-lookup"><span data-stu-id="61f01-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="61f01-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="61f01-130">$orderby</span></span> | <span data-ttu-id="61f01-131">Сортирует результаты.</span><span class="sxs-lookup"><span data-stu-id="61f01-131">Sorts the results.</span></span> |
| <span data-ttu-id="61f01-132">$select</span><span class="sxs-lookup"><span data-stu-id="61f01-132">$select</span></span> | <span data-ttu-id="61f01-133">Выбирает свойства, включаемые в ответ.</span><span class="sxs-lookup"><span data-stu-id="61f01-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="61f01-134">$skip</span><span class="sxs-lookup"><span data-stu-id="61f01-134">$skip</span></span> | <span data-ttu-id="61f01-135">Пропускает первые n результатов.</span><span class="sxs-lookup"><span data-stu-id="61f01-135">Skips the first n results.</span></span> |
| <span data-ttu-id="61f01-136">$top</span><span class="sxs-lookup"><span data-stu-id="61f01-136">$top</span></span> | <span data-ttu-id="61f01-137">Возвращает только первые n результатов.</span><span class="sxs-lookup"><span data-stu-id="61f01-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="61f01-138">Чтобы использовать параметры запроса OData, их необходимо включить явным образом.</span><span class="sxs-lookup"><span data-stu-id="61f01-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="61f01-139">Их можно включить глобально для всего приложения или включить для конкретных контроллеров или определенных действий.</span><span class="sxs-lookup"><span data-stu-id="61f01-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="61f01-140">Чтобы включить параметры запроса OData глобально, вызовите **енаблекуерисуппорт** для класса **HttpConfiguration** при запуске:</span><span class="sxs-lookup"><span data-stu-id="61f01-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="61f01-141">Метод **енаблекуерисуппорт** включает глобальные параметры запроса для любого действия контроллера, возвращающего тип **IQueryable** .</span><span class="sxs-lookup"><span data-stu-id="61f01-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="61f01-142">Если вы не хотите, чтобы параметры запроса были включены для всего приложения, можно включить их для конкретных действий контроллера, добавив атрибут [с возможностью **запроса]** к методу действия.</span><span class="sxs-lookup"><span data-stu-id="61f01-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="61f01-143">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="61f01-143">Example Queries</span></span>

<span data-ttu-id="61f01-144">В этом разделе показаны типы запросов, которые можно использовать с помощью параметров запроса OData.</span><span class="sxs-lookup"><span data-stu-id="61f01-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="61f01-145">Конкретные сведения о параметрах запроса см. в документации OData по адресу [www.OData.org](http://www.odata.org/).</span><span class="sxs-lookup"><span data-stu-id="61f01-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="61f01-146">Сведения о $expand и $select см. [в разделе использование $SELECT, $Expand и $value в веб-API ASP.NET OData](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="61f01-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="61f01-147">**Подкачка, управляемая клиентом**</span><span class="sxs-lookup"><span data-stu-id="61f01-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="61f01-148">Для больших наборов сущностей клиенту может потребоваться ограничить количество результатов.</span><span class="sxs-lookup"><span data-stu-id="61f01-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="61f01-149">Например, клиент может отображать 10 записей за раз, со ссылками "Далее" для получения следующей страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="61f01-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="61f01-150">Для этого клиент использует параметры $top и $skip.</span><span class="sxs-lookup"><span data-stu-id="61f01-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="61f01-151">Параметр $top задает максимальное число возвращаемых записей, а параметр $skip задает количество записей для пропуска.</span><span class="sxs-lookup"><span data-stu-id="61f01-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="61f01-152">В предыдущем примере выдаются записи с 21 по 30.</span><span class="sxs-lookup"><span data-stu-id="61f01-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="61f01-153">**Фильтрация**</span><span class="sxs-lookup"><span data-stu-id="61f01-153">**Filtering**</span></span>

<span data-ttu-id="61f01-154">Параметр $filter позволяет клиенту фильтровать результаты, применяя логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="61f01-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="61f01-155">Выражения фильтра являются достаточно мощными; в их число входят логические и арифметические операторы, строковые функции и функции даты.</span><span class="sxs-lookup"><span data-stu-id="61f01-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="61f01-156">Возврат всех продуктов с категорией, равным "Toys".</span><span class="sxs-lookup"><span data-stu-id="61f01-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="61f01-157">`http://localhost/Products?$filter=Category`EQ "Toys"</span><span class="sxs-lookup"><span data-stu-id="61f01-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="61f01-158">Возвращает все продукты с ценой меньше 10.</span><span class="sxs-lookup"><span data-stu-id="61f01-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="61f01-159">`http://localhost/Products?$filter=Price`lt 10</span><span class="sxs-lookup"><span data-stu-id="61f01-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="61f01-160">Логические операторы. Возвращает все продукты, где Price >= 5 и Price <= 15.</span><span class="sxs-lookup"><span data-stu-id="61f01-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="61f01-161">`http://localhost/Products?$filter=Price`GE 5 и Price Le 15</span><span class="sxs-lookup"><span data-stu-id="61f01-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="61f01-162">Строковые функции: возвращает все продукты с именем "ZZ" в имени.</span><span class="sxs-lookup"><span data-stu-id="61f01-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="61f01-163">Функции даты: возвращаются все продукты с ReleaseDate после 2005.</span><span class="sxs-lookup"><span data-stu-id="61f01-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="61f01-164">`http://localhost/Products?$filter=year(ReleaseDate)`gt 2005</span><span class="sxs-lookup"><span data-stu-id="61f01-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="61f01-165">**Сортировка**</span><span class="sxs-lookup"><span data-stu-id="61f01-165">**Sorting**</span></span>

<span data-ttu-id="61f01-166">Чтобы отсортировать результаты, используйте фильтр $orderby.</span><span class="sxs-lookup"><span data-stu-id="61f01-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="61f01-167">Сортировка по цене.</span><span class="sxs-lookup"><span data-stu-id="61f01-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="61f01-168">Сортировать по цене в убывающем порядке (от самого высокого до самого низкого).</span><span class="sxs-lookup"><span data-stu-id="61f01-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="61f01-169">Сортировать по категории, а затем сортировать по цене в порядке убывания в категориях.</span><span class="sxs-lookup"><span data-stu-id="61f01-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="61f01-170">Подкачка, управляемая сервером</span><span class="sxs-lookup"><span data-stu-id="61f01-170">Server-Driven Paging</span></span>

<span data-ttu-id="61f01-171">Если база данных содержит миллионы записей, вы не хотите отсылать их в одной полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="61f01-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="61f01-172">Чтобы избежать этого, сервер может ограничить количество записей, отправляемых в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="61f01-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="61f01-173">Чтобы включить серверную подкачку, задайте свойство **pageSize** в атрибуте, который можно **запросить** .</span><span class="sxs-lookup"><span data-stu-id="61f01-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="61f01-174">Значение — это максимальное число возвращаемых записей.</span><span class="sxs-lookup"><span data-stu-id="61f01-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="61f01-175">Если контроллер Возвращает формат OData, текст ответа будет содержать ссылку на следующую страницу данных:</span><span class="sxs-lookup"><span data-stu-id="61f01-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="61f01-176">Клиент может использовать эту ссылку для выборки следующей страницы.</span><span class="sxs-lookup"><span data-stu-id="61f01-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="61f01-177">Чтобы узнать общее число записей в результирующем наборе, клиент может установить параметр $inlinecount запроса со значением "allpages".</span><span class="sxs-lookup"><span data-stu-id="61f01-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="61f01-178">Значение "allpages" указывает серверу включить в ответ общее число:</span><span class="sxs-lookup"><span data-stu-id="61f01-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="61f01-179">Ссылки на следующую страницу и встроенное число должны иметь формат OData.</span><span class="sxs-lookup"><span data-stu-id="61f01-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="61f01-180">Причина заключается в том, что OData определяет специальные поля в тексте ответа для хранения ссылки и количества.</span><span class="sxs-lookup"><span data-stu-id="61f01-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="61f01-181">Для форматов, отличных от OData, по-прежнему поддерживается поддержка ссылок на следующую страницу и встроенного подсчета путем заключения результатов запроса в **объект &lt; пажересулт &gt; T** .</span><span class="sxs-lookup"><span data-stu-id="61f01-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="61f01-182">Однако для этого требуется немного больше кода.</span><span class="sxs-lookup"><span data-stu-id="61f01-182">However, it requires a bit more code.</span></span> <span data-ttu-id="61f01-183">Например:</span><span class="sxs-lookup"><span data-stu-id="61f01-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="61f01-184">Ниже приведен пример ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="61f01-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="61f01-185">Ограничение параметров запроса</span><span class="sxs-lookup"><span data-stu-id="61f01-185">Limiting the Query Options</span></span>

<span data-ttu-id="61f01-186">Параметры запроса позволяют клиенту получить большой контроль над запросом, который выполняется на сервере.</span><span class="sxs-lookup"><span data-stu-id="61f01-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="61f01-187">В некоторых случаях может потребоваться ограничить доступные варианты по соображениям безопасности или производительности.</span><span class="sxs-lookup"><span data-stu-id="61f01-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="61f01-188">Атрибут **[с поддержкой запроса]** имеет некоторые встроенные свойства для этого.</span><span class="sxs-lookup"><span data-stu-id="61f01-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="61f01-189">Рассмотрим некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="61f01-189">Here are some examples.</span></span>

<span data-ttu-id="61f01-190">Разрешить только $skip и $top для поддержки разбиения на страницы и других действий:</span><span class="sxs-lookup"><span data-stu-id="61f01-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="61f01-191">Разрешить упорядочение только по определенным свойствам, чтобы предотвратить сортировку по свойствам, которые не индексируются в базе данных:</span><span class="sxs-lookup"><span data-stu-id="61f01-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="61f01-192">Разрешить логическую функцию "EQ", но не другие логические функции:</span><span class="sxs-lookup"><span data-stu-id="61f01-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="61f01-193">Не разрешать арифметические операторы:</span><span class="sxs-lookup"><span data-stu-id="61f01-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="61f01-194">Вы можете глобально ограничить параметры, создав экземпляр **куеряблеаттрибуте** и передав его в функцию **енаблекуерисуппорт** :</span><span class="sxs-lookup"><span data-stu-id="61f01-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="61f01-195">Прямой вызов параметров запроса</span><span class="sxs-lookup"><span data-stu-id="61f01-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="61f01-196">Вместо использования атрибута [с поддержкой **запроса]** можно вызывать параметры запроса непосредственно в контроллере.</span><span class="sxs-lookup"><span data-stu-id="61f01-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="61f01-197">Для этого добавьте параметр **одатакуерйоптионс** в метод контроллера.</span><span class="sxs-lookup"><span data-stu-id="61f01-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="61f01-198">В этом случае атрибут [с поддержкой **запроса]** не требуется.</span><span class="sxs-lookup"><span data-stu-id="61f01-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="61f01-199">Веб-API заполняет **одатакуерйоптионс** из строки запроса URI.</span><span class="sxs-lookup"><span data-stu-id="61f01-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="61f01-200">Чтобы применить запрос, передайте **IQueryable** методу **ApplyTo** .</span><span class="sxs-lookup"><span data-stu-id="61f01-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="61f01-201">Метод возвращает другой **IQueryable**.</span><span class="sxs-lookup"><span data-stu-id="61f01-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="61f01-202">Для более сложных сценариев, если у вас нет поставщика запросов **IQueryable** , можно проверить **одатакуерйоптионс** и преобразовать параметры запроса в другую форму.</span><span class="sxs-lookup"><span data-stu-id="61f01-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="61f01-203">(Например, см. запись блога Рагхурам Надиминти, посвященная [преобразованию запросов OData в HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), в которую также входит [Пример](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span><span class="sxs-lookup"><span data-stu-id="61f01-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="61f01-204">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="61f01-204">Query Validation</span></span>

<span data-ttu-id="61f01-205">Атрибут **[с поддержкой запроса]** проверяет запрос перед его выполнением.</span><span class="sxs-lookup"><span data-stu-id="61f01-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="61f01-206">Шаг проверки выполняется в методе **куеряблеаттрибуте. ValidateQuery** .</span><span class="sxs-lookup"><span data-stu-id="61f01-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="61f01-207">Также можно настроить процесс проверки.</span><span class="sxs-lookup"><span data-stu-id="61f01-207">You can also customize the validation process.</span></span>

<span data-ttu-id="61f01-208">См. также [руководство по безопасности OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="61f01-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="61f01-209">Сначала Переопределите один из классов проверяющего элемента управления, определенный в пространстве имен **Web. http. OData. Query. проверяющих** .</span><span class="sxs-lookup"><span data-stu-id="61f01-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="61f01-210">Например, следующий класс проверяющего элемента управления отключает параметр DESC для параметра $orderby.</span><span class="sxs-lookup"><span data-stu-id="61f01-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="61f01-211">Подклассировать атрибут **[Query]** , чтобы переопределить метод **ValidateQuery** .</span><span class="sxs-lookup"><span data-stu-id="61f01-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="61f01-212">Затем задайте настраиваемый атрибут глобально или на уровне каждого контроллера:</span><span class="sxs-lookup"><span data-stu-id="61f01-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="61f01-213">Если вы используете **одатакуерйоптионс** напрямую, задайте следующие параметры проверяющего элемента управления:</span><span class="sxs-lookup"><span data-stu-id="61f01-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
