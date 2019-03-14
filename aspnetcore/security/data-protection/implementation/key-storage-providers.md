---
title: Поставщики хранилища ключей в ASP.NET Core
author: rick-anderson
description: Дополнительные сведения о поставщиках хранилища ключей в ASP.NET Core и как настроить расположения хранилища ключей.
ms.author: riande
ms.date: 12/19/2018
uid: security/data-protection/implementation/key-storage-providers
ms.openlocfilehash: d6dabc9e4581e0891d1dd14f73e086d50b45bba4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054451"
---
# <a name="key-storage-providers-in-aspnet-core"></a><span data-ttu-id="ced43-103">Поставщики хранилища ключей в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ced43-103">Key storage providers in ASP.NET Core</span></span>

<span data-ttu-id="ced43-104">Система защиты данных [использует механизм обнаружения по умолчанию](xref:security/data-protection/configuration/default-settings) для определения, где должны сохраняться криптографических ключей.</span><span class="sxs-lookup"><span data-stu-id="ced43-104">The data protection system [employs a discovery mechanism by default](xref:security/data-protection/configuration/default-settings) to determine where cryptographic keys should be persisted.</span></span> <span data-ttu-id="ced43-105">Разработчик может переопределить механизм обнаружения по умолчанию и вручную указать расположение.</span><span class="sxs-lookup"><span data-stu-id="ced43-105">The developer can override the default discovery mechanism and manually specify the location.</span></span>

> [!WARNING]
> <span data-ttu-id="ced43-106">При указании опции явные постоянство ключа, система защиты данных отменяет регистрацию ключа шифрования по умолчанию механизм rest, поэтому ключи не шифруются при хранении.</span><span class="sxs-lookup"><span data-stu-id="ced43-106">If you specify an explicit key persistence location, the data protection system deregisters the default key encryption at rest mechanism, so keys are no longer encrypted at rest.</span></span> <span data-ttu-id="ced43-107">Рекомендуется, вы Кроме того [укажите механизм явного ключа шифрования](xref:security/data-protection/implementation/key-encryption-at-rest) для развертывания в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ced43-107">It's recommended that you additionally [specify an explicit key encryption mechanism](xref:security/data-protection/implementation/key-encryption-at-rest) for production deployments.</span></span>

## <a name="file-system"></a><span data-ttu-id="ced43-108">Файловая система</span><span class="sxs-lookup"><span data-stu-id="ced43-108">File system</span></span>

