---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: Часть 5. Создание динамического пользовательского интерфейса с помощью Knockout.js | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: b06f738d821d78f74069c3bf0f6c0880796195d2
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393292"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="81139-102">Часть 5. Создание динамического пользовательского интерфейса с помощью Knockout.js</span><span class="sxs-lookup"><span data-stu-id="81139-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="81139-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="81139-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="81139-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="81139-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="81139-105">Создание динамического пользовательского интерфейса с помощью Knockout.js</span><span class="sxs-lookup"><span data-stu-id="81139-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="81139-106">В этом разделе мы будем использовать Knockout.js для добавления функций в представлении администратора.</span><span class="sxs-lookup"><span data-stu-id="81139-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="81139-107">[Knockout.js](http://knockoutjs.com/) — это библиотека Javascript, которая позволяет легко выполнить привязку к данным элементы управления HTML.</span><span class="sxs-lookup"><span data-stu-id="81139-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="81139-108">Knockout.js использует шаблон Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="81139-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="81139-109">*Модели* — это представление на сервере данные в предметной области бизнеса (в нашем случае продуктов и заказов).</span><span class="sxs-lookup"><span data-stu-id="81139-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="81139-110">*Представление* является уровень представления (HTML).</span><span class="sxs-lookup"><span data-stu-id="81139-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="81139-111">*Модель представления* — объект Javascript, которая содержит данные модели.</span><span class="sxs-lookup"><span data-stu-id="81139-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="81139-112">Модель представления — это абстракция код пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="81139-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="81139-113">Он не имеет сведений о представление HTML.</span><span class="sxs-lookup"><span data-stu-id="81139-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="81139-114">Вместо этого он представляет абстрактные функции, представления, например «список элементов».</span><span class="sxs-lookup"><span data-stu-id="81139-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="81139-115">Представление данных привязан к модели представления.</span><span class="sxs-lookup"><span data-stu-id="81139-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="81139-116">Обновления для модели представления автоматически отражаются в представлении.</span><span class="sxs-lookup"><span data-stu-id="81139-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="81139-117">Модель представления также получает события из представления, например нажатие кнопки и выполняет операции в модели, например создание заказа.</span><span class="sxs-lookup"><span data-stu-id="81139-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="81139-118">Сначала мы определим модели представления.</span><span class="sxs-lookup"><span data-stu-id="81139-118">First we'll define the view-model.</span></span> <span data-ttu-id="81139-119">После этого выполняется привязка HTML-разметка для модели представления.</span><span class="sxs-lookup"><span data-stu-id="81139-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="81139-120">Добавьте следующий раздел Razor Admin.cshtml:</span><span class="sxs-lookup"><span data-stu-id="81139-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="81139-121">В этом разделе можно добавить в любом месте в файле.</span><span class="sxs-lookup"><span data-stu-id="81139-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="81139-122">При визуализации представления, раздел отображается в нижней части страницы HTML, прямо перед закрывающим &lt;/body&gt; тега.</span><span class="sxs-lookup"><span data-stu-id="81139-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="81139-123">Весь сценарий для этой страницы будет находиться внутри тег сценария, обозначается комментарий:</span><span class="sxs-lookup"><span data-stu-id="81139-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="81139-124">Во-первых определите класс модели представления:</span><span class="sxs-lookup"><span data-stu-id="81139-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="81139-125">**ko.observableArray** — это особый тип объекта в Knockout, вызывается *наблюдаемый объект*.</span><span class="sxs-lookup"><span data-stu-id="81139-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="81139-126">Из [Knockout.js документации](http://knockoutjs.com/documentation/observables.html): Наблюдаемый объект — «объект JavaScript, можно уведомлять подписчиков об изменениях.»</span><span class="sxs-lookup"><span data-stu-id="81139-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="81139-127">При изменении содержимого наблюдаемый объект, представление автоматически обновляется для соответствия.</span><span class="sxs-lookup"><span data-stu-id="81139-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="81139-128">Для заполнения `products` массива, выполнить запрос AJAX в веб-API.</span><span class="sxs-lookup"><span data-stu-id="81139-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="81139-129">Помните, что мы храниться базовый URI для API в пакет представления (см. в разделе [часть 4](using-web-api-with-entity-framework-part-4.md) руководства).</span><span class="sxs-lookup"><span data-stu-id="81139-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="81139-130">Затем добавьте функции модели представления для создания, обновления и удаления продуктов.</span><span class="sxs-lookup"><span data-stu-id="81139-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="81139-131">Эти функции отправки вызовов AJAX в веб-API и использовать результаты для обновления модели представления.</span><span class="sxs-lookup"><span data-stu-id="81139-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="81139-132">Теперь самое главное: Когда модель DOM является fulled загружено, вызов **ko.applyBindings** функции и передайте новый экземпляр класса `ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="81139-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="81139-133">**Ko.applyBindings** метод активирует Knockout и сводит модели представления к представлению.</span><span class="sxs-lookup"><span data-stu-id="81139-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="81139-134">Теперь, когда у нас есть модель представления, можно создать привязки.</span><span class="sxs-lookup"><span data-stu-id="81139-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="81139-135">В Knockout.js, это сделать, добавив `data-bind` атрибуты к элементам HTML.</span><span class="sxs-lookup"><span data-stu-id="81139-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="81139-136">Например, чтобы привязать HTML-списка в массив, используйте `foreach` привязки:</span><span class="sxs-lookup"><span data-stu-id="81139-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="81139-137">`foreach` Привязка используется для итерации по массиву и создает дочерние элементы для каждого объекта в массиве.</span><span class="sxs-lookup"><span data-stu-id="81139-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="81139-138">Привязки для дочерних элементов может ссылаться на свойства объектов массива.</span><span class="sxs-lookup"><span data-stu-id="81139-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="81139-139">Добавьте следующие привязки в список «обновление продукты»:</span><span class="sxs-lookup"><span data-stu-id="81139-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="81139-140">`<li>` Элемент присутствует в пределах **foreach** привязки.</span><span class="sxs-lookup"><span data-stu-id="81139-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="81139-141">Что означает, что будет частичной визуализации элемента один раз для каждого продукта в `products` массива.</span><span class="sxs-lookup"><span data-stu-id="81139-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="81139-142">Все привязки в `<li>` элементе ссылаться на этот экземпляр продукта.</span><span class="sxs-lookup"><span data-stu-id="81139-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="81139-143">Например `$data.Name` ссылается на `Name` свойство над продуктом.</span><span class="sxs-lookup"><span data-stu-id="81139-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="81139-144">Чтобы задать значения текстовые входные данные, используйте `value` привязки.</span><span class="sxs-lookup"><span data-stu-id="81139-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="81139-145">Кнопки привязаны к функциям на модель представление, с помощью `click` привязки.</span><span class="sxs-lookup"><span data-stu-id="81139-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="81139-146">Экземпляр продукта передается как параметр для каждой функции.</span><span class="sxs-lookup"><span data-stu-id="81139-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="81139-147">Дополнительные сведения [Knockout.js документации](http://knockoutjs.com/documentation/observables.html) имеет хорошее описания различных привязок.</span><span class="sxs-lookup"><span data-stu-id="81139-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="81139-148">Добавьте привязку для **отправить** событий в форме добавить продукт:</span><span class="sxs-lookup"><span data-stu-id="81139-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="81139-149">Эта привязка вызывает `create` функции в модели представления для создания нового продукта.</span><span class="sxs-lookup"><span data-stu-id="81139-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="81139-150">Ниже приведен полный код для представления администрирования:</span><span class="sxs-lookup"><span data-stu-id="81139-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="81139-151">Запустите приложение, войдите с помощью учетной записи администратора и щелкните ссылку «Admin».</span><span class="sxs-lookup"><span data-stu-id="81139-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="81139-152">Следует просмотреть список продуктов и иметь возможность создания, обновления или удаления продуктов.</span><span class="sxs-lookup"><span data-stu-id="81139-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="81139-153">[Назад](using-web-api-with-entity-framework-part-4.md)
> [Вперед](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="81139-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
