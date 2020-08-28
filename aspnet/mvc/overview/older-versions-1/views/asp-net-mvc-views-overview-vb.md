---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: Общие сведения о представлениях MVC ASP.NET (VB) | Документация Майкрософт
author: StephenWalther
description: Что такое представление MVC ASP.NET и как оно отличается от HTML-страницы? В этом руководстве Стивен Вальтер знакомит вас с представлениями и демонстрирует, как можно выполнить t...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044671"
---
# <a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="47d84-104">Общие сведения о представлениях ASP.NET MVC (VB)</span><span class="sxs-lookup"><span data-stu-id="47d84-104">ASP.NET MVC Views Overview (VB)</span></span>

<span data-ttu-id="47d84-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="47d84-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="47d84-106">Что такое представление MVC ASP.NET и как оно отличается от HTML-страницы?</span><span class="sxs-lookup"><span data-stu-id="47d84-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="47d84-107">В этом руководстве Стивен Вальтер знакомит вас с представлениями и демонстрирует, как можно воспользоваться преимуществами представления данных и вспомогательных функций HTML в рамках представления.</span><span class="sxs-lookup"><span data-stu-id="47d84-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="47d84-108">Цель этого руководства — предоставить краткое введение в представления ASP.NET MVC, просмотр данных и вспомогательные методы HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="47d84-109">К концу этого руководства вы узнаете, как создавать новые представления, передавать данные из контроллера в представление и использовать вспомогательные методы HTML для создания содержимого в представлении.</span><span class="sxs-lookup"><span data-stu-id="47d84-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="47d84-110">Основные сведения о представлениях</span><span class="sxs-lookup"><span data-stu-id="47d84-110">Understanding Views</span></span>

<span data-ttu-id="47d84-111">В отличие от страниц ASP.NET или Active Server, ASP.NET MVC не содержит ничего, непосредственно соответствующего странице.</span><span class="sxs-lookup"><span data-stu-id="47d84-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="47d84-112">В приложении ASP.NET MVC отсутствует страница на диске, соответствующая пути URL-адреса, введенного в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="47d84-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="47d84-113">Самым близким к странице в приложении ASP.NET MVC является то, что оно называется *представлением*.</span><span class="sxs-lookup"><span data-stu-id="47d84-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="47d84-114">В приложении ASP.NET MVC входящие запросы браузера сопоставляются с действиями контроллера.</span><span class="sxs-lookup"><span data-stu-id="47d84-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="47d84-115">Действие контроллера может возвращать представление.</span><span class="sxs-lookup"><span data-stu-id="47d84-115">A controller action might return a view.</span></span> <span data-ttu-id="47d84-116">Однако действие контроллера может выполнять другие действия, например перенаправление на другое действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="47d84-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="47d84-117">В листинге 1 содержится простой контроллер с именем HomeController.</span><span class="sxs-lookup"><span data-stu-id="47d84-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="47d84-118">HomeController предоставляет два действия контроллера с именами index () и Details ().</span><span class="sxs-lookup"><span data-stu-id="47d84-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="47d84-119">**Листинг 1-HomeController. vb**</span><span class="sxs-lookup"><span data-stu-id="47d84-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="47d84-120">Вы можете вызвать первое действие, действие index (), введя следующий URL-адрес в адресную строку браузера:</span><span class="sxs-lookup"><span data-stu-id="47d84-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="47d84-121">/хоме/индекс</span><span class="sxs-lookup"><span data-stu-id="47d84-121">/Home/Index</span></span>

<span data-ttu-id="47d84-122">Вы можете вызвать второе действие, действие Details (), введя этот адрес в браузере:</span><span class="sxs-lookup"><span data-stu-id="47d84-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="47d84-123">/хоме/детаилс</span><span class="sxs-lookup"><span data-stu-id="47d84-123">/Home/Details</span></span>

