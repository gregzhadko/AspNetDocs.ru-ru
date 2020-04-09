---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Создание пользовательских HTML-помощников (СЗ) Документы Майкрософт
author: microsoft
description: Цель этого учебника состоит в том, чтобы продемонстрировать, как вы можете создавать пользовательские HTML Helpers, которые можно использовать в своих представлениях MVC. Воспользовавшись HTML Helper...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675329"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="cd9f8-104">Создание настраиваемых вспомогательных методов HTML (C#)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="cd9f8-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="cd9f8-106">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="cd9f8-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="cd9f8-107">Цель этого учебника состоит в том, чтобы продемонстрировать, как вы можете создавать пользовательские HTML Helpers, которые можно использовать в своих представлениях MVC.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="cd9f8-108">Воспользовавшись HTML Helpers, вы можете уменьшить количество утомительного ввода HTML-тегов, которые необходимо выполнить для создания стандартной страницы HTML.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="cd9f8-109">Цель этого учебника состоит в том, чтобы продемонстрировать, как вы можете создавать пользовательские HTML Helpers, которые можно использовать в своих представлениях MVC.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="cd9f8-110">Воспользовавшись HTML Helpers, вы можете уменьшить количество утомительного ввода HTML-тегов, которые необходимо выполнить для создания стандартной страницы HTML.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="cd9f8-111">В первой части этого урока я описываю некоторые из существующих HTML Помощников, включенных в ASP.NET платформу MVC.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="cd9f8-112">Далее я описываю два способа создания пользовательских HTML Helpers: я объясняю, как создавать пользовательские HTML Helpers, создавая статический метод и создавая метод расширения.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="cd9f8-113">Понимание HTML Помощники</span><span class="sxs-lookup"><span data-stu-id="cd9f8-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="cd9f8-114">HTML Helper — это всего лишь метод, который возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="cd9f8-115">Строка может представлять любой тип содержимого, который вы хотите.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="cd9f8-116">Например, можно использовать HTML Helpers для визуализации `<input>` `<img>` стандартных HTML-тегов, таких как HTML и теги.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="cd9f8-117">Вы также можете использовать HTML Helpers для визуализации более сложного содержимого, такого как полоса вкладок или HTML-таблица данных базы данных.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="cd9f8-118">Платформа ASP.NET MVC включает в себя следующий набор стандартных HTML Помощников (это не полный список):</span><span class="sxs-lookup"><span data-stu-id="cd9f8-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="cd9f8-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-119">Html.ActionLink()</span></span>
- <span data-ttu-id="cd9f8-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-120">Html.BeginForm()</span></span>
- <span data-ttu-id="cd9f8-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-121">Html.CheckBox()</span></span>
- <span data-ttu-id="cd9f8-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-122">Html.DropDownList()</span></span>
- <span data-ttu-id="cd9f8-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-123">Html.EndForm()</span></span>
- <span data-ttu-id="cd9f8-124">Html.Скрытые()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-124">Html.Hidden()</span></span>
- <span data-ttu-id="cd9f8-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-125">Html.ListBox()</span></span>
- <span data-ttu-id="cd9f8-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-126">Html.Password()</span></span>
- <span data-ttu-id="cd9f8-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-127">Html.RadioButton()</span></span>
- <span data-ttu-id="cd9f8-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-128">Html.TextArea()</span></span>
- <span data-ttu-id="cd9f8-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="cd9f8-129">Html.TextBox()</span></span>

