---
uid: webhooks/source
title: ASP.NET исходный код WebHooks и пакеты NuGet Документы Майкрософт
author: rick-anderson
description: Ссылки на исходный код ASP.NET WebHooks и пакеты NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675326"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="92ac6-103">ASP.NET исходный код WebHooks и пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="92ac6-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="92ac6-104">Microsoft ASP.NET WebHooks является частью семейства модулей Microsoft ASP.NET и размещается в качестве [проекта с открытым исходным кодом на GitHub](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="92ac6-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="92ac6-105">Это означает, что мы принимаем взносы, но, пожалуйста, посмотрите на [Рекомендации](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) по вкладу, прежде чем подавать запрос на вытягивание.</span><span class="sxs-lookup"><span data-stu-id="92ac6-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="92ac6-106">Эта онлайн-документация, которую вы читаете сейчас, также размещается как [Открытый исходный код на GitHub,](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) а также принимает взносы.</span><span class="sxs-lookup"><span data-stu-id="92ac6-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="92ac6-107">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="92ac6-107">NuGet packages</span></span>

<span data-ttu-id="92ac6-108">[Пакеты NuGet разделены](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) на три части:</span><span class="sxs-lookup"><span data-stu-id="92ac6-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="92ac6-109">[Общие](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Общий пакет, который совместно между отправителями и получателями.</span><span class="sxs-lookup"><span data-stu-id="92ac6-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="92ac6-110">[Отправитель](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Набор пакетов, поддерживающих отправку собственных WebHooks другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="92ac6-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="92ac6-111">Функциональность для отправки WebHooks описана более подробно в [Отправке WebHooks](sending/senders.md).</span><span class="sxs-lookup"><span data-stu-id="92ac6-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="92ac6-112">[Приемники](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Набор пакетов, поддерживающих получение WebHooks от других.</span><span class="sxs-lookup"><span data-stu-id="92ac6-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="92ac6-113">Функциональность для получения WebHooks описана более подробно в [Receiving WebHooks](receiving/index.md).</span><span class="sxs-lookup"><span data-stu-id="92ac6-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
