---
title: Настройка модели удостоверения в ASP.NET Core
author: ajcvickers
description: В этой статье описывается настройка базовой модели данных Entity Framework Core для ASP.NET Core Identity.
ms.author: avickers
ms.date: 09/24/2018
uid: security/authentication/customize_identity_model
ms.openlocfilehash: 90c867eeac0e64bfe77cc7a829d61e831a2fb8e1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024781"
---
# <a name="identity-model-customization-in-aspnet-core"></a><span data-ttu-id="c19df-103">Настройка модели удостоверения в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c19df-103">Identity model customization in ASP.NET Core</span></span>

<span data-ttu-id="c19df-104">По [Артур Vickers](https://github.com/ajcvickers)</span><span class="sxs-lookup"><span data-stu-id="c19df-104">By [Arthur Vickers](https://github.com/ajcvickers)</span></span>

<span data-ttu-id="c19df-105">Удостоверение ASP.NET Core предоставляет платформу для управления и хранения учетных записей пользователей в приложениях ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c19df-105">ASP.NET Core Identity provides a framework for managing and storing user accounts in ASP.NET Core apps.</span></span> <span data-ttu-id="c19df-106">Удостоверение добавляется в проект при **учетные записи отдельных пользователей** выбран в качестве механизма проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c19df-106">Identity is added to your project when **Individual User Accounts** is selected as the authentication mechanism.</span></span> <span data-ttu-id="c19df-107">По умолчанию удостоверение позволяет использовать из Entity Framework (EF) Core модели данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-107">By default, Identity makes use of an Entity Framework (EF) Core data model.</span></span> <span data-ttu-id="c19df-108">В этой статье описывается настройка модели удостоверения.</span><span class="sxs-lookup"><span data-stu-id="c19df-108">This article describes how to customize the Identity model.</span></span>

## <a name="identity-and-ef-core-migrations"></a><span data-ttu-id="c19df-109">Удостоверение и миграций EF Core</span><span class="sxs-lookup"><span data-stu-id="c19df-109">Identity and EF Core Migrations</span></span>

<span data-ttu-id="c19df-110">Прежде чем изучать модель, это полезно для понимания принципов работы удостоверений с [миграций EF Core](/ef/core/managing-schemas/migrations/) для создания и обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-110">Before examining the model, it's useful to understand how Identity works with [EF Core Migrations](/ef/core/managing-schemas/migrations/) to create and update a database.</span></span> <span data-ttu-id="c19df-111">На верхнем уровне выполняется:</span><span class="sxs-lookup"><span data-stu-id="c19df-111">At the top level, the process is:</span></span>

1. <span data-ttu-id="c19df-112">Определение или обновление [модели данных в коде](/ef/core/modeling/).</span><span class="sxs-lookup"><span data-stu-id="c19df-112">Define or update a [data model in code](/ef/core/modeling/).</span></span>
1. <span data-ttu-id="c19df-113">Добавьте миграцию для преобразования этой модели в изменения, которые могут быть применены к базе данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-113">Add a Migration to translate this model into changes that can be applied to the database.</span></span>
1. <span data-ttu-id="c19df-114">Проверьте, что миграция правильно представляет свои намерения.</span><span class="sxs-lookup"><span data-stu-id="c19df-114">Check that the Migration correctly represents your intentions.</span></span>
1. <span data-ttu-id="c19df-115">Применение миграции для обновления базы данных должны быть синхронизированы с моделью.</span><span class="sxs-lookup"><span data-stu-id="c19df-115">Apply the Migration to update the database to be in sync with the model.</span></span>
1. <span data-ttu-id="c19df-116">Повторите шаги 1 – 4 для дополнительного уточнения модели и поддерживать синхронизацию базы данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-116">Repeat steps 1 through 4 to further refine the model and keep the database in sync.</span></span>

<span data-ttu-id="c19df-117">Для добавления и применить миграции, используйте один из следующих подходов:</span><span class="sxs-lookup"><span data-stu-id="c19df-117">Use one of the following approaches to add and apply Migrations:</span></span>

* <span data-ttu-id="c19df-118">**Консоль диспетчера пакетов** окна (PMC), если с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c19df-118">The **Package Manager Console** (PMC) window if using Visual Studio.</span></span> <span data-ttu-id="c19df-119">Дополнительные сведения см. в разделе [инструменты EF Core PMC](/ef/core/miscellaneous/cli/powershell).</span><span class="sxs-lookup"><span data-stu-id="c19df-119">For more information, see [EF Core PMC tools](/ef/core/miscellaneous/cli/powershell).</span></span>
* <span data-ttu-id="c19df-120">.NET Core CLI при помощи командной строки.</span><span class="sxs-lookup"><span data-stu-id="c19df-120">The .NET Core CLI if using the command line.</span></span> <span data-ttu-id="c19df-121">Дополнительные сведения см. в разделе [средства командной строки EF Core .NET](/ef/core/miscellaneous/cli/dotnet).</span><span class="sxs-lookup"><span data-stu-id="c19df-121">For more information, see [EF Core .NET command line tools](/ef/core/miscellaneous/cli/dotnet).</span></span>
* <span data-ttu-id="c19df-122">Щелкнув **применить миграции** кнопку на странице ошибки при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="c19df-122">Clicking the **Apply Migrations** button on the error page when the app is run.</span></span>

<span data-ttu-id="c19df-123">ASP.NET Core есть обработчик страницы ошибок во время разработки.</span><span class="sxs-lookup"><span data-stu-id="c19df-123">ASP.NET Core has a development-time error page handler.</span></span> <span data-ttu-id="c19df-124">Обработчик может применить миграции, при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="c19df-124">The handler can apply migrations when the app is run.</span></span> <span data-ttu-id="c19df-125">Для рабочих приложений, бывает необходимо создавать скрипты SQL по миграции и развертывания изменений базы данных как часть управляемой развертывания приложения и базы данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-125">For production apps, it's often more appropriate to generate SQL scripts from the migrations and deploy database changes as part of a controlled app and database deployment.</span></span>

<span data-ttu-id="c19df-126">Когда создается новое приложение с использованием удостоверения, шаги 1 и 2 выше уже были завершены.</span><span class="sxs-lookup"><span data-stu-id="c19df-126">When a new app using Identity is created, steps 1 and 2 above have already been completed.</span></span> <span data-ttu-id="c19df-127">То есть начальную модель данных уже существует, и первоначальной миграции был добавлен в проект.</span><span class="sxs-lookup"><span data-stu-id="c19df-127">That is, the initial data model already exists, and the initial migration has been added to the project.</span></span> <span data-ttu-id="c19df-128">Первоначальной миграции по-прежнему необходимо применить к базе данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-128">The initial migration still needs to be applied to the database.</span></span> <span data-ttu-id="c19df-129">Первоначальной миграции могут применяться через одну из следующих подходов:</span><span class="sxs-lookup"><span data-stu-id="c19df-129">The initial migration can be applied via one of the following approaches:</span></span>

* <span data-ttu-id="c19df-130">Запустите `Update-Database` в PMC.</span><span class="sxs-lookup"><span data-stu-id="c19df-130">Run `Update-Database` in PMC.</span></span>
* <span data-ttu-id="c19df-131">Запустите `dotnet ef database update` в командной строке.</span><span class="sxs-lookup"><span data-stu-id="c19df-131">Run `dotnet ef database update` in a command shell.</span></span>
* <span data-ttu-id="c19df-132">Нажмите кнопку **применить миграции** кнопку на странице ошибки при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="c19df-132">Click the **Apply Migrations** button on the error page when the app is run.</span></span>

<span data-ttu-id="c19df-133">Повторите предыдущие шаги, при внесении изменений в модель.</span><span class="sxs-lookup"><span data-stu-id="c19df-133">Repeat the preceding steps as changes are made to the model.</span></span>

## <a name="the-identity-model"></a><span data-ttu-id="c19df-134">Модель удостоверения</span><span class="sxs-lookup"><span data-stu-id="c19df-134">The Identity model</span></span>

### <a name="entity-types"></a><span data-ttu-id="c19df-135">Типы сущностей</span><span class="sxs-lookup"><span data-stu-id="c19df-135">Entity types</span></span>

<span data-ttu-id="c19df-136">Модель удостоверения состоит из следующих типов сущностей.</span><span class="sxs-lookup"><span data-stu-id="c19df-136">The Identity model consists of the following entity types.</span></span>

|<span data-ttu-id="c19df-137">Тип сущности</span><span class="sxs-lookup"><span data-stu-id="c19df-137">Entity type</span></span>|<span data-ttu-id="c19df-138">Описание</span><span class="sxs-lookup"><span data-stu-id="c19df-138">Description</span></span>                                                  |
|-----------|-------------------------------------------------------------|
|`User`     |<span data-ttu-id="c19df-139">Представляет пользователя.</span><span class="sxs-lookup"><span data-stu-id="c19df-139">Represents the user.</span></span>                                         |
|`Role`     |<span data-ttu-id="c19df-140">Представляет роль.</span><span class="sxs-lookup"><span data-stu-id="c19df-140">Represents a role.</span></span>                                           |
|`UserClaim`|<span data-ttu-id="c19df-141">Представляет утверждение, обладает пользователь.</span><span class="sxs-lookup"><span data-stu-id="c19df-141">Represents a claim that a user possesses.</span></span>                    |
|`UserToken`|<span data-ttu-id="c19df-142">Представляет маркер проверки подлинности для пользователя.</span><span class="sxs-lookup"><span data-stu-id="c19df-142">Represents an authentication token for a user.</span></span>               |
|`UserLogin`|<span data-ttu-id="c19df-143">Связывает пользователя с именем входа.</span><span class="sxs-lookup"><span data-stu-id="c19df-143">Associates a user with a login.</span></span>                              |
|`RoleClaim`|<span data-ttu-id="c19df-144">Представляет утверждение, эта роль присваивается всем пользователям в роли.</span><span class="sxs-lookup"><span data-stu-id="c19df-144">Represents a claim that's granted to all users within a role.</span></span>|
|`UserRole` |<span data-ttu-id="c19df-145">Сущность соединения, которая связывает пользователей и ролей.</span><span class="sxs-lookup"><span data-stu-id="c19df-145">A join entity that associates users and roles.</span></span>               |

### <a name="entity-type-relationships"></a><span data-ttu-id="c19df-146">Связи между типами сущностей</span><span class="sxs-lookup"><span data-stu-id="c19df-146">Entity type relationships</span></span>

<span data-ttu-id="c19df-147">[Типы сущностей](#entity-types) связаны друг с другом, одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="c19df-147">The [entity types](#entity-types) are related to each other in the following ways:</span></span>

* <span data-ttu-id="c19df-148">Каждый `User` может иметь множество `UserClaims`.</span><span class="sxs-lookup"><span data-stu-id="c19df-148">Each `User` can have many `UserClaims`.</span></span>
* <span data-ttu-id="c19df-149">Каждый `User` может иметь множество `UserLogins`.</span><span class="sxs-lookup"><span data-stu-id="c19df-149">Each `User` can have many `UserLogins`.</span></span>
* <span data-ttu-id="c19df-150">Каждый `User` может иметь множество `UserTokens`.</span><span class="sxs-lookup"><span data-stu-id="c19df-150">Each `User` can have many `UserTokens`.</span></span>
* <span data-ttu-id="c19df-151">Каждый `Role` может иметь несколько связанных `RoleClaims`.</span><span class="sxs-lookup"><span data-stu-id="c19df-151">Each `Role` can have many associated `RoleClaims`.</span></span>
* <span data-ttu-id="c19df-152">Каждый `User` может иметь несколько связанных `Roles`и каждый `Role` можно связать со многими `Users`.</span><span class="sxs-lookup"><span data-stu-id="c19df-152">Each `User` can have many associated `Roles`, and each `Role` can be associated with many `Users`.</span></span> <span data-ttu-id="c19df-153">Это отношение многие ко многим, нуждается в таблице соединения в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-153">This is a many-to-many relationship that requires a join table in the database.</span></span> <span data-ttu-id="c19df-154">В таблице соединения, представленного `UserRole` сущности.</span><span class="sxs-lookup"><span data-stu-id="c19df-154">The join table is represented by the `UserRole` entity.</span></span>

### <a name="default-model-configuration"></a><span data-ttu-id="c19df-155">Конфигурация модели по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c19df-155">Default model configuration</span></span>

<span data-ttu-id="c19df-156">Определяет удостоверение, многие *классы контекста* , наследуемым от <xref:Microsoft.EntityFrameworkCore.DbContext> Настройка и использование модели.</span><span class="sxs-lookup"><span data-stu-id="c19df-156">Identity defines many *context classes* that inherit from <xref:Microsoft.EntityFrameworkCore.DbContext> to configure and use the model.</span></span> <span data-ttu-id="c19df-157">Эта настройка выполняется с помощью [EF Core Fluent API для Code First](/ef/core/modeling/) в <xref:Microsoft.EntityFrameworkCore.DbContext.OnModelCreating*> метод класса контекста.</span><span class="sxs-lookup"><span data-stu-id="c19df-157">This configuration is done using the [EF Core Code First Fluent API](/ef/core/modeling/) in the <xref:Microsoft.EntityFrameworkCore.DbContext.OnModelCreating*> method of the context class.</span></span> <span data-ttu-id="c19df-158">По умолчанию используется:</span><span class="sxs-lookup"><span data-stu-id="c19df-158">The default configuration is:</span></span>

```csharp
builder.Entity<TUser>(b =>
{
    // Primary key
    b.HasKey(u => u.Id);

    // Indexes for "normalized" username and email, to allow efficient lookups
    b.HasIndex(u => u.NormalizedUserName).HasName("UserNameIndex").IsUnique();
    b.HasIndex(u => u.NormalizedEmail).HasName("EmailIndex");

    // Maps to the AspNetUsers table
    b.ToTable("AspNetUsers");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(u => u.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.UserName).HasMaxLength(256);
    b.Property(u => u.NormalizedUserName).HasMaxLength(256);
    b.Property(u => u.Email).HasMaxLength(256);
    b.Property(u => u.NormalizedEmail).HasMaxLength(256);

    // The relationships between User and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each User can have many UserClaims
    b.HasMany<TUserClaim>().WithOne().HasForeignKey(uc => uc.UserId).IsRequired();

    // Each User can have many UserLogins
    b.HasMany<TUserLogin>().WithOne().HasForeignKey(ul => ul.UserId).IsRequired();

    // Each User can have many UserTokens
    b.HasMany<TUserToken>().WithOne().HasForeignKey(ut => ut.UserId).IsRequired();

    // Each User can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.UserId).IsRequired();
});

builder.Entity<TUserClaim>(b =>
{
    // Primary key
    b.HasKey(uc => uc.Id);

    // Maps to the AspNetUserClaims table
    b.ToTable("AspNetUserClaims");
});

builder.Entity<TUserLogin>(b =>
{
    // Composite primary key consisting of the LoginProvider and the key to use
    // with that provider
    b.HasKey(l => new { l.LoginProvider, l.ProviderKey });

    // Limit the size of the composite key columns due to common DB restrictions
    b.Property(l => l.LoginProvider).HasMaxLength(128);
    b.Property(l => l.ProviderKey).HasMaxLength(128);

    // Maps to the AspNetUserLogins table
    b.ToTable("AspNetUserLogins");
});

builder.Entity<TUserToken>(b =>
{
    // Composite primary key consisting of the UserId, LoginProvider and Name
    b.HasKey(t => new { t.UserId, t.LoginProvider, t.Name });

    // Limit the size of the composite key columns due to common DB restrictions
    b.Property(t => t.LoginProvider).HasMaxLength(maxKeyLength);
    b.Property(t => t.Name).HasMaxLength(maxKeyLength);

    // Maps to the AspNetUserTokens table
    b.ToTable("AspNetUserTokens");
});

builder.Entity<TRole>(b =>
{
    // Primary key
    b.HasKey(r => r.Id);

    // Index for "normalized" role name to allow efficient lookups
    b.HasIndex(r => r.NormalizedName).HasName("RoleNameIndex").IsUnique();

    // Maps to the AspNetRoles table
    b.ToTable("AspNetRoles");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(r => r.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.Name).HasMaxLength(256);
    b.Property(u => u.NormalizedName).HasMaxLength(256);

    // The relationships between Role and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each Role can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.RoleId).IsRequired();

    // Each Role can have many associated RoleClaims
    b.HasMany<TRoleClaim>().WithOne().HasForeignKey(rc => rc.RoleId).IsRequired();
});

builder.Entity<TRoleClaim>(b =>
{
    // Primary key
    b.HasKey(rc => rc.Id);

    // Maps to the AspNetRoleClaims table
    b.ToTable("AspNetRoleClaims");
});

builder.Entity<TUserRole>(b =>
{
    // Primary key
    b.HasKey(r => new { r.UserId, r.RoleId });

    // Maps to the AspNetUserRoles table
    b.ToTable("AspNetUserRoles");
});
```

### <a name="model-generic-types"></a><span data-ttu-id="c19df-159">Универсальные типы модели</span><span class="sxs-lookup"><span data-stu-id="c19df-159">Model generic types</span></span>

<span data-ttu-id="c19df-160">По умолчанию определяет удостоверение [среда CLR](/dotnet/standard/glossary#clr) типы (CLR) для каждого типа сущности в списке выше.</span><span class="sxs-lookup"><span data-stu-id="c19df-160">Identity defines default [Common Language Runtime](/dotnet/standard/glossary#clr) (CLR) types for each of the entity types listed above.</span></span> <span data-ttu-id="c19df-161">Эти типы начинаются с *удостоверений*:</span><span class="sxs-lookup"><span data-stu-id="c19df-161">These types are all prefixed with *Identity*:</span></span>

* `IdentityUser`
* `IdentityRole`
* `IdentityUserClaim`
* `IdentityUserToken`
* `IdentityUserLogin`
* `IdentityRoleClaim`
* `IdentityUserRole`

<span data-ttu-id="c19df-162">Вместо того чтобы непосредственно использовать эти типы, типы можно использовать как базовые классы для типов приложения.</span><span class="sxs-lookup"><span data-stu-id="c19df-162">Rather than using these types directly, the types can be used as base classes for the app's own types.</span></span> <span data-ttu-id="c19df-163">`DbContext` Классы, определенные по удостоверению универсальны, таким образом, можно использовать различные типы среды CLR для одного или нескольких типов сущностей в модели.</span><span class="sxs-lookup"><span data-stu-id="c19df-163">The `DbContext` classes defined by Identity are generic, such that different CLR types can be used for one or more of the entity types in the model.</span></span> <span data-ttu-id="c19df-164">Эти универсальные типы также позволяют `User` типа первичного ключа (PK) данных должен быть изменен.</span><span class="sxs-lookup"><span data-stu-id="c19df-164">These generic types also allow the `User` primary key (PK) data type to be changed.</span></span>

<span data-ttu-id="c19df-165">При использовании удостоверений с поддержкой для ролей, <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext> должен использоваться класс.</span><span class="sxs-lookup"><span data-stu-id="c19df-165">When using Identity with support for roles, an <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext> class should be used.</span></span> <span data-ttu-id="c19df-166">Пример:</span><span class="sxs-lookup"><span data-stu-id="c19df-166">For example:</span></span>

```csharp
// Uses all the built-in Identity types
// Uses `string` as the key type
public class IdentityDbContext
    : IdentityDbContext<IdentityUser, IdentityRole, string>
{
}

// Uses the built-in Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityDbContext<TUser>
    : IdentityDbContext<TUser, IdentityRole, string>
        where TUser : IdentityUser
{
}

// Uses the built-in Identity types except with custom User and Role types
// The key type is defined by TKey
public class IdentityDbContext<TUser, TRole, TKey> : IdentityDbContext<
    TUser, TRole, TKey, IdentityUserClaim<TKey>, IdentityUserRole<TKey>,
    IdentityUserLogin<TKey>, IdentityRoleClaim<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TRole : IdentityRole<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments
// The key type is defined by TKey
public abstract class IdentityDbContext<
    TUser, TRole, TKey, TUserClaim, TUserRole, TUserLogin, TRoleClaim, TUserToken>
    : IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
         where TUser : IdentityUser<TKey>
         where TRole : IdentityRole<TKey>
         where TKey : IEquatable<TKey>
         where TUserClaim : IdentityUserClaim<TKey>
         where TUserRole : IdentityUserRole<TKey>
         where TUserLogin : IdentityUserLogin<TKey>
         where TRoleClaim : IdentityRoleClaim<TKey>
         where TUserToken : IdentityUserToken<TKey>
```

<span data-ttu-id="c19df-167">Можно также использовать удостоверение без ролей (только утверждения), в этом случае <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUserContext`1> должен использоваться класс:</span><span class="sxs-lookup"><span data-stu-id="c19df-167">It's also possible to use Identity without roles (only claims), in which case an <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUserContext`1> class should be used:</span></span>

```csharp
// Uses the built-in non-role Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityUserContext<TUser>
    : IdentityUserContext<TUser, string>
        where TUser : IdentityUser
{
}

// Uses the built-in non-role Identity types except with a custom User type
// The key type is defined by TKey
public class IdentityUserContext<TUser, TKey> : IdentityUserContext<
    TUser, TKey, IdentityUserClaim<TKey>, IdentityUserLogin<TKey>,
    IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments, with no roles
// The key type is defined by TKey
public abstract class IdentityUserContext<
    TUser, TKey, TUserClaim, TUserLogin, TUserToken> : DbContext
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
        where TUserClaim : IdentityUserClaim<TKey>
        where TUserLogin : IdentityUserLogin<TKey>
        where TUserToken : IdentityUserToken<TKey>
{
}
```

## <a name="customize-the-model"></a><span data-ttu-id="c19df-168">Настройка модели</span><span class="sxs-lookup"><span data-stu-id="c19df-168">Customize the model</span></span>

<span data-ttu-id="c19df-169">Отправной точкой для настройки модели является производным от типа соответствующего контекста.</span><span class="sxs-lookup"><span data-stu-id="c19df-169">The starting point for model customization is to derive from the appropriate context type.</span></span> <span data-ttu-id="c19df-170">См. в разделе [универсальных типов модели](#model-generic-types) раздел.</span><span class="sxs-lookup"><span data-stu-id="c19df-170">See the [Model generic types](#model-generic-types) section.</span></span> <span data-ttu-id="c19df-171">Этот тип контекста обычно вызывается `ApplicationDbContext` и создается в шаблонах ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c19df-171">This context type is customarily called `ApplicationDbContext` and is created by the ASP.NET Core templates.</span></span>

<span data-ttu-id="c19df-172">Контекст используется для настройки модели двумя способами:</span><span class="sxs-lookup"><span data-stu-id="c19df-172">The context is used to configure the model in two ways:</span></span>

* <span data-ttu-id="c19df-173">Предоставление сущности и типы ключей для параметров универсального типа.</span><span class="sxs-lookup"><span data-stu-id="c19df-173">Supplying entity and key types for the generic type parameters.</span></span>
* <span data-ttu-id="c19df-174">Переопределение `OnModelCreating` изменение сопоставления этих типов.</span><span class="sxs-lookup"><span data-stu-id="c19df-174">Overriding `OnModelCreating` to modify the mapping of these types.</span></span>

<span data-ttu-id="c19df-175">При переопределении метода `OnModelCreating`, `base.OnModelCreating` необходимо сначала вызвать; переопределения конфигурации должен быть вызван, далее.</span><span class="sxs-lookup"><span data-stu-id="c19df-175">When overriding `OnModelCreating`, `base.OnModelCreating` should be called first; the overriding configuration should be called next.</span></span> <span data-ttu-id="c19df-176">EF Core обычно имеет политику побеждает последний — один для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c19df-176">EF Core generally has a last-one-wins policy for configuration.</span></span> <span data-ttu-id="c19df-177">Например если `ToTable` сначала вызывается метод для типа сущности с именем одной таблицы и затем снова позднее с помощью другое имя таблицы, имя таблицы во втором вызове будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="c19df-177">For example, if the `ToTable` method for an entity type is called first with one table name and then again later with a different table name, the table name in the second call is used.</span></span>

### <a name="custom-user-data"></a><span data-ttu-id="c19df-178">Пользовательские данные</span><span class="sxs-lookup"><span data-stu-id="c19df-178">Custom user data</span></span>

<span data-ttu-id="c19df-179">[Пользовательские данные](xref:security/authentication/add-user-data) поддерживается путем наследования от `IdentityUser`.</span><span class="sxs-lookup"><span data-stu-id="c19df-179">[Custom user data](xref:security/authentication/add-user-data) is supported by inheriting from `IdentityUser`.</span></span> <span data-ttu-id="c19df-180">Имя этого типа обычно `ApplicationUser`:</span><span class="sxs-lookup"><span data-stu-id="c19df-180">It's customary to name this type `ApplicationUser`:</span></span>


```csharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

<span data-ttu-id="c19df-181">Используйте `ApplicationUser` тип как универсальный аргумент для контекста:</span><span class="sxs-lookup"><span data-stu-id="c19df-181">Use the `ApplicationUser` type as a generic argument for the context:</span></span>

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="c19df-182">Нет необходимости в Переопределите `OnModelCreating` в `ApplicationDbContext` класса.</span><span class="sxs-lookup"><span data-stu-id="c19df-182">There's no need to override `OnModelCreating` in the `ApplicationDbContext` class.</span></span> <span data-ttu-id="c19df-183">Сопоставляет EF Core `CustomTag` свойство по соглашению.</span><span class="sxs-lookup"><span data-stu-id="c19df-183">EF Core maps the `CustomTag` property by convention.</span></span> <span data-ttu-id="c19df-184">Тем не менее, требуется обновить, чтобы создать новую базу данных `CustomTag` столбца.</span><span class="sxs-lookup"><span data-stu-id="c19df-184">However, the database needs to be updated to create a new `CustomTag` column.</span></span> <span data-ttu-id="c19df-185">Чтобы создать столбец, добавить миграцию и затем обновить базу данных, как описано в разделе [удостоверений и миграций EF Core](#identity-and-ef-core-migrations).</span><span class="sxs-lookup"><span data-stu-id="c19df-185">To create the column, add a migration, and then update the database as described in [Identity and EF Core Migrations](#identity-and-ef-core-migrations).</span></span>

<span data-ttu-id="c19df-186">Обновление `Startup.ConfigureServices` использовать новый `ApplicationUser` класса:</span><span class="sxs-lookup"><span data-stu-id="c19df-186">Update `Startup.ConfigureServices` to use the new `ApplicationUser` class:</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
services.AddDefaultIdentity<ApplicationUser>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultUI();
```

<span data-ttu-id="c19df-187">В ASP.NET Core 2.1 или более поздней версии удостоверение предоставляется как библиотека классов Razor.</span><span class="sxs-lookup"><span data-stu-id="c19df-187">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="c19df-188">Дополнительные сведения см. в разделе <xref:security/authentication/scaffold-identity>.</span><span class="sxs-lookup"><span data-stu-id="c19df-188">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="c19df-189">Следовательно, предыдущий код требует вызова <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span><span class="sxs-lookup"><span data-stu-id="c19df-189">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="c19df-190">Если удостоверение шаблон был использован для добавления в проект файлы, удалите вызов `AddDefaultUI`.</span><span class="sxs-lookup"><span data-stu-id="c19df-190">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span> <span data-ttu-id="c19df-191">Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="c19df-191">For more information, see:</span></span>

* [<span data-ttu-id="c19df-192">Удостоверение шаблона</span><span class="sxs-lookup"><span data-stu-id="c19df-192">Scaffold Identity</span></span>](xref:security/authentication/scaffold-identity)
* [<span data-ttu-id="c19df-193">Добавление, скачивание и удаление пользовательские данные для удостоверения</span><span class="sxs-lookup"><span data-stu-id="c19df-193">Add, download, and delete custom user data to Identity</span></span>](xref:security/authentication/add-user-data)

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();
```

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
        .AddDefaultTokenProviders();
```

::: moniker-end

### <a name="change-the-primary-key-type"></a><span data-ttu-id="c19df-194">Изменение типа первичного ключа</span><span class="sxs-lookup"><span data-stu-id="c19df-194">Change the primary key type</span></span>

<span data-ttu-id="c19df-195">Изменение типа данных столбца первичного ключа после создания базы данных является проблемой для многих систем баз данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-195">A change to the PK column's data type after the database has been created is problematic on many database systems.</span></span> <span data-ttu-id="c19df-196">Изменение первичный ключ обычно включает в себя удаление и повторное создание таблицы.</span><span class="sxs-lookup"><span data-stu-id="c19df-196">Changing the PK typically involves dropping and re-creating the table.</span></span> <span data-ttu-id="c19df-197">Таким образом типы ключей должны быть заданы в первоначальной миграции, при создании базы данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-197">Therefore, key types should be specified in the initial migration when the database is created.</span></span>

<span data-ttu-id="c19df-198">Выполните следующие действия, чтобы изменить тип первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="c19df-198">Follow these steps to change the PK type:</span></span>

1. <span data-ttu-id="c19df-199">Если база данных была создана перед изменением первичного ключа, запустите `Drop-Database` (PMC) или `dotnet ef database drop` (CLI) .NET Core для его удаления.</span><span class="sxs-lookup"><span data-stu-id="c19df-199">If the database was created before the PK change, run `Drop-Database` (PMC) or `dotnet ef database drop` (.NET Core CLI) to delete it.</span></span>
2. <span data-ttu-id="c19df-200">После подтверждения удаления базы данных, удалите первоначальной миграции с `Remove-Migration` (PMC) или `dotnet ef migrations remove` (.NET Core CLI).</span><span class="sxs-lookup"><span data-stu-id="c19df-200">After confirming deletion of the database, remove the initial migration with `Remove-Migration` (PMC) or `dotnet ef migrations remove` (.NET Core CLI).</span></span>
3. <span data-ttu-id="c19df-201">Обновление `ApplicationDbContext` класса для наследования от <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext`3>.</span><span class="sxs-lookup"><span data-stu-id="c19df-201">Update the `ApplicationDbContext` class to derive from <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext`3>.</span></span> <span data-ttu-id="c19df-202">Укажите новый тип ключа для `TKey`.</span><span class="sxs-lookup"><span data-stu-id="c19df-202">Specify the new key type for `TKey`.</span></span> <span data-ttu-id="c19df-203">Например, чтобы использовать `Guid` тип ключа:</span><span class="sxs-lookup"><span data-stu-id="c19df-203">For example, to use a `Guid` key type:</span></span>

    ```csharp
    public class ApplicationDbContext
        : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

    ::: moniker range=">= aspnetcore-2.0"

    <span data-ttu-id="c19df-204">В приведенном выше коде универсальные классы <xref:Microsoft.AspNetCore.Identity.IdentityUser`1> и <xref:Microsoft.AspNetCore.Identity.IdentityRole`1> должен быть указан для использования нового типа ключа.</span><span class="sxs-lookup"><span data-stu-id="c19df-204">In the preceding code, the generic classes <xref:Microsoft.AspNetCore.Identity.IdentityUser`1> and <xref:Microsoft.AspNetCore.Identity.IdentityRole`1> must be specified to use the new key type.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    <span data-ttu-id="c19df-205">В приведенном выше коде универсальные классы <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUser`1> и <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityRole`1> должен быть указан для использования нового типа ключа.</span><span class="sxs-lookup"><span data-stu-id="c19df-205">In the preceding code, the generic classes <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUser`1> and <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityRole`1> must be specified to use the new key type.</span></span>

    ::: moniker-end

    <span data-ttu-id="c19df-206">`Startup.ConfigureServices` должны быть обновлены для использования универсального пользователя:</span><span class="sxs-lookup"><span data-stu-id="c19df-206">`Startup.ConfigureServices` must be updated to use the generic user:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    ```csharp
    services.AddDefaultIdentity<IdentityUser<Guid>>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    ```csharp
    services.AddIdentity<IdentityUser<Guid>, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    ```csharp
    services.AddIdentity<IdentityUser<Guid>, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

4. <span data-ttu-id="c19df-207">Если пользовательский `ApplicationUser` класс используется, обновите наследование от класса `IdentityUser`.</span><span class="sxs-lookup"><span data-stu-id="c19df-207">If a custom `ApplicationUser` class is being used, update the class to inherit from `IdentityUser`.</span></span> <span data-ttu-id="c19df-208">Пример:</span><span class="sxs-lookup"><span data-stu-id="c19df-208">For example:</span></span>

    ::: moniker range="<= aspnetcore-1.1"

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Models/ApplicationUser.cs?name=snippet_ApplicationUser&highlight=4)]

    ::: moniker-end

    ::: moniker range=">= aspnetcore-2.0"

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationUser.cs?name=snippet_ApplicationUser&highlight=4)]

    ::: moniker-end

    <span data-ttu-id="c19df-209">Обновление `ApplicationDbContext` для ссылки на пользовательский `ApplicationUser` класса:</span><span class="sxs-lookup"><span data-stu-id="c19df-209">Update `ApplicationDbContext` to reference the custom `ApplicationUser` class:</span></span>

    ```csharp
    public class ApplicationDbContext
        : IdentityDbContext<ApplicationUser, IdentityRole<Guid>, Guid>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

    <span data-ttu-id="c19df-210">Зарегистрируйте класс контекста пользовательской базы данных, при добавлении службы удостоверений в `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="c19df-210">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    ```csharp
    services.AddDefaultIdentity<ApplicationUser>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultUI()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="c19df-211">Тип данных первичный ключ определяется путем анализа <xref:Microsoft.EntityFrameworkCore.DbContext> объекта.</span><span class="sxs-lookup"><span data-stu-id="c19df-211">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    <span data-ttu-id="c19df-212">В ASP.NET Core 2.1 или более поздней версии удостоверение предоставляется как библиотека классов Razor.</span><span class="sxs-lookup"><span data-stu-id="c19df-212">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="c19df-213">Дополнительные сведения см. в разделе <xref:security/authentication/scaffold-identity>.</span><span class="sxs-lookup"><span data-stu-id="c19df-213">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="c19df-214">Следовательно, предыдущий код требует вызова <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span><span class="sxs-lookup"><span data-stu-id="c19df-214">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="c19df-215">Если удостоверение шаблон был использован для добавления в проект файлы, удалите вызов `AddDefaultUI`.</span><span class="sxs-lookup"><span data-stu-id="c19df-215">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span>

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="c19df-216">Тип данных первичный ключ определяется путем анализа <xref:Microsoft.EntityFrameworkCore.DbContext> объекта.</span><span class="sxs-lookup"><span data-stu-id="c19df-216">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="c19df-217"><xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> Метод принимает `TKey` тип первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="c19df-217">The <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> method accepts a `TKey` type indicating the primary key's data type.</span></span>

    ::: moniker-end

5. <span data-ttu-id="c19df-218">Если пользовательский `ApplicationRole` класс используется, обновите наследование от класса `IdentityRole<TKey>`.</span><span class="sxs-lookup"><span data-stu-id="c19df-218">If a custom `ApplicationRole` class is being used, update the class to inherit from `IdentityRole<TKey>`.</span></span> <span data-ttu-id="c19df-219">Пример:</span><span class="sxs-lookup"><span data-stu-id="c19df-219">For example:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationRole.cs?name=snippet_ApplicationRole&highlight=4)]

    <span data-ttu-id="c19df-220">Обновление `ApplicationDbContext` для ссылки на пользовательский `ApplicationRole` класса.</span><span class="sxs-lookup"><span data-stu-id="c19df-220">Update `ApplicationDbContext` to reference the custom `ApplicationRole` class.</span></span> <span data-ttu-id="c19df-221">Например, следующий класс ссылается на пользовательский `ApplicationUser` и пользовательское `ApplicationRole`:</span><span class="sxs-lookup"><span data-stu-id="c19df-221">For example, the following class references a custom `ApplicationUser` and a custom `ApplicationRole`:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="c19df-222">Зарегистрируйте класс контекста пользовательской базы данных, при добавлении службы удостоверений в `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="c19df-222">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=13-16)]

    <span data-ttu-id="c19df-223">Тип данных первичный ключ определяется путем анализа <xref:Microsoft.EntityFrameworkCore.DbContext> объекта.</span><span class="sxs-lookup"><span data-stu-id="c19df-223">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    <span data-ttu-id="c19df-224">В ASP.NET Core 2.1 или более поздней версии удостоверение предоставляется как библиотека классов Razor.</span><span class="sxs-lookup"><span data-stu-id="c19df-224">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="c19df-225">Дополнительные сведения см. в разделе <xref:security/authentication/scaffold-identity>.</span><span class="sxs-lookup"><span data-stu-id="c19df-225">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="c19df-226">Следовательно, предыдущий код требует вызова <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span><span class="sxs-lookup"><span data-stu-id="c19df-226">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="c19df-227">Если удостоверение шаблон был использован для добавления в проект файлы, удалите вызов `AddDefaultUI`.</span><span class="sxs-lookup"><span data-stu-id="c19df-227">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span>

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    [!code-csharp[](customize-identity-model/samples/2.0/RazorPagesSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="c19df-228">Зарегистрируйте класс контекста пользовательской базы данных, при добавлении службы удостоверений в `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="c19df-228">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.0/RazorPagesSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

    <span data-ttu-id="c19df-229">Тип данных первичный ключ определяется путем анализа <xref:Microsoft.EntityFrameworkCore.DbContext> объекта.</span><span class="sxs-lookup"><span data-stu-id="c19df-229">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="c19df-230">Зарегистрируйте класс контекста пользовательской базы данных, при добавлении службы удостоверений в `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="c19df-230">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

    <span data-ttu-id="c19df-231"><xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> Метод принимает `TKey` тип первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="c19df-231">The <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> method accepts a `TKey` type indicating the primary key's data type.</span></span>

    ::: moniker-end

### <a name="add-navigation-properties"></a><span data-ttu-id="c19df-232">Добавление свойства навигации</span><span class="sxs-lookup"><span data-stu-id="c19df-232">Add navigation properties</span></span>

<span data-ttu-id="c19df-233">Изменение конфигурации модели для связи может оказаться сложнее, чем вносить другие изменения.</span><span class="sxs-lookup"><span data-stu-id="c19df-233">Changing the model configuration for relationships can be more difficult than making other changes.</span></span> <span data-ttu-id="c19df-234">Замените существующие связи, а не новые, создать дополнительные связи необходимо соблюдать осторожность.</span><span class="sxs-lookup"><span data-stu-id="c19df-234">Care must be taken to replace the existing relationships rather than create new, additional relationships.</span></span> <span data-ttu-id="c19df-235">В частности измененные связи необходимо указать же свойства внешнего ключа (FK) как существующую связь.</span><span class="sxs-lookup"><span data-stu-id="c19df-235">In particular, the changed relationship must specify the same foreign key (FK) property as the existing relationship.</span></span> <span data-ttu-id="c19df-236">Например, связь между `Users` и `UserClaims` является, по умолчанию задан следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c19df-236">For example, the relationship between `Users` and `UserClaims` is, by default, specified as follows:</span></span>

```csharp
builder.Entity<TUser>(b =>
{
    // Each User can have many UserClaims
    b.HasMany<TUserClaim>()
     .WithOne()
     .HasForeignKey(uc => uc.UserId)
     .IsRequired();
});
```

<span data-ttu-id="c19df-237">Для этого отношения внешнего ключа указывается как `UserClaim.UserId` свойство.</span><span class="sxs-lookup"><span data-stu-id="c19df-237">The FK for this relationship is specified as the `UserClaim.UserId` property.</span></span> <span data-ttu-id="c19df-238">`HasMany` и `WithOne` можно вызвать без аргументов для создания связи без свойства навигации.</span><span class="sxs-lookup"><span data-stu-id="c19df-238">`HasMany` and `WithOne` are called without arguments to create the relationship without navigation properties.</span></span>

<span data-ttu-id="c19df-239">Добавьте свойство навигации, чтобы `ApplicationUser` , позволяющий связанные `UserClaims` ссылка от пользователя:</span><span class="sxs-lookup"><span data-stu-id="c19df-239">Add a navigation property to `ApplicationUser` that allows associated `UserClaims` to be referenced from the user:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

<span data-ttu-id="c19df-240">`TKey` Для `IdentityUserClaim<TKey>` — это тип, указанный для первичного ключа пользователей.</span><span class="sxs-lookup"><span data-stu-id="c19df-240">The `TKey` for `IdentityUserClaim<TKey>` is the type specified for the PK of users.</span></span> <span data-ttu-id="c19df-241">В этом случае `TKey` является `string` так, как используются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c19df-241">In this case, `TKey` is `string` because the defaults are being used.</span></span> <span data-ttu-id="c19df-242">Он имеет **не** тип первичного ключа для `UserClaim` типа сущности.</span><span class="sxs-lookup"><span data-stu-id="c19df-242">It's **not** the PK type for the `UserClaim` entity type.</span></span>

<span data-ttu-id="c19df-243">Теперь, когда существует свойство навигации, должно быть настроено в `OnModelCreating`:</span><span class="sxs-lookup"><span data-stu-id="c19df-243">Now that the navigation property exists, it must be configured in `OnModelCreating`:</span></span>

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();
        });
    }
}
```

<span data-ttu-id="c19df-244">Обратите внимание на то, что связь настроен так же, как ранее, только с помощью свойства навигации, указанного в вызове `HasMany`.</span><span class="sxs-lookup"><span data-stu-id="c19df-244">Notice that relationship is configured exactly as it was before, only with a navigation property specified in the call to `HasMany`.</span></span>

<span data-ttu-id="c19df-245">Свойства навигации существуют только в модель EF, а не в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-245">The navigation properties only exist in the EF model, not the database.</span></span> <span data-ttu-id="c19df-246">Так как для связи внешнего ключа не изменилось, такое изменение модели не требует обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-246">Because the FK for the relationship hasn't changed, this kind of model change doesn't require the database to be updated.</span></span> <span data-ttu-id="c19df-247">Это можно проверить путем добавления миграции после внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="c19df-247">This can be checked by adding a migration after making the change.</span></span> <span data-ttu-id="c19df-248">`Up` И `Down` методы являются пустыми.</span><span class="sxs-lookup"><span data-stu-id="c19df-248">The `Up` and `Down` methods are empty.</span></span>

### <a name="add-all-user-navigation-properties"></a><span data-ttu-id="c19df-249">Добавить все свойства навигации пользователя</span><span class="sxs-lookup"><span data-stu-id="c19df-249">Add all User navigation properties</span></span>

<span data-ttu-id="c19df-250">Используя в качестве рекомендации в разделе выше, в следующем примере настраивается свойства односторонней навигации для всех отношений пользователя:</span><span class="sxs-lookup"><span data-stu-id="c19df-250">Using the section above as guidance, the following example configures unidirectional navigation properties for all relationships on User:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<IdentityUserRole<string>> UserRoles { get; set; }
}
```

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne()
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });
    }
}
```

### <a name="add-user-and-role-navigation-properties"></a><span data-ttu-id="c19df-251">Добавление свойства навигации пользователя и роли</span><span class="sxs-lookup"><span data-stu-id="c19df-251">Add User and Role navigation properties</span></span>

<span data-ttu-id="c19df-252">Используя в качестве рекомендации в разделе выше, в следующем примере настраивается свойства навигации для всех отношений на пользователя и роли:</span><span class="sxs-lookup"><span data-stu-id="c19df-252">Using the section above as guidance, the following example configures navigation properties for all relationships on User and Role:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}
```

```csharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        IdentityUserClaim<string>, ApplicationUserRole, IdentityUserLogin<string>,
        IdentityRoleClaim<string>, IdentityUserToken<string>>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();
        });

    }
}
```

<span data-ttu-id="c19df-253">Примечания.</span><span class="sxs-lookup"><span data-stu-id="c19df-253">Notes:</span></span>

* <span data-ttu-id="c19df-254">Этот пример также включает `UserRole` сущности, который необходим для перемещения по связи многие ко многим от пользователей к ролям соединения.</span><span class="sxs-lookup"><span data-stu-id="c19df-254">This example also includes the `UserRole` join entity, which is needed to navigate the many-to-many relationship from Users to Roles.</span></span>
* <span data-ttu-id="c19df-255">Не забудьте изменить типы свойства навигации, соответствующим образом `ApplicationXxx` вместо теперь используются типы `IdentityXxx` типов.</span><span class="sxs-lookup"><span data-stu-id="c19df-255">Remember to change the types of the navigation properties to reflect that `ApplicationXxx` types are now being used instead of `IdentityXxx` types.</span></span>
* <span data-ttu-id="c19df-256">Не забывайте использовать `ApplicationXxx` в универсальном `ApplicationContext` определения.</span><span class="sxs-lookup"><span data-stu-id="c19df-256">Remember to use the `ApplicationXxx` in the generic `ApplicationContext` definition.</span></span>

