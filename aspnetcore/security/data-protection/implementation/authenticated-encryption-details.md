---
title: Сведения о шифрование с проверкой подлинности в ASP.NET Core
author: rick-anderson
description: Дополнительные сведения о реализации шифрования для защиты данных ASP.NET Core прошел проверку подлинности.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/authenticated-encryption-details
ms.openlocfilehash: ac650e5c32e7eacc4088225e63f56340f95e1913
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047721"
---
# <a name="authenticated-encryption-details-in-aspnet-core"></a><span data-ttu-id="b0bec-103">Сведения о шифрование с проверкой подлинности в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b0bec-103">Authenticated encryption details in ASP.NET Core</span></span>

<a name="data-protection-implementation-authenticated-encryption-details"></a>

<span data-ttu-id="b0bec-104">Вызовы IDataProtector.Protect являются операциями шифрование с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="b0bec-104">Calls to IDataProtector.Protect are authenticated encryption operations.</span></span> <span data-ttu-id="b0bec-105">Предоставляет метод защитить конфиденциальность и подлинность, и он привязывается к цепочке назначения, который был использован для получения данного конкретного экземпляра IDataProtector его корня IDataProtectionProvider.</span><span class="sxs-lookup"><span data-stu-id="b0bec-105">The Protect method offers both confidentiality and authenticity, and it's tied to the purpose chain that was used to derive this particular IDataProtector instance from its root IDataProtectionProvider.</span></span>