<span data-ttu-id="47d84-124">Действие index () возвращает представление.</span><span class="sxs-lookup"><span data-stu-id="47d84-124">The Index() action returns a view.</span></span> <span data-ttu-id="47d84-125">Большинство создаваемых действий будут возвращать представления.</span><span class="sxs-lookup"><span data-stu-id="47d84-125">Most actions that you create will return views.</span></span> <span data-ttu-id="47d84-126">Однако действие может возвращать другие типы результатов действий.</span><span class="sxs-lookup"><span data-stu-id="47d84-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="47d84-127">Например, действие Details () возвращает Редиректтоактионресулт, который перенаправляет входящий запрос в действие index ().</span><span class="sxs-lookup"><span data-stu-id="47d84-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="47d84-128">Действие index () содержит следующую одну строку кода:</span><span class="sxs-lookup"><span data-stu-id="47d84-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="47d84-129">View ()</span><span class="sxs-lookup"><span data-stu-id="47d84-129">View()</span></span>

<span data-ttu-id="47d84-130">Эта строка кода возвращает представление, которое должно находиться по следующему пути на веб-сервере:</span><span class="sxs-lookup"><span data-stu-id="47d84-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="47d84-131">\виевс\хоме\индекс.аспкс</span><span class="sxs-lookup"><span data-stu-id="47d84-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="47d84-132">Путь к представлению выводится из имени контроллера и имени действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="47d84-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="47d84-133">При желании вы можете быть явными для представления.</span><span class="sxs-lookup"><span data-stu-id="47d84-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="47d84-134">Следующая строка кода возвращает представление с именем Fred:</span><span class="sxs-lookup"><span data-stu-id="47d84-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="47d84-135">Вид (Fred)</span><span class="sxs-lookup"><span data-stu-id="47d84-135">View( Fred )</span></span>

<span data-ttu-id="47d84-136">При выполнении этой строки кода представление возвращается по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="47d84-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="47d84-137">\виевс\хоме\фред.аспкс</span><span class="sxs-lookup"><span data-stu-id="47d84-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="47d84-138">Если вы планируете создавать модульные тесты для приложения ASP.NET MVC, рекомендуется явно указывать имена представлений.</span><span class="sxs-lookup"><span data-stu-id="47d84-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="47d84-139">Таким образом, можно создать модульный тест, чтобы убедиться, что ожидаемое представление было возвращено действием контроллера.</span><span class="sxs-lookup"><span data-stu-id="47d84-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="47d84-140">Добавление содержимого в представление</span><span class="sxs-lookup"><span data-stu-id="47d84-140">Adding Content to a View</span></span>

<span data-ttu-id="47d84-141">Представление — это стандартный HTML-документ (X), который может содержать скрипты.</span><span class="sxs-lookup"><span data-stu-id="47d84-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="47d84-142">Для добавления динамического содержимого в представление используются скрипты.</span><span class="sxs-lookup"><span data-stu-id="47d84-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="47d84-143">Например, представление в листинге 2 отображает текущую дату и время.</span><span class="sxs-lookup"><span data-stu-id="47d84-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="47d84-144">**Листинг 2. \Виевс\хоме\индекс.аспкс**</span><span class="sxs-lookup"><span data-stu-id="47d84-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="47d84-145">Обратите внимание, что текст страницы HTML в листинге 2 содержит следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="47d84-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="47d84-146">&lt;% Response. Write (DateTime. Now)%&gt;</span><span class="sxs-lookup"><span data-stu-id="47d84-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="47d84-147">&lt; &gt; Для обозначения начала и конца скрипта используются разделители скриптов% и%.</span><span class="sxs-lookup"><span data-stu-id="47d84-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="47d84-148">Этот сценарий написан на языке Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="47d84-148">This script is written in Visual basic.</span></span> <span data-ttu-id="47d84-149">Он отображает текущую дату и время, вызывая метод Response. Write () для отрисовки содержимого в браузере.</span><span class="sxs-lookup"><span data-stu-id="47d84-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="47d84-150">Разделители скриптов &lt; % и% &gt; могут использоваться для выполнения одной или нескольких инструкций.</span><span class="sxs-lookup"><span data-stu-id="47d84-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="47d84-151">Так как вы вызываете Response. Write () так часто, корпорация Майкрософт предоставляет вам ярлык для вызова метода Response. Write ().</span><span class="sxs-lookup"><span data-stu-id="47d84-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="47d84-152">Представление в листинге 3 использует разделители &lt; % = и% &gt; в качестве ярлыка для вызова Response. Write ().</span><span class="sxs-lookup"><span data-stu-id="47d84-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="47d84-153">**Листинг 3. Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="47d84-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="47d84-154">Для создания динамического содержимого в представлении можно использовать любой язык .NET.</span><span class="sxs-lookup"><span data-stu-id="47d84-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="47d84-155">Как правило, для записи контроллеров и представлений используется либо Visual Basic .NET, либо C#.</span><span class="sxs-lookup"><span data-stu-id="47d84-155">Normally, you'll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="47d84-156">Использование вспомогательных функций HTML для создания содержимого представления</span><span class="sxs-lookup"><span data-stu-id="47d84-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="47d84-157">Чтобы упростить добавление содержимого в представление, можно воспользоваться преимуществом, которое называется *вспомогательным модулем HTML*.</span><span class="sxs-lookup"><span data-stu-id="47d84-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="47d84-158">HTML-вспомогательный метод, как правило, является методом, который создает строку.</span><span class="sxs-lookup"><span data-stu-id="47d84-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="47d84-159">Вспомогательные элементы HTML можно использовать для создания стандартных HTML-элементов, таких как текстовые поля, ссылки, раскрывающиеся списки и списки.</span><span class="sxs-lookup"><span data-stu-id="47d84-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="47d84-160">Например, представление в листинге 4 использует преимущества трех вспомогательных функций HTML — Бегинформ (), TextBox () и Password () для создания формы входа (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="47d84-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="47d84-161">**Листинг 4 — \Виевс\хоме\логин.аспкс**</span><span class="sxs-lookup"><span data-stu-id="47d84-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

