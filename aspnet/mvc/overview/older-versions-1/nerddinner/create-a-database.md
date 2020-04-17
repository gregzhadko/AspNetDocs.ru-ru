---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Создание базы данных | Документация Майкрософт
author: rick-anderson
description: Шаг 2 показывает шаги по созданию базы данных, содержащей все данные ужина и RSVP для нашего приложения NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541615"
---
# <a name="create-a-database"></a><span data-ttu-id="1c56c-103">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="1c56c-103">Create a Database</span></span>

<span data-ttu-id="1c56c-104">[корпорацией Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1c56c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1c56c-105">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="1c56c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="1c56c-106">Это шаг 2 [бесплатного "NerdDinner" приложение учебник,](introducing-the-nerddinner-tutorial.md) который ходит через как построить небольшой, но полный, веб-приложение с помощью ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="1c56c-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="1c56c-107">Шаг 2 показывает шаги по созданию базы данных, содержащей все данные ужина и RSVP для нашего приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="1c56c-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="1c56c-108">Если вы используете ASP.NET MVC 3, мы рекомендуем вам следовать [начиная с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.</span><span class="sxs-lookup"><span data-stu-id="1c56c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="1c56c-109">NerdDinner Шаг 2: Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="1c56c-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="1c56c-110">Мы будем использовать базу данных для хранения всех данных Dinner и RSVP для нашего приложения NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="1c56c-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="1c56c-111">На приведенных ниже шагах показано создание базы данных с помощью бесплатного издания S'L Server Express (которое можно легко установить с помощью V2 [установки веб-платформы Microsoft).](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="1c56c-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="1c56c-112">Весь код, который мы напишем, работает как с S'L Server Express, так и с полным сервером S'L.</span><span class="sxs-lookup"><span data-stu-id="1c56c-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="1c56c-113">Создание новой базы данных сервера S'L Server Express</span><span class="sxs-lookup"><span data-stu-id="1c56c-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="1c56c-114">Начнем с нажатия правого нажима на наш веб-проект, а затем выберем команду меню **Add-&gt;New Item:**</span><span class="sxs-lookup"><span data-stu-id="1c56c-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="1c56c-115">Это позволит поднять Visual Studio в "Добавить новый пункт" диалог.</span><span class="sxs-lookup"><span data-stu-id="1c56c-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="1c56c-116">Мы отфильтруем по категории "Данные" и выберем шаблон элемента "База данных серверов":</span><span class="sxs-lookup"><span data-stu-id="1c56c-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="1c56c-117">Мы назовем базу данных сервера S'L Server Express, которая мы хотим создать "NerdDinner.mdf" и ударить нормально.</span><span class="sxs-lookup"><span data-stu-id="1c56c-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="1c56c-118">Visual Studio спросит нас, хотим ли мы добавить\_этот файл в наш каталог данных приложения (который уже настроен с помощью ACL-аналитики безопасности как для чтения),</span><span class="sxs-lookup"><span data-stu-id="1c56c-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="1c56c-119">Мы нажмем кнопку "Да", и наша новая база данных будет создана и добавлена в наш Solution Explorer:</span><span class="sxs-lookup"><span data-stu-id="1c56c-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="1c56c-120">Создание таблиц в нашей базе данных</span><span class="sxs-lookup"><span data-stu-id="1c56c-120">Creating Tables within our Database</span></span>

<span data-ttu-id="1c56c-121">Теперь у нас есть новая пустая база данных.</span><span class="sxs-lookup"><span data-stu-id="1c56c-121">We now have a new empty database.</span></span> <span data-ttu-id="1c56c-122">Давайте добавим к нему несколько таблиц.</span><span class="sxs-lookup"><span data-stu-id="1c56c-122">Let's add some tables to it.</span></span>

<span data-ttu-id="1c56c-123">Для этого мы перейдем к окну вкладок "Server Explorer" в Visual Studio, что позволяет нам управлять базами данных и серверами.</span><span class="sxs-lookup"><span data-stu-id="1c56c-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="1c56c-124">Базы данных сервера Сервер экспресс, хранящиеся в папке «Данные приложения»\_нашего приложения, будут автоматически отображаться в серверном исследователе.</span><span class="sxs-lookup"><span data-stu-id="1c56c-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="1c56c-125">Мы можем дополнительно использовать значок «Подключение к базе данных» в верхней части окна «Исследователь сервера», чтобы добавить в список дополнительные базы данных сервера S'L (как локальные, так и удаленные):</span><span class="sxs-lookup"><span data-stu-id="1c56c-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="1c56c-126">Мы добавим две таблицы в нашу базу данных NerdDinner - один для хранения наших dinners, а другой для отслеживания RSVP приемов к ним.</span><span class="sxs-lookup"><span data-stu-id="1c56c-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="1c56c-127">Мы можем создать новые таблицы, нажав правой кнопкой мыши на папке "Таблицы" в нашей базе данных и выбрав команду меню "Добавить новый стол":</span><span class="sxs-lookup"><span data-stu-id="1c56c-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="1c56c-128">Это откроет конструктор таблицы, что позволяет нам настроить схему нашей таблицы.</span><span class="sxs-lookup"><span data-stu-id="1c56c-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="1c56c-129">Для нашей таблицы "Dinners" мы добавим 10 столбцов данных:</span><span class="sxs-lookup"><span data-stu-id="1c56c-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="1c56c-130">Мы хотим, чтобы колонка "DinnerID" была уникальным основным ключом для таблицы.</span><span class="sxs-lookup"><span data-stu-id="1c56c-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="1c56c-131">Мы можем настроить это, нажав правой кнопкой мыши на столбце "DinnerID" и выбрав элемент меню "Set Primary Key":</span><span class="sxs-lookup"><span data-stu-id="1c56c-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="1c56c-132">В дополнение к тому, чтобы сделать DinnerID основным ключом, мы также хотим настроить его как "идентичность" столбец, значение которого автоматически приращено, как новые строки данных добавляются в таблицу (имеется в виду первый вставлен ужин строки будет иметь DinnerID 1, второй вставленный ряд будет иметь DinnerID 2, и т.д.).</span><span class="sxs-lookup"><span data-stu-id="1c56c-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="1c56c-133">Мы можем сделать это, выбрав столбец "DinnerID", а затем используйте редактор "Column Properties" для установки свойства "(Is Identity)" на столбце "Да".</span><span class="sxs-lookup"><span data-stu-id="1c56c-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="1c56c-134">Мы будем использовать стандартные значения идентификации (начало с 1 и приращение 1 на каждой новой строке Ужина):</span><span class="sxs-lookup"><span data-stu-id="1c56c-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="1c56c-135">Затем мы сохраним нашу таблицу, введя Ctrl-S или используя команду меню **&gt;File- Save.**</span><span class="sxs-lookup"><span data-stu-id="1c56c-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="1c56c-136">Это подскажет нам назвать таблицу.</span><span class="sxs-lookup"><span data-stu-id="1c56c-136">This will prompt us to name the table.</span></span> <span data-ttu-id="1c56c-137">Мы назовем его "Ужины":</span><span class="sxs-lookup"><span data-stu-id="1c56c-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="1c56c-138">Наша новая таблица Dinners будет отображаться в нашей базе данных в сервере explorer.</span><span class="sxs-lookup"><span data-stu-id="1c56c-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="1c56c-139">Затем мы повторим вышеуказанные шаги и создадим таблицу "RSVP".</span><span class="sxs-lookup"><span data-stu-id="1c56c-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="1c56c-140">Эта таблица с 3 колонками.</span><span class="sxs-lookup"><span data-stu-id="1c56c-140">This table with have 3 columns.</span></span> <span data-ttu-id="1c56c-141">Мы наведием столбец RsvpID в качестве основного ключа, а также сделаем его столбцом идентификации:</span><span class="sxs-lookup"><span data-stu-id="1c56c-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="1c56c-142">Мы сохраним его и дадим ему название "RSVP".</span><span class="sxs-lookup"><span data-stu-id="1c56c-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="1c56c-143">Настройка взаимоотношений между таблицами для иностранных ключей</span><span class="sxs-lookup"><span data-stu-id="1c56c-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="1c56c-144">Теперь у нас есть две таблицы в нашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="1c56c-144">We now have two tables within our database.</span></span> <span data-ttu-id="1c56c-145">Наш последний шаг проектирования схемы будет устанавливать "один к многим" отношения между этими двумя таблицами - так что мы можем связать каждый ужин строки с нулем или более RSVP строки, которые применяются к нему.</span><span class="sxs-lookup"><span data-stu-id="1c56c-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="1c56c-146">Мы сделаем это путем настройки таблицы RSVP "DinnerID" колонке иметь иностранного ключа отношения с "DinnerID" колонке в таблице "Ужины".</span><span class="sxs-lookup"><span data-stu-id="1c56c-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="1c56c-147">Для этого мы откроем таблицу RSVP в таблице дизайнера, дважды нажав на него в исследователье сервера.</span><span class="sxs-lookup"><span data-stu-id="1c56c-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="1c56c-148">Затем мы выберем столбец "DinnerID" в ней, право-нажмите кнопку, и выберите "Отношения ..." команда контекстного меню:</span><span class="sxs-lookup"><span data-stu-id="1c56c-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="1c56c-149">Это позволит вывести диалог, который мы можем использовать для настройки отношений между таблицами:</span><span class="sxs-lookup"><span data-stu-id="1c56c-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="1c56c-150">Мы нажмем кнопку "Добавить", чтобы добавить новое отношение к диалогу.</span><span class="sxs-lookup"><span data-stu-id="1c56c-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="1c56c-151">Как только связь была добавлена, мы расширим "Таблицы и колонки спецификации" дерево-вид узла в сетке свойств вправо от диалога, а затем нажмите "..." кнопка справа от него:</span><span class="sxs-lookup"><span data-stu-id="1c56c-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="1c56c-152">Нажав на кнопку "..." кнопка подведет еще один диалог, который позволяет нам указать, какие таблицы и столбцы участвуют в отношениях, а также позволит нам назвать отношения.</span><span class="sxs-lookup"><span data-stu-id="1c56c-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="1c56c-153">Мы изменим основной ключевой стол, чтобы быть "Ужины", и выберем столбец "DinnerID" в таблице Dinners в качестве основного ключа.</span><span class="sxs-lookup"><span data-stu-id="1c56c-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="1c56c-154">Наша таблица RSVP будет таблицей с иностранными ключами, и RSVP. Колонка DinnerID будет ассоциироваться как иностранный ключ:</span><span class="sxs-lookup"><span data-stu-id="1c56c-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="1c56c-155">Теперь каждая строка в таблице RSVP будет ассоциироваться со строкой в таблице Ужин.</span><span class="sxs-lookup"><span data-stu-id="1c56c-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="1c56c-156">Сервер S'L будет поддерживать референциальную целостность для нас – и не позволит нам добавить новую строку RSVP, если она не указывает на действительную строку Ужин.</span><span class="sxs-lookup"><span data-stu-id="1c56c-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="1c56c-157">Это также не позволит нам удалять строку Ужин, если Есть еще RSVP строки, ссылаясь на него.</span><span class="sxs-lookup"><span data-stu-id="1c56c-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="1c56c-158">Добавление данных в наши таблицы</span><span class="sxs-lookup"><span data-stu-id="1c56c-158">Adding Data to our Tables</span></span>

<span data-ttu-id="1c56c-159">Давайте закончим, добавив некоторые примеры данных в нашу таблицу Ужины.</span><span class="sxs-lookup"><span data-stu-id="1c56c-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="1c56c-160">Мы можем добавить данные в таблицу, нажав на нее в правом доступе в Server Explorer и выбрав команду "Показать таблицу":</span><span class="sxs-lookup"><span data-stu-id="1c56c-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="1c56c-161">Мы добавим несколько строк данных Ужина, которые мы можем использовать позже, когда мы начинаем реализацию приложения:</span><span class="sxs-lookup"><span data-stu-id="1c56c-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="1c56c-162">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="1c56c-162">Next Step</span></span>

<span data-ttu-id="1c56c-163">Мы закончили создавать нашу базу данных.</span><span class="sxs-lookup"><span data-stu-id="1c56c-163">We've finished creating our database.</span></span> <span data-ttu-id="1c56c-164">Теперь создадим классы моделей, которые мы можем использовать для запроса и обновления.</span><span class="sxs-lookup"><span data-stu-id="1c56c-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c56c-165">[Назад](create-a-new-aspnet-mvc-project.md)
> [Вперед](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="1c56c-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
