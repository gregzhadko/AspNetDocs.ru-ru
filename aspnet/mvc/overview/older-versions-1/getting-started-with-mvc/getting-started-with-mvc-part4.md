---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Создание базы данных | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основные сведения по ASP.NET MVC. Создание простого веб-приложения, которое считывает и записывает в базу данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: b75057f3128662a9bbdd641dc0a7c1ba09fbbe87
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59388196"
---
# <a name="creating-a-database"></a><span data-ttu-id="09c88-104">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="09c88-104">Creating a Database</span></span>

<span data-ttu-id="09c88-105">по [(Scott hanselman)](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="09c88-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="09c88-106">Это руководство для начинающих, в котором представлены основные сведения по ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="09c88-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="09c88-107">Вы создадите простое веб-приложение, которое считывает и записывает в базу данных.</span><span class="sxs-lookup"><span data-stu-id="09c88-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="09c88-108">Посетите [центр обучения ASP.NET MVC](../../../index.md) для поиска других ASP.NET MVC, учебники и примеры.</span><span class="sxs-lookup"><span data-stu-id="09c88-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="09c88-109">В этом разделе мы собираемся создать новую SQL Express, мы будем использовать для хранения и извлечения данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="09c88-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="09c88-110">Из интегрированной среды разработки Visual Web Developer, выберите представление | Обозреватель серверов.</span><span class="sxs-lookup"><span data-stu-id="09c88-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="09c88-111">Щелкните правой кнопкой подключения к данным и нажмите кнопку Добавить соединение...</span><span class="sxs-lookup"><span data-stu-id="09c88-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="09c88-113">В диалоговом окне Выбор источника данных выберите Microsoft SQL Server и нажмите кнопку Продолжить.</span><span class="sxs-lookup"><span data-stu-id="09c88-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="09c88-114">В диалоговом окне "Добавить подключение", введите «. \SQLEXPRESS» для имени сервера и введите «Movies» в качестве имени новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="09c88-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

[![A<span data-ttu-id="09c88-115">диалоговое окно подключения дд]</span><span class="sxs-lookup"><span data-stu-id="09c88-115">dd Connection dialog]</span></span>(getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

<span data-ttu-id="09c88-116">Нажмите «ОК», и появляется если вы хотите создать эту базу данных.</span><span class="sxs-lookup"><span data-stu-id="09c88-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="09c88-117">Выберите "Да".</span><span class="sxs-lookup"><span data-stu-id="09c88-117">Select yes.</span></span>

[![C<span data-ttu-id="09c88-118">Создание фильмов?]</span><span class="sxs-lookup"><span data-stu-id="09c88-118">reate Movies?]</span></span>(getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

<span data-ttu-id="09c88-119">Теперь у вас есть пустой базы данных в обозревателе серверов.</span><span class="sxs-lookup"><span data-stu-id="09c88-119">Now you've got an empty database in Server Explorer.</span></span>

![Добавление новой таблицы](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="09c88-121">Щелкните правой кнопкой мыши в таблицах и нажмите кнопку Добавить таблицу.</span><span class="sxs-lookup"><span data-stu-id="09c88-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="09c88-122">Будет отображаться в конструкторе таблиц.</span><span class="sxs-lookup"><span data-stu-id="09c88-122">The Table Designer will appear.</span></span> <span data-ttu-id="09c88-123">Добавьте столбцы для Id, Title, ReleaseDate, Жанр и цена.</span><span class="sxs-lookup"><span data-stu-id="09c88-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="09c88-124">Щелкните правой кнопкой столбец идентификатора, и нажмите кнопку Задать первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="09c88-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="09c88-125">Вот какие моей области конструктора, как выглядит.</span><span class="sxs-lookup"><span data-stu-id="09c88-125">Here's what my design areas looks like.</span></span>

[![D<span data-ttu-id="09c88-126">Редактор таблиц азы данных]</span><span class="sxs-lookup"><span data-stu-id="09c88-126">atabase Table Editor]</span></span>(getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

<span data-ttu-id="09c88-127">Кроме того выберите столбец, идентификатор и в группе свойств столбца ниже изменить «Спецификация идентификатора» значение «Да».</span><span class="sxs-lookup"><span data-stu-id="09c88-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

[![I<span data-ttu-id="09c88-128">sIdentity - свойства столбца]</span><span class="sxs-lookup"><span data-stu-id="09c88-128">sIdentity - Column Properties]</span></span>(getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

<span data-ttu-id="09c88-129">Если у вас есть задачи, щелкните значок "Сохранить" на панели инструментов или выберите файл | Сохраните в меню и назовите таблицу "**фильма**" (в единственном числе).</span><span class="sxs-lookup"><span data-stu-id="09c88-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="09c88-130">У нас есть базы данных и таблицу!</span><span class="sxs-lookup"><span data-stu-id="09c88-130">We've got a database and a table!</span></span>

[![C<span data-ttu-id="09c88-131">Выберите имя]</span><span class="sxs-lookup"><span data-stu-id="09c88-131">hoose Name]</span></span>(getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

<span data-ttu-id="09c88-132">Вернитесь в обозреватель сервера и щелкните правой кнопкой мыши в таблице Movie, а затем выберите «Показать таблицу данных».</span><span class="sxs-lookup"><span data-stu-id="09c88-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="09c88-133">Введите несколько фильмов, поэтому нашей базе данных имеет некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="09c88-133">Enter a few movies so our database has some data.</span></span>

[![D<span data-ttu-id="09c88-134">Редактирование таблиц азы данных]</span><span class="sxs-lookup"><span data-stu-id="09c88-134">atabase Table Editing]</span></span>(getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a><span data-ttu-id="09c88-135">Создание модели</span><span class="sxs-lookup"><span data-stu-id="09c88-135">Creating a Model</span></span>

<span data-ttu-id="09c88-136">Теперь вернитесь в обозреватель решений, в правой части интегрированной среды разработки и щелкните папку Models правой кнопкой мыши и выберите Add | Новый элемент.</span><span class="sxs-lookup"><span data-stu-id="09c88-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

[![a<span data-ttu-id="09c88-137">ddnewmodelitem]</span><span class="sxs-lookup"><span data-stu-id="09c88-137">ddnewmodelitem]</span></span>(getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

<span data-ttu-id="09c88-138">Мы собираемся создать сущностную модель из нашей новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="09c88-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="09c88-139">Это добавит набора классов в наш проект, который упрощает процесс для нас для запроса и управления данными в базе данных.</span><span class="sxs-lookup"><span data-stu-id="09c88-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="09c88-140">Выберите узел данных в левой части диалогового окна и затем выберите шаблон элемента модели EDM ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="09c88-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="09c88-141">Назовите файл Movies.edmx.</span><span class="sxs-lookup"><span data-stu-id="09c88-141">Name it Movies.edmx.</span></span>

[![A<span data-ttu-id="09c88-142">ddNewDataModel]</span><span class="sxs-lookup"><span data-stu-id="09c88-142">ddNewDataModel]</span></span>(getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

<span data-ttu-id="09c88-143">Нажмите кнопку «Добавить».</span><span class="sxs-lookup"><span data-stu-id="09c88-143">Click the "Add" button.</span></span> <span data-ttu-id="09c88-144">Затем откроется «мастер моделей EDM».</span><span class="sxs-lookup"><span data-stu-id="09c88-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="09c88-145">В новое диалоговое окно, которое появляется выберите пункт Создать из базы данных.</span><span class="sxs-lookup"><span data-stu-id="09c88-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="09c88-146">Так как мы только что внесли базу данных, необходимо только сообщить о новой базе данных и соответствующей таблицей Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="09c88-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="09c88-147">Нажмите кнопку рядом с полем, сохранить наши подключения к базе данных в конфигурации нашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="09c88-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="09c88-148">Теперь проверьте таблицы и фильмов флажок и нажмите кнопку Готово.</span><span class="sxs-lookup"><span data-stu-id="09c88-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

[![E<span data-ttu-id="09c88-149">расходуемых мастер моделей EDM]</span><span class="sxs-lookup"><span data-stu-id="09c88-149">ntity Data Model Wizard]</span></span>(getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

<span data-ttu-id="09c88-150">Теперь мы см. в разделе нашей новой таблицы Movie в конструкторе Entity Framework и доступ к нему из кода.</span><span class="sxs-lookup"><span data-stu-id="09c88-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

[![M<span data-ttu-id="09c88-151">ovies - Microsoft Visual Web Developer 2010 Express]</span><span class="sxs-lookup"><span data-stu-id="09c88-151">ovies - Microsoft Visual Web Developer 2010 Express]</span></span>(getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

<span data-ttu-id="09c88-152">В области конструктора отобразится класс «Фильма».</span><span class="sxs-lookup"><span data-stu-id="09c88-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="09c88-153">Этот класс сопоставляется с таблицей «Фильма» в нашей базе данных, а каждое свойство в ней сопоставляет со столбцом с таблицей.</span><span class="sxs-lookup"><span data-stu-id="09c88-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="09c88-154">Каждый экземпляр класса «Фильма» будет соответствовать строки в таблице «Фильма».</span><span class="sxs-lookup"><span data-stu-id="09c88-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="09c88-155">Если вам не нравятся именования по умолчанию и сопоставления соглашения, используемые платформой Entity Framework, можно использовать конструктор Entity Framework, изменить или настроить их.</span><span class="sxs-lookup"><span data-stu-id="09c88-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="09c88-156">Для этого приложения будет использовать значения по умолчанию и сохраните файл как-является.</span><span class="sxs-lookup"><span data-stu-id="09c88-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="09c88-157">Теперь поработаем со некоторые реальные данные!</span><span class="sxs-lookup"><span data-stu-id="09c88-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="09c88-158">[Назад](getting-started-with-mvc-part3.md)
> [Вперед](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="09c88-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
