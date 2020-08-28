---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: Добавление нового поля | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045147"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="b1f60-102">Добавление нового поля</span><span class="sxs-lookup"><span data-stu-id="b1f60-102">Adding a New Field</span></span>

<span data-ttu-id="b1f60-103">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b1f60-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="b1f60-104">В этом разделе вы будете использовать Entity Framework Code First Migrations для переноса некоторых изменений в классы модели, чтобы изменения применялись к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="b1f60-105">По умолчанию при использовании Entity Framework Code First для автоматического создания базы данных, как это было сделано ранее в этом руководстве, Code First добавляет таблицу в базу данных, чтобы определить, синхронизирована ли схема базы данных с классами модели, из которых она была создана.</span><span class="sxs-lookup"><span data-stu-id="b1f60-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="b1f60-106">Если они не синхронизированы, Entity Framework выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="b1f60-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="b1f60-107">Это упрощает отслеживание проблем во время разработки, которые в противном случае могут быть найдены (путем маскировки ошибок) во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="b1f60-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="b1f60-108">Настройка Code First Migrations для изменений модели</span><span class="sxs-lookup"><span data-stu-id="b1f60-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="b1f60-109">Перейдите к обозреватель решений.</span><span class="sxs-lookup"><span data-stu-id="b1f60-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="b1f60-110">Щелкните правой кнопкой мыши файл *movies. mdf* и выберите **Удалить** , чтобы удалить базу данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="b1f60-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="b1f60-111">Если файл *movies. mdf* не отображается, щелкните значок **Показать все файлы** , показанный ниже в красном контуре.</span><span class="sxs-lookup"><span data-stu-id="b1f60-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="b1f60-112">Постройте приложение, чтобы убедиться в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="b1f60-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="b1f60-113">В меню **Сервис** выберите **Диспетчер пакетов NuGet** , а затем **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="b1f60-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Добавить пакет man](adding-a-new-field/_static/image2.png)

