---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: Динамическое заполнение элемента управления, с помощью кода JavaScript (C#) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: e8b49f41f132cc31ca458ce0af3b74dbb54f225e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026571"
---
<a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="f0c01-103">Динамическое заполнение элемента управления с помощью кода JavaScript (C#)</span><span class="sxs-lookup"><span data-stu-id="f0c01-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>
====================
<span data-ttu-id="f0c01-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f0c01-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f0c01-105">[Скачать код](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f0c01-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="f0c01-106">Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="f0c01-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="f0c01-107">Можно также активировать заполнение, с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="f0c01-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="f0c01-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="f0c01-108">Overview</span></span>

<span data-ttu-id="f0c01-109">`DynamicPopulate` Элемента управления в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы.</span><span class="sxs-lookup"><span data-stu-id="f0c01-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="f0c01-110">Можно также активировать заполнение, с помощью пользовательского кода JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="f0c01-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="f0c01-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="f0c01-111">Steps</span></span>

<span data-ttu-id="f0c01-112">Во-первых, необходимо, чтобы к веб-службе ASP.NET, который реализует метод, вызываемый `DynamicPopulateExtender` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="f0c01-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="f0c01-113">Веб-служба реализует метод `getDate()` , ожидает один аргумент типа строки, называемой `contextKey`, так как `DynamicPopulate` элемент управления отправляет понимается набор сведений о контексте с каждый вызов веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f0c01-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="f0c01-114">Ниже приведен код (файл `DynamicPopulate.cs.asmx`) который получает текущую дату в одном из трех форматов:</span><span class="sxs-lookup"><span data-stu-id="f0c01-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="f0c01-115">На следующем шаге создайте новый сайт ASP.NET и начать с элементом управления ASP.NET AJAX ScriptManager:</span><span class="sxs-lookup"><span data-stu-id="f0c01-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="f0c01-116">Затем добавьте элемент управления label (например с помощью HTML-элемент управления с тем же именем, или `<asp:Label />` веб-элемент управления) где позже будет показано, результатом вызова веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f0c01-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="f0c01-117">Далее включите `DynamicPopulateExtender` управление и предоставляют данные веб-службы, целевой элемент управления, но не имя элемента управления, который запускает заполнение, это будет сделано позже с помощью пользовательским кодом JavaScript!</span><span class="sxs-lookup"><span data-stu-id="f0c01-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="f0c01-118">Теперь в компонент JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f0c01-118">Now to the JavaScript part.</span></span> <span data-ttu-id="f0c01-119">`$find()` Функции, определенные в библиотеке AJAX для ASP.NET, такие как возвращает ссылку на стороне сервера объекты ASP.NET AJAX Control Toolkit `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="f0c01-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="f0c01-120">В текущем файле `$find("dpe")` возвращает ссылку на `DynamicPopulateExtender` элемента управления на странице.</span><span class="sxs-lookup"><span data-stu-id="f0c01-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="f0c01-121">Он предоставляет метод, называемый `populate()` чего начнется процесс динамического заполнения.</span><span class="sxs-lookup"><span data-stu-id="f0c01-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="f0c01-122">`populate()` Метод требует один аргумент: контекстный ключ, который будет использоваться в качестве аргумента `getDate()` веб-метод.</span><span class="sxs-lookup"><span data-stu-id="f0c01-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="f0c01-123">Например `$find("dpe").populate("format1")` заполнения метку с текущей датой в формате месяц день год.</span><span class="sxs-lookup"><span data-stu-id="f0c01-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="f0c01-124">Чтобы сделать пример более гибкий, пользователь может выбрать один из нескольких форматов даты.</span><span class="sxs-lookup"><span data-stu-id="f0c01-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="f0c01-125">Для каждой из них отображается типа "переключатель".</span><span class="sxs-lookup"><span data-stu-id="f0c01-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="f0c01-126">Один раз когда пользователь щелкает переключатель, код JavaScript динамически заполняет метку с выбранным форматом даты.</span><span class="sxs-lookup"><span data-stu-id="f0c01-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="f0c01-127">Ниже приведены эти переключатели.</span><span class="sxs-lookup"><span data-stu-id="f0c01-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="f0c01-128">Обратите внимание, что в контексте типа "переключатель", выражение JavaScript `this.value` ссылается на значение «текущий», которая может быть точно те же данные `getDate()` метод может работать с.</span><span class="sxs-lookup"><span data-stu-id="f0c01-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>


<span data-ttu-id="f0c01-129">[![Нажмите кнопку извлекает дату с сервера, в указанном формате](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f0c01-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="f0c01-130">Нажмите кнопку извлекает дату с сервера, в формате, заданном ([Просмотр полноразмерного изображения](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f0c01-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f0c01-131">[Назад](dynamically-populating-a-control-cs.md)
> [Вперед](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f0c01-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>