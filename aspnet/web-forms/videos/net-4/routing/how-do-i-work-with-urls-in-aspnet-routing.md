---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: 'Инструкции: Работать с URL-адресами в маршрутизации ASP.NET? | Документы Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показано, как указать URL-адреса для веб-сайта, использующего маршрутизации ASP.NET. Во-первых создается веб-сайта и маршрутизация определяется в ГК...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: eb1060fd9cc9469dc2b1d2e918823316c36840cb
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404823"
---
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a><span data-ttu-id="f5c80-105">Инструкции: Работать с URL-адресами в маршрутизации ASP.NET?</span><span class="sxs-lookup"><span data-stu-id="f5c80-105">How Do I: Work with URLs in ASP.NET Routing?</span></span>

<span data-ttu-id="f5c80-106">по [Крис Пелз](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f5c80-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f5c80-107">В этом видео Крис Пелз показано, как указать URL-адреса для веб-сайта, использующего маршрутизации ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f5c80-107">In this video Chris Pels shows how to specify URLs in a web site that utilizes ASP.NET routing.</span></span> <span data-ttu-id="f5c80-108">Во-первых создается веб-сайта и маршрутизация определяется в глобальный класс приложения (.asax).</span><span class="sxs-lookup"><span data-stu-id="f5c80-108">First, a web site is created and routing is defined in the Global Application Class (.asax).</span></span> <span data-ttu-id="f5c80-109">Затем создается пример веб-страницы и URL-адрес, на основе определенному маршруту добавляется на страницу, используя стандартный «жестко запрограммированный» подход, например, «~/Stats/Visitors».</span><span class="sxs-lookup"><span data-stu-id="f5c80-109">Next, a sample web page is created and a URL based upon a defined route is added to the page using the standard "hard coded" approach, e.g., "~/Stats/Visitors".</span></span> <span data-ttu-id="f5c80-110">Затем другую ссылку добавляется на страницу, который динамически создает же URL-адрес в разметке, с помощью метода RouteValue, который принимает имя маршрута и параметры.</span><span class="sxs-lookup"><span data-stu-id="f5c80-110">Another link is then added to the page which dynamically generates the same URL in markup using the RouteValue method which accepts the route name and parameters.</span></span> <span data-ttu-id="f5c80-111">Же URL-адрес затем реализуется с помощью кода, а не разметку непосредственно в страницу.</span><span class="sxs-lookup"><span data-stu-id="f5c80-111">The same URL is then implemented using code rather than markup directly in the page.</span></span> <span data-ttu-id="f5c80-112">Затем изменяются исходный маршрут и расположение физической страницы, в результате чего жестко запрограммированные ссылки больше не работает, тогда как оба динамически создаются работы ссылок должным образом.</span><span class="sxs-lookup"><span data-stu-id="f5c80-112">The original route and physical page location are then changed, resulting in the hard coded link no longer working whereas both dynamically generated links function properly.</span></span> <span data-ttu-id="f5c80-113">Наконец затем рассматривается значение динамически генерируемые ссылки обеспечивают доступ.</span><span class="sxs-lookup"><span data-stu-id="f5c80-113">Finally, the value of dynamically generated links is then discussed.</span></span>

[<span data-ttu-id="f5c80-114">&#9654;Просмотрите видео (20 минут)</span><span class="sxs-lookup"><span data-stu-id="f5c80-114">&#9654; Watch video (20 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [<span data-ttu-id="f5c80-115">Назад</span><span class="sxs-lookup"><span data-stu-id="f5c80-115">Previous</span></span>](how-do-i-use-routing-with-aspnet-web-forms.md)
