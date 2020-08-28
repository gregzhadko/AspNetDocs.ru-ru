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
# <a name="adding-a-model"></a>Добавление модели

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

В этом разделе вы добавите некоторые классы для управления фильмами в базе данных. Эти классы будут &quot; &quot; частью модели приложения ASP.NET MVC.

Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как [Entity Framework](https://docs.microsoft.com/ef/) , для определения и работы с этими классами модели. Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*. Code First позволяет создавать объекты модели, создавая простые классы. (Они также известны как классы POCO, от &quot; обычных старых объектов CLR. &quot; ) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки. Если сначала необходимо создать базу данных, вы по-прежнему можете следовать этому учебнику, чтобы узнать о разработке приложений MVC и EF. Затем вы можете следовать учебнику по созданию шаблонов для Tom Физмакенс [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) , в котором рассматривается первый подход к базе данных.

## <a name="adding-model-classes"></a>Добавление классов модели

В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.

![](adding-a-model/_static/image1.png)

Введите имя *класса* &quot; Movie &quot; .

Добавьте в класс следующие пять свойств `Movie` :

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Мы будем использовать `Movie` класс для представления фильмов в базе данных. Каждый экземпляр `Movie` объекта будет соответствовать строке в таблице базы данных, а каждое свойство `Movie` класса будет сопоставляться со столбцом в таблице.

Примечание. для использования System. Data. Entity и связанного класса необходимо установить [Entity Framework пакет NuGet](https://www.nuget.org/packages/EntityFramework/). Чтобы получить дополнительные инструкции, перейдите по ссылке.

В том же файле добавьте следующий `MovieDBContext` класс:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext`Класс представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление `Movie` экземпляров классов в базе данных. Объект `MovieDBContext` является производным от `DbContext` базового класса, предоставляемого Entity Framework.

Чтобы иметь возможность ссылаться `DbContext` и `DbSet` , необходимо добавить следующую `using` инструкцию в начало файла:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Это можно сделать, вручную добавив оператор using или наведя указатель мыши на красную волнистую линию, щелкнув `Show potential fixes` и щелкнув `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Примечание. несколько неиспользуемых `using` инструкций были удалены. В Visual Studio неиспользуемые зависимости будут отображаться серым цветом. Чтобы удалить неиспользуемые зависимости, наведите указатель мыши на серые зависимости, щелкните `Show potential fixes` и щелкните **Удалить неиспользуемые функции using.**

![](adding-a-model/_static/image3.png)

Мы наконец добавили модель (M в MVC). В следующем разделе вы будете работать со строкой подключения к базе данных.

> [!div class="step-by-step"]
> [Назад](adding-a-view.md)
> [Вперед](creating-a-connection-string.md)
