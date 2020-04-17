---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Наследовать с комплексом типа в OData v4 с ASP.NET Web API Документы Майкрософт
author: rick-anderson
description: Согласно спецификации OData v4, сложный тип может наследоваться от другого сложного типа. (Сложный тип представляет собой структурированный тип без ключа.) Веб-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543604"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Наследовать сложный тип в OData v4 с ASP.NET Web API

[корпорацией Майкрософт](https://github.com/microsoft)

> Согласно [спецификации](http://www.odata.org/documentation/odata-version-4-0/)OData v4, сложный тип может наследовать от другого сложного типа. *(Сложный* тип представляет собой структурированный тип без ключа.) Web API OData 5.3 поддерживает наследование сложного типа.
> 
> В этой теме показано, как построить модель данных сущности (EDM) со сложными типами наследования. Для полного исходного [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)кода см.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в учебнике
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>Типовая иерархия

Чтобы проиллюстрировать сложное наследование типа, мы используем следующую иерархию классов.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`является абстрактным сложным типом. `Rectangle`, `Triangle`, `Circle` и являются сложными `RoundRectangle` типами, `Rectangle`полученными из `Shape`, и происходит от . `Window`— тип сущности `Shape` и содержит экземпляр.

Вот классы CLR, которые определяют эти типы.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>Создание модели EDM

Для создания EDM можно использовать **ODataConventionModelBuilder,** который выводит отношения наследования из типов CLR.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Вы также можете построить EDM явно, используя **ODataModelBuilder**. Это требует больше кода, но дает вам больше контроля над EDM.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Эти два примера создают одну и ту же схему EDM.

## <a name="metadata-document"></a>Метаданный документ

Вот документ метаданных OData, показывающий наследование сложного типа.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

Из документа метаданных можно увидеть:

- Сложный `Shape` тип абстрактный.
- В `Rectangle` `Triangle`, `Circle` и сложный тип `Shape`имеют базовый тип .
- Тип `RoundRectangle` имеет базовый `Rectangle`тип.

## <a name="casting-complex-types"></a>Типы кастинг-комплексов

Кастинг на сложных типах теперь поддерживается. Например, следующий запрос отбрасывает `Shape` `Rectangle`a к .

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Вот полезная нагрузка ответа:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
