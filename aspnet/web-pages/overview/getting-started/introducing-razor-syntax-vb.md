---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Введение в программирование веб-ASP.NET с использованием синтаксиса Razor (Visual Basic) | Документация Майкрософт
author: Rick-Anderson
description: В этом приложении предоставляет общие сведения о программировании с помощью веб-страниц ASP.NET в Visual Basic с использованием синтаксиса Razor.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: e6b63afb9492e810e19999c7c7ffe074ad510bda
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59406773"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="bcdca-103">Введение в программирование веб-ASP.NET с использованием синтаксиса Razor (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="bcdca-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="bcdca-104">по [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bcdca-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bcdca-105">В этой статье дает Общие сведения о программировании с помощью веб-страниц ASP.NET с использованием синтаксиса Razor и Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="bcdca-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="bcdca-106">ASP.NET — технология Майкрософт для выполнения динамических веб-страниц на веб-серверах.</span><span class="sxs-lookup"><span data-stu-id="bcdca-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="bcdca-107">**Вы узнаете, как**:</span><span class="sxs-lookup"><span data-stu-id="bcdca-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="bcdca-108">Top 8, программирование советов по началу работы с программирования веб-страниц ASP.NET с использованием синтаксиса Razor.</span><span class="sxs-lookup"><span data-stu-id="bcdca-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="bcdca-109">Основные концепции программирования вам.</span><span class="sxs-lookup"><span data-stu-id="bcdca-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="bcdca-110">Какой код сервера ASP.NET и синтаксиса Razor посвящен.</span><span class="sxs-lookup"><span data-stu-id="bcdca-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="bcdca-111">Версии программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="bcdca-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="bcdca-112">Веб-страниц ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="bcdca-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="bcdca-113">Этот учебник также работает с ASP.NET Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="bcdca-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="bcdca-114">Большинство примеров использования ASP.NET Web Pages с синтаксисом Razor используйте C#.</span><span class="sxs-lookup"><span data-stu-id="bcdca-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="bcdca-115">Но синтаксис Razor поддерживает Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="bcdca-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="bcdca-116">Для программирования веб-страницу ASP.NET в Visual Basic, создать веб-страницы с *.vbhtml* расширение имени файла, а затем добавьте код Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="bcdca-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="bcdca-117">Этой статье приводится обзор работы с языком Visual Basic и синтаксис для создания веб-страниц ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bcdca-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdca-118">Шаблоны веб-сайт по умолчанию Microsoft WebMatrix (**кондитерской**, **Photo Gallery**, и **начального сайта**т. д.) доступны в версиях C# и Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="bcdca-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="bcdca-119">Шаблоны Visual Basic, можно установить как пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="bcdca-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="bcdca-120">Шаблоны веб-сайта, устанавливаются в корневой папке веб-сайта в папку с именем *шаблоны Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="bcdca-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="bcdca-121">Top 8 советов по программированию</span><span class="sxs-lookup"><span data-stu-id="bcdca-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="bcdca-122">В этом разделе перечислены несколько советов, которые абсолютно необходимо знать, как приступить к созданию кода сервера ASP.NET с использованием синтаксиса Razor.</span><span class="sxs-lookup"><span data-stu-id="bcdca-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="bcdca-123">1. Добавьте код для страницы с помощью символа @</span><span class="sxs-lookup"><span data-stu-id="bcdca-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="bcdca-124">`@` Символ запускает встроенные выражения, одной инструкции блоков и блоков с несколькими инструкциями:</span><span class="sxs-lookup"><span data-stu-id="bcdca-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="bcdca-125">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-125">The result displayed in a browser:</span></span>

![Razor Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **<span data-ttu-id="bcdca-127">Кодировка HTML</span><span class="sxs-lookup"><span data-stu-id="bcdca-127">HTML Encoding</span></span>**
> 
> <span data-ttu-id="bcdca-128">При выводе содержимого на страницы с помощью `@` символов, как и в предыдущих примерах ASP.NET HTML кодирует выходные данные.</span><span class="sxs-lookup"><span data-stu-id="bcdca-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="bcdca-129">Этот параметр заменяет зарезервированные символы HTML (например, `<` и `>` и `&`) с кодами, которые позволяют символов для отображения в качестве символов на веб-странице, а как HTML-теги или сущности.</span><span class="sxs-lookup"><span data-stu-id="bcdca-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="bcdca-130">Без HTML-кодирования, выходные данные из кода сервера могут отображаться неправильно и может предоставить доступ к странице угрозам безопасности.</span><span class="sxs-lookup"><span data-stu-id="bcdca-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="bcdca-131">Если ваша цель — вывод HTML-разметка, отображает теги как разметка (например `<p></p>` для абзаца или `<em></em>` для выделения текста), см. в разделе [Объединение текста, разметка и код в блоках кода](#BM_CombiningTextMarkupAndCode) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bcdca-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="bcdca-132">Дополнительные сведения о HTML-кодирования в [работа с HTML-форм в веб-узлы веб-страниц ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="bcdca-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="bcdca-133">2. Заключите блоки кода с кодом... Полный код</span><span class="sxs-lookup"><span data-stu-id="bcdca-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="bcdca-134">Блок кода включает в себя один или несколько операторов кода, а заключено с ключевыми словами `Code` и `End Code`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="bcdca-135">Поместите открывающий `Code` ключевое слово сразу же после `@` символ &#8212; не должно быть пробелов между ними.</span><span class="sxs-lookup"><span data-stu-id="bcdca-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="bcdca-136">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-136">The result displayed in a browser:</span></span>

![Razor Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="bcdca-138">3. Внутри блока завершении каждого оператора с разрывом строки</span><span class="sxs-lookup"><span data-stu-id="bcdca-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="bcdca-139">В блоке кода Visual Basic каждая инструкция завершается разрыв строки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="bcdca-140">(Далее в этой статье вы увидите способ упаковки оператор много кода на несколько строк, при необходимости.)</span><span class="sxs-lookup"><span data-stu-id="bcdca-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="bcdca-141">4. Использовать переменные для хранения значений</span><span class="sxs-lookup"><span data-stu-id="bcdca-141">4. You use variables to store values</span></span>

<span data-ttu-id="bcdca-142">Можно хранить значения в *переменной*, включая строки, числа и даты, и т.д. Создание новой переменной с помощью `Dim` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="bcdca-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="bcdca-143">Значения переменных можно вставить непосредственно в страницы с помощью `@`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="bcdca-144">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-144">The result displayed in a browser:</span></span>

![Razor Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="bcdca-146">5. Вы литеральные значения строк следует заключить в двойные кавычки</span><span class="sxs-lookup"><span data-stu-id="bcdca-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="bcdca-147">Объект *строка* — это последовательность символов, которые обрабатываются как текст.</span><span class="sxs-lookup"><span data-stu-id="bcdca-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="bcdca-148">Чтобы указать строку, заключите его в двойные кавычки:</span><span class="sxs-lookup"><span data-stu-id="bcdca-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="bcdca-149">Чтобы внедрить двойные кавычки в пределах строковое значение, вставьте два символа двойной кавычки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="bcdca-150">Двойные кавычки появляться только один раз в выходных данных страницы, введите его как `""` в кавычках в строку и если он отображается дважды, введите его как `""""` в строке в кавычках.</span><span class="sxs-lookup"><span data-stu-id="bcdca-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="bcdca-151">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-151">The result displayed in a browser:</span></span>

![Razor Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="bcdca-153">6. Код Visual Basic регистр не учитывается</span><span class="sxs-lookup"><span data-stu-id="bcdca-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="bcdca-154">Язык Visual Basic не чувствителен к регистру.</span><span class="sxs-lookup"><span data-stu-id="bcdca-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="bcdca-155">Программирование ключевые слова (такие как `Dim`, `If`, и `True`) и имена переменных (как `myString`, или `subTotal`) могут быть записаны в любом случае.</span><span class="sxs-lookup"><span data-stu-id="bcdca-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="bcdca-156">Следующие строки кода присвоить значение переменной `lastname` использование строчных букв имени, а затем значение переменной с помощью имени в верхнем регистре.</span><span class="sxs-lookup"><span data-stu-id="bcdca-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="bcdca-157">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="bcdca-159">7. Большая часть программирования включает работу с объектами</span><span class="sxs-lookup"><span data-stu-id="bcdca-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="bcdca-160">Объект представляет нечто, что можно программировать &#8212; страницы текстовое поле, файл, изображения, веб-запроса, сообщение электронной почты, запись о заказчике (строки базы данных), и т.д. Объекты имеют свойства, описывающие их характеристики &#8212; имеет объект с текстовыми полями `Text` , объект запроса имеет `Url` , сообщение электронной почты имеет `From` свойства, а объект customer имеет `FirstName` свойство.</span><span class="sxs-lookup"><span data-stu-id="bcdca-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="bcdca-161">Объекты также имеют методы, которые являются &quot;команд&quot; они могут выполнять.</span><span class="sxs-lookup"><span data-stu-id="bcdca-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="bcdca-162">Примеры включают объект файла `Save` метод, объект изображения `Rotate` метод и объект по электронной почте `Send` метод.</span><span class="sxs-lookup"><span data-stu-id="bcdca-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="bcdca-163">Вы будете часто иметь дело с `Request` объект, который предоставляет сведения, такие как значения формы поля на странице (текстовые поля, и т.д.), тип браузера, выдавший запрос, URL-адрес страницы, удостоверение пользователя и т. д. В этом примере показано, как доступ к свойствам `Request` объекта и как вызывать `MapPath` метод `Request` объекта, который дает абсолютный путь к странице на сервере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="bcdca-164">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-164">The result displayed in a browser:</span></span>

![Razor Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="bcdca-166">8. Можно написать код, который принимает решения</span><span class="sxs-lookup"><span data-stu-id="bcdca-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="bcdca-167">Ключевой особенностью динамических веб-страниц — это, вы можете определять порядок действий в зависимости от условия.</span><span class="sxs-lookup"><span data-stu-id="bcdca-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="bcdca-168">Наиболее распространенный способ сделать это — с `If` инструкции (и необязательно `Else` инструкции).</span><span class="sxs-lookup"><span data-stu-id="bcdca-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="bcdca-169">Инструкция `If IsPost` является быстрым способом написания `If IsPost = True`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="bcdca-170">Вместе с `If` инструкции, существует множество способов для проверки условий, повторите блоки кода, и т. д., которые являются описано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bcdca-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="bcdca-171">Результат отображается в браузере (после нажатия кнопки **отправить**):</span><span class="sxs-lookup"><span data-stu-id="bcdca-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **<span data-ttu-id="bcdca-173">HTTP GET и POST методы и свойства IsPost</span><span class="sxs-lookup"><span data-stu-id="bcdca-173">HTTP GET and POST Methods and the IsPost Property</span></span>**
> 
> <span data-ttu-id="bcdca-174">Протокол, используемый для веб-страниц (HTTP) поддерживает очень ограниченный набор методов (&quot;команд&quot;), которые используются для выполнения запросов к серверу.</span><span class="sxs-lookup"><span data-stu-id="bcdca-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="bcdca-175">Два самых распространенных рисков: GET, который используется для чтения страницы, и POST, который используется для отправки страницы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="bcdca-176">Как правило первый раз пользователь запрашивает страницу, страница запрашивается с помощью запроса GET.</span><span class="sxs-lookup"><span data-stu-id="bcdca-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="bcdca-177">Если пользователь заполняет форму и затем нажимает **отправить**, браузер отправляет запрос POST на сервер.</span><span class="sxs-lookup"><span data-stu-id="bcdca-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="bcdca-178">В веб-программирования часто бывает полезно знать ли страница запрашивается как GET или POST, чтобы вы знаете, как для обработки страницы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="bcdca-179">Веб-страницах ASP.NET, можно использовать `IsPost` свойство, чтобы увидеть, является ли запрос GET или POST.</span><span class="sxs-lookup"><span data-stu-id="bcdca-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="bcdca-180">Если запрос POST, `IsPost` свойство возвратит значение true, и вы можете выполнять действия, такие как чтение значения текстовых полей в форме.</span><span class="sxs-lookup"><span data-stu-id="bcdca-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="bcdca-181">Вы увидите множество примеров продемонстрируем способ обработки страницы по-разному в зависимости от значения `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="bcdca-182">Простой пример кода</span><span class="sxs-lookup"><span data-stu-id="bcdca-182">A Simple Code Example</span></span>

<span data-ttu-id="bcdca-183">Эта процедура показано, как создать страницу, которая иллюстрирует основные приемы программирования.</span><span class="sxs-lookup"><span data-stu-id="bcdca-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="bcdca-184">В примере создайте страницу, которая позволяет пользователям вводить двух чисел, а затем он добавляет их и отображает результат.</span><span class="sxs-lookup"><span data-stu-id="bcdca-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="bcdca-185">В редакторе создайте файл и назовите его *AddNumbers.vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="bcdca-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="bcdca-186">Скопируйте следующий код и разметку в странице, заменив все уже на странице.</span><span class="sxs-lookup"><span data-stu-id="bcdca-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="bcdca-187">Ниже приведены некоторые аспекты отметить:</span><span class="sxs-lookup"><span data-stu-id="bcdca-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="bcdca-188">`@` Символ запускается первым блоком кода в странице, и перед `totalMessage` переменной, внедренных в нижней.</span><span class="sxs-lookup"><span data-stu-id="bcdca-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="bcdca-189">В верхней части страницы будет заключен в `Code...End Code`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="bcdca-190">Переменные `total`, `num1`, `num2`, и `totalMessage` хранить несколько чисел и строка.</span><span class="sxs-lookup"><span data-stu-id="bcdca-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="bcdca-191">Строковый литерал значение, присваиваемое `totalMessage` переменная находится в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="bcdca-192">Так как код Visual Basic регистр не учитывается, если `totalMessage` переменная используется в нижней части страницы, имени должна соответствовать только правильность написания объявления переменных в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="bcdca-193">Регистр не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="bcdca-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="bcdca-194">Выражение `num1.AsInt()`  +  `num2.AsInt()` показано, как работать с объектами и методами.</span><span class="sxs-lookup"><span data-stu-id="bcdca-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="bcdca-195">`AsInt` Метод для каждой переменной преобразует строку, введенные пользователем в целое число (целое число), которые могут быть добавлены.</span><span class="sxs-lookup"><span data-stu-id="bcdca-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="bcdca-196">`<form>` Тег включает `method="post"` атрибута.</span><span class="sxs-lookup"><span data-stu-id="bcdca-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="bcdca-197">Указывает, что когда пользователь щелкает **добавить**, страницы будут отправляться на сервер с помощью метода HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="bcdca-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="bcdca-198">При отправке страницы, код `If IsPost` принимает значение true и условная кода, результат сложения чисел.</span><span class="sxs-lookup"><span data-stu-id="bcdca-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="bcdca-199">Сохраните страницу и запустите его в браузере.</span><span class="sxs-lookup"><span data-stu-id="bcdca-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="bcdca-200">(Убедитесь, что выбран страницы **файлы** рабочей области, прежде чем запускать его.) Введите двумя целыми числами и нажмите кнопку **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="bcdca-202">Язык Visual Basic и синтаксис</span><span class="sxs-lookup"><span data-stu-id="bcdca-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="bcdca-203">Вы уже видели простой пример, как создать веб-страницу ASP.NET, и как можно добавить код сервера для HTML-разметка.</span><span class="sxs-lookup"><span data-stu-id="bcdca-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="bcdca-204">Здесь вы узнаете основы работы с Visual Basic для написания кода сервера ASP.NET с использованием синтаксиса Razor &#8212; то есть правила языка программирования.</span><span class="sxs-lookup"><span data-stu-id="bcdca-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="bcdca-205">Если вы являетесь опытным при программировании (особенно если вы использовали, C, C++, C#, Visual Basic или JavaScript), большая часть сведений здесь будут знакомы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="bcdca-206">Возможно, необходимо ознакомиться только с добавляется как WebMatrix код разметки в *.vbhtml* файлов.</span><span class="sxs-lookup"><span data-stu-id="bcdca-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a>  <span data-ttu-id="bcdca-207">Объединение текста, разметки и кода в блоках кода</span><span class="sxs-lookup"><span data-stu-id="bcdca-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="bcdca-208">В блоках кода сервера часто нужно будет выводить текст и разметку страницы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="bcdca-209">Если блок кода сервера содержит текст, не кода и, вместо этого должны отображаться как есть, ASP.NET необходимо иметь возможность различать этот текст из кода.</span><span class="sxs-lookup"><span data-stu-id="bcdca-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="bcdca-210">Для этого можно использовать следующие способы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-210">There are several ways to do this.</span></span>

- <span data-ttu-id="bcdca-211">Заключите текст в HTML-элемент блока как `<p></p>` или `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="bcdca-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="bcdca-212">HTML-элемента может включать текст, дополнительных элементов HTML и код сервера выражения.</span><span class="sxs-lookup"><span data-stu-id="bcdca-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="bcdca-213">Когда ASP.NET обнаруживает открывающий тег HTML (например, `<p>`), он отображает все, что элемент и его содержимое в виде браузера (и разрешает выражений код сервера).</span><span class="sxs-lookup"><span data-stu-id="bcdca-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="bcdca-214">Используйте `@:` оператор или `<text>` элемент.</span><span class="sxs-lookup"><span data-stu-id="bcdca-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="bcdca-215">`@:` Выводит одну строку содержимого, содержащего обычный текст или непарные теги HTML; `<text>` элемент заключает в себе несколько строк для вывода.</span><span class="sxs-lookup"><span data-stu-id="bcdca-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="bcdca-216">Эти параметры полезны в тех случаях, если не требуется для отрисовки HTML-элемента как часть выходных данных.</span><span class="sxs-lookup"><span data-stu-id="bcdca-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="bcdca-217">В следующем примере повторяется предыдущий пример, но использует одну пару `<text>` тегов, чтобы заключить текст для отображения.</span><span class="sxs-lookup"><span data-stu-id="bcdca-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="bcdca-218">В следующем примере `<text>` и `</text>` теги заключите три строки, каждая из которых имеет неавтономные текста и несовпадающие HTML-теги (`<br />`), а также серверный код и соответствующие теги HTML.</span><span class="sxs-lookup"><span data-stu-id="bcdca-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="bcdca-219">Опять же, может предшествовать каждой строки по отдельности с помощью `@:` оператор; либо works способом.</span><span class="sxs-lookup"><span data-stu-id="bcdca-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="bcdca-220">При выводе текста как показано в этом разделе &#8212; с помощью HTML-элемент, `@:` оператора, или `<text>` элемент &#8212; ASP.NET не HTML-кодирование выходных данных.</span><span class="sxs-lookup"><span data-stu-id="bcdca-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="bcdca-221">(Как уже отмечалось, ASP.NET кодировать выходные данные выражения кода сервера и блоков кода сервера, которым предшествует `@`, за исключением особых случаев, указанных в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="bcdca-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="bcdca-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="bcdca-222">Whitespace</span></span>

<span data-ttu-id="bcdca-223">Лишние пробелы в операторе (и за ее пределами строковым литералом) не влияют на инструкцию:</span><span class="sxs-lookup"><span data-stu-id="bcdca-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="bcdca-224">Разбиение длинных операторов на несколько строк</span><span class="sxs-lookup"><span data-stu-id="bcdca-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="bcdca-225">Длинный код инструкции можно разбить на несколько строк с помощью символа подчеркивания `_` (в Visual Basic называемый *символ продолжения*) после каждой строки кода.</span><span class="sxs-lookup"><span data-stu-id="bcdca-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="bcdca-226">Чтобы приостановить выполнение инструкции на следующую строку, в конце строки добавьте пробел, а затем символ продолжения.</span><span class="sxs-lookup"><span data-stu-id="bcdca-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="bcdca-227">Оператор Continue на следующей строке.</span><span class="sxs-lookup"><span data-stu-id="bcdca-227">Continue the statement on the next line.</span></span> <span data-ttu-id="bcdca-228">Можно включить операторов на столько строк, сколько необходимо для повышения удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="bcdca-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="bcdca-229">Следующие инструкции равнозначны:</span><span class="sxs-lookup"><span data-stu-id="bcdca-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="bcdca-230">Тем не менее нельзя создать оболочку строки середине строкового литерала.</span><span class="sxs-lookup"><span data-stu-id="bcdca-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="bcdca-231">Следующий пример не будет работать:</span><span class="sxs-lookup"><span data-stu-id="bcdca-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="bcdca-232">Чтобы объединить длинную строку, которая переносится на несколько строк, такие как приведенный выше код, необходимо использовать *оператор объединения* (`&`), который вы увидите далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bcdca-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="bcdca-233">Комментарии к коду</span><span class="sxs-lookup"><span data-stu-id="bcdca-233">Code comments</span></span>

<span data-ttu-id="bcdca-234">Комментарии можно оставлять заметки как для себя или другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="bcdca-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="bcdca-235">Комментарии синтаксис Razor начинаются с префикса `@*` и заканчиваться `*@`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="bcdca-236">Внутри блоков кода можно использовать комментарии синтаксис Razor, или можно использовать обычный символ комментария Visual Basic, который является либо одинарные (`'`) в качестве префикса для каждой строки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="bcdca-237">Переменные</span><span class="sxs-lookup"><span data-stu-id="bcdca-237">Variables</span></span>

<span data-ttu-id="bcdca-238">Переменная является именованный объект, который используется для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="bcdca-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="bcdca-239">Вы можно назвать переменные, но имя должно начинаться с буквы и не может содержать пробелы или зарезервированные символы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="bcdca-240">В Visual Basic как показано выше, не имеет значения регистра букв в имени переменной.</span><span class="sxs-lookup"><span data-stu-id="bcdca-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="bcdca-241">Переменные и типы данных</span><span class="sxs-lookup"><span data-stu-id="bcdca-241">Variables and data types</span></span>

<span data-ttu-id="bcdca-242">Переменная может иметь определенный тип данных, который указывает, какие данные хранятся в переменной.</span><span class="sxs-lookup"><span data-stu-id="bcdca-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="bcdca-243">У вас есть строковых переменных, в которых хранятся строковые значения (например &quot;Здравствуй, мир&quot;), целочисленные переменные, которые сохраняют значения целого числа (например, 3 или 79) и переменные date, в которых хранятся значения даты в различных форматах (например, 4/12/2012 или марта 2009 г. ).</span><span class="sxs-lookup"><span data-stu-id="bcdca-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="bcdca-244">И многие другие типы данных, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="bcdca-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="bcdca-245">Тем не менее не нужно указывать тип переменной.</span><span class="sxs-lookup"><span data-stu-id="bcdca-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="bcdca-246">В большинстве случаев ASP.NET может определить тип, в зависимости от того, как используются данные в переменной.</span><span class="sxs-lookup"><span data-stu-id="bcdca-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="bcdca-247">(Иногда необходимо указать тип, вы увидите примеры, когда это значение равно true.)</span><span class="sxs-lookup"><span data-stu-id="bcdca-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="bcdca-248">Чтобы объявить переменную без указания типа, используйте `Dim` плюс имя переменной (например, `Dim myVar`).</span><span class="sxs-lookup"><span data-stu-id="bcdca-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="bcdca-249">Чтобы объявить переменную с типом, используйте `Dim` плюс имя переменной, за которым следует `As` и затем имя типа (например, `Dim myVar As String`).</span><span class="sxs-lookup"><span data-stu-id="bcdca-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="bcdca-250">В следующем примере некоторые встроенные выражения, которые используют переменные на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="bcdca-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="bcdca-251">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-251">The result displayed in a browser:</span></span>

![Razor Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="bcdca-253">Преобразование и тестирование типы данных</span><span class="sxs-lookup"><span data-stu-id="bcdca-253">Converting and testing data types</span></span>

<span data-ttu-id="bcdca-254">Несмотря на то, что ASP.NET обычно можно автоматически определить тип данных, иногда это невозможно.</span><span class="sxs-lookup"><span data-stu-id="bcdca-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="bcdca-255">Таким образом может потребоваться помощь ASP.NET, выполнив явное преобразование.</span><span class="sxs-lookup"><span data-stu-id="bcdca-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="bcdca-256">Даже если у вас нет для преобразования типов, иногда бывает полезно проверить, какие типы данных вы можете работать с.</span><span class="sxs-lookup"><span data-stu-id="bcdca-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="bcdca-257">Наиболее распространенным случаем является необходимость преобразования строки в другой тип, такой как целое число или дату.</span><span class="sxs-lookup"><span data-stu-id="bcdca-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="bcdca-258">В примере показан типичный случай, где необходимо преобразовать строку в число.</span><span class="sxs-lookup"><span data-stu-id="bcdca-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="bcdca-259">Как правило входные данные пользователя будут доставляться вам как строки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="bcdca-260">Даже если предлагается ввести номер, и даже если они вводят цифры, при отправке ввод данных пользователем и прочитать его в код, данные в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="bcdca-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="bcdca-261">Таким образом необходимо преобразовать строку в число.</span><span class="sxs-lookup"><span data-stu-id="bcdca-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="bcdca-262">В примере при попытке выполнить арифметические операции над значениями без преобразования их, возникает следующая ошибка, так как ASP.NET не удается добавить две строки:</span><span class="sxs-lookup"><span data-stu-id="bcdca-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="bcdca-263">Для преобразования значений в целые числа, следует вызвать `AsInt` метод.</span><span class="sxs-lookup"><span data-stu-id="bcdca-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="bcdca-264">Если преобразование прошло успешно, затем можно добавить номера.</span><span class="sxs-lookup"><span data-stu-id="bcdca-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="bcdca-265">Ниже перечислены некоторые распространенные методы преобразования и тестирования для переменных.</span><span class="sxs-lookup"><span data-stu-id="bcdca-265">The following table lists some common conversion and test methods for variables.</span></span>


:::row:::
    :::column:::
        <strong>Method</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Example</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        Converts a string that represents a whole number (like &quot;593&quot;) to an integer.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number. (In ASP.NET, a decimal number is more precise than a floating-point number.)
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        Converts a string that represents a date and time value to the ASP.NET `DateTime` type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        Converts any other data type to a string.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::


## <a name="operators"></a><span data-ttu-id="bcdca-266">Операторы</span><span class="sxs-lookup"><span data-stu-id="bcdca-266">Operators</span></span>

<span data-ttu-id="bcdca-267">Оператор — это ключевое слово или символ, который сообщает ASP.NET, какого рода команду, выполняемую в выражении.</span><span class="sxs-lookup"><span data-stu-id="bcdca-267">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="bcdca-268">Visual Basic поддерживает многие операторы, но требуется только для распознавания немного, чтобы приступить к разработке веб-страниц ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bcdca-268">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="bcdca-269">В следующей таблице перечислены наиболее распространенные операторы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-269">The following table summarizes the most common operators.</span></span>


:::row:::
    :::column:::
        <strong>Operator</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Examples</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        Math operators used in numerical expressions.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        Assignment and equality. Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        Inequality. Returns `True` if the values are not equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        Less than, greater than, less than or equal, and greater than or equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        Concatenation, which is used to join strings.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        The increment and decrement operators, which add and subtract 1 (respectively) from a variable.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        Dot. Used to distinguish objects and their properties and methods.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        Parentheses. Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        Not. Reverses a true value to false and vice versa. Typically used as a shorthand way to test for `False` (that is, for not `True`).
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        Logical AND and OR, which are used to link conditions together.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="bcdca-270">Работа с файлом и пути к папкам в коде</span><span class="sxs-lookup"><span data-stu-id="bcdca-270">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="bcdca-271">Вы будете часто работать пути файлов и папок в коде.</span><span class="sxs-lookup"><span data-stu-id="bcdca-271">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="bcdca-272">Ниже приведен пример структуры физическую папку для веб-сайта, которое может отображаться на компьютере разработчика:</span><span class="sxs-lookup"><span data-stu-id="bcdca-272">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="bcdca-273">Ниже приведены некоторые важные сведения о URL-адреса и пути.</span><span class="sxs-lookup"><span data-stu-id="bcdca-273">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="bcdca-274">URL-адрес начинается с любым именем домена (`http://www.example.com`) или имя сервера (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="bcdca-274">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="bcdca-275">URL-адрес соответствует физический путь на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bcdca-275">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="bcdca-276">Например `http://myserver` может соответствовать папке *C:\websites\mywebsite* на сервере.</span><span class="sxs-lookup"><span data-stu-id="bcdca-276">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="bcdca-277">Виртуальный путь является сокращением для представления путей в коде без указания полного пути.</span><span class="sxs-lookup"><span data-stu-id="bcdca-277">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="bcdca-278">Он включает в себя часть URL-адрес, который следует за именем домена или сервера.</span><span class="sxs-lookup"><span data-stu-id="bcdca-278">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="bcdca-279">При использовании виртуальных путей, можно перенести код в другой домен или сервер без необходимости обновите пути.</span><span class="sxs-lookup"><span data-stu-id="bcdca-279">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="bcdca-280">Ниже приведен пример, чтобы помочь вам понять различия:</span><span class="sxs-lookup"><span data-stu-id="bcdca-280">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="bcdca-281">Полный URL-адрес</span><span class="sxs-lookup"><span data-stu-id="bcdca-281">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="bcdca-282">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="bcdca-282">Server name</span></span> | *<span data-ttu-id="bcdca-283">mycompanyserver</span><span class="sxs-lookup"><span data-stu-id="bcdca-283">mycompanyserver</span></span>* |
| <span data-ttu-id="bcdca-284">Виртуальный путь</span><span class="sxs-lookup"><span data-stu-id="bcdca-284">Virtual path</span></span> | *<span data-ttu-id="bcdca-285">/HumanResources/CompanyPolicy.htm</span><span class="sxs-lookup"><span data-stu-id="bcdca-285">/humanresources/CompanyPolicy.htm</span></span>* |
| <span data-ttu-id="bcdca-286">Физический путь</span><span class="sxs-lookup"><span data-stu-id="bcdca-286">Physical path</span></span> | *<span data-ttu-id="bcdca-287">C:\mywebsites\humanresources\CompanyPolicy.htm</span><span class="sxs-lookup"><span data-stu-id="bcdca-287">C:\mywebsites\humanresources\CompanyPolicy.htm</span></span>* |

<span data-ttu-id="bcdca-288">Виртуальный корневой каталог — /, так же, как корень диска c диск — \.</span><span class="sxs-lookup"><span data-stu-id="bcdca-288">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="bcdca-289">(Виртуальная папка пути всегда использовать символы косой черты). Виртуальный путь к папке не нужно иметь то же имя как физический каталог; Это может быть псевдонимом.</span><span class="sxs-lookup"><span data-stu-id="bcdca-289">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="bcdca-290">(На рабочих серверах, виртуальный путь редко соответствует как полный физический путь.)</span><span class="sxs-lookup"><span data-stu-id="bcdca-290">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="bcdca-291">При работе с файлами и папками в коде, иногда требуется для ссылки на физический путь и иногда виртуального пути, в зависимости от того, какие объекты, которыми вы работаете.</span><span class="sxs-lookup"><span data-stu-id="bcdca-291">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="bcdca-292">ASP.NET предоставляет эти средства для работы с пути файлов и папок в коде: `Server.MapPath` метод и `~` оператор и `Href` метод.</span><span class="sxs-lookup"><span data-stu-id="bcdca-292">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="bcdca-293">Преобразование виртуальных и физических путей: метод Server.MapPath</span><span class="sxs-lookup"><span data-stu-id="bcdca-293">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="bcdca-294">`Server.MapPath` Метод преобразует виртуальный путь (например */default.cshtml*) в абсолютный физический путь (например *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="bcdca-294">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="bcdca-295">Этот метод использовать когда требуется полный физический путь.</span><span class="sxs-lookup"><span data-stu-id="bcdca-295">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="bcdca-296">Типичный пример — при чтении или записи в текстовый файл или файл изображения на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="bcdca-296">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="bcdca-297">Абсолютный физический путь веб-сайта на сервере размещения сайта обычно не известен, поэтому этот метод можно преобразовать путь вы знаете, виртуальный путь, соответствующий путь на сервере для вас.</span><span class="sxs-lookup"><span data-stu-id="bcdca-297">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="bcdca-298">Передайте виртуальный путь к файлу или папке в метод и возвращает физический путь:</span><span class="sxs-lookup"><span data-stu-id="bcdca-298">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="bcdca-299">Ссылка на виртуальный корневой каталог: ~ оператор и метод Href</span><span class="sxs-lookup"><span data-stu-id="bcdca-299">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="bcdca-300">В *.cshtml* или *.vbhtml* файл, вы можете ссылаться на пути виртуального корневого каталога, используя `~` оператор.</span><span class="sxs-lookup"><span data-stu-id="bcdca-300">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="bcdca-301">Это очень удобно, так как для перемещения страниц на узле и все ссылки, содержащиеся в них на другие страницы не будет нарушена.</span><span class="sxs-lookup"><span data-stu-id="bcdca-301">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="bcdca-302">Это также удобно в случае, если когда-либо переместить веб-сайта в другое расположение.</span><span class="sxs-lookup"><span data-stu-id="bcdca-302">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="bcdca-303">Далее приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="bcdca-303">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="bcdca-304">Если веб-сайт `http://myserver/myapp`, вот как ASP.NET будет интерпретировать эти пути, при запуске страницы:</span><span class="sxs-lookup"><span data-stu-id="bcdca-304">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- `myImagesFolder`<span data-ttu-id="bcdca-305">:</span><span class="sxs-lookup"><span data-stu-id="bcdca-305">:</span></span> `http://myserver/myapp/images`
- `myStyleSheet` <span data-ttu-id="bcdca-306">:</span><span class="sxs-lookup"><span data-stu-id="bcdca-306">:</span></span> `http://myserver/myapp/styles/Stylesheet.css`

<span data-ttu-id="bcdca-307">(Вы не увидите эти пути в качестве значения переменной, но ASP.NET будет рассматривать пути, как в случае, они были).</span><span class="sxs-lookup"><span data-stu-id="bcdca-307">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="bcdca-308">Можно использовать `~` оператор, как в серверном коде (как описано выше), так и в разметке, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bcdca-308">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="bcdca-309">В разметке, использовании `~` оператор для создания путей к ресурсам, например файлы изображений, другие веб-страниц и файлов CSS.</span><span class="sxs-lookup"><span data-stu-id="bcdca-309">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="bcdca-310">При запуске страницы ASP.NET, просматривает страницы (код и разметку) и разрешает все `~` ссылки на соответствующий путь.</span><span class="sxs-lookup"><span data-stu-id="bcdca-310">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="bcdca-311">Условной логики и циклов</span><span class="sxs-lookup"><span data-stu-id="bcdca-311">Conditional Logic and Loops</span></span>

<span data-ttu-id="bcdca-312">Код сервера ASP.NET позволяет выполнять задачи на основе условий и написать код, который повторяется определенное число раз, то есть код инструкции, выполняется цикл).</span><span class="sxs-lookup"><span data-stu-id="bcdca-312">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="bcdca-313">Проверка условий</span><span class="sxs-lookup"><span data-stu-id="bcdca-313">Testing conditions</span></span>

<span data-ttu-id="bcdca-314">Для тестирования на выполнение простого условия можно использовать `If...Then` инструкцию, которая возвращает `True` или `False` зависимости от теста, можно указать:</span><span class="sxs-lookup"><span data-stu-id="bcdca-314">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="bcdca-315">`If` Ключевое слово начинается блок.</span><span class="sxs-lookup"><span data-stu-id="bcdca-315">The `If` keyword starts a block.</span></span> <span data-ttu-id="bcdca-316">Тест этот сам (условие) соответствует `If` ключевое слово и возвращает значение true или false.</span><span class="sxs-lookup"><span data-stu-id="bcdca-316">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="bcdca-317">`If` Заканчивается инструкция `Then`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-317">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="bcdca-318">Операторы, которые будут выполняться, если аргумент имеет значение true, заключенных с `If` и `End If`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-318">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="bcdca-319">`If` Инструкция может содержать `Else` блок, который задает операторы, которые выполняются, если условие имеет значение false:</span><span class="sxs-lookup"><span data-stu-id="bcdca-319">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="bcdca-320">Если `If` инструкции начинается блок кода, не нужно использовать обычный `Code...End Code` инструкции, чтобы включить блоки.</span><span class="sxs-lookup"><span data-stu-id="bcdca-320">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="bcdca-321">Можно просто добавить `@` блоку, и он будет работать.</span><span class="sxs-lookup"><span data-stu-id="bcdca-321">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="bcdca-322">Этот подход работает с `If` а также другие программирования ключевые слова, которые следуют блоки кода, включая Visual Basic `For`, `For Each`, `Do While`и т. д.</span><span class="sxs-lookup"><span data-stu-id="bcdca-322">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="bcdca-323">Можно добавить несколько условий, используя один или несколько `ElseIf` блоков:</span><span class="sxs-lookup"><span data-stu-id="bcdca-323">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="bcdca-324">В этом примере, если первое условие в `If` блок не имеет значение true, `ElseIf` проверяется условие.</span><span class="sxs-lookup"><span data-stu-id="bcdca-324">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="bcdca-325">Если это условие выполнено, операторы в `ElseIf` блоке.</span><span class="sxs-lookup"><span data-stu-id="bcdca-325">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="bcdca-326">Если ни одно из условий не соблюдается, операторы в `Else` блоке.</span><span class="sxs-lookup"><span data-stu-id="bcdca-326">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="bcdca-327">Можно добавить любое количество `ElseIf` блокирует, а затем закройте с `Else` заблокировать, в виде &quot;все остальное&quot; условие.</span><span class="sxs-lookup"><span data-stu-id="bcdca-327">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="bcdca-328">Чтобы протестировать большое количество условий, используйте `Select Case` блок:</span><span class="sxs-lookup"><span data-stu-id="bcdca-328">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="bcdca-329">Значение для проверки, указан в скобках (в примере переменная дня недели).</span><span class="sxs-lookup"><span data-stu-id="bcdca-329">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="bcdca-330">Каждого отдельного теста использует `Case` инструкцию, которая содержит значение.</span><span class="sxs-lookup"><span data-stu-id="bcdca-330">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="bcdca-331">Если значение `Case` инструкции совпадает со значением теста, код, который `Case` выполняется блок.</span><span class="sxs-lookup"><span data-stu-id="bcdca-331">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="bcdca-332">Результат выполнения двух последних блоки условий, отображаемый в браузере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-332">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="bcdca-334">Циклическое кода</span><span class="sxs-lookup"><span data-stu-id="bcdca-334">Looping code</span></span>

<span data-ttu-id="bcdca-335">Часто требуется многократно выполнять те же операторы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-335">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="bcdca-336">Для этого цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-336">You do this by looping.</span></span> <span data-ttu-id="bcdca-337">Например вы часто выполняются те же операторы для каждого элемента в коллекции данных.</span><span class="sxs-lookup"><span data-stu-id="bcdca-337">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="bcdca-338">Если вы знаете, точно того, как часто необходимо применить цикл, можно использовать `For` цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-338">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="bcdca-339">Этот тип цикла удобен для подсчета или отсчет:</span><span class="sxs-lookup"><span data-stu-id="bcdca-339">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="bcdca-340">Цикл начинается с `For` ключевое слово, и три элемента:</span><span class="sxs-lookup"><span data-stu-id="bcdca-340">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="bcdca-341">Сразу после `For` инструкции, объявите переменную счетчика (не обязательно использовать `Dim`) и укажите диапазон, как показано на `i = 10 to 20`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-341">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="bcdca-342">Это означает, что переменная `i` начинается нумерацию строк с 10 и продолжается до достижения 20 (включительно).</span><span class="sxs-lookup"><span data-stu-id="bcdca-342">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="bcdca-343">Между `For` и `Next` инструкций — содержимое блока.</span><span class="sxs-lookup"><span data-stu-id="bcdca-343">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="bcdca-344">Это может содержать один или несколько операторов кода, которые выполняются с каждого цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-344">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="bcdca-345">`Next i` Инструкция завершает цикл.</span><span class="sxs-lookup"><span data-stu-id="bcdca-345">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="bcdca-346">Он увеличивает значение счетчика и запуске следующей итерации цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-346">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="bcdca-347">Строка кода между `For` и `Next` строк содержит код, который выполняется для каждой итерации цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-347">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="bcdca-348">Разметка создает новый абзац (`<p>` элемент) каждый раз и добавляет строку в выходные данные, отображают значение i (счетчик).</span><span class="sxs-lookup"><span data-stu-id="bcdca-348">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="bcdca-349">Когда вы запускаете эту страницу, в примере создается 11 строк, отображение выходных данных, с текстом в каждой строке, указывающее номер элемента.</span><span class="sxs-lookup"><span data-stu-id="bcdca-349">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="bcdca-351">Если вы работаете в коллекции или массива, часто используют `For Each` цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-351">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="bcdca-352">Коллекция — это группа схожих объектов и `For Each` цикле позволяет выполнить задачу для каждого элемента в коллекции.</span><span class="sxs-lookup"><span data-stu-id="bcdca-352">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="bcdca-353">Этот тип цикла удобен для коллекций, так как в отличие от `For` цикл, у вас нет для увеличения значения счетчика или ограничить.</span><span class="sxs-lookup"><span data-stu-id="bcdca-353">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="bcdca-354">Вместо этого `For Each` код цикла просто продолжается через коллекцию до его завершения.</span><span class="sxs-lookup"><span data-stu-id="bcdca-354">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="bcdca-355">Этот пример возвращает элементы в `Request.ServerVariables` коллекции (который содержит сведения о веб-сервере).</span><span class="sxs-lookup"><span data-stu-id="bcdca-355">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="bcdca-356">Она использует `For Each` цикл для отображения имени каждого элемента путем создания нового `<li>` элемента в HTML-маркированного списка.</span><span class="sxs-lookup"><span data-stu-id="bcdca-356">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="bcdca-357">`For Each` Ключевого слова следуют переменную, которая представляет один элемент в коллекции (в примере `myItem`), за которым следует `In` ключевое слово, и вы хотите организовать цикл по коллекции.</span><span class="sxs-lookup"><span data-stu-id="bcdca-357">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="bcdca-358">В теле `For Each` цикла, можно получить доступ к текущего элемента, с помощью переменной, объявленный ранее.</span><span class="sxs-lookup"><span data-stu-id="bcdca-358">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="bcdca-360">Чтобы создать цикл программирования более общего назначения, используйте `Do While` инструкции:</span><span class="sxs-lookup"><span data-stu-id="bcdca-360">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="bcdca-361">Этот цикл начинается с `Do While` ключевое слово, и условия, следует блок для повторения.</span><span class="sxs-lookup"><span data-stu-id="bcdca-361">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="bcdca-362">Циклы обычно увеличивается (Добавление) или уменьшения (вычитаемое) переменной или объекта, используемые для подсчета.</span><span class="sxs-lookup"><span data-stu-id="bcdca-362">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="bcdca-363">В примере `+=` оператор добавляет 1 к значению переменной при каждом выполнении цикла.</span><span class="sxs-lookup"><span data-stu-id="bcdca-363">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="bcdca-364">(Чтобы уменьшают значение переменной в цикле, который отсчитывает, используйте оператор декремента `-=`.)</span><span class="sxs-lookup"><span data-stu-id="bcdca-364">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="bcdca-365">Объекты и коллекции</span><span class="sxs-lookup"><span data-stu-id="bcdca-365">Objects and Collections</span></span>

<span data-ttu-id="bcdca-366">Почти все в на веб-сайте ASP.NET — это объект, включая саму веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="bcdca-366">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="bcdca-367">В этом разделе рассматриваются некоторые важные объекты, которые вы будете работать с часто в коде.</span><span class="sxs-lookup"><span data-stu-id="bcdca-367">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="bcdca-368">Объекты страниц</span><span class="sxs-lookup"><span data-stu-id="bcdca-368">Page objects</span></span>

<span data-ttu-id="bcdca-369">Самый простой объект в ASP.NET является страница.</span><span class="sxs-lookup"><span data-stu-id="bcdca-369">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="bcdca-370">Можно получить доступ к свойствам объекта страницу напрямую без любой подходящий объект.</span><span class="sxs-lookup"><span data-stu-id="bcdca-370">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="bcdca-371">Следующий код получает путь к файлу страницы, с помощью `Request` объект страницы:</span><span class="sxs-lookup"><span data-stu-id="bcdca-371">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="bcdca-372">Можно использовать свойства `Page` объекта, чтобы получить массу информации, такие как:</span><span class="sxs-lookup"><span data-stu-id="bcdca-372">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- `Request`<span data-ttu-id="bcdca-373">.</span><span class="sxs-lookup"><span data-stu-id="bcdca-373">.</span></span> <span data-ttu-id="bcdca-374">Как вы уже видели, это коллекция сведений о текущем запросе, включая тип браузера, выдавший запрос, URL-адрес страницы, удостоверение пользователя и т. д.</span><span class="sxs-lookup"><span data-stu-id="bcdca-374">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- `Response`<span data-ttu-id="bcdca-375">.</span><span class="sxs-lookup"><span data-stu-id="bcdca-375">.</span></span> <span data-ttu-id="bcdca-376">Это коллекция сведений об ответе (страницы), отправляемого в браузер при серверный код завершения работы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-376">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="bcdca-377">Например это свойство можно использовать для записи сведений в ответ.</span><span class="sxs-lookup"><span data-stu-id="bcdca-377">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="bcdca-378">Коллекция объектов (массивов и словарей)</span><span class="sxs-lookup"><span data-stu-id="bcdca-378">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="bcdca-379">Коллекция — это группа объектов одного типа, например, коллекцию `Customer` объекты из базы данных.</span><span class="sxs-lookup"><span data-stu-id="bcdca-379">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="bcdca-380">ASP.NET содержит множество встроенных коллекций, включая `Request.Files` коллекции.</span><span class="sxs-lookup"><span data-stu-id="bcdca-380">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="bcdca-381">Вы будете часто работать с данными в коллекции.</span><span class="sxs-lookup"><span data-stu-id="bcdca-381">You'll often work with data in collections.</span></span> <span data-ttu-id="bcdca-382">Два распространенных типов коллекций являются *массива* и *словарь*.</span><span class="sxs-lookup"><span data-stu-id="bcdca-382">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="bcdca-383">Массив полезно в том случае, если вы хотите хранить коллекции схожих элементов, но не нужно создавать отдельную переменную для хранения каждого элемента:</span><span class="sxs-lookup"><span data-stu-id="bcdca-383">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="bcdca-384">В массивах можно объявить определенный тип данных, например `String`, `Integer`, или `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-384">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="bcdca-385">Чтобы указать, что переменная может содержать массив, добавить круглые скобки к имени переменной в объявлении (такие как `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="bcdca-385">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="bcdca-386">Можно получить доступ к элементам в массиве с помощью их положение (индекс) или с помощью `For Each` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcdca-386">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="bcdca-387">Массив индексы отсчитываются от нуля &#8212; то есть первый элемент находится в позиции 0, второй элемент находится в позиции 1 и т. д.</span><span class="sxs-lookup"><span data-stu-id="bcdca-387">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="bcdca-388">Можно определить количество элементов в массиве, получив его `Length` свойство.</span><span class="sxs-lookup"><span data-stu-id="bcdca-388">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="bcdca-389">Чтобы получить позицию конкретного элемента в массиве (т. е для поиска массив), используйте `Array.IndexOf` метод.</span><span class="sxs-lookup"><span data-stu-id="bcdca-389">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="bcdca-390">Вы можете также выполнять действия как обратное содержимое массива ( `Array.Reverse` метод) или Сортировка содержимого ( `Array.Sort` метод).</span><span class="sxs-lookup"><span data-stu-id="bcdca-390">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="bcdca-391">В результате выполнения код массив строки, отображаемый в браузере.</span><span class="sxs-lookup"><span data-stu-id="bcdca-391">The output of the string array code displayed in a browser:</span></span>

![Razor Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="bcdca-393">Словарь является коллекцией пар "ключ значение", где можно ввести ключ (или имя), чтобы задать или получить соответствующее значение:</span><span class="sxs-lookup"><span data-stu-id="bcdca-393">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="bcdca-394">Чтобы создать словарь, используйте `New` ключевое слово, чтобы указать, что вы создаете новый `Dictionary` объекта.</span><span class="sxs-lookup"><span data-stu-id="bcdca-394">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="bcdca-395">Словарь можно назначить переменной с помощью `Dim` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="bcdca-395">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="bcdca-396">Можно указать типы данных элементов в словаре, с помощью скобок ( `( )` ).</span><span class="sxs-lookup"><span data-stu-id="bcdca-396">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="bcdca-397">В конце объявления необходимо добавить еще одной пары скобок, так как это фактически является методом, который создает новый словарь.</span><span class="sxs-lookup"><span data-stu-id="bcdca-397">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="bcdca-398">Для добавления элементов в словарь, можно вызвать `Add` метод переменной словарь (`myScores` в данном случае), а затем укажите ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="bcdca-398">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="bcdca-399">Кроме того можно использовать скобки для указания ключа и выполните простые присваивания, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="bcdca-399">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="bcdca-400">Чтобы получить значение из словаря, необходимо указать ключ в круглые скобки:</span><span class="sxs-lookup"><span data-stu-id="bcdca-400">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="bcdca-401">Вызов методов с параметрами</span><span class="sxs-lookup"><span data-stu-id="bcdca-401">Calling Methods with Parameters</span></span>

<span data-ttu-id="bcdca-402">Как было показано ранее в этой статье, объекты, которые программируется с имеют методы.</span><span class="sxs-lookup"><span data-stu-id="bcdca-402">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="bcdca-403">Например `Database` объект может иметь `Database.Connect` метод.</span><span class="sxs-lookup"><span data-stu-id="bcdca-403">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="bcdca-404">Многие методы также имеют один или несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="bcdca-404">Many methods also have one or more parameters.</span></span> <span data-ttu-id="bcdca-405">Объект *параметр* является значение, которое можно передать в метод, чтобы включить этот метод для выполнения необходимых задач.</span><span class="sxs-lookup"><span data-stu-id="bcdca-405">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="bcdca-406">Например, взгляните на объявление для `Request.MapPath` метод, который принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="bcdca-406">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="bcdca-407">Этот метод возвращает физический путь на сервере, который соответствует для заданного виртуального пути.</span><span class="sxs-lookup"><span data-stu-id="bcdca-407">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="bcdca-408">Три параметра для метода являются `virtualPath`, `baseVirtualDir`, и `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="bcdca-408">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="bcdca-409">(Обратите внимание на то, что в объявлении с типами данных, данных, которые они оставлю перечисляются параметры). При вызове этого метода необходимо указать значения для всех трех параметров.</span><span class="sxs-lookup"><span data-stu-id="bcdca-409">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="bcdca-410">При использовании Visual Basic с синтаксисом Razor, у вас есть два варианта для передачи параметров в метод: *позиционные параметры* или *именованные параметры*.</span><span class="sxs-lookup"><span data-stu-id="bcdca-410">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="bcdca-411">Чтобы вызвать метод, с помощью позиционные параметры, параметры передаются в строгом порядке, который указан в объявлении метода.</span><span class="sxs-lookup"><span data-stu-id="bcdca-411">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="bcdca-412">(Вы обычно будет этот порядок по чтению документации для метода.) Необходимо соблюдать порядок и какого-либо параметра невозможно пропустить &#8212; при необходимости можно передать пустую строку (`""`) или значение null для позиционного параметра, которое не имеет значения для.</span><span class="sxs-lookup"><span data-stu-id="bcdca-412">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="bcdca-413">В следующем примере предполагается, что у вас есть папка с именем *сценариев* на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="bcdca-413">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="bcdca-414">Этот код вызывает `Request.MapPath` метод и передает эти значения для трех параметров в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="bcdca-414">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="bcdca-415">Затем отображается сопоставленные результирующий контур.</span><span class="sxs-lookup"><span data-stu-id="bcdca-415">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="bcdca-416">При существует много параметров для метода, можно сохранить код более понятным и удобочитаемым с помощью именованных параметров.</span><span class="sxs-lookup"><span data-stu-id="bcdca-416">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="bcdca-417">Чтобы вызвать метод с использованием именованных параметров, укажите имя параметра, за которым следует `:=` и затем укажите значение.</span><span class="sxs-lookup"><span data-stu-id="bcdca-417">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="bcdca-418">Именованных параметров удобен тем, что их можно добавить в любом порядке, который вы хотите.</span><span class="sxs-lookup"><span data-stu-id="bcdca-418">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="bcdca-419">(Недостаток заключается в вызове метода не является компактным).</span><span class="sxs-lookup"><span data-stu-id="bcdca-419">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="bcdca-420">В следующем примере вызывается тот же метод, как описано выше, но использует именованные параметры для предоставления значений:</span><span class="sxs-lookup"><span data-stu-id="bcdca-420">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="bcdca-421">Как видите, эти параметры передаются в другом порядке.</span><span class="sxs-lookup"><span data-stu-id="bcdca-421">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="bcdca-422">Тем не менее при выполнении предыдущего примера и в этом примере, они будут возвращать то же значение.</span><span class="sxs-lookup"><span data-stu-id="bcdca-422">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="bcdca-423">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="bcdca-423">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="bcdca-424">Операторы Try-Catch</span><span class="sxs-lookup"><span data-stu-id="bcdca-424">Try-Catch statements</span></span>

<span data-ttu-id="bcdca-425">У вас будет часто инструкций в коде, может завершиться ошибкой по соображениям за пределами элемента управления.</span><span class="sxs-lookup"><span data-stu-id="bcdca-425">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="bcdca-426">Пример:</span><span class="sxs-lookup"><span data-stu-id="bcdca-426">For example:</span></span>

- <span data-ttu-id="bcdca-427">Если код пытается открыть, создание, чтение или запись в файл, может возникнуть все виды ошибок.</span><span class="sxs-lookup"><span data-stu-id="bcdca-427">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="bcdca-428">Файл может отсутствовать, может быть заблокирован, код может не иметь разрешения и т. д.</span><span class="sxs-lookup"><span data-stu-id="bcdca-428">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="bcdca-429">Аналогичным образом Если код пытается выполнить обновления записей в базе данных, могут быть проблемы с разрешениями, подключение к базе данных могут быть удалены, сохраняемые данные может быть недопустимым и т. д.</span><span class="sxs-lookup"><span data-stu-id="bcdca-429">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="bcdca-430">С точки зрения программирования, называются таких ситуациях *исключения*.</span><span class="sxs-lookup"><span data-stu-id="bcdca-430">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="bcdca-431">Если код обнаруживает исключение, он создает (вызывает) сообщение об ошибке, в лучшем случае к пользователям.</span><span class="sxs-lookup"><span data-stu-id="bcdca-431">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="bcdca-433">В ситуациях, где ваш код может обнаружить исключения, а также чтобы избежать сообщения об ошибках этого типа, можно использовать `Try/Catch` инструкций.</span><span class="sxs-lookup"><span data-stu-id="bcdca-433">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="bcdca-434">В `Try` инструкции, запустите код, который вы проверяете.</span><span class="sxs-lookup"><span data-stu-id="bcdca-434">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="bcdca-435">В одной или нескольких `Catch` инструкций, можно произвести поиск конкретных ошибок (определенные типы исключений), которые могли возникнуть.</span><span class="sxs-lookup"><span data-stu-id="bcdca-435">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="bcdca-436">Можно включить столько `Catch` инструкциях, как вам нужно искать ошибки, которые вы ожидаем.</span><span class="sxs-lookup"><span data-stu-id="bcdca-436">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdca-437">Рекомендуется избегать использования `Response.Redirect` метод в `Try/Catch` инструкции, так как он может вызвать исключение в страницу.</span><span class="sxs-lookup"><span data-stu-id="bcdca-437">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="bcdca-438">Пример страницы, которая создает текстовый файл, при первом запросе и затем отображает кнопку, которая позволяет пользователю открыть файл.</span><span class="sxs-lookup"><span data-stu-id="bcdca-438">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="bcdca-439">В примере намеренно используется недопустимое имя файла, чтобы он вызовет исключение.</span><span class="sxs-lookup"><span data-stu-id="bcdca-439">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="bcdca-440">Код включает `Catch` инструкций для двух возможных исключений: `FileNotFoundException`, это происходит, если имя файла недопустимо, и `DirectoryNotFoundException`, это происходит, если ASP.NET даже не удается найти папку.</span><span class="sxs-lookup"><span data-stu-id="bcdca-440">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="bcdca-441">(Чтобы увидеть, как оно работает, если все работает надлежащим образом можно Раскомментировать инструкция в примере.)</span><span class="sxs-lookup"><span data-stu-id="bcdca-441">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="bcdca-442">Если ваш код не обрабатывает исключение, вы увидите страницу ошибки, как и на предыдущем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="bcdca-442">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="bcdca-443">Тем не менее `Try/Catch` раздел помогает предотвратить просмотр таких ошибок пользователя.</span><span class="sxs-lookup"><span data-stu-id="bcdca-443">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="bcdca-444">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bcdca-444">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="bcdca-445">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="bcdca-445">Reference Documentation</span></span>

- [<span data-ttu-id="bcdca-446">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bcdca-446">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="bcdca-447">Язык Visual Basic</span><span class="sxs-lookup"><span data-stu-id="bcdca-447">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
