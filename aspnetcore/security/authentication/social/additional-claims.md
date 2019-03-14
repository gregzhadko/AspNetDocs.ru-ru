---
title: Сохранять дополнительные утверждения и маркеры от внешних поставщиков в ASP.NET Core
author: guardrex
description: Узнайте, как установить дополнительные утверждения и маркеры от внешних поставщиков.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/social/additional-claims
ms.openlocfilehash: 9a24ac138950ef2bedac48f506655d06520137cf
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049321"
---
# <a name="persist-additional-claims-and-tokens-from-external-providers-in-aspnet-core"></a><span data-ttu-id="4738a-103">Сохранять дополнительные утверждения и маркеры от внешних поставщиков в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4738a-103">Persist additional claims and tokens from external providers in ASP.NET Core</span></span>

<span data-ttu-id="4738a-104">Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)</span><span class="sxs-lookup"><span data-stu-id="4738a-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4738a-105">Приложения ASP.NET Core можно установить дополнительные утверждения и маркеры от внешних поставщиков проверки подлинности, таких как Facebook, Google, Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="4738a-105">An ASP.NET Core app can establish additional claims and tokens from external authentication providers, such as Facebook, Google, Microsoft, and Twitter.</span></span> <span data-ttu-id="4738a-106">Каждый поставщик раскрывает различные сведения о пользователях на платформе, но шаблон для получения и преобразования данных пользователя в дополнительные утверждения одинаков.</span><span class="sxs-lookup"><span data-stu-id="4738a-106">Each provider reveals different information about users on its platform, but the pattern for receiving and transforming user data into additional claims is the same.</span></span>

<span data-ttu-id="4738a-107">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/social/additional-claims/samples) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="4738a-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/social/additional-claims/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4738a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4738a-108">Prerequisites</span></span>

<span data-ttu-id="4738a-109">Решите, какие поставщики внешней проверки подлинности для поддержки в приложении.</span><span class="sxs-lookup"><span data-stu-id="4738a-109">Decide which external authentication providers to support in the app.</span></span> <span data-ttu-id="4738a-110">Для каждого поставщика Регистрация приложения и получить идентификатор клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="4738a-110">For each provider, register the app and obtain a client ID and client secret.</span></span> <span data-ttu-id="4738a-111">Дополнительные сведения см. в разделе <xref:security/authentication/social/index>.</span><span class="sxs-lookup"><span data-stu-id="4738a-111">For more information, see <xref:security/authentication/social/index>.</span></span> <span data-ttu-id="4738a-112">[Пример приложения](#sample-app-instructions) использует [поставщик проверки подлинности Google](xref:security/authentication/google-logins).</span><span class="sxs-lookup"><span data-stu-id="4738a-112">The [sample app](#sample-app-instructions) uses the [Google authentication provider](xref:security/authentication/google-logins).</span></span>

## <a name="set-the-client-id-and-client-secret"></a><span data-ttu-id="4738a-113">Задание идентификатора и секрета клиента</span><span class="sxs-lookup"><span data-stu-id="4738a-113">Set the client ID and client secret</span></span>

<span data-ttu-id="4738a-114">Поставщик проверки подлинности OAuth устанавливает отношение доверия с помощью приложения с помощью идентификатора клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="4738a-114">The OAuth authentication provider establishes a trust relationship with an app using a client ID and client secret.</span></span> <span data-ttu-id="4738a-115">Идентификатор клиента и секрет клиента, создаваемые для приложения поставщика внешней проверки подлинности при регистрации приложения с поставщиком.</span><span class="sxs-lookup"><span data-stu-id="4738a-115">Client ID and client secret values are created for the app by the external authentication provider when the app is registered with the provider.</span></span> <span data-ttu-id="4738a-116">Каждый внешний поставщик, приложение использует должны быть настроены независимо друг от друга идентификатор клиента и секрет клиента поставщика.</span><span class="sxs-lookup"><span data-stu-id="4738a-116">Each external provider that the app uses must be configured independently with the provider's client ID and client secret.</span></span> <span data-ttu-id="4738a-117">Дополнительные сведения см. в разделах поставщика внешней проверки подлинности, которые применяются к вашему сценарию:</span><span class="sxs-lookup"><span data-stu-id="4738a-117">For more information, see the external authentication provider topics that apply to your scenario:</span></span>

* [<span data-ttu-id="4738a-118">Проверка подлинности Facebook</span><span class="sxs-lookup"><span data-stu-id="4738a-118">Facebook authentication</span></span>](xref:security/authentication/facebook-logins)
* [<span data-ttu-id="4738a-119">Проверка подлинности Google</span><span class="sxs-lookup"><span data-stu-id="4738a-119">Google authentication</span></span>](xref:security/authentication/google-logins)
* [<span data-ttu-id="4738a-120">Проверка подлинности Майкрософт</span><span class="sxs-lookup"><span data-stu-id="4738a-120">Microsoft authentication</span></span>](xref:security/authentication/microsoft-logins)
* [<span data-ttu-id="4738a-121">Проверка подлинности Twitter</span><span class="sxs-lookup"><span data-stu-id="4738a-121">Twitter authentication</span></span>](xref:security/authentication/twitter-logins)
* [<span data-ttu-id="4738a-122">Другие поставщики проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4738a-122">Other authentication providers</span></span>](xref:security/authentication/otherlogins)
* [<span data-ttu-id="4738a-123">OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="4738a-123">OpenIdConnect</span></span>](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2)

<span data-ttu-id="4738a-124">Пример приложения настраивает поставщик проверки подлинности Google с Идентификатором клиента и секрет клиента, предоставляемый Google:</span><span class="sxs-lookup"><span data-stu-id="4738a-124">The sample app configures the Google authentication provider with a client ID and client secret provided by Google:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Startup.cs?name=snippet_AddGoogle&highlight=4,6)]

