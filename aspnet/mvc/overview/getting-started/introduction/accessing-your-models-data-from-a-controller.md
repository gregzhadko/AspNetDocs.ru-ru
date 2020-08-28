---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045173"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Доступ к данным модели из контроллера

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

В этом разделе вы создадите новый `MoviesController` класс и запишете код, который получает данные фильмов и отображает его в браузере с помощью шаблона представления.

**Создайте приложение,** прежде чем переходить к следующему шагу. Если вы не создаете приложение, вы получите сообщение об ошибке при добавлении контроллера.

В обозреватель решений щелкните правой кнопкой мыши папку *Controllers* и выберите команду **Добавить**, а затем — **контроллер**.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

В диалоговом окне **Добавление шаблона** выберите **контроллер MVC 5 с представлениями с помощью Entity Framework**и нажмите кнопку **добавить**.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Выберите **фильм (MvcMovie. Models)** для класса Model.
- Выберите **мовиедбконтекст (MvcMovie. Models)** для класса контекста данных.
- В качестве имени контроллера введите **MoviesController**.

  На рисунке ниже показано диалоговое окно завершено.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

Нажмите кнопку **Добавить**. (Если появляется сообщение об ошибке, то, возможно, приложение не было собрано до начала добавления контроллера.) Visual Studio создает следующие файлы и папки:

- Файл *MoviesController.CS* в папке *Controllers* .
- Папка *виевс\мовиес* .
- В новой папке *Виевс\мовиес* *создаются. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml*и *index. cshtml* .

