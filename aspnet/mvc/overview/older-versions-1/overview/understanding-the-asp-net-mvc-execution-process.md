---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Понимание процесса ASP.NET выполнения MVC (ru) Документы Майкрософт
author: rick-anderson
description: Узнайте, как ASP.NET mVC-платформа обрабатывает запрос браузера шаг за шагом.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541030"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="ae929-103">Общие сведения о процессе выполнения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ae929-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="ae929-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ae929-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ae929-105">Узнайте, как ASP.NET mVC-платформа обрабатывает запрос браузера шаг за шагом.</span><span class="sxs-lookup"><span data-stu-id="ae929-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="ae929-106">Запросы на ASP.NET веб-приложении на основе MVC сначала проходят через объект **UrlRoutingModule,** который является модулем HTTP.</span><span class="sxs-lookup"><span data-stu-id="ae929-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="ae929-107">Этот модуль анализирует запрос и выбирает маршрут.</span><span class="sxs-lookup"><span data-stu-id="ae929-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="ae929-108">Объект **UrlRoutingModule** выбирает первый объект маршрута, который соответствует текущему запросу.</span><span class="sxs-lookup"><span data-stu-id="ae929-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="ae929-109">(Объект маршрута — это класс, реализуемый **routeBase**и обычно который является экземпляром класса **Route.)** Если маршруты не совпадают, объект **UrlRoutingModule** ничего не делает и позволяет запросу вернуться к обычной обработке запроса ASP.NET или IIS.</span><span class="sxs-lookup"><span data-stu-id="ae929-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="ae929-110">Из выбранного объекта **Маршрута** объект **UrlRoutingModule** получает объект **IRouteHandler,** связанный с объектом **Маршрута.**</span><span class="sxs-lookup"><span data-stu-id="ae929-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="ae929-111">Как правило, в приложении MVC это будет экземпляр **MvcRouteHandler.**</span><span class="sxs-lookup"><span data-stu-id="ae929-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="ae929-112">Экземпляр **IRouteHandler** создает объект **IHttpHandler** и передает его **объектi IHttpContext.**</span><span class="sxs-lookup"><span data-stu-id="ae929-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="ae929-113">По умолчанию экземпляр **IHttpHandler** для MVC является объектом **MvcHandler.**</span><span class="sxs-lookup"><span data-stu-id="ae929-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="ae929-114">Затем объект **MvcHandler** выбирает контроллер, который в конечном итоге будет обрабатывать запрос.</span><span class="sxs-lookup"><span data-stu-id="ae929-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="ae929-115">Если веб-приложение ASP.NET на базе MVC запускается в IIS 7.0, для проектов MVC не требуется расширение имени файла.</span><span class="sxs-lookup"><span data-stu-id="ae929-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="ae929-116">В IIS 6.0 для обработки необходимо, чтобы расширение имени файла MVC было связано с библиотекой DLL ISAPI ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ae929-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="ae929-117">Модуль и обработчик являются точками входа в ASP.NET mVC.</span><span class="sxs-lookup"><span data-stu-id="ae929-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="ae929-118">Они отвечают за следующее:</span><span class="sxs-lookup"><span data-stu-id="ae929-118">They perform the following actions:</span></span>

- <span data-ttu-id="ae929-119">Выбор нужного контроллера в веб-приложении MVC.</span><span class="sxs-lookup"><span data-stu-id="ae929-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="ae929-120">Получение отдельного экземпляра контроллера.</span><span class="sxs-lookup"><span data-stu-id="ae929-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="ae929-121">Вызов **исчергивайте** метод выполнения контроллера.</span><span class="sxs-lookup"><span data-stu-id="ae929-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="ae929-122">Ниже перечислены этапы выполнения для проекта MVC Web:</span><span class="sxs-lookup"><span data-stu-id="ae929-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="ae929-123">Получение первого запроса к приложению.</span><span class="sxs-lookup"><span data-stu-id="ae929-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="ae929-124">В файле Global.asax объекты **маршрута** добавляются к объекту **RouteTable.**</span><span class="sxs-lookup"><span data-stu-id="ae929-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="ae929-125">Выполнение маршрутизации</span><span class="sxs-lookup"><span data-stu-id="ae929-125">Perform routing</span></span> 

    - <span data-ttu-id="ae929-126">Модуль **UrlRoutingModule** использует первый объект сопоставления **маршрута** в коллекции **RouteTable** для создания объекта **RouteData,** который он затем использует для создания объекта **RequestContext** **(IHttpContext).**</span><span class="sxs-lookup"><span data-stu-id="ae929-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="ae929-127">Создание обработчика запроса MVC</span><span class="sxs-lookup"><span data-stu-id="ae929-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="ae929-128">Объект **MvcRouteHandler** создает экземпляр класса **MvcHandler** и передает экземпляр экземпляра **RequestContext.**</span><span class="sxs-lookup"><span data-stu-id="ae929-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="ae929-129">Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="ae929-129">Create controller</span></span> 

    - <span data-ttu-id="ae929-130">Объект **MvcHandler** использует экземпляр **RequestContext** для идентификации объекта **IControllerFactory** (обычно экземпляра класса **DefaultControllerFactory)** для создания экземпляра контроллера.</span><span class="sxs-lookup"><span data-stu-id="ae929-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="ae929-131">Выполняет контроллер - экземпляр **MvcHandler** вызывает метод **выполнения** контроллера.</span><span class="sxs-lookup"><span data-stu-id="ae929-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="ae929-132">Вызов действия</span><span class="sxs-lookup"><span data-stu-id="ae929-132">Invoke action</span></span> 

    - <span data-ttu-id="ae929-133">Большинство контроллеров наследуют из базового класса **контроллера.**</span><span class="sxs-lookup"><span data-stu-id="ae929-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="ae929-134">Для контроллеров, которые делают это, объект **ControllerActionInvoker,** связанный с контроллером, определяет, какой метод действия класса контроллера вызывает, а затем вызывает этот метод.</span><span class="sxs-lookup"><span data-stu-id="ae929-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="ae929-135">Выполнение результата</span><span class="sxs-lookup"><span data-stu-id="ae929-135">Execute result</span></span> 

    - <span data-ttu-id="ae929-136">Типичный метод действия может получать пользовательский ввод, готовить соответствующие данные ответа, а затем выполнять результат, возвращая тип результата.</span><span class="sxs-lookup"><span data-stu-id="ae929-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="ae929-137">Встроенные типы результатов, которые могут быть выполнены, включают в себя следующие: **ViewResult** (который отображает представление и является наиболее часто используемым типом результата), **RedirectToRouteResult**, **RedirectResult,** **ContentResult**, **JsonResult**и **EmptyResult.**</span><span class="sxs-lookup"><span data-stu-id="ae929-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
