---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Создание REST API с маршрутизацией атрибутов в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045186"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="6a4d7-102">Создание REST API с маршрутизацией атрибутов в веб-API ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="6a4d7-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="6a4d7-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6a4d7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="6a4d7-104">Веб-API 2 поддерживает новый тип маршрутизации, называемый *маршрутизацией атрибутов*.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="6a4d7-105">Общие сведения о маршрутизации атрибутов см. в разделе [Маршрутизация атрибутов в веб-API 2](attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="6a4d7-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="6a4d7-106">В этом учебнике для создания REST API коллекции книг будет использоваться маршрутизация атрибутов.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="6a4d7-107">API будет поддерживать следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-107">The API will support the following actions:</span></span>

| <span data-ttu-id="6a4d7-108">Действие</span><span class="sxs-lookup"><span data-stu-id="6a4d7-108">Action</span></span> | <span data-ttu-id="6a4d7-109">Пример URI</span><span class="sxs-lookup"><span data-stu-id="6a4d7-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="6a4d7-110">Получение списка всех книг.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-110">Get a list of all books.</span></span> | <span data-ttu-id="6a4d7-111">/апи/букс</span><span class="sxs-lookup"><span data-stu-id="6a4d7-111">/api/books</span></span> |
| <span data-ttu-id="6a4d7-112">Получение книги по ИДЕНТИФИКАТОРу.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-112">Get a book by ID.</span></span> | <span data-ttu-id="6a4d7-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="6a4d7-113">/api/books/1</span></span> |
| <span data-ttu-id="6a4d7-114">Получение сведений о книге.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-114">Get the details of a book.</span></span> | <span data-ttu-id="6a4d7-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="6a4d7-115">/api/books/1/details</span></span> |
| <span data-ttu-id="6a4d7-116">Получите список книг по жанрам.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-116">Get a list of books by genre.</span></span> | <span data-ttu-id="6a4d7-117">/апи/букс/фантаси</span><span class="sxs-lookup"><span data-stu-id="6a4d7-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="6a4d7-118">Получение списка книг по дате публикации.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="6a4d7-119">/API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (альтернативная форма)</span><span class="sxs-lookup"><span data-stu-id="6a4d7-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="6a4d7-120">Получение списка книг по определенному автору.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="6a4d7-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="6a4d7-121">/api/authors/1/books</span></span> |

<span data-ttu-id="6a4d7-122">Все методы доступны только для чтения (HTTP-запросы GET).</span><span class="sxs-lookup"><span data-stu-id="6a4d7-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="6a4d7-123">Для уровня данных мы будем использовать Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="6a4d7-124">Записи книги будут иметь следующие поля:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="6a4d7-125">ID</span><span class="sxs-lookup"><span data-stu-id="6a4d7-125">ID</span></span>
- <span data-ttu-id="6a4d7-126">Название</span><span class="sxs-lookup"><span data-stu-id="6a4d7-126">Title</span></span>
- <span data-ttu-id="6a4d7-127">Genre</span><span class="sxs-lookup"><span data-stu-id="6a4d7-127">Genre</span></span>
- <span data-ttu-id="6a4d7-128">дата публикации.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-128">Publication date</span></span>
- <span data-ttu-id="6a4d7-129">Цена</span><span class="sxs-lookup"><span data-stu-id="6a4d7-129">Price</span></span>
- <span data-ttu-id="6a4d7-130">Описание</span><span class="sxs-lookup"><span data-stu-id="6a4d7-130">Description</span></span>
- <span data-ttu-id="6a4d7-131">Аусорид (внешний ключ к таблице authors)</span><span class="sxs-lookup"><span data-stu-id="6a4d7-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="6a4d7-132">Однако для большинства запросов API вернет подмножество этих данных (заголовок, автор и жанр).</span><span class="sxs-lookup"><span data-stu-id="6a4d7-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="6a4d7-133">Для получения полной записи клиент запрашивает `/api/books/{id}/details` .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a4d7-134">Обязательные условия</span><span class="sxs-lookup"><span data-stu-id="6a4d7-134">Prerequisites</span></span>