### <a name="add-all-navigation-properties"></a><span data-ttu-id="c19df-257">Добавить все свойства навигации</span><span class="sxs-lookup"><span data-stu-id="c19df-257">Add all navigation properties</span></span>

<span data-ttu-id="c19df-258">Используя в качестве рекомендации в разделе выше, в следующем примере настраивается свойства навигации для всех связей для всех типов сущностей:</span><span class="sxs-lookup"><span data-stu-id="c19df-258">Using the section above as guidance, the following example configures navigation properties for all relationships on all entity types:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<ApplicationUserClaim> Claims { get; set; }
    public virtual ICollection<ApplicationUserLogin> Logins { get; set; }
    public virtual ICollection<ApplicationUserToken> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
    public virtual ICollection<ApplicationRoleClaim> RoleClaims { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserClaim : IdentityUserClaim<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationUserLogin : IdentityUserLogin<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationRoleClaim : IdentityRoleClaim<string>
{
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserToken : IdentityUserToken<string>
{
    public virtual ApplicationUser User { get; set; }
}
```

```csharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        ApplicationUserClaim, ApplicationUserRole, ApplicationUserLogin,
        ApplicationRoleClaim, ApplicationUserToken>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne(e => e.User)
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne(e => e.User)
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne(e => e.User)
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();

            // Each Role can have many associated RoleClaims
            b.HasMany(e => e.RoleClaims)
                .WithOne(e => e.Role)
                .HasForeignKey(rc => rc.RoleId)
                .IsRequired();
        });
    }
}
```

### <a name="use-composite-keys"></a><span data-ttu-id="c19df-259">Используйте составные ключи</span><span class="sxs-lookup"><span data-stu-id="c19df-259">Use composite keys</span></span>

<span data-ttu-id="c19df-260">Предыдущих разделах демонстрируется изменение типа ключа, используемого в модели удостоверения.</span><span class="sxs-lookup"><span data-stu-id="c19df-260">The preceding sections demonstrated changing the type of key used in the Identity model.</span></span> <span data-ttu-id="c19df-261">Изменение ключа модели удостоверения с помощью составных ключей не поддерживается и не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="c19df-261">Changing the Identity key model to use composite keys isn't supported or recommended.</span></span> <span data-ttu-id="c19df-262">С помощью составного ключа с удостоверением включает в себя изменение, как код Identity manager взаимодействует с моделью.</span><span class="sxs-lookup"><span data-stu-id="c19df-262">Using a composite key with Identity involves changing how the Identity manager code interacts with the model.</span></span> <span data-ttu-id="c19df-263">Такая настройка выходит за рамки настоящего документа.</span><span class="sxs-lookup"><span data-stu-id="c19df-263">This customization is beyond the scope of this document.</span></span>

### <a name="change-tablecolumn-names-and-facets"></a><span data-ttu-id="c19df-264">Изменения имен таблицы или столбца и аспекты</span><span class="sxs-lookup"><span data-stu-id="c19df-264">Change table/column names and facets</span></span>

<span data-ttu-id="c19df-265">Чтобы изменить имена таблиц и столбцов, вызовите `base.OnModelCreating`.</span><span class="sxs-lookup"><span data-stu-id="c19df-265">To change the names of tables and columns, call `base.OnModelCreating`.</span></span> <span data-ttu-id="c19df-266">Затем добавьте конфигурацию, чтобы переопределить любые параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c19df-266">Then, add configuration to override any of the defaults.</span></span> <span data-ttu-id="c19df-267">Например, для изменения имени всех таблиц удостоверений:</span><span class="sxs-lookup"><span data-stu-id="c19df-267">For example, to change the name of all the Identity tables:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.ToTable("MyUsers");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.ToTable("MyUserClaims");
    });

    modelBuilder.Entity<IdentityUserLogin<string>>(b =>
    {
        b.ToTable("MyUserLogins");
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.ToTable("MyUserTokens");
    });

    modelBuilder.Entity<IdentityRole>(b =>
    {
        b.ToTable("MyRoles");
    });

    modelBuilder.Entity<IdentityRoleClaim<string>>(b =>
    {
        b.ToTable("MyRoleClaims");
    });

    modelBuilder.Entity<IdentityUserRole<string>>(b =>
    {
        b.ToTable("MyUserRoles");
    });
}
```

