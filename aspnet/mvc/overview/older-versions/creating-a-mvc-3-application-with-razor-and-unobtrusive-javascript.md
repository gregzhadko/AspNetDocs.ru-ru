---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Создание приложения MVC 3 с помощью Razor и ненавязчивого JavaScript (ru) Документы Майкрософт
author: rick-anderson
description: Образец веб-приложения «Список пользователей» демонстрирует, насколько просто создавать ASP.NET приложения MVC 3 с помощью движка представления Razor. Образец применения s. .
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542460"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="cc157-104">Создание приложения на MVC 3 с помощью Razor и ненавязчивого JavaScript</span><span class="sxs-lookup"><span data-stu-id="cc157-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="cc157-105">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cc157-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="cc157-106">Образец веб-приложения «Список пользователей» демонстрирует, насколько просто создавать ASP.NET приложения MVC 3 с помощью движка представления Razor.</span><span class="sxs-lookup"><span data-stu-id="cc157-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="cc157-107">Пример приложения показывает, как использовать новый движок представления Razor с ASP.NET версии MVC 3 и Visual Studio 2010 для создания вымышленного веб-сайта списка пользователей, который включает в себя такие функции, как создание, отображение, редактирование и удаливание пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="cc157-108">В этом уроке описаны шаги, предпринятые для создания образца списка пользователей ASP.NET приложениеM MVC 3.</span><span class="sxs-lookup"><span data-stu-id="cc157-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="cc157-109">Проект Visual Studio с исходным кодом C и VB доступен для сопровождения этой темы: [Скачать](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="cc157-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="cc157-110">Если у вас есть вопросы об этом учебнике, пожалуйста, разместите их на [форуме MVC](https://forums.asp.net/1146.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc157-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="cc157-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="cc157-111">Overview</span></span>

<span data-ttu-id="cc157-112">Приложение, которое вы будете строить простой веб-сайт список пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="cc157-113">Пользователи могут вводить, просматривать и обновлять информацию о пользователе.</span><span class="sxs-lookup"><span data-stu-id="cc157-113">Users can enter, view, and update user information.</span></span>

![Пример сайта](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="cc157-115">Вы можете скачать VB и C е завершенный проект [здесь](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span><span class="sxs-lookup"><span data-stu-id="cc157-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="cc157-116">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="cc157-116">Creating the Web Application</span></span>

<span data-ttu-id="cc157-117">Чтобы начать учебник, откройте Visual Studio 2010 и создайте новый проект с использованием *шаблона ASP.NET веб-приложений MVC 3 MVC 3.*</span><span class="sxs-lookup"><span data-stu-id="cc157-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="cc157-118">Назовите приложение &quot;Mvc3Razor&quot;.</span><span class="sxs-lookup"><span data-stu-id="cc157-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="cc157-119">[![Новый проект MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="cc157-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="cc157-120">В **диалоге проекта New ASP.NET MVC 3** выберите **Internet Application,** выберите движок представления Razor, а затем нажмите **OK.**</span><span class="sxs-lookup"><span data-stu-id="cc157-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Новый диалог проекта mVC 3 ASP.NET](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="cc157-122">В этом учебнике вы не будете использовать ASP.NET поставщика членства, так что вы можете удалить все файлы, связанные с логином и членством.</span><span class="sxs-lookup"><span data-stu-id="cc157-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="cc157-123">В **Solution Explorer**удалите следующие файлы и каталоги:</span><span class="sxs-lookup"><span data-stu-id="cc157-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="cc157-124">*Контролеры-бухгалтеры*</span><span class="sxs-lookup"><span data-stu-id="cc157-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="cc157-125">*Модели-AccountModels*</span><span class="sxs-lookup"><span data-stu-id="cc157-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="cc157-126">*Просмотр\\_LogOnPartialы*</span><span class="sxs-lookup"><span data-stu-id="cc157-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="cc157-127">*Просмотры (и* все файлы в этом каталоге)</span><span class="sxs-lookup"><span data-stu-id="cc157-127">*Views\Account* (and all the files in this directory)</span></span>

![Солн Эксп](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="cc157-129">Отойдите файл <em> \_Layout.cshtml</em> и замените `<div>` разметку внутри элемента, названного `logindisplay` сообщением <em>&quot;</em>Login Disabled.&quot;</span><span class="sxs-lookup"><span data-stu-id="cc157-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="cc157-130">Следующий пример показывает новую разметку:</span><span class="sxs-lookup"><span data-stu-id="cc157-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="cc157-131">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="cc157-131">Adding the Model</span></span>

<span data-ttu-id="cc157-132">В **Solution Explorer**, правой кнопкой кнопку *Модели* папку, выберите **Добавить,** а затем нажмите **класс**.</span><span class="sxs-lookup"><span data-stu-id="cc157-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Новый пользовательский класс Mdl](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="cc157-134">Назовите класс `UserModel`.</span><span class="sxs-lookup"><span data-stu-id="cc157-134">Name the class `UserModel`.</span></span> <span data-ttu-id="cc157-135">Замените содержимое файла *UserModel* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cc157-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="cc157-136">Класс `UserModel` представляет пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="cc157-137">Каждый участник класса аннотируется с [требуемым](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) атрибутом из пространства имен [DataAnnotations.](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)</span><span class="sxs-lookup"><span data-stu-id="cc157-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="cc157-138">Атрибуты в пространстве имен [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) обеспечивают автоматическую проверку на стороне клиента и сервера для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="cc157-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="cc157-139">Откройте `HomeController` класс и `using` добавьте директиву, `UserModel` `Users` чтобы вы могли получить доступ к классам:</span><span class="sxs-lookup"><span data-stu-id="cc157-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="cc157-140">Сразу после `HomeController` объявления добавьте следующий комментарий `Users` и ссылку на класс:</span><span class="sxs-lookup"><span data-stu-id="cc157-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="cc157-141">Класс `Users` представляет собой упрощенный хранилище данных в памяти, который вы будете использовать в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cc157-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="cc157-142">В реальном приложении вы будете использовать базу данных для хранения информации о пользователе.</span><span class="sxs-lookup"><span data-stu-id="cc157-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="cc157-143">Первые несколько строк `HomeController` файла отображаются в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="cc157-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="cc157-144">Создайте приложение таким образом, чтобы модель пользователя была доступна мастеру строительных лесов на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="cc157-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="cc157-145">Создание представления по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cc157-145">Creating the Default View</span></span>

<span data-ttu-id="cc157-146">Следующим шагом является добавление метода действия и представления для отображения пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="cc157-147">Удалите существующий файл *«Домашний индекс».*</span><span class="sxs-lookup"><span data-stu-id="cc157-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="cc157-148">Вы создадите новый файл *Индекса* для отображения пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="cc157-149">В `HomeController` классе замените содержимое `Index` метода следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cc157-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="cc157-150">Нажмите правой `Index` кнопкой мыши внутри метода, а затем нажмите **Добавить вид**.</span><span class="sxs-lookup"><span data-stu-id="cc157-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Добавление представления](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="cc157-152">Выберите **возможность создания сильно типового представления.**</span><span class="sxs-lookup"><span data-stu-id="cc157-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="cc157-153">Для **просмотра класса данных,** выберите **Mvc3Razor.Models.UserModel**.</span><span class="sxs-lookup"><span data-stu-id="cc157-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="cc157-154">(Если вы не видите **Mvc3Razor.Models.UserModel** в поле **класса данных View,** вам необходимо создать проект.) Убедитесь, что движок представления настроен на **Razor.**</span><span class="sxs-lookup"><span data-stu-id="cc157-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="cc157-155">Установите **содержимое просмотра** в **список,** а затем нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cc157-155">Set **View content** to **List** and then click **Add**.</span></span>

![Добавление представления индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="cc157-157">Новое представление автоматически подмостки пользовательских данных, `Index` которые передаются в представление.</span><span class="sxs-lookup"><span data-stu-id="cc157-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="cc157-158">Изучите недавно созданный файл *«Домашний индекс».*</span><span class="sxs-lookup"><span data-stu-id="cc157-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="cc157-159">**Создать новые,** **отсвативайте,** **Детали**и **Удалить** ссылки не работают, но остальная часть страницы является функциональной.</span><span class="sxs-lookup"><span data-stu-id="cc157-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="cc157-160">Запустите страницу.</span><span class="sxs-lookup"><span data-stu-id="cc157-160">Run the page.</span></span> <span data-ttu-id="cc157-161">Вы видите список пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-161">You see a list of users.</span></span>

![Страница индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="cc157-163">Откройте файл *Index.cshtml* `ActionLink` и замените разметку для **Edit,** **Подробности**и **Удалить** со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cc157-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="cc157-164">Имя пользователя используется в качестве идентификатора для поиска выбранной записи в ссылках **Edit,** **Details**и **Delete.**</span><span class="sxs-lookup"><span data-stu-id="cc157-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="cc157-165">Создание представления деталей</span><span class="sxs-lookup"><span data-stu-id="cc157-165">Creating the Details View</span></span>

<span data-ttu-id="cc157-166">Следующим шагом является добавление `Details` метода действия и представления для отображения деталей пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc157-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="cc157-168">Добавьте `Details` следующий метод к домашнему контроллеру:</span><span class="sxs-lookup"><span data-stu-id="cc157-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="cc157-169">Нажмите правой `Details` кнопкой мыши внутри метода, а затем выберите <strong>Добавить вид</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc157-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="cc157-170">Убедитесь, что в поле <strong>класса данных View</strong> содержится <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span><span class="sxs-lookup"><span data-stu-id="cc157-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="cc157-171">Установите <strong>содержимое view</strong> для <strong>деталей,</strong> а затем нажмите <strong>Добавить</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc157-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Добавление представления деталей](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="cc157-173">Запустите приложение и выберите ссылку на детали.</span><span class="sxs-lookup"><span data-stu-id="cc157-173">Run the application and select a details link.</span></span> <span data-ttu-id="cc157-174">Автоматические строительные леса показывают каждое свойство в модели.</span><span class="sxs-lookup"><span data-stu-id="cc157-174">The automatic scaffolding shows each property in the model.</span></span>

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="cc157-176">Создание представления об отсылке</span><span class="sxs-lookup"><span data-stu-id="cc157-176">Creating the Edit View</span></span>

<span data-ttu-id="cc157-177">Добавьте `Edit` следующий метод к домашнему контроллеру.</span><span class="sxs-lookup"><span data-stu-id="cc157-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="cc157-178">Добавьте представление, как в предыдущих шагах, но установите **содержимое view** для **edit.**</span><span class="sxs-lookup"><span data-stu-id="cc157-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Добавление представления edit](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="cc157-180">Запустите приложение и отодевать имя и фамилию одного из пользователей.</span><span class="sxs-lookup"><span data-stu-id="cc157-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="cc157-181">Если вы `DataAnnotation` нарушаете какие-либо `UserModel` ограничения, которые были применены к классу, при отправке формы вы увидите ошибки проверки, которые производятся кодом сервера.</span><span class="sxs-lookup"><span data-stu-id="cc157-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="cc157-182">Например, если вы измените&quot; &quot;имя&quot; &quot;Ann на A, при отправке формы в форме отображается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="cc157-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="cc157-183">В этом уроке вы рассматриваете имя пользователя в качестве основного ключа.</span><span class="sxs-lookup"><span data-stu-id="cc157-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="cc157-184">Таким образом, свойство имени пользователя не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="cc157-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="cc157-185">В файле *Edit.cshtml* сразу `Html.BeginForm` после оператора установите имя пользователя как скрытое поле.</span><span class="sxs-lookup"><span data-stu-id="cc157-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="cc157-186">Это приводит к тому, что свойство передается в модели.</span><span class="sxs-lookup"><span data-stu-id="cc157-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="cc157-187">Следующий фрагмент кода показывает `Hidden` размещение оператора:</span><span class="sxs-lookup"><span data-stu-id="cc157-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="cc157-188">Замените `TextBoxFor` `ValidationMessageFor` и разметку для `DisplayFor` имени пользователя вызовом.</span><span class="sxs-lookup"><span data-stu-id="cc157-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="cc157-189">Метод `DisplayFor` отображает свойство как элемент только для чтения.</span><span class="sxs-lookup"><span data-stu-id="cc157-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="cc157-190">В следующем примере приведена полная разметка.</span><span class="sxs-lookup"><span data-stu-id="cc157-190">The following example shows the completed markup.</span></span> <span data-ttu-id="cc157-191">Оригинал `TextBoxFor` и `ValidationMessageFor` звонки комментируются с Razor начать комментарий и конец-комментарий символов (`@* *@`)</span><span class="sxs-lookup"><span data-stu-id="cc157-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="cc157-192">Включение проверки клиента на стороне</span><span class="sxs-lookup"><span data-stu-id="cc157-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="cc157-193">Для включения проверки на стороне клиента в ASP.NET MVC 3 необходимо установить два флага и включить три файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cc157-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="cc157-194">Откройте файл *Web.config* приложения.</span><span class="sxs-lookup"><span data-stu-id="cc157-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="cc157-195">Проверить `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` и верны в настройках приложения.</span><span class="sxs-lookup"><span data-stu-id="cc157-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="cc157-196">Следующий фрагмент из корневого файла *Web.config* показывает правильные настройки:</span><span class="sxs-lookup"><span data-stu-id="cc157-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="cc157-197">Установка `UnobtrusiveJavaScriptEnabled` на истину позволяет ненавязчивым Ajax и ненавязчивой проверки клиента.</span><span class="sxs-lookup"><span data-stu-id="cc157-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="cc157-198">При использовании ненавязчивой проверки правила проверки превращаются в атрибуты HTML5.</span><span class="sxs-lookup"><span data-stu-id="cc157-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="cc157-199">Имена атрибутов HTML5 могут состоять только из букв, цифр и тире.</span><span class="sxs-lookup"><span data-stu-id="cc157-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="cc157-200">Установка `ClientValidationEnabled` на истину позволяет клиентской проверки.</span><span class="sxs-lookup"><span data-stu-id="cc157-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="cc157-201">Установив эти ключи в файле *web.config* приложения, вы позволяете проверку клиента и ненавязчивый JavaScript для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="cc157-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="cc157-202">Вы также можете включить или отключить эти параметры в отдельных представлениях или в методах контроллера, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="cc157-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="cc157-203">Также необходимо включить несколько файлов JavaScript в отрисованные представления.</span><span class="sxs-lookup"><span data-stu-id="cc157-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="cc157-204">Простой способ включить JavaScript во все представления — добавить их в файл *«Общие\\_Layout.cshtml».*</span><span class="sxs-lookup"><span data-stu-id="cc157-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="cc157-205">Замените `<head>` элемент файла \* \_Layout.cshtml\* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cc157-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="cc157-206">Первые два сценария j'ery размещаются в Microsoft Ajax Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="cc157-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="cc157-207">Воспользовавшись Microsoft Ajax CDN, вы можете значительно улучшить производительность приложений в первом хите.</span><span class="sxs-lookup"><span data-stu-id="cc157-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="cc157-208">Запустите приложение и нажмите ссылку на отодевать.</span><span class="sxs-lookup"><span data-stu-id="cc157-208">Run the application and click an edit link.</span></span> <span data-ttu-id="cc157-209">Просмотр источника страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="cc157-209">View the page's source in the browser.</span></span> <span data-ttu-id="cc157-210">Источник браузера показывает много атрибутов формы `data-val` (для проверки данных).</span><span class="sxs-lookup"><span data-stu-id="cc157-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="cc157-211">При включении проверки клиента и ненавязчивой JavaScript ввода полей с `data-val="true"` правилом проверки клиента содержат атрибут, чтобы вызвать ненавязчивую проверку клиента.</span><span class="sxs-lookup"><span data-stu-id="cc157-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="cc157-212">Например, `City` поле в модели было украшено [атрибутом Required,](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) что приводит к html, показанным в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="cc157-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="cc157-213">Для каждого правила проверки клиента добавляется атрибут, `data-val-rulename="message"`который имеет форму.</span><span class="sxs-lookup"><span data-stu-id="cc157-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="cc157-214">Используя `City` приведенный ранее пример поля, требуемое правило `data-val-required` проверки &quot;клиента генерирует атрибут&quot;и требуется поле City.</span><span class="sxs-lookup"><span data-stu-id="cc157-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="cc157-215">Запустите приложение, отодвите одного `City` из пользователей и очистите поле.</span><span class="sxs-lookup"><span data-stu-id="cc157-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="cc157-216">При вывозе вкладки из поля вы видите сообщение об ошибке проверки клиента.</span><span class="sxs-lookup"><span data-stu-id="cc157-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Город требуется](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="cc157-218">Аналогичным образом, для каждого параметра в правиле проверки клиента `data-val-rulename-paramname=paramvalue`добавляется атрибут, который имеет форму.</span><span class="sxs-lookup"><span data-stu-id="cc157-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="cc157-219">Например, `FirstName` свойство аннотировано атрибутом [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) и определяет минимальную длину 3 и максимальную длину 8.</span><span class="sxs-lookup"><span data-stu-id="cc157-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="cc157-220">Названо `length` правило проверки данных `max` с именем параметра и значением параметра 8.</span><span class="sxs-lookup"><span data-stu-id="cc157-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="cc157-221">Ниже отображается HTML, который `FirstName` генерируется для поля при отобрасвании одного из пользователей:</span><span class="sxs-lookup"><span data-stu-id="cc157-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="cc157-222">Для получения дополнительной информации о ненавязчивой проверки клиента, см запись [Ненавязчивая проверка клиента в ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) в блоге Брэда Уилсона.</span><span class="sxs-lookup"><span data-stu-id="cc157-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="cc157-223">В ASP.NET MVC 3 Beta, иногда необходимо представить форму для того, чтобы начать проверку на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="cc157-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="cc157-224">Это может быть изменено для окончательного выпуска.</span><span class="sxs-lookup"><span data-stu-id="cc157-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="cc157-225">Создание представления о создании</span><span class="sxs-lookup"><span data-stu-id="cc157-225">Creating the Create View</span></span>

<span data-ttu-id="cc157-226">Следующим шагом является добавление `Create` метода действия и представления, чтобы пользователь мог создать нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc157-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="cc157-227">Добавьте `Create` следующий метод к домашнему контроллеру:</span><span class="sxs-lookup"><span data-stu-id="cc157-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="cc157-228">Добавьте представление, как в предыдущих шагах, но установите **содержимое view** для **создания.**</span><span class="sxs-lookup"><span data-stu-id="cc157-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Создание представления](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="cc157-230">Запустите приложение, выберите ссылку **«Создать»** и добавьте нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc157-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="cc157-231">Метод `Create` автоматически использует проверку на стороне клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="cc157-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="cc157-232">Попробуйте ввести имя пользователя, содержащее белое пространство, например &quot;Бен X&quot;.</span><span class="sxs-lookup"><span data-stu-id="cc157-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="cc157-233">При выражаемеименно из поля имени пользователя отображается ошибка проверки на стороне клиента ()`White space is not allowed`</span><span class="sxs-lookup"><span data-stu-id="cc157-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="cc157-234">Добавить метод удаления</span><span class="sxs-lookup"><span data-stu-id="cc157-234">Add the Delete method</span></span>

<span data-ttu-id="cc157-235">Чтобы завершить обучение, добавьте следующий `Delete` метод в домашний контроллер:</span><span class="sxs-lookup"><span data-stu-id="cc157-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="cc157-236">Добавьте `Delete` представление, как и в предыдущих шагах, установив **содержимое View** для **удаления.**</span><span class="sxs-lookup"><span data-stu-id="cc157-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Удалить представление](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="cc157-238">Теперь у вас есть простой, но полностью функциональный ASP.NET mVC 3 приложение с проверкой.</span><span class="sxs-lookup"><span data-stu-id="cc157-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
