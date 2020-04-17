---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Объединение и минификация активов в веб-страницах ASP.NET (Razor) Документы Майкрософт
author: rick-anderson
description: Комплектация и минификация являются способами, чтобы сделать ваш сайт быстрее. Bundling позволяет комбинировать несколько JavaScript ( .js ) файлы или несколько каскадных стиль листа (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539930"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="24417-104">Объединение и минификация активов на сайте веб-страниц ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="24417-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="24417-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="24417-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="24417-106">Комплектация и минификация являются способами, чтобы сделать ваш сайт быстрее.</span><span class="sxs-lookup"><span data-stu-id="24417-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="24417-107">Bundling позволяет комбинировать несколько файлов JavaScript (*.js)* или несколько каскадных таблиц стилей (*.css*) файлы, так что они могут быть загружены как единое целое, а не по одному за один раз.</span><span class="sxs-lookup"><span data-stu-id="24417-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="24417-108">Minification выжимает пробел и выполняет другие типы сжатия, чтобы сделать загруженные файлы как можно меньше.</span><span class="sxs-lookup"><span data-stu-id="24417-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="24417-109">RC-релиз ASP.NET Web Pages 2 не поддерживает комплектацию и минификацию, поскольку пакет, содержащий необходимые элементы, еще не доступен в Microsoft WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="24417-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="24417-110">Приносим извинения за неудобства.</span><span class="sxs-lookup"><span data-stu-id="24417-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="24417-111">Ожидается, что пакет будет доступен в окончательном выпуске веб-страниц ASP.NET 2 и WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="24417-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
