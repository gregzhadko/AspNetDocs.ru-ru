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
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET зависимости приемника WebHooks

Microsoft ASP.NET WebHooks разработан с учетом впрыски зависимостей. Большинство зависимостей в системе можно заменить альтернативными реализациями с помощью двигателя впрыска зависимостей.

См, в [см.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) Если никакая зависимость не зарегистрирована, используется реализация по умолчанию. Смотрите [список](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) реализаций по умолчанию.
