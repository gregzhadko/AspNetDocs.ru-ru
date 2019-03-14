---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Создание конечной точки OData v3 с веб-API 2 | Документация Майкрософт
author: MikeWasson
description: Open Data Protocol (OData) — это протокол доступа к данным веб-приложений. OData предоставляет универсальный способ структуру данных, запроса данных и работы с данными...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 2e0d3b45fd51192d227d852dc2f05b45ca42944c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031201"
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="d1158-104">Создание конечной точки OData v3 с веб-API 2</span><span class="sxs-lookup"><span data-stu-id="d1158-104">Creating an OData v3 Endpoint with Web API 2</span></span>
====================
<span data-ttu-id="d1158-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d1158-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d1158-106">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="d1158-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="d1158-107">[Open Data Protocol](http://www.odata.org/) (OData) — это протокол доступа к данным веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d1158-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="d1158-108">OData предоставляет универсальный способ структуру данных, запрашивать данные и манипулировать набором данных с помощью операций CRUD (Создание, чтение, обновление и удаление).</span><span class="sxs-lookup"><span data-stu-id="d1158-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="d1158-109">OData поддерживает форматы JSON и AtomPub (XML).</span><span class="sxs-lookup"><span data-stu-id="d1158-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="d1158-110">OData также определяет способ получения доступа к метаданным о данных.</span><span class="sxs-lookup"><span data-stu-id="d1158-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="d1158-111">Клиенты могут использовать метаданные для обнаружения сведений о типе и связи для набора данных.</span><span class="sxs-lookup"><span data-stu-id="d1158-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="d1158-112">Веб-API ASP.NET позволяет легко создать конечную точку OData для набора данных.</span><span class="sxs-lookup"><span data-stu-id="d1158-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="d1158-113">Вы можете контролировать, поддерживаемые конечной точкой точно, какие операции OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="d1158-114">Вы можете разместить несколько конечных точек OData, вместе с конечными точками не OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="d1158-115">У вас есть полный контроль над вашей модели данных, серверной части бизнес-логики и уровень данных.</span><span class="sxs-lookup"><span data-stu-id="d1158-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d1158-116">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="d1158-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="d1158-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d1158-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="d1158-118">Веб-API 2</span><span class="sxs-lookup"><span data-stu-id="d1158-118">Web API 2</span></span>
> - <span data-ttu-id="d1158-119">OData версии 3</span><span class="sxs-lookup"><span data-stu-id="d1158-119">OData Version 3</span></span>
> - <span data-ttu-id="d1158-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d1158-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="d1158-121">Fiddler веб-отладки, прокси-сервера (необязательно)</span><span class="sxs-lookup"><span data-stu-id="d1158-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="d1158-122">В добавлена поддержка Web API OData [ASP.NET и веб-инструменты 2012.2 обновление](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="d1158-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="d1158-123">Тем не менее в этом руководстве используется формирование шаблонов, который был добавлен в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d1158-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>


<span data-ttu-id="d1158-124">В этом руководстве вы создадите простой конечной точки OData, который клиенты могут выполнять запросы.</span><span class="sxs-lookup"><span data-stu-id="d1158-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="d1158-125">Кроме того, будет создан клиент C# для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d1158-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="d1158-126">После завершения этого учебника, следующий набор учебных курсов показано, как добавить дополнительные функциональные возможности, включая отношений сущностей, действия, и выберите развернуть $/ $.</span><span class="sxs-lookup"><span data-stu-id="d1158-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="d1158-127">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1158-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="d1158-128">Добавьте модель EDM</span><span class="sxs-lookup"><span data-stu-id="d1158-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="d1158-129">Добавить контроллер OData</span><span class="sxs-lookup"><span data-stu-id="d1158-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="d1158-130">Добавьте модель EDM и маршрута</span><span class="sxs-lookup"><span data-stu-id="d1158-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="d1158-131">Заполнение базы данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="d1158-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="d1158-132">Изучение конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="d1158-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="d1158-133">Форматы сериализации OData</span><span class="sxs-lookup"><span data-stu-id="d1158-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="d1158-134">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1158-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="d1158-135">В этом руководстве вы создадите конечную точку OData, которая поддерживает основные операции CRUD.</span><span class="sxs-lookup"><span data-stu-id="d1158-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="d1158-136">Конечная точка будет предоставлять один ресурс, список продуктов.</span><span class="sxs-lookup"><span data-stu-id="d1158-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="d1158-137">Последующих руководствах будут добавлены дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="d1158-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="d1158-138">Запустите Visual Studio и выберите **новый проект** с начальной страницы.</span><span class="sxs-lookup"><span data-stu-id="d1158-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="d1158-139">Или с **файл** меню, выберите **New** и затем **проекта**.</span><span class="sxs-lookup"><span data-stu-id="d1158-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="d1158-140">В **шаблоны** области выберите **установленные шаблоны** и разверните узел Visual C#.</span><span class="sxs-lookup"><span data-stu-id="d1158-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="d1158-141">В разделе **Visual C#** выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="d1158-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="d1158-142">Выберите **веб-приложение ASP.NET** шаблона.</span><span class="sxs-lookup"><span data-stu-id="d1158-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="d1158-143">В **новый проект ASP.NET** диалоговом окне выберите **пустой** шаблона.</span><span class="sxs-lookup"><span data-stu-id="d1158-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="d1158-144">В разделе &quot;добавить папки и основные ссылки для... &quot;, проверьте **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="d1158-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="d1158-145">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d1158-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="d1158-146">Добавьте модель EDM</span><span class="sxs-lookup"><span data-stu-id="d1158-146">Add an Entity Model</span></span>

<span data-ttu-id="d1158-147">*Модель* — это объект, представляющий данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="d1158-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="d1158-148">В этом учебнике мы должны модель, которая представляет продукт.</span><span class="sxs-lookup"><span data-stu-id="d1158-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="d1158-149">Соответствует модели тип сущности OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="d1158-150">В обозревателе решений щелкните правой кнопкой мыши папку Models.</span><span class="sxs-lookup"><span data-stu-id="d1158-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="d1158-151">В контекстном меню выберите **добавить** выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="d1158-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="d1158-152">В **Add New** товара диалоговое окно, назовите класс &quot;продукта&quot;.</span><span class="sxs-lookup"><span data-stu-id="d1158-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="d1158-153">По соглашению классы моделей, помещаются в папку Models.</span><span class="sxs-lookup"><span data-stu-id="d1158-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="d1158-154">У вас нет следуют соглашению в своих собственных проектах. Однако мы будем использовать в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="d1158-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>


<span data-ttu-id="d1158-155">В файле добавьте следующее определение класса:</span><span class="sxs-lookup"><span data-stu-id="d1158-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="d1158-156">Свойство ID будет ключ сущности.</span><span class="sxs-lookup"><span data-stu-id="d1158-156">The ID property will be the entity key.</span></span> <span data-ttu-id="d1158-157">Клиенты могут запрашивать продуктов по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="d1158-157">Clients can query products by ID.</span></span> <span data-ttu-id="d1158-158">Это поле также будет первичного ключа в базе данных серверной части.</span><span class="sxs-lookup"><span data-stu-id="d1158-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="d1158-159">Теперь выполните сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="d1158-159">Build the project now.</span></span> <span data-ttu-id="d1158-160">В следующем шаге мы будем использовать некоторые формирования шаблонов Visual Studio, который использует отражение для поиска типа продукта.</span><span class="sxs-lookup"><span data-stu-id="d1158-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="d1158-161">Добавить контроллер OData</span><span class="sxs-lookup"><span data-stu-id="d1158-161">Add an OData Controller</span></span>

<span data-ttu-id="d1158-162">Объект *контроллера* является классом, который обрабатывает HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="d1158-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="d1158-163">Вы определяете отдельный контроллер для каждого набора сущностей в вы службы OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="d1158-164">В этом руководстве мы создадим один контроллер.</span><span class="sxs-lookup"><span data-stu-id="d1158-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="d1158-165">В обозревателе решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="d1158-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="d1158-166">Выберите **добавить** , а затем выберите **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="d1158-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="d1158-167">В **Добавление шаблона** диалоговом окне выберите &quot;контроллер Web API 2 OData с действиями, использующий Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="d1158-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="d1158-168">В **Добавление контроллера** диалоговое окно, имя контроллера «ProductsController».</span><span class="sxs-lookup"><span data-stu-id="d1158-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="d1158-169">Выберите &quot;использовать асинхронные действия контроллера&quot; флажок.</span><span class="sxs-lookup"><span data-stu-id="d1158-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="d1158-170">В **модели** раскрывающегося списка выберите класс Product.</span><span class="sxs-lookup"><span data-stu-id="d1158-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="d1158-171">Нажмите кнопку **новый контекст данных...**  кнопки.</span><span class="sxs-lookup"><span data-stu-id="d1158-171">Click the **New data context...** button.</span></span> <span data-ttu-id="d1158-172">Оставьте имя по умолчанию для типа контекста данных и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="d1158-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="d1158-173">В диалоговом окне "Добавление контроллера" Добавление контроллера нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="d1158-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="d1158-174">Примечание. Если вы получаете сообщение об ошибке &quot;произошла ошибка при получении тип... &quot;, убедитесь, что вы создали проект Visual Studio после добавления к классу продукта.</span><span class="sxs-lookup"><span data-stu-id="d1158-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="d1158-175">Формирование шаблонов использует отражение для поиска класса.</span><span class="sxs-lookup"><span data-stu-id="d1158-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="d1158-176">Формирование шаблонов добавляет в проект два файла кода:</span><span class="sxs-lookup"><span data-stu-id="d1158-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="d1158-177">Products.cs определяет контроллер Web API, который реализует конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="d1158-178">ProductServiceContext.cs предоставляет методы для запроса основной базе данных, использующий Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d1158-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="d1158-179">Добавьте модель EDM и маршрута</span><span class="sxs-lookup"><span data-stu-id="d1158-179">Add the EDM and Route</span></span>

<span data-ttu-id="d1158-180">В обозревателе решений, разверните приложение\_запустите папку и откройте файл WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="d1158-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="d1158-181">Этот класс содержит код конфигурации для веб-API.</span><span class="sxs-lookup"><span data-stu-id="d1158-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="d1158-182">Замените этот код следующим:</span><span class="sxs-lookup"><span data-stu-id="d1158-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="d1158-183">Этот код делает две вещи:</span><span class="sxs-lookup"><span data-stu-id="d1158-183">This code does two things:</span></span>

- <span data-ttu-id="d1158-184">Создает Entity Data Model (EDM) для конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="d1158-185">Добавляет маршрут для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d1158-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="d1158-186">EDM является абстрактной моделью данных.</span><span class="sxs-lookup"><span data-stu-id="d1158-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="d1158-187">Модель EDM используется для создания документа метаданных и определения URI для службы.</span><span class="sxs-lookup"><span data-stu-id="d1158-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="d1158-188">**ODataConventionModelBuilder** создает EDM, используя набор соглашений об именовании по умолчанию модели EDM.</span><span class="sxs-lookup"><span data-stu-id="d1158-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="d1158-189">Этот подход требует наименьшего объема кода.</span><span class="sxs-lookup"><span data-stu-id="d1158-189">This approach requires the least code.</span></span> <span data-ttu-id="d1158-190">Если требуется больший контроль над модели EDM, можно использовать **ODataModelBuilder** класс, чтобы создать модель EDM путем добавления свойств, разделов и свойств навигации явным образом.</span><span class="sxs-lookup"><span data-stu-id="d1158-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="d1158-191">**EntitySet** метод добавляет в модель EDM набор сущностей:</span><span class="sxs-lookup"><span data-stu-id="d1158-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="d1158-192">Строка «Продукты» определяет имя набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="d1158-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="d1158-193">Имя контроллера должно соответствовать имени набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="d1158-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="d1158-194">В этом руководстве набор сущностей, который называется «Продукты» и именем контроллера `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="d1158-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="d1158-195">Если вы с именем «ProductSet» набора сущностей, следует присвоить имя контроллера `ProductSetController`.</span><span class="sxs-lookup"><span data-stu-id="d1158-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="d1158-196">Обратите внимание на то, что конечная точка может иметь несколько наборов сущностей.</span><span class="sxs-lookup"><span data-stu-id="d1158-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="d1158-197">Вызовите **EntitySet&lt;T&gt;**  для каждой сущности, установить, а затем определить соответствующий контроллер.</span><span class="sxs-lookup"><span data-stu-id="d1158-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="d1158-198">**MapODataRoute** метод добавляет маршрут для конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="d1158-199">Первый параметр — это понятное имя для маршрута.</span><span class="sxs-lookup"><span data-stu-id="d1158-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="d1158-200">Клиенты службы, это имя не отображается.</span><span class="sxs-lookup"><span data-stu-id="d1158-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="d1158-201">Второй параметр — префикс URI для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d1158-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="d1158-202">Учитывая этот код, URI для набора сущностей Products — http://<em>hostname</em>  /odata/продуктов.</span><span class="sxs-lookup"><span data-stu-id="d1158-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="d1158-203">Приложение может иметь более одной конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="d1158-204">Для каждой конечной точки, вызовите <strong>MapODataRoute</strong> и укажите уникальное имя маршрута и уникальный префикс URI.</span><span class="sxs-lookup"><span data-stu-id="d1158-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="d1158-205">Заполнение базы данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="d1158-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="d1158-206">На этом шаге используется Entity Framework для инициализации базы данных с некоторые тестовые данные.</span><span class="sxs-lookup"><span data-stu-id="d1158-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="d1158-207">Этот шаг является необязательным, но вы можете сразу тестирование конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="d1158-208">Из **средства** меню, выберите **диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="d1158-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d1158-209">В окне консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d1158-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="d1158-210">Это добавляет папку с именем миграций и файл кода Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="d1158-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="d1158-211">Откройте этот файл и добавьте следующий код, чтобы `Configuration.Seed` метод.</span><span class="sxs-lookup"><span data-stu-id="d1158-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="d1158-212">В окне консоли диспетчера пакетов введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d1158-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="d1158-213">Эти команды создают код, который создает базу данных, а затем выполняет этот код.</span><span class="sxs-lookup"><span data-stu-id="d1158-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="d1158-214">Изучение конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="d1158-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="d1158-215">В этом разделе мы будем использовать [Fiddler Web Debugging Proxy](http://www.fiddler2.com) для отправки запросов к конечной точке и изучения ответные сообщения.</span><span class="sxs-lookup"><span data-stu-id="d1158-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="d1158-216">Это поможет вам понять возможности конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="d1158-217">В Visual Studio нажмите клавишу F5, чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="d1158-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="d1158-218">По умолчанию Visual Studio открывает браузер `http://localhost:*port*`, где *порт* — номер порта, настроенный в параметрах проекта.</span><span class="sxs-lookup"><span data-stu-id="d1158-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="d1158-219">Можно изменить номер порта в параметрах проекта.</span><span class="sxs-lookup"><span data-stu-id="d1158-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="d1158-220">В обозревателе решений щелкните правой кнопкой мыши проект и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="d1158-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="d1158-221">В окне «Свойства» выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="d1158-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="d1158-222">Введите номер порта в разделе **URL-адрес проекта**.</span><span class="sxs-lookup"><span data-stu-id="d1158-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="d1158-223">Сервисный документ</span><span class="sxs-lookup"><span data-stu-id="d1158-223">Service Document</span></span>

<span data-ttu-id="d1158-224">*Сервисный документ* содержит список наборов сущностей для конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="d1158-225">Чтобы получить Сервисный документ, отправьте запрос GET к корневому URI службы.</span><span class="sxs-lookup"><span data-stu-id="d1158-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="d1158-226">С помощью Fiddler, введите следующий URI в **Composer** вкладку: `http://localhost:port/odata/`, где *порт* — номер порта.</span><span class="sxs-lookup"><span data-stu-id="d1158-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="d1158-227">Нажмите кнопку **Execute** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d1158-227">Click the **Execute** button.</span></span> <span data-ttu-id="d1158-228">Fiddler приложение отправляет запрос HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="d1158-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="d1158-229">Вы должны увидеть ответ в списке веб-сеансами.</span><span class="sxs-lookup"><span data-stu-id="d1158-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="d1158-230">Если все работает, код состояния будет 200.</span><span class="sxs-lookup"><span data-stu-id="d1158-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="d1158-231">Дважды щелкните ответ в списке веб-сеансами, чтобы просмотреть сведения о ответное сообщение на вкладке «Инспекторы».</span><span class="sxs-lookup"><span data-stu-id="d1158-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="d1158-232">Необработанное сообщение ответа HTTP должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d1158-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="d1158-233">По умолчанию веб-API возвращает Сервисный документ в формате AtomPub.</span><span class="sxs-lookup"><span data-stu-id="d1158-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="d1158-234">Чтобы запросить JSON, добавьте следующий заголовок HTTP-запроса:</span><span class="sxs-lookup"><span data-stu-id="d1158-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="d1158-235">Теперь в HTTP-ответа содержит полезные данные JSON:</span><span class="sxs-lookup"><span data-stu-id="d1158-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="d1158-236">Документ метаданных службы</span><span class="sxs-lookup"><span data-stu-id="d1158-236">Service Metadata Document</span></span>

<span data-ttu-id="d1158-237">*Документ метаданных службы* описывается модель данных, службы, с помощью языка XML языка определения концептуальной схемы (CSDL).</span><span class="sxs-lookup"><span data-stu-id="d1158-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="d1158-238">Документ метаданных показана структура данных в службе и может использоваться для создания кода клиента.</span><span class="sxs-lookup"><span data-stu-id="d1158-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="d1158-239">Чтобы получить документ метаданных, отправьте запрос GET к `http://localhost:port/odata/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="d1158-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="d1158-240">Вот метаданные для конечной точки, в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d1158-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="d1158-241">Набор сущностей</span><span class="sxs-lookup"><span data-stu-id="d1158-241">Entity Set</span></span>

<span data-ttu-id="d1158-242">Для получения набора сущностей Products, отправьте запрос GET к `http://localhost:port/odata/Products`.</span><span class="sxs-lookup"><span data-stu-id="d1158-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="d1158-243">Объект</span><span class="sxs-lookup"><span data-stu-id="d1158-243">Entity</span></span>

<span data-ttu-id="d1158-244">Для получения конкретного продукта, отправьте запрос GET к `http://localhost:port/odata/Products(1)`, где «1» — это код продукта.</span><span class="sxs-lookup"><span data-stu-id="d1158-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="d1158-245">Форматы сериализации OData</span><span class="sxs-lookup"><span data-stu-id="d1158-245">OData Serialization Formats</span></span>

<span data-ttu-id="d1158-246">OData поддерживает несколько форматов сериализации:</span><span class="sxs-lookup"><span data-stu-id="d1158-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="d1158-247">Atom Pub (XML)</span><span class="sxs-lookup"><span data-stu-id="d1158-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="d1158-248">JSON «light» (впервые представлено в OData v3)</span><span class="sxs-lookup"><span data-stu-id="d1158-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="d1158-249">JSON «verbose» (OData v2)</span><span class="sxs-lookup"><span data-stu-id="d1158-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="d1158-250">По умолчанию веб-API использует формат «light» AtomPubJSON.</span><span class="sxs-lookup"><span data-stu-id="d1158-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="d1158-251">Чтобы получить формат AtomPub, задайте заголовок Accept «application/atom + xml».</span><span class="sxs-lookup"><span data-stu-id="d1158-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="d1158-252">Ниже приведен пример текста ответа.</span><span class="sxs-lookup"><span data-stu-id="d1158-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="d1158-253">Вы увидите одним из очевидных недостатков формат Atom. Это гораздо более подробным, чем JSON light.</span><span class="sxs-lookup"><span data-stu-id="d1158-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="d1158-254">Тем не менее если у вас есть клиент, который понимает AtomPub, клиент может предпочитать этот формат JSON.</span><span class="sxs-lookup"><span data-stu-id="d1158-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="d1158-255">Ниже приведен JSON облегченная версия той же сущности.</span><span class="sxs-lookup"><span data-stu-id="d1158-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="d1158-256">Формат JSON light появилась в версии 3 протокола OData.</span><span class="sxs-lookup"><span data-stu-id="d1158-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="d1158-257">Для обеспечения обратной совместимости старые «verbose» формат JSON может запрашиваться клиентом.</span><span class="sxs-lookup"><span data-stu-id="d1158-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="d1158-258">Чтобы запросить подробный формат JSON, задайте для заголовка Accept `application/json;odata=verbose`.</span><span class="sxs-lookup"><span data-stu-id="d1158-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="d1158-259">Ниже приведен подробный версии.</span><span class="sxs-lookup"><span data-stu-id="d1158-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="d1158-260">Этот формат передает дополнительные метаданные в текст ответа, который можно добавляют существенные системные издержки на весь сеанс.</span><span class="sxs-lookup"><span data-stu-id="d1158-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="d1158-261">Кроме того он добавляет уровень косвенного обращения, заключив объект в свойство с именем «d».</span><span class="sxs-lookup"><span data-stu-id="d1158-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1158-262">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="d1158-262">Next Steps</span></span>

- [<span data-ttu-id="d1158-263">Добавление отношений сущностей</span><span class="sxs-lookup"><span data-stu-id="d1158-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="d1158-264">Добавление действия OData</span><span class="sxs-lookup"><span data-stu-id="d1158-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="d1158-265">Вызов службы OData из клиента .NET</span><span class="sxs-lookup"><span data-stu-id="d1158-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
