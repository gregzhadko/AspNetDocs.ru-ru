---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Проверка модели в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/20/2012
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 611a6466e160387592df678b3b8556625ff8e234
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033411"
---
<a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="54a27-102">Проверка модели в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="54a27-102">Model Validation in ASP.NET Web API</span></span>
====================
<span data-ttu-id="54a27-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="54a27-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="54a27-104">Когда клиент отправляет данные в веб-API, часто требуется проверять данные перед обработкой.</span><span class="sxs-lookup"><span data-stu-id="54a27-104">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> <span data-ttu-id="54a27-105">В этой статье показано, как для создания заметок к моделям, использование заметок для проверки данных и обработки ошибок проверки в веб-API.</span><span class="sxs-lookup"><span data-stu-id="54a27-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span>

## <a name="data-annotations"></a><span data-ttu-id="54a27-106">Заметки к данным</span><span class="sxs-lookup"><span data-stu-id="54a27-106">Data Annotations</span></span>

<span data-ttu-id="54a27-107">В веб-API ASP.NET, можно использовать атрибуты из [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) пространства имен, чтобы задать правила проверки для свойства в модели.</span><span class="sxs-lookup"><span data-stu-id="54a27-107">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="54a27-108">Рассмотрим следующую модель:</span><span class="sxs-lookup"><span data-stu-id="54a27-108">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="54a27-109">Если вы использовали проверка модели в ASP.NET MVC, это должна быть знакома.</span><span class="sxs-lookup"><span data-stu-id="54a27-109">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="54a27-110">**Требуется** атрибут говорится, что `Name` свойство не должно иметь значение null.</span><span class="sxs-lookup"><span data-stu-id="54a27-110">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="54a27-111">**Диапазон** атрибут говорится, что `Weight` должен находиться в диапазоне от 0 до 999.</span><span class="sxs-lookup"><span data-stu-id="54a27-111">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="54a27-112">Предположим, что клиент отправляет запрос POST с следующее представление JSON:</span><span class="sxs-lookup"><span data-stu-id="54a27-112">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="54a27-113">Вы увидите, что клиент не включил `Name` свойство, которое помечается как требуется.</span><span class="sxs-lookup"><span data-stu-id="54a27-113">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="54a27-114">Когда веб-API преобразует JSON-файла в `Product` экземпляр, он проверяет `Product` от атрибутов проверки.</span><span class="sxs-lookup"><span data-stu-id="54a27-114">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="54a27-115">В действии контроллера можно проверить, допустима ли модель:</span><span class="sxs-lookup"><span data-stu-id="54a27-115">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="54a27-116">Проверка модели не гарантирует, что данные клиента безопасен.</span><span class="sxs-lookup"><span data-stu-id="54a27-116">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="54a27-117">Возможно, потребуется дополнительная проверка другим уровням приложения.</span><span class="sxs-lookup"><span data-stu-id="54a27-117">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="54a27-118">(Например, уровень данных может принудительно применять ограничения внешних ключей.) Руководства [с помощью веб-API с Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) исследует некоторые из этих проблем.</span><span class="sxs-lookup"><span data-stu-id="54a27-118">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="54a27-119">**«Заниженных учета»**: Недостаточное число ресурсов учета происходит, когда клиент оставляет out некоторые свойства.</span><span class="sxs-lookup"><span data-stu-id="54a27-119">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="54a27-120">Например предположим, что клиент отправляет следующее:</span><span class="sxs-lookup"><span data-stu-id="54a27-120">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="54a27-121">Здесь, клиент не указал значения для `Price` или `Weight`.</span><span class="sxs-lookup"><span data-stu-id="54a27-121">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="54a27-122">Модуль форматирования JSON назначается значение по умолчанию, от нуля до отсутствующие свойства.</span><span class="sxs-lookup"><span data-stu-id="54a27-122">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="54a27-123">Состояние модели является допустимым, так как нуль является допустимым значением для этих свойств.</span><span class="sxs-lookup"><span data-stu-id="54a27-123">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="54a27-124">Является ли это проблемой зависит от сценария.</span><span class="sxs-lookup"><span data-stu-id="54a27-124">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="54a27-125">Например в операции обновления, может потребоваться различать «ноль» и «не установлено».</span><span class="sxs-lookup"><span data-stu-id="54a27-125">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="54a27-126">Чтобы заставить клиентов, чтобы задать значение, сделайте свойство, допускающее значение NULL и set **требуется** атрибут:</span><span class="sxs-lookup"><span data-stu-id="54a27-126">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="54a27-127">**«Чрезмерной передачи данных»**: Клиент также может отправлять *дополнительные* данных, чем ожидалось.</span><span class="sxs-lookup"><span data-stu-id="54a27-127">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="54a27-128">Пример:</span><span class="sxs-lookup"><span data-stu-id="54a27-128">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="54a27-129">Здесь JSON включает свойство («цвет»), которое не существует в `Product` модели.</span><span class="sxs-lookup"><span data-stu-id="54a27-129">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="54a27-130">В этом случае модуль форматирования JSON просто игнорирует это значение.</span><span class="sxs-lookup"><span data-stu-id="54a27-130">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="54a27-131">(Модуль форматирования XML делает то же самое.) От чрезмерной передачи данных вызывает проблемы, если модель содержит свойства, которые должны быть доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="54a27-131">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="54a27-132">Пример:</span><span class="sxs-lookup"><span data-stu-id="54a27-132">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="54a27-133">Вы не хотите пользователям обновлять `IsAdmin` свойства и повысить свои права до Администраторы!</span><span class="sxs-lookup"><span data-stu-id="54a27-133">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="54a27-134">Наиболее безопасным при этом важно использовать класс модели, которая точно совпадает с допустимых клиента для отправки:</span><span class="sxs-lookup"><span data-stu-id="54a27-134">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="54a27-135">В блоге Брэда уилсона: "[vs проверка входных данных. Проверка модели в ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)«содержит подробное обсуждение заниженных учета и от чрезмерной передачи данных.</span><span class="sxs-lookup"><span data-stu-id="54a27-135">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="54a27-136">Несмотря на то, что, является запись об ASP.NET MVC 2, вопросы по-прежнему относятся к веб-API.</span><span class="sxs-lookup"><span data-stu-id="54a27-136">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>


