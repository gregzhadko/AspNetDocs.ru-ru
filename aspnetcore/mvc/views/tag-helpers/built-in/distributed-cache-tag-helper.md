---
title: Вспомогательная функция тега распределенного кэша в ASP.NET Core
author: pkellner
description: Сведения об использовании вспомогательной функции для тэга распределенного кэша.
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: a5b33451a763c297c6d7885855a321c43435abb4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043921"
---
# <a name="distributed-cache-tag-helper-in-aspnet-core"></a><span data-ttu-id="b39f6-103">Вспомогательная функция тега распределенного кэша в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b39f6-103">Distributed Cache Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="b39f6-104">Авторы: [Питер Кельнер (Peter Kellner)](http://peterkellner.net) и [Люк Лэтэм (Luke Latham)](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="b39f6-104">By [Peter Kellner](http://peterkellner.net) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b39f6-105">Вспомогательная функция тега распределенного кэша позволяет существенно повысить производительность приложения ASP.NET Core за счет кэширования его содержимого в источник распределенного кэша.</span><span class="sxs-lookup"><span data-stu-id="b39f6-105">The Distributed Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to a distributed cache source.</span></span>

<span data-ttu-id="b39f6-106">Общие сведения о вспомогательных функциях тегов см. здесь: <xref:mvc/views/tag-helpers/intro>.</span><span class="sxs-lookup"><span data-stu-id="b39f6-106">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

<span data-ttu-id="b39f6-107">Вспомогательная функция тега распределенного кэша наследуется от того же базового класса, что и вспомогательная функция тега кэша.</span><span class="sxs-lookup"><span data-stu-id="b39f6-107">The Distributed Cache Tag Helper inherits from the same base class as the Cache Tag Helper.</span></span> <span data-ttu-id="b39f6-108">Все атрибуты [вспомогательной функции тега кэша](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper) доступны вспомогательной функции тега распределенного кэша.</span><span class="sxs-lookup"><span data-stu-id="b39f6-108">All of the [Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper) attributes are available to the Distributed Tag Helper.</span></span>

