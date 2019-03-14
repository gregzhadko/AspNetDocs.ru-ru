---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: Интеграция Datepicker пользовательского интерфейса JQuery с помощью привязки модели и веб-форм | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств показано основными аспектами с помощью привязки модели с проектом веб-форм ASP.NET. Привязка модели позволяет взаимодействие с данными более прямой-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: ff1b17295c58d40d55bdcd4346b83121b579bb4c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030961"
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="9d51b-104">Интеграция Datepicker пользовательского интерфейса JQuery с помощью привязки модели и веб-форм</span><span class="sxs-lookup"><span data-stu-id="9d51b-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>
====================
<span data-ttu-id="9d51b-105">по [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9d51b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9d51b-106">В этой серии руководств показано основными аспектами с помощью привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9d51b-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="9d51b-107">Привязка модели упрощает взаимодействие с данными более эффективную чем работа с данными объектов источника (например, элемент управления ObjectDataSource и SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="9d51b-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="9d51b-108">Эта серия начинается с вводный материал и перемещает до более продвинутых в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="9d51b-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="9d51b-109">Этом руководстве показано, как добавить пользовательский Интерфейс JQuery [Datepicker мини-приложение](http://jqueryui.com/datepicker/) для веб-формы и использование модели привязки для обновления базы данных с выбранным значением.</span><span class="sxs-lookup"><span data-stu-id="9d51b-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="9d51b-110">Этот учебник основан на проект, созданный в [первый](retrieving-data.md) и [второй](updating-deleting-and-creating-data.md) части серии.</span><span class="sxs-lookup"><span data-stu-id="9d51b-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="9d51b-111">Вы можете [загрузить](https://go.microsoft.com/fwlink/?LinkId=286116) весь проект полностью на C# или Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="9d51b-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="9d51b-112">Загружаемый код работает с Visual Studio 2012 или Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9d51b-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="9d51b-113">Он использует шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2013, в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9d51b-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="9d51b-114">Вы создадите</span><span class="sxs-lookup"><span data-stu-id="9d51b-114">What you'll build</span></span>

<span data-ttu-id="9d51b-115">В этом руководстве вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9d51b-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="9d51b-116">Добавление свойства в модели для записи учащегося Дата регистрации</span><span class="sxs-lookup"><span data-stu-id="9d51b-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="9d51b-117">Разрешить пользователю выбрать дату регистрации с помощью мини-приложение Datepicker пользовательского интерфейса JQuery</span><span class="sxs-lookup"><span data-stu-id="9d51b-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="9d51b-118">Принудительное применение правил проверки для Дата регистрации</span><span class="sxs-lookup"><span data-stu-id="9d51b-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="9d51b-119">Datepicker пользовательского интерфейса JQuery мини-приложение позволяет пользователям легко выбрать дату из календаря, возникающего, когда пользователь взаимодействует с полем.</span><span class="sxs-lookup"><span data-stu-id="9d51b-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="9d51b-120">Использование этого мини-приложения может быть более удобным для пользователей, чем вручную вводить даты.</span><span class="sxs-lookup"><span data-stu-id="9d51b-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="9d51b-121">Интеграция Datepicker мини-приложения в страницу, которая использует привязку модели для данных операций требуется только небольшой объем дополнительной работы.</span><span class="sxs-lookup"><span data-stu-id="9d51b-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="9d51b-122">Добавить новое свойство в модель</span><span class="sxs-lookup"><span data-stu-id="9d51b-122">Add a new property to the model</span></span>

<span data-ttu-id="9d51b-123">Во-первых, вы добавите **Datetime** свойство для обучения модели и перенести это изменение в базе данных.</span><span class="sxs-lookup"><span data-stu-id="9d51b-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="9d51b-124">Откройте **UniversityModels.cs**и добавьте выделенный код в модель Student.</span><span class="sxs-lookup"><span data-stu-id="9d51b-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="9d51b-125">**RangeAttribute** включается для применения правил проверки для свойства.</span><span class="sxs-lookup"><span data-stu-id="9d51b-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="9d51b-126">В этом учебнике предполагается, что университета Contoso была основана на 1 января 2013 г, и поэтому более ранние даты регистрации недопустимы.</span><span class="sxs-lookup"><span data-stu-id="9d51b-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="9d51b-127">В окне управления пакетами, добавить миграцию, выполнив команду **AddEnrollmentDate добавьте миграции**.</span><span class="sxs-lookup"><span data-stu-id="9d51b-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="9d51b-128">Обратите внимание на то, что код миграции добавляет новый столбец даты и времени на таблицу Student.</span><span class="sxs-lookup"><span data-stu-id="9d51b-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="9d51b-129">В соответствии с значением, которое указано в RangeAttribute, добавьте значение по умолчанию для нового столбца, как показано в выделенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="9d51b-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="9d51b-130">Сохраните изменения в файл для миграции.</span><span class="sxs-lookup"><span data-stu-id="9d51b-130">Save your change to the migration file.</span></span>

<span data-ttu-id="9d51b-131">Необходимо повторно заполнить данными.</span><span class="sxs-lookup"><span data-stu-id="9d51b-131">You do not need to seed the data again.</span></span> <span data-ttu-id="9d51b-132">Таким образом, откройте **Configuration.cs** в папку Migrations и удалите или закомментируйте код в **начальное значение** метод.</span><span class="sxs-lookup"><span data-stu-id="9d51b-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="9d51b-133">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="9d51b-133">Save and close the file.</span></span>

<span data-ttu-id="9d51b-134">Теперь выполните команду **обновления базы данных**.</span><span class="sxs-lookup"><span data-stu-id="9d51b-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="9d51b-135">Обратите внимание на то, что этот столбец существует в базе данных и всех существующих записей имеют значения по умолчанию для параметра EnrollmentDate.</span><span class="sxs-lookup"><span data-stu-id="9d51b-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="9d51b-136">Добавление динамических элементов управления для Дата регистрации</span><span class="sxs-lookup"><span data-stu-id="9d51b-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="9d51b-137">Теперь вы добавите элементы управления для отображения и редактирования и дату зачисления.</span><span class="sxs-lookup"><span data-stu-id="9d51b-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="9d51b-138">На этом этапе значение изменяется в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="9d51b-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="9d51b-139">Далее в этом руководстве текстового поля изменится на JQuery Datepicker мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="9d51b-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="9d51b-140">Во-первых, важно отметить, что не нужно вносить изменения в **AddStudent.aspx** файла.</span><span class="sxs-lookup"><span data-stu-id="9d51b-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="9d51b-141">Элемент управления DynamicEntity автоматически будет отображать новое свойство.</span><span class="sxs-lookup"><span data-stu-id="9d51b-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="9d51b-142">Откройте **Students.aspx**и добавьте следующий выделенный код.</span><span class="sxs-lookup"><span data-stu-id="9d51b-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="9d51b-143">Запустите приложение и обратите внимание на то, что значение даты регистрации можно задать путем ввода даты.</span><span class="sxs-lookup"><span data-stu-id="9d51b-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="9d51b-144">При добавлении нового учащегося:</span><span class="sxs-lookup"><span data-stu-id="9d51b-144">When adding a new student:</span></span>

![даты](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="9d51b-146">Или редактировании существующего значения:</span><span class="sxs-lookup"><span data-stu-id="9d51b-146">Or, editing an existing value:</span></span>

![изменить дату](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="9d51b-148">Введя works даты, но он может оказаться обслуживание клиентов, которые вы хотите предоставить.</span><span class="sxs-lookup"><span data-stu-id="9d51b-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="9d51b-149">В следующем разделе вы включите выбора даты через календаря.</span><span class="sxs-lookup"><span data-stu-id="9d51b-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="9d51b-150">Установите пакет NuGet для работы с помощью пользовательского интерфейса JQuery</span><span class="sxs-lookup"><span data-stu-id="9d51b-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="9d51b-151">**Пользовательского интерфейса сок** простая интеграция пользовательского интерфейса JQuery мини-приложений в веб-приложения с помощью пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="9d51b-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="9d51b-152">Чтобы использовать этот пакет, установите его через NuGet.</span><span class="sxs-lookup"><span data-stu-id="9d51b-152">To use this package, install it through NuGet.</span></span>

![Добавление пользовательского интерфейса сок](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="9d51b-154">Версия пользовательского интерфейса сок, который вы устанавливаете может конфликтовать с версии JQuery в приложении.</span><span class="sxs-lookup"><span data-stu-id="9d51b-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="9d51b-155">Прежде чем продолжить с этим руководством, попробуйте запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9d51b-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="9d51b-156">Если возникла ошибка JavaScript, необходимо согласовать версии JQuery.</span><span class="sxs-lookup"><span data-stu-id="9d51b-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="9d51b-157">Можно добавить ожидаемую версию служб JQuery в папке скриптов (версия 1.8.2 во время написания этого учебника), или в Site.master укажите путь к файлу JQuery.</span><span class="sxs-lookup"><span data-stu-id="9d51b-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="9d51b-158">Настройка шаблона даты и времени для включения Datepicker мини-приложения</span><span class="sxs-lookup"><span data-stu-id="9d51b-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="9d51b-159">Вы добавите Datepicker мини-приложения в шаблон динамических данных для редактирования значения даты и времени.</span><span class="sxs-lookup"><span data-stu-id="9d51b-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="9d51b-160">Добавление мини-приложения в шаблон, он автоматически отображается в форме для добавления нового учащегося, а также в представлении в виде сетки для редактирования учащихся.</span><span class="sxs-lookup"><span data-stu-id="9d51b-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="9d51b-161">Откройте **DateTime\_Edit.ascx платформы**и добавьте следующий выделенный код.</span><span class="sxs-lookup"><span data-stu-id="9d51b-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="9d51b-162">В файле кода будет задайте минимальное и максимальное даты для элемента управления DatePicker.</span><span class="sxs-lookup"><span data-stu-id="9d51b-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="9d51b-163">Задавая эти значения, позволит пользователям перейти к недопустимые даты.</span><span class="sxs-lookup"><span data-stu-id="9d51b-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="9d51b-164">Вы получите минимальное и максимальное значения из **RangeAttribute** на свойство типа DateTime, если он указан.</span><span class="sxs-lookup"><span data-stu-id="9d51b-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="9d51b-165">Откройте **DateTime\_Edit.ascx.cs**и добавьте следующий выделенный код на страницу\_метод Load.</span><span class="sxs-lookup"><span data-stu-id="9d51b-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="9d51b-166">Запустите веб-приложение и перейдите на страницу AddStudent.</span><span class="sxs-lookup"><span data-stu-id="9d51b-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="9d51b-167">Укажите значения для полей и обратите внимание, что если щелкнуть текстовое поле для регистрации даты календаря.</span><span class="sxs-lookup"><span data-stu-id="9d51b-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![Выбор даты](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="9d51b-169">Выберите дату, а затем нажмите кнопку **вставить**.</span><span class="sxs-lookup"><span data-stu-id="9d51b-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="9d51b-170">RangeAttribute принудительную проверку на сервере.</span><span class="sxs-lookup"><span data-stu-id="9d51b-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="9d51b-171">Установив свойство minDate Datepicker, также применить проверку на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="9d51b-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="9d51b-172">Календарь не позволяющие переходить к даты до значение minDate.</span><span class="sxs-lookup"><span data-stu-id="9d51b-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="9d51b-173">При редактировании записи в представлении в виде сетки, календарь также отображается.</span><span class="sxs-lookup"><span data-stu-id="9d51b-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![DatePicker в GridView](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="9d51b-175">Заключение</span><span class="sxs-lookup"><span data-stu-id="9d51b-175">Conclusion</span></span>

<span data-ttu-id="9d51b-176">В этом руководстве вы узнали, как включить JQuery мини-приложения в веб-форму, которая использует привязку модели.</span><span class="sxs-lookup"><span data-stu-id="9d51b-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="9d51b-177">В следующем [руководстве](using-query-string-values-to-retrieve-data.md), будет использовать значения строки запроса, при выборе данных.</span><span class="sxs-lookup"><span data-stu-id="9d51b-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9d51b-178">[Назад](sorting-paging-and-filtering-data.md)
> [Вперед](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="9d51b-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
