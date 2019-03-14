---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Знакомство с веб-страниц ASP.NET — удаление базы данных | Документация Майкрософт
author: Rick-Anderson
description: Этом руководстве показано, как удалить запись отдельной базы данных. Предполагается, что завершена рядов через обновление базы данных в ASP.NET Web АП...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: b2ef8fcc8cc534bd31fea83bf0b085b85995f417
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028611"
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="577b7-104">Знакомство с веб-страниц ASP.NET — удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="577b7-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>
====================
<span data-ttu-id="577b7-105">по [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="577b7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="577b7-106">Этом руководстве показано, как удалить запись отдельной базы данных.</span><span class="sxs-lookup"><span data-stu-id="577b7-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="577b7-107">Предполагается, вы выполнили рядов через [обновление базы данных в ASP.NET Web Pages](updating-data.md).</span><span class="sxs-lookup"><span data-stu-id="577b7-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="577b7-108">Вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="577b7-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="577b7-109">Как выбрать отдельную запись из списка записей.</span><span class="sxs-lookup"><span data-stu-id="577b7-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="577b7-110">Как удалить запись из базы данных.</span><span class="sxs-lookup"><span data-stu-id="577b7-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="577b7-111">Как проверить, что определенные нажатие кнопки в форме.</span><span class="sxs-lookup"><span data-stu-id="577b7-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="577b7-112">Функции и технологии:</span><span class="sxs-lookup"><span data-stu-id="577b7-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="577b7-113">`WebGrid` Вспомогательный.</span><span class="sxs-lookup"><span data-stu-id="577b7-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="577b7-114">SQL `Delete` команды.</span><span class="sxs-lookup"><span data-stu-id="577b7-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="577b7-115">`Database.Execute` Метод для выполнения SQL `Delete` команды.</span><span class="sxs-lookup"><span data-stu-id="577b7-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="577b7-116">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="577b7-116">What You'll Build</span></span>

<span data-ttu-id="577b7-117">В предыдущем руководстве вы узнали, как обновить существующую запись базы данных.</span><span class="sxs-lookup"><span data-stu-id="577b7-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="577b7-118">Это руководство представляет собой подобно, за исключением того, что вместо обновления запись, вы удалите его.</span><span class="sxs-lookup"><span data-stu-id="577b7-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="577b7-119">Процессы являются практически так же, за исключением того, что удаление проще использовать, поэтому здесь будет короткий.</span><span class="sxs-lookup"><span data-stu-id="577b7-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="577b7-120">В *фильмы* обновим страницу, `WebGrid` вспомогательный, потому что он отображается как **удалить** ссылку рядом с каждой фильма, сопровождающее **изменить** ссылку, добавленный ранее.</span><span class="sxs-lookup"><span data-stu-id="577b7-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![Страница ссылки для каждого из фильмов](deleting-data/_static/image1.png)

<span data-ttu-id="577b7-122">Как и в редактирования, при нажатии кнопки **удалить** ссылку, откроется на другую страницу, где сведения о фильме уже находится в форме:</span><span class="sxs-lookup"><span data-stu-id="577b7-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![Удалить страницу фильмов с фильмом отображается](deleting-data/_static/image2.png)

<span data-ttu-id="577b7-124">Можно затем нажмите кнопку для удаления записи без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="577b7-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="577b7-125">Добавление ссылки к списку фильмов</span><span class="sxs-lookup"><span data-stu-id="577b7-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="577b7-126">Начнем с добавления **удалить** связать `WebGrid` вспомогательный.</span><span class="sxs-lookup"><span data-stu-id="577b7-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="577b7-127">Эту ссылку, аналогичную **изменить** ссылка добавлена в предыдущем руководстве.</span><span class="sxs-lookup"><span data-stu-id="577b7-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="577b7-128">Откройте *Movies.cshtml* файла.</span><span class="sxs-lookup"><span data-stu-id="577b7-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="577b7-129">Изменение `WebGrid` разметки в основной области страницы, добавив столбец.</span><span class="sxs-lookup"><span data-stu-id="577b7-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="577b7-130">Ниже приведен измененной разметкой.</span><span class="sxs-lookup"><span data-stu-id="577b7-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="577b7-131">Новый столбец является такой:</span><span class="sxs-lookup"><span data-stu-id="577b7-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="577b7-132">Способ настройки сетки **изменить** столбец крайние левые в сетке и **удалить** крайний правый столбец.</span><span class="sxs-lookup"><span data-stu-id="577b7-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="577b7-133">(Отсутствует запятая после `Year` столбец, в случае, если можно не заметить, что.) Нет ничего особенного куда эти столбцы ссылку, и можно так же легко, поместить их рядом друг с другом.</span><span class="sxs-lookup"><span data-stu-id="577b7-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="577b7-134">В этом случае они отдельный, которое затрудняет их смешанным.</span><span class="sxs-lookup"><span data-stu-id="577b7-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![Страница фильмов с помощью ссылки "Изменить" и "сведения о отмечена Показать, что они не являются рядом друг с другом](deleting-data/_static/image3.png)

