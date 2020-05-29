---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Включение в OData v4 с помощью веб-API 2,2 | Документация Майкрософт
author: rick-anderson
description: 'Обычно доступ к сущности можно получить только в том случае, если она была инкапсулирована в набор сущностей. Но OData v4 предоставляет два дополнительных параметра: Singleton и Con...'
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3be81eac9de4686a0d187396e951b121ea65bac4
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173008"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="daa59-104">Включение в OData v4 с помощью веб-API 2,2</span><span class="sxs-lookup"><span data-stu-id="daa59-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="daa59-105">по Жинфу Tan</span><span class="sxs-lookup"><span data-stu-id="daa59-105">by Jinfu Tan</span></span>

> <span data-ttu-id="daa59-106">Обычно доступ к сущности можно получить только в том случае, если она была инкапсулирована в набор сущностей.</span><span class="sxs-lookup"><span data-stu-id="daa59-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="daa59-107">Но OData v4 предоставляет два дополнительных параметра: Singleton и Contain, которые поддерживаются WebAPI 2,2.</span><span class="sxs-lookup"><span data-stu-id="daa59-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="daa59-108">В этом разделе показано, как определить вложение в конечной точке OData в WebApi 2,2.</span><span class="sxs-lookup"><span data-stu-id="daa59-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="daa59-109">Дополнительные сведения о [включении см. в разделе Включение в OData](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/).</span><span class="sxs-lookup"><span data-stu-id="daa59-109">For more information about containment, see [Containment is coming with OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/).</span></span> <span data-ttu-id="daa59-110">Чтобы создать конечную точку OData v4 в веб-API, см. раздел [Создание конечной точки OData v4 с помощью веб-API ASP.NET 2,2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="daa59-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="daa59-111">Сначала мы создадим модель домена включения в службе OData, используя эту модель данных:</span><span class="sxs-lookup"><span data-stu-id="daa59-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![Модель данных](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="daa59-113">Учетная запись содержит много Пайментинструментс (PI), но мы не определим набор сущностей для PI.</span><span class="sxs-lookup"><span data-stu-id="daa59-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="daa59-114">Вместо этого доступ к PI можно получить только через учетную запись.</span><span class="sxs-lookup"><span data-stu-id="daa59-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="daa59-115">Решение, используемое в этом разделе, можно загрузить из [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span><span class="sxs-lookup"><span data-stu-id="daa59-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="daa59-116">Определение модели данных</span><span class="sxs-lookup"><span data-stu-id="daa59-116">Defining the data model</span></span>

1. <span data-ttu-id="daa59-117">Определите типы CLR.</span><span class="sxs-lookup"><span data-stu-id="daa59-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="daa59-118">`Contained`Атрибут используется для свойств навигации вложения.</span><span class="sxs-lookup"><span data-stu-id="daa59-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="daa59-119">Создание модели EDM на основе типов CLR.</span><span class="sxs-lookup"><span data-stu-id="daa59-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="daa59-120">Компонент `ODataConventionModelBuilder` будет выполнять сборку модели EDM, если `Contained` атрибут добавляется к соответствующему свойству навигации.</span><span class="sxs-lookup"><span data-stu-id="daa59-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="daa59-121">Если свойство является типом коллекции, `GetCount(string NameContains)` будет также создана функция.</span><span class="sxs-lookup"><span data-stu-id="daa59-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="daa59-122">Созданные метаданные будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="daa59-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="daa59-123">`ContainsTarget`Атрибут указывает, что свойство навигации является вложением.</span><span class="sxs-lookup"><span data-stu-id="daa59-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="daa59-124">Определение содержащего контроллера набора сущностей</span><span class="sxs-lookup"><span data-stu-id="daa59-124">Define the containing entity set controller</span></span>

<span data-ttu-id="daa59-125">Содержащиеся сущности не имеют собственного контроллера; действие определяется в содержащем его контроллере набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="daa59-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="daa59-126">В этом примере есть Аккаунтсконтроллер, но нет Пайментинструментсконтроллер.</span><span class="sxs-lookup"><span data-stu-id="daa59-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="daa59-127">Если путь OData имеет 4 или более сегментов, работает только маршрутизация атрибутов, например `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` в контроллере выше.</span><span class="sxs-lookup"><span data-stu-id="daa59-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="daa59-128">В противном случае работает и атрибут, и Обычная маршрутизация: например, `GetPayInPIs(int key)` соответствует `GET ~/Accounts(1)/PayinPIs` .</span><span class="sxs-lookup"><span data-stu-id="daa59-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="daa59-129">*Благодарим вас за первоначальное содержимое этой статьи, Leo Hu.*</span><span class="sxs-lookup"><span data-stu-id="daa59-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
