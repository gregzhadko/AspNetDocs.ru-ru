---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[Инструкции] Элемент управления, кэширование страницы ASP.NET на основе пользовательских сведений | Документация Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показывает способ управления критерии для кэширования страницы ASP.NET на основе пользовательских сведений. Пример страницы создается и затем O...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: a9ed2baad3460441bc57d97bf74f6de5977db0c9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032231"
---
<a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="526d6-104">[Инструкции] Элемент управления, кэширование страницы ASP.NET на основе пользовательских сведений</span><span class="sxs-lookup"><span data-stu-id="526d6-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>
====================
<span data-ttu-id="526d6-105">по [Крис Пелз](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="526d6-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="526d6-106">В этом видео Крис Пелз показывает способ управления критерии для кэширования страницы ASP.NET на основе пользовательских сведений.</span><span class="sxs-lookup"><span data-stu-id="526d6-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="526d6-107">Пример страницы создается и используется директива OutputCache VaryByCustom атрибут, который содержит пользовательское значение.</span><span class="sxs-lookup"><span data-stu-id="526d6-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="526d6-108">Затем метод GetVaryCustomByString() переопределяется в модуль global.asax, который обеспечивает обработку настраиваемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="526d6-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="526d6-109">В этом методе возвращается строка, однозначно идентифицирующий кэшированная версия страницы.</span><span class="sxs-lookup"><span data-stu-id="526d6-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="526d6-110">Наконец здесь ведется дискуссия о том, как кэширования с помощью пользовательского значения можно использовать несколькими способами для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="526d6-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="526d6-111">&#9654;Просмотрите видео (12 минут)</span><span class="sxs-lookup"><span data-stu-id="526d6-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