## <a name="establish-the-authentication-scope"></a><span data-ttu-id="4738a-125">Установить область проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4738a-125">Establish the authentication scope</span></span>

<span data-ttu-id="4738a-126">Укажите список разрешений для получения от поставщика, путем указания <xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthOptions.Scope*>.</span><span class="sxs-lookup"><span data-stu-id="4738a-126">Specify the list of permissions to retrieve from the provider by specifying the <xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthOptions.Scope*>.</span></span> <span data-ttu-id="4738a-127">В следующей таблице отображаются области проверки подлинности для распространенных внешних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="4738a-127">Authentication scopes for common external providers appear in the following table.</span></span>

| <span data-ttu-id="4738a-128">Поставщик</span><span class="sxs-lookup"><span data-stu-id="4738a-128">Provider</span></span>  | <span data-ttu-id="4738a-129">Область</span><span class="sxs-lookup"><span data-stu-id="4738a-129">Scope</span></span>                                                            |
| --------- | ---------------------------------------------------------------- |
| <span data-ttu-id="4738a-130">Facebook</span><span class="sxs-lookup"><span data-stu-id="4738a-130">Facebook</span></span>  | `https://www.facebook.com/dialog/oauth`                          |
| <span data-ttu-id="4738a-131">Google</span><span class="sxs-lookup"><span data-stu-id="4738a-131">Google</span></span>    | `https://www.googleapis.com/auth/plus.login`                     |
| <span data-ttu-id="4738a-132">Майкрософт</span><span class="sxs-lookup"><span data-stu-id="4738a-132">Microsoft</span></span> | `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` |
| <span data-ttu-id="4738a-133">Twitter</span><span class="sxs-lookup"><span data-stu-id="4738a-133">Twitter</span></span>   | `https://api.twitter.com/oauth/authenticate`                     |

<span data-ttu-id="4738a-134">Пример приложения добавляет Google `plus.login` область для запроса входа Google + в разрешениях:</span><span class="sxs-lookup"><span data-stu-id="4738a-134">The sample app adds the Google `plus.login` scope to request Google+ sign in permissions:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Startup.cs?name=snippet_AddGoogle&highlight=7)]

## <a name="map-user-data-keys-and-create-claims"></a><span data-ttu-id="4738a-135">Сопоставить ключи данных пользователя и создать утверждения</span><span class="sxs-lookup"><span data-stu-id="4738a-135">Map user data keys and create claims</span></span>