<span data-ttu-id="ced43-109">Чтобы настроить файл на основе системы ключа репозиторием, вызовите [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) конфигурации подпрограммы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ced43-109">To configure a file system-based key repository, call the [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) configuration routine as shown below.</span></span> <span data-ttu-id="ced43-110">Укажите [DirectoryInfo](/dotnet/api/system.io.directoryinfo) указанием на репозиторий, где должны храниться ключи:</span><span class="sxs-lookup"><span data-stu-id="ced43-110">Provide a [DirectoryInfo](/dotnet/api/system.io.directoryinfo) pointing to the repository where keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"c:\temp-keys\"));
}
```

<span data-ttu-id="ced43-111">`DirectoryInfo` Можно указать папку на локальном компьютере, или он может указывать на папку в общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="ced43-111">The `DirectoryInfo` can point to a directory on the local machine, or it can point to a folder on a network share.</span></span> <span data-ttu-id="ced43-112">Если указывает на каталог на локальном компьютере (и в случае, является то, что только приложения на локальном компьютере требуется доступ, чтобы использовать этот репозиторий), рассмотрите возможность использования [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (в Windows) для шифрования ключей при хранении.</span><span class="sxs-lookup"><span data-stu-id="ced43-112">If pointing to a directory on the local machine (and the scenario is that only apps on the local machine require access to use this repository), consider using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (on Windows) to encrypt the keys at rest.</span></span> <span data-ttu-id="ced43-113">В противном случае рассмотрите возможность использования [сертификат X.509](xref:security/data-protection/implementation/key-encryption-at-rest) для шифрования ключей при хранении.</span><span class="sxs-lookup"><span data-stu-id="ced43-113">Otherwise, consider using an [X.509 certificate](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt keys at rest.</span></span>

## <a name="azure-and-redis"></a><span data-ttu-id="ced43-114">Azure и Redis</span><span class="sxs-lookup"><span data-stu-id="ced43-114">Azure and Redis</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="ced43-115">[Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) и [Microsoft.AspNetCore.DataProtection.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.StackExchangeRedis/) пакетов разрешено хранить ключи защиты данных в хранилище Azure или Redis кэш.</span><span class="sxs-lookup"><span data-stu-id="ced43-115">The [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) and [Microsoft.AspNetCore.DataProtection.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.StackExchangeRedis/) packages allow storing data protection keys in Azure Storage or a Redis cache.</span></span> <span data-ttu-id="ced43-116">Ключи могут совместно использоваться в нескольких экземплярах веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ced43-116">Keys can be shared across several instances of a web app.</span></span> <span data-ttu-id="ced43-117">Приложения могут совместно использовать файлы cookie проверки подлинности или CSRF защиты на нескольких серверах.</span><span class="sxs-lookup"><span data-stu-id="ced43-117">Apps can share authentication cookies or CSRF protection across multiple servers.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="ced43-118">[Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) и [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) пакетов разрешено хранить ключи защиты данных в хранилище Azure или кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="ced43-118">The [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) and [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) packages allow storing data protection keys in Azure Storage or a Redis cache.</span></span> <span data-ttu-id="ced43-119">Ключи могут совместно использоваться в нескольких экземплярах веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ced43-119">Keys can be shared across several instances of a web app.</span></span> <span data-ttu-id="ced43-120">Приложения могут совместно использовать файлы cookie проверки подлинности или CSRF защиты на нескольких серверах.</span><span class="sxs-lookup"><span data-stu-id="ced43-120">Apps can share authentication cookies or CSRF protection across multiple servers.</span></span>

::: moniker-end

<span data-ttu-id="ced43-121">Чтобы настроить поставщик хранилища больших двоичных объектов Azure, вызовите один из [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) перегрузки:</span><span class="sxs-lookup"><span data-stu-id="ced43-121">To configure the Azure Blob Storage provider, call one of the [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blob URI including SAS token>"));
}
```

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="ced43-122">Чтобы настроить на Redis, вызовите один из [PersistKeysToStackExchangeRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.stackexchangeredisdataprotectionbuilderextensions.persistkeystostackexchangeredis) перегрузки:</span><span class="sxs-lookup"><span data-stu-id="ced43-122">To configure on Redis, call one of the [PersistKeysToStackExchangeRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.stackexchangeredisdataprotectionbuilderextensions.persistkeystostackexchangeredis) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToStackExchangeRedis(redis, "DataProtection-Keys");
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="ced43-123">Чтобы настроить на Redis, вызовите один из [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) перегрузки:</span><span class="sxs-lookup"><span data-stu-id="ced43-123">To configure on Redis, call one of the [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToRedis(redis, "DataProtection-Keys");
}
```

::: moniker-end

<span data-ttu-id="ced43-124">Дополнительные сведения см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="ced43-124">For more information, see the following topics:</span></span>

* [<span data-ttu-id="ced43-125">StackExchange.Redis ConnectionMultiplexer</span><span class="sxs-lookup"><span data-stu-id="ced43-125">StackExchange.Redis ConnectionMultiplexer</span></span>](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Basics.md)
* [<span data-ttu-id="ced43-126">Кэш Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="ced43-126">Azure Redis Cache</span></span>](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache#connect-to-the-cache)
* [<span data-ttu-id="ced43-127">Примеры ASPNET/DataProtection</span><span class="sxs-lookup"><span data-stu-id="ced43-127">aspnet/DataProtection samples</span></span>](https://github.com/aspnet/AspNetCore/tree/2.2.0/src/DataProtection/samples)

## <a name="registry"></a><span data-ttu-id="ced43-128">Реестр</span><span class="sxs-lookup"><span data-stu-id="ced43-128">Registry</span></span>

<span data-ttu-id="ced43-129">**Применяется только для развертывания Windows.**</span><span class="sxs-lookup"><span data-stu-id="ced43-129">**Only applies to Windows deployments.**</span></span>

<span data-ttu-id="ced43-130">Иногда приложение может не иметь доступ на запись в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="ced43-130">Sometimes the app might not have write access to the file system.</span></span> <span data-ttu-id="ced43-131">Рассмотрим ситуацию, где приложение выполняется как учетная запись виртуальной службы (такие как *w3wp.exe*удостоверение пула приложений).</span><span class="sxs-lookup"><span data-stu-id="ced43-131">Consider a scenario where an app is running as a virtual service account (such as *w3wp.exe*'s app pool identity).</span></span> <span data-ttu-id="ced43-132">В этом случае администратор может подготовить раздел реестра, доступную учетную запись службы.</span><span class="sxs-lookup"><span data-stu-id="ced43-132">In these cases, the administrator can provision a registry key that's accessible by the service account identity.</span></span> <span data-ttu-id="ced43-133">Вызовите [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) метод расширения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ced43-133">Call the [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) extension method as shown below.</span></span> <span data-ttu-id="ced43-134">Укажите [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) указывает на место хранения криптографических ключей:</span><span class="sxs-lookup"><span data-stu-id="ced43-134">Provide a [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) pointing to the location where cryptographic keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToRegistry(Registry.CurrentUser.OpenSubKey(@"SOFTWARE\Sample\keys"));
}
```

