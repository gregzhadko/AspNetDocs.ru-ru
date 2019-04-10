---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Редактирование кода веб-форм ASP.NET в Visual Studio 2013 | Документация Майкрософт
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 328dc6fb61ac562131b11b36b40f574ca5a53866
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59397374"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="93182-102">Редактирование кода в веб-формах ASP.NET в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="93182-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>

<span data-ttu-id="93182-103">по [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="93182-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="93182-104">На многих страницах веб-форма ASP.NET вы напишете код на Visual Basic, C# или другом языке.</span><span class="sxs-lookup"><span data-stu-id="93182-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="93182-105">Редактор кода в Visual Studio может помочь быстро написать код и избежать ошибок.</span><span class="sxs-lookup"><span data-stu-id="93182-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="93182-106">Кроме того редактор предоставляет способ для создания повторно используемого кода с целью сокращения объема работы, которые необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="93182-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="93182-107">В этом пошаговом руководстве показаны различные возможности в редакторе кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93182-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="93182-108">В этом пошаговом руководстве описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="93182-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="93182-109">Исправьте встроенные ошибки в написании кода.</span><span class="sxs-lookup"><span data-stu-id="93182-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="93182-110">Рефакторинг и переименуйте кода.</span><span class="sxs-lookup"><span data-stu-id="93182-110">Refactor and rename code.</span></span>
- <span data-ttu-id="93182-111">Переименуйте переменные и объекты.</span><span class="sxs-lookup"><span data-stu-id="93182-111">Rename variables and objects.</span></span>
- <span data-ttu-id="93182-112">Вставка фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="93182-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93182-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="93182-113">Prerequisites</span></span>


<span data-ttu-id="93182-114">Для выполнения данного пошагового руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="93182-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="93182-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) или [Microsoft Visual Studio Express 2013 для Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="93182-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="93182-116">Платформа .NET Framework устанавливается автоматически.</span><span class="sxs-lookup"><span data-stu-id="93182-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="93182-117">Microsoft Visual Studio 2013 и Microsoft Visual Studio Express 2013 для Web будет часто обращаться как к Visual Studio данной серии учебных курсов.</span><span class="sxs-lookup"><span data-stu-id="93182-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="93182-118">При использовании Visual Studio, в этом пошаговом руководстве предполагается, что выбрана **веб-разработки** набор параметров при первом запуске Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93182-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="93182-119">Дополнительные сведения см. в разделе [Как Выберите параметры среды веб-разработки](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="93182-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="93182-120">Создание проекта веб-приложения и страницы</span><span class="sxs-lookup"><span data-stu-id="93182-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="93182-121">В этой части пошагового руководства будет создать проект веб-приложения и добавьте новую страницу к нему.</span><span class="sxs-lookup"><span data-stu-id="93182-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="93182-122">Чтобы создать проект веб-приложения</span><span class="sxs-lookup"><span data-stu-id="93182-122">To create a Web application project</span></span>

1. <span data-ttu-id="93182-123">Open Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93182-123">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="93182-124">В меню **Файл** выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="93182-124">On the **File** menu, select **New Project**.</span></span>  
    ![Меню "файл"](code-editing-in-web-forms-pages/_static/image1.png)

    <span data-ttu-id="93182-126">Откроется диалоговое окно **Новый проект** .</span><span class="sxs-lookup"><span data-stu-id="93182-126">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="93182-127">Выберите **шаблоны**  - &gt; **Visual C#**  - &gt; **Web** группы шаблонов в левой части.</span><span class="sxs-lookup"><span data-stu-id="93182-127">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="93182-128">Выберите **веб-приложение ASP.NET** шаблона в центральном столбце.</span><span class="sxs-lookup"><span data-stu-id="93182-128">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="93182-129">Присвойте проекту имя ***BasicWebApp*** и нажмите кнопку **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="93182-129">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
![Диалоговое окно “Новый проект”](code-editing-in-web-forms-pages/_static/image2.png)
6. <span data-ttu-id="93182-131">Затем выберите **веб-форм** шаблона и нажмите кнопку **ОК** кнопку, чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="93182-131">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
![Диалоговое окно "новый проект ASP.NET"](code-editing-in-web-forms-pages/_static/image3.png)  

    <span data-ttu-id="93182-133">Visual Studio создает новый проект, включающий стандартные функциональные возможности, на основе шаблона веб-форм.</span><span class="sxs-lookup"><span data-stu-id="93182-133">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>


## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="93182-134">Создание новой страницы ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="93182-134">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="93182-135">Когда вы создаете новое приложение веб-форм с помощью **веб-приложение ASP.NET** шаблон проекта Visual Studio добавляет страницы ASP.NET (страницы веб-форм) с именем *Default.aspx*, а также как несколько файлов и папки.</span><span class="sxs-lookup"><span data-stu-id="93182-135">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="93182-136">Можно использовать *Default.aspx* страницу как на домашнюю страницу веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="93182-136">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="93182-137">Тем не менее в этом пошаговом руководстве будет создавать и работать с новой страницы.</span><span class="sxs-lookup"><span data-stu-id="93182-137">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="93182-138">Добавление страницы в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="93182-138">To add a page to the Web application</span></span>


1. <span data-ttu-id="93182-139">В **обозревателе решений**, щелкните правой кнопкой мыши имя веб-приложения (в этом руководстве, имя приложения — **BasicWebSite**), а затем нажмите кнопку **добавить**  - &gt; **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="93182-139">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="93182-140">Откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="93182-140">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="93182-141">Выберите **Visual C#**  - &gt; **Web** группы шаблонов в левой части.</span><span class="sxs-lookup"><span data-stu-id="93182-141">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="93182-142">Выберите **веб-формы** из середины списка и назовите его *FirstWebPage.aspx*.</span><span class="sxs-lookup"><span data-stu-id="93182-142">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    ![Диалоговое окно ''Добавление нового элемента''](code-editing-in-web-forms-pages/_static/image4.png)
3. <span data-ttu-id="93182-144">Нажмите кнопку **добавить** добавить страницу веб-формы в проект.</span><span class="sxs-lookup"><span data-stu-id="93182-144">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="93182-145">Visual Studio создаст новую страницу и открывает его.</span><span class="sxs-lookup"><span data-stu-id="93182-145">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="93182-146">Затем установите эта новая страница в качестве стартовой страницы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="93182-146">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="93182-147">В **обозревателе решений**, щелкните правой кнопкой мыши новую страницу с именем *FirstWebPage.aspx* и выберите **задать в качестве начальной страницы**.</span><span class="sxs-lookup"><span data-stu-id="93182-147">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="93182-148">При запуске этого приложения, чтобы проверить ход работы, автоматически появится эта новая страница в браузере.</span><span class="sxs-lookup"><span data-stu-id="93182-148">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>


## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="93182-149">Исправление встроенного ошибок кода</span><span class="sxs-lookup"><span data-stu-id="93182-149">Correcting Inline Coding Errors</span></span>


<span data-ttu-id="93182-150">Редактор кода в Visual Studio помогает избежать ошибок, как написать код, а также при внесении ошибки, редактор кода позволяет, чтобы исправить эту ошибку.</span><span class="sxs-lookup"><span data-stu-id="93182-150">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="93182-151">В этой части пошагового руководства будет написать строку кода, иллюстрирующие возможности исправления ошибок в редакторе.</span><span class="sxs-lookup"><span data-stu-id="93182-151">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="93182-152">Для исправления простых ошибок программирования в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93182-152">To correct simple coding errors in Visual Studio</span></span>


1. <span data-ttu-id="93182-153">В **разработки** дважды щелкните пустую страницу, чтобы создать обработчик для **нагрузки** событий для страницы.</span><span class="sxs-lookup"><span data-stu-id="93182-153">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="93182-154">Обработчик событий при использовании только как место для написания кода.</span><span class="sxs-lookup"><span data-stu-id="93182-154">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="93182-155">Внутри обработчика, введите следующую строку, которая содержит ошибку и нажмите клавишу **ввод**:</span><span class="sxs-lookup"><span data-stu-id="93182-155">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="93182-156">При нажатии клавиши **ввод**, редактор кода помещает зеленого и красного подчеркивание (часто вызывают &quot;волнистой&quot; строк) в областях кода, которые возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="93182-156">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="93182-157">Зеленой линией указывает на предупреждение.</span><span class="sxs-lookup"><span data-stu-id="93182-157">A green underline indicates a warning.</span></span> <span data-ttu-id="93182-158">Красной линией указывает на ошибку, необходимо исправить.</span><span class="sxs-lookup"><span data-stu-id="93182-158">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="93182-159">Наведите указатель мыши на `myStr` чтобы увидеть подсказку, которая сообщает о предупреждении.</span><span class="sxs-lookup"><span data-stu-id="93182-159">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="93182-160">Кроме того наведите указатель мыши на красную линию, чтобы просмотреть сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="93182-160">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="93182-161">Ниже приведен код с подчеркивание.</span><span class="sxs-lookup"><span data-stu-id="93182-161">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="93182-162">![Текст приветствия в режиме конструктора](code-editing-in-web-forms-pages/_static/image5.png "текст приветствия в режиме конструктора")</span><span class="sxs-lookup"><span data-stu-id="93182-162">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="93182-163">Ошибки необходимо устранить, добавив точку с запятой `;` до конца строки.</span><span class="sxs-lookup"><span data-stu-id="93182-163">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="93182-164">Предупреждение просто сообщит, что вы не использовали `myStr` еще переменной.</span><span class="sxs-lookup"><span data-stu-id="93182-164">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="93182-165">Просмотреть текущий код форматирования параметров в Visual Studio, выбрав **средства**  - &gt; **параметры**  - &gt; **шрифты и Цвета**.</span><span class="sxs-lookup"><span data-stu-id="93182-165">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>


## <a name="refactoring-and-renaming"></a><span data-ttu-id="93182-166">Оптимизация кода и переименование</span><span class="sxs-lookup"><span data-stu-id="93182-166">Refactoring and Renaming</span></span>

<span data-ttu-id="93182-167">Рефакторинг — это программным методом, включающим реструктуризацию кода, чтобы упростить для понимания и поддерживать, сохранением его функциональных возможностей.</span><span class="sxs-lookup"><span data-stu-id="93182-167">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="93182-168">Простой пример может быть писать код в обработчик событий для получения данных из базы данных.</span><span class="sxs-lookup"><span data-stu-id="93182-168">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="93182-169">При разработке страницы, вы обнаруживаете, что необходимо обращаться к данным из нескольких разных обработчиков.</span><span class="sxs-lookup"><span data-stu-id="93182-169">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="93182-170">Таким образом путем создания метода доступа к данным на странице и вставка вызовы метода в обработчиках при рефакторинге кода страницы.</span><span class="sxs-lookup"><span data-stu-id="93182-170">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="93182-171">Редактор кода содержит средства, помогающие выполнять различные задачи оптимизации кода.</span><span class="sxs-lookup"><span data-stu-id="93182-171">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="93182-172">В этом пошаговом руководстве вы будете использовать два метода оптимизации кода: переименование переменных и методы извлечения.</span><span class="sxs-lookup"><span data-stu-id="93182-172">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="93182-173">Другие параметры оптимизации кода включают инкапсуляцию полей, преобразование локальных переменных в параметры метода и управление параметрами метода.</span><span class="sxs-lookup"><span data-stu-id="93182-173">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="93182-174">Доступность этих параметров оптимизации зависит от расположения в коде.</span><span class="sxs-lookup"><span data-stu-id="93182-174">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="93182-175">Рефакторинг кода</span><span class="sxs-lookup"><span data-stu-id="93182-175">Refactoring Code</span></span>

<span data-ttu-id="93182-176">Обычным сценарием оптимизации кода является создание (извлечение) метода из кода, который находится внутри другого элемента, например метод.</span><span class="sxs-lookup"><span data-stu-id="93182-176">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="93182-177">Это уменьшает размер исходного элемента и делает извлеченные код для повторного использования.</span><span class="sxs-lookup"><span data-stu-id="93182-177">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="93182-178">В этой части пошагового руководства будет написать простой код и затем извлечение метода из него.</span><span class="sxs-lookup"><span data-stu-id="93182-178">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="93182-179">Рефакторинг поддерживается для C#, поэтому вы создадите страницы, который использует в качестве языка программирования C#.</span><span class="sxs-lookup"><span data-stu-id="93182-179">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="93182-180">Извлечение метода на странице C#</span><span class="sxs-lookup"><span data-stu-id="93182-180">To extract a method in a C# page</span></span>

1. <span data-ttu-id="93182-181">Переключиться в режим **разработки** представления.</span><span class="sxs-lookup"><span data-stu-id="93182-181">Switch to **Design** view.</span></span>
2. <span data-ttu-id="93182-182">В **элементов**, из **стандартный** вкладке, перетащите [кнопку](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) на страницу.</span><span class="sxs-lookup"><span data-stu-id="93182-182">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="93182-183">Дважды щелкните **кнопку** управления, чтобы создать обработчик для его [щелкните](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) событий, а затем добавьте следующий выделенный код:</span><span class="sxs-lookup"><span data-stu-id="93182-183">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="93182-184">Код создает **ArrayList** использует цикл для загрузки в него значения объекта и затем использует другой цикл для отображения содержимого **ArrayList** объекта.</span><span class="sxs-lookup"><span data-stu-id="93182-184">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="93182-185">Нажмите клавишу **CTRL + F5** для запуска страницы и нажмите кнопку **кнопку** чтобы убедиться в том, что вы видите следующее:</span><span class="sxs-lookup"><span data-stu-id="93182-185">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="93182-186">Вернитесь в редактор кода, а затем выберите следующие строки в обработчике событий.</span><span class="sxs-lookup"><span data-stu-id="93182-186">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="93182-187">Правой кнопкой мыши, нажмите кнопку **рефакторинг**, а затем выберите **извлечение метода**.</span><span class="sxs-lookup"><span data-stu-id="93182-187">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="93182-188">**Извлечение метода** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="93182-188">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="93182-189">В **новому методу имя** введите **DisplayArray**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="93182-189">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="93182-190">Редактор кода создаст новый метод с именем `DisplayArray`и поместит вызов нового метода в **щелкните** обработчик, где изначально находился цикл.</span><span class="sxs-lookup"><span data-stu-id="93182-190">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="93182-191">Нажмите клавишу **CTRL + F5** снова запустить страницу, а затем нажмите кнопку **кнопку**.</span><span class="sxs-lookup"><span data-stu-id="93182-191">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="93182-192">Страницы работает так же, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="93182-192">The page functions the same as it did before.</span></span> <span data-ttu-id="93182-193">`DisplayArray` Метод теперь может быть вызов из любого места в классе страницы.</span><span class="sxs-lookup"><span data-stu-id="93182-193">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="93182-194">Переименование переменных</span><span class="sxs-lookup"><span data-stu-id="93182-194">Renaming Variables</span></span>

<span data-ttu-id="93182-195">При работе с переменными, а также объекты, можно переименовать их после уже заданы в коде.</span><span class="sxs-lookup"><span data-stu-id="93182-195">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="93182-196">Тем не менее переименование, переменные и объекты, может вызвать код, чтобы сделать недействительными будет пропущено переименование одну из ссылок.</span><span class="sxs-lookup"><span data-stu-id="93182-196">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="93182-197">Таким образом рефакторинг можно использовать для выполнения переименования.</span><span class="sxs-lookup"><span data-stu-id="93182-197">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="93182-198">Использование рефакторинга для переименования переменной</span><span class="sxs-lookup"><span data-stu-id="93182-198">To use refactoring to rename a variable</span></span>


1. <span data-ttu-id="93182-199">В **щелкните** обработчик событий, найдите следующую строку:</span><span class="sxs-lookup"><span data-stu-id="93182-199">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="93182-200">Щелкните правой кнопкой мыши имя переменной `alist`, выберите **рефакторинг**, а затем выберите **Переименовать**.</span><span class="sxs-lookup"><span data-stu-id="93182-200">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="93182-201">**Переименовать** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="93182-201">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="93182-202">В **новое имя** введите **ArrayList1** и убедитесь, что **Предварительный просмотр изменений ссылок** флажка.</span><span class="sxs-lookup"><span data-stu-id="93182-202">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="93182-203">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="93182-203">Then click **OK**.</span></span>

    <span data-ttu-id="93182-204">**Просмотр изменений** диалоговое окно отображается, а также отображается дерево, содержащее все ссылки на переменную, которая при переименовании.</span><span class="sxs-lookup"><span data-stu-id="93182-204">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="93182-205">Нажмите кнопку **применить** закрыть **Просмотр изменений** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="93182-205">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="93182-206">Переменные, относящиеся именно к экземпляр, который вы выбрали переименовываются.</span><span class="sxs-lookup"><span data-stu-id="93182-206">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="93182-207">Обратите внимание, что переменная `alist` в следующей строке не переименовывается.</span><span class="sxs-lookup"><span data-stu-id="93182-207">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="93182-208">Переменная `alist` в этой строке не переименован, поскольку он не представляет то же значение, что переменная `alist` переименованный.</span><span class="sxs-lookup"><span data-stu-id="93182-208">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="93182-209">Переменная `alist` в `DisplayArray` объявление является локальной переменной для этого метода.</span><span class="sxs-lookup"><span data-stu-id="93182-209">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="93182-210">Это иллюстрирует, что с помощью рефакторинга для переименования переменные отличается от простого действия поиска и замены в редакторе. Рефакторинг переименования переменные с знания семантики переменной, с которым идет работа.</span><span class="sxs-lookup"><span data-stu-id="93182-210">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>


## <a name="inserting-snippets"></a><span data-ttu-id="93182-211">Вставка фрагментов</span><span class="sxs-lookup"><span data-stu-id="93182-211">Inserting Snippets</span></span>

<span data-ttu-id="93182-212">Так как существует много задач кодирования, которые часто необходимо выполнять разработчикам веб-форм, редактор кода предоставляет библиотеку фрагментов, или блоков предварительно написанного кода.</span><span class="sxs-lookup"><span data-stu-id="93182-212">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="93182-213">Эти фрагменты кода можно вставить в страницу.</span><span class="sxs-lookup"><span data-stu-id="93182-213">You can insert these snippets into your page.</span></span>

<span data-ttu-id="93182-214">Каждый язык, который используется в Visual Studio имеет небольшие различия в способ вставки фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="93182-214">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="93182-215">Сведения о вставке фрагментов см. в разделе [фрагменты кода IntelliSense в Visual Basic](https://msdn.microsoft.com/library/18yz4be4.aspx).</span><span class="sxs-lookup"><span data-stu-id="93182-215">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="93182-216">Сведения о вставке фрагментов кода в Visual C#, см. в разделе [фрагменты кода Visual C#](https://msdn.microsoft.com/library/z41h7fat.aspx).</span><span class="sxs-lookup"><span data-stu-id="93182-216">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93182-217">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="93182-217">Next Steps</span></span>

<span data-ttu-id="93182-218">В этом пошаговом руководстве показаны базовые возможности редактора кода Visual Studio 2010 для исправления ошибок в коде, рефакторинга кода, переименование переменных и вставки фрагментов кода в код.</span><span class="sxs-lookup"><span data-stu-id="93182-218">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="93182-219">Дополнительные функции в редакторе делают разработку приложения и быстро.</span><span class="sxs-lookup"><span data-stu-id="93182-219">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="93182-220">Например, можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="93182-220">For example, you might want to:</span></span>

- <span data-ttu-id="93182-221">Дополнительные сведения о функциях, IntelliSense, такие как изменение параметров IntelliSense, управление фрагментами кода и поиск фрагментов кода в Интернете.</span><span class="sxs-lookup"><span data-stu-id="93182-221">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="93182-222">Дополнительные сведения см. в статье [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx) (Использование IntelliSense).</span><span class="sxs-lookup"><span data-stu-id="93182-222">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="93182-223">Вы научитесь создавать собственные фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="93182-223">Learn how to create your own code snippets.</span></span> <span data-ttu-id="93182-224">Дополнительные сведения см. в разделе [Создание и использование фрагментов кода](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="93182-224">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="93182-225">Дополнительные сведения о функциях языка Visual Basic, фрагменты кода IntelliSense, такие как настройка фрагментов и устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="93182-225">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="93182-226">Дополнительные сведения см. в разделе [фрагменты кода IntelliSense в Visual Basic](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="93182-226">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="93182-227">Дополнительные сведения о C#-отдельных функций IntelliSense, такие как рефакторинг и фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="93182-227">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="93182-228">Дополнительные сведения см. в разделе [IntelliSense для Visual C#](https://msdn.microsoft.com/library/43f44291.aspx).</span><span class="sxs-lookup"><span data-stu-id="93182-228">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