<span data-ttu-id="577b7-136">Новый столбец отображается ссылка (`<a>` элемент), текст которых говорит: «Удалить».</span><span class="sxs-lookup"><span data-stu-id="577b7-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="577b7-137">Цель ссылки (его `href` атрибут) — это код, который в конечном счете разрешается в нечто вроде этот URL-адрес с `id` значение отличается для каждого фильма:</span><span class="sxs-lookup"><span data-stu-id="577b7-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="577b7-138">Эта ссылка будет вызывать страницу с именем *DeleteMovie* и передать ему идентификатор фильма, вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="577b7-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="577b7-139">Этот учебник не вдаваться в подробности об правила составления эту ссылку, так как это почти идентичен **изменить** ссылку из предыдущего учебного курса ([обновление базы данных в ASP.NET Web Pages](updating-data.md)).</span><span class="sxs-lookup"><span data-stu-id="577b7-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="577b7-140">Создание страницы "Delete"</span><span class="sxs-lookup"><span data-stu-id="577b7-140">Creating the Delete Page</span></span>

<span data-ttu-id="577b7-141">Теперь вы можете создать страницу, которая будет целевой для **удалить** ссылку в сетке.</span><span class="sxs-lookup"><span data-stu-id="577b7-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="577b7-142">**Важные** метод сначала выбрать запись для удаления, и затем с помощью отдельной странице и кнопки, для подтверждения процесс очень важно для безопасности.</span><span class="sxs-lookup"><span data-stu-id="577b7-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="577b7-143">Как уже говорилось в предыдущих учебных курсах, делая *любой* изменений на веб-сайт должен *всегда* сделать с помощью формы &mdash; то есть с помощью операции HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="577b7-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="577b7-144">Если Вы дали изменение сайта только по ссылке (то есть с использованием операции GET), может выполнять простые запросы к веб-узла и удалять данные.</span><span class="sxs-lookup"><span data-stu-id="577b7-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="577b7-145">Даже поисковой системой, индексирования сайт случайно может вызвать удаление данных только по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="577b7-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="577b7-146">Если приложение разрешает пользователям изменить запись, вам нужно пользователь получает записи для редактирования в любом случае.</span><span class="sxs-lookup"><span data-stu-id="577b7-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="577b7-147">Но у вас может возникнуть желание пропустить этот шаг для удаления записи.</span><span class="sxs-lookup"><span data-stu-id="577b7-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="577b7-148">Однако не пропускайте этот шаг.</span><span class="sxs-lookup"><span data-stu-id="577b7-148">Don't skip that step, though.</span></span> <span data-ttu-id="577b7-149">(Это также полезно для пользователей см. запись и убедитесь, что они удалить запись, они предназначены.)</span><span class="sxs-lookup"><span data-stu-id="577b7-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="577b7-150">В последующих учебного набора вы увидите, как добавить функции входа в систему, чтобы пользователю нужно войти, прежде чем удаление записи.</span><span class="sxs-lookup"><span data-stu-id="577b7-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>