Visual Studio автоматически создавала методы и представления действия [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (создание, чтение, обновление и удаление) для вас (автоматическое создание методов и ПРЕДСТАВЛЕНИЙ действий CRUD называется формированием шаблонов). Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.

Запустите приложение и щелкните ссылку на **ролик MVC** (или перейдите к `Movies` контроллеру, добавив */Movies* к URL-адресу в адресной строке браузера). Так как приложение полагается на маршрутизацию по умолчанию (определенную в файле * \_ старт\раутеконфиг.КС приложения* ), запрос обозревателя `http://localhost:xxxxx/Movies` направляется к `Index` методу действия по умолчанию `Movies` контроллера. Иными словами, запрос браузера фактически аналогичен `http://localhost:xxxxx/Movies` запросу браузера `http://localhost:xxxxx/Movies/Index` . Результатом является пустой список фильмов, так как вы еще не добавили их.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Создание фильма

Щелкните ссылку **Create New** (Создать). Введите некоторые сведения о фильме и нажмите кнопку **создать** .

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Возможно, вы не сможете вводить десятичные или запятые в поле Price. Для поддержки проверки jQuery для национальных стандартов, отличных от английского, которые используют запятую ( &quot; , &quot; ) для десятичной запятой и форматы даты, отличные от US-English, необходимо включить *globalize.js* и определенные *языки и региональные параметры и globalize.cultures.js* файла (из [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) и JavaScript для использования `Globalize.parseFloat` . Я покажу, как это сделать в следующем руководстве. А пока вводите целые числа, такие как 10.

Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных. Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Создайте еще несколько записей фильмов. Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.

## <a name="examining-the-generated-code"></a>Проверка созданного кода

Откройте файл *контроллерс\мовиесконтроллер.КС* и изучите созданный `Index` метод. Ниже показана часть контроллера фильмов с `Index` методом.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Запрос к `Movies` контроллеру возвращает все записи в `Movies` таблице, а затем передает результаты в `Index` представление. Следующая строка из `MoviesController` класса создает экземпляр контекста базы данных Movie, как описано выше. Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Строго типизированные модели и @model ключевое слово

Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью `ViewBag` объекта. `ViewBag`— Это динамический объект, предоставляющий удобный способ для передачи сведений в представление.

MVC также предоставляет возможность передачи *строго* типизированных объектов в шаблон представления. Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) в редакторе Visual Studio. Механизм формирования шаблонов в Visual Studio использовал такой подход (то есть передает *строго* типизированную модель) с `MoviesController` классом и шаблонами представления при создании методов и представлений.

В файле *контроллерс\мовиесконтроллер.КС* проверьте созданный `Details` метод. `Details`Метод показан ниже.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`Параметр обычно передается как данные маршрута. Например, для `http://localhost:1234/movies/details/1` контроллера будет задан контроллер ролика, действие — `details` и значение `id` 1. Идентификатор можно также передать в строку запроса следующим образом:

`http://localhost:1234/movies/details?id=1`

Если `Movie` найден, экземпляр `Movie` модели передается в `Details` представление:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

Изучите содержимое файла *виевс\мовиес\детаилс.кштмл* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

Включив `@model` инструкцию в начало файла шаблона представления, можно указать тип объекта, который предполагается просмотреть. При создании контроллера movie Visual Studio автоматически включает следующий оператор `@model` в начало файла *Details.cshtml*:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Эта директива `@model` обеспечивает доступ к фильму, который контроллер передал в представление с использованием строго типизированного объекта `Model`. Например, в шаблоне *Details. cshtml* код передает каждое поле Movie в `DisplayNameFor` вспомогательные методы HTML и [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) со строго типизированным `Model` объектом. `Create`Методы и `Edit` шаблонов представлений также передают объект модели фильма.

Изучите шаблон представления *index. cshtml* и `Index` метод в файле *MoviesController.CS* . Обратите внимание, как код создает [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) объект при вызове `View` вспомогательного метода в `Index` методе действия. Затем код передает этот `Movies` список из `Index` метода действия в представление:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

При создании контроллера фильма Visual Studio автоматически включил в `@model` начало файла *index. cshtml* следующую инструкцию:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Эта `@model` директива позволяет получить доступ к списку фильмов, переданных контроллером в представление с помощью `Model` строго типизированного объекта. Например, в шаблоне *index. cshtml* код проходит через фильмы, выполняя `foreach` оператор над строго типизированным `Model` объектом:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

Так как `Model` объект является строго типизированным (как `IEnumerable<Movie>` объект), каждый `item` объект в цикле имеет тип `Movie` . Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.

![моделинтеллисенсе](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>Работа с SQL Server LocalDB

Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на `Movies` базу данных, которая еще не существовала, поэтому Code First автоматически создала базу данных. Чтобы убедиться, что он создан, найдите папку * \_ данных приложения* . Если файл *movies. mdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " * \_ Данные приложения* ".

![](accessing-your-models-data-from-a-controller/_static/image9.png)

Дважды щелкните *movies. mdf* , чтобы открыть **Обозреватель сервера**, а затем разверните папку **таблицы** , чтобы просмотреть таблицу фильмов. Обратите внимание на значок ключа рядом с ИДЕНТИФИКАТОРом. По умолчанию EF сделает свойство с именем ID первичным ключом. Дополнительные сведения о EF и MVC см. в разделе о отличном руководстве Tom Dykstra) по [MVC и EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

Щелкните таблицу правой кнопкой мыши `Movies` и выберите команду **Показать данные таблицы** , чтобы просмотреть созданные данные.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

Щелкните правой кнопкой мыши `Movies` таблицу и выберите пункт **Открыть определение таблицы** , чтобы просмотреть структуру таблицы, которая Entity Framework Code First создана.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

Обратите внимание, что схема `Movies` таблицы сопоставляется с `Movie` созданным ранее классом. Entity Framework Code First автоматически создали эту схему на основе вашего `Movie` класса.

По завершении закройте подключение, щелкнув правой кнопкой мыши *мовиедбконтекст* и выбрав **закрыть подключение**. (Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Теперь у вас есть база данных и страницы для отображения, редактирования, обновления и удаления данных. В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим `SearchIndex` метод и `SearchIndex` представление, которые позволяют искать фильмы в этой базе данных. Дополнительные сведения об использовании Entity Framework с MVC см. в разделе [Создание модели данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Назад](creating-a-connection-string.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)