> [!IMPORTANT]
> <span data-ttu-id="ced43-135">Мы рекомендуем использовать [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) для шифрования ключей при хранении.</span><span class="sxs-lookup"><span data-stu-id="ced43-135">We recommend using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt the keys at rest.</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="entity-framework-core"></a><span data-ttu-id="ced43-136">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="ced43-136">Entity Framework Core</span></span>

<span data-ttu-id="ced43-137">[Microsoft.AspNetCore.DataProtection.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.EntityFrameworkCore/) пакет предоставляет механизм для хранения ключей защиты данных в базу данных с помощью Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="ced43-137">The [Microsoft.AspNetCore.DataProtection.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.EntityFrameworkCore/) package provides a mechanism for storing data protection keys to a database using Entity Framework Core.</span></span> <span data-ttu-id="ced43-138">`Microsoft.AspNetCore.DataProtection.EntityFrameworkCore` Пакет NuGet должны добавляться в файл проекта не является частью [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app).</span><span class="sxs-lookup"><span data-stu-id="ced43-138">The `Microsoft.AspNetCore.DataProtection.EntityFrameworkCore` NuGet package must be added to the project file, it's not part of the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

<span data-ttu-id="ced43-139">При использовании этого пакета ключи могут совместно использоваться несколькими экземплярами веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ced43-139">With this package, keys can be shared across multiple instances of a web app.</span></span>

<span data-ttu-id="ced43-140">Чтобы настроить поставщика EF Core, вызовите [ `PersistKeysToDbContext<TContext>` ](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcoredataprotectionextensions.persistkeystodbcontext) метод:</span><span class="sxs-lookup"><span data-stu-id="ced43-140">To configure the EF Core provider, call the [`PersistKeysToDbContext<TContext>`](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcoredataprotectionextensions.persistkeystodbcontext) method:</span></span>

[!code-csharp[Main](key-storage-providers/sample/Startup.cs?name=snippet&highlight=13-15)]

<span data-ttu-id="ced43-141">Универсальный параметр `TContext`, должен наследовать от [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) и [IDataProtectionKeyContext](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcore.idataprotectionkeycontext):</span><span class="sxs-lookup"><span data-stu-id="ced43-141">The generic parameter, `TContext`, must inherit from [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) and [IDataProtectionKeyContext](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcore.idataprotectionkeycontext):</span></span>

