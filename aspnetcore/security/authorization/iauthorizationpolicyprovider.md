---
title: Поставщики пользовательской политики авторизации в ASP.NET Core
author: mjrousos
description: Сведения об использовании пользовательских IAuthorizationPolicyProvider в приложении ASP.NET Core для динамического создания политик авторизации.
ms.author: riande
ms.custom: mvc
ms.date: 01/21/2019
uid: security/authorization/iauthorizationpolicyprovider
ms.openlocfilehash: ca57a9fd8e3c11f15fe14bbe4538bc748c4c84b6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039131"
---
# <a name="custom-authorization-policy-providers-using-iauthorizationpolicyprovider-in-aspnet-core"></a><span data-ttu-id="85457-103">Настраиваемые поставщики политики авторизации, используя IAuthorizationPolicyProvider в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="85457-103">Custom Authorization Policy Providers using IAuthorizationPolicyProvider in ASP.NET Core</span></span> 

<span data-ttu-id="85457-104">По [Майк Роусос](https://github.com/mjrousos)</span><span class="sxs-lookup"><span data-stu-id="85457-104">By [Mike Rousos](https://github.com/mjrousos)</span></span>

<span data-ttu-id="85457-105">Обычно при использовании [авторизации на основе политики](xref:security/authorization/policies), регистрации политики путем вызова `AuthorizationOptions.AddPolicy` как часть конфигурации службы авторизации.</span><span class="sxs-lookup"><span data-stu-id="85457-105">Typically when using [policy-based authorization](xref:security/authorization/policies), policies are registered by calling `AuthorizationOptions.AddPolicy` as part of authorization service configuration.</span></span> <span data-ttu-id="85457-106">В некоторых случаях может оказаться возможно (или желательно) для регистрации всех политик авторизации таким образом.</span><span class="sxs-lookup"><span data-stu-id="85457-106">In some scenarios, it may not be possible (or desirable) to register all authorization policies in this way.</span></span> <span data-ttu-id="85457-107">В таких случаях можно использовать пользовательский `IAuthorizationPolicyProvider` для управления, как передаются политик авторизации.</span><span class="sxs-lookup"><span data-stu-id="85457-107">In those cases, you can use a custom `IAuthorizationPolicyProvider` to control how authorization policies are supplied.</span></span>

<span data-ttu-id="85457-108">Примеры сценариев, где пользовательское [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) может быть полезно включить:</span><span class="sxs-lookup"><span data-stu-id="85457-108">Examples of scenarios where a custom [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) may be useful include:</span></span>

* <span data-ttu-id="85457-109">Использовать внешнюю службу для предоставления оценки политики.</span><span class="sxs-lookup"><span data-stu-id="85457-109">Using an external service to provide policy evaluation.</span></span>
* <span data-ttu-id="85457-110">С помощью большой диапазон политики (для номера разных мест или возрасте, например), поэтому нет смысла для добавления каждой политики авторизации для отдельных с `AuthorizationOptions.AddPolicy` вызова.</span><span class="sxs-lookup"><span data-stu-id="85457-110">Using a large range of policies (for different room numbers or ages, for example), so it doesn’t make sense to add each individual authorization policy with an `AuthorizationOptions.AddPolicy` call.</span></span>
* <span data-ttu-id="85457-111">Создание политики в среде выполнения, на основе сведений из внешнего источника данных (например, базу данных) или динамически определить требования к проверке подлинности посредством другого механизма.</span><span class="sxs-lookup"><span data-stu-id="85457-111">Creating policies at runtime based on information in an external data source (like a database) or determining authorization requirements dynamically through another mechanism.</span></span>

<span data-ttu-id="85457-112">[Просмотреть или скачать образец кода](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider) из [репозиторий AspNetCore GitHub](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="85457-112">[View or download sample code](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider) from the [AspNetCore GitHub repository](https://github.com/aspnet/AspNetCore).</span></span> <span data-ttu-id="85457-113">Скачайте репозиторий aspnet/AspNetCore ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="85457-113">Download the aspnet/AspNetCore repository ZIP file.</span></span> <span data-ttu-id="85457-114">Распакуйте файл.</span><span class="sxs-lookup"><span data-stu-id="85457-114">Unzip the file.</span></span> <span data-ttu-id="85457-115">Перейдите к *src/Security/примеры/CustomPolicyProvider* папки проекта.</span><span class="sxs-lookup"><span data-stu-id="85457-115">Navigate to the *src/Security/samples/CustomPolicyProvider* project folder.</span></span>

## <a name="customize-policy-retrieval"></a><span data-ttu-id="85457-116">Настройки политики извлечения</span><span class="sxs-lookup"><span data-stu-id="85457-116">Customize policy retrieval</span></span>

<span data-ttu-id="85457-117">Приложения ASP.NET Core используют реализацию `IAuthorizationPolicyProvider` интерфейс для получения политики авторизации.</span><span class="sxs-lookup"><span data-stu-id="85457-117">ASP.NET Core apps use an implementation of the `IAuthorizationPolicyProvider` interface to retrieve authorization policies.</span></span> <span data-ttu-id="85457-118">По умолчанию [DefaultAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) регистрируется и используется.</span><span class="sxs-lookup"><span data-stu-id="85457-118">By default, [DefaultAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) is registered and used.</span></span> <span data-ttu-id="85457-119">`DefaultAuthorizationPolicyProvider` Возвращает политики из `AuthorizationOptions` в `IServiceCollection.AddAuthorization` вызова.</span><span class="sxs-lookup"><span data-stu-id="85457-119">`DefaultAuthorizationPolicyProvider` returns policies from the `AuthorizationOptions` provided in an `IServiceCollection.AddAuthorization` call.</span></span>

<span data-ttu-id="85457-120">Это поведение можно настроить путем регистрации другой `IAuthorizationPolicyProvider` реализации в приложении [внедрения зависимостей](xref:fundamentals/dependency-injection) контейнера.</span><span class="sxs-lookup"><span data-stu-id="85457-120">You can customize this behavior by registering a different `IAuthorizationPolicyProvider` implementation in the app’s [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> 

<span data-ttu-id="85457-121">`IAuthorizationPolicyProvider` Интерфейс содержит два API:</span><span class="sxs-lookup"><span data-stu-id="85457-121">The `IAuthorizationPolicyProvider` interface contains two APIs:</span></span>

* <span data-ttu-id="85457-122">[GetPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) возвращает политику авторизации для заданного имени.</span><span class="sxs-lookup"><span data-stu-id="85457-122">[GetPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) returns an authorization policy for a given name.</span></span>
* <span data-ttu-id="85457-123">[GetDefaultPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync) возвращает политику авторизации по умолчанию (политика, используемая для `[Authorize]` атрибутов без политику, указанную).</span><span class="sxs-lookup"><span data-stu-id="85457-123">[GetDefaultPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync) returns the default authorization policy (the policy used for `[Authorize]` attributes without a policy specified).</span></span> 

<span data-ttu-id="85457-124">Реализовав эти два API-интерфейсы, вы можете настроить, каким образом предоставляются политики авторизации.</span><span class="sxs-lookup"><span data-stu-id="85457-124">By implementing these two APIs, you can customize how authorization policies are provided.</span></span>

## <a name="parameterized-authorize-attribute-example"></a><span data-ttu-id="85457-125">Параметризованные авторизовать пример атрибута</span><span class="sxs-lookup"><span data-stu-id="85457-125">Parameterized authorize attribute example</span></span>

<span data-ttu-id="85457-126">Один из сценариев где `IAuthorizationPolicyProvider` полезно используется, чтобы предоставить настраиваемый `[Authorize]` атрибуты, чьи требования зависят от параметра.</span><span class="sxs-lookup"><span data-stu-id="85457-126">One scenario where `IAuthorizationPolicyProvider` is useful is enabling custom `[Authorize]` attributes whose requirements depend on a parameter.</span></span> <span data-ttu-id="85457-127">Например, в [авторизации на основе политики](xref:security/authorization/policies) документации, на основе возраста («AtLeast21») политика была использована в качестве образца.</span><span class="sxs-lookup"><span data-stu-id="85457-127">For example, in [policy-based authorization](xref:security/authorization/policies) documentation, an age-based (“AtLeast21”) policy was used as a sample.</span></span> <span data-ttu-id="85457-128">Если другой контроллер действия в приложении должны быть доступными для пользователей *различных* возраста, может оказаться полезным для многих различных политик на основе возраста.</span><span class="sxs-lookup"><span data-stu-id="85457-128">If different controller actions in an app should be made available to users of *different* ages, it might be useful to have many different age-based policies.</span></span> <span data-ttu-id="85457-129">Вместо регистрации все различные возрастное политики, которые приложение нужно включить в `AuthorizationOptions`, вы можете создать политики динамически на основе собственной `IAuthorizationPolicyProvider`.</span><span class="sxs-lookup"><span data-stu-id="85457-129">Instead of registering all the different age-based policies that the application will need in `AuthorizationOptions`, you can generate the policies dynamically with a custom `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="85457-130">Чтобы сделать с помощью политики, проще, можно добавить заметку действия с пользовательский атрибут авторизации как `[MinimumAgeAuthorize(20)]`.</span><span class="sxs-lookup"><span data-stu-id="85457-130">To make using the policies easier, you can annotate actions with custom authorization attribute like `[MinimumAgeAuthorize(20)]`.</span></span>

## <a name="custom-authorization-attributes"></a><span data-ttu-id="85457-131">Атрибуты настраиваемой авторизации</span><span class="sxs-lookup"><span data-stu-id="85457-131">Custom Authorization Attributes</span></span>

<span data-ttu-id="85457-132">Политики авторизации идентифицируются по их именам.</span><span class="sxs-lookup"><span data-stu-id="85457-132">Authorization policies are identified by their names.</span></span> <span data-ttu-id="85457-133">Пользовательский `MinimumAgeAuthorizeAttribute` описано ранее, необходимо сопоставить аргументов в строку, которая может использоваться для получения соответствующей политики авторизации.</span><span class="sxs-lookup"><span data-stu-id="85457-133">The custom `MinimumAgeAuthorizeAttribute` described previously needs to map arguments into a string that can be used to retrieve the corresponding authorization policy.</span></span> <span data-ttu-id="85457-134">Это можно сделать путем наследования от `AuthorizeAttribute` и `Age` свойство wrap `AuthorizeAttribute.Policy` свойство.</span><span class="sxs-lookup"><span data-stu-id="85457-134">You can do this by deriving from `AuthorizeAttribute` and making the `Age` property wrap the `AuthorizeAttribute.Policy` property.</span></span>

```csharp
internal class MinimumAgeAuthorizeAttribute : AuthorizeAttribute
{
    const string POLICY_PREFIX = "MinimumAge";

    public MinimumAgeAuthorizeAttribute(int age) => Age = age;

    // Get or set the Age property by manipulating the underlying Policy property
    public int Age
    {
        get
        {
            if (int.TryParse(Policy.Substring(POLICY_PREFIX.Length), out var age))
            {
                return age;
            }
            return default(int);
        }
        set
        {
            Policy = $"{POLICY_PREFIX}{value.ToString()}";
        }
    }
}
```

<span data-ttu-id="85457-135">Этот тип атрибута имеет `Policy` строки на основе жестко префикса (`"MinimumAge"`) и является целым числом, переданный через конструктор.</span><span class="sxs-lookup"><span data-stu-id="85457-135">This attribute type has a `Policy` string based on the hard-coded prefix (`"MinimumAge"`) and an integer passed in via the constructor.</span></span>

<span data-ttu-id="85457-136">Его можно применить к действиям в так же, как другие `Authorize` атрибуты, за исключением того, что он принимает целое число как параметр.</span><span class="sxs-lookup"><span data-stu-id="85457-136">You can apply it to actions in the same way as other `Authorize` attributes except that it takes an integer as a parameter.</span></span>

```csharp
[MinimumAgeAuthorize(10)]
public IActionResult RequiresMinimumAge10()
```

## <a name="custom-iauthorizationpolicyprovider"></a><span data-ttu-id="85457-137">Пользовательские IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="85457-137">Custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="85457-138">Пользовательский `MinimumAgeAuthorizeAttribute` облегчает политики запроса авторизации для любой минимальный возраст требуемого.</span><span class="sxs-lookup"><span data-stu-id="85457-138">The custom `MinimumAgeAuthorizeAttribute` makes it easy to request authorization policies for any minimum age desired.</span></span> <span data-ttu-id="85457-139">Далее проблемы убедиться, что политики авторизации доступны для всех этих разных возрастов.</span><span class="sxs-lookup"><span data-stu-id="85457-139">The next problem to solve is making sure that authorization policies are available for all of those different ages.</span></span> <span data-ttu-id="85457-140">Именно здесь `IAuthorizationPolicyProvider` полезно.</span><span class="sxs-lookup"><span data-stu-id="85457-140">This is where an `IAuthorizationPolicyProvider` is useful.</span></span>

<span data-ttu-id="85457-141">При использовании `MinimumAgeAuthorizationAttribute`, имена политик авторизации будет соответствовать шаблону `"MinimumAge" + Age`, поэтому пользовательский `IAuthorizationPolicyProvider` должен создать политики авторизации с:</span><span class="sxs-lookup"><span data-stu-id="85457-141">When using `MinimumAgeAuthorizationAttribute`, the authorization policy names will follow the pattern `"MinimumAge" + Age`, so the custom `IAuthorizationPolicyProvider` should generate authorization policies by:</span></span>

* <span data-ttu-id="85457-142">Синтаксический анализ возраст с имя политики.</span><span class="sxs-lookup"><span data-stu-id="85457-142">Parsing the age from the policy name.</span></span>
* <span data-ttu-id="85457-143">С помощью `AuthorizationPolicyBuilder` для создания нового `AuthorizationPolicy`</span><span class="sxs-lookup"><span data-stu-id="85457-143">Using `AuthorizationPolicyBuilder` to create a new `AuthorizationPolicy`</span></span>
* <span data-ttu-id="85457-144">Добавление требований к политике на основе возраста с `AuthorizationPolicyBuilder.AddRequirements`.</span><span class="sxs-lookup"><span data-stu-id="85457-144">Adding requirements to the policy based on the age with `AuthorizationPolicyBuilder.AddRequirements`.</span></span> <span data-ttu-id="85457-145">Можно использовать в других сценариях `RequireClaim`, `RequireRole`, или `RequireUserName` вместо этого.</span><span class="sxs-lookup"><span data-stu-id="85457-145">In other scenarios, you might use `RequireClaim`, `RequireRole`, or `RequireUserName` instead.</span></span>

```csharp
internal class MinimumAgePolicyProvider : IAuthorizationPolicyProvider
{
    const string POLICY_PREFIX = "MinimumAge";

    // Policies are looked up by string name, so expect 'parameters' (like age)
    // to be embedded in the policy names. This is abstracted away from developers
    // by the more strongly-typed attributes derived from AuthorizeAttribute
    // (like [MinimumAgeAuthorize()] in this sample)
    public Task<AuthorizationPolicy> GetPolicyAsync(string policyName)
    {
        if (policyName.StartsWith(POLICY_PREFIX, StringComparison.OrdinalIgnoreCase) &&
            int.TryParse(policyName.Substring(POLICY_PREFIX.Length), out var age))
        {
            var policy = new AuthorizationPolicyBuilder();
            policy.AddRequirements(new MinimumAgeRequirement(age));
            return Task.FromResult(policy.Build());
        }

        return Task.FromResult<AuthorizationPolicy>(null);
    }
}
```

## <a name="multiple-authorization-policy-providers"></a><span data-ttu-id="85457-146">Несколько поставщиков политики авторизации</span><span class="sxs-lookup"><span data-stu-id="85457-146">Multiple authorization policy providers</span></span>

<span data-ttu-id="85457-147">При использовании пользовательских `IAuthorizationPolicyProvider` реализаций, имейте в виду, что ASP.NET Core использует только один экземпляр `IAuthorizationPolicyProvider`.</span><span class="sxs-lookup"><span data-stu-id="85457-147">When using custom `IAuthorizationPolicyProvider` implementations, keep in mind that ASP.NET Core only uses one instance of `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="85457-148">Если пользовательский поставщик не может предоставить политики авторизации для имена всех политик, он должен выполнить откат до резервного копирования поставщика.</span><span class="sxs-lookup"><span data-stu-id="85457-148">If a custom provider isn't able to provide authorization policies for all policy names, it should fall back to a backup provider.</span></span> <span data-ttu-id="85457-149">Имена политик могут включать, поступающими от политики по умолчанию для `[Authorize]` атрибуты без имени.</span><span class="sxs-lookup"><span data-stu-id="85457-149">Policy names might include those that come from a default policy for `[Authorize]` attributes without a name.</span></span>

<span data-ttu-id="85457-150">Например рассмотрим, что приложение требуется политики возраста пользовательский и более традиционных получения политик на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="85457-150">For example, consider an application needed both custom age policies and more traditional role-based policy retrieval.</span></span> <span data-ttu-id="85457-151">Такое приложение может использовать поставщик политики настраиваемой авторизации:</span><span class="sxs-lookup"><span data-stu-id="85457-151">Such an app could use a custom authorization policy provider that:</span></span>

* <span data-ttu-id="85457-152">Пытается проанализировать имена политик.</span><span class="sxs-lookup"><span data-stu-id="85457-152">Attempts to parse policy names.</span></span> 
* <span data-ttu-id="85457-153">Вызывает другую политику поставщика (например `DefaultAuthorizationPolicyProvider`) Если политика не может содержать возраст.</span><span class="sxs-lookup"><span data-stu-id="85457-153">Calls into a different policy provider (like `DefaultAuthorizationPolicyProvider`) if the policy name doesn't contain an age.</span></span>

## <a name="default-policy"></a><span data-ttu-id="85457-154">Политика по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85457-154">Default policy</span></span>

<span data-ttu-id="85457-155">Помимо предоставления политики авторизации для именованный, настраиваемый `IAuthorizationPolicyProvider` должен реализовывать `GetDefaultPolicyAsync` для предоставления политику авторизации для `[Authorize]` атрибутов без указанное имя политики.</span><span class="sxs-lookup"><span data-stu-id="85457-155">In addition to providing named authorization policies, a custom `IAuthorizationPolicyProvider` needs to implement `GetDefaultPolicyAsync` to provide an authorization policy for `[Authorize]` attributes without a policy name specified.</span></span>

<span data-ttu-id="85457-156">Во многих случаях этот атрибут авторизации требуется только прошедший проверку пользователь, чтобы принимать необходимые политики с помощью вызова `RequireAuthenticatedUser`:</span><span class="sxs-lookup"><span data-stu-id="85457-156">In many cases, this authorization attribute only requires an authenticated user, so you can make the necessary policy with a call to `RequireAuthenticatedUser`:</span></span>

```csharp
public Task<AuthorizationPolicy> GetDefaultPolicyAsync() => 
    Task.FromResult(new AuthorizationPolicyBuilder().RequireAuthenticatedUser().Build());
```

<span data-ttu-id="85457-157">Как и в случае со всеми аспектами пользовательского `IAuthorizationPolicyProvider`, этот параметр можно изменить, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="85457-157">As with all aspects of a custom `IAuthorizationPolicyProvider`, you can customize this, as needed.</span></span> <span data-ttu-id="85457-158">В некоторых случаях:</span><span class="sxs-lookup"><span data-stu-id="85457-158">In some cases:</span></span>

* <span data-ttu-id="85457-159">Политики авторизации по умолчанию не может быть использована.</span><span class="sxs-lookup"><span data-stu-id="85457-159">Default authorization policies might not be used.</span></span>
* <span data-ttu-id="85457-160">Получение политики по умолчанию можно делегировать переход на резервный ресурс `IAuthorizationPolicyProvider`.</span><span class="sxs-lookup"><span data-stu-id="85457-160">Retrieving the default policy can be delegated to a fallback `IAuthorizationPolicyProvider`.</span></span>

## <a name="use-a-custom-iauthorizationpolicyprovider"></a><span data-ttu-id="85457-161">Используйте пользовательские IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="85457-161">Use a custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="85457-162">Для использования настраиваемых политик из `IAuthorizationPolicyProvider`, необходимо:</span><span class="sxs-lookup"><span data-stu-id="85457-162">To use custom policies from an `IAuthorizationPolicyProvider`, you must:</span></span>

* <span data-ttu-id="85457-163">Зарегистрируйте соответствующий `AuthorizationHandler` типов с помощью внедрения зависимостей (описано в разделе [авторизации на основе политики](xref:security/authorization/policies#authorization-handlers)), как и для всех сценариев на основе политик авторизации.</span><span class="sxs-lookup"><span data-stu-id="85457-163">Register the appropriate `AuthorizationHandler` types with dependency injection (described in [policy-based authorization](xref:security/authorization/policies#authorization-handlers)), as with all policy-based authorization scenarios.</span></span>
* <span data-ttu-id="85457-164">Регистрация пользовательского `IAuthorizationPolicyProvider` типа в коллекцию служб для внедрения зависимостей приложения (в `Startup.ConfigureServices`) для замены поставщика политики по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="85457-164">Register the custom `IAuthorizationPolicyProvider` type in the app's dependency injection service collection (in `Startup.ConfigureServices`) to replace the default policy provider.</span></span>

```csharp
services.AddSingleton<IAuthorizationPolicyProvider, MinimumAgePolicyProvider>();
```

<span data-ttu-id="85457-165">Полный пользовательский `IAuthorizationPolicyProvider` пример можно найти в [репозиторий GitHub aspnet/AuthSamples](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider).</span><span class="sxs-lookup"><span data-stu-id="85457-165">A complete custom `IAuthorizationPolicyProvider` sample is available in the [aspnet/AuthSamples GitHub repository](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider).</span></span>
