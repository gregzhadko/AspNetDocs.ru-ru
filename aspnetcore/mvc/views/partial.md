---
title: Частичные представления в ASP.NET Core
author: ardalis
description: Узнайте, как с помощью частичных представлений разбить большие файлы разметки на части и предотвратить дублирование стандартных блоков разметки на веб-страницах приложений ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 09/11/2018
uid: mvc/views/partial
ms.openlocfilehash: ff4b99580990edbd768128d77214e664a1e29e56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033301"
---
# <a name="partial-views-in-aspnet-core"></a><span data-ttu-id="7a92e-103">Частичные представления в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7a92e-103">Partial views in ASP.NET Core</span></span>

<span data-ttu-id="7a92e-104">Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith), [Люк Лэтэм](https://github.com/guardrex) (Luke Latham), [Махер Джендуби](https://twitter.com/maherjend) (Maher JENDOUBI), [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Скотт Собер](https://twitter.com/scottsauber) (Scott Sauber).</span><span class="sxs-lookup"><span data-stu-id="7a92e-104">By [Steve Smith](https://ardalis.com/), [Luke Latham](https://github.com/guardrex), [Maher JENDOUBI](https://twitter.com/maherjend), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Scott Sauber](https://twitter.com/scottsauber)</span></span>

<span data-ttu-id="7a92e-105">Частичное представление — это файл разметки [Razor](xref:mvc/views/razor) (*.cshtml*), отображающий выходные данные HTML *внутри* выходных данных другого файла разметки.</span><span class="sxs-lookup"><span data-stu-id="7a92e-105">A partial view is a [Razor](xref:mvc/views/razor) markup file (*.cshtml*) that renders HTML output *within* another markup file's rendered output.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7a92e-106">Термин *частичное представление* используется при разработке приложения MVC, в котором файлы разметки именуются *представлениями*, или приложения Razor Pages, в котором файлы разметки именуются *страницами*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-106">The term *partial view* is used when developing either an MVC app, where markup files are called *views*, or a Razor Pages app, where markup files are called *pages*.</span></span> <span data-ttu-id="7a92e-107">В этой статье все представления MVC и страницы Razor Pages будут называться *файлами разметки*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-107">This topic generically refers to MVC views and Razor Pages pages as *markup files*.</span></span>

::: moniker-end

<span data-ttu-id="7a92e-108">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="7a92e-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-partial-views"></a><span data-ttu-id="7a92e-109">Когда следует использовать частичные представления</span><span class="sxs-lookup"><span data-stu-id="7a92e-109">When to use partial views</span></span>

<span data-ttu-id="7a92e-110">Частичные представления позволяют эффективно выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="7a92e-110">Partial views are an effective way to:</span></span>

* <span data-ttu-id="7a92e-111">Разбить большие файлы разметки на мелкие компоненты.</span><span class="sxs-lookup"><span data-stu-id="7a92e-111">Break up large markup files into smaller components.</span></span>

  <span data-ttu-id="7a92e-112">Если используется крупный и сложный файл разметки, состоящий из нескольких логических частей, будет удобнее работать с этими частями как с отдельными частичными представлениями.</span><span class="sxs-lookup"><span data-stu-id="7a92e-112">In a large, complex markup file composed of several logical pieces, there's an advantage to working with each piece isolated into a partial view.</span></span> <span data-ttu-id="7a92e-113">Код в файле разметки сократится до разумного размера и будет содержать только общую структуру страницы и ссылки на частичные представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-113">The code in the markup file is manageable because the markup only contains the overall page structure and references to partial views.</span></span>
* <span data-ttu-id="7a92e-114">Сократить дублирование элементов разметки в разных файлах разметки.</span><span class="sxs-lookup"><span data-stu-id="7a92e-114">Reduce the duplication of common markup content across markup files.</span></span>

  <span data-ttu-id="7a92e-115">Если во многих файлах разметки используются одинаковые элементы, частичное представление переносит такое дублируемое содержимого в отдельный файл частичного представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-115">When the same markup elements are used across markup files, a partial view removes the duplication of markup content into one partial view file.</span></span> <span data-ttu-id="7a92e-116">Так, когда частичное представление изменится, автоматически обновятся выводимые данные для всех файлов разметки, использующих это частичное представление.</span><span class="sxs-lookup"><span data-stu-id="7a92e-116">When the markup is changed in the partial view, it updates the rendered output of the markup files that use the partial view.</span></span>

<span data-ttu-id="7a92e-117">Частичные представления не следует использовать для выделения стандартных элементов макета.</span><span class="sxs-lookup"><span data-stu-id="7a92e-117">Partial views shouldn't be used to maintain common layout elements.</span></span> <span data-ttu-id="7a92e-118">Повторяющиеся элементы макета следует определять в файле [_Layout.cshtml](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="7a92e-118">Common layout elements should be specified in [_Layout.cshtml](xref:mvc/views/layout) files.</span></span>

<span data-ttu-id="7a92e-119">Не используйте частичное представление там, где требуется сложная логика визуализации или выполнение кода для визуализации разметки.</span><span class="sxs-lookup"><span data-stu-id="7a92e-119">Don't use a partial view where complex rendering logic or code execution is required to render the markup.</span></span> <span data-ttu-id="7a92e-120">В этой ситуации лучше применить [компонент представления](xref:mvc/views/view-components).</span><span class="sxs-lookup"><span data-stu-id="7a92e-120">Instead of a partial view, use a [view component](xref:mvc/views/view-components).</span></span>

## <a name="declare-partial-views"></a><span data-ttu-id="7a92e-121">Объявление частичных представлений</span><span class="sxs-lookup"><span data-stu-id="7a92e-121">Declare partial views</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="7a92e-122">Частичное представление — это файл разметки *.cshtml*, размещенный в папке *Views* (в модели MVC) или *Pages* (в модели Razor Pages).</span><span class="sxs-lookup"><span data-stu-id="7a92e-122">A partial view is a *.cshtml* markup file maintained within the *Views* folder (MVC) or *Pages* folder (Razor Pages).</span></span>

<span data-ttu-id="7a92e-123">В модели ASP.NET Core MVC элемент контроллера <xref:Microsoft.AspNetCore.Mvc.ViewResult> может возвращать представление или частичное представление.</span><span class="sxs-lookup"><span data-stu-id="7a92e-123">In ASP.NET Core MVC, a controller's <xref:Microsoft.AspNetCore.Mvc.ViewResult> is capable of returning either a view or a partial view.</span></span> <span data-ttu-id="7a92e-124">Аналогичная возможность будет добавлена для Razor Pages в ASP.NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="7a92e-124">An analogous capability is planned for Razor Pages in ASP.NET Core 2.2.</span></span> <span data-ttu-id="7a92e-125">В Razor Pages <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> может возвращать <xref:Microsoft.AspNetCore.Mvc.PartialViewResult>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-125">In Razor Pages, a <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> can return a <xref:Microsoft.AspNetCore.Mvc.PartialViewResult>.</span></span> <span data-ttu-id="7a92e-126">См. дополнительные сведения о [создании ссылок на частичные представления и их отображении](#reference-a-partial-view).</span><span class="sxs-lookup"><span data-stu-id="7a92e-126">Referencing and rendering partial views is described in the [Reference a partial view](#reference-a-partial-view) section.</span></span>

<span data-ttu-id="7a92e-127">В отличие от представления MVC и отображения страниц, частичное представление не выполняет файл *_ViewStart.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-127">Unlike MVC view or page rendering, a partial view doesn't run *_ViewStart.cshtml*.</span></span> <span data-ttu-id="7a92e-128">Дополнительные сведения о файле *_ViewStart.cshtml*, см. здесь: <xref:mvc/views/layout>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-128">For more information on *_ViewStart.cshtml*, see <xref:mvc/views/layout>.</span></span>

<span data-ttu-id="7a92e-129">Имена файлов частичного представления обычно начинаются с символа подчеркивания (`_`).</span><span class="sxs-lookup"><span data-stu-id="7a92e-129">Partial view file names often begin with an underscore (`_`).</span></span> <span data-ttu-id="7a92e-130">Это соглашение об именовании не является обязательным требованием, но помогает отличать частичные представления от обычных представлений и страниц.</span><span class="sxs-lookup"><span data-stu-id="7a92e-130">This naming convention isn't required, but it helps to visually differentiate partial views from views and pages.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="7a92e-131">Частичное представление — это файл разметки *.cshtml*, размещенный в папке *Views*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-131">A partial view is a *.cshtml* markup file maintained within the *Views* folder.</span></span>

<span data-ttu-id="7a92e-132">Элемент контроллера <xref:Microsoft.AspNetCore.Mvc.ViewResult> может возвращать представление или частичное представление.</span><span class="sxs-lookup"><span data-stu-id="7a92e-132">A controller's <xref:Microsoft.AspNetCore.Mvc.ViewResult> is capable of returning either a view or a partial view.</span></span>

<span data-ttu-id="7a92e-133">В отличие от представления MVC, частичное представление не выполняет файл *_ViewStart.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-133">Unlike MVC view rendering, a partial view doesn't run *_ViewStart.cshtml*.</span></span> <span data-ttu-id="7a92e-134">Дополнительные сведения о файле *_ViewStart.cshtml*, см. здесь: <xref:mvc/views/layout>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-134">For more information on *_ViewStart.cshtml*, see <xref:mvc/views/layout>.</span></span>

<span data-ttu-id="7a92e-135">Имена файлов частичного представления обычно начинаются с символа подчеркивания (`_`).</span><span class="sxs-lookup"><span data-stu-id="7a92e-135">Partial view file names often begin with an underscore (`_`).</span></span> <span data-ttu-id="7a92e-136">Это соглашение об именовании не является обязательным требованием, но помогает отличать частичные представления от обычных представлений.</span><span class="sxs-lookup"><span data-stu-id="7a92e-136">This naming convention isn't required, but it helps to visually differentiate partial views from views.</span></span>

::: moniker-end

## <a name="reference-a-partial-view"></a><span data-ttu-id="7a92e-137">Ссылка на частичное представление</span><span class="sxs-lookup"><span data-stu-id="7a92e-137">Reference a partial view</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7a92e-138">В файле разметки частичное представление может указываться несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="7a92e-138">Within a markup file, there are several ways to reference a partial view.</span></span> <span data-ttu-id="7a92e-139">Мы рекомендуем использовать в приложениях один из следующих методов асинхронного отображения:</span><span class="sxs-lookup"><span data-stu-id="7a92e-139">We recommend that apps use one of the following asynchronous rendering approaches:</span></span>

* [<span data-ttu-id="7a92e-140">Вспомогательная функция тега частичного представления</span><span class="sxs-lookup"><span data-stu-id="7a92e-140">Partial Tag Helper</span></span>](#partial-tag-helper)
* [<span data-ttu-id="7a92e-141">Асинхронное вспомогательное приложение HTML</span><span class="sxs-lookup"><span data-stu-id="7a92e-141">Asynchronous HTML Helper</span></span>](#asynchronous-html-helper)

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="7a92e-142">В файле разметки частичное представление может указываться двумя способами.</span><span class="sxs-lookup"><span data-stu-id="7a92e-142">Within a markup file, there are two ways to reference a partial view:</span></span>

* [<span data-ttu-id="7a92e-143">Асинхронное вспомогательное приложение HTML</span><span class="sxs-lookup"><span data-stu-id="7a92e-143">Asynchronous HTML Helper</span></span>](#asynchronous-html-helper)
* [<span data-ttu-id="7a92e-144">Синхронное вспомогательное приложение HTML</span><span class="sxs-lookup"><span data-stu-id="7a92e-144">Synchronous HTML Helper</span></span>](#synchronous-html-helper)

<span data-ttu-id="7a92e-145">Мы рекомендуем использовать в приложениях [асинхронное вспомогательное приложение HTML](#asynchronous-html-helper).</span><span class="sxs-lookup"><span data-stu-id="7a92e-145">We recommend that apps use the [Asynchronous HTML Helper](#asynchronous-html-helper).</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a><span data-ttu-id="7a92e-146">Вспомогательная функция тега частичного представления</span><span class="sxs-lookup"><span data-stu-id="7a92e-146">Partial Tag Helper</span></span>

<span data-ttu-id="7a92e-147">Для [вспомогательной функции тега частичного представления](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper) требуется ASP.NET Core 2.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7a92e-147">The [Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper) requires ASP.NET Core 2.1 or later.</span></span>

<span data-ttu-id="7a92e-148">Вспомогательная функция тега частичного представления синхронно отображает содержимое, используя близкий к HTML синтаксис:</span><span class="sxs-lookup"><span data-stu-id="7a92e-148">The Partial Tag Helper renders content asynchronously and uses an HTML-like syntax:</span></span>

```cshtml
<partial name="_PartialName" />
```

<span data-ttu-id="7a92e-149">Если присутствует расширение файла, вспомогательная функция тега ссылается на частичное представление, которое необходимо разместить в той же папке, что и вызывающий его файл разметки:</span><span class="sxs-lookup"><span data-stu-id="7a92e-149">When a file extension is present, the Tag Helper references a partial view that must be in the same folder as the markup file calling the partial view:</span></span>

```cshtml
<partial name="_PartialName.cshtml" />
```

<span data-ttu-id="7a92e-150">В следующем примере есть ссылка на частичное представление из корня приложения.</span><span class="sxs-lookup"><span data-stu-id="7a92e-150">The following example references a partial view from the app root.</span></span> <span data-ttu-id="7a92e-151">Пути, начинающиеся с тильды и косой черты (`~/`) или с косой черты (`/`), используют корневой каталог приложения:</span><span class="sxs-lookup"><span data-stu-id="7a92e-151">Paths that start with a tilde-slash (`~/`) or a slash (`/`) refer to the app root:</span></span>

<span data-ttu-id="7a92e-152">**Razor Pages**</span><span class="sxs-lookup"><span data-stu-id="7a92e-152">**Razor Pages**</span></span>

```cshtml
<partial name="~/Pages/Folder/_PartialName.cshtml" />
<partial name="/Pages/Folder/_PartialName.cshtml" />
```

<span data-ttu-id="7a92e-153">**MVC**</span><span class="sxs-lookup"><span data-stu-id="7a92e-153">**MVC**</span></span>

```cshtml
<partial name="~/Views/Folder/_PartialName.cshtml" />
<partial name="/Views/Folder/_PartialName.cshtml" />
```

<span data-ttu-id="7a92e-154">В следующем примере есть ссылка на частичное представление с относительным путем.</span><span class="sxs-lookup"><span data-stu-id="7a92e-154">The following example references a partial view with a relative path:</span></span>

```cshtml
<partial name="../Account/_PartialName.cshtml" />
```

<span data-ttu-id="7a92e-155">Дополнительные сведения см. в разделе <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-155">For more information, see <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>.</span></span>

::: moniker-end

### <a name="asynchronous-html-helper"></a><span data-ttu-id="7a92e-156">Асинхронный вспомогательный метод HTML</span><span class="sxs-lookup"><span data-stu-id="7a92e-156">Asynchronous HTML Helper</span></span>

<span data-ttu-id="7a92e-157">Если вы используете вспомогательное приложение HTML, мы рекомендуем использовать <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-157">When using an HTML Helper, the best practice is to use <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*>.</span></span> <span data-ttu-id="7a92e-158">`PartialAsync` возвращает тип <xref:Microsoft.AspNetCore.Html.IHtmlContent> в оболочке <xref:System.Threading.Tasks.Task`1>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-158">`PartialAsync` returns an <xref:Microsoft.AspNetCore.Html.IHtmlContent> type wrapped in a <xref:System.Threading.Tasks.Task`1>.</span></span> <span data-ttu-id="7a92e-159">Для указания метода имя ожидающего вызова дополняется префиксом `@`.</span><span class="sxs-lookup"><span data-stu-id="7a92e-159">The method is referenced by prefixing the awaited call with an `@` character:</span></span>

```cshtml
@await Html.PartialAsync("_PartialName")
```

<span data-ttu-id="7a92e-160">Если присутствует расширение файла, вспомогательная функция HTML ссылается на частичное представление, которое необходимо разместить в той же папке, что и вызывающий его файл разметки:</span><span class="sxs-lookup"><span data-stu-id="7a92e-160">When the file extension is present, the HTML Helper references a partial view that must be in the same folder as the markup file calling the partial view:</span></span>

```cshtml
@await Html.PartialAsync("_PartialName.cshtml")
```

<span data-ttu-id="7a92e-161">В следующем примере есть ссылка на частичное представление из корня приложения.</span><span class="sxs-lookup"><span data-stu-id="7a92e-161">The following example references a partial view from the app root.</span></span> <span data-ttu-id="7a92e-162">Пути, начинающиеся с тильды и косой черты (`~/`) или с косой черты (`/`), используют корневой каталог приложения:</span><span class="sxs-lookup"><span data-stu-id="7a92e-162">Paths that start with a tilde-slash (`~/`) or a slash (`/`) refer to the app root:</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7a92e-163">**Razor Pages**</span><span class="sxs-lookup"><span data-stu-id="7a92e-163">**Razor Pages**</span></span>

```cshtml
@await Html.PartialAsync("~/Pages/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Pages/Folder/_PartialName.cshtml")
```

<span data-ttu-id="7a92e-164">**MVC**</span><span class="sxs-lookup"><span data-stu-id="7a92e-164">**MVC**</span></span>

::: moniker-end

```cshtml
@await Html.PartialAsync("~/Views/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Views/Folder/_PartialName.cshtml")
```

<span data-ttu-id="7a92e-165">В следующем примере есть ссылка на частичное представление с относительным путем.</span><span class="sxs-lookup"><span data-stu-id="7a92e-165">The following example references a partial view with a relative path:</span></span>

```cshtml
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

<span data-ttu-id="7a92e-166">Вы также можете выполнить преобразование для просмотра частичного представления с помощью <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-166">Alternatively, you can render a partial view with <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*>.</span></span> <span data-ttu-id="7a92e-167">Этот метод не возвращает <xref:Microsoft.AspNetCore.Html.IHtmlContent>.</span><span class="sxs-lookup"><span data-stu-id="7a92e-167">This method doesn't return an <xref:Microsoft.AspNetCore.Html.IHtmlContent>.</span></span> <span data-ttu-id="7a92e-168">Он передает выводимые данные непосредственно в ответ в потоковом режиме.</span><span class="sxs-lookup"><span data-stu-id="7a92e-168">It streams the rendered output directly to the response.</span></span> <span data-ttu-id="7a92e-169">Так как этот метод не возвращает результат, его необходимо вызывать в блоке кода Razor.</span><span class="sxs-lookup"><span data-stu-id="7a92e-169">Because the method doesn't return a result, it must be called within a Razor code block:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

<span data-ttu-id="7a92e-170">Так как `RenderPartialAsync` выполняет потоковую передачу отображаемого содержимого, его производительность в некоторых сценариях выше.</span><span class="sxs-lookup"><span data-stu-id="7a92e-170">Since `RenderPartialAsync` streams rendered content, it provides better performance in some scenarios.</span></span> <span data-ttu-id="7a92e-171">В системах критической важности следует замерить время отображения страницы при использовании двух подходов и использовать тот из них, который создает ответ быстрее.</span><span class="sxs-lookup"><span data-stu-id="7a92e-171">In performance-critical situations, benchmark the page using both approaches and use the approach that generates a faster response.</span></span>

### <a name="synchronous-html-helper"></a><span data-ttu-id="7a92e-172">Синхронный вспомогательный метод HTML</span><span class="sxs-lookup"><span data-stu-id="7a92e-172">Synchronous HTML Helper</span></span>

<span data-ttu-id="7a92e-173"><xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> и <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*> — это синхронные эквиваленты `PartialAsync` и `RenderPartialAsync` соответственно.</span><span class="sxs-lookup"><span data-stu-id="7a92e-173"><xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> and <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*> are the synchronous equivalents of `PartialAsync` and `RenderPartialAsync`, respectively.</span></span> <span data-ttu-id="7a92e-174">Мы не рекомендуем использовать синхронные эквиваленты, так как в некоторых случаях они приводят к взаимоблокировке.</span><span class="sxs-lookup"><span data-stu-id="7a92e-174">The synchronous equivalents aren't recommended because there are scenarios in which they deadlock.</span></span> <span data-ttu-id="7a92e-175">Синхронные методы будут удалены в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="7a92e-175">The synchronous methods are targeted for removal in a future release.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a92e-176">Если вам нужно выполнять код, используйте [компонент представления](xref:mvc/views/view-components) вместо частичного представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-176">If you need to execute code, use a [view component](xref:mvc/views/view-components) instead of a partial view.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7a92e-177">Вызов `Partial` или `RenderPartial` генерирует предупреждение анализатора Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a92e-177">Calling `Partial` or `RenderPartial` results in a Visual Studio analyzer warning.</span></span> <span data-ttu-id="7a92e-178">Например, наличие `Partial` приведет к появлению такого сообщения:</span><span class="sxs-lookup"><span data-stu-id="7a92e-178">For example, the presence of `Partial` yields the following warning message:</span></span>

> <span data-ttu-id="7a92e-179">Использование IHtmlHelper.Partial может привести к взаимоблокировкам приложения.</span><span class="sxs-lookup"><span data-stu-id="7a92e-179">Use of IHtmlHelper.Partial may result in application deadlocks.</span></span> <span data-ttu-id="7a92e-180">Попробуйте использовать &lt;частичное&gt; вспомогательное приложение тега или IHtmlHelper.PartialAsync.</span><span class="sxs-lookup"><span data-stu-id="7a92e-180">Consider using &lt;partial&gt; Tag Helper or IHtmlHelper.PartialAsync.</span></span>

<span data-ttu-id="7a92e-181">Вместо вызовов `@Html.Partial` используйте `@await Html.PartialAsync` или [вспомогательное приложение тега частичного представления](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="7a92e-181">Replace calls to `@Html.Partial` with `@await Html.PartialAsync` or the [Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper).</span></span> <span data-ttu-id="7a92e-182">Дополнительные сведения о переносе вспомогательной функции тега частичного представления см. в разделе [Перенос из вспомогательного метода HTML](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper).</span><span class="sxs-lookup"><span data-stu-id="7a92e-182">For more information on Partial Tag Helper migration, see [Migrate from an HTML Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper).</span></span>

::: moniker-end

## <a name="partial-view-discovery"></a><span data-ttu-id="7a92e-183">Обнаружение частичного представления</span><span class="sxs-lookup"><span data-stu-id="7a92e-183">Partial view discovery</span></span>

<span data-ttu-id="7a92e-184">Если ссылка на частичное представление указывает только имя файла, без расширения, просматриваются следующие расположения в указанном порядке:</span><span class="sxs-lookup"><span data-stu-id="7a92e-184">When a partial view is referenced by name without a file extension, the following locations are searched in the stated order:</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7a92e-185">**Razor Pages**</span><span class="sxs-lookup"><span data-stu-id="7a92e-185">**Razor Pages**</span></span>

1. <span data-ttu-id="7a92e-186">папка текущей выполняемой страницы;</span><span class="sxs-lookup"><span data-stu-id="7a92e-186">Currently executing page's folder</span></span>
1. <span data-ttu-id="7a92e-187">граф каталога на уровень выше папки страницы.</span><span class="sxs-lookup"><span data-stu-id="7a92e-187">Directory graph above the page's folder</span></span>
1. `/Shared`
1. `/Pages/Shared`
1. `/Views/Shared`

<span data-ttu-id="7a92e-188">**MVC**</span><span class="sxs-lookup"><span data-stu-id="7a92e-188">**MVC**</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`
1. `/Pages/Shared`

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`

::: moniker-end

<span data-ttu-id="7a92e-189">К обнаружению частичного представления применяются следующие соглашения:</span><span class="sxs-lookup"><span data-stu-id="7a92e-189">The following conventions apply to partial view discovery:</span></span>

* <span data-ttu-id="7a92e-190">допускается использовать разные частичные представления с одним именем файла, если они расположены в разных папках;</span><span class="sxs-lookup"><span data-stu-id="7a92e-190">Different partial views with the same file name are allowed when the partial views are in different folders.</span></span>
* <span data-ttu-id="7a92e-191">если ссылка на частичное представление содержит имя файла без расширения, а частичные представления с таким именем одновременно присутствуют в папке вызывающего объекта и в папке *Shared*, используется частичное представление из папки вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="7a92e-191">When referencing a partial view by name without a file extension and the partial view is present in both the caller's folder and the *Shared* folder, the partial view in the caller's folder supplies the partial view.</span></span> <span data-ttu-id="7a92e-192">Если нужное частичное представление отсутствует в папке вызывающего объекта, используется частичное представление из папки *Shared*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-192">If the partial view isn't present in the caller's folder, the partial view is provided from the *Shared* folder.</span></span> <span data-ttu-id="7a92e-193">Частичных представления в папке *Shared* именуются *общие частичные представления* или *частичные представления по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-193">Partial views in the *Shared* folder are called *shared partial views* or *default partial views*.</span></span>
* <span data-ttu-id="7a92e-194">Частичные представления можно вызывать *по цепочке*&mdash;одно частичное представление можно вызвать другое частичное представление, если при этом не создается циклических ссылок.</span><span class="sxs-lookup"><span data-stu-id="7a92e-194">Partial views can be *chained*&mdash;a partial view can call another partial view if a circular reference isn't formed by the calls.</span></span> <span data-ttu-id="7a92e-195">Относительные пути всегда указываются относительно расположения текущего файла, но не корневого или родительского каталога.</span><span class="sxs-lookup"><span data-stu-id="7a92e-195">Relative paths are always relative to the current file, not to the root or parent of the file.</span></span>

> [!NOTE]
> <span data-ttu-id="7a92e-196">Объект [Razor](xref:mvc/views/razor) `section`, определенный в частичном представлении, невидим для родительских файлов разметки.</span><span class="sxs-lookup"><span data-stu-id="7a92e-196">A [Razor](xref:mvc/views/razor) `section` defined in a partial view is invisible to parent markup files.</span></span> <span data-ttu-id="7a92e-197">Объект `section` видим только для частичного представления, в котором он определен.</span><span class="sxs-lookup"><span data-stu-id="7a92e-197">The `section` is only visible to the partial view in which it's defined.</span></span>

## <a name="access-data-from-partial-views"></a><span data-ttu-id="7a92e-198">Доступ к данным из частичных представлений</span><span class="sxs-lookup"><span data-stu-id="7a92e-198">Access data from partial views</span></span>

<span data-ttu-id="7a92e-199">Когда создается экземпляр частичного представления, он получает *копию* словаря `ViewData` из родительского представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-199">When a partial view is instantiated, it receives a *copy* of the parent's `ViewData` dictionary.</span></span> <span data-ttu-id="7a92e-200">Изменения, вносимые в данные в частичном представлении, не сохраняются в родительском представлении.</span><span class="sxs-lookup"><span data-stu-id="7a92e-200">Updates made to the data within the partial view aren't persisted to the parent view.</span></span> <span data-ttu-id="7a92e-201">Изменения объекта `ViewData` в частичном представлении утрачиваются при возврате этого представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-201">`ViewData` changes in a partial view are lost when the partial view returns.</span></span>

<span data-ttu-id="7a92e-202">В следующем примере показано, как передать экземпляр [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) в частичное представление:</span><span class="sxs-lookup"><span data-stu-id="7a92e-202">The following example demonstrates how to pass an instance of [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) to a partial view:</span></span>

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

<span data-ttu-id="7a92e-203">В частичное представление можно передать модель.</span><span class="sxs-lookup"><span data-stu-id="7a92e-203">You can pass a model into a partial view.</span></span> <span data-ttu-id="7a92e-204">Модель может являться пользовательским объектом.</span><span class="sxs-lookup"><span data-stu-id="7a92e-204">The model can be a custom object.</span></span> <span data-ttu-id="7a92e-205">Модель можно передать с помощью `PartialAsync` (передает блок содержимого вызывающему объекту) или `RenderPartialAsync` (выполняет потоковую передачу содержимого в выходные данные):</span><span class="sxs-lookup"><span data-stu-id="7a92e-205">You can pass a model with `PartialAsync` (renders a block of content to the caller) or `RenderPartialAsync` (streams the content to the output):</span></span>

```cshtml
@await Html.PartialAsync("_PartialName", model)
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7a92e-206">**Razor Pages**</span><span class="sxs-lookup"><span data-stu-id="7a92e-206">**Razor Pages**</span></span>

<span data-ttu-id="7a92e-207">Следующая разметка для примера приложения взята со страницы *Pages/ArticlesRP/ReadRP.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-207">The following markup in the sample app is from the *Pages/ArticlesRP/ReadRP.cshtml* page.</span></span> <span data-ttu-id="7a92e-208">Эта страница содержит два частичных представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-208">The page contains two partial views.</span></span> <span data-ttu-id="7a92e-209">Второе частичное представление передает модель и объект `ViewData` в первое частичное представление.</span><span class="sxs-lookup"><span data-stu-id="7a92e-209">The second partial view passes in a model and `ViewData` to the partial view.</span></span> <span data-ttu-id="7a92e-210">Используйте перегрузку конструктора `ViewDataDictionary`, чтобы передать новый словарь `ViewData` и при этом сохранить существующий словарь `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="7a92e-210">The `ViewDataDictionary` constructor overload is used to pass a new `ViewData` dictionary while retaining the existing `ViewData` dictionary.</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/ReadRP.cshtml?name=snippet_ReadPartialViewRP&highlight=5,15-19)]

<span data-ttu-id="7a92e-211">*Pages/Shared/_AuthorPartialRP.cshtml* — это первое частичное представление, указанное в файле разметки *ReadRP.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7a92e-211">*Pages/Shared/_AuthorPartialRP.cshtml* is the first partial view referenced by the *ReadRP.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/Shared/_AuthorPartialRP.cshtml)]

<span data-ttu-id="7a92e-212">*Pages/ArticlesRP/_ArticleSectionRP.cshtml* — это второе частичное представление, указанное в файле разметки *ReadRP.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7a92e-212">*Pages/ArticlesRP/_ArticleSectionRP.cshtml* is the second partial view referenced by the *ReadRP.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/_ArticleSectionRP.cshtml)]

<span data-ttu-id="7a92e-213">**MVC**</span><span class="sxs-lookup"><span data-stu-id="7a92e-213">**MVC**</span></span>

::: moniker-end

<span data-ttu-id="7a92e-214">В приведенной ниже разметке для примера приложения показано представление *Views/Articles/Read.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-214">The following markup in the sample app shows the *Views/Articles/Read.cshtml* view.</span></span> <span data-ttu-id="7a92e-215">Это представление содержит два частичных представления.</span><span class="sxs-lookup"><span data-stu-id="7a92e-215">The view contains two partial views.</span></span> <span data-ttu-id="7a92e-216">Второе частичное представление передает модель и объект `ViewData` в первое частичное представление.</span><span class="sxs-lookup"><span data-stu-id="7a92e-216">The second partial view passes in a model and `ViewData` to the partial view.</span></span> <span data-ttu-id="7a92e-217">Используйте перегрузку конструктора `ViewDataDictionary`, чтобы передать новый словарь `ViewData` и при этом сохранить существующий словарь `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="7a92e-217">The `ViewDataDictionary` constructor overload is used to pass a new `ViewData` dictionary while retaining the existing `ViewData` dictionary.</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=5,15-19)]

<span data-ttu-id="7a92e-218">*Views/Shared/_AuthorPartialRP.cshtml* — это первое частичное представление, указанное в файле разметки *Read.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7a92e-218">*Views/Shared/_AuthorPartial.cshtml* is the first partial view referenced by the *ReadRP.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

<span data-ttu-id="7a92e-219">*Views/Shared/_ArticleSection.cshtml* — это второе частичное представление, указанное в файле разметки *Read.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7a92e-219">*Views/Articles/_ArticleSection.cshtml* is the second partial view referenced by the *Read.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

<span data-ttu-id="7a92e-220">Во время выполнения частичные представления встраиваются в выходные данные родительского представления, которое также преобразовывается для просмотра в общем макете *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7a92e-220">At runtime, the partials are rendered into the parent markup file's rendered output, which itself is rendered within the shared *_Layout.cshtml*.</span></span> <span data-ttu-id="7a92e-221">Первое частичное представление отображает имя автора статьи и дату публикации:</span><span class="sxs-lookup"><span data-stu-id="7a92e-221">The first partial view renders the article author's name and publication date:</span></span>

> <span data-ttu-id="7a92e-222">Abraham Lincoln</span><span class="sxs-lookup"><span data-stu-id="7a92e-222">Abraham Lincoln</span></span>
>
> <span data-ttu-id="7a92e-223">Это частичное представление из &lt;общего каталога файлов частичного представления&gt;.</span><span class="sxs-lookup"><span data-stu-id="7a92e-223">This partial view from &lt;shared partial view file path&gt;.</span></span>
> <span data-ttu-id="7a92e-224">11/19/1863 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="7a92e-224">11/19/1863 12:00:00 AM</span></span>

<span data-ttu-id="7a92e-225">Второе частичное представление отображает разделы статьи:</span><span class="sxs-lookup"><span data-stu-id="7a92e-225">The second partial view renders the article's sections:</span></span>

> <span data-ttu-id="7a92e-226">Раздел один индекс: 0</span><span class="sxs-lookup"><span data-stu-id="7a92e-226">Section One Index: 0</span></span>
>
> <span data-ttu-id="7a92e-227">Four score and seven years ago...</span><span class="sxs-lookup"><span data-stu-id="7a92e-227">Four score and seven years ago ...</span></span>
>
> <span data-ttu-id="7a92e-228">Индекс раздела: 1</span><span class="sxs-lookup"><span data-stu-id="7a92e-228">Section Two Index: 1</span></span>
>
> <span data-ttu-id="7a92e-229">Now we are engaged in a great civil war, testing...</span><span class="sxs-lookup"><span data-stu-id="7a92e-229">Now we are engaged in a great civil war, testing ...</span></span>
>
> <span data-ttu-id="7a92e-230">Индекс в разделе 3: 2</span><span class="sxs-lookup"><span data-stu-id="7a92e-230">Section Three Index: 2</span></span>
>
> <span data-ttu-id="7a92e-231">But, in a larger sense, we can not dedicate...</span><span class="sxs-lookup"><span data-stu-id="7a92e-231">But, in a larger sense, we can not dedicate ...</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a92e-232">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a92e-232">Additional resources</span></span>

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end