<span data-ttu-id="577b7-151">Создание страницы с именем *DeleteMovie.cshtml* и замените в файле, используя следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="577b7-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="577b7-152">Эта разметка аналогичен *EditMovie* страниц, но вместо использования текстовых полей (`<input type="text">`), разметка включает `<span>` элементов.</span><span class="sxs-lookup"><span data-stu-id="577b7-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="577b7-153">Нет ничего здесь, чтобы изменить.</span><span class="sxs-lookup"><span data-stu-id="577b7-153">There's nothing here to edit.</span></span> <span data-ttu-id="577b7-154">Что необходимо сделать всего лишь отображения сведений о фильмах, таким образом, пользователи могут убедиться, что они удаления правой фильма.</span><span class="sxs-lookup"><span data-stu-id="577b7-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="577b7-155">Разметка уже содержит ссылку, которая дает пользователю возможность вернуться на страницу список фильмов.</span><span class="sxs-lookup"><span data-stu-id="577b7-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="577b7-156">Как и в *EditMovie* страницы, идентификатор выбранный фильм сохраняется в скрытом поле.</span><span class="sxs-lookup"><span data-stu-id="577b7-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="577b7-157">(Он передается на страницу в первую очередь как значения строки запроса.) Существует `Html.ValidationSummary` вызов, который будет отображать ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="577b7-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="577b7-158">В этом случае ошибка может быть, что идентификатор фильма, не был передан на страницу или что идентификатор фильма является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="577b7-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="577b7-159">Такая ситуация может возникать, если кто-то работал эту страницу без его предварительного выбора фильм в *фильмы* страницы.</span><span class="sxs-lookup"><span data-stu-id="577b7-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="577b7-160">Подпись кнопки — **удалить фильма**, и его имя атрибута задано значение `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="577b7-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="577b7-161">`name` Атрибут будет использоваться в коде для обозначения кнопки отправки формы.</span><span class="sxs-lookup"><span data-stu-id="577b7-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="577b7-162">Вы напишете код для 1) чтения сведений о фильмах, при первом отображении страницы и (2) фактическое удаление фильм, когда пользователь нажимает кнопку.</span><span class="sxs-lookup"><span data-stu-id="577b7-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="577b7-163">Добавление кода для чтения одного фильма</span><span class="sxs-lookup"><span data-stu-id="577b7-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="577b7-164">В верхней части *DeleteMovie.cshtml* странице, добавьте следующий блок кода:</span><span class="sxs-lookup"><span data-stu-id="577b7-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="577b7-165">Эта разметка совпадает со значением соответствующий код в *EditMovie* страницы.</span><span class="sxs-lookup"><span data-stu-id="577b7-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="577b7-166">Он получает идентификатор фильма из строки запроса и использует идентификатор для чтения записи из базы данных.</span><span class="sxs-lookup"><span data-stu-id="577b7-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="577b7-167">Код включает проверку (`IsInt()` и `row != null`) чтобы убедиться в том, что идентификатор фильма, передаваемого на страницу является допустимым.</span><span class="sxs-lookup"><span data-stu-id="577b7-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="577b7-168">Помните, что этот код следует запускать только в первый раз страница выполняется.</span><span class="sxs-lookup"><span data-stu-id="577b7-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="577b7-169">Вы не хотите повторное чтение запись фильма из базы данных, когда пользователь щелкает **удалить фильма** кнопки.</span><span class="sxs-lookup"><span data-stu-id="577b7-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="577b7-170">Таким образом, код для чтения фильма находится внутри тест, который говорит `if(!IsPost)` &mdash; т.е *Если запрос не операцию post (отправки формы)*.</span><span class="sxs-lookup"><span data-stu-id="577b7-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="577b7-171">Добавление кода, чтобы удалить выбранный фильм</span><span class="sxs-lookup"><span data-stu-id="577b7-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="577b7-172">Чтобы удалить фильм, когда пользователь нажимает кнопку, добавьте следующий код внутри закрывающую скобку `@` блок:</span><span class="sxs-lookup"><span data-stu-id="577b7-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="577b7-173">Этот код аналогичен коду для обновления существующей записи, но проще.</span><span class="sxs-lookup"><span data-stu-id="577b7-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="577b7-174">По сути, код выполняет SQL `Delete` инструкции.</span><span class="sxs-lookup"><span data-stu-id="577b7-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="577b7-175">Как и в *EditMovie* странице код находится в `if(IsPost)` блока.</span><span class="sxs-lookup"><span data-stu-id="577b7-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="577b7-176">На этот раз `if()` немного сложнее ситуация:</span><span class="sxs-lookup"><span data-stu-id="577b7-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="577b7-177">Существует два условия здесь.</span><span class="sxs-lookup"><span data-stu-id="577b7-177">There are two conditions here.</span></span> <span data-ttu-id="577b7-178">Во-первых, что идет отправка страницы, как вы уже видели &mdash; `if(IsPost)`.</span><span class="sxs-lookup"><span data-stu-id="577b7-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="577b7-179">Второе: `!Request["buttonDelete"].IsEmpty()`, это означает, что запрос содержит объект с именем `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="577b7-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="577b7-180">Конечно он является косвенным способом тестирования, какая кнопка отправки формы.</span><span class="sxs-lookup"><span data-stu-id="577b7-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="577b7-181">Если форма содержит несколько кнопок отправки, в запросе отображается только имя кнопки, которая была нажата.</span><span class="sxs-lookup"><span data-stu-id="577b7-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="577b7-182">Таким образом, логически Если имя конкретной кнопки отображается в запросе &mdash; или как указано в коде, если эта кнопка не является пустой &mdash; , при нажатии кнопки отправки формы.</span><span class="sxs-lookup"><span data-stu-id="577b7-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="577b7-183">`&&` Означает, что оператор «и» (логическое и).</span><span class="sxs-lookup"><span data-stu-id="577b7-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="577b7-184">Таким образом весь `if` условие...</span><span class="sxs-lookup"><span data-stu-id="577b7-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="577b7-185">*Этот запрос является публикацией (не первого запроса)*</span><span class="sxs-lookup"><span data-stu-id="577b7-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="577b7-186">AND</span><span class="sxs-lookup"><span data-stu-id="577b7-186">AND</span></span>  
  
