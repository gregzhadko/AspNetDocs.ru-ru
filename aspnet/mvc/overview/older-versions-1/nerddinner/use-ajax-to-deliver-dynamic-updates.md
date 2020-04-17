---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Используйте AJAX для предоставления динамических обновлений (ru) Документы Майкрософт
author: rick-anderson
description: Шаг 10 реализует поддержку для зарегистрированных пользователей RSVP их интерес к посещению ужина, используя Ajax основе подхода, интегрированного в деталях ужина ...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541251"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="c65eb-103">Использование AJAX для доставки динамических обновлений</span><span class="sxs-lookup"><span data-stu-id="c65eb-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="c65eb-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c65eb-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c65eb-105">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="c65eb-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c65eb-106">Это шаг 10 бесплатно ["NerdDinner" приложение учебник,](introducing-the-nerddinner-tutorial.md) который ходит через как построить небольшой, но полный, веб-приложение с помощью ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="c65eb-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c65eb-107">Шаг 10 реализует поддержку для зарегистрированных пользователей RSVP их интерес к посещению ужина, используя Ajax основе подхода, интегрированного в странице детали ужина.</span><span class="sxs-lookup"><span data-stu-id="c65eb-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="c65eb-108">Если вы используете ASP.NET MVC 3, мы рекомендуем вам следовать [начиная с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.</span><span class="sxs-lookup"><span data-stu-id="c65eb-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="c65eb-109">NerdDinner Шаг 10: AJAX Включение RSVPs принимает</span><span class="sxs-lookup"><span data-stu-id="c65eb-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="c65eb-110">Теперь давайте реализуем поддержку для зарегистрированных пользователей RSVP их интерес к посещению ужина.</span><span class="sxs-lookup"><span data-stu-id="c65eb-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="c65eb-111">Мы включим это с помощью подхода, основанного на AJAX, интегрированном на странице деталей ужина.</span><span class="sxs-lookup"><span data-stu-id="c65eb-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="c65eb-112">Указание того, является ли пользователь RSVP'd</span><span class="sxs-lookup"><span data-stu-id="c65eb-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="c65eb-113">Пользователи могут посетить */Ужины / Подробная информация /* URL-адрес, чтобы увидеть подробную информацию о конкретном ужине:</span><span class="sxs-lookup"><span data-stu-id="c65eb-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="c65eb-114">Метод действия «Подробности() реализован так:</span><span class="sxs-lookup"><span data-stu-id="c65eb-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="c65eb-115">Наш первый шаг к реализации поддержки RSVP будет добавить "IsUserRegistered (имя пользователя) " вспомогательный метод для нашего объекта ужин (в пределах Dinner.cs частичного класса мы построили ранее).</span><span class="sxs-lookup"><span data-stu-id="c65eb-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="c65eb-116">Этот метод помощника возвращает сярвые или ложные в зависимости от того, является ли пользователь в настоящее время RSVP'd для ужина:</span><span class="sxs-lookup"><span data-stu-id="c65eb-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="c65eb-117">Затем мы можем добавить следующий код в наш шаблон представления Details.aspx для отображения соответствующего сообщения с указанием того, зарегистрирован пользователь или нет для события:</span><span class="sxs-lookup"><span data-stu-id="c65eb-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="c65eb-118">И теперь, когда пользователь посещает ужин они зарегистрированы они будут видеть это сообщение:</span><span class="sxs-lookup"><span data-stu-id="c65eb-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="c65eb-119">И когда они посещают ужин они не зарегистрированы, потому что они увидят ниже сообщение:</span><span class="sxs-lookup"><span data-stu-id="c65eb-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="c65eb-120">Внедрение метода действий в регистрах</span><span class="sxs-lookup"><span data-stu-id="c65eb-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="c65eb-121">Теперь давайте добавим функциональность, необходимую для того, чтобы пользователи могли включить RSVP на ужин со страницы деталей.</span><span class="sxs-lookup"><span data-stu-id="c65eb-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="c65eb-122">Для реализации этого мы создадим новый класс "RSVPController", нажав на каталог&gt;"Контролеры" и выбрав команду меню Add- Controller.</span><span class="sxs-lookup"><span data-stu-id="c65eb-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="c65eb-123">Мы реализуем метод действий «Регистрация» в новом классе RSVPController, который принимает идентификатор для ужина в качестве аргумента, извлекаем соответствующий объект Ужина, проверяем, находится ли в настоящее время в списке пользователей, зарегистрировавшихся для него, и если не добавляет для него объект RSVP:</span><span class="sxs-lookup"><span data-stu-id="c65eb-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="c65eb-124">Обратите внимание выше, как мы возвращаем простую строку в качестве вывода метода действия.</span><span class="sxs-lookup"><span data-stu-id="c65eb-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="c65eb-125">Мы могли бы встроить это сообщение в шаблон представления, но так как оно настолько мало, мы просто используем метод помощника Content () на базовом классе контроллера и вернем строку сообщение, как выше.</span><span class="sxs-lookup"><span data-stu-id="c65eb-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="c65eb-126">Вызов метода действий RSVPForEvent с помощью AJAX</span><span class="sxs-lookup"><span data-stu-id="c65eb-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="c65eb-127">Мы будем использовать AJAX для использования метода действий Регистра из нашего представления «Подробности».</span><span class="sxs-lookup"><span data-stu-id="c65eb-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="c65eb-128">Реализация этого довольно проста.</span><span class="sxs-lookup"><span data-stu-id="c65eb-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="c65eb-129">Сначала мы добавим две ссылки на библиотеку сценариев:</span><span class="sxs-lookup"><span data-stu-id="c65eb-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="c65eb-130">Первая библиотека ссылается на ядро ASP.NET библиотеке сценариев клиентов AJAX.</span><span class="sxs-lookup"><span data-stu-id="c65eb-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="c65eb-131">Этот файл приблизительно 24k в размере (сжатого) и содержит основные клиент-стороны AJAX функциональность.</span><span class="sxs-lookup"><span data-stu-id="c65eb-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="c65eb-132">Вторая библиотека содержит функции утилиты, которые интегрируются со встроенными методами помощи ASP.NET MVC (которые мы будем использовать в ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="c65eb-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="c65eb-133">Затем мы можем обновить код шаблона представления, который мы добавили ранее, чтобы вместо ввода сообщения "Вы не зарегистрированы для этого события", мы вместо этого отображаем ссылку, которая при нажатии выполняет вызов AJAX, который вызывает наш метод действий RSVPForEvent на нашем контроллере RSVP и RSVPs пользователя:</span><span class="sxs-lookup"><span data-stu-id="c65eb-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="c65eb-134">Метод помощника Ajax.ActionLink() используется выше, является встроенным ASP.NET MVC и похож на метод помощника Html.ActionLink() за исключением того, что вместо выполнения стандартной навигации он делает звонок AJAX к методу действия при нажатии ссылки.</span><span class="sxs-lookup"><span data-stu-id="c65eb-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="c65eb-135">Выше мы называем "Регистрация" метод действия на контроллере "RSVP" и передачи DinnerID как "id" параметр к нему.</span><span class="sxs-lookup"><span data-stu-id="c65eb-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="c65eb-136">Окончательный параметр AjaxOptions, который мы перебираем, указывает на то, &lt;&gt; что мы хотим взять содержимое, возвращенное из метода действия, и обновить элемент HTML div на странице, идентификатор которой является "rsvpmsg".</span><span class="sxs-lookup"><span data-stu-id="c65eb-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="c65eb-137">И теперь, когда пользователь просматривает на обед они не зарегистрированы еще они увидят ссылку на RSVP для него:</span><span class="sxs-lookup"><span data-stu-id="c65eb-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="c65eb-138">Если они нажимают на ссылку "RSVP для этого события", они вызовут AJAX методдействия Регистра на контроллере RSVP, и когда он завершится, они увидят обновленное сообщение, как ниже:</span><span class="sxs-lookup"><span data-stu-id="c65eb-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="c65eb-139">Пропускная способность сети и трафик, участвующих при принятии этого вызова AJAX действительно легкий.</span><span class="sxs-lookup"><span data-stu-id="c65eb-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="c65eb-140">Когда пользователь нажимает на ссылку "RSVP для этого события", небольшой запрос сети HTTP POST на */Dinners/Register/1* URL, который выглядит ниже на проводе:</span><span class="sxs-lookup"><span data-stu-id="c65eb-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="c65eb-141">И ответ от нашего метода действий Регистра просто:</span><span class="sxs-lookup"><span data-stu-id="c65eb-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="c65eb-142">Этот легкий вызов быстро и будет работать даже над медленной сети.</span><span class="sxs-lookup"><span data-stu-id="c65eb-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="c65eb-143">Добавление анимации j'ери</span><span class="sxs-lookup"><span data-stu-id="c65eb-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="c65eb-144">Функциональность AJAX, которая мы реализовали, работает хорошо и быстро.</span><span class="sxs-lookup"><span data-stu-id="c65eb-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="c65eb-145">Иногда это может произойти так быстро, однако, что пользователь может не заметить, что ссылка RSVP была заменена новым текстом.</span><span class="sxs-lookup"><span data-stu-id="c65eb-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="c65eb-146">Чтобы сделать результат немного более очевидным, мы можем добавить простую анимацию, чтобы привлечь внимание к сообщению об обновлении.</span><span class="sxs-lookup"><span data-stu-id="c65eb-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="c65eb-147">Шаблон проекта MVC ASP.NET по умолчанию включает в себя j'ery – отличную (и очень популярную) библиотеку JavaScript с открытым исходным кодом, которая также поддерживается корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c65eb-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="c65eb-148">j's'еry предоставляет ряд функций, в том числе хороший HTML DOM выбор и эффекты библиотеки.</span><span class="sxs-lookup"><span data-stu-id="c65eb-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="c65eb-149">Для использования j'we'ry мы сначала добавим ссылку на сценарий к нему.</span><span class="sxs-lookup"><span data-stu-id="c65eb-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="c65eb-150">Поскольку мы будем использовать j'ery в различных местах на нашем сайте, мы добавим ссылку на сценарий в нашем файле Master Master master page, чтобы все страницы могли использовать его.</span><span class="sxs-lookup"><span data-stu-id="c65eb-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="c65eb-151">*Совет: убедитесь, что вы установили JavaScript intellisense hotfix для VS 2008 SP1, который позволяет более богатую поддержку интеллекта для файлов JavaScript (в том числе j'ery). Вы можете скачать его из:http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="c65eb-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="c65eb-152">Код, написанный с помощью J'ery, часто использует глобальный метод JavaScript «$.)», который извлекает один или несколько HTML элементов с помощью селектора CSS.</span><span class="sxs-lookup"><span data-stu-id="c65eb-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="c65eb-153">Например, *$("#rsvpmsg")* выбирает любой html элемент с идом rsvpmsg, в то время как *$("something")* будет выбирать все элементы с "что-то" имя класса CSS.</span><span class="sxs-lookup"><span data-stu-id="c65eb-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="c65eb-154">Вы также можете написать более продвинутые запросы, такие как "вернуть все проверенные радиокнопки" с помощью запроса селектора, как: *$("вход"@type(радио)@checked*.</span><span class="sxs-lookup"><span data-stu-id="c65eb-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="c65eb-155">После того как вы выбрали элементы, вы можете вызвать методы на них принять меры, как их сокрытие: *$("#rsvpmsg") скрыть();;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;*</span><span class="sxs-lookup"><span data-stu-id="c65eb-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="c65eb-156">Для нашего сценария RSVP мы определим простую функцию JavaScript под названием "AnimateRSVPMessage", которая выбирает div "rsvpmsg" &lt;&gt; и оживляет размер его текстового содержимого.</span><span class="sxs-lookup"><span data-stu-id="c65eb-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="c65eb-157">Ниже код запускает текст небольшой, а затем вызывает его увеличение в течение 400 миллисекунд таймфрейм:</span><span class="sxs-lookup"><span data-stu-id="c65eb-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="c65eb-158">Затем мы можем просунуть эту функцию JavaScript, которая будет вызвана после того, как наш вызов AJAX успешно завершается, передав свое имя нашему методу помощника Ajax.ActionLink() (через свойство события AjaxOptions "OnSuccess"):</span><span class="sxs-lookup"><span data-stu-id="c65eb-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="c65eb-159">И теперь, когда "RSVP для этого события" ссылка нажата и наш вызов AJAX завершаетуспешно, содержание сообщения, отправленного обратно будет анимировать и расти большой:</span><span class="sxs-lookup"><span data-stu-id="c65eb-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="c65eb-160">Помимо предоставления события «OnSuccess», объект AjaxOptions предоставляет события OnBegin, OnFailure и OnComplete, которые можно обрабатывать (наряду с множеством других свойств и полезных опций).</span><span class="sxs-lookup"><span data-stu-id="c65eb-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="c65eb-161">Очистка - Рефактор из RSVP Частичное представление</span><span class="sxs-lookup"><span data-stu-id="c65eb-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="c65eb-162">Наш шаблон представления деталей начинает получать немного долго, что сверхурочно сделает его немного сложнее понять.</span><span class="sxs-lookup"><span data-stu-id="c65eb-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="c65eb-163">Чтобы улучшить читаемость кода, давайте закончим, создав частичное представление - RSVPStatus.ascx - который инкапсулирует весь код представления RSVP для нашей страницы детали.</span><span class="sxs-lookup"><span data-stu-id="c65eb-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="c65eb-164">Мы можем сделать это, нажав правой кнопкой мыши на&gt;папке «Виды» (Просмотры) и выбрать команду меню Add- View.</span><span class="sxs-lookup"><span data-stu-id="c65eb-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="c65eb-165">Мы будем иметь его принять Ужин объект, как его сильно типом ViewModel.</span><span class="sxs-lookup"><span data-stu-id="c65eb-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="c65eb-166">Затем мы можем скопировать/ вставить содержимое RSVP из нашего просмотра Details.aspx в него.</span><span class="sxs-lookup"><span data-stu-id="c65eb-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="c65eb-167">После того как мы сделали это, давайте также создать еще один частичный вид - EditAndDeleteLinks.ascx - что инкапсулирует наш код представления ссылки и отсечения.</span><span class="sxs-lookup"><span data-stu-id="c65eb-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="c65eb-168">Мы также будем иметь его принять ужин объект, как его сильно типизированных ViewModel, и копировать / вставить логику edit и удалить из нашего Просмотра Details.aspx в него.</span><span class="sxs-lookup"><span data-stu-id="c65eb-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="c65eb-169">Наш шаблон представления деталей может включать в себя только два вызова html.RenderPartial() метода внизу:</span><span class="sxs-lookup"><span data-stu-id="c65eb-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="c65eb-170">Это делает код чище для чтения и обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c65eb-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="c65eb-171">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="c65eb-171">Next Step</span></span>

<span data-ttu-id="c65eb-172">Давайте теперь рассмотрим, как мы можем использовать AJAX еще дальше и добавить интерактивную поддержку отображения в наше приложение.</span><span class="sxs-lookup"><span data-stu-id="c65eb-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c65eb-173">[Назад](secure-applications-using-authentication-and-authorization.md)
> [Вперед](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="c65eb-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