<span data-ttu-id="b39f6-109">Вспомогательная функция тега распределенного кэша использует [внедрение через конструктор](xref:fundamentals/dependency-injection#constructor-injection-behavior).</span><span class="sxs-lookup"><span data-stu-id="b39f6-109">The Distributed Cache Tag Helper uses [constructor injection](xref:fundamentals/dependency-injection#constructor-injection-behavior).</span></span> <span data-ttu-id="b39f6-110">Интерфейс <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> передается в конструктор вспомогательной функции тега распределенного кэша.</span><span class="sxs-lookup"><span data-stu-id="b39f6-110">The <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface is passed into the Distributed Cache Tag Helper's constructor.</span></span> <span data-ttu-id="b39f6-111">Если конкретная реализация `IDistributedCache` не создается в `Startup.ConfigureServices` (*Startup.cs*), вспомогательная функция тега распределенного кэша использует тот же поставщик в памяти для хранения кэшированных данных, что и [вспомогательная функция тега кэша](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="b39f6-111">If no concrete implementation of `IDistributedCache` is created in `Startup.ConfigureServices` (*Startup.cs*), the Distributed Cache Tag Helper uses the same in-memory provider for storing cached data as the [Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).</span></span>

## <a name="distributed-cache-tag-helper-attributes"></a><span data-ttu-id="b39f6-112">Атрибуты вспомогательной функции тега распределенного кэша</span><span class="sxs-lookup"><span data-stu-id="b39f6-112">Distributed Cache Tag Helper Attributes</span></span>

### <a name="attributes-shared-with-the-cache-tag-helper"></a><span data-ttu-id="b39f6-113">Атрибуты, используемые совместно с вспомогательной функцией тега кэша</span><span class="sxs-lookup"><span data-stu-id="b39f6-113">Attributes shared with the Cache Tag Helper</span></span>

* `enabled`
* `expires-on`
* `expires-after`
* `expires-sliding`
* `vary-by-header`
* `vary-by-query`
* `vary-by-route`
* `vary-by-cookie`
* `vary-by-user`
* `vary-by priority`

<span data-ttu-id="b39f6-114">Вспомогательная функция тега распределенного кэша наследует от того же класса, что и вспомогательная функция тега кэша.</span><span class="sxs-lookup"><span data-stu-id="b39f6-114">The Distributed Cache Tag Helper inherits from the same class as Cache Tag Helper.</span></span> <span data-ttu-id="b39f6-115">Описание этих атрибутов см. в разделе [Вспомогательная функция тега кэша](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="b39f6-115">For descriptions of these attributes, see the [Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).</span></span>

### <a name="name"></a><span data-ttu-id="b39f6-116">имя</span><span class="sxs-lookup"><span data-stu-id="b39f6-116">name</span></span>

| <span data-ttu-id="b39f6-117">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="b39f6-117">Attribute Type</span></span> | <span data-ttu-id="b39f6-118">Пример</span><span class="sxs-lookup"><span data-stu-id="b39f6-118">Example</span></span>                               |
| -------------- | ------------------------------------- |
| <span data-ttu-id="b39f6-119">String</span><span class="sxs-lookup"><span data-stu-id="b39f6-119">String</span></span>         | `my-distributed-cache-unique-key-101` |

<span data-ttu-id="b39f6-120">`name` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b39f6-120">`name` is required.</span></span> <span data-ttu-id="b39f6-121">Атрибут `name` используется в качестве ключа для каждого хранимого экземпляра кэша.</span><span class="sxs-lookup"><span data-stu-id="b39f6-121">The `name` attribute is used as a key for each stored cache instance.</span></span> <span data-ttu-id="b39f6-122">В отличие от вспомогательной функции тега кэша, которая присваивает ключ кэша каждому экземпляру на основе имени страницы Razor и расположения на странице Razor, ключ вспомогательной функции тега распределенного кэша основан только на атрибуте `name`.</span><span class="sxs-lookup"><span data-stu-id="b39f6-122">Unlike the Cache Tag Helper that assigns a cache key to each instance based on the Razor page name and location in the Razor page, the Distributed Cache Tag Helper only bases its key on the attribute `name`.</span></span>

<span data-ttu-id="b39f6-123">Пример</span><span class="sxs-lookup"><span data-stu-id="b39f6-123">Example:</span></span>

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a><span data-ttu-id="b39f6-124">Реализации IDistributedCache для вспомогательной функции тега распределенного кэша</span><span class="sxs-lookup"><span data-stu-id="b39f6-124">Distributed Cache Tag Helper IDistributedCache implementations</span></span>

<span data-ttu-id="b39f6-125">В ASP.NET Core есть две встроенные реализации интерфейса <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>.</span><span class="sxs-lookup"><span data-stu-id="b39f6-125">There are two implementations of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> built in to ASP.NET Core.</span></span> <span data-ttu-id="b39f6-126">Одна из них основана на SQL Server, а другая — на Redis.</span><span class="sxs-lookup"><span data-stu-id="b39f6-126">One is based on SQL Server, and the other is based on Redis.</span></span> <span data-ttu-id="b39f6-127">Сведения об этих реализациях можно найти по адресу <xref:performance/caching/distributed>.</span><span class="sxs-lookup"><span data-stu-id="b39f6-127">Details of these implementations can be found at <xref:performance/caching/distributed>.</span></span> <span data-ttu-id="b39f6-128">Обе реализации предусматривают задание экземпляра `IDistributedCache` в `Startup`.</span><span class="sxs-lookup"><span data-stu-id="b39f6-128">Both implementations involve setting an instance of `IDistributedCache` in `Startup`.</span></span>

<span data-ttu-id="b39f6-129">Атрибуты тегов, связанные с использованием определенной реализации `IDistributedCache`, отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="b39f6-129">There are no tag attributes specifically associated with using any specific implementation of `IDistributedCache`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b39f6-130">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b39f6-130">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