[!code-csharp[Main](key-storage-providers/sample/MyKeysContext.cs)]

<span data-ttu-id="ced43-142">Создание `DataProtectionKeys` таблицы.</span><span class="sxs-lookup"><span data-stu-id="ced43-142">Create the `DataProtectionKeys` table.</span></span> 

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="ced43-143">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ced43-143">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="ced43-144">Выполните следующие команды в **консоль диспетчера пакетов** окна (PMC):</span><span class="sxs-lookup"><span data-stu-id="ced43-144">Execute the following commands in the **Package Manager Console** (PMC) window:</span></span>

```PowerShell
Add-Migration AddDataProtectionKeys -Context MyKeysContext
Update-Database -Context MyKeysContext
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="ced43-145">Интерфейс командной строки .NET Core</span><span class="sxs-lookup"><span data-stu-id="ced43-145">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="ced43-146">Выполните следующие команды в командной строке:</span><span class="sxs-lookup"><span data-stu-id="ced43-146">Execute the following commands in a command shell:</span></span>

```console
dotnet ef migrations add AddDataProtectionKeys --context MyKeysContext
dotnet ef database update --context MyKeysContext
```

---

<span data-ttu-id="ced43-147">`MyKeysContext` является `DbContext` определенный в предыдущем примере кода.</span><span class="sxs-lookup"><span data-stu-id="ced43-147">`MyKeysContext` is the `DbContext` defined in the preceding code sample.</span></span> <span data-ttu-id="ced43-148">Если вы используете `DbContext` с другим именем, замените вашей `DbContext` имя `MyKeysContext`.</span><span class="sxs-lookup"><span data-stu-id="ced43-148">If you're using a `DbContext` with a different name, substitute your `DbContext` name for `MyKeysContext`.</span></span>

<span data-ttu-id="ced43-149">`DataProtectionKeys` На сущность класса принимает структуру, представленную в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="ced43-149">The `DataProtectionKeys` class/entity adopts the structure shown in the following table.</span></span>

| <span data-ttu-id="ced43-150">Свойство или поле</span><span class="sxs-lookup"><span data-stu-id="ced43-150">Property/Field</span></span> | <span data-ttu-id="ced43-151">Тип CLR</span><span class="sxs-lookup"><span data-stu-id="ced43-151">CLR Type</span></span> | <span data-ttu-id="ced43-152">Тип SQL</span><span class="sxs-lookup"><span data-stu-id="ced43-152">SQL Type</span></span>              |
| -------------- | -------- | --------------------- |
| `Id`           | `int`    | <span data-ttu-id="ced43-153">`int`, Первичный ключ, не равно null</span><span class="sxs-lookup"><span data-stu-id="ced43-153">`int`, PK, not null</span></span>   |
| `FriendlyName` | `string` | <span data-ttu-id="ced43-154">`nvarchar(MAX)`, значение null</span><span class="sxs-lookup"><span data-stu-id="ced43-154">`nvarchar(MAX)`, null</span></span> |
| `Xml`          | `string` | <span data-ttu-id="ced43-155">`nvarchar(MAX)`, значение null</span><span class="sxs-lookup"><span data-stu-id="ced43-155">`nvarchar(MAX)`, null</span></span> |

::: moniker-end

## <a name="custom-key-repository"></a><span data-ttu-id="ced43-156">Пользовательский репозиторий ключа</span><span class="sxs-lookup"><span data-stu-id="ced43-156">Custom key repository</span></span>

<span data-ttu-id="ced43-157">Если механизмы в поле не подходит, разработчик может указать собственный механизм сохраняемости ключа, предоставляя пользовательский [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository).</span><span class="sxs-lookup"><span data-stu-id="ced43-157">If the in-box mechanisms aren't appropriate, the developer can specify their own key persistence mechanism by providing a custom [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository).</span></span>
