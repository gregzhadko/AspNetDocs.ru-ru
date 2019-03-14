---
title: Добавление поиска на страницы Razor ASP.NET Core
author: rick-anderson
description: Инструкции по добавлению поиска на страницы Razor ASP.NET Core
ms.author: riande
ms.date: 12/3/2018
uid: tutorials/razor-pages/search
ms.openlocfilehash: 3900b33f31fef79327d01b0579208355b0bce90c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061521"
---
# <a name="add-search-to-aspnet-core-razor-pages"></a>Добавление поиска на страницы Razor ASP.NET Core

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

[!INCLUDE[](~/includes/rp/download.md)]

В следующих разделах добавляется поиск фильмов по *жанру* или *имени*.

Добавьте следующие выделенные свойства в файл *Pages/Movies/Index.cshtml.cs*:

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

* `SearchString`: содержит текст, который пользователи вводят в поле поиска. `SearchString` декорируется атрибутом [`[BindProperty]`](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute). `[BindProperty]` связывает значения из формы и строки запроса с тем же именем, что и у свойства. `(SupportsGet = true)` является обязательным для привязки в запросах GET.
* `Genres`: содержит список жанров. `Genres` дает пользователю возможность выбрать жанр в списке. Для `SelectList` требуется `using Microsoft.AspNetCore.Mvc.Rendering;`.
* `MovieGenre`: содержит конкретный жанр, выбранный пользователем, например "Western" (Вестерн).
* `Genres` и `MovieGenre` рассматриваются позднее в этом учебнике.

[!INCLUDE[](~/includes/bind-get.md)]

Обновите метод `OnGetAsync` страницы Index, добавив следующий код:

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

В первой строке метода `OnGetAsync` создается запрос [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) для выбора фильмов:

```csharp
// using System.Linq;
var movies = from m in _context.Movie
             select m;
```

Этот запрос *только* определяется в этой точке и **не** выполняется для базы данных.

Если свойство `SearchString` не равно NULL и не пусто, запрос фильмов изменяется для фильтрации по строке поиска:

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

Код `s => s.Title.Contains()` представляет собой [лямбда-выражение](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions). Лямбда-выражения используются в запросах [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) на основе методов в качестве аргументов стандартных методов операторов запроса, таких как метод [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) или `Contains` (используется в предшествующем коде). Запросы LINQ не выполняются, если они определяются или изменяются путем вызова метода (например, `Where`, `Contains` или `OrderBy`). Вместо этого выполнение запроса откладывается. Это означает, что вычисление выражения откладывается до тех пор, пока не будет выполнена итерация его реализованного значения или не будет вызван метод `ToListAsync`. Дополнительные сведения см. в разделе [Выполнение запроса](/dotnet/framework/data/adonet/ef/language-reference/query-execution).

**Примечание.** Метод [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) выполняется в базе данных, а не в коде C#. Регистр символов запроса учитывается в зависимости от параметров базы данных и сортировки. В SQL Server метод `Contains` сопоставляется с [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), в котором регистр символов не учитывается. В SQLite при параметрах сортировки по умолчанию регистр символов учитывается.

Перейдите на страницу Movies и добавьте строку запроса, такую как `?searchString=Ghost`, к URL-адресу (например, `https://localhost:5001/Movies?searchString=Ghost`). Отображаются отфильтрованные фильмы.

![Представление Index](search/_static/ghost.png)

Если на страницу Index добавлен следующий шаблон маршрута, строку поиска можно передать в виде сегмента URL-адреса (например, `https://localhost:5001/Movies/Ghost`).

```cshtml
@page "{searchString?}"
```

Предыдущее ограничение маршрута разрешало поиск названия в виде данных маршрута (сегмент URL-адреса) вместо значения строки запроса.  Символ `?` в `"{searchString?}"` означает, что этот параметр является необязательным.

![Представление Index, в URL-адрес которого добавлено слово ghost, возвращает два фильма: Ghostbusters и Ghostbusters 2](search/_static/g2.png)

Среда выполнения ASP.NET Core использует [привязку модели](xref:mvc/models/model-binding), чтобы присвоить значение свойства `SearchString` по строке запроса (`?searchString=Ghost`) или данным маршрута (`https://localhost:5001/Movies/Ghost`). Привязка модели не учитывает регистр символов.

Тем не менее пользователи вряд ли будут изменять URL-адрес для поиска фильмов. На этом шаге добавляется пользовательский интерфейс для поиска фильмов. Если было добавлено ограничение маршрута `"{searchString?}"`, удалите его.

Откройте файл *Pages/Movies/Index.cshtml* и добавьте разметку `<form>`, которая выделена в следующем коде:

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

Тег HTML `<form>` использует следующие [вспомогательные функции тегов](xref:mvc/views/tag-helpers/intro):

* [вспомогательная функция тега форм](xref:mvc/views/working-with-forms#the-form-tag-helper). При отправке формы строка фильтра отправляется на страницу *Pages/Movies/Index* в строке запроса.
* [Вспомогательная функция тега Input](xref:mvc/views/working-with-forms#the-input-tag-helper)

Сохраните изменения и проверьте работу фильтра.

![Представление Index со словом ghost в текстовом поле фильтра по названию](search/_static/filter.png)

## <a name="search-by-genre"></a>Поиск по жанру

Обновите метод `OnGetAsync`, используя следующий код:

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

Следующий код определяет запрос LINQ, который извлекает все жанры из базы данных.

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

Список жанров `SelectList` создается путем проецирования отдельных жанров.

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]

### <a name="add-search-by-genre-to-the-razor-page"></a>Добавление поиска по жанру на страницу Razor

Обновите файл *Index.cshtml* следующим образом:

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

Проверьте работу приложения, выполнив поиск по жанру, по названию фильма и по обоим этим параметрам.

> [!div class="step-by-step"]
> [Предыдущая статья. Обновление страниц](xref:tutorials/razor-pages/da1)
> [Следующая статья. Добавление нового поля](xref:tutorials/razor-pages/new-field)
