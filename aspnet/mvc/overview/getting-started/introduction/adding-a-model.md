---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Добавление модели | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045121"
---
# <a name="adding-a-model"></a><span data-ttu-id="d5fb8-102">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="d5fb8-102">Adding a Model</span></span>

<span data-ttu-id="d5fb8-103">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d5fb8-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="d5fb8-104">В этом разделе вы добавите некоторые классы для управления фильмами в базе данных.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="d5fb8-105">Эти классы будут &quot; &quot; частью модели приложения ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="d5fb8-106">Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как [Entity Framework](https://docs.microsoft.com/ef/) , для определения и работы с этими классами модели.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="d5fb8-107">Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="d5fb8-108">Code First позволяет создавать объекты модели, создавая простые классы.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="d5fb8-109">(Они также известны как классы POCO, от &quot; обычных старых объектов CLR. &quot; ) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="d5fb8-110">Если сначала необходимо создать базу данных, вы по-прежнему можете следовать этому учебнику, чтобы узнать о разработке приложений MVC и EF.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="d5fb8-111">Затем вы можете следовать учебнику по созданию шаблонов для Tom Физмакенс [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) , в котором рассматривается первый подход к базе данных.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="d5fb8-112">Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="d5fb8-112">Adding Model Classes</span></span>

<span data-ttu-id="d5fb8-113">В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="d5fb8-114">Введите имя *класса* &quot; Movie &quot; .</span><span class="sxs-lookup"><span data-stu-id="d5fb8-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="d5fb8-115">Добавьте в класс следующие пять свойств `Movie` :</span><span class="sxs-lookup"><span data-stu-id="d5fb8-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="d5fb8-116">Мы будем использовать `Movie` класс для представления фильмов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="d5fb8-117">Каждый экземпляр `Movie` объекта будет соответствовать строке в таблице базы данных, а каждое свойство `Movie` класса будет сопоставляться со столбцом в таблице.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="d5fb8-118">Примечание. для использования System. Data. Entity и связанного класса необходимо установить [Entity Framework пакет NuGet](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="d5fb8-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="d5fb8-119">Чтобы получить дополнительные инструкции, перейдите по ссылке.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="d5fb8-120">В том же файле добавьте следующий `MovieDBContext` класс:</span><span class="sxs-lookup"><span data-stu-id="d5fb8-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="d5fb8-121">`MovieDBContext`Класс представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление `Movie` экземпляров классов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="d5fb8-122">Объект `MovieDBContext` является производным от `DbContext` базового класса, предоставляемого Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="d5fb8-123">Чтобы иметь возможность ссылаться `DbContext` и `DbSet` , необходимо добавить следующую `using` инструкцию в начало файла:</span><span class="sxs-lookup"><span data-stu-id="d5fb8-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="d5fb8-124">Это можно сделать, вручную добавив оператор using или наведя указатель мыши на красную волнистую линию, щелкнув `Show potential fixes` и щелкнув `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="d5fb8-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="d5fb8-125">Примечание. несколько неиспользуемых `using` инструкций были удалены.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="d5fb8-126">В Visual Studio неиспользуемые зависимости будут отображаться серым цветом.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="d5fb8-127">Чтобы удалить неиспользуемые зависимости, наведите указатель мыши на серые зависимости, щелкните `Show potential fixes` и щелкните **Удалить неиспользуемые функции using.**</span><span class="sxs-lookup"><span data-stu-id="d5fb8-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="d5fb8-128">Мы наконец добавили модель (M в MVC).</span><span class="sxs-lookup"><span data-stu-id="d5fb8-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="d5fb8-129">В следующем разделе вы будете работать со строкой подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="d5fb8-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d5fb8-130">[Назад](adding-a-view.md)
> [Вперед](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="d5fb8-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
