---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Создание модульных тестов для приложений ASP.NET MVC (C#) | Документация Майкрософт
author: StephenWalther
description: Сведения о создании модульных тестов для действий контроллера. Стивен Вальтер в этом руководстве показано, как протестировать действия контроллера возвращает parti ли...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 1193d7dc6fc29dfdac5637c9391a82f9f3566073
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59407735"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="4b2fc-104">Создание модульных тестов для приложений ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="4b2fc-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="4b2fc-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="4b2fc-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="4b2fc-106">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="4b2fc-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="4b2fc-107">Сведения о создании модульных тестов для действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="4b2fc-108">В этом руководстве Стивен Вальтер показано, как проверить ли действие контроллера возвращает конкретное представление, возвращает определенный набор данных или другой тип результата действия.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="4b2fc-109">Целью данного учебника — продемонстрировать, как можно создавать модульные тесты для контроллеров в your ASP.NET MVC приложений.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="4b2fc-110">Мы обсудим, как создать три разных типа модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="4b2fc-111">Вы узнаете, как для представления, возвращаемого действием контроллера тестирования, как проверить данные представления, возвращаемое в результате действия контроллера и способы тестирования независимо от того, имеется ли одно действие контроллера перенаправит вас на второе действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="4b2fc-112">Создание контроллера при тестировании</span><span class="sxs-lookup"><span data-stu-id="4b2fc-112">Creating the Controller under Test</span></span>

<span data-ttu-id="4b2fc-113">Начнем с создания контроллера, к которому мы намерены протестировать.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="4b2fc-114">Контроллер, с именем `ProductController`, содержащийся в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

**<span data-ttu-id="4b2fc-115">Листинг 1.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-115">Listing 1 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="4b2fc-116">`ProductController` Содержит два метода действия с именем `Index()` и `Details()`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="4b2fc-117">Оба метода действия возвращают представления.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-117">Both action methods return a view.</span></span> <span data-ttu-id="4b2fc-118">Обратите внимание, что `Details()` действие принимает параметр с именем Id.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="4b2fc-119">Тестирование представления возвращаемые контроллера</span><span class="sxs-lookup"><span data-stu-id="4b2fc-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="4b2fc-120">Представьте, что нам нужно протестировать ли `ProductController` возвращает правильное представление.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="4b2fc-121">Мы хотим, чтобы убедиться, что при `ProductController.Details()` вызывается действие, возвращается в представлении сведений.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="4b2fc-122">Класс test в листинге 2 содержит модульного теста для тестирования представления, возвращаемого с `ProductController.Details()` действие.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

**<span data-ttu-id="4b2fc-123">Листинг 2.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-123">Listing 2 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="4b2fc-124">Класс в листинге 2 включает метод теста с именем `TestDetailsView()`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="4b2fc-125">Этот метод содержит три строки кода.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-125">This method contains three lines of code.</span></span> <span data-ttu-id="4b2fc-126">В первой строке кода создается новый экземпляр класса `ProductController` класса.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="4b2fc-127">Вторая строка кода вызывает контроллера `Details()` метода действия.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="4b2fc-128">Наконец, последняя строка ли возвращаемый представление проверки кода `Details()` действие является представлением сведений.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="4b2fc-129">`ViewResult.ViewName` Свойство представляет имя представления, возвращаемого с помощью контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="4b2fc-130">Одно важное предупреждение о тестировании это свойство.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-130">One big warning about testing this property.</span></span> <span data-ttu-id="4b2fc-131">Существует два способа, что контроллер может возвратить представление.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="4b2fc-132">Контроллер может явным образом вернуть представление следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4b2fc-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="4b2fc-133">Кроме того имя представления можно быть выведены из имени действия контроллера следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4b2fc-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="4b2fc-134">Это действие контроллера также возвращает представление с именем `Details`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="4b2fc-135">Тем не менее имя представления выводится из имени действия.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="4b2fc-136">Если вы хотите протестировать имя представления, вы должны явно возвращается имя представления из действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="4b2fc-137">Запуском модульного теста в листинге 2, либо введя сочетание **Ctrl + R, A** или щелкнув **запустить все тесты в решении** кнопку (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="4b2fc-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="4b2fc-138">Если тест проходит успешно, вы увидите в окне результатов теста на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


[![R<span data-ttu-id="4b2fc-139">Отменить все тесты в решении]</span><span class="sxs-lookup"><span data-stu-id="4b2fc-139">un All Tests in Solution]</span></span>(creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

<span data-ttu-id="4b2fc-140">**Рис 01**: Выполнение всех тестов в решении ([Просмотр полноразмерного изображения](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4b2fc-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


[![S<span data-ttu-id="4b2fc-141">uccess!]</span><span class="sxs-lookup"><span data-stu-id="4b2fc-141">uccess!]</span></span>(creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

<span data-ttu-id="4b2fc-142">**Рис. 02**: Готово!</span><span class="sxs-lookup"><span data-stu-id="4b2fc-142">**Figure 02**: Success!</span></span> <span data-ttu-id="4b2fc-143">([Просмотр полноразмерного изображения](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4b2fc-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="4b2fc-144">Тестирование представления данных возвращается с помощью контроллера</span><span class="sxs-lookup"><span data-stu-id="4b2fc-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="4b2fc-145">Контроллер MVC передает данные для представления, используя такую вещь *`View Data`*.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="4b2fc-146">Например, представьте, что вы хотите отобразить сведения для конкретного продукта, при вызове `ProductController Details()` действие.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="4b2fc-147">В этом случае можно создать экземпляр `Product` класс (определенный в модели) и передать экземпляр для `Details` представление, используя преимущества `View Data`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="4b2fc-148">Измененный `ProductController` в листинге 3 включает в себя обновленный `Details()` действие, которое возвращает продукт.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

**<span data-ttu-id="4b2fc-149">Листинг 3.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-149">Listing 3 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="4b2fc-150">Во-первых, `Details()` действие создает новый экземпляр класса `Product` класс, представляющий переносного компьютера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="4b2fc-151">Далее, экземпляр `Product` класса передается в качестве второго параметра `View()` метод.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="4b2fc-152">Можно написать модульные тесты для проверки ожидаемых данных содержатся в представлении данных.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="4b2fc-153">Модульный тест в листинге 4 тестах, независимо от того, имеется ли продукт, представляющий переносной компьютер возвращается при вызове `ProductController Details()` метода действия.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

**<span data-ttu-id="4b2fc-154">Листинг 4.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-154">Listing 4 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="4b2fc-155">В листинге 4 `TestDetailsView()` метод проверяет данные представления, возвращаемые при вызове `Details()` метод.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="4b2fc-156">`ViewData` Предоставляется как свойство `ViewResult` возвращенные вызовом `Details()` метод.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="4b2fc-157">`ViewData.Model` Свойство содержит результат передается в представление.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="4b2fc-158">Тест просто продукта, содержащиеся в представлении данных проверяет, имеет ли имя ноутбука.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="4b2fc-159">Тестирование результата действия возвращается с помощью контроллера</span><span class="sxs-lookup"><span data-stu-id="4b2fc-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="4b2fc-160">Более сложные действия контроллера могут возвращать различные типы результатов действий в зависимости от значений параметров, передаваемых действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="4b2fc-161">Действие контроллера могут возвращать различные типы результатов действий, в том числе `ViewResult`, `RedirectToRouteResult`, или `JsonResult`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="4b2fc-162">Например, измененный `Details()` в листинге 5 вы возвращаетесь `Details` просмотра при передаче допустимый код продукта в действие.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="4b2fc-163">Если передается недопустимый продуктом Id — идентификатор со значением меньше 1, то вы будете перенаправлены на `Index()` действие.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

**<span data-ttu-id="4b2fc-164">Листинг 5.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-164">Listing 5 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="4b2fc-165">Можно тестировать реакцию на событие `Details()` действие с модульным тестом в листинге 6.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="4b2fc-166">В листинге 6 модульный тест проверяет, что вы будете перенаправлены на `Index` просмотра при передаче идентификатора значение -1 `Details()` метод.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

**<span data-ttu-id="4b2fc-167">Листинг 6.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-167">Listing 6 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="4b2fc-168">При вызове `RedirectToAction()` в действие контроллера, действия контроллера методом `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="4b2fc-169">Тест проверки ли `RedirectToRouteResult` перенаправляет пользователя на выполнение действия контроллера с именем `Index`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="4b2fc-170">Сводка</span><span class="sxs-lookup"><span data-stu-id="4b2fc-170">Summary</span></span>

<span data-ttu-id="4b2fc-171">В этом руководстве вы узнали, как для создания модульных тестов для действий контроллеров MVC.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="4b2fc-172">Во-первых вы узнали, как проверить, возвращается ли правильное представление с помощью действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="4b2fc-173">Вы узнали, как использовать `ViewResult.ViewName` свойство для проверки имени представления.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="4b2fc-174">Далее мы рассмотрели, как можно проверить содержимое `View Data`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="4b2fc-175">Вы узнали, как проверить, возвращаются ли оптимальный продукт в `View Data` после вызова действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="4b2fc-176">Наконец мы рассмотрели, как вы можете протестировать различные типы результатов действий возвращаются из действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="4b2fc-177">Вы узнали, как проверить ли контроллер возвращает `ViewResult` или `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="4b2fc-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4b2fc-178">Далее</span><span class="sxs-lookup"><span data-stu-id="4b2fc-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
