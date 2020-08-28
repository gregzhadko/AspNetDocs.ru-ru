---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: Изучение методов Details и DELETE | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 9c4e66454d6995bd750b62ef8b461bcfbdfb4b4f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045095"
---
# <a name="examining-the-details-and-delete-methods"></a>Изучение методов Details и Delete

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

В этой части руководства вы изучите автоматически созданные `Details` `Delete` методы и.

## <a name="examining-the-details-and-delete-methods"></a>Изучение методов Details и Delete

Откройте `Movie` контроллер и изучите `Details` метод.

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

Подсистема формирования шаблонов MVC, создавшая этот метод действия, добавляет комментарий, показывающий HTTP-запрос, который вызывает метод. В этом случае это `GET` запрос с тремя сегментами URL-адреса, `Movies` контроллером, `Details` методом и `ID` значением.

Code First упрощает поиск данных с помощью `Find` метода. Важная функция безопасности, встроенная в метод, заключается в том, что код проверяет, `Find` был ли метод нашел фильм, прежде чем код пытается выполнить какие-либо действия с ним. Например, злоумышленник может вызвать ошибки на сайте, изменив URL-адрес, созданный ссылками, `http://localhost:xxxx/Movies/Details/1` на нечто вроде `http://localhost:xxxx/Movies/Details/12345` (или другое значение, которое не представляет реальный фильм). Если вы не проверили наличие фильма со значением NULL, то в случае ненулевого фильма возникнет ошибка базы данных.

Просмотрите методы `Delete` и `DeleteConfirmed`.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

Обратите внимание, что `Delete` метод HTTP GET не удаляет указанный фильм, он возвращает представление фильма, в котором можно отправить ( `HttpPost` ) удаление. Выполнение операции удаления в ответ на запрос GET (или выполнение операции редактирования, создания или любой другой операции, изменяющей данные) открывает брешь в системе безопасности. Дополнительные сведения об этом см. в разделе блога Вальтер для Стивен [ASP.NET #46 — не используйте ссылки DELETE, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

Метод `HttpPost`, который удаляет данные, называется `DeleteConfirmed`, поэтому метод HTTP POST обладает уникальной сигнатурой или именем. Ниже приведены сигнатуры двух методов:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

Требуется, чтобы в среде CLR перегруженные методы имели уникальную сигнатуру параметров (то же имя метода, но другой список параметров). Однако здесь необходимы два метода удаления — один для GET и один для командлета POST, который имеет одинаковую сигнатуру параметра. (Они оба должны принимать целочисленное значение в качестве параметра.)

Чтобы отсортировать это, можно выполнить несколько действий. Одним из них является присвоение методам различных имен. Именно это было представлено в предыдущем примере механизма формирования шаблонов. Но в этом случае возникает небольшая проблема: ASP.NET сопоставляет сегменты URL-адреса с методами действий по имени, а при переименовании метода, как правило, маршрутизация не сможет найти этот метод. Решение показано в примере, а именно: в метод `DeleteConfirmed` следует добавить атрибут `ActionName("Delete")`. Это эффективно выполняет сопоставление для системы маршрутизации, чтобы URL-адрес, включающий */делете/* для запроса POST, нашел `DeleteConfirmed` метод.

Другой распространенный способ избежать проблем с методами, имеющими идентичные имена и сигнатуры, — искусственно изменить сигнатуру метода POST, включив в него неиспользуемый параметр. Например, некоторые разработчики добавляют тип параметра `FormCollection` , который передается методу POST, а затем просто не использует параметр:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>Сводка

Теперь у вас есть полное приложение MVC ASP.NET, которое хранит данные в локальной базе данных. Вы можете создавать, читать, обновлять, удалять и искать фильмы.

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>Next Steps

После создания и тестирования веб-приложения необходимо сделать его доступным для других пользователей через Интернет. Для этого необходимо развернуть его для поставщика услуг размещения веб-сайтов. Корпорация Майкрософт предлагает бесплатное веб-размещение для 10 веб-сайтов в [бесплатной пробной учетной записи Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Я предлагаю вам далее перейти к [развертыванию безопасного приложения ASP.NET MVC с членством, OAuth и базой данных SQL в Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Отличным руководством является промежуточный уровень Dykstra), [создающий модель данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). [StackOverflow](http://stackoverflow.com/help) и [форумы ASP.NET MVC](https://forums.asp.net/1146.aspx) — это отличное место для задаваемых вопросов. [Подпишитесь](https://twitter.com/RickAndMSFT) на Twitter, чтобы получать обновления в моих последних учебных курсах.

Обратная связь — Добро пожаловать.

— [Рик Андерсон (](https://blogs.msdn.com/rickAndy) Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
— [Скотт Hanselman](http://www.hanselman.com/blog/) Twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [Назад](adding-validation.md)
