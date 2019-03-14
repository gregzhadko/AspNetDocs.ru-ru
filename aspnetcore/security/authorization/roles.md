---
title: Ролевая авторизация в ASP.NET Core
author: rick-anderson
description: Узнайте, как ограничить доступ контроллера и действия в ASP.NET Core, передав атрибут Authorize ролей.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/roles
ms.openlocfilehash: c38e7144166ce7741eee6e3acb4d1c952ad4f024
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054381"
---
# <a name="role-based-authorization-in-aspnet-core"></a>Ролевая авторизация в ASP.NET Core

<a name="security-authorization-role-based"></a>

При создании удостоверения может принадлежать одной или нескольких ролей. Например Трейси может принадлежать к роли администратора и пользователя, пока Скотт может принадлежать только к роли пользователя. Как эти роли создаются и управляются зависит от хранилище процесса авторизации. Роли имеют доступ к деятельность разработчика [IsInRole](/dotnet/api/system.security.principal.genericprincipal.isinrole) метод [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal) класса.

## <a name="adding-role-checks"></a>Добавление проверки роли

Проверки авторизации на основе ролей являются декларативными&mdash;разработчик внедряет их в свой код от контроллера или действия в контроллере, определения ролей, которые текущий пользователь должен быть членом для доступа к запрошенному ресурсу.

Например, следующий код ограничивает доступ ко всем действиям на `AdministrationController` пользователям, являются членами `Administrator` роли:

```csharp
[Authorize(Roles = "Administrator")]
public class AdministrationController : Controller
{
}
```

Можно указать несколько ролей в виде списка с разделителями-запятыми:

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

Этот контроллер не превысит доступными пользователям, которые являются членами объекта `HRManager` роли или `Finance` роли.

Если применить несколько атрибутов доступ к пользователю необходимо быть членом всех ролей, указанных; Следующий пример требует, что пользователь должен быть одновременно членом групп `PowerUser` и `ControlPanelUser` роли.

```csharp
[Authorize(Roles = "PowerUser")]
[Authorize(Roles = "ControlPanelUser")]
public class ControlPanelController : Controller
{
}
```

Ограничить доступ, применив атрибуты авторизации дополнительных ролей на уровне действия:

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

В предыдущем коде фрагмент кода членах `Administrator` роли или `PowerUser` роли контроллера и `SetTime` действие, но только члены `Administrator` роли `ShutDown` действие.

Можно также заблокировать контроллера, но Разрешить анонимные, не прошедшие проверку подлинности доступа к отдельным действиям.

```csharp
[Authorize]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [AllowAnonymous]
    public ActionResult Login()
    {
    }
}
```

::: moniker range=">= aspnetcore-2.0"

Для страниц Razor `AuthorizeAttribute` можно применить, либо:

* С помощью [соглашение](xref:razor-pages/razor-pages-conventions#page-model-action-conventions), или
* Применение `AuthorizeAttribute` для `PageModel` экземпляр:

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public class UpdateModel : PageModel
{
    public ActionResult OnPost()
    {
    }
}
```

> [!IMPORTANT]
> Фильтрация атрибутов, включая `AuthorizeAttribute`, может применяться только к модели страницы и не может применяться к определенной странице методы обработчика.
::: moniker-end


<a name="security-authorization-role-policy"></a>

## <a name="policy-based-role-checks"></a>Проверок роли на основе политик

Требования к роли могут также выражаться с помощью нового синтаксиса политики, где разработчик регистрирует политику при запуске как часть конфигурации службы авторизации. Это обычно происходит в `ConfigureServices()` в вашей *Startup.cs* файла.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("RequireAdministratorRole",
             policy => policy.RequireRole("Administrator"));
    });
}
```

Политики применяются с помощью `Policy` свойство `AuthorizeAttribute` атрибута:

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public IActionResult Shutdown()
{
    return View();
}
```

Если вы хотите указать несколько ролей, разрешенных в требования, а затем их можно указать в качестве параметров для `RequireRole` метод:

```csharp
options.AddPolicy("ElevatedRights", policy =>
                  policy.RequireRole("Administrator", "PowerUser", "BackupAdministrator"));
```

В этом примере разрешает пользователям, принадлежащим к `Administrator`, `PowerUser` или `BackupAdministrator` ролей.

### <a name="add-role-services-to-identity"></a>Добавление служб роли удостоверению

Добавление [AddRoles](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) для добавления служб ролей:

[!code-csharp[](roles/samples/Startup.cs?name=snippet&highlight=7)]
