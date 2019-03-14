---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: Добавление контроллера | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленную версию этого учебника доступен здесь, использующий ASP.NET MVC 5 и Visual Studio 2013. Это более безопасное и гораздо проще выполнить и демонстрационных версий...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6cc64cd9ed7a8a4cf053a63d22214bf31a80147b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057751"
---
<a name="adding-a-controller"></a><span data-ttu-id="ff310-104">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="ff310-104">Adding a Controller</span></span>
====================
<span data-ttu-id="ff310-105">по [Рик Андерсон]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="ff310-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="ff310-106">Обновленную версию этого учебника доступен [здесь](../../getting-started/introduction/getting-started.md) , использующий ASP.NET MVC 5 и Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ff310-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="ff310-107">Она более безопасные, гораздо проще следовать и показаны дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="ff310-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="ff310-108">MVC означает *model-view-controller*.</span><span class="sxs-lookup"><span data-stu-id="ff310-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="ff310-109">MVC — это шаблон для разработки приложений, которые хорошо продуманной архитектурой, пригодного для тестирования и простые в обслуживании.</span><span class="sxs-lookup"><span data-stu-id="ff310-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="ff310-110">Приложения на основе MVC содержат:</span><span class="sxs-lookup"><span data-stu-id="ff310-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="ff310-111">**M** odels: Классы, представляющие данные приложения и используют логику проверки для реализации бизнес-правил к этим данным.</span><span class="sxs-lookup"><span data-stu-id="ff310-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="ff310-112">**V** редставления: Файлы шаблонов, которые приложение использует для динамического создания HTML-ответов.</span><span class="sxs-lookup"><span data-stu-id="ff310-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="ff310-113">**C** ontrollers: Классы, которые обрабатывают входящие запросы браузера, извлекают данные модели, а затем укажите шаблоны представлений, которые возвращают ответ в браузере.</span><span class="sxs-lookup"><span data-stu-id="ff310-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="ff310-114">Мы будет обсуждаться в этой серии руководств, все эти концепции и показать, как их использовать для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="ff310-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="ff310-115">Начнем с создания класса контроллера.</span><span class="sxs-lookup"><span data-stu-id="ff310-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="ff310-116">В **обозревателе решений**, щелкните правой кнопкой мыши *контроллеров* папку, а затем выберите **Добавление контроллера**.</span><span class="sxs-lookup"><span data-stu-id="ff310-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="ff310-117">Назовите новый контроллер &quot;HelloWorldController&quot;.</span><span class="sxs-lookup"><span data-stu-id="ff310-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="ff310-118">Оставьте как шаблон по умолчанию **пустой контроллер MVC** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff310-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![Добавление контроллера](adding-a-controller/_static/image2.png)

