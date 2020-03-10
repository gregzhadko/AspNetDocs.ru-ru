---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Маршрутизация в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449250"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="a10f8-102">Маршрутизация в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a10f8-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="a10f8-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a10f8-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a10f8-104">В этой статье описывается, как веб-API ASP.NET маршрутизирует HTTP-запросы к контроллерам.</span><span class="sxs-lookup"><span data-stu-id="a10f8-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="a10f8-105">Если вы знакомы с ASP.NET MVC, маршрутизация веб-API очень похожа на маршрутизацию MVC.</span><span class="sxs-lookup"><span data-stu-id="a10f8-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="a10f8-106">Основное отличие заключается в том, что веб-API использует команду HTTP, а не путь URI, чтобы выбрать действие.</span><span class="sxs-lookup"><span data-stu-id="a10f8-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="a10f8-107">Можно также использовать маршрутизацию в стиле MVC в веб-API.</span><span class="sxs-lookup"><span data-stu-id="a10f8-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="a10f8-108">В этой статье не предполагается знание ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a10f8-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="a10f8-109">Таблицы маршрутизации</span><span class="sxs-lookup"><span data-stu-id="a10f8-109">Routing Tables</span></span>

<span data-ttu-id="a10f8-110">В веб-API ASP.NET *контроллер* — это класс, обрабатывающий HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="a10f8-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="a10f8-111">Открытые методы контроллера называются *методами действий* или просто *действиями*.</span><span class="sxs-lookup"><span data-stu-id="a10f8-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="a10f8-112">Когда платформа веб-API получает запрос, она направляет запрос в действие.</span><span class="sxs-lookup"><span data-stu-id="a10f8-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="a10f8-113">Чтобы определить, какое действие следует вызвать, платформа использует *таблицу маршрутизации*.</span><span class="sxs-lookup"><span data-stu-id="a10f8-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="a10f8-114">Шаблон проекта Visual Studio для веб-API создает маршрут по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="a10f8-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="a10f8-115">Этот маршрут определяется в файле *WebApiConfig.CS* , который размещается в каталоге *app\_Start* .</span><span class="sxs-lookup"><span data-stu-id="a10f8-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a10f8-116">Дополнительные сведения о классе `WebApiConfig` см. в разделе [настройка веб-API ASP.NET](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="a10f8-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="a10f8-117">При самостоятельном размещении веб-API необходимо задать таблицу маршрутизации непосредственно в объекте `HttpSelfHostConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="a10f8-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="a10f8-118">Дополнительные сведения см. [в разделе самостоятельное размещение веб-API](../older-versions/self-host-a-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="a10f8-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="a10f8-119">Каждая запись в таблице маршрутизации содержит *шаблон маршрута*.</span><span class="sxs-lookup"><span data-stu-id="a10f8-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="a10f8-120">Шаблоном маршрута по умолчанию для веб-API является &quot;API/{Controller}/{ID}&quot;.</span><span class="sxs-lookup"><span data-stu-id="a10f8-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="a10f8-121">В этом шаблоне &quot;API&quot; является сегментом пути литерала, а {Controller} и {ID} являются переменными-заполнителями.</span><span class="sxs-lookup"><span data-stu-id="a10f8-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="a10f8-122">Когда платформа веб-API получает запрос HTTP, она пытается сопоставить URI с одним из шаблонов маршрутов в таблице маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a10f8-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="a10f8-123">Если маршрут не найден, клиент получает ошибку 404.</span><span class="sxs-lookup"><span data-stu-id="a10f8-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="a10f8-124">Например, следующие URI соответствуют маршруту по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="a10f8-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="a10f8-125">/апи/контактс</span><span class="sxs-lookup"><span data-stu-id="a10f8-125">/api/contacts</span></span>
- <span data-ttu-id="a10f8-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="a10f8-126">/api/contacts/1</span></span>
- <span data-ttu-id="a10f8-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="a10f8-127">/api/products/gizmo1</span></span>

<span data-ttu-id="a10f8-128">Однако следующий URI не совпадает, поскольку в нем отсутствует сегмент&quot; &quot;API:</span><span class="sxs-lookup"><span data-stu-id="a10f8-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="a10f8-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="a10f8-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="a10f8-130">Причина использования "API" в маршруте заключается в предотвращении конфликтов с маршрутизацией ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a10f8-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="a10f8-131">Таким образом, можно иметь &quot;/контактс&quot; перейдите к контроллеру MVC и &quot;/АПИ/контактс&quot; перейдите к контроллеру веб-API.</span><span class="sxs-lookup"><span data-stu-id="a10f8-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="a10f8-132">Конечно, если вы не хотите это соглашение, можно изменить таблицу маршрутов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a10f8-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="a10f8-133">После обнаружения совпадающего маршрута веб-API выбирает контроллер и действие:</span><span class="sxs-lookup"><span data-stu-id="a10f8-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="a10f8-134">Чтобы найти контроллер, веб-API добавляет &quot;контроллера&quot; к значению переменной *{Controller}* .</span><span class="sxs-lookup"><span data-stu-id="a10f8-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="a10f8-135">Чтобы найти действие, веб-API просматривает команду HTTP, а затем ищет действие, имя которого начинается с имени HTTP-команды.</span><span class="sxs-lookup"><span data-stu-id="a10f8-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="a10f8-136">Например, при использовании запроса GET веб-API ищет действие с префиксом &quot;Get&quot;, например &quot;связи&quot; или &quot;Жеталлконтактс&quot;.</span><span class="sxs-lookup"><span data-stu-id="a10f8-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="a10f8-137">Это соглашение относится только к командам GET, POST, WHERE, DELETE, HEAD, OPTIONS и PATCH.</span><span class="sxs-lookup"><span data-stu-id="a10f8-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="a10f8-138">Вы можете включить другие HTTP-команды с помощью атрибутов на контроллере.</span><span class="sxs-lookup"><span data-stu-id="a10f8-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="a10f8-139">Позже мы увидим пример.</span><span class="sxs-lookup"><span data-stu-id="a10f8-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="a10f8-140">Другие переменные заполнителя в шаблоне маршрута, такие как *{ID},* сопоставляются с параметрами действия.</span><span class="sxs-lookup"><span data-stu-id="a10f8-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="a10f8-141">Давайте рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="a10f8-141">Let's look at an example.</span></span> <span data-ttu-id="a10f8-142">Предположим, что вы определили следующий контроллер:</span><span class="sxs-lookup"><span data-stu-id="a10f8-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="a10f8-143">Ниже приведены некоторые возможные HTTP-запросы, а также действие, которое вызывается для каждого из них:</span><span class="sxs-lookup"><span data-stu-id="a10f8-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="a10f8-144">HTTP-команда</span><span class="sxs-lookup"><span data-stu-id="a10f8-144">HTTP Verb</span></span> | <span data-ttu-id="a10f8-145">Путь URI</span><span class="sxs-lookup"><span data-stu-id="a10f8-145">URI Path</span></span> | <span data-ttu-id="a10f8-146">Действие</span><span class="sxs-lookup"><span data-stu-id="a10f8-146">Action</span></span> | <span data-ttu-id="a10f8-147">Параметр</span><span class="sxs-lookup"><span data-stu-id="a10f8-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a10f8-148">GET</span><span class="sxs-lookup"><span data-stu-id="a10f8-148">GET</span></span> | <span data-ttu-id="a10f8-149">API и продукты</span><span class="sxs-lookup"><span data-stu-id="a10f8-149">api/products</span></span> | <span data-ttu-id="a10f8-150">жеталлпродуктс</span><span class="sxs-lookup"><span data-stu-id="a10f8-150">GetAllProducts</span></span> | <span data-ttu-id="a10f8-151">*None*</span><span class="sxs-lookup"><span data-stu-id="a10f8-151">*(none)*</span></span> |
| <span data-ttu-id="a10f8-152">GET</span><span class="sxs-lookup"><span data-stu-id="a10f8-152">GET</span></span> | <span data-ttu-id="a10f8-153">API/Products/4</span><span class="sxs-lookup"><span data-stu-id="a10f8-153">api/products/4</span></span> | <span data-ttu-id="a10f8-154">жетпродуктбид</span><span class="sxs-lookup"><span data-stu-id="a10f8-154">GetProductById</span></span> | <span data-ttu-id="a10f8-155">4</span><span class="sxs-lookup"><span data-stu-id="a10f8-155">4</span></span> |
| <span data-ttu-id="a10f8-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="a10f8-156">DELETE</span></span> | <span data-ttu-id="a10f8-157">API/Products/4</span><span class="sxs-lookup"><span data-stu-id="a10f8-157">api/products/4</span></span> | <span data-ttu-id="a10f8-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="a10f8-158">DeleteProduct</span></span> | <span data-ttu-id="a10f8-159">4</span><span class="sxs-lookup"><span data-stu-id="a10f8-159">4</span></span> |
| <span data-ttu-id="a10f8-160">POST</span><span class="sxs-lookup"><span data-stu-id="a10f8-160">POST</span></span> | <span data-ttu-id="a10f8-161">API и продукты</span><span class="sxs-lookup"><span data-stu-id="a10f8-161">api/products</span></span> | <span data-ttu-id="a10f8-162">*(нет совпадения)*</span><span class="sxs-lookup"><span data-stu-id="a10f8-162">*(no match)*</span></span> |  |

<span data-ttu-id="a10f8-163">Обратите внимание, что сегмент *{ID}* URI, если он есть, сопоставлен с параметром *ID* действия.</span><span class="sxs-lookup"><span data-stu-id="a10f8-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="a10f8-164">В этом примере контроллер определяет два метода GET: один с параметром *ID* , а другой — без параметров.</span><span class="sxs-lookup"><span data-stu-id="a10f8-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="a10f8-165">Кроме того, обратите внимание, что запрос POST завершится ошибкой, так как контроллер не определяет метод &quot;POST...&quot;.</span><span class="sxs-lookup"><span data-stu-id="a10f8-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="a10f8-166">Варианты маршрутизации</span><span class="sxs-lookup"><span data-stu-id="a10f8-166">Routing Variations</span></span>

<span data-ttu-id="a10f8-167">В предыдущем разделе описан базовый механизм маршрутизации для веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a10f8-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="a10f8-168">В этом разделе описываются некоторые варианты.</span><span class="sxs-lookup"><span data-stu-id="a10f8-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="a10f8-169">команды HTTP</span><span class="sxs-lookup"><span data-stu-id="a10f8-169">HTTP verbs</span></span>

<span data-ttu-id="a10f8-170">Вместо использования соглашения об именовании для HTTP-команд можно явно указать команду HTTP для действия, добавив метод действия в один из следующих атрибутов:</span><span class="sxs-lookup"><span data-stu-id="a10f8-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="a10f8-171">В следующем примере метод `FindProduct` сопоставлен с запросами GET:</span><span class="sxs-lookup"><span data-stu-id="a10f8-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="a10f8-172">Чтобы разрешить несколько HTTP-команд для действия или разрешить HTTP-команды, отличные от GET, WHERE, POST, DELETE, HEAD, OPTIONS и PATCH, используйте атрибут `[AcceptVerbs]`, который принимает список HTTP-команд.</span><span class="sxs-lookup"><span data-stu-id="a10f8-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="a10f8-173">Маршрутизация по имени действия</span><span class="sxs-lookup"><span data-stu-id="a10f8-173">Routing by Action Name</span></span>

<span data-ttu-id="a10f8-174">При использовании шаблона маршрутизации по умолчанию веб-API использует команду HTTP для выбора действия.</span><span class="sxs-lookup"><span data-stu-id="a10f8-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="a10f8-175">Однако можно также создать маршрут, в котором имя действия включено в URI:</span><span class="sxs-lookup"><span data-stu-id="a10f8-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="a10f8-176">В этом шаблоне маршрута параметр *{Action}* присваивает имя методу действия на контроллере.</span><span class="sxs-lookup"><span data-stu-id="a10f8-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="a10f8-177">С этим стилем маршрутизации используйте атрибуты, чтобы указать разрешенные HTTP-команды.</span><span class="sxs-lookup"><span data-stu-id="a10f8-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="a10f8-178">Например, предположим, что контроллер имеет следующий метод:</span><span class="sxs-lookup"><span data-stu-id="a10f8-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="a10f8-179">В этом случае запрос GET для "API/Products/Details/1" будет сопоставлен методу `Details`.</span><span class="sxs-lookup"><span data-stu-id="a10f8-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="a10f8-180">Этот стиль маршрутизации аналогичен ASP.NET MVC и может быть подходящим для API-интерфейса в стиле RPC.</span><span class="sxs-lookup"><span data-stu-id="a10f8-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="a10f8-181">Имя действия можно переопределить с помощью атрибута `[ActionName]`.</span><span class="sxs-lookup"><span data-stu-id="a10f8-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="a10f8-182">В следующем примере есть два действия, которые сопоставляются с &quot;API/Products/thumbnail/*ID*. Один поддерживает GET, а другой поддерживает POST:</span><span class="sxs-lookup"><span data-stu-id="a10f8-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="a10f8-183">Не являющиеся действиями</span><span class="sxs-lookup"><span data-stu-id="a10f8-183">Non-Actions</span></span>

<span data-ttu-id="a10f8-184">Чтобы предотвратить вызов метода в качестве действия, используйте атрибут `[NonAction]`.</span><span class="sxs-lookup"><span data-stu-id="a10f8-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="a10f8-185">Это сигнализирует платформе, что метод не является действием, даже если он в противном случае будет соответствовать правилам маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a10f8-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="a10f8-186">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a10f8-186">Further Reading</span></span>

<span data-ttu-id="a10f8-187">В этом разделе предоставлено общее представление о маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a10f8-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="a10f8-188">Дополнительные сведения см. в разделе [Маршрутизация и выбор действий](routing-and-action-selection.md), описывающие, как платформа сопоставляет URI с маршрутом, выбирает контроллер, а затем выбирает действие для вызова.</span><span class="sxs-lookup"><span data-stu-id="a10f8-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