<span data-ttu-id="b1f60-115">В окне **консоли диспетчера пакетов** в `PM>` командной строке введите</span><span class="sxs-lookup"><span data-stu-id="b1f60-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="b1f60-116">Включение и миграция — ContextTypeName MvcMovie. Models. Мовиедбконтекст</span><span class="sxs-lookup"><span data-stu-id="b1f60-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="b1f60-117">Команда **включить-миграции** (показанная выше) создает файл *Configuration.CS* в новой папке *migrations* .</span><span class="sxs-lookup"><span data-stu-id="b1f60-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="b1f60-118">Visual Studio откроет файл *Configuration.CS* .</span><span class="sxs-lookup"><span data-stu-id="b1f60-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="b1f60-119">Замените `Seed` метод в файле *Configuration.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b1f60-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="b1f60-120">Наведите указатель мыши на красную волнистую линию в разделе `Movie` и щелкните `Show Potential Fixes` , а затем выберите **Использование** **MvcMovie. Models;**</span><span class="sxs-lookup"><span data-stu-id="b1f60-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="b1f60-121">При этом добавляется следующая инструкция using:</span><span class="sxs-lookup"><span data-stu-id="b1f60-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="b1f60-122">Code First Migrations вызывает `Seed` метод после каждой миграции (то есть вызывает **Обновление базы данных** в консоли диспетчера пакетов), и этот метод обновляет уже вставленные строки или вставляет их, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="b1f60-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="b1f60-123">Метод [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) в следующем коде выполняет операцию "Upsert":</span><span class="sxs-lookup"><span data-stu-id="b1f60-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="b1f60-124">Поскольку метод [SEED](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) выполняется при каждой миграции, вы не можете просто вставлять данные, так как добавляемые строки уже будут существовать после первой миграции, создающей базу данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="b1f60-125">Операция "[Upsert](http://en.wikipedia.org/wiki/Upsert)" предотвращает ошибки, которые могут возникать при попытке вставить уже существующую строку, но переопределяет любые изменения данных, которые могли быть сделаны при тестировании приложения.</span><span class="sxs-lookup"><span data-stu-id="b1f60-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="b1f60-126">При использовании тестовых данных в некоторых таблицах может быть нежелательно: в некоторых случаях при изменении данных во время тестирования необходимо сохранить изменения после обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="b1f60-127">В этом случае необходимо выполнить операцию условной вставки: вставить строку, если она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="b1f60-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="b1f60-128">Первый параметр, передаваемый методу [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) , указывает свойство, используемое для проверки, существует ли уже строка.</span><span class="sxs-lookup"><span data-stu-id="b1f60-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="b1f60-129">Для этой цели можно использовать свойство тестовых данных видеофильмов, `Title` так как каждый заголовок в списке уникален:</span><span class="sxs-lookup"><span data-stu-id="b1f60-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="b1f60-130">В этом коде предполагается, что заголовки являются уникальными.</span><span class="sxs-lookup"><span data-stu-id="b1f60-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="b1f60-131">Если вы вручную добавите повторяющееся название, вы получите следующее исключение при следующем выполнении миграции.</span><span class="sxs-lookup"><span data-stu-id="b1f60-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="b1f60-132">*Последовательность содержит более одного элемента*</span><span class="sxs-lookup"><span data-stu-id="b1f60-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="b1f60-133">Дополнительные сведения о методе [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) см. в разделе [использование метода AddOrUpdate EF 4,3](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/).</span><span class="sxs-lookup"><span data-stu-id="b1f60-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="b1f60-134">**Нажмите клавиши CTRL + SHIFT + B, чтобы выполнить сборку проекта.** (Если на этом этапе не выполняется сборка, следующие действия завершаются ошибкой.)</span><span class="sxs-lookup"><span data-stu-id="b1f60-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="b1f60-135">Следующим шагом является создание `DbMigration` класса для первоначальной миграции.</span><span class="sxs-lookup"><span data-stu-id="b1f60-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="b1f60-136">При такой миграции создается новая база данных, поэтому файл *Movie. mdf* был удален на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b1f60-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="b1f60-137">В окне **консоли диспетчера пакетов** введите команду, `add-migration Initial` чтобы создать первоначальную миграцию.</span><span class="sxs-lookup"><span data-stu-id="b1f60-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="b1f60-138">Имя «Initial» является произвольным и используется для имени создаваемого файла миграции.</span><span class="sxs-lookup"><span data-stu-id="b1f60-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="b1f60-139">Code First Migrations создает другой файл класса в папке *migrations* (с именем *{датестамп} \_ Initial.CS* ), а этот класс содержит код, создающий схему базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="b1f60-140">Имя файла миграции предварительно исправлено с меткой времени, помогающей в упорядочении.</span><span class="sxs-lookup"><span data-stu-id="b1f60-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="b1f60-141">Изучите файл \* \_ Initial.CS {датестамп}\* , содержащий инструкции по созданию `Movies` таблицы для базы данных Movie.</span><span class="sxs-lookup"><span data-stu-id="b1f60-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="b1f60-142">При обновлении базы данных в приведенных ниже инструкциях будет запущен файл \* \_ Initial.CS {датестамп}\* и создана схема базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="b1f60-143">Затем будет выполнен метод **SEED** для заполнения базы данных тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="b1f60-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="b1f60-144">В **консоли диспетчера пакетов**введите команду, `update-database` чтобы создать базу данных, и запустите `Seed` метод.</span><span class="sxs-lookup"><span data-stu-id="b1f60-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="b1f60-145">Если появляется сообщение об ошибке, показывающее, что таблица уже существует и не может быть создана, возможно, приложение было запущено после удаления базы данных и перед выполнением `update-database` .</span><span class="sxs-lookup"><span data-stu-id="b1f60-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="b1f60-146">В этом случае удалите файл *movies. mdf* еще раз и повторите `update-database` команду.</span><span class="sxs-lookup"><span data-stu-id="b1f60-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="b1f60-147">Если вы по-прежнему получаете сообщение об ошибке, удалите папку и содержимое миграции, а затем начните с указания в верхней части этой страницы (которая удаляет файл *movies. mdf* , а затем переходит к включению-миграции).</span><span class="sxs-lookup"><span data-stu-id="b1f60-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="b1f60-148">Если вы по-прежнему получаете ошибку, откройте обозреватель объектов SQL Server и удалите базу данных из списка.</span><span class="sxs-lookup"><span data-stu-id="b1f60-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="b1f60-149">Запустите приложение и перейдите по URL-адресу */Movies* .</span><span class="sxs-lookup"><span data-stu-id="b1f60-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="b1f60-150">Отобразятся начальные данные.</span><span class="sxs-lookup"><span data-stu-id="b1f60-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="b1f60-151">Добавление свойства Rating в модель Movie</span><span class="sxs-lookup"><span data-stu-id="b1f60-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="b1f60-152">Начните с добавления нового `Rating` свойства в существующий `Movie` класс.</span><span class="sxs-lookup"><span data-stu-id="b1f60-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="b1f60-153">Откройте файл *моделс\мовие.КС* и добавьте `Rating` свойство следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b1f60-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="b1f60-154">Теперь полный `Movie` класс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b1f60-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="b1f60-155">Постройте приложение (Ctrl + Shift + B).</span><span class="sxs-lookup"><span data-stu-id="b1f60-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="b1f60-156">Так как вы добавили в класс новое поле `Movie` , вам также нужно обновить *белый список* привязки, чтобы включить это новое свойство.</span><span class="sxs-lookup"><span data-stu-id="b1f60-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="b1f60-157">Обновите `bind` атрибут для `Create` `Edit` методов действия и, чтобы включить `Rating` свойство:</span><span class="sxs-lookup"><span data-stu-id="b1f60-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="b1f60-158">Также необходимо обновить шаблоны представлений, чтобы реализовать отображение, создание и редактирование нового свойства `Rating` в представлении браузера.</span><span class="sxs-lookup"><span data-stu-id="b1f60-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="b1f60-159">Откройте файл *\виевс\мовиес\индекс.кштмл* и добавьте `<th>Rating</th>` заголовок столбца сразу после столбца **Price** .</span><span class="sxs-lookup"><span data-stu-id="b1f60-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="b1f60-160">Затем добавьте `<td>` столбец рядом с концом шаблона, чтобы отобразить `@item.Rating` значение.</span><span class="sxs-lookup"><span data-stu-id="b1f60-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="b1f60-161">Ниже показано, как выглядит обновленный шаблон представления *index. cshtml* :</span><span class="sxs-lookup"><span data-stu-id="b1f60-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="b1f60-162">Затем откройте файл *\виевс\мовиес\креате.кштмл* и добавьте `Rating` поле со следующей выделенной разметкой.</span><span class="sxs-lookup"><span data-stu-id="b1f60-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="b1f60-163">При этом текстовое поле подготавливается к просмотру, что позволяет указать рейтинг при создании нового фильма.</span><span class="sxs-lookup"><span data-stu-id="b1f60-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="b1f60-164">Теперь вы обновили код приложения для поддержки нового `Rating` Свойства.</span><span class="sxs-lookup"><span data-stu-id="b1f60-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="b1f60-165">Запустите приложение и перейдите по URL-адресу */Movies* .</span><span class="sxs-lookup"><span data-stu-id="b1f60-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="b1f60-166">Однако при этом вы увидите одну из следующих ошибок:</span><span class="sxs-lookup"><span data-stu-id="b1f60-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="b1f60-167">Модель, которая является резервной моделью контекста "Мовиедбконтекст", изменилась с момента создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="b1f60-168">Рекомендуется использовать Code First Migrations для обновления базы данных ( https://go.microsoft.com/fwlink/?LinkId=238269) .</span><span class="sxs-lookup"><span data-stu-id="b1f60-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="b1f60-169">Вы видите эту ошибку, так как обновленный `Movie` класс модели в приложении отличается от схемы `Movie` таблицы существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="b1f60-170">(В таблице базы данных отсутствует столбец `Rating`.)</span><span class="sxs-lookup"><span data-stu-id="b1f60-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="b1f60-171">Устранить эту ошибку можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="b1f60-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="b1f60-172">Можно с помощью Entity Framework автоматически удалить и повторно создать базу данных на основе новой схемы класса модели.</span><span class="sxs-lookup"><span data-stu-id="b1f60-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="b1f60-173">Этот подход удобен на ранних стадиях цикла разработки, когда все действия осуществляются с тестовой базой данных. В этом случае развитие модели и схемы базы данных осуществляется одновременно.</span><span class="sxs-lookup"><span data-stu-id="b1f60-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="b1f60-174">Недостаток этого подхода заключается в том, что в базе данных теряются существующие данные — поэтому вы *не* хотите использовать этот подход в рабочей базе данных!</span><span class="sxs-lookup"><span data-stu-id="b1f60-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="b1f60-175">При разработке приложения часто используется инициализатор для автоматического заполнения базы тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="b1f60-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="b1f60-176">Дополнительные сведения об Entity Framework инициализаторах баз данных см. в разделе [ASP.NET MVC/Entity Framework Tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="b1f60-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="b1f60-177">Можно явно изменить схему существующей базы данных в соответствии с новыми классами модели.</span><span class="sxs-lookup"><span data-stu-id="b1f60-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="b1f60-178">Преимущество такого подхода состоит в том, что сохраняются все данные.</span><span class="sxs-lookup"><span data-stu-id="b1f60-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="b1f60-179">Это изменение можно выполнить как вручную, так и с помощью соответствующего скрипта базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="b1f60-180">Можно обновить схему базы данных с помощью Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="b1f60-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="b1f60-181">В этом руководстве используется Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="b1f60-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="b1f60-182">Обновите метод SEED, чтобы он выдает значение для нового столбца.</span><span class="sxs-lookup"><span data-stu-id="b1f60-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="b1f60-183">Откройте файл Migrations\Configuration.cs и добавьте поле рейтинга в каждый объект Movie.</span><span class="sxs-lookup"><span data-stu-id="b1f60-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="b1f60-184">Выполните сборку решения, а затем откройте окно **консоли диспетчера пакетов** и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b1f60-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="b1f60-185">`add-migration`Команда сообщает платформе миграции, что необходимо проверить текущую модель фильма с текущей схемой базы данных фильмов, и создать необходимый код для переноса базы данных в новую модель.</span><span class="sxs-lookup"><span data-stu-id="b1f60-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="b1f60-186">*Оценка* имени является произвольной и используется для имени файла миграции.</span><span class="sxs-lookup"><span data-stu-id="b1f60-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="b1f60-187">Полезно использовать понятное имя для шага миграции.</span><span class="sxs-lookup"><span data-stu-id="b1f60-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="b1f60-188">По завершении этой команды Visual Studio открывает файл класса, который определяет новый `DbMigration` производный класс, и в `Up` методе можно увидеть код, создающий новый столбец.</span><span class="sxs-lookup"><span data-stu-id="b1f60-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="b1f60-189">Выполните сборку решения, а затем введите `update-database` команду в окне **консоли диспетчера пакетов** .</span><span class="sxs-lookup"><span data-stu-id="b1f60-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="b1f60-190">На следующем рисунке показаны выходные данные в окне **консоли диспетчера пакетов** (Дата предустановленной *оценки* метки даты будет отличаться).</span><span class="sxs-lookup"><span data-stu-id="b1f60-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="b1f60-191">Повторно запустите приложение и перейдите по URL-адресу/movies.</span><span class="sxs-lookup"><span data-stu-id="b1f60-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="b1f60-192">Можно увидеть новое поле рейтинг.</span><span class="sxs-lookup"><span data-stu-id="b1f60-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="b1f60-193">Щелкните ссылку **создать** , чтобы добавить новый фильм.</span><span class="sxs-lookup"><span data-stu-id="b1f60-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="b1f60-194">Обратите внимание, что можно добавить оценку.</span><span class="sxs-lookup"><span data-stu-id="b1f60-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="b1f60-196">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b1f60-196">Click **Create**.</span></span> <span data-ttu-id="b1f60-197">Теперь новый фильм, включая рейтинг, отображается в списке фильмов:</span><span class="sxs-lookup"><span data-stu-id="b1f60-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="b1f60-199">Теперь, когда проект использует миграции, не нужно удалять базу данных при добавлении нового поля или при других обновлениях схемы.</span><span class="sxs-lookup"><span data-stu-id="b1f60-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="b1f60-200">В следующем разделе будут внесены изменения в схему и использованы миграции для обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="b1f60-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="b1f60-201">Также следует добавить `Rating` поле в шаблоны представлений Правка, сведения и удалить.</span><span class="sxs-lookup"><span data-stu-id="b1f60-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="b1f60-202">Вы можете снова ввести команду "обновить базу данных" в окне **консоли диспетчера пакетов** , и код миграции не будет выполняться, так как схема соответствует модели.</span><span class="sxs-lookup"><span data-stu-id="b1f60-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="b1f60-203">Однако при выполнении команды "обновить базу данных" `Seed` метод снова будет запущен, и если вы изменили какие-либо начальные данные, эти изменения будут потеряны, так как `Seed` метод операции Upsert данные.</span><span class="sxs-lookup"><span data-stu-id="b1f60-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="b1f60-204">Дополнительные сведения о `Seed` методе см. в Dykstra)ном руководстве по [ASP.NET MVC и Entity Framework](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="b1f60-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="b1f60-205">В этом разделе вы узнали, как можно изменить объекты модели и синхронизировать базу данных с изменениями.</span><span class="sxs-lookup"><span data-stu-id="b1f60-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="b1f60-206">Вы также узнали, как заполнить созданную базу данных образцами данных, чтобы вы могли испытать сценарии.</span><span class="sxs-lookup"><span data-stu-id="b1f60-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="b1f60-207">Это было просто краткое введение в Code First. Дополнительные сведения о теме см. в разделе [Создание модели данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) .</span><span class="sxs-lookup"><span data-stu-id="b1f60-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="b1f60-208">Теперь рассмотрим, как можно добавить расширенную логику проверки к классам модели и обеспечить применение некоторых бизнес-правил.</span><span class="sxs-lookup"><span data-stu-id="b1f60-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b1f60-209">[Назад](adding-search.md)
> [Вперед](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="b1f60-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
