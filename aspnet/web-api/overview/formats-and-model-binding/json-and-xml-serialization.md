---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: JSON и XML Сериализация в ASP.NET Web API - ASP.NET 4.x
author: MikeWasson
description: Описывает предки JSON и XML в ASP.NET Web API за ASP.NET 4.x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675835"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>JSON и XML Сериализация в ASP.NET Web API

[Майк Уоссон](https://github.com/MikeWasson)

В этой статье описаны статьи JSON и XML в ASP.NET Web API.

В ASP.NET Web API, *formatter медиа-типа* является объектом, который может:

- Читать объекты CLR из тела сообщений HTTP
- Запись объектов CLR в тело сообщения HTTP

Web API предоставляет предписывание медиа-типа как для JSON, так и для XML. Рамки вставляют эти предзначения в конвейер по умолчанию. Клиенты могут запросить JSON или XML в заголовке запроса HTTP.

## <a name="contents"></a>Содержимое

- [JSON Медиа-Тип Formatter](#json_media_type_formatter)

    - [Только для чтения свойства](#json_readonly)
    - [Даты](#json_dates)
    - [Отступы](#json_indenting)
    - [Верблюд Касинг](#json_camelcasing)
    - [Анонимные и слабо набранные объекты](#json_anon)
- [XML Медиа-Тип Formatter](#xml_media_type_formatter)

    - [Только для чтения свойства](#xml_readonly)
    - [Даты](#xml_dates)
    - [Отступы](#xml_indenting)
    - [Установка серизаторов Per-Type XML](#xml_pertype)
- [Удаление JSON или XML Formatter](#removing_the_json_or_xml_formatter)
- [Обработка ссылки на круговые объекты](#handling_circular_object_references)
- [Тестирование сериализации объектов](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Медиа-Тип Formatter

Форматирование JSON обеспечивается классом **JsonMediaTypeFormatter.** По умолчанию **JsonMediaTypeFormatter** использует [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) библиотеку для выполнения сериализации. Json.NET является сторонним проектом с открытым исходным кодом.

Если вы предпочитаете, вы можете настроить класс **JsonMediaTypeFormatter,** чтобы использовать **DataContractJsonSerializer** вместо Json.NET. Для этого установите свойство **UseDataContractJsonSerializer** на **истину:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>Сериализация JSON

В этом разделе описаны некоторые конкретные поведения formatter JSON, использующие [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) сериализатор по умолчанию. Это не должна быть всеобъемлющая документация Json.NET библиотеки; для получения дополнительной информации см [Json.NET.](http://james.newtonking.com/projects/json/help/)

#### <a name="what-gets-serialized"></a>Что получает сериализации?

По умолчанию все публичные свойства и поля включены в сериализованный JSON. Чтобы опустить свойство или поле, украсьте его атрибутом **JsonIgnore.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

Если вы &quot;предпочитаете&quot; подход, выбираемый, украсьте класс атрибутом **DataContract.** При наличии этого атрибута участники игнорируются, если у них нет **DataMember.** Вы также можете использовать **DataMember** для сериализации частных членов.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Только для чтения свойства

Свойства только для чтения сериализируются по умолчанию.

<a id="json_dates"></a>
### <a name="dates"></a>даты.

По умолчанию Json.NET пишет даты в формате [ISO 8601.](http://www.w3.org/TR/NOTE-datetime) Даты в UTC (Кооркоорорное универсальное время) написаны суффиксом "я". Даты в местное время включают в себя смещение часового пояса. Пример:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

По умолчанию Json.NET сохраняет часовой пояс. Вы можете переопределить это, установив свойство DateTime'oneHandling:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

Если вы предпочитаете использовать формат`"\/Date(ticks)\/"`даты Microsoft [JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) () вместо ISO 8601, установите свойство **DateFormatHandling** на настройках serializer:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Отступы

Чтобы написать отступом JSON, установите настройки **форматирования** на **Formatting.Indented:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Верблюд Касинг

Чтобы написать имена свойств JSON с корпусом верблюда, не изменяя модель данных, установите **CamelCasePropertyNames.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Анонимные и слабо набранные объекты

Метод действия может вернуть анонимный объект и сериализировать его в JSON. Пример:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

Тело сообщения ответа будет содержать следующее JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Если ваш веб-aPI получает от клиентов слабо структурированные объекты JSON, можно разработать тело запроса в **типе Newtonsoft.JObject.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

Тем не менее, как правило, лучше использовать сильно набранные объекты данных. Тогда вам не нужно анализировать данные самостоятельно, и вы получаете преимущества проверки модели.

Серийный xML не поддерживает анонимные типы или экземпляры **JObject.** Если вы используете эти функции для данных JSON, следует удалить из конвейера материал XML, как описано позднее в этой статье.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML Медиа-Тип Formatter

Форматирование XML обеспечивается классом **XmlMediaTypeFormatter.** По умолчанию **XmlMediaTypeFormatter** использует класс **DataContractSerializer** для выполнения сериализации.

Если вы предпочитаете, вы можете настроить **XmlMediaTypeFormatter** использовать **XmlSerializer** вместо **DataContractSerializer**. Чтобы сделать это, установите свойство **UseXmlSerializer** на **истину:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

Класс **XmlSerializer** поддерживает более узкий набор типов, чем **DataContractSerializer,** но дает больше контроля над полученным XML. Рассмотрите возможность использования **XmlSerializer,** если вам необходимо сопоставить существующую схему XML.

### <a name="xml-serialization"></a>Сериализация XML

В этом разделе описаны некоторые конкретные поведения XML formatter, используя по умолчанию **DataContractSerializer.**

По умолчанию DataContractSerializer ведет себя следующим образом:

- Все свойства чтения/записи общего пользования/записи сериализируются. Чтобы опустить свойство или поле, украсьте его атрибутом **IgnoreDataMember.**
- Частные и защищенные члены не сериализуются.
- Свойства только для чтения не сериализируются. (Однако содержимое свойства коллекции только для чтения сериализуется.)
- Имена классов и членов пишутся в XML точно так же, как они отображаются в декларации класса.
- Используется пространство имен XML по умолчанию.

Если вам нужно больше контроля над сериализацией, вы можете украсить класс атрибутом **DataContract.** При этом атрибуте класс сериализируется следующим образом:

- &quot;Выберите&quot; подход: Свойства и поля не сериализируются по умолчанию. Чтобы выставить нанету свойство или поле, украсьте его атрибутом **DataMember.**
- Чтобы сериализовать частного или защищенного участника, украсьте его атрибутом **DataMember.**
- Свойства только для чтения не сериализируются.
- Чтобы изменить отогнание имени класса в XML, установите параметр *имени* в атрибуте **DataContract.**
- Чтобы изменить отогнание имени участника в XML, установите параметр *имени* в атрибуте **DataMember.**
- Чтобы изменить пространство имен XML, установите параметр *Namespace* в классе **DataContract.**

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Только для чтения свойства

Свойства только для чтения не сериализируются. Если свойство только для чтения имеет резервное частное поле, можно отметить частное поле атрибутом **DataMember.** Этот подход требует атрибута **DataContract** в классе.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>даты.

Даты написаны в формате ISO 8601. Например, &quot;2012-05-23T20:21:37.9116538&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Отступы

Чтобы написать отступ XML, установите свойство **Indent** на **истину:**

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>Установка серизаторов Per-Type XML

Можно установить различные серийные XML для различных типов CLR. Например, у вас может быть определенный объект данных, который требует **XmlSerializer** для обратной совместимости. Вы можете использовать **XmlSerializer** для этого объекта и продолжать использовать **DataContractSerializer** для других типов.

Чтобы установить серийный xML для определенного типа, позвоните **SetSerializer.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Вы можете указать **XmlSerializer** или любой объект, который происходит от **XmlObjectSerializer**.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>Удаление JSON или XML Formatter

Вы можете удалить formatter JSON или XML из списка навсегда, если вы не хотите их использовать. Основные причины для этого:

- Ограничить ваши ответы Web API на определенный тип носителя. Например, можно решить поддерживать только ответы JSON и удалить значение XML.
- Заменить по умолчанию formatter на пользовательский formatter. Например, можно заменить formatter JSON на собственную пользовательскую реализацию formatter JSON.

Следующий код показывает, как удалить предтечи по умолчанию. Назовите это методом **запуска приложений,\_** определенным в Global.asax.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Обработка ссылки на круговые объекты

По умолчанию formatters JSON и XML пишут все объекты как значения. Если два свойства относятся к одному и тому же объекту или если один и тот же объект появляется дважды в коллекции, то значение будет сериализировать объект дважды. Это особая проблема, если график объекта содержит циклы, потому что serializer будет бросать исключение, когда он обнаруживает цикл в графике.

Рассмотрим следующие модели объектов и контроллер.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Вызов этого действия приведет к тому, что formatter выведет исключение, что переводится клиенту в код статуса 500 (Внутренняя ошибка сервера).

Чтобы сохранить ссылки на объекты в JSON, добавьте следующий код в метод **запуска приложений\_** в файлЕ Global.asax:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Теперь действие контроллера вернет JSON, который выглядит следующим образом:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Обратите внимание, что &quot;сериалайзер добавляет свойство $id&quot; к обоим объектам. Кроме того, он обнаруживает, что свойство Employee.Department создает цикл, поэтому он&quot;&quot;заменяет значение ссылкой на объект: $ref:&quot;1&quot;.

> [!NOTE]
> Ссылки на объекты не являются стандартными в JSON. Прежде чем использовать эту функцию, подумайте, смогут ли ваши клиенты разобрать результаты. Возможно, лучше просто удалить циклы с графика. Например, ссылка от сотрудника обратно в отдел на самом деле не требуется в этом примере.

Чтобы сохранить ссылки на объекты в XML, у вас есть два варианта. Более простой вариант `[DataContract(IsReference=true)]` заключается в добавлении к классу модели. Параметр *IsReference* позволяет ссылаться на объекты. Помните, что **DataContract** делает сериализацию отказаться, так что вам также нужно будет добавить **атрибуты DataMember** к свойствам:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Теперь formatter будет производить XML похож на следующие:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Если вы хотите избежать атрибутов в классе моделей, есть еще один вариант: создать новый экземпляр **DataContractSerializer** и установить *preserveObjectСсылки* на **истину** в конструкторе. Затем установите этот экземпляр в качестве сериализатора для каждого типа на formatter медиа-типа XML. Следующий код показывает, как это сделать:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Тестирование сериализации объектов

При проектировании веб-API полезно проверить, как будут сериализованы объекты данных. Это можно сделать без создания контроллера или вызывая действие контроллера.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
