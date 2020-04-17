---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: Проверка с помощью валидаторов аннотации данных (СЗ) Документы Майкрософт
author: rick-anderson
description: Воспользуйтесь преимуществами модели аннотации данных Binder для выполнения проверки в ASP.NET mVC-приложении. Узнайте, как использовать различные типы валидатора...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 28ea52b9b412431d59d7afdd1c7cce93a50a7e2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542681"
---
# <a name="validation-with-the-data-annotation-validators-c"></a><span data-ttu-id="5b784-104">Проверка с помощью проверяющих элементов управления заметок к данным (C#)</span><span class="sxs-lookup"><span data-stu-id="5b784-104">Validation with the Data Annotation Validators (C#)</span></span>

<span data-ttu-id="5b784-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5b784-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5b784-106">Воспользуйтесь преимуществами модели аннотации данных Binder для выполнения проверки в ASP.NET mVC-приложении.</span><span class="sxs-lookup"><span data-stu-id="5b784-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="5b784-107">Узнайте, как использовать различные типы атрибутов валидатора и работать с ними в рамочной системе сущности Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5b784-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="5b784-108">В этом уроке вы узнаете, как использовать валидаторы аннотации данных для выполнения проверки в ASP.NET mVC-приложении.</span><span class="sxs-lookup"><span data-stu-id="5b784-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="5b784-109">Преимущество использования валидаторов аннотации данных заключается в том, что они позволяют выполнять проверку, просто добавляя один или несколько атрибутов, таких как атрибут «Требуемый» или «Струнный длина», в свойство класса.</span><span class="sxs-lookup"><span data-stu-id="5b784-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="5b784-110">Прежде чем использовать валидаторы аннотации данных, необходимо загрузить модель "Биндер" по каннотам данных.</span><span class="sxs-lookup"><span data-stu-id="5b784-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="5b784-111">Вы можете скачать данные Аннотации Модель Binder Образец с веб-сайта CodePlex, нажав [здесь](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span><span class="sxs-lookup"><span data-stu-id="5b784-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="5b784-112">Важно понимать, что модель наятивов данных Binder не является официальной частью платформы Microsoft ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5b784-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="5b784-113">Хотя модель наятирований данных Была создана командой Microsoft ASP.NET MVC, корпорация Майкрософт не предлагает официальную поддержку продуктов для модели данных Binder, описанной и используемой в этом уроке.</span><span class="sxs-lookup"><span data-stu-id="5b784-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="5b784-114">Использование связующего модели аннотации данных</span><span class="sxs-lookup"><span data-stu-id="5b784-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="5b784-115">Для того, чтобы использовать модельный разбойники данных в ASP.NET mVC-приложении, сначала необходимо добавить ссылку на сборку Microsoft.Web.Mvc.DataAnnotations.dll и сборку System.ComponentModel.DataAnnotations.dll.</span><span class="sxs-lookup"><span data-stu-id="5b784-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="5b784-116">Выберите вариант меню **Project, добавьте справку**.</span><span class="sxs-lookup"><span data-stu-id="5b784-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="5b784-117">Далее нажмите на вкладку **«Обзор»** и просмотрите место, где вы скачали (и расстегнули) образец модели Binder **(см. рисунок 1).**</span><span class="sxs-lookup"><span data-stu-id="5b784-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

<span data-ttu-id="5b784-118">**Рисунок 1**: Добавление ссылки на данные Аннотации модель Биндер ([Нажмите, чтобы просмотреть полноразмерное изображение](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5b784-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span></span>

<span data-ttu-id="5b784-119">Выберите сборку Microsoft.Web.Mvc.DataAnnotations.dll и System.ComponentModel.DataAnnotations.dll сборки и нажмите **кнопку OK.**</span><span class="sxs-lookup"><span data-stu-id="5b784-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="5b784-120">Вы не можете использовать сборку System.ComponentModel.DataAnnotations.dll, включенную в пакет рамочной службы .NET 1 с моделью Binder.</span><span class="sxs-lookup"><span data-stu-id="5b784-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="5b784-121">Вы должны использовать версию Сборки System.ComponentModel.DataAnnotations.dll, включенную в загрузку модели модели Binder.</span><span class="sxs-lookup"><span data-stu-id="5b784-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="5b784-122">Наконец, необходимо зарегистрировать модель DataAnnotations Binder в файле Global.asax.</span><span class="sxs-lookup"><span data-stu-id="5b784-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="5b784-123">Добавьте следующую строку\_кода в обработчик события\_Application Start() так, чтобы метод «Старт приложения») выглядел следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5b784-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

<span data-ttu-id="5b784-124">Эта строка кода регистрирует ataAnnotationsModelInder в качестве связующего элемента модели по умолчанию для всего приложения MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5b784-124">This line of code registers the ataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="5b784-125">Использование атрибутов валидатора аннотации данных</span><span class="sxs-lookup"><span data-stu-id="5b784-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="5b784-126">При использовании модели обновилий данных Inder вы используете атрибуты валидатора для выполнения проверки.</span><span class="sxs-lookup"><span data-stu-id="5b784-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="5b784-127">В пространстве имен System.ComponentModel.DataAnnotations включены следующие атрибуты валидатора:</span><span class="sxs-lookup"><span data-stu-id="5b784-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="5b784-128">Диапазон - Позволяет проверить, падает ли значение свойства между определенным диапазоном значений.</span><span class="sxs-lookup"><span data-stu-id="5b784-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="5b784-129">RegularExpression - Позволяет проверить, соответствует ли значение свойства определенному шаблону регулярного выражения.</span><span class="sxs-lookup"><span data-stu-id="5b784-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="5b784-130">Требуется - Позволяет пометить свойство по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="5b784-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="5b784-131">StringLength - Позволяет указать максимальную длину для свойства строки.</span><span class="sxs-lookup"><span data-stu-id="5b784-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="5b784-132">Проверка — базовый класс для всех атрибутов валидатора.</span><span class="sxs-lookup"><span data-stu-id="5b784-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5b784-133">Если ваши потребности в проверке не удовлетворяются ни одним из стандартных валидаторов, то у вас всегда есть возможность создания пользовательского атрибута валидатора, нанаследовав новый атрибут валидатора из базового атрибута валидации.</span><span class="sxs-lookup"><span data-stu-id="5b784-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="5b784-134">Класс продукта в **листинге 1** иллюстрирует, как использовать эти атрибуты валидатора.</span><span class="sxs-lookup"><span data-stu-id="5b784-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="5b784-135">Свойства имени, описания и UnitPrice помечены по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="5b784-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="5b784-136">Свойство имени должно иметь длину строки менее 10 символов.</span><span class="sxs-lookup"><span data-stu-id="5b784-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="5b784-137">Наконец, свойство UnitPrice должно соответствовать шаблону регулярного выражения, представляющего сумму в валюте.</span><span class="sxs-lookup"><span data-stu-id="5b784-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

<span data-ttu-id="5b784-138">**Список 1**: Модели»Продукт.cs</span><span class="sxs-lookup"><span data-stu-id="5b784-138">**Listing 1**: Models\Product.cs</span></span>

<span data-ttu-id="5b784-139">Класс продукта иллюстрирует, как использовать один дополнительный атрибут: атрибут DisplayName.</span><span class="sxs-lookup"><span data-stu-id="5b784-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="5b784-140">Атрибут DisplayName позволяет изменять имя свойства при отображении свойства в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5b784-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="5b784-141">Вместо отображения сообщения об ошибке "Требуется поле UnitPrice" можно отобразить сообщение об ошибке "Требуется поле цены".</span><span class="sxs-lookup"><span data-stu-id="5b784-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5b784-142">Если вы хотите полностью настроить сообщение об ошибке, отображаемое валидатором, то вы можете назначить пользовательское сообщение об ошибке свойству ErrorMessage валидатора следующим образом:`<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="5b784-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="5b784-143">Вы можете использовать класс продукта в **листинге 1** с действием контроллера Create() в **листинге 2**.</span><span class="sxs-lookup"><span data-stu-id="5b784-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="5b784-144">Это действие контроллера отображает представление «Создание», когда состояние модели содержит ошибки.</span><span class="sxs-lookup"><span data-stu-id="5b784-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

<span data-ttu-id="5b784-145">**Список 2**: Контролеры/ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="5b784-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="5b784-146">Наконец, вы можете создать представление в **листинге 3,** нажав на действие Create() и выбрав вариант меню **Добавить вид.**</span><span class="sxs-lookup"><span data-stu-id="5b784-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="5b784-147">Создайте сильно типифицированный вид с классом продукта в качестве класса модели.</span><span class="sxs-lookup"><span data-stu-id="5b784-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="5b784-148">Выберите **Создать** из списка выпадающих просмотров содержимого (см. **рисунок 2).**</span><span class="sxs-lookup"><span data-stu-id="5b784-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

<span data-ttu-id="5b784-149">**Рисунок 2**: Добавление представления создания</span><span class="sxs-lookup"><span data-stu-id="5b784-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

<span data-ttu-id="5b784-150">**Список 3**: Просмотры »Продукт»Создать.aspx</span><span class="sxs-lookup"><span data-stu-id="5b784-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5b784-151">Удалите поле Id из формы «Создание», генерируемой опцией меню **Add View.**</span><span class="sxs-lookup"><span data-stu-id="5b784-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="5b784-152">Поскольку поле Id соответствует столбцу identity, вы не хотите, чтобы пользователи могли вводить значение для этого поля.</span><span class="sxs-lookup"><span data-stu-id="5b784-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="5b784-153">Если вы отправляете форму для создания продукта и не вводите значения для требуемых полей, отображаются сообщения об ошибке проверки на **рисунке 3.**</span><span class="sxs-lookup"><span data-stu-id="5b784-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

<span data-ttu-id="5b784-154">**Рисунок 3**: Отсутствующие необходимые поля</span><span class="sxs-lookup"><span data-stu-id="5b784-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="5b784-155">Если вы вводите недействительную сумму валюты, отображается сообщение об ошибке на **рисунке 4.**</span><span class="sxs-lookup"><span data-stu-id="5b784-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

<span data-ttu-id="5b784-156">**Рисунок 4**: Недействительная сумма валюты</span><span class="sxs-lookup"><span data-stu-id="5b784-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="5b784-157">Использование валидаторов аннотации данных с рамочной системой entity</span><span class="sxs-lookup"><span data-stu-id="5b784-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="5b784-158">Если вы используете рамочную программу Microsoft Entity для генерации классов моделей данных, то вы не можете применять атрибуты валидатора непосредственно к классам.</span><span class="sxs-lookup"><span data-stu-id="5b784-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="5b784-159">Поскольку проектировщик сущности создает классы моделей, любые изменения, внесенные в классы моделей, будут перезаписаны при следующем внесении изменений в проект.»</span><span class="sxs-lookup"><span data-stu-id="5b784-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="5b784-160">Если вы хотите использовать валидаторы с классами, генерируемыми Рамочной системой сущности, то необходимо создать классы мета-данных.</span><span class="sxs-lookup"><span data-stu-id="5b784-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="5b784-161">Валидаторы применяются к классу мета данных вместо того, чтобы применять валидаторы к реальному классу.</span><span class="sxs-lookup"><span data-stu-id="5b784-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="5b784-162">Например, представьте, что вы создали класс Movie с помощью рамочной системы entity (см. **рисунок 5).**</span><span class="sxs-lookup"><span data-stu-id="5b784-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="5b784-163">Представьте себе, кроме того, что вы хотите сделать название фильма и директор свойства необходимых свойств.</span><span class="sxs-lookup"><span data-stu-id="5b784-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="5b784-164">В этом случае можно создать частичный класс и класс мета данных в **листинге 4.**</span><span class="sxs-lookup"><span data-stu-id="5b784-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

<span data-ttu-id="5b784-165">**Рисунок 5**: Класс фильма, сгенерированный Рамочной системой entity</span><span class="sxs-lookup"><span data-stu-id="5b784-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

<span data-ttu-id="5b784-166">**Список 4**: Модели»Movie.cs</span><span class="sxs-lookup"><span data-stu-id="5b784-166">**Listing 4**: Models\Movie.cs</span></span>

<span data-ttu-id="5b784-167">Файл в **листинге 4** содержит два класса под названием Movie и MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="5b784-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="5b784-168">Класс Фильма является частичным классом.</span><span class="sxs-lookup"><span data-stu-id="5b784-168">The Movie class is a partial class.</span></span> <span data-ttu-id="5b784-169">Он соответствует частичному классу, генерируемому Рамочной системой сущности, которая содержится в файле DataModel.Designer.vb.</span><span class="sxs-lookup"><span data-stu-id="5b784-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="5b784-170">В настоящее время фреймворк .NET не поддерживает частичные свойства.</span><span class="sxs-lookup"><span data-stu-id="5b784-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="5b784-171">Таким образом, нет возможности применить атрибуты валидатора к свойствам класса Movie, определенным в файле DataModel.Designer.vb, применяя атрибуты валидатора к свойствам класса Movie, определенным в файле в **листинге 4**.</span><span class="sxs-lookup"><span data-stu-id="5b784-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="5b784-172">Обратите внимание, что частичное класс Movie украшен атрибутом MetadataType, который указывает на класс MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="5b784-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="5b784-173">Класс MovieMetaData содержит прокси-свойства для свойств класса Movie.</span><span class="sxs-lookup"><span data-stu-id="5b784-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="5b784-174">Атрибуты валидатора применяются к свойствам класса MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="5b784-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="5b784-175">Свойства Title, Director и DateReleased помечены как требуемые свойства.</span><span class="sxs-lookup"><span data-stu-id="5b784-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="5b784-176">Свойство Директора должно быть присвоено строке, содержащей менее 5 символов.</span><span class="sxs-lookup"><span data-stu-id="5b784-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="5b784-177">Наконец, атрибут DisplayName применяется к свойству DateReleased для отображения сообщения об ошибке, например" Требуется поле Типа Наиболее выпущенного поля.</span><span class="sxs-lookup"><span data-stu-id="5b784-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="5b784-178">вместо ошибки "Требуется поле DateReleased".</span><span class="sxs-lookup"><span data-stu-id="5b784-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5b784-179">Обратите внимание, что свойства прокси в классе MovieMetaData не должны представлять те же типы, что и соответствующие свойства в классе Movie.</span><span class="sxs-lookup"><span data-stu-id="5b784-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="5b784-180">Например, свойство директора является свойством строки в классе Movie и свойством объекта в классе MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="5b784-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="5b784-181">Страница на **рисунке 6** иллюстрирует сообщения об ошибках, возвращенные при вводе недействительных значений для свойств Movie.</span><span class="sxs-lookup"><span data-stu-id="5b784-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

<span data-ttu-id="5b784-182">**Рисунок 6**: Использование валидаторов с рамкой entity[(Нажмите, чтобы просмотреть полноразмерное изображение)](validation-with-the-data-annotation-validators-cs/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="5b784-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="5b784-183">Сводка</span><span class="sxs-lookup"><span data-stu-id="5b784-183">Summary</span></span>

<span data-ttu-id="5b784-184">В этом уроке вы узнали, как воспользоваться моделью индикации данных Binder для выполнения проверки в ASP.NET mVC-приложении.</span><span class="sxs-lookup"><span data-stu-id="5b784-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="5b784-185">Вы узнали, как использовать различные типы атрибутов валидатора, такие как атрибуты Требуемого и Струнного Длины.</span><span class="sxs-lookup"><span data-stu-id="5b784-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="5b784-186">Вы также узнали, как использовать эти атрибуты при работе с рамочной системой сущности Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5b784-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5b784-187">[Назад](validating-with-a-service-layer-cs.md)
> [Вперед](creating-model-classes-with-the-entity-framework-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5b784-187">[Previous](validating-with-a-service-layer-cs.md)
[Next](creating-model-classes-with-the-entity-framework-vb.md)</span></span>
