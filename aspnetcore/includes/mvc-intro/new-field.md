---
ms.openlocfilehash: e098ad497b13b4add583de017885cdbed952a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036761"
---
<!-- This include not used by windows version -->
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a>Добавление нового поля в приложение MVC ASP.NET Core

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

В этом руководстве в таблицу `Movies` добавляется новое поле. После изменения схемы (и добавления нового поля) мы удалим старую базу данных и создадим новую. Этот подход применяется на ранней стадии разработки, когда в базе отсутствуют важные рабочие данные.

После того, как приложение развернуто и содержит нужные данные, при изменении схемы нельзя удалять существующую базу данных. Платформа Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) позволяет обновлять схему и переносить базу данных без потери данных. При работе с SQL Server миграция выполняется достаточно часто, но в SQLlite набор операций, связанных со схемой миграции, крайне ограничен. Дополнительные сведения см. в разделе [Ограничения в SQLite](/ef/core/providers/sqlite/limitations).

## <a name="adding-a-rating-property-to-the-movie-model"></a>Добавление свойства Rating в модель Movie

Откройте файл *Models/Movie.cs* и добавьте свойство `Rating`:

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Models/MovieDateRating.cs?highlight=12&name=snippet)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

::: moniker-end

Поскольку в класс `Movie` было добавлено новое поле, необходимо также обновить белый список привязки, включив в него новое свойство. В файле *MoviesController.cs* обновите атрибут `[Bind]` для методов действия `Create` и `Edit`, включив свойство `Rating`:

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

Также необходимо обновить шаблоны представлений, чтобы реализовать отображение, создание и редактирование нового свойства `Rating` в представлении браузера.

Измените файл */Views/Movies/Index.cshtml* и добавьте поле `Rating`:

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexGenreRating.cshtml?highlight=17,39&range=24-64)]

Обновите файл */Views/Movies/Create.cshtml*, указав поле `Rating`.

Для работы приложения необходимо обновить базу данных, включив в нее новое поле. Если запустить приложение сейчас, появится следующее исключение `SqliteException`:

```
SqliteException: SQLite Error 1: 'no such column: m.Rating'.
```

Эта ошибка связана с тем, что обновленный класс модели Movie отличается от схемы таблицы Movie в существующей базе данных. (В таблице базы данных отсутствует столбец `Rating`.)

Устранить эту ошибку можно несколькими способами:

1. Можно удалить базу данных и затем с помощью Entity Framework автоматически повторно создать ее на основе новой схемы класса модели. При таком подходе теряются существующие данные в базе, поэтому он не применяется для рабочей базы данных. При разработке приложения часто используется инициализатор для автоматического заполнения базы тестовыми данными.

2. Можно вручную изменить схему существующей базы данных в соответствии с новыми классами модели. Преимущество такого подхода состоит в том, что сохраняются все данные. Это изменение можно выполнить как вручную, так и с помощью соответствующего скрипта базы данных.

3. Можно обновить схему базы данных с помощью Code First Migrations.

В рамках этого руководства мы удалим и повторно создадим базу данных при изменении схемы. Для удаления базы данных выполните следующую команду из терминала:

`dotnet ef database drop`

Обновите класс `SeedData` так, чтобы он предоставлял значение нового столбца. Ниже показан пример изменения, которое необходимо выполнить для каждого `new Movie`.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

Добавьте поле `Rating` в представления `Edit`, `Details` и `Delete`.

Запустите приложение и проверьте возможность создания, редактирования и отображения фильмов с использованием поля `Rating`. шаблоны.
