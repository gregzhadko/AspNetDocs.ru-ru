---
title: Добавление нового поля на страницу Razor в ASP.NET Core
author: rick-anderson
description: Демонстрирует, как добавить новое поле на страницу Razor с помощью Entity Framework Core
ms.author: riande
ms.custom: mvc
ms.date: 12/5/2018
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: 98de39c63c992dce7d60563df316d848339b811a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050421"
---
# <a name="add-a-new-field-to-a-razor-page-in-aspnet-core"></a>Добавление нового поля на страницу Razor в ASP.NET Core

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

[!INCLUDE[](~/includes/rp/download.md)]

В этом разделе [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First Migrations используется для выполнения следующих задач:

* Добавление нового поля в модель.
* Перенос изменений в схеме нового поля в базу данных.

Если вы используете EF Code First для автоматического создания базы данных, Code First:

* добавляет в нее таблицу, которая позволяет отслеживать синхронизацию схемы базы данных с классами модели, на основе которой она была создана.
* если классы модели не синхронизированы с базой данных, EF выдает исключение.

Автоматическая проверка синхронизации схемы и модели упрощает поиск нарушений согласованности базы данных и кода.

## <a name="adding-a-rating-property-to-the-movie-model"></a>Добавление свойства Rating в модель Movie

Откройте файл *Models/Movie.cs* и добавьте свойство `Rating`:

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

Построение приложения.

Измените файл *Pages/Movies/Index.cshtml* и добавьте в него поле `Rating`:

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/IndexRating.cshtml.?highlight=40-42,61-63)]

Обновите следующие страницы:

* Добавьте поле `Rating` на страницы "Delete" (Удаление) и "Details" (Сведения).
* Обновите файл [Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml), добавив в него поле `Rating`.
* Добавьте поле `Rating` на страницу "Edit" (Редактирование).

Для работы приложения необходимо обновить базу данных, включив в нее новое поле. Если запустить приложение сейчас, возникнет исключение `SqlException`:

`SqlException: Invalid column name 'Rating'.`

Эта ошибка связана с тем, что обновленный класс модели Movie отличается от схемы таблицы Movie в базе данных. (В таблице базы данных отсутствует столбец `Rating`.)

Устранить эту ошибку можно несколькими способами:

1. Можно с помощью Entity Framework автоматически удалить и повторно создать базу данных на основе новой схемы класса модели. Этот подход удобен на ранних стадиях цикла разработки. В этом случае развитие модели и схемы базы данных осуществляется одновременно. Недостатком такого подхода является потеря существующих данных в базе. В рабочей базе данных применять этот подход не следует! При разработке приложения часто выполняется удаление базы данных при изменении схемы, для чего используется инициализатор для автоматического заполнения базы тестовыми данными.

2. Можно явно изменить схему существующей базы данных в соответствии с новыми классами модели. Преимущество такого подхода состоит в том, что сохраняются все данные. Это изменение можно выполнить как вручную, так и с помощью соответствующего скрипта базы данных.

3. Можно обновить схему базы данных с помощью Code First Migrations.

В этом руководстве используется Code First Migrations.

Обновите класс `SeedData` так, чтобы он предоставлял значение нового столбца. Ниже показан пример изменения, которое необходимо выполнить для каждого блока `new Movie`.

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs?name=snippet1&highlight=8)]

См. [готовый файл SeedData.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs).

Постройте решение.

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

<a name="pmc"></a>

### <a name="add-a-migration-for-the-rating-field"></a>Добавление миграции для поля Rating

В меню **Сервис** последовательно выберите пункты **Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.
В PMC введите следующие команды:

```powershell
Add-Migration Rating
Update-Database
```

Команда `Add-Migration` задает следующие инструкции для платформы:

* Сравните модель `Movie` со схемой базы данных `Movie`.
* Создайте код для переноса схемы базы данных в новую модель.

В качестве имени файла переноса используется произвольное имя "Rating". Рекомендуется присваивать этому файлу понятное имя.

Команда `Update-Database` указывает платформе, что нужно применить изменения схемы к базе данных.

<a name="ssox"></a>

Если удалить все записи из базы данных, при инициализации она будет заполнена начальными значениями и в нее будет включено поле `Rating`. Это можно сделать с помощью ссылок удаления в браузере или из [обозревателя объектов SQL Server](xref:tutorials/razor-pages/sql#ssox) (SSOX).

Другой вариант — удалить базу данных и использовать миграции для повторного создания базы данных. Удаление базы данных в SSOX:

* Выберите базу данных в SSOX.
* Щелкните базу данных правой кнопкой мыши и выберите *Удалить*.
* Выберите **Закрыть существующие соединения**.
* Нажмите кнопку **ОК**.
* Обновите базу данных в [PMC](xref:tutorials/razor-pages/new-field#pmc).

  ```powershell
  Update-Database
  ```

<!-- Code -------------------------->
# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[Visual Studio Code/Visual Studio для Mac](#tab/visual-studio-code+visual-studio-mac)

<!-- copy/paste this tab to the next. Not worth an include  -->

Выполните следующие команды интерфейса командной строки .NET Core:

```console
dotnet ef migrations add Rating
dotnet ef database update
```

Команда `ef migrations add` задает следующие инструкции для платформы:

* Сравните модель `Movie` со схемой базы данных `Movie`.
* Создайте код для переноса схемы базы данных в новую модель.

В качестве имени файла переноса используется произвольное имя "Rating". Рекомендуется присваивать этому файлу понятное имя.

Команда `ef database update` указывает платформе, что нужно применить изменения схемы к базе данных.

Если удалить все записи из базы данных, при инициализации она будет заполнена начальными значениями и в нее будет включено поле `Rating`. Это можно сделать с помощью ссылок удаления в браузере или с помощью инструмента SQLite.

Другой вариант — удалить базу данных и использовать миграции для повторного создания базы данных. Чтобы удалить базу данных, удалите файл базы данных (*MvcMovie.db*). Затем выполните команду `ef database update`: 

```console
dotnet ef database update
```

> [!NOTE]
> Многие операции изменения схемы не поддерживаются поставщиком EF Core SQLite. Например, добавление столбца поддерживается, но удаление столбца не поддерживается. При добавлении миграции для удаления столбца команда `ef migrations add` выполняется успешно, а команда `ef database update` — нет. Можно обойти некоторые ограничения вручную, написав код миграции для перестроения таблицы. Перестройка таблицы включает в себя переименование существующей таблицы, создание новой таблицы, копирование данных в новую таблицу и удаление старой таблицы. Дополнительные сведения см. в следующих ресурсах:
> * [Ограничения поставщика базы данных SQLite EF Core](/ef/core/providers/sqlite/limitations)
> * [Настройка кода миграции](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [Присвоение начальных значений данных](/ef/core/modeling/data-seeding)

---  
<!-- End of VS tabs -->

Запустите приложение и проверьте возможность создания, редактирования и отображения фильмов с использованием поля `Rating`. Если база данных не заполнена начальными значениями, задайте точку останова в методе `SeedData.Initialize`.

> [!div class="step-by-step"]
> [Предыдущая статья. Добавление поиска](xref:tutorials/razor-pages/search)
> [Следующая статья. Добавление проверки](xref:tutorials/razor-pages/validation)