<span data-ttu-id="cd9f8-130">Например, рассмотрим форму в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="cd9f8-131">Эта форма отображается с помощью двух стандартных HTML Помощников (см. рисунок 1).</span><span class="sxs-lookup"><span data-stu-id="cd9f8-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="cd9f8-132">Эта форма `Html.BeginForm()` использует `Html.TextBox()` методы helper для визуализации простой html-формы.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="cd9f8-133">[![Страница, отрисована с помощью HTML-помощников](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="cd9f8-134">**Рисунок 01**: Страница, отрисована с помощью HTML Помощников[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-custom-html-helpers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="cd9f8-135">**Список 1 -`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="cd9f8-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="cd9f8-136">Метод Html.BeginForm() Метод помощника используется для создания `<form>` открывающих и закрывающихся HTML-тегов.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="cd9f8-137">Обратите внимание, что `Html.BeginForm()` метод вызывается в использовании оператора.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="cd9f8-138">Использование оператора гарантирует, `<form>` что тег закрывается в конце блока использования.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="cd9f8-139">Если вы предпочитаете, вместо создания блока использования, вы можете вызвать html.EndForm() Метод помощника, чтобы закрыть `<form>` тег.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="cd9f8-140">Используйте какой бы подход `<form>` к созданию тега открытия и закрытия, который кажется вам наиболее интуитивным.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="cd9f8-141">Методы `Html.TextBox()` Helper используются в листинге `<input>` 1 для визуализации HTML-тегов.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="cd9f8-142">Если вы выберете источник просмотра в браузере, то вы увидите источник HTML в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="cd9f8-143">Обратите внимание, что источник содержит стандартные HTML-теги.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd9f8-144">обратите внимание, что `Html.TextBox()`помощник -HTML `<%= %>` отображается `<% %>` с тегами вместо тегов.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="cd9f8-145">Если вы не включаете равный знак, то ничего не отображается в браузере.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="cd9f8-146">Платформа mVC ASP.NET содержит небольшой набор помощников.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="cd9f8-147">Скорее всего, вам нужно будет расширить платформу MVC с пользовательскими HTML Helpers.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="cd9f8-148">В оставшейся части этого урока вы узнаете два метода создания пользовательских HTML Помощников.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="cd9f8-149">**Список 2 -`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="cd9f8-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="cd9f8-150">Создание HTML-помощников с помощью статических методов</span><span class="sxs-lookup"><span data-stu-id="cd9f8-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="cd9f8-151">Самый простой способ создать новый HTML Helper — создать статический метод, который возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="cd9f8-152">Представьте, например, что вы решили создать новый HTML `<label>` Helper, который отображает HTML-тег.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="cd9f8-153">Вы можете использовать класс в листинге 2 для визуализации `<label>` .</span><span class="sxs-lookup"><span data-stu-id="cd9f8-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="cd9f8-154">**Список 2 -`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="cd9f8-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="cd9f8-155">В листинге 2 нет ничего особенного в классе.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="cd9f8-156">Метод `Label()` просто возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="cd9f8-157">В измененном представлении индекса в листинге 3 используется для визуализации `LabelHelper` HTML-тегов. `<label>`</span><span class="sxs-lookup"><span data-stu-id="cd9f8-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="cd9f8-158">Обратите внимание, что `<%@ imports %>` представление содержит `Application1.Helpers` директиву, которая импортирует пространство имен.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="cd9f8-159">**Список 2 -`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="cd9f8-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="cd9f8-160">Создание HTML-помощников с помощью методов расширения</span><span class="sxs-lookup"><span data-stu-id="cd9f8-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="cd9f8-161">Если вы хотите создать HTML Helpers, которые работают так же, как стандартные HTML Helpers, включенные в ASP.NET mVC, то вам нужно создать методы расширения.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="cd9f8-162">Методы расширения позволяют добавлять новые методы в существующий класс.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="cd9f8-163">При создании метода HTML Helper вы добавляете новые методы в класс HtmlHelper, представленный html-свойством представления.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="cd9f8-164">Класс в листинге 3 добавляет `HtmlHelper` метод `Label()`расширения к названному классу.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="cd9f8-165">Есть несколько вещей, которые вы должны заметить об этом классе.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="cd9f8-166">Во-первых, обратите внимание, что класс является статическим классом.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="cd9f8-167">Необходимо определить метод расширения со статическим классом.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="cd9f8-168">Во-вторых, обратите внимание, что первому параметру метода `Label()` предшествует ключевое слово. `this`</span><span class="sxs-lookup"><span data-stu-id="cd9f8-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="cd9f8-169">Первый параметр метода расширения указывает на класс, который расширяет сятвик.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="cd9f8-170">**Список 3 -`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="cd9f8-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="cd9f8-171">После создания метода расширения и успешного создания приложения метод расширения появляется в Visual Studio Intellisense, как и все другие методы класса (см. рисунок 2).</span><span class="sxs-lookup"><span data-stu-id="cd9f8-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="cd9f8-172">Разница лишь в том, что методы расширения появляются со специальным символом рядом с ними (иконка нисходящей стрелки).</span><span class="sxs-lookup"><span data-stu-id="cd9f8-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="cd9f8-173">[![Использование метода расширения Html.Label()](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="cd9f8-174">**Рисунок 02**: Использование метода расширения Html.Label()[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-custom-html-helpers-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="cd9f8-175">В измененном представлении индекса в листинге 4 используется метод `<label>` расширения Html.Label() для визуализации всех своих тегов.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="cd9f8-176">**Список 4 -`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="cd9f8-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="cd9f8-177">Сводка</span><span class="sxs-lookup"><span data-stu-id="cd9f8-177">Summary</span></span>

<span data-ttu-id="cd9f8-178">В этом уроке вы узнали два способа создания пользовательских HTML Помощники.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="cd9f8-179">Во-первых, вы узнали, как создать пользовательский `Label()` HTML Helper, создав статический метод, который возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="cd9f8-180">Далее вы узнали, `Label()` как создать пользовательский метод HTML `HtmlHelper` Helper, создав метод расширения в классе.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="cd9f8-181">В этом учебнике я сосредоточился на создании чрезвычайно простого метода HTML Helper.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="cd9f8-182">Поймите, что HTML Helper может быть настолько сложным, насколько вы хотите.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="cd9f8-183">Можно создавать HTML-помощники, которые визуализировать богатое содержимое, такое как представления деревьев, меню или таблицы данных базы данных.</span><span class="sxs-lookup"><span data-stu-id="cd9f8-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cd9f8-184">[Назад](asp-net-mvc-views-overview-cs.md)
> [Вперед](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="cd9f8-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