<span data-ttu-id="6a4d7-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional или Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="6a4d7-136">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a4d7-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="6a4d7-137">Сначала запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-137">Start by running Visual Studio.</span></span> <span data-ttu-id="6a4d7-138">В меню **Файл** выберите пункт **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="6a4d7-139">Разверните категорию **установленные**  >  **Visual C#** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="6a4d7-140">В разделе **Visual C#** выберите **веб**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="6a4d7-141">В списке шаблонов проектов выберите **ASP.NET веб-приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="6a4d7-142">Назовите проект &quot; буксапи &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="6a4d7-143">В диалоговом окне **Создание веб-приложения ASP.NET** выберите **пустой** шаблон.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="6a4d7-144">В разделе "Добавление папок и основных ссылок для" установите флажок **веб-API** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="6a4d7-145">Нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="6a4d7-146">Будет создан каркас проекта, настроенного для работы веб-API.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="6a4d7-147">Модели предметной области</span><span class="sxs-lookup"><span data-stu-id="6a4d7-147">Domain Models</span></span>

<span data-ttu-id="6a4d7-148">Затем добавьте классы для моделей предметной области.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-148">Next, add classes for domain models.</span></span> <span data-ttu-id="6a4d7-149">В обозревателе решений щелкните правой кнопкой мыши папку Models.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="6a4d7-150">Нажмите кнопку **Добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="6a4d7-151">Назовите класс `Author`.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="6a4d7-152">Замените код в Author.cs следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="6a4d7-153">Теперь добавьте еще один класс с именем `Book` .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="6a4d7-154">Добавление контроллера веб-API</span><span class="sxs-lookup"><span data-stu-id="6a4d7-154">Add a Web API Controller</span></span>

<span data-ttu-id="6a4d7-155">На этом шаге мы добавим контроллер веб-API, который использует Entity Framework в качестве уровня данных.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="6a4d7-156">Для сборки проекта нажмите CTRL+SHIFT+B.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="6a4d7-157">Entity Framework использует отражение для обнаружения свойств моделей, поэтому для создания схемы базы данных требуется скомпилированная сборка.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="6a4d7-158">В обозревателе решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6a4d7-159">Нажмите кнопку **Добавить**, а затем выберите **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="6a4d7-160">В диалоговом окне **Добавление шаблона** выберите **контроллер веб-API 2 с действиями с помощью Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="6a4d7-161">В диалоговом окне **Добавление контроллера** в поле **имя контроллера**введите &quot; буксконтроллер &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="6a4d7-162">Установите &quot; флажок использовать асинхронные действия контроллера &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="6a4d7-163">В качестве **класса модели**выберите &quot; книга &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="6a4d7-164">(Если класс не отображается `Book` в раскрывающемся списке, убедитесь, что вы создали проект.) Затем нажмите кнопку "+".</span><span class="sxs-lookup"><span data-stu-id="6a4d7-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="6a4d7-165">Нажмите кнопку **Добавить** в диалоговом окне **новый контекст данных** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="6a4d7-166">Нажмите кнопку **Добавить** в диалоговом окне **Добавление контроллера** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="6a4d7-167">Формирование шаблонов добавляет класс с именем `BooksController` , который определяет контроллер API.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="6a4d7-168">Он также добавляет класс с именем `BooksAPIContext` в папку Models, который определяет контекст данных для Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="6a4d7-169">Заполнение базы данных</span><span class="sxs-lookup"><span data-stu-id="6a4d7-169">Seed the Database</span></span>

<span data-ttu-id="6a4d7-170">В меню Сервис выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="6a4d7-171">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="6a4d7-172">Эта команда создает папку Migrations и добавляет новый файл кода с именем Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="6a4d7-173">Откройте этот файл и добавьте в метод следующий код `Configuration.Seed` .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="6a4d7-174">В окне консоли диспетчера пакетов введите следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="6a4d7-175">Эти команды создают локальную базу данных и вызывают метод SEED для заполнения базы данных.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="6a4d7-176">Добавление классов DTO</span><span class="sxs-lookup"><span data-stu-id="6a4d7-176">Add DTO Classes</span></span>

