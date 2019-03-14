---
title: Прочие ASP.NET Core интерфейсы API защиты данных
author: rick-anderson
description: Дополнительные сведения об интерфейсе защиты данных ISecret для ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 114cdd6209970e46b827e403fbe79b95692d0242
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033161"
---
# <a name="miscellaneous-aspnet-core-data-protection-apis"></a><span data-ttu-id="bfe10-103">Прочие ASP.NET Core интерфейсы API защиты данных</span><span class="sxs-lookup"><span data-stu-id="bfe10-103">Miscellaneous ASP.NET Core Data Protection APIs</span></span>

<a name="data-protection-extensibility-mics-apis"></a>

>[!WARNING]
> <span data-ttu-id="bfe10-104">Типы, реализующие любые из следующих интерфейсов должны быть потокобезопасными для нескольких клиентов.</span><span class="sxs-lookup"><span data-stu-id="bfe10-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="isecret"></a><span data-ttu-id="bfe10-105">ISecret</span><span class="sxs-lookup"><span data-stu-id="bfe10-105">ISecret</span></span>

<span data-ttu-id="bfe10-106">`ISecret` Интерфейс представляет значение секрета, например материал криптографического ключа.</span><span class="sxs-lookup"><span data-stu-id="bfe10-106">The `ISecret` interface represents a secret value, such as cryptographic key material.</span></span> <span data-ttu-id="bfe10-107">Он содержит следующие поверхность API:</span><span class="sxs-lookup"><span data-stu-id="bfe10-107">It contains the following API surface:</span></span>

* <span data-ttu-id="bfe10-108">`Length`: `int`</span><span class="sxs-lookup"><span data-stu-id="bfe10-108">`Length`: `int`</span></span>

* <span data-ttu-id="bfe10-109">`Dispose()`: `void`</span><span class="sxs-lookup"><span data-stu-id="bfe10-109">`Dispose()`: `void`</span></span>

* <span data-ttu-id="bfe10-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span><span class="sxs-lookup"><span data-stu-id="bfe10-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span></span>

<span data-ttu-id="bfe10-111">`WriteSecretIntoBuffer` Метод заполняет предоставленный буфер с необработанное значение секрета.</span><span class="sxs-lookup"><span data-stu-id="bfe10-111">The `WriteSecretIntoBuffer` method populates the supplied buffer with the raw secret value.</span></span> <span data-ttu-id="bfe10-112">Причина этого API принимает буфера в качестве параметра вместо возврата `byte[]` напрямую — это том, что это даёт вызывающий объект для закрепления объекта буфера, ограничивая секретный раскрытия в управляемых сборщика мусора.</span><span class="sxs-lookup"><span data-stu-id="bfe10-112">The reason this API takes the buffer as a parameter rather than returning a `byte[]` directly is that this gives the caller the opportunity to pin the buffer object, limiting secret exposure to the managed garbage collector.</span></span>

<span data-ttu-id="bfe10-113">`Secret` Тип — это конкретная реализация `ISecret` где секретное значение хранится в памяти в процессе.</span><span class="sxs-lookup"><span data-stu-id="bfe10-113">The `Secret` type is a concrete implementation of `ISecret` where the secret value is stored in in-process memory.</span></span> <span data-ttu-id="bfe10-114">На платформах Windows, секретное значение шифруется с помощью [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="bfe10-114">On Windows platforms, the secret value is encrypted via [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span></span>
