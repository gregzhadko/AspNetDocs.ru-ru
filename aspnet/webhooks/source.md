---
uid: webhooks/source
title: Исходный код ASP.NET веб-перехватчики и пакетов NuGet | Документация Майкрософт
author: rick-anderson
description: Ссылки на исходный код ASP.NET веб-перехватчики и пакеты NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ff716b476f7dc69b6071d3febd5b5871e4f02689
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027191"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="1637f-103">Исходный код ASP.NET веб-перехватчики и пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="1637f-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="1637f-104">Веб-перехватчики Microsoft ASP.NET является частью семейства Microsoft ASP.NET, модулей и размещен как управляющий [открытым проектом источник на GitHub](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="1637f-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="1637f-105">Это означает, что мы принимаем работы, но см. в [рекомендациями по участию](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) перед отправкой запроса на включение внесенных изменений.</span><span class="sxs-lookup"><span data-stu-id="1637f-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="1637f-106">Теперь этот электронной документации, который вы читаете также размещен как управляющий [открытым исходным кодом на GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) , а также принимает вклад.</span><span class="sxs-lookup"><span data-stu-id="1637f-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="1637f-107">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="1637f-107">NuGet packages</span></span>

<span data-ttu-id="1637f-108">[Пакеты NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) можно разделить на три части:</span><span class="sxs-lookup"><span data-stu-id="1637f-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="1637f-109">[Распространенные](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Распространенные пакет, который разделяется между отправителями и получателями.</span><span class="sxs-lookup"><span data-stu-id="1637f-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="1637f-110">[Отправитель](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Набор пакетов, поддержкой собственных веб-перехватчики пересылки другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="1637f-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="1637f-111">Функциональные возможности для отправки веб-перехватчики описан более подробно в [отправки веб-перехватчики](sending/index.md).</span><span class="sxs-lookup"><span data-stu-id="1637f-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/index.md).</span></span>

* <span data-ttu-id="1637f-112">[Приемники](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Набор пакетов, поддерживающих получение веб-перехватчики от других.</span><span class="sxs-lookup"><span data-stu-id="1637f-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="1637f-113">Функциональность для получения веб-перехватчики описан более подробно в [получения веб-перехватчики](receiving/index.md).</span><span class="sxs-lookup"><span data-stu-id="1637f-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
