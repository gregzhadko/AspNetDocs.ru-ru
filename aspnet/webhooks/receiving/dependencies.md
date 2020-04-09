---
uid: webhooks/receiving/dependencies
title: ASP.NET зависимости приемника WebHooks (ru) Документы Майкрософт
author: rick-anderson
description: Зависимость от приемника и инъекция зависимостей в ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675199"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="a00db-103">ASP.NET зависимости приемника WebHooks</span><span class="sxs-lookup"><span data-stu-id="a00db-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="a00db-104">Microsoft ASP.NET WebHooks разработан с учетом впрыски зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a00db-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="a00db-105">Большинство зависимостей в системе можно заменить альтернативными реализациями с помощью двигателя впрыска зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a00db-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="a00db-106">См, в [см.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)</span><span class="sxs-lookup"><span data-stu-id="a00db-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="a00db-107">Если никакая зависимость не зарегистрирована, используется реализация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a00db-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="a00db-108">Смотрите [список](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) реализаций по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a00db-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
