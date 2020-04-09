---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Трассировка в ASP.NET Web API Документы Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675757"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="fcc54-102">Маршрутизация в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fcc54-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="fcc54-103">[Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fcc54-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fcc54-104">В этой статье описывается, как ASP.NET веб-API маршруты HTTP запросов контроллеров.</span><span class="sxs-lookup"><span data-stu-id="fcc54-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="fcc54-105">Если вы знакомы с ASP.NET MVC, то трассировка Web API очень похожа на трассировку MVC.</span><span class="sxs-lookup"><span data-stu-id="fcc54-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="fcc54-106">Основное отличие заключается в том, что Web API использует глагол HTTP, а не путь URI, чтобы выбрать действие.</span><span class="sxs-lookup"><span data-stu-id="fcc54-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="fcc54-107">В Web API можно также использовать трассу в стиле MVC.</span><span class="sxs-lookup"><span data-stu-id="fcc54-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="fcc54-108">Эта статья не предполагает каких-либо знаний о ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fcc54-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="fcc54-109">Таблицы для реанивания</span><span class="sxs-lookup"><span data-stu-id="fcc54-109">Routing Tables</span></span>

<span data-ttu-id="fcc54-110">В ASP.NET Web API *контроллер* представляет собой класс, который обрабатывает запросы HTTP.</span><span class="sxs-lookup"><span data-stu-id="fcc54-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="fcc54-111">Публичные методы контроллера называются *методами действия* или просто *действиями.*</span><span class="sxs-lookup"><span data-stu-id="fcc54-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="fcc54-112">Когда платформа Web API получает запрос, она направляет запрос на действие.</span><span class="sxs-lookup"><span data-stu-id="fcc54-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="fcc54-113">Чтобы определить, какое действие следует вызвать, в фреймворке используется *таблица размывания.*</span><span class="sxs-lookup"><span data-stu-id="fcc54-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="fcc54-114">Шаблон проекта Visual Studio для Web API создает маршрут по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="fcc54-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="fcc54-115">Этот маршрут определен в *WebApiConfig.cs* файле, который помещается в каталог *\_App Start:*</span><span class="sxs-lookup"><span data-stu-id="fcc54-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="fcc54-116">Для получения дополнительной `WebApiConfig` информации о классе см [ASP.NET.](../advanced/configuring-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="fcc54-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="fcc54-117">Если вы самостоятельно размещаете Web API, необходимо установить таблицу трассировки непосредственно на объекте. `HttpSelfHostConfiguration`</span><span class="sxs-lookup"><span data-stu-id="fcc54-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="fcc54-118">Для получения дополнительной информации [см.](../older-versions/self-host-a-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="fcc54-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="fcc54-119">Каждая запись в таблице маршрутов содержит *шаблон маршрута.*</span><span class="sxs-lookup"><span data-stu-id="fcc54-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="fcc54-120">Шаблон маршрута по умолчанию &quot;для Web API является api/(контроллер) / (id)&quot;.</span><span class="sxs-lookup"><span data-stu-id="fcc54-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="fcc54-121">В этом &quot;шаблоне&quot; api является буквальным сегментом пути, а «контроллер» и «id» являются переменными заполнителя.</span><span class="sxs-lookup"><span data-stu-id="fcc54-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="fcc54-122">Когда платформа Web API получает запрос HTTP, она пытается сопоставить URI с одним из шаблонов маршрутов в таблице маршрутов.</span><span class="sxs-lookup"><span data-stu-id="fcc54-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="fcc54-123">Если маршрут не совпадает, клиент получает ошибку 404.</span><span class="sxs-lookup"><span data-stu-id="fcc54-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="fcc54-124">Например, следующие URIs соответствуют маршруту по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="fcc54-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="fcc54-125">/api/контакты</span><span class="sxs-lookup"><span data-stu-id="fcc54-125">/api/contacts</span></span>
- <span data-ttu-id="fcc54-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="fcc54-126">/api/contacts/1</span></span>
- <span data-ttu-id="fcc54-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="fcc54-127">/api/products/gizmo1</span></span>

<span data-ttu-id="fcc54-128">Тем не менее, следующие URI не &quot;совпадает, потому что ему не хватает сегмента api:&quot;</span><span class="sxs-lookup"><span data-stu-id="fcc54-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="fcc54-129">/контакты/1</span><span class="sxs-lookup"><span data-stu-id="fcc54-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="fcc54-130">Причина использования "апи" в маршруте заключается в том, чтобы избежать столкновений с маршрутизированием ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fcc54-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="fcc54-131">Таким образом, вы &quot;можете&quot; иметь /контакты перейти к контроллеру MVC, и &quot;/api/контакты&quot; перейти к контроллеру Web API.</span><span class="sxs-lookup"><span data-stu-id="fcc54-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="fcc54-132">Конечно, если вам не нравится эта конвенция, вы можете изменить таблицу маршрутов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fcc54-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="fcc54-133">После того, как будет найден соответствующий маршрут, Web API выбирает контроллер и действие:</span><span class="sxs-lookup"><span data-stu-id="fcc54-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="fcc54-134">Чтобы найти контроллер, Web &quot;API добавляет контроллер&quot; к значению переменной *«контроллер».*</span><span class="sxs-lookup"><span data-stu-id="fcc54-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="fcc54-135">Чтобы найти действие, Web API смотрит на глагол HTTP, а затем ищет действие, имя которого начинается с имени глагола HTTP.</span><span class="sxs-lookup"><span data-stu-id="fcc54-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="fcc54-136">Например, с помощью запроса GET Web API &quot;&quot;ищет прикрепимые действия get, &quot;такие как GetContact&quot; или &quot;GetAllContacts.&quot;</span><span class="sxs-lookup"><span data-stu-id="fcc54-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="fcc54-137">Эта конвенция распространяется только на глаголы GET, POST, PUT, DELETE, HEAD, OPTIONS и PATCH.</span><span class="sxs-lookup"><span data-stu-id="fcc54-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="fcc54-138">Вы можете включить другие глаголы HTTP, используя атрибуты на контроллере.</span><span class="sxs-lookup"><span data-stu-id="fcc54-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="fcc54-139">Мы увидим пример этого позже.</span><span class="sxs-lookup"><span data-stu-id="fcc54-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="fcc54-140">Другие переменные заполнителя в шаблоне маршрута, такие как *«id»,* отображаются по параметрам действия.</span><span class="sxs-lookup"><span data-stu-id="fcc54-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="fcc54-141">Давайте рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="fcc54-141">Let's look at an example.</span></span> <span data-ttu-id="fcc54-142">Предположим, что вы определяете следующий контроллер:</span><span class="sxs-lookup"><span data-stu-id="fcc54-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="fcc54-143">Вот некоторые возможные запросы HTTP, а также действие, которое вызывается для каждого из них:</span><span class="sxs-lookup"><span data-stu-id="fcc54-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="fcc54-144">HTTP-команда</span><span class="sxs-lookup"><span data-stu-id="fcc54-144">HTTP Verb</span></span> | <span data-ttu-id="fcc54-145">Путь URI</span><span class="sxs-lookup"><span data-stu-id="fcc54-145">URI Path</span></span> | <span data-ttu-id="fcc54-146">Действие</span><span class="sxs-lookup"><span data-stu-id="fcc54-146">Action</span></span> | <span data-ttu-id="fcc54-147">Параметр</span><span class="sxs-lookup"><span data-stu-id="fcc54-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fcc54-148">GET</span><span class="sxs-lookup"><span data-stu-id="fcc54-148">GET</span></span> | <span data-ttu-id="fcc54-149">апи/продукты</span><span class="sxs-lookup"><span data-stu-id="fcc54-149">api/products</span></span> | <span data-ttu-id="fcc54-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="fcc54-150">GetAllProducts</span></span> | <span data-ttu-id="fcc54-151">*(нет)*</span><span class="sxs-lookup"><span data-stu-id="fcc54-151">*(none)*</span></span> |
| <span data-ttu-id="fcc54-152">GET</span><span class="sxs-lookup"><span data-stu-id="fcc54-152">GET</span></span> | <span data-ttu-id="fcc54-153">api/продукты/4</span><span class="sxs-lookup"><span data-stu-id="fcc54-153">api/products/4</span></span> | <span data-ttu-id="fcc54-154">GetProductbyid</span><span class="sxs-lookup"><span data-stu-id="fcc54-154">GetProductById</span></span> | <span data-ttu-id="fcc54-155">4</span><span class="sxs-lookup"><span data-stu-id="fcc54-155">4</span></span> |
| <span data-ttu-id="fcc54-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="fcc54-156">DELETE</span></span> | <span data-ttu-id="fcc54-157">api/продукты/4</span><span class="sxs-lookup"><span data-stu-id="fcc54-157">api/products/4</span></span> | <span data-ttu-id="fcc54-158">УдалитьПродукт</span><span class="sxs-lookup"><span data-stu-id="fcc54-158">DeleteProduct</span></span> | <span data-ttu-id="fcc54-159">4</span><span class="sxs-lookup"><span data-stu-id="fcc54-159">4</span></span> |
| <span data-ttu-id="fcc54-160">POST</span><span class="sxs-lookup"><span data-stu-id="fcc54-160">POST</span></span> | <span data-ttu-id="fcc54-161">апи/продукты</span><span class="sxs-lookup"><span data-stu-id="fcc54-161">api/products</span></span> | <span data-ttu-id="fcc54-162">*(без совпадений)*</span><span class="sxs-lookup"><span data-stu-id="fcc54-162">*(no match)*</span></span> |  |

<span data-ttu-id="fcc54-163">Обратите внимание, что сегмент *URI,* если он присутствует, отображается по параметру *идентификатора* действия.</span><span class="sxs-lookup"><span data-stu-id="fcc54-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="fcc54-164">В этом примере контроллер определяет два метода GET, один с параметром *идентификатора* и один без параметров.</span><span class="sxs-lookup"><span data-stu-id="fcc54-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="fcc54-165">Кроме того, обратите внимание, что запрос POST не &quot;удастся, потому что контроллер не определяет сообщение ... &quot; метод.</span><span class="sxs-lookup"><span data-stu-id="fcc54-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="fcc54-166">Вариации реаутинга</span><span class="sxs-lookup"><span data-stu-id="fcc54-166">Routing Variations</span></span>

<span data-ttu-id="fcc54-167">В предыдущем разделе описан базовый механизм реуктора для ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="fcc54-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="fcc54-168">В этом разделе описаны некоторые вариации.</span><span class="sxs-lookup"><span data-stu-id="fcc54-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="fcc54-169">Команды HTTP</span><span class="sxs-lookup"><span data-stu-id="fcc54-169">HTTP verbs</span></span>

<span data-ttu-id="fcc54-170">Вместо того, чтобы использовать конвенцию именования для глаголов HTTP, можно прямо указать глагол HTTP для действия, усвоив метод действия одним из следующих атрибутов:</span><span class="sxs-lookup"><span data-stu-id="fcc54-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="fcc54-171">В следующем примере `FindProduct` метод отображается на запросах GET:</span><span class="sxs-lookup"><span data-stu-id="fcc54-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="fcc54-172">Чтобы разрешить несколько глаголов HTTP для действия, или разрешить глаголы HTTP, кроме GET, PUT, `[AcceptVerbs]` POST, DELETE, HEAD, OPTIONS и PATCH, используйте атрибут, который использует список глаголов HTTP.</span><span class="sxs-lookup"><span data-stu-id="fcc54-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="fcc54-173">Расшатывание по названию действия</span><span class="sxs-lookup"><span data-stu-id="fcc54-173">Routing by Action Name</span></span>

<span data-ttu-id="fcc54-174">С шаблоном трассировки по умолчанию Web API использует глагол HTTP для выбора действия.</span><span class="sxs-lookup"><span data-stu-id="fcc54-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="fcc54-175">Тем не менее, вы также можете создать маршрут, где имя действия включено в URI:</span><span class="sxs-lookup"><span data-stu-id="fcc54-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="fcc54-176">В этом шаблоне маршрута параметр *«действие»* называет метод действия на контроллере.</span><span class="sxs-lookup"><span data-stu-id="fcc54-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="fcc54-177">С этим стилем разгрома используйте атрибуты для указания допустимых глаголов HTTP.</span><span class="sxs-lookup"><span data-stu-id="fcc54-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="fcc54-178">Например, предположим, что у контроллера есть следующий метод:</span><span class="sxs-lookup"><span data-stu-id="fcc54-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="fcc54-179">В этом случае запрос GET на "api/products/details/1" `Details` будет отображаться к методу.</span><span class="sxs-lookup"><span data-stu-id="fcc54-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="fcc54-180">Этот стиль конечной связи похож на ASP.NET MVC и может быть подходящим для API в стиле RPC.</span><span class="sxs-lookup"><span data-stu-id="fcc54-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="fcc54-181">Вы можете переопределить имя действия `[ActionName]` с помощью атрибута.</span><span class="sxs-lookup"><span data-stu-id="fcc54-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="fcc54-182">В следующем примере, Есть два &quot;действия, которые карта для api / продукты / thumbnail /*id*. Один поддерживает GET, а другой поддерживает POST:</span><span class="sxs-lookup"><span data-stu-id="fcc54-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="fcc54-183">Недействия</span><span class="sxs-lookup"><span data-stu-id="fcc54-183">Non-Actions</span></span>

<span data-ttu-id="fcc54-184">Чтобы предотвратить вызов метода в качестве действия, используйте `[NonAction]` атрибут.</span><span class="sxs-lookup"><span data-stu-id="fcc54-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="fcc54-185">Это сигнализирует системе, что метод не является действием, даже если он в противном случае соответствует правилам разгрома.</span><span class="sxs-lookup"><span data-stu-id="fcc54-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="fcc54-186">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="fcc54-186">Further Reading</span></span>

<span data-ttu-id="fcc54-187">Эта тема предоставила представление на высоком уровне о разгроме.</span><span class="sxs-lookup"><span data-stu-id="fcc54-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="fcc54-188">Для получения более подробной информации см. [Маршрутирование и выбор действий,](routing-and-action-selection.md)в котором точно описывается, как фреймворк соответствует URI маршруту, выбирает контроллер, а затем выбирает действие для вызывания.</span><span class="sxs-lookup"><span data-stu-id="fcc54-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