<span data-ttu-id="c19df-268">Эти примеры используют типы удостоверений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c19df-268">These examples use the default Identity types.</span></span> <span data-ttu-id="c19df-269">При использовании типа приложения, такие как `ApplicationUser`, настройка этого типа вместо типа по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c19df-269">If using an app type such as `ApplicationUser`, configure that type instead of the default type.</span></span>

<span data-ttu-id="c19df-270">В следующем примере изменяется некоторые имена столбцов:</span><span class="sxs-lookup"><span data-stu-id="c19df-270">The following example changes some column names:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(e => e.Email).HasColumnName("EMail");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.Property(e => e.ClaimType).HasColumnName("CType");
        b.Property(e => e.ClaimValue).HasColumnName("CValue");
    });
}
```

<span data-ttu-id="c19df-271">Некоторые типы столбцов базы данных можно настроить с определенными *аспекты* (например, максимально `string` допустимая длина).</span><span class="sxs-lookup"><span data-stu-id="c19df-271">Some types of database columns can be configured with certain *facets* (for example, the maximum `string` length allowed).</span></span> <span data-ttu-id="c19df-272">В следующем примере задается максимальная длина столбца для нескольких `string` свойства в модели:</span><span class="sxs-lookup"><span data-stu-id="c19df-272">The following example sets column maximum lengths for several `string` properties in the model:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(u => u.UserName).HasMaxLength(128);
        b.Property(u => u.NormalizedUserName).HasMaxLength(128);
        b.Property(u => u.Email).HasMaxLength(128);
        b.Property(u => u.NormalizedEmail).HasMaxLength(128);
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.Property(t => t.LoginProvider).HasMaxLength(128);
        b.Property(t => t.Name).HasMaxLength(128);
    });
}
```