## <a name="handling-validation-errors"></a><span data-ttu-id="54a27-137">Обработка ошибок проверки</span><span class="sxs-lookup"><span data-stu-id="54a27-137">Handling Validation Errors</span></span>

<span data-ttu-id="54a27-138">Веб-API не возвращает автоматически ошибку клиенту при сбое проверки.</span><span class="sxs-lookup"><span data-stu-id="54a27-138">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="54a27-139">Возлагается действие контроллера, чтобы проверить состояние модели и реагировать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="54a27-139">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="54a27-140">Также можно создать фильтр действий для проверки состояния модели, перед вызовом действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="54a27-140">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="54a27-141">Ниже показан пример:</span><span class="sxs-lookup"><span data-stu-id="54a27-141">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="54a27-142">Если проверка модели не пройдена, этот фильтр возвращает ответ HTTP, который содержит ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="54a27-142">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="54a27-143">В этом случае действие контроллера не вызывается.</span><span class="sxs-lookup"><span data-stu-id="54a27-143">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="54a27-144">Чтобы применить фильтр ко всем контроллерам веб-API, добавьте экземпляр фильтра, который **HttpConfiguration.Filters** коллекции во время настройки:</span><span class="sxs-lookup"><span data-stu-id="54a27-144">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="54a27-145">Другой вариант — установить фильтр в качестве атрибута на отдельным контроллерам или действиям контроллера:</span><span class="sxs-lookup"><span data-stu-id="54a27-145">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
