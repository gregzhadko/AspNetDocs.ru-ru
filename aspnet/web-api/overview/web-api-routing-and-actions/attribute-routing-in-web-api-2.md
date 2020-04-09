---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: АтрибутИрование в ASP.NET Web API 2 Документы Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675386"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="672b1-102">Реукторация атрибутов в ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="672b1-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="672b1-103">[Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="672b1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="672b1-104">*Трассировка* — это то, как Web API соответствует URI действию.</span><span class="sxs-lookup"><span data-stu-id="672b1-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="672b1-105">Web API 2 поддерживает новый тип трассировки, называемый *размыванием атрибутов.*</span><span class="sxs-lookup"><span data-stu-id="672b1-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="672b1-106">Как следует из названия, маршрутирование атрибутов использует атрибуты для определения маршрутов.</span><span class="sxs-lookup"><span data-stu-id="672b1-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="672b1-107">Трассировка атрибутов дает вам больше контроля над URIs в вашем веб-API.</span><span class="sxs-lookup"><span data-stu-id="672b1-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="672b1-108">Например, можно легко создать УРИ, описывающие иерархии ресурсов.</span><span class="sxs-lookup"><span data-stu-id="672b1-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="672b1-109">Более ранний стиль разгрома, называемый реуляционным, по-прежнему полностью поддерживается.</span><span class="sxs-lookup"><span data-stu-id="672b1-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="672b1-110">На самом деле, вы можете объединить обе техники в одном проекте.</span><span class="sxs-lookup"><span data-stu-id="672b1-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="672b1-111">В этой теме показано, как включить разгром атрибутов, и описаны различные параметры для разгрома атрибутов.</span><span class="sxs-lookup"><span data-stu-id="672b1-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="672b1-112">Для сквозного учебника, использующемся трассировку атрибутов, [см.](create-a-rest-api-with-attribute-routing.md)</span><span class="sxs-lookup"><span data-stu-id="672b1-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="672b1-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="672b1-113">Prerequisites</span></span>

<span data-ttu-id="672b1-114">[Визуальная студия 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Сообщество, Профессиональный или Корпоративный выпуск</span><span class="sxs-lookup"><span data-stu-id="672b1-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="672b1-115">Кроме того, используйте NuGet Package Manager для установки необходимых пакетов.</span><span class="sxs-lookup"><span data-stu-id="672b1-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="672b1-116">Из меню **Инструменты** в Visual Studio, выберите **NuGet менеджер пакета**, а затем выберите **консоль менеджер пакетов**.</span><span class="sxs-lookup"><span data-stu-id="672b1-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="672b1-117">Введите следующую команду в окне консоли менеджера пакетов:</span><span class="sxs-lookup"><span data-stu-id="672b1-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="672b1-118">Почему атрибут ирование?</span><span class="sxs-lookup"><span data-stu-id="672b1-118">Why Attribute Routing?</span></span>

<span data-ttu-id="672b1-119">В первом выпуске Web API использовалась реуктора *на основе конвенций.*</span><span class="sxs-lookup"><span data-stu-id="672b1-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="672b1-120">В этом типе маршрутизации вы определяете один или несколько шаблонов маршрутов, которые в основном являются параметражными строками.</span><span class="sxs-lookup"><span data-stu-id="672b1-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="672b1-121">Когда фреймворк получает запрос, он сопоставляет URI с шаблоном маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="672b1-122">Для получения дополнительной информации о реунетировке на основе конвенций с [ASP.NETм.](routing-in-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="672b1-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="672b1-123">Одним из преимуществ реуктора на основе конвенций является то, что шаблоны определяются в одном месте, а правила разгрома последовательно применяются во всех контроллерах.</span><span class="sxs-lookup"><span data-stu-id="672b1-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="672b1-124">К сожалению, на основе конвенций, что затрудняет поддержку некоторых шаблонов URI, которые распространены в RESTful AIS.</span><span class="sxs-lookup"><span data-stu-id="672b1-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="672b1-125">Например, ресурсы часто содержат детские ресурсы: у клиентов есть заказы, у фильмов есть актеры, у книг есть авторы и так далее.</span><span class="sxs-lookup"><span data-stu-id="672b1-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="672b1-126">Естественно создавать УРИ, отражающие эти отношения:</span><span class="sxs-lookup"><span data-stu-id="672b1-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="672b1-127">Этот тип URI трудно создать с помощью конференц-реуктора.</span><span class="sxs-lookup"><span data-stu-id="672b1-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="672b1-128">Хотя это может быть сделано, результаты не масштабируются хорошо, если у вас есть много контроллеров или типов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="672b1-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="672b1-129">При маршрутизаторе атрибутов тривиально определить маршрут для этого URI.</span><span class="sxs-lookup"><span data-stu-id="672b1-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="672b1-130">Вы просто добавляете атрибут в действие контроллера:</span><span class="sxs-lookup"><span data-stu-id="672b1-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="672b1-131">Вот некоторые другие шаблоны, которые атрибут разгрома делает легко.</span><span class="sxs-lookup"><span data-stu-id="672b1-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="672b1-132">**Управление версиями API**</span><span class="sxs-lookup"><span data-stu-id="672b1-132">**API versioning**</span></span>

<span data-ttu-id="672b1-133">В этом примере "/api/v1/products" будет направляться другому контроллеру, чем "/api/v2/products".</span><span class="sxs-lookup"><span data-stu-id="672b1-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="672b1-134">**Перегруженные сегменты URI**</span><span class="sxs-lookup"><span data-stu-id="672b1-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="672b1-135">В этом примере "1" — это номер заказа, но «ожидающий» карты к коллекции.</span><span class="sxs-lookup"><span data-stu-id="672b1-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="672b1-136">**Несколько типов параметров**</span><span class="sxs-lookup"><span data-stu-id="672b1-136">**Multiple parameter types**</span></span>

<span data-ttu-id="672b1-137">В этом примере "1" является номером заказа, но "2013/06/16" указывает дату.</span><span class="sxs-lookup"><span data-stu-id="672b1-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="672b1-138">Включение реуктора атрибутов</span><span class="sxs-lookup"><span data-stu-id="672b1-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="672b1-139">Чтобы включить маршрутизирование атрибутов, звоните **MapHttpAttributeRoutes** во время конфигурации.</span><span class="sxs-lookup"><span data-stu-id="672b1-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="672b1-140">Этот метод расширения определен в классе **System.Web.httpConfigurationExtensions.**</span><span class="sxs-lookup"><span data-stu-id="672b1-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="672b1-141">Реуничная реуктора может быть объединена с реунетировкой [на основе конвенций.](routing-in-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="672b1-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="672b1-142">Чтобы определить маршруты, основанные на конвенциях, позвоните в метод **MapHttpRoute.**</span><span class="sxs-lookup"><span data-stu-id="672b1-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="672b1-143">Для получения дополнительной информации о настройке Web API см [ASP.NET.](../advanced/configuring-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="672b1-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="672b1-144">Примечание: Миграция из Web API 1</span><span class="sxs-lookup"><span data-stu-id="672b1-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="672b1-145">До Web API 2 шаблоны проекта Web API генерировали код следующим образом:</span><span class="sxs-lookup"><span data-stu-id="672b1-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="672b1-146">Если возможно расширение реаутирования атрибутов, этот код будет бросать исключение.</span><span class="sxs-lookup"><span data-stu-id="672b1-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="672b1-147">При обновлении существующего проекта Web API для использования входном атрибутике не забудьте обновить этот код конфигурации до следующего:</span><span class="sxs-lookup"><span data-stu-id="672b1-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="672b1-148">Для получения дополнительной информации см [ASP.NET.](../advanced/configuring-aspnet-web-api.md#webhost)</span><span class="sxs-lookup"><span data-stu-id="672b1-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="672b1-149">Добавление атрибутов маршрута</span><span class="sxs-lookup"><span data-stu-id="672b1-149">Adding Route Attributes</span></span>

<span data-ttu-id="672b1-150">Вот пример маршрута, определяемого с помощью атрибута:</span><span class="sxs-lookup"><span data-stu-id="672b1-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="672b1-151">Строка &quot;клиентов / «customerId»/заказы&quot; является шаблоном URI для маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="672b1-152">Web API пытается сопоставить запрос URI с шаблоном.</span><span class="sxs-lookup"><span data-stu-id="672b1-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="672b1-153">В этом примере "клиенты" и "заказы" являются буквальными сегментами, а "customerId" является переменным параметром.</span><span class="sxs-lookup"><span data-stu-id="672b1-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="672b1-154">Следующие URIs будут соответствовать этому шаблону:</span><span class="sxs-lookup"><span data-stu-id="672b1-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="672b1-155">Можно ограничить соответствие, используя [ограничения,](#constraints)описанные позже в этой теме.</span><span class="sxs-lookup"><span data-stu-id="672b1-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="672b1-156">Обратите внимание, что параметр &quot;«customerId»&quot; в шаблоне маршрута соответствует названию параметра *customerId* в методе.</span><span class="sxs-lookup"><span data-stu-id="672b1-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="672b1-157">Когда Web API вызывает действие контроллера, он пытается связать параметры маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="672b1-158">Например, если URI `http://example.com/customers/1/orders`является, Web API пытается связать значение "1" с параметром *customerId* в действии.</span><span class="sxs-lookup"><span data-stu-id="672b1-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="672b1-159">Шаблон URI может иметь несколько параметров:</span><span class="sxs-lookup"><span data-stu-id="672b1-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="672b1-160">Любые методы контроллера, не имеющие атрибута маршрута, используют маршрутную маршрутизм на основе конвенции.</span><span class="sxs-lookup"><span data-stu-id="672b1-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="672b1-161">Таким образом, можно объединить оба типа реуктора в одном проекте.</span><span class="sxs-lookup"><span data-stu-id="672b1-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="672b1-162">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="672b1-162">HTTP Methods</span></span>

<span data-ttu-id="672b1-163">Web API также выбирает действия на основе метода HTTP запроса (GET, POST и т.д.).</span><span class="sxs-lookup"><span data-stu-id="672b1-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="672b1-164">По умолчанию Web API ищет нечувствительный к нечувствительным совпадение с началом имени метода контроллера.</span><span class="sxs-lookup"><span data-stu-id="672b1-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="672b1-165">Например, метод контроллера, названный, `PutCustomers` соответствует запросу HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="672b1-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="672b1-166">Вы можете переопределить эту конвенцию, усвоив метод с любыми следующими атрибутами:</span><span class="sxs-lookup"><span data-stu-id="672b1-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="672b1-167">**(HttpDelete)**</span><span class="sxs-lookup"><span data-stu-id="672b1-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="672b1-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="672b1-168">**[HttpGet]**</span></span>
- <span data-ttu-id="672b1-169">**(Httphead)**</span><span class="sxs-lookup"><span data-stu-id="672b1-169">**[HttpHead]**</span></span>
- <span data-ttu-id="672b1-170">**(HttpOptions)**</span><span class="sxs-lookup"><span data-stu-id="672b1-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="672b1-171">**(Httppatch)**</span><span class="sxs-lookup"><span data-stu-id="672b1-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="672b1-172">**(HttpPost)**</span><span class="sxs-lookup"><span data-stu-id="672b1-172">**[HttpPost]**</span></span>
- <span data-ttu-id="672b1-173">**(Httpput)**</span><span class="sxs-lookup"><span data-stu-id="672b1-173">**[HttpPut]**</span></span>

<span data-ttu-id="672b1-174">Следующий пример отображает метод CreateBook для запросов HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="672b1-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="672b1-175">Для всех других методов HTTP, включая нестандартные методы, используйте атрибут **AcceptVerbs,** который использует список методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="672b1-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="672b1-176">Префиксы маршрута</span><span class="sxs-lookup"><span data-stu-id="672b1-176">Route Prefixes</span></span>

<span data-ttu-id="672b1-177">Часто маршруты в контроллере начинаются с одной и той же префикса.</span><span class="sxs-lookup"><span data-stu-id="672b1-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="672b1-178">Пример:</span><span class="sxs-lookup"><span data-stu-id="672b1-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="672b1-179">Вы можете установить общую префикс для всего контроллера, используя атрибут **«RoutePrefix»:**</span><span class="sxs-lookup"><span data-stu-id="672b1-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="672b1-180">Используйте tilde (я) на атрибуте метода, чтобы переопределить префикс маршрута:</span><span class="sxs-lookup"><span data-stu-id="672b1-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="672b1-181">Префикс маршрута может включать параметры:</span><span class="sxs-lookup"><span data-stu-id="672b1-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="672b1-182">Ограничения маршрута</span><span class="sxs-lookup"><span data-stu-id="672b1-182">Route Constraints</span></span>

<span data-ttu-id="672b1-183">Ограничения маршрута позволяют ограничить согласование параметров в шаблоне маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="672b1-184">Общий синтаксис является &quot;«параметр:ограничение».&quot;</span><span class="sxs-lookup"><span data-stu-id="672b1-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="672b1-185">Пример:</span><span class="sxs-lookup"><span data-stu-id="672b1-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="672b1-186">Здесь первый маршрут будет выбран только &quot;&quot; в том случае, если сегмент идентификатора URI является бесразмереным.</span><span class="sxs-lookup"><span data-stu-id="672b1-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="672b1-187">В противном случае будет выбран второй маршрут.</span><span class="sxs-lookup"><span data-stu-id="672b1-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="672b1-188">В следующей таблице перечислены ограничения, которые поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="672b1-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="672b1-189">Ограничение</span><span class="sxs-lookup"><span data-stu-id="672b1-189">Constraint</span></span> | <span data-ttu-id="672b1-190">Описание</span><span class="sxs-lookup"><span data-stu-id="672b1-190">Description</span></span> | <span data-ttu-id="672b1-191">Пример</span><span class="sxs-lookup"><span data-stu-id="672b1-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="672b1-192">alpha</span><span class="sxs-lookup"><span data-stu-id="672b1-192">alpha</span></span> | <span data-ttu-id="672b1-193">Матчи верхнего регистра или нижней регистра латинских алфавитных символов (a-z, A-)</span><span class="sxs-lookup"><span data-stu-id="672b1-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="672b1-194">х:альфа</span><span class="sxs-lookup"><span data-stu-id="672b1-194">{x:alpha}</span></span> |
| <span data-ttu-id="672b1-195">bool</span><span class="sxs-lookup"><span data-stu-id="672b1-195">bool</span></span> | <span data-ttu-id="672b1-196">Соответствует значению Boolean.</span><span class="sxs-lookup"><span data-stu-id="672b1-196">Matches a Boolean value.</span></span> | <span data-ttu-id="672b1-197">(x:bool)</span><span class="sxs-lookup"><span data-stu-id="672b1-197">{x:bool}</span></span> |
| <span data-ttu-id="672b1-198">DATETIME</span><span class="sxs-lookup"><span data-stu-id="672b1-198">datetime</span></span> | <span data-ttu-id="672b1-199">Соответствует значению **DateTime.**</span><span class="sxs-lookup"><span data-stu-id="672b1-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="672b1-200">время свидания:</span><span class="sxs-lookup"><span data-stu-id="672b1-200">{x:datetime}</span></span> |
| <span data-ttu-id="672b1-201">Decimal</span><span class="sxs-lookup"><span data-stu-id="672b1-201">decimal</span></span> | <span data-ttu-id="672b1-202">Соответствует десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="672b1-202">Matches a decimal value.</span></span> | <span data-ttu-id="672b1-203">x:десятичная)</span><span class="sxs-lookup"><span data-stu-id="672b1-203">{x:decimal}</span></span> |
| <span data-ttu-id="672b1-204">double</span><span class="sxs-lookup"><span data-stu-id="672b1-204">double</span></span> | <span data-ttu-id="672b1-205">Соответствует 64-битное значение плавающей точки.</span><span class="sxs-lookup"><span data-stu-id="672b1-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="672b1-206">х:двойной)</span><span class="sxs-lookup"><span data-stu-id="672b1-206">{x:double}</span></span> |
| <span data-ttu-id="672b1-207">FLOAT</span><span class="sxs-lookup"><span data-stu-id="672b1-207">float</span></span> | <span data-ttu-id="672b1-208">Соответствует 32-битное плавающее значение.</span><span class="sxs-lookup"><span data-stu-id="672b1-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="672b1-209">(x:float)</span><span class="sxs-lookup"><span data-stu-id="672b1-209">{x:float}</span></span> |
| <span data-ttu-id="672b1-210">guid</span><span class="sxs-lookup"><span data-stu-id="672b1-210">guid</span></span> | <span data-ttu-id="672b1-211">Соответствует значению GUID.</span><span class="sxs-lookup"><span data-stu-id="672b1-211">Matches a GUID value.</span></span> | <span data-ttu-id="672b1-212">(x:guid)</span><span class="sxs-lookup"><span data-stu-id="672b1-212">{x:guid}</span></span> |
| <span data-ttu-id="672b1-213">INT</span><span class="sxs-lookup"><span data-stu-id="672b1-213">int</span></span> | <span data-ttu-id="672b1-214">Соответствует 32-битное значение.</span><span class="sxs-lookup"><span data-stu-id="672b1-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="672b1-215">(x:int)</span><span class="sxs-lookup"><span data-stu-id="672b1-215">{x:int}</span></span> |
| <span data-ttu-id="672b1-216">length</span><span class="sxs-lookup"><span data-stu-id="672b1-216">length</span></span> | <span data-ttu-id="672b1-217">Соответствует строке с указанной длиной или в пределах заданного диапазона длин.</span><span class="sxs-lookup"><span data-stu-id="672b1-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="672b1-218">x:длина (6) x:длина (1,20)</span><span class="sxs-lookup"><span data-stu-id="672b1-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="672b1-219">long</span><span class="sxs-lookup"><span data-stu-id="672b1-219">long</span></span> | <span data-ttu-id="672b1-220">Соответствует 64-битное значение.</span><span class="sxs-lookup"><span data-stu-id="672b1-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="672b1-221">х:длинный)</span><span class="sxs-lookup"><span data-stu-id="672b1-221">{x:long}</span></span> |
| <span data-ttu-id="672b1-222">max</span><span class="sxs-lookup"><span data-stu-id="672b1-222">max</span></span> | <span data-ttu-id="672b1-223">Соответствует ряду с максимальным значением.</span><span class="sxs-lookup"><span data-stu-id="672b1-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="672b1-224">х:макс (10)</span><span class="sxs-lookup"><span data-stu-id="672b1-224">{x:max(10)}</span></span> |
| <span data-ttu-id="672b1-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="672b1-225">maxlength</span></span> | <span data-ttu-id="672b1-226">Соответствует строке с максимальной длиной.</span><span class="sxs-lookup"><span data-stu-id="672b1-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="672b1-227">x:maxlength (10)</span><span class="sxs-lookup"><span data-stu-id="672b1-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="672b1-228">Min</span><span class="sxs-lookup"><span data-stu-id="672b1-228">min</span></span> | <span data-ttu-id="672b1-229">Соответствует ряду с минимальным значением.</span><span class="sxs-lookup"><span data-stu-id="672b1-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="672b1-230">х:мин (10)</span><span class="sxs-lookup"><span data-stu-id="672b1-230">{x:min(10)}</span></span> |
| <span data-ttu-id="672b1-231">миндлина</span><span class="sxs-lookup"><span data-stu-id="672b1-231">minlength</span></span> | <span data-ttu-id="672b1-232">Соответствует строке с минимальной длиной.</span><span class="sxs-lookup"><span data-stu-id="672b1-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="672b1-233">(x:minlength))</span><span class="sxs-lookup"><span data-stu-id="672b1-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="672b1-234">range</span><span class="sxs-lookup"><span data-stu-id="672b1-234">range</span></span> | <span data-ttu-id="672b1-235">Соответствует целым числам в пределах диапазона значений.</span><span class="sxs-lookup"><span data-stu-id="672b1-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="672b1-236">диапазон (10,50)</span><span class="sxs-lookup"><span data-stu-id="672b1-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="672b1-237">regex</span><span class="sxs-lookup"><span data-stu-id="672b1-237">regex</span></span> | <span data-ttu-id="672b1-238">Соответствует регулярному выражению.</span><span class="sxs-lookup"><span data-stu-id="672b1-238">Matches a regular expression.</span></span> | <span data-ttu-id="672b1-239">x:regex ('d{3}-d{3}-d{4}$))</span><span class="sxs-lookup"><span data-stu-id="672b1-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="672b1-240">Обратите внимание, что некоторые &quot;ограничения,&quot;такие как мин, принимают аргументы в скобках.</span><span class="sxs-lookup"><span data-stu-id="672b1-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="672b1-241">Можно применить несколько ограничений к параметру, разделенному толстой кишка.</span><span class="sxs-lookup"><span data-stu-id="672b1-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="672b1-242">Пользовательские ограничения маршрутов</span><span class="sxs-lookup"><span data-stu-id="672b1-242">Custom Route Constraints</span></span>

<span data-ttu-id="672b1-243">Можно создать пользовательские ограничения маршрута, реализовав интерфейс **IHttpRouteConstraint.**</span><span class="sxs-lookup"><span data-stu-id="672b1-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="672b1-244">Например, следующее ограничение ограничивает параметр ненулевым значением рядом.</span><span class="sxs-lookup"><span data-stu-id="672b1-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="672b1-245">Следующий код показывает, как зарегистрировать ограничение:</span><span class="sxs-lookup"><span data-stu-id="672b1-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="672b1-246">Теперь вы можете применить ограничение в своих маршрутах:</span><span class="sxs-lookup"><span data-stu-id="672b1-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="672b1-247">Вы также можете заменить весь класс **DefaultInlineConstraintResolver,** внедрив интерфейс **IInlineConstraintResolver.**</span><span class="sxs-lookup"><span data-stu-id="672b1-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="672b1-248">Это заменит все встроенные ограничения, если только реализация **IInlineConstraintResolver** специально не добавит их.</span><span class="sxs-lookup"><span data-stu-id="672b1-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="672b1-249">Дополнительные параметры URI и значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="672b1-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="672b1-250">Можно сделать параметр URI необязательным, добавив вопросительный знак к параметру маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="672b1-251">Если параметр маршрута неявляется, необходимо определить значение по умолчанию для параметра метода.</span><span class="sxs-lookup"><span data-stu-id="672b1-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="672b1-252">В этом `/api/books/locale/1033` примере и `/api/books/locale` верните тот же ресурс.</span><span class="sxs-lookup"><span data-stu-id="672b1-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="672b1-253">Кроме того, в шаблоне маршрута можно указать значение по умолчанию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="672b1-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="672b1-254">Это почти то же самое, что и в предыдущем примере, но при применении значения по умолчанию существует небольшая разница в поведении.</span><span class="sxs-lookup"><span data-stu-id="672b1-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="672b1-255">В первом примере (""'lcid:int?) значение по умолчанию 1033 присваивается непосредственно параметру метода, поэтому параметр будет иметь это точное значение.</span><span class="sxs-lookup"><span data-stu-id="672b1-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="672b1-256">Во втором примере ("""lcid:int-1033") значение по умолчанию "1033" проходит процесс привязки модели.</span><span class="sxs-lookup"><span data-stu-id="672b1-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="672b1-257">Модель-связующего по умолчанию преобразует "1033" в числовое значение 1033.</span><span class="sxs-lookup"><span data-stu-id="672b1-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="672b1-258">Тем не менее, вы можете подключить пользовательские модели связующего, которые могли бы сделать что-то другое.</span><span class="sxs-lookup"><span data-stu-id="672b1-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="672b1-259">(В большинстве случаев, если у вас нет пользовательских связующих моделей в конвейере, эти две формы будут эквивалентными.)</span><span class="sxs-lookup"><span data-stu-id="672b1-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="672b1-260">Названия маршрутов</span><span class="sxs-lookup"><span data-stu-id="672b1-260">Route Names</span></span>

<span data-ttu-id="672b1-261">В Web API каждый маршрут имеет свое имя.</span><span class="sxs-lookup"><span data-stu-id="672b1-261">In Web API, every route has a name.</span></span> <span data-ttu-id="672b1-262">Имена маршрутов полезны для создания ссылок, так что вы можете включить ссылку в ответ HTTP.</span><span class="sxs-lookup"><span data-stu-id="672b1-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="672b1-263">Чтобы указать имя маршрута, установите свойство **имени** на атрибуте.</span><span class="sxs-lookup"><span data-stu-id="672b1-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="672b1-264">В следующем примере показано, как установить имя маршрута, а также как использовать имя маршрута при создании ссылки.</span><span class="sxs-lookup"><span data-stu-id="672b1-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="672b1-265">Заказ маршрута</span><span class="sxs-lookup"><span data-stu-id="672b1-265">Route Order</span></span>

<span data-ttu-id="672b1-266">Когда фреймворк пытается сопоставить URI с маршрутом, он оценивает маршруты в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="672b1-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="672b1-267">Чтобы указать порядок, установите свойство **Заказа** в атрибуте маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="672b1-268">В первую очередь оцениваются более низкие значения.</span><span class="sxs-lookup"><span data-stu-id="672b1-268">Lower values are evaluated first.</span></span> <span data-ttu-id="672b1-269">Значение заказа по умолчанию равен нулю.</span><span class="sxs-lookup"><span data-stu-id="672b1-269">The default order value is zero.</span></span>

<span data-ttu-id="672b1-270">Вот как определяется общий порядок:</span><span class="sxs-lookup"><span data-stu-id="672b1-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="672b1-271">Сравните свойство **заказа** атрибута маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="672b1-272">Посмотрите на каждый сегмент URI в шаблоне маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="672b1-273">Для каждого сегмента закажите следующее:</span><span class="sxs-lookup"><span data-stu-id="672b1-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="672b1-274">Литературные сегменты.</span><span class="sxs-lookup"><span data-stu-id="672b1-274">Literal segments.</span></span>
    2. <span data-ttu-id="672b1-275">Параметры маршрута с ограничениями.</span><span class="sxs-lookup"><span data-stu-id="672b1-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="672b1-276">Параметры маршрута без ограничений.</span><span class="sxs-lookup"><span data-stu-id="672b1-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="672b1-277">Сегменты параметров Wildcard с ограничениями.</span><span class="sxs-lookup"><span data-stu-id="672b1-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="672b1-278">Параметр Wildcard сегментируется без ограничений.</span><span class="sxs-lookup"><span data-stu-id="672b1-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="672b1-279">В случае галстука маршруты заказываются нечувствительным или нечувствительным сравнением строк ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) шаблона маршрута.</span><span class="sxs-lookup"><span data-stu-id="672b1-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="672b1-280">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="672b1-280">Here is an example.</span></span> <span data-ttu-id="672b1-281">Предположим, вы определяете следующий контроллер:</span><span class="sxs-lookup"><span data-stu-id="672b1-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="672b1-282">Эти маршруты упорядочены следующим образом.</span><span class="sxs-lookup"><span data-stu-id="672b1-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="672b1-283">заказы/детали</span><span class="sxs-lookup"><span data-stu-id="672b1-283">orders/details</span></span>
2. <span data-ttu-id="672b1-284">заказы/id</span><span class="sxs-lookup"><span data-stu-id="672b1-284">orders/{id}</span></span>
3. <span data-ttu-id="672b1-285">заказы/«Имя клиента»</span><span class="sxs-lookup"><span data-stu-id="672b1-285">orders/{customerName}</span></span>
4. <span data-ttu-id="672b1-286">заказы/дата\*</span><span class="sxs-lookup"><span data-stu-id="672b1-286">orders/{\*date}</span></span>
5. <span data-ttu-id="672b1-287">заказы/ожидающие</span><span class="sxs-lookup"><span data-stu-id="672b1-287">orders/pending</span></span>

<span data-ttu-id="672b1-288">Обратите внимание, что "детали" является буквальным сегментом и появляется перед "id", но "в ожидании" появляется последним, потому что свойство **Заказа** 1.</span><span class="sxs-lookup"><span data-stu-id="672b1-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="672b1-289">(Этот пример предполагает, что нет клиентов с именами "подробности" или "в ожидании".</span><span class="sxs-lookup"><span data-stu-id="672b1-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="672b1-290">В общем, старайтесь избегать неоднозначных маршрутов.</span><span class="sxs-lookup"><span data-stu-id="672b1-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="672b1-291">В этом примере лучшим `GetByCustomer` шаблоном маршрута является "клиенты /"CustomerName" )</span><span class="sxs-lookup"><span data-stu-id="672b1-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