<span data-ttu-id="47d84-162">[![Диалоговое окно New Project (Новый проект)](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="47d84-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="47d84-163">**Рис. 01**. Стандартная форма входа ([щелкните, чтобы просмотреть изображение с полным размером](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="47d84-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="47d84-164">Все методы вспомогательных методов HTML вызываются в свойстве HTML представления.</span><span class="sxs-lookup"><span data-stu-id="47d84-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="47d84-165">Например, можно отобразить текстовое поле, вызвав метод HTML. TextBox ().</span><span class="sxs-lookup"><span data-stu-id="47d84-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="47d84-166">Обратите внимание, что при &lt; &gt; вызове вспомогательных методов HTML. TextBox () и HTML. Password () используются разделители скриптов% = и%.</span><span class="sxs-lookup"><span data-stu-id="47d84-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="47d84-167">Эти вспомогательные методы просто возвращают строку.</span><span class="sxs-lookup"><span data-stu-id="47d84-167">These helpers simply return a string.</span></span> <span data-ttu-id="47d84-168">Чтобы отобразить строку в браузере, необходимо вызвать метод Response. Write ().</span><span class="sxs-lookup"><span data-stu-id="47d84-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="47d84-169">Использование вспомогательных методов HTML является необязательным.</span><span class="sxs-lookup"><span data-stu-id="47d84-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="47d84-170">Они упрощают жизнь, уменьшая объем кода HTML и скрипта, который необходимо написать.</span><span class="sxs-lookup"><span data-stu-id="47d84-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="47d84-171">Представление в листинге 5 отображает ту же форму, что и представление в листинге 4 без использования вспомогательных функций HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="47d84-172">**Листинг 5. \Виевс\хоме\логин.аспкс**</span><span class="sxs-lookup"><span data-stu-id="47d84-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="47d84-173">Вы также можете создать собственные вспомогательные методы HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="47d84-174">Например, можно создать вспомогательный метод GridView (), который автоматически отображает набор записей базы данных в HTML-таблице.</span><span class="sxs-lookup"><span data-stu-id="47d84-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="47d84-175">В этом разделе рассматривается **Создание настраиваемых**вспомогательных функций HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="47d84-176">Использование представления данных для передачи данных в представление</span><span class="sxs-lookup"><span data-stu-id="47d84-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="47d84-177">Для передачи данных из контроллера в представление используются данные представления.</span><span class="sxs-lookup"><span data-stu-id="47d84-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="47d84-178">Представьте себе данные представления, например пакет, отправляемый по почте.</span><span class="sxs-lookup"><span data-stu-id="47d84-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="47d84-179">Все данные, передаваемые из контроллера в представление, должны отправляться с помощью этого пакета.</span><span class="sxs-lookup"><span data-stu-id="47d84-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="47d84-180">Например, контроллер в листинге 6 добавляет сообщение для просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="47d84-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="47d84-181">**Листинг 6-Продуктконтроллер. vb**</span><span class="sxs-lookup"><span data-stu-id="47d84-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="47d84-182">Свойство ViewData контроллера представляет коллекцию пар имен и значений.</span><span class="sxs-lookup"><span data-stu-id="47d84-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="47d84-183">В листинге 6 метод Index () добавляет элемент в коллекцию данных View с именем Message со значением Hello World!.</span><span class="sxs-lookup"><span data-stu-id="47d84-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="47d84-184">Когда представление возвращается методом index (), данные представления передаются в представление автоматически.</span><span class="sxs-lookup"><span data-stu-id="47d84-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="47d84-185">Представление в листинге 7 извлекает сообщение из данных представления и готовит его к просмотру в браузере.</span><span class="sxs-lookup"><span data-stu-id="47d84-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="47d84-186">**Листинг 7. \Виевс\продукт\индекс.аспкс**</span><span class="sxs-lookup"><span data-stu-id="47d84-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="47d84-187">Обратите внимание, что представление использует преимущества вспомогательного метода HTML HTML. Encoded () при подготовке сообщения.</span><span class="sxs-lookup"><span data-stu-id="47d84-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="47d84-188">Вспомогательный метод HTML HTML. Encoded () кодирует специальные символы, такие как &lt; и, &gt; в символы, которые могут быть зашифрованы для просмотра на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="47d84-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="47d84-189">При отрисовке содержимого, отправляемого пользователем на веб-сайт, необходимо кодировать содержимое, чтобы предотвратить атаки путем внедрения кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="47d84-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="47d84-190">(Поскольку мы создали сообщение в Продуктконтроллер, нам не нужно кодировать сообщение.</span><span class="sxs-lookup"><span data-stu-id="47d84-190">(Because we created the message ourselves in the ProductController, we don't really need to encode the message.</span></span> <span data-ttu-id="47d84-191">Однако рекомендуется всегда вызывать метод HTML. Encoded () при отображении содержимого, полученного из представления данных в представлении.)</span><span class="sxs-lookup"><span data-stu-id="47d84-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="47d84-192">В листинге 7 мы использовали преимущества представления данных для передачи простого строкового сообщения из контроллера в представление.</span><span class="sxs-lookup"><span data-stu-id="47d84-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="47d84-193">Можно также использовать представление данных для передачи других типов данных, таких как коллекция записей базы данных, из контроллера в представление.</span><span class="sxs-lookup"><span data-stu-id="47d84-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="47d84-194">Например, если нужно отобразить содержимое таблицы базы данных Products в представлении, то необходимо передать коллекцию записей базы данных в представлении данные.</span><span class="sxs-lookup"><span data-stu-id="47d84-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="47d84-195">Также имеется возможность передачи строго типизированных данных представления из контроллера в представление.</span><span class="sxs-lookup"><span data-stu-id="47d84-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="47d84-196">Этот раздел рассматривается в учебнике **понимание данных и представлений строго типизированного представления**.</span><span class="sxs-lookup"><span data-stu-id="47d84-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="47d84-197">Сводка</span><span class="sxs-lookup"><span data-stu-id="47d84-197">Summary</span></span>

<span data-ttu-id="47d84-198">В этом руководстве предоставлены краткие сведения о ASP.NET представлениях MVC, просмотре данных и вспомогательных элементах HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="47d84-199">В первом разделе вы узнали, как добавлять новые представления в проект.</span><span class="sxs-lookup"><span data-stu-id="47d84-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="47d84-200">Вы узнали, что необходимо добавить представление в правую папку, чтобы вызвать его из определенного контроллера.</span><span class="sxs-lookup"><span data-stu-id="47d84-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="47d84-201">Далее обсуждалась тема вспомогательных функций HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="47d84-202">Вы узнали, как вспомогательные методы HTML позволяют легко создавать стандартное содержимое HTML.</span><span class="sxs-lookup"><span data-stu-id="47d84-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="47d84-203">Наконец, вы узнали, как использовать преимущества представления данных для передачи данных из контроллера в представление.</span><span class="sxs-lookup"><span data-stu-id="47d84-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="47d84-204">[Назад](passing-data-to-view-master-pages-cs.md)
> [Вперед](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="47d84-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>