<span data-ttu-id="577b7-187">*`buttonDelete`Была* *кнопка кнопки отправки формы.*</span><span class="sxs-lookup"><span data-stu-id="577b7-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="577b7-188">Эта форма (на самом деле, эта страница) содержит только одна кнопка, поэтому проверка значения дополнительных `buttonDelete` технически не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="577b7-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="577b7-189">Тем не менее которые вы собираетесь выполнить операцию, приведет к окончательному удалению данных.</span><span class="sxs-lookup"><span data-stu-id="577b7-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="577b7-190">Таким образом вы хотите быть в том, как можно более, что вы выполняете операцию только в том случае, когда пользователь явно запрашивает его.</span><span class="sxs-lookup"><span data-stu-id="577b7-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="577b7-191">Например предположим, что расширить эту страницу позже и добавить другие кнопки к ним.</span><span class="sxs-lookup"><span data-stu-id="577b7-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="577b7-192">Даже в таком случае код, который удаляет фильм будет выполняться только в том случае, если `buttonDelete` была нажата кнопка.</span><span class="sxs-lookup"><span data-stu-id="577b7-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="577b7-193">Как и в *EditMovie* страницы, получите идентификатор из скрытого поля, а затем выполните команду SQL.</span><span class="sxs-lookup"><span data-stu-id="577b7-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="577b7-194">Синтаксис `Delete` инструкция является:</span><span class="sxs-lookup"><span data-stu-id="577b7-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="577b7-195">Крайне важно включить `WHERE` предложение и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="577b7-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="577b7-196">Если опустить предложение WHERE, *будут удалены все записи в таблице*.</span><span class="sxs-lookup"><span data-stu-id="577b7-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="577b7-197">Как вы уже видели, можно передать значение идентификатора команду SQL с помощью заполнителя.</span><span class="sxs-lookup"><span data-stu-id="577b7-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="577b7-198">Тестирование процесса удаления фильма</span><span class="sxs-lookup"><span data-stu-id="577b7-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="577b7-199">Теперь можно протестировать.</span><span class="sxs-lookup"><span data-stu-id="577b7-199">Now you can test.</span></span> <span data-ttu-id="577b7-200">Запустите *фильмы* и нажмите кнопку **удалить** рядом с фильм.</span><span class="sxs-lookup"><span data-stu-id="577b7-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="577b7-201">Когда *DeleteMovie* появится страница, нажмите кнопку **удалить фильма**.</span><span class="sxs-lookup"><span data-stu-id="577b7-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![Удалить страницу фильма с выделенной кнопкой "Удалить фильма"](deleting-data/_static/image4.png)

<span data-ttu-id="577b7-203">При нажатии кнопки код удаляет фильмов и возвращает список фильмов.</span><span class="sxs-lookup"><span data-stu-id="577b7-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="577b7-204">Там можно найти удаленные фильма и убедитесь, что оно будет удалено.</span><span class="sxs-lookup"><span data-stu-id="577b7-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="577b7-205">В ближайшее время</span><span class="sxs-lookup"><span data-stu-id="577b7-205">Coming Up Next</span></span>

<span data-ttu-id="577b7-206">Следующее руководство показано, как предоставить все страницы узла, общий внешний вид и макет.</span><span class="sxs-lookup"><span data-stu-id="577b7-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="577b7-207">Полный пример для страницы фильма (обновление с помощью ссылок удаления)</span><span class="sxs-lookup"><span data-stu-id="577b7-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="577b7-208">Полный пример для DeleteMovie страницы</span><span class="sxs-lookup"><span data-stu-id="577b7-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="577b7-209">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="577b7-209">Additional Resources</span></span>

- [<span data-ttu-id="577b7-210">Введение в программирование веб-ASP.NET с помощью синтаксиса Razor</span><span class="sxs-lookup"><span data-stu-id="577b7-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="577b7-211">[Инструкция DELETE SQL](http://www.w3schools.com/sql/sql_delete.asp) на сайте W3Schools</span><span class="sxs-lookup"><span data-stu-id="577b7-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="577b7-212">[Назад](updating-data.md)
> [Вперед](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="577b7-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
