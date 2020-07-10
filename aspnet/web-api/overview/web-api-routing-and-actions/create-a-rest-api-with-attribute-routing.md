---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Создание REST API с маршрутизацией атрибутов в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188846"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>Создание REST API с маршрутизацией атрибутов в веб-API ASP.NET 2

по [Майк Уоссон](https://github.com/MikeWasson)

Веб-API 2 поддерживает новый тип маршрутизации, называемый *маршрутизацией атрибутов*. Общие сведения о маршрутизации атрибутов см. в разделе [Маршрутизация атрибутов в веб-API 2](attribute-routing-in-web-api-2.md). В этом учебнике для создания REST API коллекции книг будет использоваться маршрутизация атрибутов. API будет поддерживать следующие действия:

| Действие | Пример URI |
| --- | --- |
| Получение списка всех книг. | /апи/букс |
| Получение книги по ИДЕНТИФИКАТОРу. | /api/books/1 |
| Получение сведений о книге. | /api/books/1/details |
| Получите список книг по жанрам. | /апи/букс/фантаси |
| Получение списка книг по дате публикации. | /API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (альтернативная форма) |
| Получение списка книг по определенному автору. | /api/authors/1/books |

Все методы доступны только для чтения (HTTP-запросы GET).

Для уровня данных мы будем использовать Entity Framework. Записи книги будут иметь следующие поля:

- ID
- Название
- Genre
- дата публикации.
- Цена
- Описание
- Аусорид (внешний ключ к таблице authors)

Однако для большинства запросов API вернет подмножество этих данных (заголовок, автор и жанр). Для получения полной записи клиент запрашивает `/api/books/{id}/details` .

## <a name="prerequisites"></a>Предварительные требования

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional или Enterprise Edition.

## <a name="create-the-visual-studio-project"></a>Создание проекта Visual Studio

Сначала запустите Visual Studio. В меню **Файл** выберите пункт **Создать**, а затем — **Проект**.

Разверните категорию **установленные**  >  **Visual C#** . В разделе **Visual C#** выберите **веб**. В списке шаблонов проектов выберите **ASP.NET веб-приложение (.NET Framework)**. Назовите проект &quot; буксапи &quot; .

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

В диалоговом окне **Создание веб-приложения ASP.NET** выберите **пустой** шаблон. В разделе "Добавление папок и основных ссылок для" установите флажок **веб-API** . Нажмите кнопку **OK**.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

Будет создан каркас проекта, настроенного для работы веб-API.

### <a name="domain-models"></a>Модели предметной области

Затем добавьте классы для моделей предметной области. В обозревателе решений щелкните правой кнопкой мыши папку Models. Нажмите кнопку **Добавить**, а затем выберите **класс**. Назовите класс `Author`.

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Замените код в Author.cs следующим кодом:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

Теперь добавьте еще один класс с именем `Book` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Добавление контроллера веб-API

На этом шаге мы добавим контроллер веб-API, который использует Entity Framework в качестве уровня данных.

Для сборки проекта нажмите CTRL+SHIFT+B. Entity Framework использует отражение для обнаружения свойств моделей, поэтому для создания схемы базы данных требуется скомпилированная сборка.

В обозревателе решений щелкните правой кнопкой мыши папку Controllers. Нажмите кнопку **Добавить**, а затем выберите **контроллер**.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

В диалоговом окне **Добавление шаблона** выберите **контроллер веб-API 2 с действиями с помощью Entity Framework**.

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

В диалоговом окне **Добавление контроллера** в поле **имя контроллера**введите &quot; буксконтроллер &quot; . Установите &quot; флажок использовать асинхронные действия контроллера &quot; . В качестве **класса модели**выберите &quot; книга &quot; . (Если класс не отображается `Book` в раскрывающемся списке, убедитесь, что вы создали проект.) Затем нажмите кнопку "+".

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

Нажмите кнопку **Добавить** в диалоговом окне **новый контекст данных** .

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

Нажмите кнопку **Добавить** в диалоговом окне **Добавление контроллера** . Формирование шаблонов добавляет класс с именем `BooksController` , который определяет контроллер API. Он также добавляет класс с именем `BooksAPIContext` в папку Models, который определяет контекст данных для Entity Framework.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>Заполнение базы данных

В меню Сервис выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.

В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

Эта команда создает папку Migrations и добавляет новый файл кода с именем Configuration.cs. Откройте этот файл и добавьте в метод следующий код `Configuration.Seed` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

В окне консоли диспетчера пакетов введите следующие команды.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

Эти команды создают локальную базу данных и вызывают метод SEED для заполнения базы данных.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>Добавление классов DTO

Если запустить приложение сейчас и отправить запрос GET в/API/Books/1, ответ будет выглядеть следующим образом. (Добавлен отступ для удобочитаемости.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

Вместо этого я хочу, чтобы этот запрос возвращал подмножество полей. Кроме того, я хочу, чтобы он возвращал имя автора, а не идентификатор автора. Для этого мы изменим методы контроллера, чтобы возвращали *объект передачи данных* (DTO) вместо модели EF. DTO — это объект, предназначенный только для переноса данных.

В Обозреватель решений щелкните правой кнопкой мыши проект и выберите команду **Добавить**  |  **новую папку**. Назовите папку &quot; DTO &quot; . Добавьте класс с именем `BookDto` в папку DTO со следующим определением:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

Добавьте еще один класс с именем `BookDetailDto`.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

Затем обновите `BooksController` класс, чтобы он возвращал `BookDto` экземпляры. Мы будем использовать метод [запроса. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) для `Book` экземпляров проекта в `BookDto` экземплярах. Ниже приведен обновленный код для класса Controller.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> Я удалил `PutBook` методы, `PostBook` и `DeleteBook` , так как они не нужны для работы с этим руководством.

Теперь, если вы запустите приложение и запросите/API/Books/1, текст ответа должен выглядеть следующим образом:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>Добавление атрибутов маршрута

Далее мы преобразуем контроллер для использования маршрутизации атрибутов. Сначала добавьте атрибут **RoutePrefix** к контроллеру. Этот атрибут определяет начальные сегменты URI для всех методов на этом контроллере.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

Затем добавьте атрибуты **[Route]** к действиям контроллера следующим образом:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

Шаблон маршрута для каждого метода контроллера — это префикс плюс строка, указанная в атрибуте **Route** . Для `GetBook` метода шаблон маршрута включает параметризованную строку &quot; {ID: int} &quot; , которая соответствует, если сегмент URI содержит целочисленное значение.

| Метод | Шаблон маршрута | Пример URI |
| --- | --- | --- |
| `GetBooks` | "API/книги" | `http://localhost/api/books` |
| `GetBook` | "API/Books/{ID: int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>Получение сведений о книге

Чтобы получить сведения о книге, клиент отправит запрос GET в `/api/books/{id}/details` , где *{ID}* — это идентификатор книги.

Добавьте следующий метод в класс `BooksController`.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

Если вы запрашиваете запрос `/api/books/1/details` , ответ будет выглядеть следующим образом:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>Получение книг по жанру

Чтобы получить список книг по определенному жанру, клиент отправит запрос GET в `/api/books/genre` , где *Жанр* — название жанра. (Например, `/api/books/fantasy`).

Добавьте следующий метод в `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

Здесь мы определяем маршрут, который содержит параметр {жанр} в шаблоне URI. Обратите внимание, что веб-API может отличать эти два URI и пересылать их разным методам:

`/api/books/1`

`/api/books/fantasy`

Это обусловлено тем, что `GetBook` метод включает ограничение, которое сегмент "ID" должен иметь целочисленное значение:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

Если вы запрашиваете/АПИ/букс/Фантаси, ответ будет выглядеть следующим образом:

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>Получить книги по автору

Чтобы получить список книг для конкретного автора, клиент отправит запрос GET в `/api/authors/id/books` , где *ID* — это идентификатор автора.

Добавьте следующий метод в `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

Этот пример интересно, поскольку &quot; книги &quot; обрабатываются дочерним ресурсом &quot; авторов &quot; . Этот шаблон довольно распространен в интерфейсах API RESTFUL.

Тильда (~) в шаблоне маршрута переопределяет префикс маршрута в атрибуте **RoutePrefix** .

## <a name="get-books-by-publication-date"></a>Получение книг по дате публикации

Чтобы получить список книг по дате публикации, клиент отправит запрос GET в `/api/books/date/yyyy-mm-dd` , где *гггг-мм-дд* — это дата.

Вот один из способов:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`Параметр ограничен в соответствии со значением **DateTime** . Это работает, но на самом деле он более разрешительно, чем хотелось бы. Например, эти URI также будут соответствовать маршруту:

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

Для разрешения этих URI ничего не так. Однако можно ограничить маршрут до определенного формата, добавив ограничение регулярного выражения в шаблон маршрута:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

Теперь будут соответствовать только даты в формате &quot; гггг-мм-дд &quot; . Обратите внимание, что мы не будем использовать регулярное выражение для проверки фактической даты. Это обрабатывается, когда веб-API пытается преобразовать сегмент URI в экземпляр **DateTime** . Недопустимая дата, например "2012-47-99", не будет преобразована, и клиент получит ошибку 404.

Можно также поддерживать разделитель косой черты ( `/api/books/date/yyyy/mm/dd` ), добавив еще один атрибут **[Route]** с другим регулярным выражением.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

Здесь есть небольшие, но важные подробности. Второй шаблон маршрута содержит символ-шаблон ( \* ) в начале параметра {pubDate}:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

Это указывает механизму маршрутизации, что {pubDate} должно соответствовать остальной части URI. По умолчанию параметр шаблона соответствует одному сегменту URI. В этом случае нам нужно, чтобы {pubDate} занимал несколько сегментов URI:

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>Код контроллера

Ниже приведен полный код для класса Буксконтроллер.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>Сводка

Маршрутизация атрибутов обеспечивает более широкие возможности управления и гибкость при проектировании URI для API.
