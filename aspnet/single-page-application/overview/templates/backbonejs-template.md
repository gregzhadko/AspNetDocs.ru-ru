---
uid: single-page-application/overview/templates/backbonejs-template
title: Шаблон backbone | Документация Майкрософт
author: madskristensen
description: Шаблон Backbone.js SPA
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 325c4f5370340b2e223521fada77cf0e78a67b5b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025241"
---
<a name="backbone-template"></a><span data-ttu-id="d15fb-103">Шаблон Backbone</span><span class="sxs-lookup"><span data-stu-id="d15fb-103">Backbone Template</span></span>
====================
<span data-ttu-id="d15fb-104">по [Мэдсом Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="d15fb-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="d15fb-105">Шаблон Backbone SPA было написано с Кази Манзур Рашид</span><span class="sxs-lookup"><span data-stu-id="d15fb-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="d15fb-106">Загрузить шаблон Backbone.js SPA</span><span class="sxs-lookup"><span data-stu-id="d15fb-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)


<span data-ttu-id="d15fb-107">Для начала работы, быстрого создания интерактивных клиентские веб-приложений с помощью предназначен данный шаблон Backbone.js SPA [Backbone.js.](http://backbonejs.org/)</span><span class="sxs-lookup"><span data-stu-id="d15fb-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="d15fb-108">Шаблон предоставляет начальной основу для разработки приложения Backbone.js в ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d15fb-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="d15fb-109">Изначально он предоставляет функции базового пользовательского входа в систему, включая сброс пароля регистрации, входа в систему пользователя и подтверждение пользователя с помощью шаблонов базовый адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="d15fb-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="d15fb-110">Требования:</span><span class="sxs-lookup"><span data-stu-id="d15fb-110">Requirements:</span></span>

- [<span data-ttu-id="d15fb-111">Обновление ASP.NET и веб-инструментами 2012.2</span><span class="sxs-lookup"><span data-stu-id="d15fb-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="d15fb-112">Создание проекта шаблона магистрали</span><span class="sxs-lookup"><span data-stu-id="d15fb-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="d15fb-113">Скачайте и установите шаблон, нажав кнопку "скачать" выше.</span><span class="sxs-lookup"><span data-stu-id="d15fb-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="d15fb-114">Шаблон упаковывается в формате Visual Studio Extension (VSIX).</span><span class="sxs-lookup"><span data-stu-id="d15fb-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="d15fb-115">Может потребоваться перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d15fb-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="d15fb-116">В **шаблоны** области выберите **установленные шаблоны** и разверните **Visual C#** узла.</span><span class="sxs-lookup"><span data-stu-id="d15fb-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="d15fb-117">В разделе **Visual C#** выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="d15fb-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="d15fb-118">В списке шаблонов проектов выберите **веб-приложение ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="d15fb-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="d15fb-119">Имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d15fb-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="d15fb-120">В **новый проект** мастера можно выбрать проект SPA Backbone.js.</span><span class="sxs-lookup"><span data-stu-id="d15fb-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="d15fb-121">Нажмите клавиши Ctrl-F5, чтобы построить и запустить приложение без отладки, или нажмите клавишу F5, чтобы запустить программу с отладкой.</span><span class="sxs-lookup"><span data-stu-id="d15fb-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="d15fb-122">Нажав кнопку «Моя учетная запись» можно открыть страницу входа:</span><span class="sxs-lookup"><span data-stu-id="d15fb-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="d15fb-123">Пошаговое руководство. Код клиента</span><span class="sxs-lookup"><span data-stu-id="d15fb-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="d15fb-124">Давайте начинается со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="d15fb-124">Let's starts with the client side.</span></span> <span data-ttu-id="d15fb-125">Сценарии приложений клиента находятся в папке ~/Scripts/application.</span><span class="sxs-lookup"><span data-stu-id="d15fb-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="d15fb-126">Приложение создается на языке [TypeScript](http://www.typescriptlang.org/) (TS-файлы) которые компилируются в код JavaScript (JS-файлов).</span><span class="sxs-lookup"><span data-stu-id="d15fb-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="d15fb-127">**Приложение**</span><span class="sxs-lookup"><span data-stu-id="d15fb-127">**Application**</span></span>

<span data-ttu-id="d15fb-128">`Application` определяется в application.ts.</span><span class="sxs-lookup"><span data-stu-id="d15fb-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="d15fb-129">Этот объект Инициализирует приложение и выступает в качестве корневого пространства имен.</span><span class="sxs-lookup"><span data-stu-id="d15fb-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="d15fb-130">Это обеспечивает сведения о конфигурации и состояния, который совместно используется приложение, например является ли пользователь выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="d15fb-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="d15fb-131">`application.start` Метод создает модальных представлений и присоединяет обработчики событий для события уровня приложения, например вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="d15fb-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="d15fb-132">Далее создается по умолчанию маршрутизатором и проверяет, задано ли любой URL-адрес на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="d15fb-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="d15fb-133">Если нет, он перенаправляет на URL-адрес по умолчанию (#! /).</span><span class="sxs-lookup"><span data-stu-id="d15fb-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="d15fb-134">**События**</span><span class="sxs-lookup"><span data-stu-id="d15fb-134">**Events**</span></span>

<span data-ttu-id="d15fb-135">События всегда важны, при разработке слабо связанными компонентами.</span><span class="sxs-lookup"><span data-stu-id="d15fb-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="d15fb-136">Приложения часто выполняют несколько операций в ответ на действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="d15fb-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="d15fb-137">Магистраль предоставляет встроенные события с компонентами, такими как модель, коллекции и представления.</span><span class="sxs-lookup"><span data-stu-id="d15fb-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="d15fb-138">Вместо создания зависимостей между среди этих компонентов, в шаблоне используется модель «pub/sub»: `events` Объект, определенный в events.ts, выступает в роли концентратора событий для публикации и подписки на события приложения.</span><span class="sxs-lookup"><span data-stu-id="d15fb-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="d15fb-139">`events` Объекта является единственным.</span><span class="sxs-lookup"><span data-stu-id="d15fb-139">The `events` object is a singleton.</span></span> <span data-ttu-id="d15fb-140">Ниже показано, как подписаться на событие и последующего инициирования события:</span><span class="sxs-lookup"><span data-stu-id="d15fb-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="d15fb-141">**Маршрутизатор**</span><span class="sxs-lookup"><span data-stu-id="d15fb-141">**Router**</span></span>

<span data-ttu-id="d15fb-142">В Backbone.js маршрутизатор предоставляет методы для маршрутизации страниц на стороне клиента и соединить их действия и события.</span><span class="sxs-lookup"><span data-stu-id="d15fb-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="d15fb-143">Шаблон определяет одним маршрутизатором, в router.ts.</span><span class="sxs-lookup"><span data-stu-id="d15fb-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="d15fb-144">Маршрутизатор создает activable представления и поддерживает состояние, при переключении представлений.</span><span class="sxs-lookup"><span data-stu-id="d15fb-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="d15fb-145">(В следующем разделе описываются представления activable.) Изначально проект имеет два представления фиктивный, Home и About.</span><span class="sxs-lookup"><span data-stu-id="d15fb-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="d15fb-146">Он также содержит представления не найдено, которая отображается в том случае, если маршрут не известен.</span><span class="sxs-lookup"><span data-stu-id="d15fb-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="d15fb-147">**Представления**</span><span class="sxs-lookup"><span data-stu-id="d15fb-147">**Views**</span></span>

<span data-ttu-id="d15fb-148">Представления определяются в ~/Scripts/application и представлений.</span><span class="sxs-lookup"><span data-stu-id="d15fb-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="d15fb-149">Существует два вида представления activable и представления модальное диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d15fb-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="d15fb-150">Activable представления вызываются маршрутизатором.</span><span class="sxs-lookup"><span data-stu-id="d15fb-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="d15fb-151">При отображении activable представление всех остальных activable представлений становятся неактивными.</span><span class="sxs-lookup"><span data-stu-id="d15fb-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="d15fb-152">Создание представления "activable", расширение представления с `Activable` объекта:</span><span class="sxs-lookup"><span data-stu-id="d15fb-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="d15fb-153">Расширение с помощью `Activable` добавляет два новых метода в представление `activate` и `deactivate`.</span><span class="sxs-lookup"><span data-stu-id="d15fb-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="d15fb-154">Маршрутизатор вызывает эти методы для активации и deactive представления.</span><span class="sxs-lookup"><span data-stu-id="d15fb-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="d15fb-155">Модальные представления реализуются как [Twitter Bootstrap](http://twitter.github.com/bootstrap/) создания дочерних модальных диалогов.</span><span class="sxs-lookup"><span data-stu-id="d15fb-155">Modal views are implemented as [Twitter Bootstrap](http://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="d15fb-156">`Membership` И `Profile` представления являются модальным.</span><span class="sxs-lookup"><span data-stu-id="d15fb-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="d15fb-157">Модели представления может быть инициировано любые события приложения.</span><span class="sxs-lookup"><span data-stu-id="d15fb-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="d15fb-158">Например, в `Navigation` показано представление, щелкнув ссылку «Моя учетная запись», либо `Membership` представления или `Profile` представление, в зависимости от того, вошел ли пользователь.</span><span class="sxs-lookup"><span data-stu-id="d15fb-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="d15fb-159">`Navigation` Вкладывает щелкните обработчики событий, чтобы все дочерние элементы, имеющие `data-command` атрибута.</span><span class="sxs-lookup"><span data-stu-id="d15fb-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="d15fb-160">Вот HTML-разметка:</span><span class="sxs-lookup"><span data-stu-id="d15fb-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="d15fb-161">Ниже приведен код в navigation.ts для подключения событий:</span><span class="sxs-lookup"><span data-stu-id="d15fb-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="d15fb-162">**Модели**</span><span class="sxs-lookup"><span data-stu-id="d15fb-162">**Models**</span></span>

<span data-ttu-id="d15fb-163">Модели определяются в ~/Scripts/application/моделей.</span><span class="sxs-lookup"><span data-stu-id="d15fb-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="d15fb-164">Все модели имеют три основных действия: атрибуты по умолчанию, правила проверки и конечную точку на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d15fb-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="d15fb-165">Вот типичный пример:</span><span class="sxs-lookup"><span data-stu-id="d15fb-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="d15fb-166">**Подключаемые модули**</span><span class="sxs-lookup"><span data-stu-id="d15fb-166">**Plug-ins**</span></span>

<span data-ttu-id="d15fb-167">Папка ~/Scripts/application/lib содержит несколько подключаемых модулей под рукой jQuery. В файле form.ts определяется подключаемый модуль для работы с данными формы.</span><span class="sxs-lookup"><span data-stu-id="d15fb-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="d15fb-168">Часто необходимо сериализовать или десериализовать данные формы и какие-либо ошибки проверки модели.</span><span class="sxs-lookup"><span data-stu-id="d15fb-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="d15fb-169">Подключаемый модуль form.ts содержит методы, такие как `serializeFields`, `deserializeFields`, и `showFieldErrors`.</span><span class="sxs-lookup"><span data-stu-id="d15fb-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="d15fb-170">В следующем примере показано, как сериализовать форму в модель.</span><span class="sxs-lookup"><span data-stu-id="d15fb-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="d15fb-171">Подключаемый модуль flashbar.ts предоставляет различные виды сообщений обратной связи для пользователя.</span><span class="sxs-lookup"><span data-stu-id="d15fb-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="d15fb-172">Методы являются `$.showSuccessbar`, `$.showErrorbar` и `$.showInfobar`.</span><span class="sxs-lookup"><span data-stu-id="d15fb-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="d15fb-173">На самом деле его используется для отображения хорошо анимированных сообщения оповещения Twitter Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d15fb-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="d15fb-174">Подключаемый модуль confirm.ts заменяет браузера подтверждения, несмотря на то, что API немного отличаются:</span><span class="sxs-lookup"><span data-stu-id="d15fb-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="d15fb-175">Пошаговое руководство. Серверный код</span><span class="sxs-lookup"><span data-stu-id="d15fb-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="d15fb-176">Теперь давайте взглянем на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d15fb-176">Now let's look at the server side.</span></span>

<span data-ttu-id="d15fb-177">**Контроллеры**</span><span class="sxs-lookup"><span data-stu-id="d15fb-177">**Controllers**</span></span>

<span data-ttu-id="d15fb-178">В одностраничное приложение сервер играет лишь малую роль в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d15fb-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="d15fb-179">Как правило сервер отображает начальную страницу и затем отправляет и получает данные JSON.</span><span class="sxs-lookup"><span data-stu-id="d15fb-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="d15fb-180">Этот шаблон содержит два контроллера MVC: `HomeController` отображает начальную страницу, и `SupportsController` используется для подтверждения новых учетных записей пользователей и сбрасывать пароли.</span><span class="sxs-lookup"><span data-stu-id="d15fb-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="d15fb-181">Все остальные контроллеры в шаблоне являются контроллерами веб-API ASP.NET, отправляющие и получающие данные JSON.</span><span class="sxs-lookup"><span data-stu-id="d15fb-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="d15fb-182">По умолчанию контроллеры используют новый `WebSecurity` классом для выполнения задач, связанных с пользователем.</span><span class="sxs-lookup"><span data-stu-id="d15fb-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="d15fb-183">Тем не менее они также имеют дополнительные конструкторы, которые позволяют передавать в делегаты для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="d15fb-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="d15fb-184">Это упрощает тестирование и позволяет заменить `WebSecurity` по-другому, используя контейнер IoC.</span><span class="sxs-lookup"><span data-stu-id="d15fb-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="d15fb-185">Пример:</span><span class="sxs-lookup"><span data-stu-id="d15fb-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="d15fb-186">Представления</span><span class="sxs-lookup"><span data-stu-id="d15fb-186">Views</span></span>

<span data-ttu-id="d15fb-187">Представления предназначены модульная структура: Каждый раздел страницы имеет свой собственный выделенный представление.</span><span class="sxs-lookup"><span data-stu-id="d15fb-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="d15fb-188">В одностраничное приложение довольно часто для включения, у которых нет любой соответствующий контроллер представления.</span><span class="sxs-lookup"><span data-stu-id="d15fb-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="d15fb-189">Представление можно включить путем вызова `@Html.Partial('myView')`, но это становится несколько занудным.</span><span class="sxs-lookup"><span data-stu-id="d15fb-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="d15fb-190">Чтобы облегчить эту задачу, шаблон определяет вспомогательный метод, `IncludeClientViews`, который выполняет визуализацию всех представлений в указанной папке:</span><span class="sxs-lookup"><span data-stu-id="d15fb-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="d15fb-191">Если имя папки не указан, по умолчанию папка называется «ClientViews».</span><span class="sxs-lookup"><span data-stu-id="d15fb-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="d15fb-192">Если представление вашего клиента также использует разделяемые представления, имя частичного представления с символа подчеркивания (например, `_SignUp`).</span><span class="sxs-lookup"><span data-stu-id="d15fb-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="d15fb-193">`IncludeClientViews` Метод исключает все представления, имена которых начинаются с символа подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="d15fb-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="d15fb-194">Чтобы включить частичное представление в представление клиента, вызовите `Html.ClientView('SignUp')` вместо `Html.Partial('_SignUp')`.</span><span class="sxs-lookup"><span data-stu-id="d15fb-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="d15fb-195">**Отправка сообщения электронной почты**</span><span class="sxs-lookup"><span data-stu-id="d15fb-195">**Sending Email**</span></span>

<span data-ttu-id="d15fb-196">Для отправки электронной почты, в шаблоне используется [почтовой](http://aboutcode.net/postal).</span><span class="sxs-lookup"><span data-stu-id="d15fb-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="d15fb-197">Тем не менее, абстрагируется от остальной части кода с помощью почтовой `IMailer` интерфейс, поэтому вы можете легко заменить с другой реализацией.</span><span class="sxs-lookup"><span data-stu-id="d15fb-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="d15fb-198">Шаблоны сообщений электронной почты, находятся в папке представления или сообщений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="d15fb-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="d15fb-199">Адрес электронной почты отправителя указан в файле web.config в `sender.email` ключ **appSettings** раздел.</span><span class="sxs-lookup"><span data-stu-id="d15fb-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="d15fb-200">Кроме того, когда `debug="true"` в файле web.config, приложение не требует подтверждения электронной почты пользователя, для ускорения разработки.</span><span class="sxs-lookup"><span data-stu-id="d15fb-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="d15fb-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="d15fb-201">GitHub</span></span>

<span data-ttu-id="d15fb-202">Можно также найти шаблон Backbone.js SPA на [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span><span class="sxs-lookup"><span data-stu-id="d15fb-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>