<span data-ttu-id="ff310-120">Обратите внимание, что в **обозревателе решений** что новый файл был создан именованный *HelloWorldController.cs*.</span><span class="sxs-lookup"><span data-stu-id="ff310-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="ff310-121">Файл открыт в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="ff310-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="ff310-122">Замените содержимое файла следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="ff310-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="ff310-123">Методы контроллера будет возвращена строка HTML, в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ff310-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="ff310-124">Контроллер называется `HelloWorldController` и первый способ называется `Index`.</span><span class="sxs-lookup"><span data-stu-id="ff310-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="ff310-125">Давайте вызвать его из браузера.</span><span class="sxs-lookup"><span data-stu-id="ff310-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="ff310-126">Запустите приложение (нажмите клавишу F5 или Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="ff310-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="ff310-127">В браузере, добавьте &quot;HelloWorld&quot; к пути в адресной строке.</span><span class="sxs-lookup"><span data-stu-id="ff310-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="ff310-128">(Например, на рисунке ниже, его `http://localhost:1234/HelloWorld.`) страница в браузере будет выглядеть как на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="ff310-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="ff310-129">В методе выше код вернул строку непосредственно.</span><span class="sxs-lookup"><span data-stu-id="ff310-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="ff310-130">Вы сказали, что система должна возвращать только некоторые HTML, как и!</span><span class="sxs-lookup"><span data-stu-id="ff310-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="ff310-131">ASP.NET MVC вызывает классы другой контроллер (и различных методов действий в них), в зависимости от входящего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ff310-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="ff310-132">Логику маршрутизации URL-адрес по умолчанию используется ASP.NET MVC использует формат следующим образом, чтобы определить, какой код для вызова:</span><span class="sxs-lookup"><span data-stu-id="ff310-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="ff310-133">Первая часть URL-адреса определяет класс контроллера для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ff310-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="ff310-134">Поэтому */HelloWorld* сопоставляется `HelloWorldController` класса.</span><span class="sxs-lookup"><span data-stu-id="ff310-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="ff310-135">Вторая часть URL-адреса определяет метод действия к классу для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ff310-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="ff310-136">Поэтому */HelloWorld/индекс* вызовет `Index` метод `HelloWorldController` класс для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ff310-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="ff310-137">Обратите внимание, что нам пришлось перейдите к */HelloWorld* и `Index` метод использовался по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ff310-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="ff310-138">Это обусловлено тем, метод с именем `Index` является методом по умолчанию, который будет вызываться на контроллере, если тип не задан явным образом.</span><span class="sxs-lookup"><span data-stu-id="ff310-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="ff310-139">Перейдите по адресу `http://localhost:xxxx/HelloWorld/Welcome`.</span><span class="sxs-lookup"><span data-stu-id="ff310-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="ff310-140">`Welcome` Метод запускается и возвращает строку &quot;метод приветствия действие... &quot;.</span><span class="sxs-lookup"><span data-stu-id="ff310-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="ff310-141">MVC по умолчанию осуществляется сопоставление `/[Controller]/[ActionName]/[Parameters]`.</span><span class="sxs-lookup"><span data-stu-id="ff310-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="ff310-142">Для этого URL-адреса заданы контроллер `HelloWorld` и метод действия `Welcome`.</span><span class="sxs-lookup"><span data-stu-id="ff310-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="ff310-143">Часть URL-адреса `[Parameters]` на данный момент еще не использовалась.</span><span class="sxs-lookup"><span data-stu-id="ff310-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="ff310-144">Давайте немного изменить приведенный пример, чтобы передать сведения о параметрах из URL-адрес в контроллер (например, */HelloWorld/Welcome? имя = Скотт&amp;; numtimes = = 4*).</span><span class="sxs-lookup"><span data-stu-id="ff310-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="ff310-145">Изменение вашего `Welcome` метод включив два параметра, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ff310-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="ff310-146">Обратите внимание, что код использует функцию необязательного параметра C#, чтобы указать, что `numTimes` параметр должен по умолчанию 1, если не передаются значения для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="ff310-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="ff310-147">Запустите приложение и перейдите к пример URL-адреса (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span><span class="sxs-lookup"><span data-stu-id="ff310-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="ff310-148">Вы можете попробовать различные значения `name` и `numtimes` в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="ff310-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="ff310-149">[Система привязки модели ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) автоматически сопоставляет именованные параметры из строки запроса в адресной строке параметров метода.</span><span class="sxs-lookup"><span data-stu-id="ff310-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="ff310-150">В обоих этих примерах контроллер предоставляет &quot;VC&quot; модели MVC — то есть работу представления и контроллера.</span><span class="sxs-lookup"><span data-stu-id="ff310-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="ff310-151">Контроллер возвращает HTML напрямую.</span><span class="sxs-lookup"><span data-stu-id="ff310-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="ff310-152">Обычно это не требуется Возвращает HTML напрямую, поскольку в этом случае заметно усложняется написание кода.</span><span class="sxs-lookup"><span data-stu-id="ff310-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="ff310-153">Вместо этого мы обычно используем файл шаблона отдельное представление для создания HTML-ответа.</span><span class="sxs-lookup"><span data-stu-id="ff310-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="ff310-154">Давайте взглянем далее в том, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="ff310-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ff310-155">[Назад](intro-to-aspnet-mvc-4.md)
> [Вперед](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="ff310-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>