### <a name="map-to-a-different-schema"></a><span data-ttu-id="c19df-273">Сопоставление в другую схему</span><span class="sxs-lookup"><span data-stu-id="c19df-273">Map to a different schema</span></span>

<span data-ttu-id="c19df-274">Схемы может вести себя по-разному для поставщиков базы данных.</span><span class="sxs-lookup"><span data-stu-id="c19df-274">Schemas can behave differently across database providers.</span></span> <span data-ttu-id="c19df-275">Для SQL Server по умолчанию является создание всех таблиц в *dbo* схемы.</span><span class="sxs-lookup"><span data-stu-id="c19df-275">For SQL Server, the default is to create all tables in the *dbo* schema.</span></span> <span data-ttu-id="c19df-276">Таблицы могут создаваться в другой схеме.</span><span class="sxs-lookup"><span data-stu-id="c19df-276">The tables can be created in a different schema.</span></span> <span data-ttu-id="c19df-277">Пример:</span><span class="sxs-lookup"><span data-stu-id="c19df-277">For example:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

::: moniker range=">= aspnetcore-2.1"

### <a name="lazy-loading"></a><span data-ttu-id="c19df-278">Отложенная загрузка</span><span class="sxs-lookup"><span data-stu-id="c19df-278">Lazy loading</span></span>

