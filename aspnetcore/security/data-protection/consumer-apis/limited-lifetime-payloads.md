---
title: Ограничение времени существования защищенных полезных данных в ASP.NET Core
author: rick-anderson
description: Узнайте, как ограничение времени существования защищенных полезных данных, с помощью API защиты данных ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/limited-lifetime-payloads
ms.openlocfilehash: 8dc3b856ec67477ec8ae777749c9bf3107eb4eda
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039591"
---
# <a name="limit-the-lifetime-of-protected-payloads-in-aspnet-core"></a><span data-ttu-id="0e436-103">Ограничение времени существования защищенных полезных данных в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0e436-103">Limit the lifetime of protected payloads in ASP.NET Core</span></span>

<span data-ttu-id="0e436-104">Существуют сценарии, где разработчик приложения хочет создать защищенных полезных данных, срок действия истекает через определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="0e436-104">There are scenarios where the application developer wants to create a protected payload that expires after a set period of time.</span></span> <span data-ttu-id="0e436-105">Например защищенных полезных данных может представлять маркер сброса пароля, который должен быть допустимы, только на один час.</span><span class="sxs-lookup"><span data-stu-id="0e436-105">For instance, the protected payload might represent a password reset token that should only be valid for one hour.</span></span> <span data-ttu-id="0e436-106">Определенно возможно для разработчика, может создавать свои собственные формат полезных данных, который содержит внедренные срок действия, и опытным разработчикам может потребоваться сделать в любом случае, но для большинства разработчиков управление этих сроков действия может увеличиваться утомительно.</span><span class="sxs-lookup"><span data-stu-id="0e436-106">It's certainly possible for the developer to create their own payload format that contains an embedded expiration date, and advanced developers may wish to do this anyway, but for the majority of developers managing these expirations can grow tedious.</span></span>

<span data-ttu-id="0e436-107">Чтобы облегчить эту задачу для аудитории разработчиков, пакет [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) содержит API для служебных программ для создания полезных данных, которые автоматически истекает после заданного периода времени.</span><span class="sxs-lookup"><span data-stu-id="0e436-107">To make this easier for our developer audience, the package [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) contains utility APIs for creating payloads that automatically expire after a set period of time.</span></span> <span data-ttu-id="0e436-108">Эти API-интерфейсы зависания за пределами класса `ITimeLimitedDataProtector` типа.</span><span class="sxs-lookup"><span data-stu-id="0e436-108">These APIs hang off of the `ITimeLimitedDataProtector` type.</span></span>

## <a name="api-usage"></a><span data-ttu-id="0e436-109">Использование API</span><span class="sxs-lookup"><span data-stu-id="0e436-109">API usage</span></span>

<span data-ttu-id="0e436-110">`ITimeLimitedDataProtector` Интерфейс является основной интерфейс для защиты и снятии с него защиты полезных данных с ограниченным сроком / автоматическим истечением срока действия.</span><span class="sxs-lookup"><span data-stu-id="0e436-110">The `ITimeLimitedDataProtector` interface is the core interface for protecting and unprotecting time-limited / self-expiring payloads.</span></span> <span data-ttu-id="0e436-111">Для создания экземпляра `ITimeLimitedDataProtector`, необходимо сначала экземпляр обычного [IDataProtector](xref:security/data-protection/consumer-apis/overview) создан с помощью определенной цели.</span><span class="sxs-lookup"><span data-stu-id="0e436-111">To create an instance of an `ITimeLimitedDataProtector`, you'll first need an instance of a regular [IDataProtector](xref:security/data-protection/consumer-apis/overview) constructed with a specific purpose.</span></span> <span data-ttu-id="0e436-112">Один раз `IDataProtector` экземпляр доступен, вызовите `IDataProtector.ToTimeLimitedDataProtector` метод расширения для получения предохранитель с возможностями истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="0e436-112">Once the `IDataProtector` instance is available, call the `IDataProtector.ToTimeLimitedDataProtector` extension method to get back a protector with built-in expiration capabilities.</span></span>

<span data-ttu-id="0e436-113">`ITimeLimitedDataProtector` предоставляет следующие методы поверхность и расширения API:</span><span class="sxs-lookup"><span data-stu-id="0e436-113">`ITimeLimitedDataProtector` exposes the following API surface and extension methods:</span></span>

* <span data-ttu-id="0e436-114">CreateProtector (строка назначения): ITimeLimitedDataProtector - этот API, сходного с существующим `IDataProtectionProvider.CreateProtector` тем, что он может использоваться для создания [цели цепочки](xref:security/data-protection/consumer-apis/purpose-strings) из предохранитель корневой с ограниченным сроком действия.</span><span class="sxs-lookup"><span data-stu-id="0e436-114">CreateProtector(string purpose) : ITimeLimitedDataProtector - This API is similar to the existing `IDataProtectionProvider.CreateProtector` in that it can be used to create [purpose chains](xref:security/data-protection/consumer-apis/purpose-strings) from a root time-limited protector.</span></span>

* <span data-ttu-id="0e436-115">Защита (byte [] открытого текста, срок действия DateTimeOffset): byte]</span><span class="sxs-lookup"><span data-stu-id="0e436-115">Protect(byte[] plaintext, DateTimeOffset expiration) : byte[]</span></span>

* <span data-ttu-id="0e436-116">Защита (открытого текста byte [], время существования TimeSpan): byte]</span><span class="sxs-lookup"><span data-stu-id="0e436-116">Protect(byte[] plaintext, TimeSpan lifetime) : byte[]</span></span>

