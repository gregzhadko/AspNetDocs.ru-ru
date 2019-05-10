---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: Часть 7. Создание главной страницы | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: aaffcecccd138d30355ac0e7ce6c86a67246cc08
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108929"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="ed1ea-102">Часть 7. Создание главной страницы</span><span class="sxs-lookup"><span data-stu-id="ed1ea-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="ed1ea-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ed1ea-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ed1ea-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="ed1ea-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="ed1ea-105">Создание главной страницы</span><span class="sxs-lookup"><span data-stu-id="ed1ea-105">Creating the Main Page</span></span>

<span data-ttu-id="ed1ea-106">В этом разделе вы создадите страницу основного приложения.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="ed1ea-107">Эта страница будет сложнее, чем для страницы, поэтому мы будем подходите к ней в несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="ed1ea-108">Кроме того вы увидите некоторые более сложные приемы Knockout.js.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="ed1ea-109">Ниже приведен базовый макет страницы.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="ed1ea-110">«Продукты» содержит массив продуктов.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="ed1ea-111">«Корзины» содержит массив продуктов с количествами.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="ed1ea-112">Нажав кнопку «Add to Cart» обновляет корзины для покупок.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="ed1ea-113">«Orders» содержит массив идентификаторов заказов.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="ed1ea-114">«Подробности» содержит подробности заказа, который является массивом элементов (продукты с количествами)</span><span class="sxs-lookup"><span data-stu-id="ed1ea-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="ed1ea-115">Мы начнем с определения некоторых базовый макет в формате HTML, без привязки данных или скрипт.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="ed1ea-116">Откройте файл Views/Home/Index.cshtml и замените содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="ed1ea-117">Затем добавьте раздел скриптов и создать пустую модель представления:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="ed1ea-118">Исходя из конструктора, ранее в виде эскиза, наша модель представления должна наблюдаемые объекты для продуктов, для покупок, заказы и сведения.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="ed1ea-119">Добавьте следующие переменные `AppViewModel` объекта:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="ed1ea-120">Пользователей можно добавить элементы из списка продуктов в корзине и удаления элементов из корзины.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="ed1ea-121">Чтобы инкапсулировать эти функции, мы создадим другого класса модели представления, который представляет продукт.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="ed1ea-122">Добавьте следующий код в файл `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="ed1ea-123">`ProductViewModel` Класс содержит две функции, которые используются для перемещения продукта и из корзины: `addItemToCart` добавляет одну единицу продукта в корзину и `removeAllFromCart` удаляет все количества продукта.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="ed1ea-124">Пользователи могут выбрать существующий заказ и получить сведения о заказе.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="ed1ea-125">Мы оформим этих функций в другой модели представления:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="ed1ea-126">`OrderDetailsViewModel` Инициализируется с порядком, и она получает сведения о заказе, отправляя запрос AJAX на сервер.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="ed1ea-127">Кроме того, обратите внимание, что `total` свойство `OrderDetailsViewModel`.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="ed1ea-128">Это свойство — это особый тип вызывается наблюдаемого объекта [вычисляемые наблюдаемый объект](http://knockoutjs.com/documentation/computedObservables.html).</span><span class="sxs-lookup"><span data-stu-id="ed1ea-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="ed1ea-129">Как и предполагает название, вычисляемый наблюдаемым позволяет привязки данных к вычисляемым значением&#8212;в этом случае общая стоимость заказа.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="ed1ea-130">Затем добавьте эти функции для `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="ed1ea-131">`resetCart` Удаляет все элементы из корзины.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="ed1ea-132">`getDetails` Возвращает сведения для заказа (с помощью принудительной отправки нового `OrderDetailsViewModel` на `details` списка).</span><span class="sxs-lookup"><span data-stu-id="ed1ea-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="ed1ea-133">`createOrder` Создает новый порядок и очистке корзины для покупок.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="ed1ea-134">Наконец инициализируйте модели представления, отправку запросов AJAX для продуктов и заказов:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="ed1ea-135">Итак, вот большой объем кода, но мы создали его вверх пошаговые, будем надеяться разработки снят.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="ed1ea-136">Теперь мы можем добавить некоторые привязки Knockout.js в HTML-код.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="ed1ea-137">**Продукты**</span><span class="sxs-lookup"><span data-stu-id="ed1ea-137">**Products**</span></span>

<span data-ttu-id="ed1ea-138">Ниже приведены привязки для списка продуктов.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="ed1ea-139">Это используется для итерации по массиву продуктов и отображает название и цену.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="ed1ea-140">Кнопка «Добавить к Order» отображается только в том случае, когда пользователь входит в систему.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="ed1ea-141">Вызовы кнопку «Добавить на заказ» `addItemToCart` на `ProductViewModel` экземпляра для продукта.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="ed1ea-142">Это показывает приятной особенностью Knockout.js: Если модель представления содержит другие модели представлений, можно применить привязок внутреннее модель.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="ed1ea-143">В этом примере привязки в пределах `foreach` применяются к каждому из `ProductViewModel` экземпляров.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="ed1ea-144">Этот подход является более понятны, чем хранение всех функций в одной модели представления.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="ed1ea-145">**Для покупок**</span><span class="sxs-lookup"><span data-stu-id="ed1ea-145">**Cart**</span></span>

<span data-ttu-id="ed1ea-146">Ниже приведены привязки для корзины для покупок.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="ed1ea-147">Это используется для итерации по массиву корзины для покупок и отображает имя, цену и количество.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="ed1ea-148">Обратите внимание на то, что ссылку «Удалить» и кнопка «Создание заказа» привязаны к функции модели представления.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="ed1ea-149">**Заказы**</span><span class="sxs-lookup"><span data-stu-id="ed1ea-149">**Orders**</span></span>

<span data-ttu-id="ed1ea-150">Ниже приведены привязки для списка заказов.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="ed1ea-151">Это выполняет итерацию по заказам и показывает идентификатора заказа.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="ed1ea-152">Событие щелчка по ссылке, привязан к `getDetails` функции.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="ed1ea-153">**Сведения о заказе**</span><span class="sxs-lookup"><span data-stu-id="ed1ea-153">**Order Details**</span></span>

<span data-ttu-id="ed1ea-154">Ниже приведены привязки для сведений о заказе.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="ed1ea-155">Это выполняет итерацию по элементам в порядке и отображает продукта, цену и количество.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="ed1ea-156">Окружающий div отображается только в том случае, если сведения о массив содержит один или несколько элементов.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ed1ea-157">Заключение</span><span class="sxs-lookup"><span data-stu-id="ed1ea-157">Conclusion</span></span>

<span data-ttu-id="ed1ea-158">В этом руководстве вы создали приложение, использующее Entity Framework для взаимодействия с базой данных и веб-API ASP.NET и предоставляет общедоступный интерфейс поверх уровня данных.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="ed1ea-159">Мы используем ASP.NET MVC 4 для отрисовки HTML-страниц и Knockout.js плюс jQuery для обеспечения динамического взаимодействия без перезагрузок страницы.</span><span class="sxs-lookup"><span data-stu-id="ed1ea-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="ed1ea-160">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="ed1ea-160">Additional resources:</span></span>

- [<span data-ttu-id="ed1ea-161">Схема содержимого для доступа к данным ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ed1ea-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="ed1ea-162">Центр разработчиков Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ed1ea-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="ed1ea-163">Назад</span><span class="sxs-lookup"><span data-stu-id="ed1ea-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