<span data-ttu-id="c19df-279">В этом разделе добавляется поддержка прокси отложенной загрузки в модель удостоверения.</span><span class="sxs-lookup"><span data-stu-id="c19df-279">In this section, support for lazy-loading proxies in the Identity model is added.</span></span> <span data-ttu-id="c19df-280">Lazy загрузка полезен в тех случаях, так как он позволяет использовать без убедитесь, что они при загрузке свойства навигации.</span><span class="sxs-lookup"><span data-stu-id="c19df-280">Lazy-loading is useful since it allows navigation properties to be used without first ensuring they're loaded.</span></span>

<span data-ttu-id="c19df-281">Типы сущностей можно сделать для отложенной загрузки несколькими способами, как описано в разделе [документации по EF Core](/ef/core/querying/related-data#lazy-loading).</span><span class="sxs-lookup"><span data-stu-id="c19df-281">Entity types can be made suitable for lazy-loading in several ways, as described in the [EF Core documentation](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="c19df-282">Для простоты используйте прокси отложенной загрузки, которая требует:</span><span class="sxs-lookup"><span data-stu-id="c19df-282">For simplicity, use lazy-loading proxies, which requires:</span></span>

* <span data-ttu-id="c19df-283">Установка [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) пакета.</span><span class="sxs-lookup"><span data-stu-id="c19df-283">Installation of the [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) package.</span></span>
* <span data-ttu-id="c19df-284">Вызов <xref:Microsoft.EntityFrameworkCore.ProxiesExtensions.UseLazyLoadingProxies*> внутри <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*>.</span><span class="sxs-lookup"><span data-stu-id="c19df-284">A call to <xref:Microsoft.EntityFrameworkCore.ProxiesExtensions.UseLazyLoadingProxies*> inside <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*>.</span></span>
* <span data-ttu-id="c19df-285">Типы общей сущности с `public virtual` свойства навигации.</span><span class="sxs-lookup"><span data-stu-id="c19df-285">Public entity types with `public virtual` navigation properties.</span></span>

<span data-ttu-id="c19df-286">В следующем примере показан вызов `UseLazyLoadingProxies` в `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="c19df-286">The following example demonstrates calling `UseLazyLoadingProxies` in `Startup.ConfigureServices`:</span></span>

```csharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
              .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="c19df-287">См. приведенные выше примеры, инструкции по добавлению свойств навигации в типы сущностей.</span><span class="sxs-lookup"><span data-stu-id="c19df-287">Refer to the preceding examples for guidance on adding navigation properties to the entity types.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c19df-288">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c19df-288">Additional resources</span></span>

* <xref:security/authentication/scaffold-identity>

::: moniker-end