<span data-ttu-id="4738a-136">В параметрах поставщика, укажите <xref:Microsoft.AspNetCore.Authentication.ClaimActionCollectionMapExtensions.MapJsonKey*> для каждого ключа в внешнего поставщика JSON пользовательские данные для удостоверения приложения для чтения при входе.</span><span class="sxs-lookup"><span data-stu-id="4738a-136">In the provider's options, specify a <xref:Microsoft.AspNetCore.Authentication.ClaimActionCollectionMapExtensions.MapJsonKey*> for each key in the external provider's JSON user data for the app identity to read on sign in.</span></span> <span data-ttu-id="4738a-137">Дополнительные сведения о типах утверждений, см. в разделе <xref:System.Security.Claims.ClaimTypes>.</span><span class="sxs-lookup"><span data-stu-id="4738a-137">For more information on claim types, see <xref:System.Security.Claims.ClaimTypes>.</span></span>

<span data-ttu-id="4738a-138">Пример приложения создает <xref:System.Security.Claims.ClaimTypes.Gender> утверждение от `gender` ключа в данных пользователя Google:</span><span class="sxs-lookup"><span data-stu-id="4738a-138">The sample app creates a <xref:System.Security.Claims.ClaimTypes.Gender> claim from the `gender` key in Google user data:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Startup.cs?name=snippet_AddGoogle&highlight=8)]

<span data-ttu-id="4738a-139">В <xref:Microsoft.AspNetCore.Identity.UI.Pages.Account.Internal.ExternalLoginModel.OnPostConfirmationAsync*>, <xref:Microsoft.AspNetCore.Identity.IdentityUser> (`ApplicationUser`) осуществил вход в приложение с помощью <xref:Microsoft.AspNetCore.Identity.SignInManager`1.SignInAsync*>.</span><span class="sxs-lookup"><span data-stu-id="4738a-139">In <xref:Microsoft.AspNetCore.Identity.UI.Pages.Account.Internal.ExternalLoginModel.OnPostConfirmationAsync*>, an <xref:Microsoft.AspNetCore.Identity.IdentityUser> (`ApplicationUser`) is signed into the app with <xref:Microsoft.AspNetCore.Identity.SignInManager`1.SignInAsync*>.</span></span> <span data-ttu-id="4738a-140">Во время входа в систему <xref:Microsoft.AspNetCore.Identity.UserManager`1> можно хранить `ApplicationUser` утверждения для пользовательских данных, доступных из <xref:Microsoft.AspNetCore.Identity.ExternalLoginInfo.Principal*>.</span><span class="sxs-lookup"><span data-stu-id="4738a-140">During the sign in process, the <xref:Microsoft.AspNetCore.Identity.UserManager`1> can store an `ApplicationUser` claim for user data available from the <xref:Microsoft.AspNetCore.Identity.ExternalLoginInfo.Principal*>.</span></span>

<span data-ttu-id="4738a-141">В примере приложения `OnPostConfirmationAsync` (*Account/ExternalLogin.cshtml.cs*) устанавливает <xref:System.Security.Claims.ClaimTypes.Gender> утверждения для со знаком в `ApplicationUser`:</span><span class="sxs-lookup"><span data-stu-id="4738a-141">In the sample app, `OnPostConfirmationAsync` (*Account/ExternalLogin.cshtml.cs*) establishes a <xref:System.Security.Claims.ClaimTypes.Gender> claim for the signed in `ApplicationUser`:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Pages/Account/ExternalLogin.cshtml.cs?name=snippet_OnPostConfirmationAsync&highlight=30-31)]

## <a name="save-the-access-token"></a><span data-ttu-id="4738a-142">Сохранить маркер доступа</span><span class="sxs-lookup"><span data-stu-id="4738a-142">Save the access token</span></span>

<span data-ttu-id="4738a-143"><xref:Microsoft.AspNetCore.Authentication.RemoteAuthenticationOptions.SaveTokens*> Определяет, следует ли хранить маркеров доступа и обновления в <xref:Microsoft.AspNetCore.Http.Authentication.AuthenticationProperties> после успешной авторизации.</span><span class="sxs-lookup"><span data-stu-id="4738a-143"><xref:Microsoft.AspNetCore.Authentication.RemoteAuthenticationOptions.SaveTokens*> defines whether access and refresh tokens should be stored in the <xref:Microsoft.AspNetCore.Http.Authentication.AuthenticationProperties> after a successful authorization.</span></span> <span data-ttu-id="4738a-144">`SaveTokens` имеет значение `false` по умолчанию, чтобы уменьшить размер файла cookie окончательной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4738a-144">`SaveTokens` is set to `false` by default to reduce the size of the final authentication cookie.</span></span>