<span data-ttu-id="6a4d7-177">Если запустить приложение сейчас и отправить запрос GET в/API/Books/1, ответ будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="6a4d7-178">(Добавлен отступ для удобочитаемости.)</span><span class="sxs-lookup"><span data-stu-id="6a4d7-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="6a4d7-179">Вместо этого я хочу, чтобы этот запрос возвращал подмножество полей.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="6a4d7-180">Кроме того, я хочу, чтобы он возвращал имя автора, а не идентификатор автора.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="6a4d7-181">Для этого мы изменим методы контроллера, чтобы возвращали *объект передачи данных* (DTO) вместо модели EF.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="6a4d7-182">DTO — это объект, предназначенный только для переноса данных.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="6a4d7-183">В Обозреватель решений щелкните правой кнопкой мыши проект и выберите команду **Добавить**  |  **новую папку**.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="6a4d7-184">Назовите папку &quot; DTO &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="6a4d7-185">Добавьте класс с именем `BookDto` в папку DTO со следующим определением:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="6a4d7-186">Добавьте еще один класс с именем `BookDetailDto`.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="6a4d7-187">Затем обновите `BooksController` класс, чтобы он возвращал `BookDto` экземпляры.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="6a4d7-188">Мы будем использовать метод [запроса. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) для `Book` экземпляров проекта в `BookDto` экземплярах.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="6a4d7-189">Ниже приведен обновленный код для класса Controller.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="6a4d7-190">Я удалил `PutBook` методы, `PostBook` и `DeleteBook` , так как они не нужны для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="6a4d7-191">Теперь, если вы запустите приложение и запросите/API/Books/1, текст ответа должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="6a4d7-192">Добавление атрибутов маршрута</span><span class="sxs-lookup"><span data-stu-id="6a4d7-192">Add Route Attributes</span></span>

<span data-ttu-id="6a4d7-193">Далее мы преобразуем контроллер для использования маршрутизации атрибутов.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="6a4d7-194">Сначала добавьте атрибут **RoutePrefix** к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="6a4d7-195">Этот атрибут определяет начальные сегменты URI для всех методов на этом контроллере.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="6a4d7-196">Затем добавьте атрибуты **[Route]** к действиям контроллера следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="6a4d7-197">Шаблон маршрута для каждого метода контроллера — это префикс плюс строка, указанная в атрибуте **Route** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="6a4d7-198">Для `GetBook` метода шаблон маршрута включает параметризованную строку &quot; {ID: int} &quot; , которая соответствует, если сегмент URI содержит целочисленное значение.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="6a4d7-199">Метод</span><span class="sxs-lookup"><span data-stu-id="6a4d7-199">Method</span></span> | <span data-ttu-id="6a4d7-200">Шаблон маршрута</span><span class="sxs-lookup"><span data-stu-id="6a4d7-200">Route Template</span></span> | <span data-ttu-id="6a4d7-201">Пример URI</span><span class="sxs-lookup"><span data-stu-id="6a4d7-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="6a4d7-202">"API/книги"</span><span class="sxs-lookup"><span data-stu-id="6a4d7-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="6a4d7-203">"API/Books/{ID: int}"</span><span class="sxs-lookup"><span data-stu-id="6a4d7-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="6a4d7-204">Получение сведений о книге</span><span class="sxs-lookup"><span data-stu-id="6a4d7-204">Get Book Details</span></span>

<span data-ttu-id="6a4d7-205">Чтобы получить сведения о книге, клиент отправит запрос GET в `/api/books/{id}/details` , где *{ID}* — это идентификатор книги.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="6a4d7-206">Добавьте следующий метод в класс `BooksController`.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="6a4d7-207">Если вы запрашиваете запрос `/api/books/1/details` , ответ будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="6a4d7-208">Получение книг по жанру</span><span class="sxs-lookup"><span data-stu-id="6a4d7-208">Get Books By Genre</span></span>

