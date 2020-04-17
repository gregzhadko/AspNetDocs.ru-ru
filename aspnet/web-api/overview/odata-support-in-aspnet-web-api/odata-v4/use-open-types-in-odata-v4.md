---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Открытые типы в OData v4 с ASP.NET Web API Документы Майкрософт
author: rick-anderson
description: В OData v4 открытый тип представляет собой структурированный тип, содержащий динамические свойства, в дополнение к любым свойствам, заявленным в определении типа. Открыть...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543734"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Открытые типы в OData v4 с ASP.NET Web API

[корпорацией Майкрософт](https://github.com/microsoft)

> В OData v4 *открытый тип* представляет собой структурированный тип, содержащий динамические свойства, в дополнение к любым свойствам, заявленным в определении типа. Открытые типы позволяют повысить гибкость моделей данных. В этом уроке показано, как использовать открытые типы в ASP.NET Web API OData.
> 
> Этот учебник предполагает, что вы уже знаете, как создать конечную точку OData в ASP.NET Web API. Если нет, начните с чтения [Создайте OData v4 Конечная точка](create-an-odata-v4-endpoint.md) в первую очередь.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в учебнике
> 
> 
> - Web API OData 5.3
> - OData v4

Во-первых, некоторые терминологии OData:

- Тип сущности: структурированный тип с ключом.
- Сложный тип: структурированный тип без ключа.
- Открытый тип: Тип с динамическими свойствами. Могут быть открыты как типы сущностей, так и сложные.

Значение динамического свойства может быть примитивным типом, сложным типом или типом перечисления; или коллекция любого из этих типов. Для получения дополнительной информации [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/)об открытых типах см.

## <a name="install-the-web-odata-libraries"></a>Установка веб-библиотеки OData

Используйте nuGet Package Manager для установки новейших библиотек Web API OData. В окне Консоль диспетчера пакетов

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Определение типов CLR

Начните с определения моделей EDM как типов CLR.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

При создании модели данных сущности (EDM)

- `Category`является типом перечисления.
- `Address`является сложным типом. (Он не имеет ключа, поэтому он не является типом сущности.)
- `Customer`— это тип сущности. (У него есть ключ.)
- `Press`является открытым сложным типом.
- `Book`— это открытый тип сущности.

Для создания открытого типа тип CLR должен `IDictionary<string, object>`иметь свойство типа, которое содержит динамические свойства.

## <a name="build-the-edm-model"></a>Создание модели EDM

Если вы используете **ODataConventionModelBuilder** для `Press` `Book` создания EDM, и автоматически добавляются `IDictionary<string, object>` в качестве открытых типов, в зависимости от наличия свойства.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Вы также можете построить EDM явно, используя **ODataModelBuilder**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Добавление контроллера OData

Затем добавьте контроллер OData. Для этого руководства мы будем использовать упрощенный контроллер, который просто поддерживает запросы GET и POST, а также использует список в памяти для хранения сущностей.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Обратите внимание, `Book` что первая инстанция не имеет динамических свойств. Второй `Book` экземпляр имеет следующие динамические свойства:

- "Опубликовано": Примитивный тип
- "Авторы": Коллекция примитивных типов
- "Другие категории": Коллекция типов перечислений.

Кроме того, свойство `Press` этого `Book` экземпляра имеет следующие динамические свойства:

- "Блог": Примитивный тип
- "Адрес": Комплексный тип

## <a name="query-the-metadata"></a>Запрос метаданных

Чтобы получить документ метаданных OData, отправьте запрос `~/$metadata`GET. Ответный орган должен выглядеть так же, как это:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Из документа метаданных можно увидеть:

- Для `Book` типов `Press` и типов значение `OpenType` атрибута верно. `Customer` Типы `Address` и типы не имеют этого атрибута.
- Тип `Book` сущности имеет три заявленных свойства: ISBN, Название и Пресс. Метаданные OData не включают `Book.Properties` свойство из класса CLR.
- Аналогичным образом, сложный `Press` тип имеет только два заявленных свойства: имя и категория. Метаданные не включают `Press.DynamicProperties` свойство из класса CLR.

## <a name="query-an-entity"></a>Запрос Сущность

Чтобы получить книгу с ISBN равна "978-0-7356-7942-9", отправить запрос GET `~/Books('978-0-7356-7942-9')`. Ответный орган должен выглядеть так же, как и следующие. (Отступ, чтобы сделать его более читаемым.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Обратите внимание, что динамические свойства включены в соответствие с заявленными свойствами.

## <a name="post-an-entity"></a>POST Сущность

Чтобы добавить объект Book, отправьте запрос `~/Books`POST. Клиент может установить динамические свойства в полезной нагрузке запроса.

Вот пример запроса. Обратите внимание на свойства "Цена" и "Опубликовано".

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Если вы установите точку разрыва в методе контроллера, можно `Properties` увидеть, что Web API добавил эти свойства в словарь.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Дополнительные ресурсы

[Пример открытого типа OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