<span data-ttu-id="4738a-145">В примере приложения задает значение `SaveTokens` для `true` в <xref:Microsoft.AspNetCore.Authentication.Google.GoogleOptions>:</span><span class="sxs-lookup"><span data-stu-id="4738a-145">The sample app sets the value of `SaveTokens` to `true` in <xref:Microsoft.AspNetCore.Authentication.Google.GoogleOptions>:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Startup.cs?name=snippet_AddGoogle&highlight=9)]

<span data-ttu-id="4738a-146">Когда `OnPostConfirmationAsync` выполняет, сохранить маркер доступа ([ExternalLoginInfo.AuthenticationTokens](xref:Microsoft.AspNetCore.Identity.ExternalLoginInfo.AuthenticationTokens*)) из внешнего поставщика в `ApplicationUser`в `AuthenticationProperties`.</span><span class="sxs-lookup"><span data-stu-id="4738a-146">When `OnPostConfirmationAsync` executes, store the access token ([ExternalLoginInfo.AuthenticationTokens](xref:Microsoft.AspNetCore.Identity.ExternalLoginInfo.AuthenticationTokens*)) from the external provider in the `ApplicationUser`'s `AuthenticationProperties`.</span></span>

<span data-ttu-id="4738a-147">Это пример приложения сохраняет маркер доступа в:</span><span class="sxs-lookup"><span data-stu-id="4738a-147">The sample app saves the access token in:</span></span>

* <span data-ttu-id="4738a-148">`OnPostConfirmationAsync` &ndash; Выполняет для регистрация нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="4738a-148">`OnPostConfirmationAsync` &ndash; Executes for new user registration.</span></span>
* <span data-ttu-id="4738a-149">`OnGetCallbackAsync` &ndash; Выполняется, если ранее зарегистрированный пользователь входит в приложение.</span><span class="sxs-lookup"><span data-stu-id="4738a-149">`OnGetCallbackAsync` &ndash; Executes when a previously registered user signs into the app.</span></span>

<span data-ttu-id="4738a-150">*Account/ExternalLogin.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="4738a-150">*Account/ExternalLogin.cshtml.cs*:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Pages/Account/ExternalLogin.cshtml.cs?name=snippet_OnPostConfirmationAsync&highlight=34-35)]

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Pages/Account/ExternalLogin.cshtml.cs?name=snippet_OnGetCallbackAsync&highlight=31-32)]

## <a name="how-to-add-additional-custom-tokens"></a><span data-ttu-id="4738a-151">Как добавить дополнительные пользовательские маркеры</span><span class="sxs-lookup"><span data-stu-id="4738a-151">How to add additional custom tokens</span></span>

<span data-ttu-id="4738a-152">Чтобы продемонстрировать, как добавить пользовательский маркер, который хранится как часть `SaveTokens`, пример приложения добавляет <xref:Microsoft.AspNetCore.Authentication.AuthenticationToken> с текущим <xref:System.DateTime> для [AuthenticationToken.Name](xref:Microsoft.AspNetCore.Authentication.AuthenticationToken.Name*) из `TicketCreated`:</span><span class="sxs-lookup"><span data-stu-id="4738a-152">To demonstrate how to add a custom token, which is stored as part of `SaveTokens`, the sample app adds an <xref:Microsoft.AspNetCore.Authentication.AuthenticationToken> with the current <xref:System.DateTime> for an [AuthenticationToken.Name](xref:Microsoft.AspNetCore.Authentication.AuthenticationToken.Name*) of `TicketCreated`:</span></span>

[!code-csharp[](additional-claims/samples/2.x/AdditionalClaimsSample/Startup.cs?name=snippet_AddGoogle&highlight=10-21)]

## <a name="sample-app-instructions"></a><span data-ttu-id="4738a-153">Примеры инструкций по назначению приложения</span><span class="sxs-lookup"><span data-stu-id="4738a-153">Sample app instructions</span></span>

