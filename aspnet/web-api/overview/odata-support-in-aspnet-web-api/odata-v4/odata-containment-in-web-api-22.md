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
ms.openlocfilehash: 50050e40c4c42bf6d769d077c27864ee6417d4db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421404"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a>Включение в OData v4 с помощью веб-API 2,2

по Жинфу Tan

> Обычно доступ к сущности можно получить только в том случае, если она была инкапсулирована в набор сущностей. Но OData v4 предоставляет два дополнительных параметра: Singleton и Contain, которые поддерживаются WebAPI 2,2.

В этом разделе показано, как определить вложение в конечной точке OData в WebApi 2,2. Дополнительные сведения о [включении см. в разделе Включение в OData](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx). Чтобы создать конечную точку OData v4 в веб-API, см. раздел [Создание конечной точки OData v4 с помощью веб-API ASP.NET 2,2](create-an-odata-v4-endpoint.md).

Сначала мы создадим модель домена включения в службе OData, используя эту модель данных:

![Модель данных](odata-containment-in-web-api-22/_static/image1.png)

Учетная запись содержит много Пайментинструментс (PI), но мы не определим набор сущностей для PI. Вместо этого доступ к PI можно получить только через учетную запись.

Решение, используемое в этом разделе, можно загрузить из [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).

## <a name="defining-the-data-model"></a>Определение модели данных

1. Определите типы CLR.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    Атрибут `Contained` используется для свойств навигации вложения.
2. Создание модели EDM на основе типов CLR.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder` будет выполнять сборку модели EDM, если атрибут `Contained` добавляется к соответствующему свойству навигации. Если свойство является типом коллекции, будет также создана `GetCount(string NameContains)` функция.

    Созданные метаданные будут выглядеть следующим образом:

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    Атрибут `ContainsTarget` указывает, что свойство навигации является вложением.

## <a name="define-the-containing-entity-set-controller"></a>Определение содержащего контроллера набора сущностей

Содержащиеся сущности не имеют собственного контроллера; действие определяется в содержащем его контроллере набора сущностей. В этом примере есть Аккаунтсконтроллер, но нет Пайментинструментсконтроллер.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

Если путь OData имеет 4 или более сегментов, работает только маршрутизация атрибутов, например `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` на контроллере выше. В противном случае работают и атрибут, и Обычная маршрутизация: например, `GetPayInPIs(int key)` соответствует `GET ~/Accounts(1)/PayinPIs`.

*Благодарим вас за первоначальное содержимое этой статьи, Leo Hu.*
