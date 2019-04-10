---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: Добавление столбца в модель | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основные сведения по ASP.NET MVC. Создание простого веб-приложения, которое считывает и записывает в базу данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 029234cf9a28a80c487504e4e0980c214e45f53a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381969"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="ab162-104">Добавление столбца в модель</span><span class="sxs-lookup"><span data-stu-id="ab162-104">Adding a Column to the Model</span></span>

<span data-ttu-id="ab162-105">по [(Scott hanselman)](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="ab162-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="ab162-106">Это руководство для начинающих, в котором представлены основные сведения по ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="ab162-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="ab162-107">Вы создадите простое веб-приложение, которое считывает и записывает в базу данных.</span><span class="sxs-lookup"><span data-stu-id="ab162-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="ab162-108">Посетите [центр обучения ASP.NET MVC](../../../index.md) для поиска других ASP.NET MVC, учебники и примеры.</span><span class="sxs-lookup"><span data-stu-id="ab162-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="ab162-109">В этом разделе мы собираемся разберем, как можно вносить изменения в схему нашей базы данных и обрабатывать изменения, в наше приложение.</span><span class="sxs-lookup"><span data-stu-id="ab162-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="ab162-110">Давайте добавим столбец «Оценка» в таблице Movie.</span><span class="sxs-lookup"><span data-stu-id="ab162-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="ab162-111">Вернитесь в интегрированную среду разработки и нажмите кнопку обозревателя базы данных.</span><span class="sxs-lookup"><span data-stu-id="ab162-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="ab162-112">Таблица Movie щелкните правой кнопкой мыши и выберите Открыть определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="ab162-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="ab162-113">Добавьте столбец «Оценка», как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ab162-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="ab162-114">Поскольку мы не имеем любые оценки, столбец можно разрешить значения NULL.</span><span class="sxs-lookup"><span data-stu-id="ab162-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="ab162-115">Нажмите кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="ab162-115">Click Save.</span></span>

[![E<span data-ttu-id="ab162-116">Ограничить редактирование фильмов таблицы]</span><span class="sxs-lookup"><span data-stu-id="ab162-116">diting Movies Table]</span></span>(getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

<span data-ttu-id="ab162-117">Затем вернитесь в обозреватель решений и откройте файл Movies.edmx (который находится в папке \Models).</span><span class="sxs-lookup"><span data-stu-id="ab162-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="ab162-118">Щелкните правой кнопкой мыши в области конструктора (белая область) и выберите Обновить модель из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ab162-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

[![M<span data-ttu-id="ab162-119">ovies - Microsoft Visual Web Developer 2010 Express (11)]</span><span class="sxs-lookup"><span data-stu-id="ab162-119">ovies - Microsoft Visual Web Developer 2010 Express (11)]</span></span>(getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

<span data-ttu-id="ab162-120">Это приведет к запуску «Мастера обновления».</span><span class="sxs-lookup"><span data-stu-id="ab162-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="ab162-121">Перейдите на вкладку "обновления" внутри него и нажмите кнопку Готово.</span><span class="sxs-lookup"><span data-stu-id="ab162-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="ab162-122">Затем наш класс модели Movie обновляется с новым столбцом.</span><span class="sxs-lookup"><span data-stu-id="ab162-122">Our Movie model class will then be updated with the new column.</span></span>

![Мастер обновления (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="ab162-124">После нажатия кнопки Готово, вы увидите, что сущность фильмов в нашей модели добавлен новый столбец оценки.</span><span class="sxs-lookup"><span data-stu-id="ab162-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

[![M<span data-ttu-id="ab162-125">ильм сущности]</span><span class="sxs-lookup"><span data-stu-id="ab162-125">ovie Entity]</span></span>(getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

<span data-ttu-id="ab162-126">Мы добавили столбец в модели базы данных, но представления не знаете о нем.</span><span class="sxs-lookup"><span data-stu-id="ab162-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="ab162-127">Обновление представлений с изменениями модели</span><span class="sxs-lookup"><span data-stu-id="ab162-127">Update Views with Model Changes</span></span>

<span data-ttu-id="ab162-128">Наши шаблоны представлений, чтобы отразить новый столбец оценки можно изменить несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="ab162-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="ab162-129">Так как мы создали эти представления путем создания их с помощью диалогового окна Add View, мы могли бы их удалить и повторно создать их снова.</span><span class="sxs-lookup"><span data-stu-id="ab162-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="ab162-130">Тем не менее обычно людей будут уже были внесены изменения их шаблонов представлений из первоначального формирования шаблонный и хотите добавить или удалить поля вручную, так же, как мы сделали с поле ID для создания.</span><span class="sxs-lookup"><span data-stu-id="ab162-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="ab162-131">Откройте шаблон \Views\Movies\Index.aspx и добавьте &lt;th&gt;Оценка&lt;/th&gt; на заголовок таблицы Movie.</span><span class="sxs-lookup"><span data-stu-id="ab162-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="ab162-132">Я добавил моего после жанра.</span><span class="sxs-lookup"><span data-stu-id="ab162-132">I added mine after Genre.</span></span> <span data-ttu-id="ab162-133">Затем в той же позиции столбца, но ниже, добавьте строку для вывода наш новый элемент управления Rating.</span><span class="sxs-lookup"><span data-stu-id="ab162-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="ab162-134">Наши окончательная версия шаблона Index.aspx будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ab162-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="ab162-135">Давайте затем откройте шаблон \Views\Movies\Create.aspx и добавьте метку и текстовое поле для новое свойство рейтинг:</span><span class="sxs-lookup"><span data-stu-id="ab162-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="ab162-136">Наши окончательная версия шаблона Create.aspx будет выглядеть следующим образом и изменим наш обозреватель заголовок и дополнительный &lt;h2&gt; заголовок на нечто вроде «Создание фильма «пока мы находимся здесь!</span><span class="sxs-lookup"><span data-stu-id="ab162-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="ab162-137">Запустите приложение, и теперь у вас есть новое поле в базе данных, который добавляется на страницу создания.</span><span class="sxs-lookup"><span data-stu-id="ab162-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="ab162-138">Добавьте новый фильм - со оценку - и нажмите кнопку Создать.</span><span class="sxs-lookup"><span data-stu-id="ab162-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

[![C<span data-ttu-id="ab162-139">создать фильм - Windows Internet Explorer]</span><span class="sxs-lookup"><span data-stu-id="ab162-139">reate a Movie - Windows Internet Explorer]</span></span>(getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

<span data-ttu-id="ab162-140">Если нажать кнопку "Создать", после этого вы перейдете на страницу индекса там, где вы новый фильм находится в списке новый столбец оценок в базе данных</span><span class="sxs-lookup"><span data-stu-id="ab162-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

[![M<span data-ttu-id="ab162-141">ильм список — Windows Internet Explorer (12)]</span><span class="sxs-lookup"><span data-stu-id="ab162-141">ovie List - Windows Internet Explorer (12)]</span></span>(getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

<span data-ttu-id="ab162-142">Этот основам вас к работе, делая контроллеров, связав их с представлениями и передачи вокруг жестко заданные данные.</span><span class="sxs-lookup"><span data-stu-id="ab162-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="ab162-143">Затем мы создали и разработанные базы данных и поместить данные в.</span><span class="sxs-lookup"><span data-stu-id="ab162-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="ab162-144">Мы извлекает данные из базы данных и отображения его в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="ab162-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="ab162-145">Затем мы добавили Создание формы, что позволило пользователю добавлять данные в базу данных сами из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ab162-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="ab162-146">Мы добавили проверку, то внесенные проверки использовать JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="ab162-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="ab162-147">Наконец мы изменения базы данных будет содержать новый столбец данных, а затем обновить наши две страницы, для создания и отображения новых данных.</span><span class="sxs-lookup"><span data-stu-id="ab162-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="ab162-148">Я теперь рекомендуем перейти к наш учебный курс промежуточного уровня «[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)", а также многих видео и материалов на [ https://asp.net/mvc ](https://asp.net/mvc) Чтобы получить дополнительные сведения об ASP.NET MVC!</span><span class="sxs-lookup"><span data-stu-id="ab162-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="ab162-149">Желаем удачи!</span><span class="sxs-lookup"><span data-stu-id="ab162-149">Enjoy!</span></span>

- <span data-ttu-id="ab162-150">Скотт Хансельман - [ http://hanselman.com ](http://hanselman.com) и [ @shanselman ](http://twitter.com/shanselman) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="ab162-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ab162-151">Назад</span><span class="sxs-lookup"><span data-stu-id="ab162-151">Previous</span></span>](getting-started-with-mvc-part7.md)
