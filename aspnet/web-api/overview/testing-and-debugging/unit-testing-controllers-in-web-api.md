---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: Контроллеры модульного тестирования в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: В этом разделе описываются некоторые методы, связанные с контроллерами модульного тестирования в веб-API 2. Перед прочтением этой статьи вы можете прочитать раздел учебника...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3b89009a375e766f1c5b439dfe3fffd43b4963b3
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172930"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="f597a-104">Контроллеры модульного тестирования в ASP.NET веб-API 2</span><span class="sxs-lookup"><span data-stu-id="f597a-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="f597a-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f597a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="f597a-106">В этом разделе описываются некоторые методы, связанные с контроллерами модульного тестирования в веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="f597a-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="f597a-107">Перед прочтением этой статьи вы можете прочитать руководство [модульное тестирование веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md), в котором показано, как добавить проект модульного теста в решение.</span><span class="sxs-lookup"><span data-stu-id="f597a-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f597a-108">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="f597a-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="f597a-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f597a-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="f597a-110">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="f597a-110">Web API 2</span></span>
> - <span data-ttu-id="f597a-111">[MOQ](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="f597a-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="f597a-112">Я использовал MOQ, но та же идея применяется к любой инфраструктуре макетирования.</span><span class="sxs-lookup"><span data-stu-id="f597a-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="f597a-113">MOQ 4.5.30 (и более поздние версии) поддерживает Visual Studio 2017, Roslyn и .NET 4,5 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="f597a-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="f597a-114">Распространенный шаблон в модульных тестах — это оператор « &quot; организовать-акт-утверждение» &quot; :</span><span class="sxs-lookup"><span data-stu-id="f597a-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="f597a-115">Расположение. Настройте все необходимые компоненты для выполнения теста.</span><span class="sxs-lookup"><span data-stu-id="f597a-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="f597a-116">Акт: выполните тест.</span><span class="sxs-lookup"><span data-stu-id="f597a-116">Act: Perform the test.</span></span>
- <span data-ttu-id="f597a-117">Assert: Проверка успешности теста.</span><span class="sxs-lookup"><span data-stu-id="f597a-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="f597a-118">На этапе упорядочивания часто используются объекты макета или заглушки.</span><span class="sxs-lookup"><span data-stu-id="f597a-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="f597a-119">Это позволяет максимально сокращать количество зависимостей, поэтому тестирование посвящено тестированию одной вещи.</span><span class="sxs-lookup"><span data-stu-id="f597a-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="f597a-120">Ниже приведены некоторые вещи, которые следует выполнять при модульном тестировании на контроллерах веб-API.</span><span class="sxs-lookup"><span data-stu-id="f597a-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="f597a-121">Действие возвращает правильный тип ответа.</span><span class="sxs-lookup"><span data-stu-id="f597a-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="f597a-122">Недопустимые параметры возвращают правильный ответ об ошибке.</span><span class="sxs-lookup"><span data-stu-id="f597a-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="f597a-123">Действие вызывает правильный метод в репозитории или слое служб.</span><span class="sxs-lookup"><span data-stu-id="f597a-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="f597a-124">Если ответ содержит модель предметной области, проверьте тип модели.</span><span class="sxs-lookup"><span data-stu-id="f597a-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="f597a-125">Это некоторые из общих моментов тестирования, но конкретные особенности зависят от реализации контроллера.</span><span class="sxs-lookup"><span data-stu-id="f597a-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="f597a-126">В частности, это значительно отличается от того, возвращают ли действия контроллера **HttpResponseMessage** или **ихттпактионресулт**.</span><span class="sxs-lookup"><span data-stu-id="f597a-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="f597a-127">Дополнительные сведения об этих типах результатов см. [в разделе результаты действий в веб-API 2](../getting-started-with-aspnet-web-api/action-results.md).</span><span class="sxs-lookup"><span data-stu-id="f597a-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="f597a-128">Тестирование действий, возвращающих HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="f597a-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="f597a-129">Ниже приведен пример контроллера, действия которого возвращают **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="f597a-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="f597a-130">Обратите внимание, что контроллер использует внедрение зависимостей для внедрения `IProductRepository` .</span><span class="sxs-lookup"><span data-stu-id="f597a-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="f597a-131">Это делает контроллер более пригодным для тестирования, так как вы можете внедрить макет репозитория.</span><span class="sxs-lookup"><span data-stu-id="f597a-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="f597a-132">Следующий модульный тест проверяет, что `Get` метод записывает в `Product` текст ответа.</span><span class="sxs-lookup"><span data-stu-id="f597a-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="f597a-133">Предположим, что `repository` является макетом `IProductRepository` .</span><span class="sxs-lookup"><span data-stu-id="f597a-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="f597a-134">Важно установить **запрос** и **конфигурацию** на контроллере.</span><span class="sxs-lookup"><span data-stu-id="f597a-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="f597a-135">В противном случае тест завершится ошибкой с **ArgumentNullException** или **InvalidOperationException**.</span><span class="sxs-lookup"><span data-stu-id="f597a-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="f597a-136">Тестирование создания ссылки</span><span class="sxs-lookup"><span data-stu-id="f597a-136">Testing Link Generation</span></span>

<span data-ttu-id="f597a-137">`Post`Метод вызывает **Урлхелпер. Link** для создания ссылок в ответе.</span><span class="sxs-lookup"><span data-stu-id="f597a-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="f597a-138">Для этого требуется немного больше настроек модульного теста.</span><span class="sxs-lookup"><span data-stu-id="f597a-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="f597a-139">Классу **урлхелпер** требуется URL-адрес запроса и данные маршрута, поэтому тесту необходимо задать значения для них.</span><span class="sxs-lookup"><span data-stu-id="f597a-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="f597a-140">Другой вариант — макет или заглушка **урлхелпер**.</span><span class="sxs-lookup"><span data-stu-id="f597a-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="f597a-141">При таком подходе вы замените значение по умолчанию [ApiController. URL](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) на макет или версию заглушки, которая возвращает фиксированное значение.</span><span class="sxs-lookup"><span data-stu-id="f597a-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="f597a-142">Давайте перепишем тест с помощью платформы [MOQ](https://github.com/Moq) .</span><span class="sxs-lookup"><span data-stu-id="f597a-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="f597a-143">Установите `Moq` пакет NuGet в тестовом проекте.</span><span class="sxs-lookup"><span data-stu-id="f597a-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="f597a-144">В этой версии не нужно настраивать данные маршрута, так как макет **урлхелпер** Возвращает константную строку.</span><span class="sxs-lookup"><span data-stu-id="f597a-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="f597a-145">Тестирование действий, возвращающих Ихттпактионресулт</span><span class="sxs-lookup"><span data-stu-id="f597a-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="f597a-146">В веб-API 2 действие контроллера может вернуть **ихттпактионресулт**, что аналогично **ACTIONRESULT** в ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f597a-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="f597a-147">Интерфейс **ихттпактионресулт** определяет шаблон команды для создания HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="f597a-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="f597a-148">Вместо создания ответа напрямую контроллер возвращает **ихттпактионресулт**.</span><span class="sxs-lookup"><span data-stu-id="f597a-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="f597a-149">Позже конвейер вызывает **ихттпактионресулт** для создания ответа.</span><span class="sxs-lookup"><span data-stu-id="f597a-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="f597a-150">Такой подход упрощает написание модульных тестов, поскольку можно пропустить множество настроек, необходимых для **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="f597a-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="f597a-151">Ниже приведен пример контроллера, действия которого возвращают **ихттпактионресулт**.</span><span class="sxs-lookup"><span data-stu-id="f597a-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="f597a-152">В этом примере показаны некоторые распространенные шаблоны, использующие **ихттпактионресулт**.</span><span class="sxs-lookup"><span data-stu-id="f597a-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="f597a-153">Давайте посмотрим, как выполнять модульное тестирование.</span><span class="sxs-lookup"><span data-stu-id="f597a-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="f597a-154">Действие возвращает 200 (ОК) с текстом ответа.</span><span class="sxs-lookup"><span data-stu-id="f597a-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="f597a-155">`Get`Метод вызывает, `Ok(product)` Если продукт найден.</span><span class="sxs-lookup"><span data-stu-id="f597a-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="f597a-156">В модульном тесте убедитесь, что возвращаемый тип — **окнеготиатедконтентресулт** , а возвращенный продукт имеет правильный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f597a-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="f597a-157">Обратите внимание, что модульный тест не выполняет результат действия.</span><span class="sxs-lookup"><span data-stu-id="f597a-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="f597a-158">Можно предположить, что результат действия правильно создает ответ HTTP.</span><span class="sxs-lookup"><span data-stu-id="f597a-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="f597a-159">(Вот почему у платформы веб-API есть собственные модульные тесты!)</span><span class="sxs-lookup"><span data-stu-id="f597a-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="f597a-160">Действие возвращает 404 (не найдено)</span><span class="sxs-lookup"><span data-stu-id="f597a-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="f597a-161">`Get`Метод вызывает, `NotFound()` Если продукт не найден.</span><span class="sxs-lookup"><span data-stu-id="f597a-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="f597a-162">В этом случае модульный тест просто проверяет, является ли возвращаемый тип **нотфаундресулт**.</span><span class="sxs-lookup"><span data-stu-id="f597a-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="f597a-163">Действие возвращает 200 (ОК) без текста ответа</span><span class="sxs-lookup"><span data-stu-id="f597a-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="f597a-164">`Delete`Вызов метода `Ok()` возвращает пустой ответ HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="f597a-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="f597a-165">Как и в предыдущем примере, модульный тест проверяет возвращаемый тип, в данном случае **окресулт**.</span><span class="sxs-lookup"><span data-stu-id="f597a-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="f597a-166">Действие возвращает 201 (создано) с заголовком Location.</span><span class="sxs-lookup"><span data-stu-id="f597a-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="f597a-167">`Post`Вызов метода `CreatedAtRoute` ВОЗВРАЩАЕТ ответ HTTP 201 с URI в заголовке Location.</span><span class="sxs-lookup"><span data-stu-id="f597a-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="f597a-168">В модульном тесте убедитесь, что действие задает правильные значения маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="f597a-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="f597a-169">Действие возвращает другой 2xx с текстом ответа</span><span class="sxs-lookup"><span data-stu-id="f597a-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="f597a-170">`Put`Вызов метода `Content` ВОЗВРАЩАЕТ ответ HTTP 202 (принято) с текстом ответа.</span><span class="sxs-lookup"><span data-stu-id="f597a-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="f597a-171">Этот случай аналогичен возврату 200 (ОК), но модульный тест должен также проверять код состояния.</span><span class="sxs-lookup"><span data-stu-id="f597a-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="f597a-172">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f597a-172">Additional Resources</span></span>

- [<span data-ttu-id="f597a-173">Имитация Entity Framework при модульном тестировании веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="f597a-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="f597a-174">[Написание тестов для службы веб-API ASP.NET](https://docs.microsoft.com/en-gb/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service) (запись блога с помощью йоуссеф мауссаауи).</span><span class="sxs-lookup"><span data-stu-id="f597a-174">[Writing tests for an ASP.NET Web API service](https://docs.microsoft.com/en-gb/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="f597a-175">Debugging ASP.NET Web API with Route Debugger (Отладка веб-API ASP.NET с помощью Route Debugger)</span><span class="sxs-lookup"><span data-stu-id="f597a-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