<span data-ttu-id="b0bec-106">IDataProtector.Protect принимает параметр byte [] открытого текста и создает byte [] защищенных полезных данных, формат которого будут описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="b0bec-106">IDataProtector.Protect takes a byte[] plaintext parameter and produces a byte[] protected payload, whose format is described below.</span></span> <span data-ttu-id="b0bec-107">(Имеется также перегрузку метода расширения, которая принимает строковый параметр открытого текста и возвращает строковые полезные данные защищенных.</span><span class="sxs-lookup"><span data-stu-id="b0bec-107">(There's also an extension method overload which takes a string plaintext parameter and returns a string protected payload.</span></span> <span data-ttu-id="b0bec-108">При использовании этого API формата защищенных полезных данных по-прежнему будут иметь ниже структуру, но он будет [кодировке base64url](https://tools.ietf.org/html/rfc4648#section-5).)</span><span class="sxs-lookup"><span data-stu-id="b0bec-108">If this API is used the protected payload format will still have the below structure, but it will be [base64url-encoded](https://tools.ietf.org/html/rfc4648#section-5).)</span></span>

## <a name="protected-payload-format"></a><span data-ttu-id="b0bec-109">Формат защищенных полезных данных</span><span class="sxs-lookup"><span data-stu-id="b0bec-109">Protected payload format</span></span>

<span data-ttu-id="b0bec-110">Формат защищенных полезных данных состоит из трех основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b0bec-110">The protected payload format consists of three primary components:</span></span>

* <span data-ttu-id="b0bec-111">32-разрядный magic заголовок, определяющий версию системы защиты данных.</span><span class="sxs-lookup"><span data-stu-id="b0bec-111">A 32-bit magic header that identifies the version of the data protection system.</span></span>

* <span data-ttu-id="b0bec-112">128-разрядный идентификатор ключа, который определяет ключ, используемый для защиты этого конкретного полезных данных.</span><span class="sxs-lookup"><span data-stu-id="b0bec-112">A 128-bit key id that identifies the key used to protect this particular payload.</span></span>

* <span data-ttu-id="b0bec-113">Остальная часть защищенных полезных данных является [относящиеся к шифратора, инкапсулированный этим ключом](xref:security/data-protection/implementation/subkeyderivation#data-protection-implementation-subkey-derivation).</span><span class="sxs-lookup"><span data-stu-id="b0bec-113">The remainder of the protected payload is [specific to the encryptor encapsulated by this key](xref:security/data-protection/implementation/subkeyderivation#data-protection-implementation-subkey-derivation).</span></span> <span data-ttu-id="b0bec-114">В следующем примере представляет ключ AES-256-CBC + шифратора HMACSHA256 и полезных данных дополнительно разделить следующим образом: \* 128-разрядный модификатор ключей.</span><span class="sxs-lookup"><span data-stu-id="b0bec-114">In the example below the key represents an AES-256-CBC + HMACSHA256 encryptor, and the payload is further subdivided as follows: \* A 128-bit key modifier.</span></span> <span data-ttu-id="b0bec-115">\* 128-разрядного вектора инициализации.</span><span class="sxs-lookup"><span data-stu-id="b0bec-115">\* A 128-bit initialization vector.</span></span> <span data-ttu-id="b0bec-116">\* 48 байт выходных данных AES-256-CBC.</span><span class="sxs-lookup"><span data-stu-id="b0bec-116">\* 48 bytes of AES-256-CBC output.</span></span> <span data-ttu-id="b0bec-117">\* С тегом проверки подлинности HMACSHA256.</span><span class="sxs-lookup"><span data-stu-id="b0bec-117">\* An HMACSHA256 authentication tag.</span></span>

<span data-ttu-id="b0bec-118">Пример защищенных полезных данных, показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b0bec-118">A sample protected payload is illustrated below.</span></span>

```
09 F0 C9 F0 80 9C 81 0C 19 66 19 40 95 36 53 F8
AA FF EE 57 57 2F 40 4C 3F 7F CC 9D CC D9 32 3E
84 17 99 16 EC BA 1F 4A A1 18 45 1F 2D 13 7A 28
79 6B 86 9C F8 B7 84 F9 26 31 FC B1 86 0A F1 56
61 CF 14 58 D3 51 6F CF 36 50 85 82 08 2D 3F 73
5F B0 AD 9E 1A B2 AE 13 57 90 C8 F5 7C 95 4E 6A
8A AA 06 EF 43 CA 19 62 84 7C 11 B2 C8 71 9D AA
52 19 2E 5B 4C 1E 54 F0 55 BE 88 92 12 C1 4B 5E
52 C9 74 A0
```

<span data-ttu-id="b0bec-119">Формат полезных данных выше первые 32 бита, или 4 байта, имеют с magic заголовок, определяющий версию (09 F0 C9 F0)</span><span class="sxs-lookup"><span data-stu-id="b0bec-119">From the payload format above the first 32 bits, or 4 bytes are the magic header identifying the version (09 F0 C9 F0)</span></span>

<span data-ttu-id="b0bec-120">Далее 128 бит, то есть 16 байт является идентификатор ключа (80 9C 81 0C 19 66 19 40 95 36 53 F8 AA FF EE 57)</span><span class="sxs-lookup"><span data-stu-id="b0bec-120">The next 128 bits, or 16 bytes is the key identifier (80 9C 81 0C 19 66 19 40 95 36 53 F8 AA FF EE 57)</span></span>

<span data-ttu-id="b0bec-121">Остаток содержит полезные данные и относится только к формата.</span><span class="sxs-lookup"><span data-stu-id="b0bec-121">The remainder contains the payload and is specific to the format used.</span></span>

>[!WARNING]
> <span data-ttu-id="b0bec-122">Все полезные данные, защищенные для заданного ключа будет начинаться с один и тот же заголовок 20-байтный ("волшебное значение", идентификатор ключа).</span><span class="sxs-lookup"><span data-stu-id="b0bec-122">All payloads protected to a given key will begin with the same 20-byte (magic value, key id) header.</span></span> <span data-ttu-id="b0bec-123">Администраторы могут использовать этот факт для диагностики, для приближения при формировании полезных данных.</span><span class="sxs-lookup"><span data-stu-id="b0bec-123">Administrators can use this fact for diagnostic purposes to approximate when a payload was generated.</span></span> <span data-ttu-id="b0bec-124">Например указанных выше полезных данных соответствует ключу {0c819c80-6619-4019-9536-53f8aaffee57}.</span><span class="sxs-lookup"><span data-stu-id="b0bec-124">For example, the payload above corresponds to key {0c819c80-6619-4019-9536-53f8aaffee57}.</span></span> <span data-ttu-id="b0bec-125">Если после проверки хранилище ключей обнаружится, что Дата активации этого конкретного ключа был 2015-01-01 и датой истечения срока действия была 2015-03-01, а затем разумно предположить, что полезные данные (если не подделаны) был создан в рамках заданного периода, предоставляют, или воспользоваться небольшой настроечным с обеих сторон.</span><span class="sxs-lookup"><span data-stu-id="b0bec-125">If after checking the key repository you find that this specific key's activation date was 2015-01-01 and its expiration date was 2015-03-01, then it's reasonable to assume that the payload (if not tampered with) was generated within that window, give or take a small fudge factor on either side.</span></span>
