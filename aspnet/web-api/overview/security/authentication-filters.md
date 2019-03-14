---
uid: web-api/overview/security/authentication-filters
title: Фильтры проверки подлинности в ASP.NET Web API 2 | Документация Майкрософт
author: MikeWasson
description: Фильтр проверки подлинности — это компонент, который выполняет проверку подлинности HTTP-запроса. Веб-API 2 и MVC 5 поддерживают фильтры проверки подлинности, но они несколько отличаются...
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: a14facad4cbd0f9be1ff7bde2667f61ec8cc2a14
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030011"
---
<a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="671eb-104">Фильтры проверки подлинности в ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="671eb-104">Authentication Filters in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="671eb-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="671eb-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="671eb-106">Фильтр проверки подлинности — это компонент, который выполняет проверку подлинности HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="671eb-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="671eb-107">Веб-API 2 и MVC 5 поддерживают фильтры проверки подлинности, но они немного отличаться, главным образом в соглашения об именовании для интерфейса фильтра.</span><span class="sxs-lookup"><span data-stu-id="671eb-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="671eb-108">В этом разделе описаны фильтры проверки подлинности веб-API.</span><span class="sxs-lookup"><span data-stu-id="671eb-108">This topic describes Web API authentication filters.</span></span>


<span data-ttu-id="671eb-109">Фильтры проверки подлинности позволяют задать схему проверки подлинности для отдельных контроллеров или действий.</span><span class="sxs-lookup"><span data-stu-id="671eb-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="671eb-110">Таким образом, ваше приложение может поддерживать различных механизмов проверки подлинности для разных ресурсов HTTP.</span><span class="sxs-lookup"><span data-stu-id="671eb-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="671eb-111">В этой статье я покажу код из [обычной проверки подлинности](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) пример [ http://aspnet.codeplex.com ](http://aspnet.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="671eb-111">In this article, I'll show code from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample on [http://aspnet.codeplex.com](http://aspnet.codeplex.com).</span></span> <span data-ttu-id="671eb-112">В примере показан фильтр проверки подлинности, где реализована схема обычной проверки подлинности доступа к HTTP (RFC 2617).</span><span class="sxs-lookup"><span data-stu-id="671eb-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="671eb-113">Фильтр реализован в классе с именем `IdentityBasicAuthenticationAttribute`.</span><span class="sxs-lookup"><span data-stu-id="671eb-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="671eb-114">Я не буду приводить весь код из примера, лишь те компоненты, которые показывают, как написать фильтр проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="671eb-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="671eb-115">Параметр фильтр проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="671eb-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="671eb-116">Как и другие фильтры фильтры проверки подлинности может быть применен контроллера, за действие или глобально ко всем контроллерам веб-API.</span><span class="sxs-lookup"><span data-stu-id="671eb-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="671eb-117">Чтобы применить фильтр проверки подлинности к контроллеру, установите для класса контроллера атрибут фильтра.</span><span class="sxs-lookup"><span data-stu-id="671eb-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="671eb-118">В следующем коде наборы `[IdentityBasicAuthentication]` фильтра на класс контроллера, который включает обычную проверку подлинности для каждого действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="671eb-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="671eb-119">Чтобы применить фильтр к одно действие, Снабдите действие с фильтром.</span><span class="sxs-lookup"><span data-stu-id="671eb-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="671eb-120">В следующем коде наборы `[IdentityBasicAuthentication]` фильтра на контроллере `Post` метод.</span><span class="sxs-lookup"><span data-stu-id="671eb-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="671eb-121">Чтобы применить фильтр ко всем контроллерам веб-API, добавьте его **GlobalConfiguration.Filters**.</span><span class="sxs-lookup"><span data-stu-id="671eb-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="671eb-122">Реализация API проверки подлинности веб-фильтра</span><span class="sxs-lookup"><span data-stu-id="671eb-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="671eb-123">В веб-API проверки подлинности фильтры реализуют [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) интерфейс.</span><span class="sxs-lookup"><span data-stu-id="671eb-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="671eb-124">Они также должны наследоваться от **System.Attribute**, чтобы применить в качестве атрибутов.</span><span class="sxs-lookup"><span data-stu-id="671eb-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="671eb-125">**IAuthenticationFilter** интерфейс содержит два метода:</span><span class="sxs-lookup"><span data-stu-id="671eb-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="671eb-126">**AuthenticateAsync** проверяет подлинность запроса, проверяя учетные данные в запросе, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="671eb-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="671eb-127">**ChallengeAsync** добавляет запрос проверки подлинности для HTTP-ответа, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="671eb-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="671eb-128">Эти методы соответствуют поток проверки подлинности, определенные в [RFC 2612](http://tools.ietf.org/html/rfc2616) и [RFC 2617](http://tools.ietf.org/html/rfc2617):</span><span class="sxs-lookup"><span data-stu-id="671eb-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="671eb-129">Клиент отправляет учетные данные в заголовке авторизации.</span><span class="sxs-lookup"><span data-stu-id="671eb-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="671eb-130">Обычно это происходит после того как клиент получает ответ 401 (неавторизованный) с сервера.</span><span class="sxs-lookup"><span data-stu-id="671eb-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="671eb-131">Тем не менее клиент может отправлять учетные данные с любым запросом, не только после получения 401.</span><span class="sxs-lookup"><span data-stu-id="671eb-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="671eb-132">Если сервер не принимает учетные данные, возвращается ответ 401 (неавторизованный).</span><span class="sxs-lookup"><span data-stu-id="671eb-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="671eb-133">Ответ включает заголовок Www-Authenticate, который содержит один или несколько проблем.</span><span class="sxs-lookup"><span data-stu-id="671eb-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="671eb-134">Каждый запрос указывает схему проверки подлинности, распознаваемой сервером.</span><span class="sxs-lookup"><span data-stu-id="671eb-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="671eb-135">Сервер также может возвратить 401 от анонимного запроса.</span><span class="sxs-lookup"><span data-stu-id="671eb-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="671eb-136">На самом деле это обычно как инициируется процесс проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="671eb-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="671eb-137">Клиент отправляет анонимный запрос.</span><span class="sxs-lookup"><span data-stu-id="671eb-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="671eb-138">Сервер возвращает 401.</span><span class="sxs-lookup"><span data-stu-id="671eb-138">The server returns 401.</span></span>
3. <span data-ttu-id="671eb-139">Клиенты послал серверу ответ с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="671eb-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="671eb-140">Этот поток включает в себя *проверки подлинности* и *авторизации* действия.</span><span class="sxs-lookup"><span data-stu-id="671eb-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="671eb-141">Проверка подлинности удостоверяет подлинность клиента.</span><span class="sxs-lookup"><span data-stu-id="671eb-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="671eb-142">Авторизация определяет ли клиент обращаться к конкретному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="671eb-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="671eb-143">В веб-API фильтры проверки подлинности обработки проверки подлинности, но не авторизации.</span><span class="sxs-lookup"><span data-stu-id="671eb-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="671eb-144">Авторизации должно выполняться с фильтра авторизации или внутри действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="671eb-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="671eb-145">Ниже приведена последовательность действий в конвейере веб-API 2:</span><span class="sxs-lookup"><span data-stu-id="671eb-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="671eb-146">Перед вызовом действия, веб-API создает список фильтров проверки подлинности для этого действия.</span><span class="sxs-lookup"><span data-stu-id="671eb-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="671eb-147">Это включает в себя фильтры область действия, контроллера, область и глобальной области.</span><span class="sxs-lookup"><span data-stu-id="671eb-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="671eb-148">Веб-вызовы API **AuthenticateAsync** на каждый фильтр в списке.</span><span class="sxs-lookup"><span data-stu-id="671eb-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="671eb-149">Каждый фильтр может проверить учетные данные, в запросе.</span><span class="sxs-lookup"><span data-stu-id="671eb-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="671eb-150">Если любой фильтр успешно проверяет учетные данные, создает фильтр **IPrincipal** и присоединяет его к запросу.</span><span class="sxs-lookup"><span data-stu-id="671eb-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="671eb-151">Фильтр также можно вызывать ошибку на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="671eb-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="671eb-152">Если Да, остальной части конвейера не выполняется.</span><span class="sxs-lookup"><span data-stu-id="671eb-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="671eb-153">Предположим, что ошибки отсутствуют, запрос проходит через оставшуюся часть конвейера.</span><span class="sxs-lookup"><span data-stu-id="671eb-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="671eb-154">Наконец, веб-API вызывает каждый фильтр проверки подлинности **ChallengeAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="671eb-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="671eb-155">Фильтры используют этот метод для добавления сложной задачей в ответ, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="671eb-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="671eb-156">Обычно (но не всегда), может произойти в ответ на сообщение об ошибке 401.</span><span class="sxs-lookup"><span data-stu-id="671eb-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="671eb-157">Ниже приведены два возможных варианта.</span><span class="sxs-lookup"><span data-stu-id="671eb-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="671eb-158">В первом фильтр проверки подлинности успешно проверяет подлинность запроса, фильтра авторизации авторизует запрос, и действие контроллера возвращает код 200 (ОК).</span><span class="sxs-lookup"><span data-stu-id="671eb-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="671eb-159">Во втором примере фильтр проверки подлинности проверяет подлинность запроса, но фильтр авторизации возвращает 401 (не санкционировано).</span><span class="sxs-lookup"><span data-stu-id="671eb-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="671eb-160">В этом случае действие контроллера не вызывается.</span><span class="sxs-lookup"><span data-stu-id="671eb-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="671eb-161">Фильтр проверки подлинности добавляет в ответ заголовок Www-Authenticate.</span><span class="sxs-lookup"><span data-stu-id="671eb-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="671eb-162">Возможны и другие сочетания&mdash;к примеру, если действие контроллера поддерживает анонимные запросы, возможно, фильтр проверки подлинности, но без авторизации.</span><span class="sxs-lookup"><span data-stu-id="671eb-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="671eb-163">Реализация метода AuthenticateAsync</span><span class="sxs-lookup"><span data-stu-id="671eb-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="671eb-164">**AuthenticateAsync** метод пытается выполнить проверку подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="671eb-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="671eb-165">Ниже представлена подпись метода:</span><span class="sxs-lookup"><span data-stu-id="671eb-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="671eb-166">**AuthenticateAsync** метода необходимо выполнить одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="671eb-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="671eb-167">Нет (no-op).</span><span class="sxs-lookup"><span data-stu-id="671eb-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="671eb-168">Создание **IPrincipal** и задайте его в запросе.</span><span class="sxs-lookup"><span data-stu-id="671eb-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="671eb-169">Задайте результат ошибки.</span><span class="sxs-lookup"><span data-stu-id="671eb-169">Set an error result.</span></span>

<span data-ttu-id="671eb-170">(1) означает, что запрос не содержал никаких учетных данных, которые понимает фильтр.</span><span class="sxs-lookup"><span data-stu-id="671eb-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="671eb-171">(2) означает, что фильтр успешно прошел проверку подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="671eb-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="671eb-172">(3) означает, что запрос было недопустимые учетные данные (например, неправильный пароль), которое инициирует сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="671eb-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="671eb-173">Вот общую структуру для реализации **AuthenticateAsync**.</span><span class="sxs-lookup"><span data-stu-id="671eb-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="671eb-174">Найдите учетные данные в запросе.</span><span class="sxs-lookup"><span data-stu-id="671eb-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="671eb-175">Если нет учетных данных, ничего не делать и возвращают (нет-op).</span><span class="sxs-lookup"><span data-stu-id="671eb-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="671eb-176">Если учетные данные, но фильтр не поддерживает схему проверки подлинности, ничего не делать и возвращают (нет-op).</span><span class="sxs-lookup"><span data-stu-id="671eb-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="671eb-177">Еще один фильтр в конвейере может понять схему.</span><span class="sxs-lookup"><span data-stu-id="671eb-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="671eb-178">Если учетные данные, которые понимает фильтр, попробуйте проверку их подлинности.</span><span class="sxs-lookup"><span data-stu-id="671eb-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="671eb-179">Если указаны неверные учетные данные, возврата 401, задав `context.ErrorResult`.</span><span class="sxs-lookup"><span data-stu-id="671eb-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="671eb-180">Если учетные данные допустимы, создайте **IPrincipal** и задайте `context.Principal`.</span><span class="sxs-lookup"><span data-stu-id="671eb-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="671eb-181">В коде показано выполните **AuthenticateAsync** метода из [обычной проверки подлинности](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) образца.</span><span class="sxs-lookup"><span data-stu-id="671eb-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample.</span></span> <span data-ttu-id="671eb-182">Комментарии указывают на каждом шаге.</span><span class="sxs-lookup"><span data-stu-id="671eb-182">The comments indicate each step.</span></span> <span data-ttu-id="671eb-183">В коде показано несколько типов ошибок: Заголовок авторизации не учетные данные, имеет неправильный формат учетных данных и ввода неправильного имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="671eb-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="671eb-184">Параметр ошибки</span><span class="sxs-lookup"><span data-stu-id="671eb-184">Setting an Error Result</span></span>

<span data-ttu-id="671eb-185">Если учетные данные недействительны, необходимо задать фильтр `context.ErrorResult` для **IHttpActionResult** , создает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="671eb-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="671eb-186">Дополнительные сведения о **IHttpActionResult**, см. в разделе [результатов действий в веб-API 2](../getting-started-with-aspnet-web-api/action-results.md).</span><span class="sxs-lookup"><span data-stu-id="671eb-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="671eb-187">Пример обычной проверки подлинности включает в себя `AuthenticationFailureResult` класс, который подходит для этой цели.</span><span class="sxs-lookup"><span data-stu-id="671eb-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="671eb-188">Реализация ChallengeAsync</span><span class="sxs-lookup"><span data-stu-id="671eb-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="671eb-189">Цель **ChallengeAsync** методом является добавления проблемы проверки подлинности в ответ, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="671eb-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="671eb-190">Ниже представлена подпись метода:</span><span class="sxs-lookup"><span data-stu-id="671eb-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="671eb-191">Метод вызывается на каждый фильтр проверки подлинности в конвейере запросов.</span><span class="sxs-lookup"><span data-stu-id="671eb-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="671eb-192">Важно понимать, что **ChallengeAsync** называется *перед* HTTP-ответе будет создана и возможно, даже до выполнения действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="671eb-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="671eb-193">При **ChallengeAsync** вызове `context.Result` содержит **IHttpActionResult**, который будет использоваться позднее для создания HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="671eb-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="671eb-194">Поэтому если **ChallengeAsync** является именем, ничего не известно об ответе HTTP еще.</span><span class="sxs-lookup"><span data-stu-id="671eb-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="671eb-195">**ChallengeAsync** метод заменяют исходное значение `context.Result` с новым **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="671eb-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="671eb-196">Это **IHttpActionResult** нужно упаковать исходного `context.Result`.</span><span class="sxs-lookup"><span data-stu-id="671eb-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="671eb-197">Я назову исходного **IHttpActionResult** *внутренний результирующий*и новый **IHttpActionResult** *внешнего результата*.</span><span class="sxs-lookup"><span data-stu-id="671eb-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="671eb-198">Внешнее результат, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="671eb-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="671eb-199">Вызовите внутренний результирующий для создания HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="671eb-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="671eb-200">Изучите ответ.</span><span class="sxs-lookup"><span data-stu-id="671eb-200">Examine the response.</span></span>
3. <span data-ttu-id="671eb-201">Добавьте запрос проверки подлинности в ответ, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="671eb-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="671eb-202">Следующий пример взят из примера обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="671eb-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="671eb-203">Он определяет **IHttpActionResult** для внешнего результата.</span><span class="sxs-lookup"><span data-stu-id="671eb-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="671eb-204">`InnerResult` Свойство содержит внутренний **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="671eb-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="671eb-205">`Challenge` Свойство представляет заголовок Www-Authentication.</span><span class="sxs-lookup"><span data-stu-id="671eb-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="671eb-206">Обратите внимание, что **ExecuteAsync** сначала вызывает `InnerResult.ExecuteAsync` для создания HTTP-ответа, а затем добавляет проблема, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="671eb-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="671eb-207">Проверьте код ответа перед добавлением на запрос.</span><span class="sxs-lookup"><span data-stu-id="671eb-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="671eb-208">Большинство схем проверки подлинности добавьте только сложной задачей при ответе 401, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="671eb-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="671eb-209">Тем не менее некоторые схемы проверки подлинности следует добавлять к предоставлен, ответ сложной задачей.</span><span class="sxs-lookup"><span data-stu-id="671eb-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="671eb-210">Например, см. в разделе [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span><span class="sxs-lookup"><span data-stu-id="671eb-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="671eb-211">Учитывая `AddChallengeOnUnauthorizedResult` класса, фактический код в **ChallengeAsync** прост.</span><span class="sxs-lookup"><span data-stu-id="671eb-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="671eb-212">Просто создать результат и присоединить его к `context.Result`.</span><span class="sxs-lookup"><span data-stu-id="671eb-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="671eb-213">Примечание. Пример обычной проверки подлинности абстрагирует эта логика немного, путем помещения его в метод расширения.</span><span class="sxs-lookup"><span data-stu-id="671eb-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="671eb-214">Объединение фильтры проверки подлинности с помощью проверки подлинности на уровне сервера</span><span class="sxs-lookup"><span data-stu-id="671eb-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="671eb-215">«Проверка подлинности на уровне сервера» предшествует framework достигает веб-API запрос проверки подлинности, выполняемая узлом (например, IIS).</span><span class="sxs-lookup"><span data-stu-id="671eb-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="671eb-216">Часто можно включить проверку подлинности на уровне сервера для остальной части приложения, но отключить контроллеры веб-API.</span><span class="sxs-lookup"><span data-stu-id="671eb-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="671eb-217">Например типичный сценарий — включение форм проверки подлинности на уровне узла, но использовать проверку подлинности на основе маркеров для веб-API.</span><span class="sxs-lookup"><span data-stu-id="671eb-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="671eb-218">Чтобы отключить проверку подлинности на уровне сервера в рамках конвейера веб-API, вызовите `config.SuppressHostPrincipal()` в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="671eb-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="671eb-219">Это приводит к веб-API удалить **IPrincipal** из любой запрос, который входит в конвейер веб-API.</span><span class="sxs-lookup"><span data-stu-id="671eb-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="671eb-220">Фактически, он &quot;un-проверяет подлинность&quot; запроса.</span><span class="sxs-lookup"><span data-stu-id="671eb-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="671eb-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="671eb-221">Additional Resources</span></span>

<span data-ttu-id="671eb-222">[Фильтры безопасности ASP.NET Web API](https://msdn.microsoft.com/magazine/dn781361.aspx) (журнал MSDN)</span><span class="sxs-lookup"><span data-stu-id="671eb-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>