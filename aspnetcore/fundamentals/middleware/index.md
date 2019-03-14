---
title: ПО промежуточного слоя ASP.NET Core
author: rick-anderson
description: Сведения о ПО промежуточного слоя ASP.NET Core и конвейере запросов.
ms.author: riande
ms.custom: mvc
ms.date: 02/17/2019
uid: fundamentals/middleware/index
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="5c32a-103">ПО промежуточного слоя ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5c32a-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="5c32a-104">Авторы: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Стив Смит](https://ardalis.com/) (Steve Smith)</span><span class="sxs-lookup"><span data-stu-id="5c32a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="5c32a-105">ПО промежуточного слоя — это программное обеспечение, выстраиваемое в виде конвейера приложения для обработки запросов и откликов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="5c32a-106">Каждый компонент:</span><span class="sxs-lookup"><span data-stu-id="5c32a-106">Each component:</span></span>

* <span data-ttu-id="5c32a-107">определяет, нужно ли передать запрос следующему компоненту в конвейере;</span><span class="sxs-lookup"><span data-stu-id="5c32a-107">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="5c32a-108">может выполнять работу как до, так и после вызова следующего компонента в конвейере.</span><span class="sxs-lookup"><span data-stu-id="5c32a-108">Can perform work before and after the next component in the pipeline.</span></span>

<span data-ttu-id="5c32a-109">Для построения конвейера запросов используются делегаты запроса.</span><span class="sxs-lookup"><span data-stu-id="5c32a-109">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="5c32a-110">Они обрабатывают каждый HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="5c32a-110">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="5c32a-111">Для их настройки служат методы расширения <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> и <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span><span class="sxs-lookup"><span data-stu-id="5c32a-111">Request delegates are configured using <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>, and <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> extension methods.</span></span> <span data-ttu-id="5c32a-112">Отдельный делегат запроса можно указать встроенным в качестве анонимного метода (называемого встроенным ПО промежуточного слоя) либо определить в многоразовом классе.</span><span class="sxs-lookup"><span data-stu-id="5c32a-112">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="5c32a-113">Эти многоразовые классы и встроенные анонимные методы являются *ПО промежуточного слоя* или *компонентами промежуточного слоя*.</span><span class="sxs-lookup"><span data-stu-id="5c32a-113">These reusable classes and in-line anonymous methods are *middleware*, also called *middleware components*.</span></span> <span data-ttu-id="5c32a-114">Каждый компонент ПО промежуточного слоя в конвейере запросов отвечает за вызов следующего компонента в конвейере или замыкает конвейер.</span><span class="sxs-lookup"><span data-stu-id="5c32a-114">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the pipeline.</span></span> <span data-ttu-id="5c32a-115">Когда промежуточный слой замыкает конвейер, он становится *терминальным промежуточным слоем*, так как препятствует обработке запроса дальнейшими компонентами промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="5c32a-115">When a middleware short-circuits, it's called a *terminal middleware* because it prevents further middleware from processing the request.</span></span>

<span data-ttu-id="5c32a-116">Статья <xref:migration/http-modules> поясняет различия между конвейерами запросов в ASP.NET Core и ASP.NET 4.x, а также содержит дополнительные примеры ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="5c32a-116"><xref:migration/http-modules> explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="5c32a-117">Создание конвейера ПО промежуточного слоя с помощью IApplicationBuilder</span><span class="sxs-lookup"><span data-stu-id="5c32a-117">Create a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="5c32a-118">Конвейер запросов ASP.NET Core состоит из последовательности делегатов запроса, вызываемых один за другим.</span><span class="sxs-lookup"><span data-stu-id="5c32a-118">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="5c32a-119">На следующей схеме демонстрируется этот принцип.</span><span class="sxs-lookup"><span data-stu-id="5c32a-119">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="5c32a-120">Поток выполнения показан черными стрелками.</span><span class="sxs-lookup"><span data-stu-id="5c32a-120">The thread of execution follows the black arrows.</span></span>

![Шаблон обработки запросов, показывающий входящий запрос, обработку в трех компонентах промежуточного слоя и запрос, покидающий приложение.](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="5c32a-124">Каждый из делегатов может выполнять операции до и после следующего делегата.</span><span class="sxs-lookup"><span data-stu-id="5c32a-124">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="5c32a-125">Делегаты обработки исключений должны вызываться в начале конвейера, чтобы перехватывать исключения, возникающие на более поздних этапах.</span><span class="sxs-lookup"><span data-stu-id="5c32a-125">Exception-handling delegates should be called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="5c32a-126">Простейшее приложение ASP.NET Core задает один делегат запроса, обрабатывающий все запросы.</span><span class="sxs-lookup"><span data-stu-id="5c32a-126">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="5c32a-127">В этом случае конвейер запросов как таковой отсутствует.</span><span class="sxs-lookup"><span data-stu-id="5c32a-127">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="5c32a-128">Вместо этого в ответ на каждый HTTP-запрос вызывается одна анонимная функция.</span><span class="sxs-lookup"><span data-stu-id="5c32a-128">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

<span data-ttu-id="5c32a-129">Первый делегат <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> завершает конвейер.</span><span class="sxs-lookup"><span data-stu-id="5c32a-129">The first <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> delegate terminates the pipeline.</span></span>

<span data-ttu-id="5c32a-130">Несколько делегатов запроса можно соединить в цепочку с помощью <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span><span class="sxs-lookup"><span data-stu-id="5c32a-130">Chain multiple request delegates together with <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span></span> <span data-ttu-id="5c32a-131">Параметр `next` представляет следующий делегат в конвейере.</span><span class="sxs-lookup"><span data-stu-id="5c32a-131">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="5c32a-132">Замыкать конвейер можно*не* вызывая параметр *next*.</span><span class="sxs-lookup"><span data-stu-id="5c32a-132">You can short-circuit the pipeline by *not* calling the *next* parameter.</span></span> <span data-ttu-id="5c32a-133">Обычно действия можно выполнять как до, так и после следующего делегата, как показано в этом примере.</span><span class="sxs-lookup"><span data-stu-id="5c32a-133">You can typically perform actions both before and after the next delegate, as the following example demonstrates:</span></span>

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

<span data-ttu-id="5c32a-134">Если делегат не передает запрос следующему делегату, это называется *замыканием конвейера запросов*.</span><span class="sxs-lookup"><span data-stu-id="5c32a-134">When a delegate doesn't pass a request to the next delegate, it's called *short-circuiting the request pipeline*.</span></span> <span data-ttu-id="5c32a-135">Замыкание часто является предпочтительным, так как позволяет избежать ненужной работы.</span><span class="sxs-lookup"><span data-stu-id="5c32a-135">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="5c32a-136">Например, [компонент промежуточного слоя для статических файлов](xref:fundamentals/static-files) может выступать в роли *терминального промежуточного слоя*, обрабатывая запрос статического файла и замыкая оставшуюся часть конвейера.</span><span class="sxs-lookup"><span data-stu-id="5c32a-136">For example, [Static File Middleware](xref:fundamentals/static-files) can act as a *terminal middleware* by processing a request for a static file and short-circuiting the rest of the pipeline.</span></span> <span data-ttu-id="5c32a-137">Компоненты промежуточного слоя, предшествующие терминальному промежуточному слою, по-прежнему обрабатывают код после их инструкций `next.Invoke`.</span><span class="sxs-lookup"><span data-stu-id="5c32a-137">Middleware added to the pipeline before the middleware that terminates further processing still processes code after their `next.Invoke` statements.</span></span> <span data-ttu-id="5c32a-138">Но учитывайте следующее предупреждение о попытке записи в ответ, который уже был отправлен.</span><span class="sxs-lookup"><span data-stu-id="5c32a-138">However, see the following warning about attempting to write to a response that has already been sent.</span></span>

> [!WARNING]
> <span data-ttu-id="5c32a-139">Не вызывайте `next.Invoke` после отправки отклика клиенту.</span><span class="sxs-lookup"><span data-stu-id="5c32a-139">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="5c32a-140">Изменения <xref:Microsoft.AspNetCore.Http.HttpResponse> после запуска отклика приведут к возникновению исключения.</span><span class="sxs-lookup"><span data-stu-id="5c32a-140">Changes to <xref:Microsoft.AspNetCore.Http.HttpResponse> after the response has started throw an exception.</span></span> <span data-ttu-id="5c32a-141">Например, таким изменением может быть задание HTTP-заголовков и кода состояния.</span><span class="sxs-lookup"><span data-stu-id="5c32a-141">For example, changes such as setting headers and a status code throw an exception.</span></span> <span data-ttu-id="5c32a-142">Запись в тело отклика после вызова `next`:</span><span class="sxs-lookup"><span data-stu-id="5c32a-142">Writing to the response body after calling `next`:</span></span>
>
> * <span data-ttu-id="5c32a-143">может вызвать нарушение протокола,</span><span class="sxs-lookup"><span data-stu-id="5c32a-143">May cause a protocol violation.</span></span> <span data-ttu-id="5c32a-144">например, при записи больше указанного значения `Content-Length`;</span><span class="sxs-lookup"><span data-stu-id="5c32a-144">For example, writing more than the stated `Content-Length`.</span></span>
> * <span data-ttu-id="5c32a-145">может привести к нарушению формата,</span><span class="sxs-lookup"><span data-stu-id="5c32a-145">May corrupt the body format.</span></span> <span data-ttu-id="5c32a-146">например, при записи нижнего колонтитула HTML в CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="5c32a-146">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="5c32a-147"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> удобно использовать для обозначения того, были ли отправлены заголовки или выполнена запись в тело отклика.</span><span class="sxs-lookup"><span data-stu-id="5c32a-147"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> is a useful hint to indicate if headers have been sent or the body has been written to.</span></span>

## <a name="order"></a><span data-ttu-id="5c32a-148">Номер</span><span class="sxs-lookup"><span data-stu-id="5c32a-148">Order</span></span>

<span data-ttu-id="5c32a-149">Порядок, в котором компоненты промежуточного слоя добавляются в метод `Startup.Configure`, определяет порядок их вызова при запросах и обратный порядок для отклика.</span><span class="sxs-lookup"><span data-stu-id="5c32a-149">The order that middleware components are added in the `Startup.Configure` method defines the order in which the middleware components are invoked on requests and the reverse order for the response.</span></span> <span data-ttu-id="5c32a-150">Соблюдение этого порядка крайне важно для обеспечения безопасности, производительности и функциональности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-150">The order is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="5c32a-151">Метод `Startup.Configure` добавляет компоненты ПО промежуточного слоя для распространенных сценариев приложений:</span><span class="sxs-lookup"><span data-stu-id="5c32a-151">The following `Startup.Configure` method adds middleware components for common app scenarios:</span></span>

::: moniker range=">= aspnetcore-2.0"

1. <span data-ttu-id="5c32a-152">Обработка исключений/ошибок</span><span class="sxs-lookup"><span data-stu-id="5c32a-152">Exception/error handling</span></span>
1. <span data-ttu-id="5c32a-153">Протокол HTTP Strict Transport Security.</span><span class="sxs-lookup"><span data-stu-id="5c32a-153">HTTP Strict Transport Security Protocol</span></span>
1. <span data-ttu-id="5c32a-154">Перенаправление HTTPS</span><span class="sxs-lookup"><span data-stu-id="5c32a-154">HTTPS redirection</span></span>
1. <span data-ttu-id="5c32a-155">Статический файловый сервер</span><span class="sxs-lookup"><span data-stu-id="5c32a-155">Static file server</span></span>
1. <span data-ttu-id="5c32a-156">Применение политик в отношении файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="5c32a-156">Cookie policy enforcement</span></span>
1. <span data-ttu-id="5c32a-157">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="5c32a-157">Authentication</span></span>
1. <span data-ttu-id="5c32a-158">Сеанс</span><span class="sxs-lookup"><span data-stu-id="5c32a-158">Session</span></span>
1. <span data-ttu-id="5c32a-159">MVC</span><span class="sxs-lookup"><span data-stu-id="5c32a-159">MVC</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    if (env.IsDevelopment())
    {
        // When the app runs in the Development environment:
        //   Use the Developer Exception Page to report app runtime errors.
        //   Use the Database Error Page to report database runtime errors.
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
    }
    else
    {
        // When the app doesn't run in the Development environment:
        //   Enable the Exception Handler Middleware to catch exceptions
        //     thrown in the following middlewares.
        //   Use the HTTP Strict Transport Security Protocol (HSTS)
        //     Middleware.
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // Use HTTPS Redirection Middleware to redirect HTTP requests to HTTPS.
    app.UseHttpsRedirection();

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Use Cookie Policy Middleware to conform to EU General Data 
    // Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // If the app uses session state, call Session Middleware after Cookie 
    // Policy Middleware and before MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. <span data-ttu-id="5c32a-160">Обработка исключений/ошибок</span><span class="sxs-lookup"><span data-stu-id="5c32a-160">Exception/error handling</span></span>
1. <span data-ttu-id="5c32a-161">Статические файлы</span><span class="sxs-lookup"><span data-stu-id="5c32a-161">Static files</span></span>
1. <span data-ttu-id="5c32a-162">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="5c32a-162">Authentication</span></span>
1. <span data-ttu-id="5c32a-163">Сеанс</span><span class="sxs-lookup"><span data-stu-id="5c32a-163">Session</span></span>
1. <span data-ttu-id="5c32a-164">MVC</span><span class="sxs-lookup"><span data-stu-id="5c32a-164">MVC</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Enable the Exception Handler Middleware to catch exceptions
    //   thrown in the following middlewares.
    app.UseExceptionHandler("/Home/Error");

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Authenticate before you access secure resources.
    app.UseIdentity();

    // If the app uses session state, call UseSession before 
    // MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

<span data-ttu-id="5c32a-165">В предыдущем примере кода каждый метод расширения ПО промежуточного слоя представляется в <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> с использованием пространства имен <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="5c32a-165">In the preceding example code, each middleware extension method is exposed on <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> through the <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> namespace.</span></span>

<span data-ttu-id="5c32a-166"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> — это первый компонент промежуточного слоя, добавленный в конвейер.</span><span class="sxs-lookup"><span data-stu-id="5c32a-166"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> is the first middleware component added to the pipeline.</span></span> <span data-ttu-id="5c32a-167">Таким образом, обработчик исключений ПО промежуточного слоя перехватывает все исключения, возникающие в последующих вызовах.</span><span class="sxs-lookup"><span data-stu-id="5c32a-167">Therefore, the Exception Handler Middleware catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="5c32a-168">Компонент промежуточного слоя для статических файлов вызывается на раннем этапе конвейера, чтобы он мог обработать запросы и выполнить замыкание, минуя остальные компоненты.</span><span class="sxs-lookup"><span data-stu-id="5c32a-168">Static File Middleware is called early in the pipeline so that it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="5c32a-169">Этот компонент **не** выполняет проверки авторизации.</span><span class="sxs-lookup"><span data-stu-id="5c32a-169">The Static File Middleware provides **no** authorization checks.</span></span> <span data-ttu-id="5c32a-170">Все обрабатываемые им файлы, включая расположенные в *wwwroot*, находятся в открытом доступе.</span><span class="sxs-lookup"><span data-stu-id="5c32a-170">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="5c32a-171">Сведения о защите статических файлов см. в статье <xref:fundamentals/static-files>.</span><span class="sxs-lookup"><span data-stu-id="5c32a-171">For an approach to secure static files, see <xref:fundamentals/static-files>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="5c32a-172">Если запрос не обрабатывается компонентом промежуточного слоя для статических файлов, он передается в компонент промежуточного слоя для проверки подлинности (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), который выполняет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-172">If the request isn't handled by the Static File Middleware, it's passed on to the Authentication Middleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), which performs authentication.</span></span> <span data-ttu-id="5c32a-173">Этот компонент не замыкает запросы, не прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-173">Authentication doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="5c32a-174">Хотя ПО промежуточного слоя для проверки подлинности проверяет подлинность запросов, авторизация (и отклонение) выполняются только после того, как MVC выберет указанную страницу Razor Page или контроллер MVC и действие.</span><span class="sxs-lookup"><span data-stu-id="5c32a-174">Although Authentication Middleware authenticates requests, authorization (and rejection) occurs only after MVC selects a specific Razor Page or MVC controller and action.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="5c32a-175">Если запрос не обрабатывается компонентом промежуточного слоя для статических файлов, он передается в компонент промежуточного слоя для удостоверений (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), который выполняет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-175">If the request isn't handled by Static File Middleware, it's passed on to the Identity Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), which performs authentication.</span></span> <span data-ttu-id="5c32a-176">Этот компонент не замыкает запросы, не прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-176">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="5c32a-177">Хотя он проверяет подлинность запросов, авторизация (и отклонение) выполняются только после того, как MVC выберет указанный контроллер и действие.</span><span class="sxs-lookup"><span data-stu-id="5c32a-177">Although Identity authenticates requests, authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

::: moniker-end

<span data-ttu-id="5c32a-178">Следующий пример показывает порядок компонентов промежуточного слоя, где запросы для статических файлов обрабатываются компонентом для статических файлов до компонента для сжатия откликов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-178">The following example demonstrates a middleware order where requests for static files are handled by Static File Middleware before Response Compression Middleware.</span></span> <span data-ttu-id="5c32a-179">Статические файлы не сжимаются с этим порядком ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="5c32a-179">Static files aren't compressed with this middleware order.</span></span> <span data-ttu-id="5c32a-180">Отклики MVC из <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> можно сжать.</span><span class="sxs-lookup"><span data-stu-id="5c32a-180">The MVC responses from <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static File Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a><span data-ttu-id="5c32a-181">Методы Use, Run и Map</span><span class="sxs-lookup"><span data-stu-id="5c32a-181">Use, Run, and Map</span></span>

<span data-ttu-id="5c32a-182">Для настройки конвейера HTTP служат методы `Use`, `Run` и `Map`.</span><span class="sxs-lookup"><span data-stu-id="5c32a-182">Configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="5c32a-183">Метод `Use` может замыкать конвейер (это происходит, если он не вызывает делегат запроса `next`).</span><span class="sxs-lookup"><span data-stu-id="5c32a-183">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="5c32a-184">`Run` является соглашением, и некоторые компоненты промежуточного слоя могут предоставлять методы `Run[Middleware]`, которые выполняются в конце конвейера.</span><span class="sxs-lookup"><span data-stu-id="5c32a-184">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="5c32a-185">Расширения <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> используются в качестве соглашения для ветвления конвейера.</span><span class="sxs-lookup"><span data-stu-id="5c32a-185"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="5c32a-186">`Map*` осуществляет ветвление конвейера запросов на основе совпадений для заданного пути запроса.</span><span class="sxs-lookup"><span data-stu-id="5c32a-186">`Map*` branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="5c32a-187">Если путь запроса начинается с заданного пути, данная ветвь выполняется.</span><span class="sxs-lookup"><span data-stu-id="5c32a-187">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="5c32a-188">Ниже приведены запросы и отклики `http://localhost:1234` на базе предыдущего кода.</span><span class="sxs-lookup"><span data-stu-id="5c32a-188">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="5c32a-189">Запрос</span><span class="sxs-lookup"><span data-stu-id="5c32a-189">Request</span></span>             | <span data-ttu-id="5c32a-190">Ответ</span><span class="sxs-lookup"><span data-stu-id="5c32a-190">Response</span></span>                     |
| ------------------- | ---------------------------- |
| <span data-ttu-id="5c32a-191">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="5c32a-191">localhost:1234</span></span>      | <span data-ttu-id="5c32a-192">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="5c32a-192">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="5c32a-193">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="5c32a-193">localhost:1234/map1</span></span> | <span data-ttu-id="5c32a-194">Map Test 1</span><span class="sxs-lookup"><span data-stu-id="5c32a-194">Map Test 1</span></span>                   |
| <span data-ttu-id="5c32a-195">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="5c32a-195">localhost:1234/map2</span></span> | <span data-ttu-id="5c32a-196">Map Test 2</span><span class="sxs-lookup"><span data-stu-id="5c32a-196">Map Test 2</span></span>                   |
| <span data-ttu-id="5c32a-197">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="5c32a-197">localhost:1234/map3</span></span> | <span data-ttu-id="5c32a-198">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="5c32a-198">Hello from non-Map delegate.</span></span> |

<span data-ttu-id="5c32a-199">Когда используется `Map`, соответствующие сегменты путей удаляются из `HttpRequest.Path` и добавляются к `HttpRequest.PathBase` для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="5c32a-199">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="5c32a-200">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) осуществляет ветвление конвейера запросов на основе результата заданного предиката.</span><span class="sxs-lookup"><span data-stu-id="5c32a-200">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="5c32a-201">Любой предикат типа `Func<HttpContext, bool>` можно использовать для сопоставления запросов с новой ветвью конвейера.</span><span class="sxs-lookup"><span data-stu-id="5c32a-201">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="5c32a-202">В следующем примере предикат служит для определения наличия переменной строки запроса `branch`.</span><span class="sxs-lookup"><span data-stu-id="5c32a-202">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="5c32a-203">Ниже приведены запросы и отклики `http://localhost:1234` на базе предыдущего кода.</span><span class="sxs-lookup"><span data-stu-id="5c32a-203">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="5c32a-204">Запрос</span><span class="sxs-lookup"><span data-stu-id="5c32a-204">Request</span></span>                       | <span data-ttu-id="5c32a-205">Ответ</span><span class="sxs-lookup"><span data-stu-id="5c32a-205">Response</span></span>                     |
| ----------------------------- | ---------------------------- |
| <span data-ttu-id="5c32a-206">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="5c32a-206">localhost:1234</span></span>                | <span data-ttu-id="5c32a-207">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="5c32a-207">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="5c32a-208">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="5c32a-208">localhost:1234/?branch=master</span></span> | <span data-ttu-id="5c32a-209">Branch used = master</span><span class="sxs-lookup"><span data-stu-id="5c32a-209">Branch used = master</span></span>         |

<span data-ttu-id="5c32a-210">`Map` поддерживает вложение, например:</span><span class="sxs-lookup"><span data-stu-id="5c32a-210">`Map` supports nesting, for example:</span></span>

```csharp
app.Map("/level1", level1App => {
    level1App.Map("/level2a", level2AApp => {
        // "/level1/level2a" processing
    });
    level1App.Map("/level2b", level2BApp => {
        // "/level1/level2b" processing
    });
});
   ```

<span data-ttu-id="5c32a-211">`Map` также может сопоставить несколько сегментов одновременно:</span><span class="sxs-lookup"><span data-stu-id="5c32a-211">`Map` can also match multiple segments at once:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a><span data-ttu-id="5c32a-212">Встроенное ПО промежуточного слоя</span><span class="sxs-lookup"><span data-stu-id="5c32a-212">Built-in middleware</span></span>

<span data-ttu-id="5c32a-213">ASP.NET Core содержит следующие компоненты промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="5c32a-213">ASP.NET Core ships with the following middleware components.</span></span> <span data-ttu-id="5c32a-214">В столбце *Порядок* указаны сведения о размещении ПО промежуточного слоя в конвейере обработки запросов и условия, в соответствии с которыми ПО промежуточного слоя может прервать обработку запроса.</span><span class="sxs-lookup"><span data-stu-id="5c32a-214">The *Order* column provides notes on middleware placement in the request processing pipeline and under what conditions the middleware may terminate request processing.</span></span> <span data-ttu-id="5c32a-215">Если промежуточный слой замыкает конвейер обработки запроса и препятствует обработке запроса дальнейшими компонентами промежуточного слоя, он называется *терминальным промежуточным слоем*.</span><span class="sxs-lookup"><span data-stu-id="5c32a-215">When a middleware short-circuits the request processing pipeline and prevents further downstream middleware from processing a request, it's called a *terminal middleware*.</span></span> <span data-ttu-id="5c32a-216">Дополнительные сведения о замыкании конвейера см. в разделе [Создание конвейера ПО промежуточного слоя с помощью IApplicationBuilder](#create-a-middleware-pipeline-with-iapplicationbuilder).</span><span class="sxs-lookup"><span data-stu-id="5c32a-216">For more information on short-circuiting, see the [Create a middleware pipeline with IApplicationBuilder](#create-a-middleware-pipeline-with-iapplicationbuilder) section.</span></span>

| <span data-ttu-id="5c32a-217">ПО промежуточного слоя</span><span class="sxs-lookup"><span data-stu-id="5c32a-217">Middleware</span></span> | <span data-ttu-id="5c32a-218">Описание:</span><span class="sxs-lookup"><span data-stu-id="5c32a-218">Description</span></span> | <span data-ttu-id="5c32a-219">Номер</span><span class="sxs-lookup"><span data-stu-id="5c32a-219">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="5c32a-220">Authentication</span><span class="sxs-lookup"><span data-stu-id="5c32a-220">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="5c32a-221">Обеспечивает поддержку проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-221">Provides authentication support.</span></span> | <span data-ttu-id="5c32a-222">Ставится перед тем, как потребуется `HttpContext.User`.</span><span class="sxs-lookup"><span data-stu-id="5c32a-222">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="5c32a-223">Является конечным для обратных вызовов OAuth.</span><span class="sxs-lookup"><span data-stu-id="5c32a-223">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="5c32a-224">Cookie Policy</span><span class="sxs-lookup"><span data-stu-id="5c32a-224">Cookie Policy</span></span>](xref:security/gdpr) | <span data-ttu-id="5c32a-225">Позволяет отслеживать согласие пользователей на хранение личных сведений и применять минимальные стандарты для полей файлов cookie, таких как `secure` и `SameSite`.</span><span class="sxs-lookup"><span data-stu-id="5c32a-225">Tracks consent from users for storing personal information and enforces minimum standards for cookie fields, such as `secure` and `SameSite`.</span></span> | <span data-ttu-id="5c32a-226">Перед ПО промежуточного слоя, которое использует файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="5c32a-226">Before middleware that issues cookies.</span></span> <span data-ttu-id="5c32a-227">Примеры Authentication, Session, MVC (TempData).</span><span class="sxs-lookup"><span data-stu-id="5c32a-227">Examples: Authentication, Session, MVC (TempData).</span></span> |
| [<span data-ttu-id="5c32a-228">CORS</span><span class="sxs-lookup"><span data-stu-id="5c32a-228">CORS</span></span>](xref:security/cors) | <span data-ttu-id="5c32a-229">Настраивает общий доступ к ресурсам независимо от источника.</span><span class="sxs-lookup"><span data-stu-id="5c32a-229">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="5c32a-230">Ставится перед компонентами, использующими CORS.</span><span class="sxs-lookup"><span data-stu-id="5c32a-230">Before components that use CORS.</span></span> |
| [<span data-ttu-id="5c32a-231">Error Handling</span><span class="sxs-lookup"><span data-stu-id="5c32a-231">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="5c32a-232">Настраивает диагностику.</span><span class="sxs-lookup"><span data-stu-id="5c32a-232">Configures diagnostics.</span></span> | <span data-ttu-id="5c32a-233">Ставится перед компонентами, выдающими ошибки.</span><span class="sxs-lookup"><span data-stu-id="5c32a-233">Before components that generate errors.</span></span> |
| [<span data-ttu-id="5c32a-234">Forwarded Headers</span><span class="sxs-lookup"><span data-stu-id="5c32a-234">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="5c32a-235">Пересылает заголовки, переданные через прокси-сервер, в текущий запрос.</span><span class="sxs-lookup"><span data-stu-id="5c32a-235">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="5c32a-236">Перед компонентами, использующими обновленные поля.</span><span class="sxs-lookup"><span data-stu-id="5c32a-236">Before components that consume the updated fields.</span></span> <span data-ttu-id="5c32a-237">Например: схема, узел, IP-адрес клиента, метод.</span><span class="sxs-lookup"><span data-stu-id="5c32a-237">Examples: scheme, host, client IP, method.</span></span> |
| [<span data-ttu-id="5c32a-238">Проверка работоспособности</span><span class="sxs-lookup"><span data-stu-id="5c32a-238">Health Check</span></span>](xref:host-and-deploy/health-checks) | <span data-ttu-id="5c32a-239">Проверяет работоспособность приложения ASP.NET Core и его зависимостей, таких как проверка доступности базы данных.</span><span class="sxs-lookup"><span data-stu-id="5c32a-239">Checks the health of an ASP.NET Core app and its dependencies, such as checking database availability.</span></span> | <span data-ttu-id="5c32a-240">Является конечным, если запрос соответствует конечной точке проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="5c32a-240">Terminal if a request matches a health check endpoint.</span></span> |
| [<span data-ttu-id="5c32a-241">HTTP Method Override</span><span class="sxs-lookup"><span data-stu-id="5c32a-241">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="5c32a-242">Разрешает входящий запрос POST для переопределения этого метода.</span><span class="sxs-lookup"><span data-stu-id="5c32a-242">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="5c32a-243">Ставится перед компонентами, использующими обновленный метод.</span><span class="sxs-lookup"><span data-stu-id="5c32a-243">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="5c32a-244">HTTPS Redirection</span><span class="sxs-lookup"><span data-stu-id="5c32a-244">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="5c32a-245">Перенаправление всех запросов HTTP на HTTPS (ASP.NET Core 2.1 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="5c32a-245">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="5c32a-246">Ставится перед компонентами, использующими URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5c32a-246">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="5c32a-247">HTTP Strict Transport Security (HSTS)</span><span class="sxs-lookup"><span data-stu-id="5c32a-247">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="5c32a-248">ПО промежуточного слоя для усовершенствования безопасности, которое добавляет специальный заголовок ответа (ASP.NET Core 2.1 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="5c32a-248">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="5c32a-249">Перед отправкой ответов и после компонентов, изменяющих запросы.</span><span class="sxs-lookup"><span data-stu-id="5c32a-249">Before responses are sent and after components that modify requests.</span></span> <span data-ttu-id="5c32a-250">Примеры Forwarded Headers, URL Rewriting.</span><span class="sxs-lookup"><span data-stu-id="5c32a-250">Examples: Forwarded Headers, URL Rewriting.</span></span> |
| [<span data-ttu-id="5c32a-251">MVC</span><span class="sxs-lookup"><span data-stu-id="5c32a-251">MVC</span></span>](xref:mvc/overview) | <span data-ttu-id="5c32a-252">Обрабатывает запросы с помощью MVC/Razor Pages (ASP.NET Core 2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="5c32a-252">Processes requests with MVC/Razor Pages (ASP.NET Core 2.0 or later).</span></span> | <span data-ttu-id="5c32a-253">Является конечным, если запрос соответствует маршруту.</span><span class="sxs-lookup"><span data-stu-id="5c32a-253">Terminal if a request matches a route.</span></span> |
| [<span data-ttu-id="5c32a-254">OWIN</span><span class="sxs-lookup"><span data-stu-id="5c32a-254">OWIN</span></span>](xref:fundamentals/owin) | <span data-ttu-id="5c32a-255">Взаимодействие с приложениями, серверами и ПО промежуточного слоя на основе OWIN.</span><span class="sxs-lookup"><span data-stu-id="5c32a-255">Interop with OWIN-based apps, servers, and middleware.</span></span> | <span data-ttu-id="5c32a-256">Является конечным, если ПО промежуточного слоя OWIN полностью обрабатывает запрос.</span><span class="sxs-lookup"><span data-stu-id="5c32a-256">Terminal if the OWIN Middleware fully processes the request.</span></span> |
| [<span data-ttu-id="5c32a-257">Кэширование ответов</span><span class="sxs-lookup"><span data-stu-id="5c32a-257">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="5c32a-258">Обеспечивает поддержку для кэширования откликов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-258">Provides support for caching responses.</span></span> | <span data-ttu-id="5c32a-259">Ставится перед компонентами, требующими кэширование.</span><span class="sxs-lookup"><span data-stu-id="5c32a-259">Before components that require caching.</span></span> |
| [<span data-ttu-id="5c32a-260">Сжатие откликов</span><span class="sxs-lookup"><span data-stu-id="5c32a-260">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="5c32a-261">Обеспечивает поддержку для сжатия откликов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-261">Provides support for compressing responses.</span></span> | <span data-ttu-id="5c32a-262">Ставится перед компонентами, требующими сжатие.</span><span class="sxs-lookup"><span data-stu-id="5c32a-262">Before components that require compression.</span></span> |
| [<span data-ttu-id="5c32a-263">Localization</span><span class="sxs-lookup"><span data-stu-id="5c32a-263">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="5c32a-264">Обеспечивает поддержку локализации.</span><span class="sxs-lookup"><span data-stu-id="5c32a-264">Provides localization support.</span></span> | <span data-ttu-id="5c32a-265">Ставится перед компонентами, для которых важна локализация.</span><span class="sxs-lookup"><span data-stu-id="5c32a-265">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="5c32a-266">Routing</span><span class="sxs-lookup"><span data-stu-id="5c32a-266">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="5c32a-267">Определяет и ограничивает маршруты запросов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-267">Defines and constrains request routes.</span></span> | <span data-ttu-id="5c32a-268">Является конечным для совпадающих маршрутов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-268">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="5c32a-269">Session</span><span class="sxs-lookup"><span data-stu-id="5c32a-269">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="5c32a-270">Обеспечивает поддержку для управления пользовательскими сеансами.</span><span class="sxs-lookup"><span data-stu-id="5c32a-270">Provides support for managing user sessions.</span></span> | <span data-ttu-id="5c32a-271">Ставится перед компонентами, требующими сеанс.</span><span class="sxs-lookup"><span data-stu-id="5c32a-271">Before components that require Session.</span></span> |
| [<span data-ttu-id="5c32a-272">Static Files</span><span class="sxs-lookup"><span data-stu-id="5c32a-272">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="5c32a-273">Обеспечивает поддержку для обработки статических файлов и просмотра каталогов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-273">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="5c32a-274">Является конечным, если запрос соответствует файлу.</span><span class="sxs-lookup"><span data-stu-id="5c32a-274">Terminal if a request matches a file.</span></span> |
| [<span data-ttu-id="5c32a-275">URL Rewriting</span><span class="sxs-lookup"><span data-stu-id="5c32a-275">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="5c32a-276">Обеспечивает поддержку для переопределения URL-адресов и перенаправления запросов.</span><span class="sxs-lookup"><span data-stu-id="5c32a-276">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="5c32a-277">Ставится перед компонентами, использующими URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5c32a-277">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="5c32a-278">WebSockets</span><span class="sxs-lookup"><span data-stu-id="5c32a-278">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="5c32a-279">Обеспечивает поддержку протокола WebSockets.</span><span class="sxs-lookup"><span data-stu-id="5c32a-279">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="5c32a-280">Ставится перед компонентами, которым нужно принимать запросы WebSocket.</span><span class="sxs-lookup"><span data-stu-id="5c32a-280">Before components that are required to accept WebSocket requests.</span></span> |

## <a name="additional-resources"></a><span data-ttu-id="5c32a-281">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5c32a-281">Additional resources</span></span>

* <xref:fundamentals/middleware/write>
* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
