---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: Проверка с помощью интерфейса IDataErrorInfo (C#) | Документация Майкрософт
author: StephenWalther
description: Стивен Вальтер показано, как для отображения пользовательской проверки ошибок путем реализации интерфейса IDataErrorInfo в классе модели.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e1399d17840a2f5301349cb91deb07b0cc34363
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421983"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="c5451-103">Проверка с помощью интерфейса IDataErrorInfo (C#)</span><span class="sxs-lookup"><span data-stu-id="c5451-103">Validating with the IDataErrorInfo Interface (C#)</span></span>

<span data-ttu-id="c5451-104">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c5451-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="c5451-105">Стивен Вальтер показано, как для отображения пользовательской проверки ошибок путем реализации интерфейса IDataErrorInfo в классе модели.</span><span class="sxs-lookup"><span data-stu-id="c5451-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>


<span data-ttu-id="c5451-106">Этот учебник призван объяснить одним из подходов к проверке в ASP.NET MVC-приложениях.</span><span class="sxs-lookup"><span data-stu-id="c5451-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="c5451-107">Вы узнаете, как запретить кто-то отправка формы HTML без указания значения для обязательных полей формы.</span><span class="sxs-lookup"><span data-stu-id="c5451-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="c5451-108">В этом руководстве вы узнаете, как выполнять проверку с помощью интерфейса IErrorDataInfo.</span><span class="sxs-lookup"><span data-stu-id="c5451-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="c5451-109">Допущения</span><span class="sxs-lookup"><span data-stu-id="c5451-109">Assumptions</span></span>

<span data-ttu-id="c5451-110">В данном случае я использую MoviesDB базы данных и таблицы базы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="c5451-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="c5451-111">Эта таблица содержит следующие столбцы:</span><span class="sxs-lookup"><span data-stu-id="c5451-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>


| **<span data-ttu-id="c5451-112">Имя столбца</span><span class="sxs-lookup"><span data-stu-id="c5451-112">Column Name</span></span>** | **<span data-ttu-id="c5451-113">Тип данных</span><span class="sxs-lookup"><span data-stu-id="c5451-113">Data Type</span></span>** | **<span data-ttu-id="c5451-114">Разрешить значения null</span><span class="sxs-lookup"><span data-stu-id="c5451-114">Allow Nulls</span></span>** |
| --- | --- | --- |
| <span data-ttu-id="c5451-115">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="c5451-115">Id</span></span> | <span data-ttu-id="c5451-116">Int</span><span class="sxs-lookup"><span data-stu-id="c5451-116">Int</span></span> | <span data-ttu-id="c5451-117">False</span><span class="sxs-lookup"><span data-stu-id="c5451-117">False</span></span> |
| <span data-ttu-id="c5451-118">Заголовок</span><span class="sxs-lookup"><span data-stu-id="c5451-118">Title</span></span> | <span data-ttu-id="c5451-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="c5451-119">Nvarchar(100)</span></span> | <span data-ttu-id="c5451-120">False</span><span class="sxs-lookup"><span data-stu-id="c5451-120">False</span></span> |
| <span data-ttu-id="c5451-121">Директор</span><span class="sxs-lookup"><span data-stu-id="c5451-121">Director</span></span> | <span data-ttu-id="c5451-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="c5451-122">Nvarchar(100)</span></span> | <span data-ttu-id="c5451-123">False</span><span class="sxs-lookup"><span data-stu-id="c5451-123">False</span></span> |
| <span data-ttu-id="c5451-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="c5451-124">DateReleased</span></span> | <span data-ttu-id="c5451-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="c5451-125">DateTime</span></span> | <span data-ttu-id="c5451-126">False</span><span class="sxs-lookup"><span data-stu-id="c5451-126">False</span></span> |


<span data-ttu-id="c5451-127">В данном случае я использую Microsoft Entity Framework для создания Мои классы модели базы данных.</span><span class="sxs-lookup"><span data-stu-id="c5451-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="c5451-128">Класс Movie, созданным Entity Framework отображается на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="c5451-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>


[![T<span data-ttu-id="c5451-129">он сущности фильма]</span><span class="sxs-lookup"><span data-stu-id="c5451-129">he Movie entity]</span></span>(validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

<span data-ttu-id="c5451-130">**Рис 01**: Объект фильма ([Просмотр полноразмерного изображения](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c5451-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="c5451-131">Дополнительные сведения об использовании платформы Entity Framework для создания классов модели базы данных, см. Мой руководстве Creating Model Classes with Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c5451-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>


## <a name="the-controller-class"></a><span data-ttu-id="c5451-132">Класс контроллера</span><span class="sxs-lookup"><span data-stu-id="c5451-132">The Controller Class</span></span>

<span data-ttu-id="c5451-133">Мы используем контроллера Home список фильмов и создание новых фильмов.</span><span class="sxs-lookup"><span data-stu-id="c5451-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="c5451-134">В листинге 1 содержится код для этого класса.</span><span class="sxs-lookup"><span data-stu-id="c5451-134">The code for this class is contained in Listing 1.</span></span>

**<span data-ttu-id="c5451-135">Listing 1 - Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="c5451-135">Listing 1 - Controllers\HomeController.cs</span></span>**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="c5451-136">Класс контроллера Home в листинге 1 содержит два действия Create().</span><span class="sxs-lookup"><span data-stu-id="c5451-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="c5451-137">Первое действие отображает HTML-форма для создания новый фильм.</span><span class="sxs-lookup"><span data-stu-id="c5451-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="c5451-138">Второе действие Create() выполняет фактическое Вставка новый фильм в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c5451-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="c5451-139">Второе действие Create() вызывается, когда форму с первое действие Create() отправляется на сервер.</span><span class="sxs-lookup"><span data-stu-id="c5451-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="c5451-140">Обратите внимание на то, что второе действие Create() содержит следующие строки кода:</span><span class="sxs-lookup"><span data-stu-id="c5451-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="c5451-141">Свойство IsValid возвращает значение false, если возникает ошибка проверки.</span><span class="sxs-lookup"><span data-stu-id="c5451-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="c5451-142">В этом случае следует создать представление, содержащее HTML-форма для создания фильма отобразится.</span><span class="sxs-lookup"><span data-stu-id="c5451-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="c5451-143">Создание разделяемого класса</span><span class="sxs-lookup"><span data-stu-id="c5451-143">Creating a Partial Class</span></span>

<span data-ttu-id="c5451-144">Класс Movie создается платформой Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c5451-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="c5451-145">Вы увидите код для класса фильма, если развернуть файл MoviesDBModel.edmx в окне обозревателя решений и откройте файл MoviesDBModel.Designer.cs в редакторе кода (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="c5451-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>


[![T<span data-ttu-id="c5451-146">код для сущности фильма]</span><span class="sxs-lookup"><span data-stu-id="c5451-146">he code for the Movie entity]</span></span>(validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

<span data-ttu-id="c5451-147">**Рис. 02**: Код для сущности фильма ([Просмотр полноразмерного изображения](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="c5451-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>


<span data-ttu-id="c5451-148">Класс Movie — это разделяемый класс.</span><span class="sxs-lookup"><span data-stu-id="c5451-148">The Movie class is a partial class.</span></span> <span data-ttu-id="c5451-149">Это означает, что мы можем добавить еще один разделяемый класс с тем же именем, чтобы расширить функциональные возможности класса Movie.</span><span class="sxs-lookup"><span data-stu-id="c5451-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="c5451-150">Мы добавим логику проверки в новый разделяемый класс.</span><span class="sxs-lookup"><span data-stu-id="c5451-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="c5451-151">Добавление класса в листинге 2 папку Models.</span><span class="sxs-lookup"><span data-stu-id="c5451-151">Add the class in Listing 2 to the Models folder.</span></span>

**<span data-ttu-id="c5451-152">Listing 2 - Models\Movie.cs</span><span class="sxs-lookup"><span data-stu-id="c5451-152">Listing 2 - Models\Movie.cs</span></span>**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="c5451-153">Обратите внимание, что класс в листинге 2 включает *частичного* модификатор.</span><span class="sxs-lookup"><span data-stu-id="c5451-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="c5451-154">Все методы и свойства, добавляемые к этому классу становятся частью класс Movie, созданным Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c5451-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="c5451-155">Добавление OnChanging и OnChanged частичных методов</span><span class="sxs-lookup"><span data-stu-id="c5451-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="c5451-156">Когда платформа Entity Framework создает класс сущностей, Entity Framework автоматически добавляет разделяемые методы в класс.</span><span class="sxs-lookup"><span data-stu-id="c5451-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="c5451-157">Платформа Entity Framework создает OnChanging и OnChanged разделяемые методы, соответствующие каждому свойству класса.</span><span class="sxs-lookup"><span data-stu-id="c5451-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="c5451-158">В случае класс Movie Entity Framework создает следующие методы:</span><span class="sxs-lookup"><span data-stu-id="c5451-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="c5451-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="c5451-159">OnIdChanging</span></span>
- <span data-ttu-id="c5451-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="c5451-160">OnIdChanged</span></span>
- <span data-ttu-id="c5451-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="c5451-161">OnTitleChanging</span></span>
- <span data-ttu-id="c5451-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="c5451-162">OnTitleChanged</span></span>
- <span data-ttu-id="c5451-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="c5451-163">OnDirectorChanging</span></span>
- <span data-ttu-id="c5451-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="c5451-164">OnDirectorChanged</span></span>
- <span data-ttu-id="c5451-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="c5451-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="c5451-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="c5451-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="c5451-167">Метод OnChanging вызывается правой перед изменением соответствующего свойства.</span><span class="sxs-lookup"><span data-stu-id="c5451-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="c5451-168">Метод OnChanged вызывается справа после изменения свойства.</span><span class="sxs-lookup"><span data-stu-id="c5451-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="c5451-169">Можно воспользоваться преимуществами эти разделяемые методы для добавления логики проверки класс Movie.</span><span class="sxs-lookup"><span data-stu-id="c5451-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="c5451-170">Обновление класс Movie в листинге 3 проверяет, что в свойствах Title и директор назначаются непустых значений.</span><span class="sxs-lookup"><span data-stu-id="c5451-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c5451-171">Разделяемый метод — это метод, определенный в классе, который не является обязательным для реализации.</span><span class="sxs-lookup"><span data-stu-id="c5451-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="c5451-172">Если не реализовать разделяемый метод, компилятор удаляет сигнатуру метода, и все вызовы метода таким образом являются без затрат времени выполнения, связанных с разделяемого метода.</span><span class="sxs-lookup"><span data-stu-id="c5451-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="c5451-173">В редакторе кода Visual Studio, можно добавить разделяемый метод, введя ключевое слово *частичного* за которыми следует пробел, чтобы просмотреть список частичных представлений для реализации.</span><span class="sxs-lookup"><span data-stu-id="c5451-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>


**<span data-ttu-id="c5451-174">Listing 3 - Models\Movie.cs</span><span class="sxs-lookup"><span data-stu-id="c5451-174">Listing 3 - Models\Movie.cs</span></span>**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="c5451-175">Например, если вы попытаетесь назначить пустую строку в свойстве Title, тогда сообщение об ошибке назначается словарь с именем \_ошибки.</span><span class="sxs-lookup"><span data-stu-id="c5451-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="c5451-176">На этом этапе ничего не произойдет при пустая строка присвоить свойству заголовка и ошибка добавляется к закрытому \_полей ошибок.</span><span class="sxs-lookup"><span data-stu-id="c5451-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="c5451-177">Нам нужно реализовать интерфейс IDataErrorInfo для предоставления этих ошибок проверки в ASP.NET MVC Framework.</span><span class="sxs-lookup"><span data-stu-id="c5451-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="c5451-178">Вы реализуете интерфейс IDataErrorInfo</span><span class="sxs-lookup"><span data-stu-id="c5451-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="c5451-179">Интерфейс IDataErrorInfo было частью .NET framework с первой версии.</span><span class="sxs-lookup"><span data-stu-id="c5451-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="c5451-180">Этот интерфейс является очень простой интерфейс:</span><span class="sxs-lookup"><span data-stu-id="c5451-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="c5451-181">Если класс реализует интерфейс IDataErrorInfo, платформа ASP.NET MVC будет использовать этот интерфейс при создании экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c5451-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="c5451-182">Например контроллер Home Create() действие принимает экземпляр класса Movie:</span><span class="sxs-lookup"><span data-stu-id="c5451-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="c5451-183">Платформа ASP.NET MVC создает экземпляр фильма, передается в действие Create() с помощью связывателя модели (DefaultModelBinder).</span><span class="sxs-lookup"><span data-stu-id="c5451-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="c5451-184">Связыватель модели отвечает за создание экземпляра объекта фильма, привязывая поля формы HTML для экземпляра объекта фильма.</span><span class="sxs-lookup"><span data-stu-id="c5451-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="c5451-185">DefaultModelBinder обнаруживает ли класс реализует интерфейс IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="c5451-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="c5451-186">Если класс реализует этот интерфейс связывателя модели вызывает IDataErrorInfo.this индексатор для каждого свойства класса.</span><span class="sxs-lookup"><span data-stu-id="c5451-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="c5451-187">Если индексатор возвращает сообщение об ошибке это сообщение об ошибке для моделирования состояние автоматически добавит связывателя модели.</span><span class="sxs-lookup"><span data-stu-id="c5451-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="c5451-188">DefaultModelBinder также проверяет свойство IDataErrorInfo.Error.</span><span class="sxs-lookup"><span data-stu-id="c5451-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="c5451-189">Это свойство предназначено для представления ошибок проверки отличных от свойств, связанный с классом.</span><span class="sxs-lookup"><span data-stu-id="c5451-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="c5451-190">Например может потребоваться применить правило проверки, который зависит от значения нескольких свойств класса фильма.</span><span class="sxs-lookup"><span data-stu-id="c5451-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="c5451-191">В этом случае возвратит ошибку проверки из свойства ошибки.</span><span class="sxs-lookup"><span data-stu-id="c5451-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="c5451-192">Обновленный класс Movie в листинге 4 реализует интерфейс IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="c5451-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

**<span data-ttu-id="c5451-193">Листинг 4 - Models\Movie.cs (реализует IDataErrorInfo)</span><span class="sxs-lookup"><span data-stu-id="c5451-193">Listing 4 - Models\Movie.cs (implements IDataErrorInfo)</span></span>**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="c5451-194">В листинге 4 проверяет свойство индексатора \_коллекцию ошибок, чтобы увидеть, если он содержит ключ, который соответствует имени свойства, передаваемое индексатора.</span><span class="sxs-lookup"><span data-stu-id="c5451-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="c5451-195">При возникновении ошибки проверки, связанные со свойством, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="c5451-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="c5451-196">Не нужно каким-либо образом использовать измененный класс Movie контроллер Home.</span><span class="sxs-lookup"><span data-stu-id="c5451-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="c5451-197">Страницы, отображаемой на рис. 3 показано, что произойдет, если значение не указано для заголовка или Директор полей формы.</span><span class="sxs-lookup"><span data-stu-id="c5451-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>


[![C<span data-ttu-id="c5451-198">методы действий ается автоматически]</span><span class="sxs-lookup"><span data-stu-id="c5451-198">reating action methods automatically]</span></span>(validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

<span data-ttu-id="c5451-199">**Рис 03**: Форма с отсутствующими значениями ([Просмотр полноразмерного изображения](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c5451-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>


<span data-ttu-id="c5451-200">Обратите внимание на то, что значение DateReleased проверяется автоматически.</span><span class="sxs-lookup"><span data-stu-id="c5451-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="c5451-201">Так как свойство DateReleased не допускает значения NULL, DefaultModelBinder выдает ошибку проверки для этого свойства автоматически при его не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="c5451-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="c5451-202">Если вы хотите изменить сообщение об ошибке для свойства DateReleased необходимо создать настраиваемый связыватель модели.</span><span class="sxs-lookup"><span data-stu-id="c5451-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="c5451-203">Сводка</span><span class="sxs-lookup"><span data-stu-id="c5451-203">Summary</span></span>

<span data-ttu-id="c5451-204">В этом руководстве вы узнали, как использовать интерфейс IDataErrorInfo для формирования сообщений об ошибках проверки.</span><span class="sxs-lookup"><span data-stu-id="c5451-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="c5451-205">Во-первых мы создали разделяемый класс Movie, который расширяет функциональность разделяемый класс Movie, созданным Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c5451-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="c5451-206">Затем мы добавили логику проверки в фильма OnTitleChanging() и OnDirectorChanging() частичные методы класса.</span><span class="sxs-lookup"><span data-stu-id="c5451-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="c5451-207">Наконец мы реализовали интерфейс IDataErrorInfo, чтобы предоставить эти сообщения проверки в ASP.NET MVC Framework.</span><span class="sxs-lookup"><span data-stu-id="c5451-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c5451-208">[Назад](performing-simple-validation-cs.md)
> [Вперед](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c5451-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>
