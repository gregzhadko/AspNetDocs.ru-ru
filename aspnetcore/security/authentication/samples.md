---
title: Примеры проверки подлинности для ASP.NET Core
author: rick-anderson
description: Ссылки на примеры проверки подлинности в ASP.NET Core репозитории.
ms.author: riande
ms.date: 01/31/2019
uid: security/authentication/samples
ms.openlocfilehash: 7b3c911d60ad4737ebd12ce6f7628ad624b11658
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059831"
---
# <a name="authentication-samples-for-aspnet-core"></a><span data-ttu-id="0801a-103">Примеры проверки подлинности для ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0801a-103">Authentication samples for ASP.NET Core</span></span>

<span data-ttu-id="0801a-104">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="0801a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0801a-105">[Репозитория ASP.NET Core](https://github.com/aspnet/AspNetCore) содержит следующие примеры проверки подлинности *AspNetCore/src/Security/samples* папку:</span><span class="sxs-lookup"><span data-stu-id="0801a-105">The [ASP.NET Core repository](https://github.com/aspnet/AspNetCore) contains the following authentication samples in the *AspNetCore/src/Security/samples* folder:</span></span>

* [<span data-ttu-id="0801a-106">Преобразование заявок</span><span class="sxs-lookup"><span data-stu-id="0801a-106">Claims transformation</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/ClaimsTransformation)
* [<span data-ttu-id="0801a-107">Файл cookie проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="0801a-107">Cookie authentication</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/Cookies)
* [<span data-ttu-id="0801a-108">Поставщик настраиваемой политики — IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="0801a-108">Custom policy provider - IAuthorizationPolicyProvider</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider)
* [<span data-ttu-id="0801a-109">Схемы динамической проверки подлинности и параметры</span><span class="sxs-lookup"><span data-stu-id="0801a-109">Dynamic authentication schemes and options</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/DynamicSchemes)
* [<span data-ttu-id="0801a-110">Внешние утверждений</span><span class="sxs-lookup"><span data-stu-id="0801a-110">External claims</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/Identity.ExternalClaims)
* [<span data-ttu-id="0801a-111">Выбор между файл cookie и другую схему проверки подлинности на основе запроса</span><span class="sxs-lookup"><span data-stu-id="0801a-111">Selecting between cookie and another authentication scheme based on the request</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/PathSchemeSelection)
* [<span data-ttu-id="0801a-112">Ограничивает доступ к статическим файлам</span><span class="sxs-lookup"><span data-stu-id="0801a-112">Restricts access to static files</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/StaticFilesAuth)

## <a name="run-the-samples"></a><span data-ttu-id="0801a-113">Выполнение примеров</span><span class="sxs-lookup"><span data-stu-id="0801a-113">Run the samples</span></span>

* <span data-ttu-id="0801a-114">Выберите [ветви](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="0801a-114">Select a [branch](https://github.com/aspnet/AspNetCore).</span></span> <span data-ttu-id="0801a-115">Например `release/2.2` </span><span class="sxs-lookup"><span data-stu-id="0801a-115">For example, `release/2.2`</span></span>
* <span data-ttu-id="0801a-116">Клонируйте или скачайте [репозитория ASP.NET Core](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="0801a-116">Clone or download the [ASP.NET Core repository](https://github.com/aspnet/AspNetCore).</span></span>
* <span data-ttu-id="0801a-117">Проверка установки [пакет SDK для .NET Core](https://www.microsoft.com/net/download/all) версию, которая соответствует клон репозитория ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0801a-117">Verify you have installed the [.NET Core SDK](https://www.microsoft.com/net/download/all) version matching the clone of the ASP.NET Core repository.</span></span>
* <span data-ttu-id="0801a-118">Перейдите к выборке в *AspNetCore/src/Security/samples* и запуск примера с `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="0801a-118">Navigate to a sample in *AspNetCore/src/Security/samples* and run the sample with `dotnet run`.</span></span>