<span data-ttu-id="6a4d7-209">Чтобы получить список книг по определенному жанру, клиент отправит запрос GET в `/api/books/genre` , где *Жанр* — название жанра.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="6a4d7-210">(Например, `/api/books/fantasy`).</span><span class="sxs-lookup"><span data-stu-id="6a4d7-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="6a4d7-211">Добавьте следующий метод в `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="6a4d7-212">Здесь мы определяем маршрут, который содержит параметр {жанр} в шаблоне URI.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="6a4d7-213">Обратите внимание, что веб-API может отличать эти два URI и пересылать их разным методам:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="6a4d7-214">Это обусловлено тем, что `GetBook` метод включает ограничение, которое сегмент "ID" должен иметь целочисленное значение:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="6a4d7-215">Если вы запрашиваете/АПИ/букс/Фантаси, ответ будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="6a4d7-216">Получить книги по автору</span><span class="sxs-lookup"><span data-stu-id="6a4d7-216">Get Books By Author</span></span>

<span data-ttu-id="6a4d7-217">Чтобы получить список книг для конкретного автора, клиент отправит запрос GET в `/api/authors/id/books` , где *ID* — это идентификатор автора.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="6a4d7-218">Добавьте следующий метод в `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="6a4d7-219">Этот пример интересно, поскольку &quot; книги &quot; обрабатываются дочерним ресурсом &quot; авторов &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="6a4d7-220">Этот шаблон довольно распространен в интерфейсах API RESTFUL.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="6a4d7-221">Тильда (~) в шаблоне маршрута переопределяет префикс маршрута в атрибуте **RoutePrefix** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="6a4d7-222">Получение книг по дате публикации</span><span class="sxs-lookup"><span data-stu-id="6a4d7-222">Get Books By Publication Date</span></span>

<span data-ttu-id="6a4d7-223">Чтобы получить список книг по дате публикации, клиент отправит запрос GET в `/api/books/date/yyyy-mm-dd` , где *гггг-мм-дд* — это дата.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="6a4d7-224">Вот один из способов:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="6a4d7-225">`{pubdate:datetime}`Параметр ограничен в соответствии со значением **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="6a4d7-226">Это работает, но на самом деле он более разрешительно, чем хотелось бы.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="6a4d7-227">Например, эти URI также будут соответствовать маршруту:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="6a4d7-228">Для разрешения этих URI ничего не так.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="6a4d7-229">Однако можно ограничить маршрут до определенного формата, добавив ограничение регулярного выражения в шаблон маршрута:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="6a4d7-230">Теперь будут соответствовать только даты в формате &quot; гггг-мм-дд &quot; .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="6a4d7-231">Обратите внимание, что мы не будем использовать регулярное выражение для проверки фактической даты.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="6a4d7-232">Это обрабатывается, когда веб-API пытается преобразовать сегмент URI в экземпляр **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="6a4d7-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="6a4d7-233">Недопустимая дата, например "2012-47-99", не будет преобразована, и клиент получит ошибку 404.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="6a4d7-234">Можно также поддерживать разделитель косой черты ( `/api/books/date/yyyy/mm/dd` ), добавив еще один атрибут **[Route]** с другим регулярным выражением.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="6a4d7-235">Здесь есть небольшие, но важные подробности.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="6a4d7-236">Второй шаблон маршрута содержит символ-шаблон ( \* ) в начале параметра {pubDate}:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

<span data-ttu-id="6a4d7-237">Это указывает механизму маршрутизации, что {pubDate} должно соответствовать остальной части URI.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="6a4d7-238">По умолчанию параметр шаблона соответствует одному сегменту URI.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="6a4d7-239">В этом случае нам нужно, чтобы {pubDate} занимал несколько сегментов URI:</span><span class="sxs-lookup"><span data-stu-id="6a4d7-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="6a4d7-240">Код контроллера</span><span class="sxs-lookup"><span data-stu-id="6a4d7-240">Controller Code</span></span>

<span data-ttu-id="6a4d7-241">Ниже приведен полный код для класса Буксконтроллер.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="6a4d7-242">Сводка</span><span class="sxs-lookup"><span data-stu-id="6a4d7-242">Summary</span></span>

<span data-ttu-id="6a4d7-243">Маршрутизация атрибутов обеспечивает более широкие возможности управления и гибкость при проектировании URI для API.</span><span class="sxs-lookup"><span data-stu-id="6a4d7-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
