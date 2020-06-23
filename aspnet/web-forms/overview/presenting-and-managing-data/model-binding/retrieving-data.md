---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Извлечение и отображение данных с помощью привязки модели и веб-форм | Документация Майкрософт
author: Rick-Anderson
description: В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET. Привязка модели делает взаимодействие данных более прямым-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240741"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="e173e-104">Извлечение и отображение данных с помощью привязки модели и веб-форм</span><span class="sxs-lookup"><span data-stu-id="e173e-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="e173e-105">В этой серии руководств демонстрируются основные аспекты использования привязки модели с проектом веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e173e-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="e173e-106">Привязка модели делает взаимодействие данных более прямым, чем работа с объектами источника данных (например, ObjectDataSource или SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="e173e-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="e173e-107">Эта серия начинается с вводного материала и переходит к более сложным концепциям в последующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="e173e-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="e173e-108">Шаблон привязки модели работает с любыми технологиями доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="e173e-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="e173e-109">В этом учебнике вы будете использовать Entity Framework, но вы можете использовать технологию доступа к данным, наиболее привычную для вас.</span><span class="sxs-lookup"><span data-stu-id="e173e-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="e173e-110">Из элемента управления сервера с привязкой к данным, такого как GridView, ListView, DetailsView или FormView, указываются имена методов, используемых для выбора, обновления, удаления и создания данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="e173e-111">В этом руководстве вы укажете значение для SelectMethod.</span><span class="sxs-lookup"><span data-stu-id="e173e-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="e173e-112">В этом методе вы предоставляете логику для извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="e173e-113">В следующем руководстве будут заданы значения для UpdateMethod, DeleteMethod и InsertMethod.</span><span class="sxs-lookup"><span data-stu-id="e173e-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="e173e-114">Вы можете [скачать](https://go.microsoft.com/fwlink/?LinkId=286116) полный проект на C# или Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="e173e-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="e173e-115">Загружаемый код работает с Visual Studio 2012 и более поздними версиями.</span><span class="sxs-lookup"><span data-stu-id="e173e-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="e173e-116">В нем используется шаблон Visual Studio 2012, который немного отличается от шаблона Visual Studio 2017, показанного в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="e173e-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="e173e-117">В этом руководстве вы запускаете приложение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e173e-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="e173e-118">Вы также можете развернуть приложение на поставщике услуг размещения и сделать его доступным через Интернет.</span><span class="sxs-lookup"><span data-stu-id="e173e-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="e173e-119">Корпорация Майкрософт предлагает бесплатное веб-размещение для 10 веб-сайтов в</span><span class="sxs-lookup"><span data-stu-id="e173e-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="e173e-120">[Бесплатная пробная учетная запись Azure](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="e173e-120">[free Azure trial account](https://azure.microsoft.com/free/dotnet/).</span></span> <span data-ttu-id="e173e-121">Сведения о том, как развернуть веб-проект Visual Studio в веб-приложениях службы приложений Azure, см. в разделе [веб-развертывание ASP.NET с использованием Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) Series.</span><span class="sxs-lookup"><span data-stu-id="e173e-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="e173e-122">В этом учебнике также показано, как использовать Entity Framework Code First Migrations для развертывания базы данных SQL Server в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e173e-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e173e-123">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="e173e-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="e173e-124">Microsoft Visual Studio 2017 или Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="e173e-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="e173e-125">Этот учебник также работает с Visual Studio 2012 и Visual Studio 2013, но существуют некоторые различия в пользовательском интерфейсе и шаблоне проекта.</span><span class="sxs-lookup"><span data-stu-id="e173e-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="e173e-126">Что будет построено</span><span class="sxs-lookup"><span data-stu-id="e173e-126">What you'll build</span></span>

<span data-ttu-id="e173e-127">В этом руководстве вы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e173e-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="e173e-128">Создание объектов данных, отражающих университет с участием учащихся в курсах</span><span class="sxs-lookup"><span data-stu-id="e173e-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="e173e-129">Построение таблиц базы данных из объектов</span><span class="sxs-lookup"><span data-stu-id="e173e-129">Build database tables from the objects</span></span>
* <span data-ttu-id="e173e-130">Заполнение базы данных тестовыми данными</span><span class="sxs-lookup"><span data-stu-id="e173e-130">Populate the database with test data</span></span>
* <span data-ttu-id="e173e-131">Отображение данных в веб-форме</span><span class="sxs-lookup"><span data-stu-id="e173e-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="e173e-132">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="e173e-132">Create the project</span></span>

1. <span data-ttu-id="e173e-133">В Visual Studio 2017 создайте проект **веб-приложения ASP.NET (.NET Framework)** с именем **контосауниверситимоделбиндинг**.</span><span class="sxs-lookup"><span data-stu-id="e173e-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![создание проекта](retrieving-data/_static/image19.png)

2. <span data-ttu-id="e173e-135">Щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e173e-135">Select **OK**.</span></span> <span data-ttu-id="e173e-136">Откроется диалоговое окно для выбора шаблона.</span><span class="sxs-lookup"><span data-stu-id="e173e-136">The dialog box to select a template appears.</span></span>

   ![Выбор веб-форм](retrieving-data/_static/image3.png)

3. <span data-ttu-id="e173e-138">Выберите шаблон **веб-формы** .</span><span class="sxs-lookup"><span data-stu-id="e173e-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="e173e-139">При необходимости измените проверку подлинности для **отдельных учетных записей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e173e-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="e173e-140">Чтобы создать проект, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e173e-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="e173e-141">Изменение внешнего вида сайта</span><span class="sxs-lookup"><span data-stu-id="e173e-141">Modify site appearance</span></span>

   <span data-ttu-id="e173e-142">Внесите несколько изменений, чтобы настроить внешний вид сайта.</span><span class="sxs-lookup"><span data-stu-id="e173e-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="e173e-143">Откройте файл Site. master.</span><span class="sxs-lookup"><span data-stu-id="e173e-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="e173e-144">Измените заголовок, чтобы отобразить **университет Contoso** , а не **мое приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="e173e-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="e173e-145">Измените текст заголовка с **имени приложения** на **contoso университет**.</span><span class="sxs-lookup"><span data-stu-id="e173e-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="e173e-146">Измените ссылки заголовка навигации на соответствующие сайту.</span><span class="sxs-lookup"><span data-stu-id="e173e-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="e173e-147">Удалите ссылки для **About** и **Contact** и, вместо этого, создайте ссылку на страницу **учащихся** , которую вы создадите.</span><span class="sxs-lookup"><span data-stu-id="e173e-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="e173e-148">Сохраните site. master.</span><span class="sxs-lookup"><span data-stu-id="e173e-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="e173e-149">Добавление веб-формы для показа данных учащихся</span><span class="sxs-lookup"><span data-stu-id="e173e-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="e173e-150">В **Обозреватель решений**щелкните правой кнопкой мыши проект, выберите **Добавить** , а затем **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="e173e-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="e173e-151">В диалоговом окне **Добавление нового элемента** выберите шаблон **веб-форма с главной страницей** и назовите его **students. aspx**.</span><span class="sxs-lookup"><span data-stu-id="e173e-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![создать страницу](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="e173e-153">Нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e173e-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="e173e-154">Для главной страницы веб-формы выберите **site. master**.</span><span class="sxs-lookup"><span data-stu-id="e173e-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="e173e-155">Щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e173e-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="e173e-156">Добавление модели данных</span><span class="sxs-lookup"><span data-stu-id="e173e-156">Add the data model</span></span>

<span data-ttu-id="e173e-157">В папке **Models** добавьте класс с именем **UniversityModels.CS**.</span><span class="sxs-lookup"><span data-stu-id="e173e-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="e173e-158">Щелкните правой кнопкой мыши элемент **модели**, выберите **Добавить**, а затем **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="e173e-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="e173e-159">Откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="e173e-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="e173e-160">В меню навигации слева выберите **код**, а затем — **класс**.</span><span class="sxs-lookup"><span data-stu-id="e173e-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![Создание класса Model](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="e173e-162">Назовите класс **UniversityModels.CS** и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e173e-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="e173e-163">В этом файле определите `SchoolContext` `Student` классы,, `Enrollment` и следующим образом `Course` :</span><span class="sxs-lookup"><span data-stu-id="e173e-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="e173e-164">`SchoolContext`Класс является производным от `DbContext` , который управляет подключением к базе данных и изменениями в данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="e173e-165">В `Student` классе Обратите внимание на атрибуты, применяемые `FirstName` к `LastName` `Year` свойствам, и.</span><span class="sxs-lookup"><span data-stu-id="e173e-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="e173e-166">В этом руководстве используются эти атрибуты для проверки данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="e173e-167">Чтобы упростить код, только эти свойства помечаются атрибутами проверки данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="e173e-168">В реальном проекте атрибуты проверки применяются ко всем свойствам, которым требуется проверка.</span><span class="sxs-lookup"><span data-stu-id="e173e-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="e173e-169">Сохраните UniversityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="e173e-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="e173e-170">Настройка базы данных на основе классов</span><span class="sxs-lookup"><span data-stu-id="e173e-170">Set up the database based on classes</span></span>

<span data-ttu-id="e173e-171">В этом руководстве для создания объектов и таблиц базы данных используется [Code First migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) .</span><span class="sxs-lookup"><span data-stu-id="e173e-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="e173e-172">В этих таблицах хранятся сведения о учащихся и их курсах.</span><span class="sxs-lookup"><span data-stu-id="e173e-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="e173e-173">Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="e173e-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="e173e-174">В **консоли диспетчера пакетов**выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e173e-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="e173e-175">Если команда выполнена успешно, отображается сообщение о том, что миграция включена.</span><span class="sxs-lookup"><span data-stu-id="e173e-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![включить миграции](retrieving-data/_static/image8.png)

      <span data-ttu-id="e173e-177">Обратите внимание, что был создан файл с именем *Configuration.CS* .</span><span class="sxs-lookup"><span data-stu-id="e173e-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="e173e-178">`Configuration`Класс содержит `Seed` метод, который может заранее заполнить таблицы базы данных тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="e173e-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="e173e-179">Предварительное заполнение базы данных</span><span class="sxs-lookup"><span data-stu-id="e173e-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="e173e-180">Откройте Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="e173e-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="e173e-181">Добавьте следующий код в метод `Seed` .</span><span class="sxs-lookup"><span data-stu-id="e173e-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="e173e-182">Кроме того, добавьте `using` оператор для `ContosoUniversityModelBinding. Models` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="e173e-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="e173e-183">Сохраните Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="e173e-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="e173e-184">В консоли диспетчера пакетов выполните команду **Добавить-миграцию начальный**.</span><span class="sxs-lookup"><span data-stu-id="e173e-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="e173e-185">Выполните команду **Update-Database**.</span><span class="sxs-lookup"><span data-stu-id="e173e-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="e173e-186">Если при выполнении этой команды появляется исключение, `StudentID` `CourseID` значения и могут отличаться от значений `Seed` методов.</span><span class="sxs-lookup"><span data-stu-id="e173e-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="e173e-187">Откройте эти таблицы базы данных и найдите существующие значения для `StudentID` и `CourseID` .</span><span class="sxs-lookup"><span data-stu-id="e173e-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="e173e-188">Добавьте эти значения в код для заполнения `Enrollments` таблицы.</span><span class="sxs-lookup"><span data-stu-id="e173e-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="e173e-189">Добавление элемента управления GridView</span><span class="sxs-lookup"><span data-stu-id="e173e-189">Add a GridView control</span></span>

<span data-ttu-id="e173e-190">Заполненные данные базы данных теперь готовы к извлечению и отображению данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="e173e-191">Откройте students. aspx.</span><span class="sxs-lookup"><span data-stu-id="e173e-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="e173e-192">Нахождение `MainContent` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="e173e-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="e173e-193">В пределах этого заполнителя добавьте элемент управления **GridView** , включающий этот код.</span><span class="sxs-lookup"><span data-stu-id="e173e-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="e173e-194">Примечания.</span><span class="sxs-lookup"><span data-stu-id="e173e-194">Things to note:</span></span>
   * <span data-ttu-id="e173e-195">Обратите внимание на значение, заданное для `SelectMethod` свойства в элементе GridView.</span><span class="sxs-lookup"><span data-stu-id="e173e-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="e173e-196">Это значение указывает метод, используемый для получения данных GridView, которые создаются на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="e173e-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="e173e-197">`ItemType`Для свойства задан `Student` класс, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="e173e-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="e173e-198">Этот параметр позволяет ссылаться на свойства класса в разметке.</span><span class="sxs-lookup"><span data-stu-id="e173e-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="e173e-199">Например, `Student` класс содержит коллекцию с именем `Enrollments` .</span><span class="sxs-lookup"><span data-stu-id="e173e-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="e173e-200">Можно использовать `Item.Enrollments` для получения этой коллекции, а затем использовать [синтаксис LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) для получения суммы зарегистрированных кредитов каждого учащегося.</span><span class="sxs-lookup"><span data-stu-id="e173e-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="e173e-201">Сохраните учащихся. aspx.</span><span class="sxs-lookup"><span data-stu-id="e173e-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="e173e-202">Добавление кода для получения данных</span><span class="sxs-lookup"><span data-stu-id="e173e-202">Add code to retrieve data</span></span>

   <span data-ttu-id="e173e-203">В файле кода программной части students. aspx добавьте метод, указанный для `SelectMethod` значения.</span><span class="sxs-lookup"><span data-stu-id="e173e-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="e173e-204">Откройте Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="e173e-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="e173e-205">Добавьте `using` инструкции для `ContosoUniversityModelBinding. Models` `System.Data.Entity` пространств имен и.</span><span class="sxs-lookup"><span data-stu-id="e173e-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="e173e-206">Добавьте указанный метод для `SelectMethod` :</span><span class="sxs-lookup"><span data-stu-id="e173e-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="e173e-207">`Include`Предложение улучшает производительность запросов, но не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="e173e-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="e173e-208">Без `Include` предложения данные извлекаются с помощью [*отложенной загрузки*](https://en.wikipedia.org/wiki/Lazy_loading), что включает отправку отдельного запроса к базе данных при каждом извлечении связанных данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="e173e-209">При использовании `Include` предложения данные извлекаются с помощью *безотлагательной загрузки*, что означает, что один запрос к базе данных получает все связанные данные.</span><span class="sxs-lookup"><span data-stu-id="e173e-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="e173e-210">Если связанные данные не используются, безотлагательная загрузка менее эффективна, так как извлекаются дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="e173e-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="e173e-211">Однако в этом случае упреждающая загрузка обеспечивает наилучшую производительность, так как для каждой записи отображаются связанные данные.</span><span class="sxs-lookup"><span data-stu-id="e173e-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="e173e-212">Дополнительные сведения о вопросах производительности при загрузке связанных данных см. в разделе **Lazy, безотлагательная и явная загрузка связанных** данных статьи [чтение связанных данных с помощью Entity Framework в приложении ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) .</span><span class="sxs-lookup"><span data-stu-id="e173e-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="e173e-213">По умолчанию данные сортируются по значениям свойства, отмеченного как ключ.</span><span class="sxs-lookup"><span data-stu-id="e173e-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="e173e-214">Можно добавить `OrderBy` предложение, чтобы указать другое значение сортировки.</span><span class="sxs-lookup"><span data-stu-id="e173e-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="e173e-215">В этом примере `StudentID` для сортировки используется свойство по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e173e-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="e173e-216">В статье [Сортировка, разбиение по страницам и фильтрация данных](sorting-paging-and-filtering-data.md) пользователю разрешено выбирать столбец для сортировки.</span><span class="sxs-lookup"><span data-stu-id="e173e-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="e173e-217">Сохраните Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="e173e-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="e173e-218">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e173e-218">Run your application</span></span> 

<span data-ttu-id="e173e-219">Запустите веб-приложение (**F5**) и перейдите на страницу **учащихся** , на которой отображается следующее:</span><span class="sxs-lookup"><span data-stu-id="e173e-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![Отображение данных](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="e173e-221">Автоматическое создание методов привязки модели</span><span class="sxs-lookup"><span data-stu-id="e173e-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="e173e-222">При работе с этой серией руководств можно просто скопировать код из учебника в проект.</span><span class="sxs-lookup"><span data-stu-id="e173e-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="e173e-223">Однако одним из недостатков этого подхода является то, что вы не сможете быть осведомлены о функции, предоставляемой Visual Studio, для автоматического создания кода для методов привязки модели.</span><span class="sxs-lookup"><span data-stu-id="e173e-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="e173e-224">При работе с собственными проектами автоматическое создание кода может сэкономить время и помочь вам понять, как реализовать операцию.</span><span class="sxs-lookup"><span data-stu-id="e173e-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="e173e-225">В этом разделе описывается функция автоматического создания кода.</span><span class="sxs-lookup"><span data-stu-id="e173e-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="e173e-226">Этот раздел является только информационным и не содержит кода, необходимого для реализации в проекте.</span><span class="sxs-lookup"><span data-stu-id="e173e-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="e173e-227">При задании значения для `SelectMethod` свойств, `UpdateMethod` , `InsertMethod` или `DeleteMethod` в коде разметки можно выбрать параметр **создать новый метод** .</span><span class="sxs-lookup"><span data-stu-id="e173e-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![Создание метода](retrieving-data/_static/image18.png)

<span data-ttu-id="e173e-229">Visual Studio не только создает метод в коде программной части с правильной сигнатурой, но также создает код реализации для выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="e173e-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="e173e-230">Если сначала задать `ItemType` свойство перед использованием функции автоматического создания кода, созданный код использует этот тип для операций.</span><span class="sxs-lookup"><span data-stu-id="e173e-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="e173e-231">Например, при задании `UpdateMethod` свойства автоматически создается следующий код:</span><span class="sxs-lookup"><span data-stu-id="e173e-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="e173e-232">Опять же, этот код не нужно добавлять в проект.</span><span class="sxs-lookup"><span data-stu-id="e173e-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="e173e-233">В следующем учебнике будут реализованы методы обновления, удаления и добавления новых данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="e173e-234">Сводка</span><span class="sxs-lookup"><span data-stu-id="e173e-234">Summary</span></span>

<span data-ttu-id="e173e-235">В этом руководстве были созданы классы модели данных и создана база данных из этих классов.</span><span class="sxs-lookup"><span data-stu-id="e173e-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="e173e-236">Вы заполнили таблицы базы данных тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="e173e-236">You filled the database tables with test data.</span></span> <span data-ttu-id="e173e-237">Вы использовали привязку модели для получения данных из базы данных, а затем отображает их в элементе управления GridView.</span><span class="sxs-lookup"><span data-stu-id="e173e-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="e173e-238">В следующем [руководстве](updating-deleting-and-creating-data.md) этой серии вы включите обновление, удаление и создание данных.</span><span class="sxs-lookup"><span data-stu-id="e173e-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e173e-239">Вперед</span><span class="sxs-lookup"><span data-stu-id="e173e-239">Next</span></span>](updating-deleting-and-creating-data.md)
