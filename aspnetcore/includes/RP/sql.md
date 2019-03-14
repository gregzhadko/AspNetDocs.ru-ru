---
ms.openlocfilehash: d963e3b52db7703e9b2fad1466a23fdeb1b8f848
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035361"
---
# <a name="work-with-sqlite-in-an-aspnet-core-razor-pages-app"></a><span data-ttu-id="885de-101">Работа с SQLite в приложении Razor Pages ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="885de-101">Work with SQLite in an ASP.NET Core Razor Pages app</span></span>

<span data-ttu-id="885de-102">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="885de-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="885de-103">Объект `MovieContext` обрабатывает задачу подключения к базе данных и сопоставления объектов `Movie` с записями базы данных.</span><span class="sxs-lookup"><span data-stu-id="885de-103">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="885de-104">Контекст базы данных регистрируется с помощью контейнера [внедрения зависимостей (DI)](xref:fundamentals/dependency-injection) в методе `ConfigureServices` в файле *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="885de-104">The database context is registered with the [Dependency Injection (DI)](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](code/Startup.cs?name=snippet2&highlight=6-8)]

<span data-ttu-id="885de-105">Дополнительные сведения об использовании `DbContext` с внедрением зависимостей см. в статье об [использовании DbContext с внедрением зависимостей](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="885de-105">For more information on using `DbContext` with DI, see [Using DbContext with DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection).</span></span>

## <a name="sqlite"></a><span data-ttu-id="885de-106">SQLite</span><span class="sxs-lookup"><span data-stu-id="885de-106">SQLite</span></span>

<span data-ttu-id="885de-107">На веб-сайте [SQLite](https://www.sqlite.org/) указывается следующее:</span><span class="sxs-lookup"><span data-stu-id="885de-107">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="885de-108">SQLite — это автономная внедряемая полнофункциональная общедоступная система управления базами данных SQL с высокой степенью надежности.</span><span class="sxs-lookup"><span data-stu-id="885de-108">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="885de-109">На данный момент SQLite является самой популярной СУБД в мире.</span><span class="sxs-lookup"><span data-stu-id="885de-109">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="885de-110">Для просмотра баз данных SQLite, а также управления ими можно использовать множество самых разных сторонних инструментов.</span><span class="sxs-lookup"><span data-stu-id="885de-110">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="885de-111">На следующем рисунке показан [DB Browser для SQLite](http://sqlitebrowser.org/).</span><span class="sxs-lookup"><span data-stu-id="885de-111">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="885de-112">Если вы предпочитаете использовать другое средство для работы с SQLite, напишите нам в комментариях, чем именно оно нравится вам.</span><span class="sxs-lookup"><span data-stu-id="885de-112">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![DB Browser для SQLite с базой данных movie](../../tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="885de-114">Заполнение базы данных</span><span class="sxs-lookup"><span data-stu-id="885de-114">Seed the database</span></span>

<span data-ttu-id="885de-115">Создайте класс `SeedData` в папке *Models*.</span><span class="sxs-lookup"><span data-stu-id="885de-115">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="885de-116">Замените сгенерированный код следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="885de-116">Replace the generated code with the following:</span></span>

[!code-csharp[](code/Models/SeedData.cs)]

<span data-ttu-id="885de-117">Если в базе данных есть фильмы, возвращается инициализатор заполнения.</span><span class="sxs-lookup"><span data-stu-id="885de-117">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="885de-118">Добавление инициализатора заполнения</span><span class="sxs-lookup"><span data-stu-id="885de-118">Add the seed initializer</span></span>

<span data-ttu-id="885de-119">Добавьте инициализатор заполнения в метод `Main` в файле *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="885de-119">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Program.cs)]

### <a name="test-the-app"></a><span data-ttu-id="885de-120">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="885de-120">Test the app</span></span>

<span data-ttu-id="885de-121">Удалите все записи в базе данных для запуска метода заполнения.</span><span class="sxs-lookup"><span data-stu-id="885de-121">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="885de-122">Остановите и запустите приложение, чтобы начать заполнение базы данных.</span><span class="sxs-lookup"><span data-stu-id="885de-122">Stop and start the app to seed the database.</span></span>

<span data-ttu-id="885de-123">В приложении будут отображены данные.</span><span class="sxs-lookup"><span data-stu-id="885de-123">The app shows the seeded data.</span></span>
