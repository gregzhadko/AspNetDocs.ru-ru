---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Создание базы данных | Документация Майкрософт
author: microsoft
description: Шаг 2 показано, как создать базу данных, содержащий все компании dinner и RSVP данных для нашего приложения NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: 6299e5d306ce59687d91658e36685cc6b3255269
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415067"
---
# <a name="create-a-database"></a><span data-ttu-id="d8dff-103">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="d8dff-103">Create a Database</span></span>

<span data-ttu-id="d8dff-104">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d8dff-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d8dff-105">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="d8dff-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d8dff-106">Это бесплатная этап 2 [руководство по использованию приложения «NerdDinner»](introducing-the-nerddinner-tutorial.md) , пошаговое рассмотрение как создать небольшой, но завершить, веб-приложения с помощью ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="d8dff-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d8dff-107">Шаг 2 показано, как создать базу данных, содержащий все компании dinner и RSVP данных для нашего приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="d8dff-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="d8dff-108">Если вы используете ASP.NET MVC 3, рекомендуется следовать [Приступая к работе с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.</span><span class="sxs-lookup"><span data-stu-id="d8dff-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="d8dff-109">NerdDinner Step 2: Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="d8dff-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="d8dff-110">Мы будем использовать базу данных для хранения всех данных компании Dinner и RSVP для нашего приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="d8dff-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="d8dff-111">Ниже описывается создание базы данных, через бесплатный выпуск SQL Server Express (который можно легко установить с помощью версии 2 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d8dff-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="d8dff-112">Весь код, мы напишем работает с SQL Server Express и полной версии SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d8dff-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="d8dff-113">Создание новой базы данных SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="d8dff-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="d8dff-114">Мы будем начать, щелкните правой кнопкой мыши на нашем веб-проект, а затем выберите **Add -&gt;новый элемент** команды меню:</span><span class="sxs-lookup"><span data-stu-id="d8dff-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="d8dff-115">Откроется диалоговое окно «Добавление нового элемента» Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8dff-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="d8dff-116">Мы фильтрация по категории «Данные» и выберите шаблон элемента «Базы данных SQL Server»:</span><span class="sxs-lookup"><span data-stu-id="d8dff-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="d8dff-117">Мы будем называть базы данных SQL Server Express, которую мы хотим создать «NerdDinner.mdf» и нажмите ok.</span><span class="sxs-lookup"><span data-stu-id="d8dff-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="d8dff-118">Visual Studio будет запрошен нам если нам нужно добавить этот файл к нашей \App\_каталог данных (который уже является каталогом установки с помощью чтения и записи списков управления доступом):</span><span class="sxs-lookup"><span data-stu-id="d8dff-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="d8dff-119">Щелкнем «Yes» и новой базе данных будет создан и добавлен в наш обозреватель решений:</span><span class="sxs-lookup"><span data-stu-id="d8dff-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="d8dff-120">Создание таблиц в базе данных</span><span class="sxs-lookup"><span data-stu-id="d8dff-120">Creating Tables within our Database</span></span>

<span data-ttu-id="d8dff-121">Теперь у нас есть новой пустой базы данных.</span><span class="sxs-lookup"><span data-stu-id="d8dff-121">We now have a new empty database.</span></span> <span data-ttu-id="d8dff-122">Давайте добавим некоторые таблицы к ней.</span><span class="sxs-lookup"><span data-stu-id="d8dff-122">Let's add some tables to it.</span></span>

<span data-ttu-id="d8dff-123">Для этого перейдем на вкладку окна «Обозреватель серверов» в Visual Studio, которая позволяет нам управлять базами данных и серверами.</span><span class="sxs-lookup"><span data-stu-id="d8dff-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="d8dff-124">SQL Server Express базы данных, хранящиеся в \App\_папку данных приложения будут автоматически отображаться в обозревателе серверов.</span><span class="sxs-lookup"><span data-stu-id="d8dff-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="d8dff-125">При необходимости можно использовать значок «Соединение с базой данных» в верхней части окна «Обозреватель серверов» для добавления в список, а также дополнительные базы данных SQL Server (локальные и удаленные):</span><span class="sxs-lookup"><span data-stu-id="d8dff-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="d8dff-126">Мы добавим две таблицы к базе данных NerdDinner — один для хранения наших ужинов, а другой для отслеживания RSVP принятия к ним.</span><span class="sxs-lookup"><span data-stu-id="d8dff-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="d8dff-127">Мы можем создать новые таблицы, щелкнув правой кнопкой мыши на папку «Таблицы» в базе данных и выбрав команду меню «Добавить новую таблицу»:</span><span class="sxs-lookup"><span data-stu-id="d8dff-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="d8dff-128">Откроется конструктор таблиц, который позволяет настроить схему нашей таблице.</span><span class="sxs-lookup"><span data-stu-id="d8dff-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="d8dff-129">Для нашей таблице «Ужинов» мы добавим 10 столбцов данных:</span><span class="sxs-lookup"><span data-stu-id="d8dff-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="d8dff-130">Нам нужен столбец «DinnerID» уникальным первичным ключом для таблицы.</span><span class="sxs-lookup"><span data-stu-id="d8dff-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="d8dff-131">Это можно настроить, щелкнув правой кнопкой мыши по столбцу «DinnerID» и выбрав пункт меню «Задать первичный ключ»:</span><span class="sxs-lookup"><span data-stu-id="d8dff-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="d8dff-132">Кроме того, что DinnerID первичный ключ, также необходимо настроить его как столбец «identity», значение которого автоматически увеличивается при добавлении новых строк данных в таблицу (первая строка вставленных компании Dinner будет иметь DinnerID 1 это означает, что второй вставляемые строки будет иметь DinnerID 2, и т.д.).</span><span class="sxs-lookup"><span data-stu-id="d8dff-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="d8dff-133">Мы можно сделать, выбрав столбец «DinnerID» и затем с помощью редактора «Свойства столбца» для установки свойства "(Is Identity)» в столбце «Да».</span><span class="sxs-lookup"><span data-stu-id="d8dff-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="d8dff-134">Мы будем использовать значения по умолчанию стандартные удостоверения (начинаются с 1 и увеличивается на 1 на каждой новой строки Dinner):</span><span class="sxs-lookup"><span data-stu-id="d8dff-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="d8dff-135">Мы затем вернемся к нашей таблице, введя сочетание клавиш Ctrl-S или с помощью **файл -&gt;Сохранить** команды меню.</span><span class="sxs-lookup"><span data-stu-id="d8dff-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="d8dff-136">Это будет предложено нам имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="d8dff-136">This will prompt us to name the table.</span></span> <span data-ttu-id="d8dff-137">Назовем его «Ужинов»:</span><span class="sxs-lookup"><span data-stu-id="d8dff-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="d8dff-138">После этого нашей новой таблицы ужинов появится в базе данных в обозревателе серверов.</span><span class="sxs-lookup"><span data-stu-id="d8dff-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="d8dff-139">Затем мы повторите описанные выше шаги и создайте таблицу «RSVP».</span><span class="sxs-lookup"><span data-stu-id="d8dff-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="d8dff-140">Эта таблица с 3 столбцами.</span><span class="sxs-lookup"><span data-stu-id="d8dff-140">This table with have 3 columns.</span></span> <span data-ttu-id="d8dff-141">Мы установки RsvpID столбец как первичный ключ и ухудшить его в столбец идентификаторов:</span><span class="sxs-lookup"><span data-stu-id="d8dff-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="d8dff-142">Мы сохраните его и присвойте ему имя «RSVP».</span><span class="sxs-lookup"><span data-stu-id="d8dff-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="d8dff-143">Настройка внешнего ключа между таблицами</span><span class="sxs-lookup"><span data-stu-id="d8dff-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="d8dff-144">Теперь у нас есть две таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="d8dff-144">We now have two tables within our database.</span></span> <span data-ttu-id="d8dff-145">Наши последний этап разработки схемы будет настроить отношение «один ко многим» между этими двумя таблицами — таким образом, чтобы мы можно связать каждую строку Dinner с ноль или более строк RSVP, применяемых к этому.</span><span class="sxs-lookup"><span data-stu-id="d8dff-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="d8dff-146">Мы сделаем это путем настройки столбца таблицы RSVP «DinnerID» требуется отношение внешнего ключа в столбец «DinnerID» в таблице «Ужинов».</span><span class="sxs-lookup"><span data-stu-id="d8dff-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="d8dff-147">Чтобы сделать это, мы откроем RSVP таблицу в конструкторе таблиц, дважды щелкнув его в обозревателе серверов.</span><span class="sxs-lookup"><span data-stu-id="d8dff-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="d8dff-148">Затем мы выберем столбец «DinnerID», щелкните правой кнопкой мыши и выберите «Связей...» Команда контекстного меню:</span><span class="sxs-lookup"><span data-stu-id="d8dff-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="d8dff-149">Откроется диалоговое окно, можно использовать для установки связи между таблицами:</span><span class="sxs-lookup"><span data-stu-id="d8dff-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="d8dff-150">Мы щелкнем кнопку «Добавить», чтобы добавить новое отношение к диалоговому окну.</span><span class="sxs-lookup"><span data-stu-id="d8dff-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="d8dff-151">После добавления связи, мы будем разверните узел дерева «Спецификация таблиц и столбцов» в сетке свойств в правой части диалогового окна и нажмите кнопку «...» справа от его:</span><span class="sxs-lookup"><span data-stu-id="d8dff-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="d8dff-152">Нажатие кнопки «...» появится другое диалоговое окно, можно указать, какие таблицы и столбцы, участвующие в связи, а также позволяет нам имя связи.</span><span class="sxs-lookup"><span data-stu-id="d8dff-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="d8dff-153">Мы изменить первичный ключ таблицы «Ужинов» и выберите столбец «DinnerID» в таблице ужинов как первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="d8dff-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="d8dff-154">В таблице внешнего ключа и RSVP, будет нашей таблице RSVP. Столбец DinnerID будет связан как внешний ключ:</span><span class="sxs-lookup"><span data-stu-id="d8dff-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="d8dff-155">Теперь каждой строки в таблице RSVP будет связан со строкой в таблице ужин.</span><span class="sxs-lookup"><span data-stu-id="d8dff-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="d8dff-156">SQL Server будет ссылочной целостности для нас — и запрет нам добавления новой строки RSVP, если он не указывает на действительную строку ужин.</span><span class="sxs-lookup"><span data-stu-id="d8dff-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="d8dff-157">Он также предотвратит нам Dinner строка удаляется, если по-прежнему RSVP строки, ссылающиеся на него.</span><span class="sxs-lookup"><span data-stu-id="d8dff-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="d8dff-158">Добавление данных в нашей таблицы</span><span class="sxs-lookup"><span data-stu-id="d8dff-158">Adding Data to our Tables</span></span>

<span data-ttu-id="d8dff-159">Давайте Готово, добавив к нашей таблице ужинов демонстрационные данные.</span><span class="sxs-lookup"><span data-stu-id="d8dff-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="d8dff-160">Можно добавить данные в таблицу, щелкнув его в обозревателе серверов и выбрав команду «Показать таблицу данных»:</span><span class="sxs-lookup"><span data-stu-id="d8dff-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="d8dff-161">Мы добавим несколько строк данных компании Dinner, который можно использовать позднее, когда мы начнем реализовывать приложения:</span><span class="sxs-lookup"><span data-stu-id="d8dff-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="d8dff-162">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="d8dff-162">Next Step</span></span>

<span data-ttu-id="d8dff-163">Мы завершили создание нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="d8dff-163">We've finished creating our database.</span></span> <span data-ttu-id="d8dff-164">Теперь создадим классов модели, которые можно использовать для запроса и обновить его.</span><span class="sxs-lookup"><span data-stu-id="d8dff-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d8dff-165">[Назад](create-a-new-aspnet-mvc-project.md)
> [Вперед](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="d8dff-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
