---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: Изучение методов Details и Delete | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: c68d7a022f14bdcf2a08696691d2b6ef888a8d54
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064941"
---
<a name="examining-the-details-and-delete-methods"></a>Изучение методов Details и Delete
====================
по [Рик Андерсон]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](sample/code-location.md)]

В этой части руководства вы рассмотрите автоматически созданный `Details` и `Delete` методы.

## <a name="examining-the-details-and-delete-methods"></a>Изучение методов Details и Delete

Откройте `Movie` контроллера и изучите `Details` метод.

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

Подсистема формирования шаблонов MVC, созданная этим методом действия добавляет комментарий, показывающий HTTP-запроса, который вызывает метод. В данном случае это `GET` запроса, состоящая из трех сегментов URL-адрес, `Movies` контроллера, `Details` метод и `ID` значение.

Код сначала облегчает поиск данных с помощью `Find` метод. Это функция важный элемент обеспечения безопасности, встроенной в метод является то, что код проверяет, `Find` метод обнаружил фильм, прежде чем код пытается выполнить любые действия с его. Например, злоумышленник может внести ошибки на сайт путем изменения созданного ссылками из URL-адрес `http://localhost:xxxx/Movies/Details/1` в нечто подобное `http://localhost:xxxx/Movies/Details/12345` (или любое другое значение, которое не представляет фактический фильм). Если вы не проверили наличие фильма со значением null, фильма со значением null приведет к ошибке базы данных.

Просмотрите методы `Delete` и `DeleteConfirmed`.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

Обратите внимание, что HTTP GET `Delete` метод не удаляет указанный фильм, он возвращает представление фильма, где вы сможете отправить (`HttpPost`) удаление. Выполнение операции удаления в ответ на запрос GET (или выполнение операции редактирования, создания или любой другой операции, изменяющей данные) открывает брешь в системе безопасности. Дополнительные сведения об этом см. запись в блоге Стивен Вальтер [46 совет # ASP.NET MVC — не использовать ссылки, удалить, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

Метод `HttpPost`, который удаляет данные, называется `DeleteConfirmed`, поэтому метод HTTP POST обладает уникальной сигнатурой или именем. Ниже приведены сигнатуры двух методов:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

Требуется, чтобы в среде CLR перегруженные методы имели уникальную сигнатуру параметров (то же имя метода, но другой список параметров). Однако здесь необходимы два метода Delete — один для GET--и один для POST, имеют такой же сигнатурой параметров. (Они оба должны принимать целочисленное значение в качестве параметра.)

Чтобы отсортировать этот выходной, можно сделать несколько вещей. Одна — предоставить методы разные имена. Именно это было представлено в предыдущем примере механизма формирования шаблонов. Но в этом случае возникает небольшая проблема: ASP.NET сопоставляет сегменты URL-адреса с методами действий по имени, а при переименовании метода, как правило, маршрутизация не сможет найти этот метод. Решение показано в примере, а именно: в метод `DeleteConfirmed` следует добавить атрибут `ActionName("Delete")`. Это фактически выполняет сопоставление для системы маршрутизации, таким образом, чтобы URL-адрес, который включает в себя */Delete/* для отправки запроса будет найти `DeleteConfirmed` метод.

Другой распространенный способ избежать с помощью методов с одинаковыми именами и сигнатурами является искусственное изменение сигнатуры метода POST для включения неиспользуемый параметр. Например, некоторые разработчики добавить тип параметра `FormCollection` , передаваемый в метод POST и затем просто не использовать параметр:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>Сводка

Теперь у вас есть полное приложение ASP.NET MVC, которое хранит данные в локальную базу данных DB. Можно создать, чтение, обновление, удаление и поиск фильмов.

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>Следующие шаги

После создания и тестирования веб-приложения, пора сделать его доступным для других пользователей через Интернет. Чтобы сделать это, необходимо развернуть его на веб-поставщик услуг размещения. Корпорация Майкрософт предлагает бесплатные услуг хостинга до 10 веб-сайтов в [бесплатную пробную учетную запись Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Я предлагаю вы затем учебник моей [развертывание приложения Secure ASP.NET MVC с членством, OAuth и базой данных SQL в Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Отличная руководство представляет собой том Дайкстра любителей [Создание модели данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). [StackOverflow](http://stackoverflow.com/help) и [форумах ASP.NET MVC](https://forums.asp.net/1146.aspx) являются отличной помещает задавать вопросы. Выполните [мне](https://twitter.com/RickAndMSFT) в twitter, поэтому вы можете получать обновления на моем новейшие учебники.

Вы откликнитесь.

— [Рик Андерсон](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
— [(Scott hanselman)](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [Назад](adding-validation.md)