<span data-ttu-id="4738a-154">Этот пример демонстрирует способы:</span><span class="sxs-lookup"><span data-stu-id="4738a-154">The sample app demonstrates how to:</span></span>

* <span data-ttu-id="4738a-155">Получите Пол пользователя от Google и сохраняет Пол утверждение со значением.</span><span class="sxs-lookup"><span data-stu-id="4738a-155">Obtain the user's gender from Google and store a gender claim with the value.</span></span>
* <span data-ttu-id="4738a-156">Store маркер доступа Google в пользователя `AuthenticationProperties`.</span><span class="sxs-lookup"><span data-stu-id="4738a-156">Store the Google access token in the user's `AuthenticationProperties`.</span></span>

<span data-ttu-id="4738a-157">Чтобы использовать пример приложения:</span><span class="sxs-lookup"><span data-stu-id="4738a-157">To use the sample app:</span></span>

1. <span data-ttu-id="4738a-158">Регистрация приложения и получить допустимый идентификатор клиента и секрет клиента для проверки подлинности Google.</span><span class="sxs-lookup"><span data-stu-id="4738a-158">Register the app and obtain a valid client ID and client secret for Google authentication.</span></span> <span data-ttu-id="4738a-159">Дополнительные сведения см. в разделе <xref:security/authentication/google-logins>.</span><span class="sxs-lookup"><span data-stu-id="4738a-159">For more information, see <xref:security/authentication/google-logins>.</span></span>
1. <span data-ttu-id="4738a-160">Указание идентификатора клиента и секрет клиента для приложения в <xref:Microsoft.AspNetCore.Authentication.Google.GoogleOptions> из `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="4738a-160">Provide the client ID and client secret to the app in the <xref:Microsoft.AspNetCore.Authentication.Google.GoogleOptions> of `Startup.ConfigureServices`.</span></span>
1. <span data-ttu-id="4738a-161">Запустите приложение и запрос страницы Мои утверждения.</span><span class="sxs-lookup"><span data-stu-id="4738a-161">Run the app and request the My Claims page.</span></span> <span data-ttu-id="4738a-162">Если пользователь не вошел в систему, которую перенаправляет пользователя приложение в Google.</span><span class="sxs-lookup"><span data-stu-id="4738a-162">When the user isn't signed in, the app redirects to Google.</span></span> <span data-ttu-id="4738a-163">Войдите с помощью Google.</span><span class="sxs-lookup"><span data-stu-id="4738a-163">Sign in with Google.</span></span> <span data-ttu-id="4738a-164">Google перенаправляет пользователя обратно к приложению (`/Home/MyClaims`).</span><span class="sxs-lookup"><span data-stu-id="4738a-164">Google redirects the user back to the app (`/Home/MyClaims`).</span></span> <span data-ttu-id="4738a-165">Пользователь проходит проверку подлинности и загрузке страницы Мои утверждения.</span><span class="sxs-lookup"><span data-stu-id="4738a-165">The user is authenticated, and the My Claims page is loaded.</span></span> <span data-ttu-id="4738a-166">Пол утверждения находится в каталоге **утверждения пользователей** со значением, полученный из Google.</span><span class="sxs-lookup"><span data-stu-id="4738a-166">The gender claim is present under **User Claims** with the value obtained from Google.</span></span> <span data-ttu-id="4738a-167">Маркер доступа появится в **свойства проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="4738a-167">The access token appears in the **Authentication Properties**.</span></span>

```
User Claims

http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier
    b36a7b09-9135-4810-b7a5-78697ff23e99
http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
    username@gmail.com
AspNet.Identity.SecurityStamp
    29G2TB881ATCUQFJSRFG1S0QJ0OOAWVT
http://schemas.xmlsoap.org/ws/2005/05/identity/claims/gender
    female
http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod
    Google

Authentication Properties

.Token.access_token
    bv42.Dgw...GQMv9ArLPs
.Token.token_type
    Bearer
.Token.expires_at
    2018-08-27T19:08:00.0000000+00:00
.Token.TicketCreated
    8/27/2018 6:08:00 PM
.TokenNames
    access_token;token_type;expires_at;TicketCreated
.issued
    Mon, 27 Aug 2018 18:08:05 GMT
.expires
    Mon, 10 Sep 2018 18:08:05 GMT
```

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]
