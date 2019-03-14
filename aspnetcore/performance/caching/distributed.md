---
title: Распределенное кэширование в ASP.NET Core
author: guardrex
description: Сведения об использовании ASP.NET Core распределенного кэша для повышения производительности приложения и масштабируемости, особенно в среде фермы облаком и сервером.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: performance/caching/distributed
ms.openlocfilehash: 7337ee3b823064c942832d8a44e4d4289bc4fd0e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052411"
---
# <a name="distributed-caching-in-aspnet-core"></a><span data-ttu-id="797b9-103">Распределенное кэширование в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="797b9-103">Distributed caching in ASP.NET Core</span></span>

<span data-ttu-id="797b9-104">Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith) и [Люк Лэтем](https://github.com/guardrex) (Luke Latham)</span><span class="sxs-lookup"><span data-stu-id="797b9-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="797b9-105">Распределенный кэш — это кэш, который совместно используется несколькими серверами приложений, обычно поддерживаются как внешняя служба на серверы приложений, обращающихся к ней.</span><span class="sxs-lookup"><span data-stu-id="797b9-105">A distributed cache is a cache shared by multiple app servers, typically maintained as an external service to the app servers that access it.</span></span> <span data-ttu-id="797b9-106">Распределенный кэш может повысить производительность и масштабируемость приложения ASP.NET Core, особенно в том случае, если приложение будет размещено в облачную службу или ферме серверов.</span><span class="sxs-lookup"><span data-stu-id="797b9-106">A distributed cache can improve the performance and scalability of an ASP.NET Core app, especially when the app is hosted by a cloud service or a server farm.</span></span>

<span data-ttu-id="797b9-107">Распределенный кэш имеет ряд преимуществ по сравнению с другими кэширования сценариев, где кэшированные данные хранятся на серверах отдельных приложений.</span><span class="sxs-lookup"><span data-stu-id="797b9-107">A distributed cache has several advantages over other caching scenarios where cached data is stored on individual app servers.</span></span>

<span data-ttu-id="797b9-108">Когда кэшированные данные распределяются, эти данные:</span><span class="sxs-lookup"><span data-stu-id="797b9-108">When cached data is distributed, the data:</span></span>

* <span data-ttu-id="797b9-109">— *Согласовано* (согласованный) между запросами на несколько серверов.</span><span class="sxs-lookup"><span data-stu-id="797b9-109">Is *coherent* (consistent) across requests to multiple servers.</span></span>
* <span data-ttu-id="797b9-110">Сохранять работоспособность после перезагрузки сервера и развертывания приложений.</span><span class="sxs-lookup"><span data-stu-id="797b9-110">Survives server restarts and app deployments.</span></span>
* <span data-ttu-id="797b9-111">Не использует локальную память.</span><span class="sxs-lookup"><span data-stu-id="797b9-111">Doesn't use local memory.</span></span>

<span data-ttu-id="797b9-112">Конфигурация распределенного кэша зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="797b9-112">Distributed cache configuration is implementation specific.</span></span> <span data-ttu-id="797b9-113">В этой статье описывается, как настроить SQL Server и распределенные кэши Redis.</span><span class="sxs-lookup"><span data-stu-id="797b9-113">This article describes how to configure SQL Server and Redis distributed caches.</span></span> <span data-ttu-id="797b9-114">Реализации сторонних также доступны, такие как [NCache](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache на сайте GitHub](https://github.com/Alachisoft/NCache)).</span><span class="sxs-lookup"><span data-stu-id="797b9-114">Third party implementations are also available, such as [NCache](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache on GitHub](https://github.com/Alachisoft/NCache)).</span></span> <span data-ttu-id="797b9-115">Независимо от того, какую реализацию установлен, приложение взаимодействует с кэша, используя <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> интерфейс.</span><span class="sxs-lookup"><span data-stu-id="797b9-115">Regardless of which implementation is selected, the app interacts with the cache using the <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface.</span></span>

<span data-ttu-id="797b9-116">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/samples/) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="797b9-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="797b9-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="797b9-117">Prerequisites</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="797b9-118">Использование SQL Server распределенный кеш, справочник по [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) или добавьте ссылку на пакет [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-118">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="797b9-119">Для использования Redis распределенный кеш, справочник по [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) и добавьте ссылку на пакет [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-119">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) and add a package reference to the [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis) package.</span></span> <span data-ttu-id="797b9-120">Пакет Redis не включен в `Microsoft.AspNetCore.App` пакета, поэтому необходимо сослаться на пакет, Redis отдельно в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="797b9-120">The Redis package isn't included in the `Microsoft.AspNetCore.App` package, so you must reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="797b9-121">Использование SQL Server распределенный кеш, справочник по [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) или добавьте ссылку на пакет [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-121">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="797b9-122">Для использования Redis распределенный кеш, справочник по [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) и добавьте ссылку на пакет [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-122">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) and add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span> <span data-ttu-id="797b9-123">Пакет Redis не включен в `Microsoft.AspNetCore.App` пакета, поэтому необходимо сослаться на пакет, Redis отдельно в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="797b9-123">The Redis package isn't included in the `Microsoft.AspNetCore.App` package, so you must reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="797b9-124">Использование SQL Server распределенный кеш, справочник по [метапакет Microsoft.AspNetCore.All](xref:fundamentals/metapackage) или добавьте ссылку на пакет [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-124">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="797b9-125">Для использования Redis распределенный кеш, справочник по [метапакет Microsoft.AspNetCore.All](xref:fundamentals/metapackage) или добавьте ссылку на пакет [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-125">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span> <span data-ttu-id="797b9-126">Redis пакет включен в `Microsoft.AspNetCore.All` пакета, поэтому не нужно сослаться на пакет Redis отдельно в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="797b9-126">The Redis package is included in `Microsoft.AspNetCore.All` package, so you don't need to reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="797b9-127">Чтобы использовать экземпляр SQL Server распределенный кеш, добавьте ссылку на пакет [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-127">To use a SQL Server distributed cache, add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="797b9-128">Для использования Redis распределенный кеш, добавьте ссылку на пакет [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) пакета.</span><span class="sxs-lookup"><span data-stu-id="797b9-128">To use a Redis distributed cache, add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span>

::: moniker-end

## <a name="idistributedcache-interface"></a><span data-ttu-id="797b9-129">Интерфейс IDistributedCache</span><span class="sxs-lookup"><span data-stu-id="797b9-129">IDistributedCache interface</span></span>

<span data-ttu-id="797b9-130"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> Интерфейс предоставляет следующие методы для работы с элементами в реализации распределенного кэша:</span><span class="sxs-lookup"><span data-stu-id="797b9-130">The <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface provides the following methods to manipulate items in the distributed cache implementation:</span></span>

* <span data-ttu-id="797b9-131"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Get*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.GetAsync*> &ndash; Принимает ключ строкового типа и извлекает кэшированного элемента как `byte[]` массив Если найдена в кэше.</span><span class="sxs-lookup"><span data-stu-id="797b9-131"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Get*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.GetAsync*> &ndash; Accepts a string key and retrieves a cached item as a `byte[]` array if found in the cache.</span></span>
* <span data-ttu-id="797b9-132"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Set*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.SetAsync*> &ndash; Добавляет элемент (как `byte[]` массива) в кэш, с помощью строкового ключа.</span><span class="sxs-lookup"><span data-stu-id="797b9-132"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Set*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.SetAsync*> &ndash; Adds an item (as `byte[]` array) to the cache using a string key.</span></span>
* <span data-ttu-id="797b9-133"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Refresh*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RefreshAsync*> &ndash; Обновляет объект в кэше, по его ключу, сброс его скользящее время ожидания (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="797b9-133"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Refresh*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RefreshAsync*> &ndash; Refreshes an item in the cache based on its key, resetting its sliding expiration timeout (if any).</span></span>
* <span data-ttu-id="797b9-134"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Remove*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RemoveAsync*> &ndash; Удаляет элемент кэша на основе его строку ключа.</span><span class="sxs-lookup"><span data-stu-id="797b9-134"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Remove*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RemoveAsync*> &ndash; Removes a cache item based on its string key.</span></span>

## <a name="establish-distributed-caching-services"></a><span data-ttu-id="797b9-135">Установить службы распределенного кэширования</span><span class="sxs-lookup"><span data-stu-id="797b9-135">Establish distributed caching services</span></span>

<span data-ttu-id="797b9-136">Зарегистрируйте реализацию <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> в `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="797b9-136">Register an implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="797b9-137">Предоставляемые платформой реализации, описанных в этом разделе включают:</span><span class="sxs-lookup"><span data-stu-id="797b9-137">Framework-provided implementations described in this topic include:</span></span>

* [<span data-ttu-id="797b9-138">Распределенные памяти кэша</span><span class="sxs-lookup"><span data-stu-id="797b9-138">Distributed Memory Cache</span></span>](#distributed-memory-cache)
* [<span data-ttu-id="797b9-139">Распределенный кэш SQL Server</span><span class="sxs-lookup"><span data-stu-id="797b9-139">Distributed SQL Server cache</span></span>](#distributed-sql-server-cache)
* [<span data-ttu-id="797b9-140">Распределенный кэш Redis</span><span class="sxs-lookup"><span data-stu-id="797b9-140">Distributed Redis cache</span></span>](#distributed-redis-cache)

### <a name="distributed-memory-cache"></a><span data-ttu-id="797b9-141">Распределенные памяти кэша</span><span class="sxs-lookup"><span data-stu-id="797b9-141">Distributed Memory Cache</span></span>

<span data-ttu-id="797b9-142">Распределенного кэша в памяти (<xref:Microsoft.Extensions.DependencyInjection.MemoryCacheServiceCollectionExtensions.AddDistributedMemoryCache*>) — это реализация предоставляемые платформой <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> , сохраняет элементы в памяти.</span><span class="sxs-lookup"><span data-stu-id="797b9-142">The Distributed Memory Cache (<xref:Microsoft.Extensions.DependencyInjection.MemoryCacheServiceCollectionExtensions.AddDistributedMemoryCache*>) is a framework-provided implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> that stores items in memory.</span></span> <span data-ttu-id="797b9-143">Распределенный кеш памяти не фактический распределенного кэша.</span><span class="sxs-lookup"><span data-stu-id="797b9-143">The Distributed Memory Cache isn't an actual distributed cache.</span></span> <span data-ttu-id="797b9-144">Кэшированные элементы хранятся в экземпляре приложения на сервере, где выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="797b9-144">Cached items are stored by the app instance on the server where the app is running.</span></span>

<span data-ttu-id="797b9-145">Распределенным кэшем памяти — это полезные реализация:</span><span class="sxs-lookup"><span data-stu-id="797b9-145">The Distributed Memory Cache is a useful implementation:</span></span>

* <span data-ttu-id="797b9-146">В сценариях разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="797b9-146">In development and testing scenarios.</span></span>
* <span data-ttu-id="797b9-147">При использовании одного сервера в рабочей среде и потребление памяти не является проблемой.</span><span class="sxs-lookup"><span data-stu-id="797b9-147">When a single server is used in production and memory consumption isn't an issue.</span></span> <span data-ttu-id="797b9-148">Реализация краткие описания распределенным кэшем памяти в кэше хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="797b9-148">Implementing the Distributed Memory Cache abstracts cached data storage.</span></span> <span data-ttu-id="797b9-149">Он позволяет реализовать настоящую распределенного кэширования решения в будущем в случае нескольких узлов или привести к необходимости устойчивость к сбоям.</span><span class="sxs-lookup"><span data-stu-id="797b9-149">It allows for implementing a true distributed caching solution in the future if multiple nodes or fault tolerance become necessary.</span></span>

<span data-ttu-id="797b9-150">Пример приложения использует распределенного кэша в памяти при запуске приложения в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="797b9-150">The sample app makes use of the Distributed Memory Cache when the app is run in the Development environment:</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_ConfigureServices&highlight=5)]

### <a name="distributed-sql-server-cache"></a><span data-ttu-id="797b9-151">Кэш распределенных SQL Server</span><span class="sxs-lookup"><span data-stu-id="797b9-151">Distributed SQL Server Cache</span></span>

<span data-ttu-id="797b9-152">Реализация распределенного кэша SQL Server (<xref:Microsoft.Extensions.DependencyInjection.SqlServerCachingServicesExtensions.AddDistributedSqlServerCache*>) позволяет распределенного кэша использовать базу данных SQL Server в качестве резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="797b9-152">The Distributed SQL Server Cache implementation (<xref:Microsoft.Extensions.DependencyInjection.SqlServerCachingServicesExtensions.AddDistributedSqlServerCache*>) allows the distributed cache to use a SQL Server database as its backing store.</span></span> <span data-ttu-id="797b9-153">Чтобы создать таблицу SQL Server кэшированного элемента в экземпляр SQL Server, можно использовать `sql-cache` средство.</span><span class="sxs-lookup"><span data-stu-id="797b9-153">To create a SQL Server cached item table in a SQL Server instance, you can use the `sql-cache` tool.</span></span> <span data-ttu-id="797b9-154">Средство создает таблицу с именем и схемой, указанной вами.</span><span class="sxs-lookup"><span data-stu-id="797b9-154">The tool creates a table with the name and schema that you specify.</span></span>

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="797b9-155">Добавить `SqlConfig.Tools` для `<ItemGroup>` элемент файла проекта и выполните `dotnet restore`.</span><span class="sxs-lookup"><span data-stu-id="797b9-155">Add `SqlConfig.Tools` to the `<ItemGroup>` element of the project file and run `dotnet restore`.</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.Extensions.Caching.SqlConfig.Tools"
                          Version="2.0.2" />
</ItemGroup>
```

::: moniker-end

<span data-ttu-id="797b9-156">Создать таблицу в SQL Server, выполнив `sql-cache create` команды.</span><span class="sxs-lookup"><span data-stu-id="797b9-156">Create a table in SQL Server by running the `sql-cache create` command.</span></span> <span data-ttu-id="797b9-157">Укажите экземпляр SQL Server (`Data Source`), базы данных (`Initial Catalog`), схемы (например, `dbo`) и имя таблицы (например, `TestCache`):</span><span class="sxs-lookup"><span data-stu-id="797b9-157">Provide the SQL Server instance (`Data Source`), database (`Initial Catalog`), schema (for example, `dbo`), and table name (for example, `TestCache`):</span></span>

```console
dotnet sql-cache create "Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
```

<span data-ttu-id="797b9-158">Чтобы указать, что средство успешно записывается сообщение:</span><span class="sxs-lookup"><span data-stu-id="797b9-158">A message is logged to indicate that the tool was successful:</span></span>

```console
Table and index were created successfully.
```

<span data-ttu-id="797b9-159">Таблицу, созданную `sql-cache` средство имеет следующую схему:</span><span class="sxs-lookup"><span data-stu-id="797b9-159">The table created by the `sql-cache` tool has the following schema:</span></span>

![Таблицы кэша SqlServer](distributed/_static/SqlServerCacheTable.png)

> [!NOTE]
> <span data-ttu-id="797b9-161">Приложение следует управлять значения кэша, используя экземпляр <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>, а не <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache>.</span><span class="sxs-lookup"><span data-stu-id="797b9-161">An app should manipulate cache values using an instance of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>, not a <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache>.</span></span>

<span data-ttu-id="797b9-162">Пример приложения реализует <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache> в среде не разработки:</span><span class="sxs-lookup"><span data-stu-id="797b9-162">The sample app implements <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache> in a non-Development environment:</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_ConfigureServices&highlight=9-15)]

> [!NOTE]
> <span data-ttu-id="797b9-163">Объект <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.ConnectionString*> (и при необходимости <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.SchemaName*> и <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.TableName*>) обычно хранятся вне системы управления версиями (например, хранимая с [Secret Manager](xref:security/app-secrets) или в *appsettings.json* / *appsettings. {Среда} .json* файлов).</span><span class="sxs-lookup"><span data-stu-id="797b9-163">A <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.ConnectionString*> (and optionally, <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.SchemaName*> and <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.TableName*>) are typically stored outside of source control (for example, stored by the [Secret Manager](xref:security/app-secrets) or in *appsettings.json*/*appsettings.{Environment}.json* files).</span></span> <span data-ttu-id="797b9-164">Строка подключения может содержать учетные данные, которые должны храниться вне системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="797b9-164">The connection string may contain credentials that should be kept out of source control systems.</span></span>

### <a name="distributed-redis-cache"></a><span data-ttu-id="797b9-165">Кэш Redis для распределенных</span><span class="sxs-lookup"><span data-stu-id="797b9-165">Distributed Redis Cache</span></span>

<span data-ttu-id="797b9-166">[Redis](https://redis.io/) -это хранилище данных в памяти с открытым исходным кодом, которое часто используется в качестве распределенного кэша.</span><span class="sxs-lookup"><span data-stu-id="797b9-166">[Redis](https://redis.io/) is an open source in-memory data store, which is often used as a distributed cache.</span></span> <span data-ttu-id="797b9-167">Redis можно использовать локально, и можно настроить [кэша Redis для Azure](https://azure.microsoft.com/services/cache/) для приложения ASP.NET Core, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="797b9-167">You can use Redis locally, and you can configure an [Azure Redis Cache](https://azure.microsoft.com/services/cache/) for an Azure-hosted ASP.NET Core app.</span></span> <span data-ttu-id="797b9-168">Приложения настраивает реализации кэша с помощью <xref:Microsoft.Extensions.Caching.Redis.RedisCache> экземпляра (<xref:Microsoft.Extensions.DependencyInjection.RedisCacheServiceCollectionExtensions.AddDistributedRedisCache*>):</span><span class="sxs-lookup"><span data-stu-id="797b9-168">An app configures the cache implementation using a <xref:Microsoft.Extensions.Caching.Redis.RedisCache> instance (<xref:Microsoft.Extensions.DependencyInjection.RedisCacheServiceCollectionExtensions.AddDistributedRedisCache*>):</span></span>

```csharp
services.AddDistributedRedisCache(options =>
{
    options.Configuration = "localhost";
    options.InstanceName = "SampleInstance";
});
```

<span data-ttu-id="797b9-169">Чтобы установить Redis на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="797b9-169">To install Redis on your local machine:</span></span>

* <span data-ttu-id="797b9-170">Установка [Chocolatey Redis пакета](https://chocolatey.org/packages/redis-64/).</span><span class="sxs-lookup"><span data-stu-id="797b9-170">Install the [Chocolatey Redis package](https://chocolatey.org/packages/redis-64/).</span></span>
* <span data-ttu-id="797b9-171">Запустите `redis-server` из командной строки.</span><span class="sxs-lookup"><span data-stu-id="797b9-171">Run `redis-server` from a command prompt.</span></span>

## <a name="use-the-distributed-cache"></a><span data-ttu-id="797b9-172">Использование распределенного кэша</span><span class="sxs-lookup"><span data-stu-id="797b9-172">Use the distributed cache</span></span>

<span data-ttu-id="797b9-173">Чтобы использовать <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> интерфейсом, запросить экземпляр <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> из любого конструктора в приложении.</span><span class="sxs-lookup"><span data-stu-id="797b9-173">To use the <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface, request an instance of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> from any constructor in the app.</span></span> <span data-ttu-id="797b9-174">Экземпляр предоставляется [внедрения зависимостей (DI)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="797b9-174">The instance is provided by [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span>

<span data-ttu-id="797b9-175">При запуске приложения, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> внедряется в `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="797b9-175">When the app starts, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> is injected into `Startup.Configure`.</span></span> <span data-ttu-id="797b9-176">Текущее время кэшируется с помощью <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime> (Дополнительные сведения см. в разделе [веб-узел: Интерфейс IApplicationLifetime](xref:fundamentals/host/web-host#iapplicationlifetime-interface)):</span><span class="sxs-lookup"><span data-stu-id="797b9-176">The current time is cached using <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime> (for more information, see [Web Host: IApplicationLifetime interface](xref:fundamentals/host/web-host#iapplicationlifetime-interface)):</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_Configure&highlight=10)]

<span data-ttu-id="797b9-177">Пример приложения внедряет <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> в `IndexModel` для использования на странице индекса.</span><span class="sxs-lookup"><span data-stu-id="797b9-177">The sample app injects <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> into the `IndexModel` for use by the Index page.</span></span>

<span data-ttu-id="797b9-178">Каждый раз при загрузке страницы индекса кэша проверяется на время кэширования в `OnGetAsync`.</span><span class="sxs-lookup"><span data-stu-id="797b9-178">Each time the Index page is loaded, the cache is checked for the cached time in `OnGetAsync`.</span></span> <span data-ttu-id="797b9-179">Если время кэширования еще не истек, отображается время.</span><span class="sxs-lookup"><span data-stu-id="797b9-179">If the cached time hasn't expired, the time is displayed.</span></span> <span data-ttu-id="797b9-180">Если 20 секунд, истекших с момента последнего обращения к время кэширования (последний раз страница была загружена), на странице отображается *кэшированных Time Expired*.</span><span class="sxs-lookup"><span data-stu-id="797b9-180">If 20 seconds have elapsed since the last time the cached time was accessed (the last time this page was loaded), the page displays *Cached Time Expired*.</span></span>

<span data-ttu-id="797b9-181">Немедленно обновить кэшированные время на текущий момент времени, выбрав **сбросить время кэширования** кнопки.</span><span class="sxs-lookup"><span data-stu-id="797b9-181">Immediately update the cached time to the current time by selecting the **Reset Cached Time** button.</span></span> <span data-ttu-id="797b9-182">Триггеры кнопку `OnPostResetCachedTime` метод обработчика.</span><span class="sxs-lookup"><span data-stu-id="797b9-182">The button triggers the `OnPostResetCachedTime` handler method.</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Pages/Index.cshtml.cs?name=snippet_IndexModel&highlight=7,14-20,25-29)]

> [!NOTE]
> <span data-ttu-id="797b9-183">Время жизни экземпляров <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> (по крайней мере, для встроенных реализаций) не обязательно должно быть ограничено одним объектом или блоком.</span><span class="sxs-lookup"><span data-stu-id="797b9-183">There's no need to use a Singleton or Scoped lifetime for <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instances (at least for the built-in implementations).</span></span>
>
> <span data-ttu-id="797b9-184">Вы также можете создать <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> экземпляра везде, где это может потребоваться, а не с помощью внедрения Зависимостей, но создание экземпляра в коде может сделать код труднее тестировать и нарушает [принципу явных зависимостей](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span><span class="sxs-lookup"><span data-stu-id="797b9-184">You can also create an <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instance wherever you might need one instead of using DI, but creating an instance in code can make your code harder to test and violates the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span></span>

## <a name="recommendations"></a><span data-ttu-id="797b9-185">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="797b9-185">Recommendations</span></span>

<span data-ttu-id="797b9-186">При принятии решения о реализации <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> лучше всего подходит для вашего приложения, необходимо учитывать следующее:</span><span class="sxs-lookup"><span data-stu-id="797b9-186">When deciding which implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> is best for your app, consider the following:</span></span>

* <span data-ttu-id="797b9-187">Существующую инфраструктуру</span><span class="sxs-lookup"><span data-stu-id="797b9-187">Existing infrastructure</span></span>
* <span data-ttu-id="797b9-188">Требования к производительности</span><span class="sxs-lookup"><span data-stu-id="797b9-188">Performance requirements</span></span>
* <span data-ttu-id="797b9-189">Стоимость</span><span class="sxs-lookup"><span data-stu-id="797b9-189">Cost</span></span>
* <span data-ttu-id="797b9-190">Опыт рабочей группы</span><span class="sxs-lookup"><span data-stu-id="797b9-190">Team experience</span></span>

<span data-ttu-id="797b9-191">Решения кэширования обычно используют хранилище в памяти для предоставления быстрого получения кэшированных данных, но память является ограниченным ресурсом и дорогостоящей развернуть.</span><span class="sxs-lookup"><span data-stu-id="797b9-191">Caching solutions usually rely on in-memory storage to provide fast retrieval of cached data, but memory is a limited resource and costly to expand.</span></span> <span data-ttu-id="797b9-192">Только хранилище часто использовать данные в кэше.</span><span class="sxs-lookup"><span data-stu-id="797b9-192">Only store commonly used data in a cache.</span></span>

<span data-ttu-id="797b9-193">Как правило кэш Redis обеспечивает высокую пропускную способность и меньшую задержку, чем при использовании кэша SQL Server.</span><span class="sxs-lookup"><span data-stu-id="797b9-193">Generally, a Redis cache provides higher throughput and lower latency than a SQL Server cache.</span></span> <span data-ttu-id="797b9-194">Тем не менее тестирование производительности обычно требуется, чтобы определить характеристики производительности стратегии кэширования.</span><span class="sxs-lookup"><span data-stu-id="797b9-194">However, benchmarking is usually required to determine the performance characteristics of caching strategies.</span></span>

<span data-ttu-id="797b9-195">Когда SQL Server используется в качестве резервного хранилища распределенного кэша, использовать ту же базу данных для кэша и хранения обычных данных приложения и извлечения может отрицательно повлиять на их производительность.</span><span class="sxs-lookup"><span data-stu-id="797b9-195">When SQL Server is used as a distributed cache backing store, use of the same database for the cache and the app's ordinary data storage and retrieval can negatively impact the performance of both.</span></span> <span data-ttu-id="797b9-196">Мы рекомендуем использовать выделенный экземпляр SQL Server для распределенного кэша, резервным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="797b9-196">We recommend using a dedicated SQL Server instance for the distributed cache backing store.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="797b9-197">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="797b9-197">Additional resources</span></span>

* [<span data-ttu-id="797b9-198">Кэш в Azure redis</span><span class="sxs-lookup"><span data-stu-id="797b9-198">Redis Cache on Azure</span></span>](https://azure.microsoft.com/documentation/services/redis-cache/)
* [<span data-ttu-id="797b9-199">База данных SQL в Azure</span><span class="sxs-lookup"><span data-stu-id="797b9-199">SQL Database on Azure</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* <span data-ttu-id="797b9-200">[Поставщик IDistributedCache для NCache в веб-ферм с ASP.NET Core](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache на сайте GitHub](https://github.com/Alachisoft/NCache))</span><span class="sxs-lookup"><span data-stu-id="797b9-200">[ASP.NET Core IDistributedCache Provider for NCache in Web Farms](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache on GitHub](https://github.com/Alachisoft/NCache))</span></span>
* <xref:performance/caching/memory>
* <xref:fundamentals/change-tokens>
* <xref:performance/caching/response>
* <xref:performance/caching/middleware>
* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper>
* <xref:host-and-deploy/web-farm>
