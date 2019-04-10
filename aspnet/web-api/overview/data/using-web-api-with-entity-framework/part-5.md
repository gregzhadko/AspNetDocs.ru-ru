---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Создание объектов передачи данных (DTO) | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 1af29955e8040c34840d4c77fc2006f59d2324dd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59395281"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="58b11-102">Создание объектов передачи данных (DTO)</span><span class="sxs-lookup"><span data-stu-id="58b11-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="58b11-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="58b11-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="58b11-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="58b11-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="58b11-105">Справа теперь наши веб-API предоставляет сущности базы данных клиенту.</span><span class="sxs-lookup"><span data-stu-id="58b11-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="58b11-106">Клиент получает данные, прямо таблиц базы данных.</span><span class="sxs-lookup"><span data-stu-id="58b11-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="58b11-107">Тем не менее это не всегда хорошая идея.</span><span class="sxs-lookup"><span data-stu-id="58b11-107">However, that's not always a good idea.</span></span> <span data-ttu-id="58b11-108">Иногда требуется изменить форму данных, отправляемых клиенту.</span><span class="sxs-lookup"><span data-stu-id="58b11-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="58b11-109">Например, можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="58b11-109">For example, you might want to:</span></span>

- <span data-ttu-id="58b11-110">Удалите циклические ссылки, (см. выше).</span><span class="sxs-lookup"><span data-stu-id="58b11-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="58b11-111">Скрыть определенных свойств, которые клиенты не должны просматривать.</span><span class="sxs-lookup"><span data-stu-id="58b11-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="58b11-112">Исключить некоторые свойства, чтобы уменьшить размер полезных данных.</span><span class="sxs-lookup"><span data-stu-id="58b11-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="58b11-113">Обработка графов объектов, содержащих вложенные объекты, чтобы сделать их более удобным для клиентов.</span><span class="sxs-lookup"><span data-stu-id="58b11-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="58b11-114">Избегайте «уязвимости типа overposting».</span><span class="sxs-lookup"><span data-stu-id="58b11-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="58b11-115">(См. в разделе [проверки модели](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) обсуждение от чрезмерной передачи данных.)</span><span class="sxs-lookup"><span data-stu-id="58b11-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="58b11-116">Отделить уровень службы из вашего уровня базы данных.</span><span class="sxs-lookup"><span data-stu-id="58b11-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="58b11-117">Для этого можно определить *объект передачи данных* (DTO).</span><span class="sxs-lookup"><span data-stu-id="58b11-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="58b11-118">DTO — это объект, который определяет, каким образом данные будут отправляться по сети.</span><span class="sxs-lookup"><span data-stu-id="58b11-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="58b11-119">Давайте посмотрим, как это работает с сущностью книги.</span><span class="sxs-lookup"><span data-stu-id="58b11-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="58b11-120">В папке Models добавьте два классы объектов передачи данных:</span><span class="sxs-lookup"><span data-stu-id="58b11-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="58b11-121">`BookDetailDTO` Класс включает все свойства из модели книги, за исключением случаев, `AuthorName` представляет собой строку, которая будет содержать имя автора.</span><span class="sxs-lookup"><span data-stu-id="58b11-121">The `BookDetailDTO` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="58b11-122">`BookDTO` Класс содержит подмножество свойств из `BookDetailDTO`.</span><span class="sxs-lookup"><span data-stu-id="58b11-122">The `BookDTO` class contains a subset of properties from `BookDetailDTO`.</span></span>

<span data-ttu-id="58b11-123">Затем замените два метода GET в `BooksController` класса с версиями, которые возвращают DTO.</span><span class="sxs-lookup"><span data-stu-id="58b11-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="58b11-124">Мы будем использовать LINQ **выберите** инструкции для преобразования из сущностей книг в DTO.</span><span class="sxs-lookup"><span data-stu-id="58b11-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="58b11-125">Ниже приведен код SQL, созданный по новому `GetBooks` метод.</span><span class="sxs-lookup"><span data-stu-id="58b11-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="58b11-126">Вы увидите, что EF преобразует LINQ **выберите** в инструкцию SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="58b11-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="58b11-127">Наконец, измените `PostBook` метод вернет объект DTO.</span><span class="sxs-lookup"><span data-stu-id="58b11-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="58b11-128">В этом руководстве мы преобразовали в DTO вручную в коде.</span><span class="sxs-lookup"><span data-stu-id="58b11-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="58b11-129">Другой вариант — использовать библиотеку как [AutoMapper](http://automapper.org/) , обрабатывает преобразование автоматически.</span><span class="sxs-lookup"><span data-stu-id="58b11-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="58b11-130">[Назад](part-4.md)
> [Вперед](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="58b11-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