* <span data-ttu-id="0e436-117">Защита (byte [] открытого текста): byte]</span><span class="sxs-lookup"><span data-stu-id="0e436-117">Protect(byte[] plaintext) : byte[]</span></span>

* <span data-ttu-id="0e436-118">Защита (текстовая строка, DateTimeOffset истечения срока действия): строка</span><span class="sxs-lookup"><span data-stu-id="0e436-118">Protect(string plaintext, DateTimeOffset expiration) : string</span></span>

* <span data-ttu-id="0e436-119">Защита (открытого текста строки, время существования TimeSpan): строка</span><span class="sxs-lookup"><span data-stu-id="0e436-119">Protect(string plaintext, TimeSpan lifetime) : string</span></span>

* <span data-ttu-id="0e436-120">Защита (текстовая строка): строка</span><span class="sxs-lookup"><span data-stu-id="0e436-120">Protect(string plaintext) : string</span></span>

<span data-ttu-id="0e436-121">Помимо основных `Protect` методы, которые принимают только открытого текста, существуют новые перегрузки, которые разрешается указывать дату окончания срока действия полезных данных.</span><span class="sxs-lookup"><span data-stu-id="0e436-121">In addition to the core `Protect` methods which take only the plaintext, there are new overloads which allow specifying the payload's expiration date.</span></span> <span data-ttu-id="0e436-122">Дату истечения срока действия может быть указан как абсолютная Дата (через `DateTimeOffset`) или как относительное время (из текущей системы времени через `TimeSpan`).</span><span class="sxs-lookup"><span data-stu-id="0e436-122">The expiration date can be specified as an absolute date (via a `DateTimeOffset`) or as a relative time (from the current system time, via a `TimeSpan`).</span></span> <span data-ttu-id="0e436-123">При вызове перегрузки, которая не принимает срок действия, полезных данных считается никогда не истекает.</span><span class="sxs-lookup"><span data-stu-id="0e436-123">If an overload which doesn't take an expiration is called, the payload is assumed never to expire.</span></span>

* <span data-ttu-id="0e436-124">Снять защиту (byte [] protectedData, out DateTimeOffset истечения срока действия): byte]</span><span class="sxs-lookup"><span data-stu-id="0e436-124">Unprotect(byte[] protectedData, out DateTimeOffset expiration) : byte[]</span></span>

* <span data-ttu-id="0e436-125">Снять защиту (protectedData byte []): byte]</span><span class="sxs-lookup"><span data-stu-id="0e436-125">Unprotect(byte[] protectedData) : byte[]</span></span>

* <span data-ttu-id="0e436-126">Снять защиту (out DateTimeOffset истечения срока действия, protectedData строка): строка</span><span class="sxs-lookup"><span data-stu-id="0e436-126">Unprotect(string protectedData, out DateTimeOffset expiration) : string</span></span>

* <span data-ttu-id="0e436-127">Снять защиту (строка protectedData): строка</span><span class="sxs-lookup"><span data-stu-id="0e436-127">Unprotect(string protectedData) : string</span></span>

<span data-ttu-id="0e436-128">`Unprotect` Методы возвращают исходные незащищенные данные.</span><span class="sxs-lookup"><span data-stu-id="0e436-128">The `Unprotect` methods return the original unprotected data.</span></span> <span data-ttu-id="0e436-129">Если полезные данные, пока еще не истек, абсолютный срок действия возвращается как Необязательный выходной параметр вместе с исходной незащищенные данные.</span><span class="sxs-lookup"><span data-stu-id="0e436-129">If the payload hasn't yet expired, the absolute expiration is returned as an optional out parameter along with the original unprotected data.</span></span> <span data-ttu-id="0e436-130">Если истек срок действия полезных данных всех перегруженных версий метода Unprotect вызовет CryptographicException.</span><span class="sxs-lookup"><span data-stu-id="0e436-130">If the payload is expired, all overloads of the Unprotect method will throw CryptographicException.</span></span>

>[!WARNING]
> <span data-ttu-id="0e436-131">Не рекомендуется использовать эти API-интерфейсы для защиты полезных данных, требующих долгосрочного или неопределенное сохраняемости.</span><span class="sxs-lookup"><span data-stu-id="0e436-131">It's not advised to use these APIs to protect payloads which require long-term or indefinite persistence.</span></span> <span data-ttu-id="0e436-132">«Я допускается для защищенных полезных данных будет невозможно восстановить после месяца?»</span><span class="sxs-lookup"><span data-stu-id="0e436-132">"Can I afford for the protected payloads to be permanently unrecoverable after a month?"</span></span> <span data-ttu-id="0e436-133">можно использовать в качестве хорошее проверенное правило; Если ответ не затем разработчики могут попробовать альтернативные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="0e436-133">can serve as a good rule of thumb; if the answer is no then developers should consider alternative APIs.</span></span>

<span data-ttu-id="0e436-134">Приведенный ниже пример использует [пути кода не DI](xref:security/data-protection/configuration/non-di-scenarios) для создания экземпляра система защиты данных.</span><span class="sxs-lookup"><span data-stu-id="0e436-134">The sample below uses the [non-DI code paths](xref:security/data-protection/configuration/non-di-scenarios) for instantiating the data protection system.</span></span> <span data-ttu-id="0e436-135">Для выполнения этого образца, убедитесь, что сначала добавили ссылку на пакет Microsoft.AspNetCore.DataProtection.Extensions.</span><span class="sxs-lookup"><span data-stu-id="0e436-135">To run this sample, ensure that you have first added a reference to the Microsoft.AspNetCore.DataProtection.Extensions package.</span></span>

[!code-csharp[](limited-lifetime-payloads/samples/limitedlifetimepayloads.cs)]