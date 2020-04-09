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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="27752-103">JSON и XML Сериализация в ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="27752-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="27752-104">[Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="27752-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="27752-105">В этой статье описаны статьи JSON и XML в ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="27752-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="27752-106">В ASP.NET Web API, *formatter медиа-типа* является объектом, который может:</span><span class="sxs-lookup"><span data-stu-id="27752-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="27752-107">Читать объекты CLR из тела сообщений HTTP</span><span class="sxs-lookup"><span data-stu-id="27752-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="27752-108">Запись объектов CLR в тело сообщения HTTP</span><span class="sxs-lookup"><span data-stu-id="27752-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="27752-109">Web API предоставляет предписывание медиа-типа как для JSON, так и для XML.</span><span class="sxs-lookup"><span data-stu-id="27752-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="27752-110">Рамки вставляют эти предзначения в конвейер по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27752-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="27752-111">Клиенты могут запросить JSON или XML в заголовке запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="27752-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="27752-112">Содержимое</span><span class="sxs-lookup"><span data-stu-id="27752-112">Contents</span></span>

- [<span data-ttu-id="27752-113">JSON Медиа-Тип Formatter</span><span class="sxs-lookup"><span data-stu-id="27752-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="27752-114">Только для чтения свойства</span><span class="sxs-lookup"><span data-stu-id="27752-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="27752-115">Даты</span><span class="sxs-lookup"><span data-stu-id="27752-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="27752-116">Отступы</span><span class="sxs-lookup"><span data-stu-id="27752-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="27752-117">Верблюд Касинг</span><span class="sxs-lookup"><span data-stu-id="27752-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="27752-118">Анонимные и слабо набранные объекты</span><span class="sxs-lookup"><span data-stu-id="27752-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="27752-119">XML Медиа-Тип Formatter</span><span class="sxs-lookup"><span data-stu-id="27752-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="27752-120">Только для чтения свойства</span><span class="sxs-lookup"><span data-stu-id="27752-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="27752-121">Даты</span><span class="sxs-lookup"><span data-stu-id="27752-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="27752-122">Отступы</span><span class="sxs-lookup"><span data-stu-id="27752-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="27752-123">Установка серизаторов Per-Type XML</span><span class="sxs-lookup"><span data-stu-id="27752-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="27752-124">Удаление JSON или XML Formatter</span><span class="sxs-lookup"><span data-stu-id="27752-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="27752-125">Обработка ссылки на круговые объекты</span><span class="sxs-lookup"><span data-stu-id="27752-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="27752-126">Тестирование сериализации объектов</span><span class="sxs-lookup"><span data-stu-id="27752-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="27752-127">JSON Медиа-Тип Formatter</span><span class="sxs-lookup"><span data-stu-id="27752-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="27752-128">Форматирование JSON обеспечивается классом **JsonMediaTypeFormatter.**</span><span class="sxs-lookup"><span data-stu-id="27752-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="27752-129">По умолчанию **JsonMediaTypeFormatter** использует [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) библиотеку для выполнения сериализации.</span><span class="sxs-lookup"><span data-stu-id="27752-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="27752-130">Json.NET является сторонним проектом с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="27752-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="27752-131">Если вы предпочитаете, вы можете настроить класс **JsonMediaTypeFormatter,** чтобы использовать **DataContractJsonSerializer** вместо Json.NET.</span><span class="sxs-lookup"><span data-stu-id="27752-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="27752-132">Для этого установите свойство **UseDataContractJsonSerializer** на **истину:**</span><span class="sxs-lookup"><span data-stu-id="27752-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="27752-133">Сериализация JSON</span><span class="sxs-lookup"><span data-stu-id="27752-133">JSON Serialization</span></span>

<span data-ttu-id="27752-134">В этом разделе описаны некоторые конкретные поведения formatter JSON, использующие [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) сериализатор по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27752-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="27752-135">Это не должна быть всеобъемлющая документация Json.NET библиотеки; для получения дополнительной информации см [Json.NET.](http://james.newtonking.com/projects/json/help/)</span><span class="sxs-lookup"><span data-stu-id="27752-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="27752-136">Что получает сериализации?</span><span class="sxs-lookup"><span data-stu-id="27752-136">What Gets Serialized?</span></span>

<span data-ttu-id="27752-137">По умолчанию все публичные свойства и поля включены в сериализованный JSON.</span><span class="sxs-lookup"><span data-stu-id="27752-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="27752-138">Чтобы опустить свойство или поле, украсьте его атрибутом **JsonIgnore.**</span><span class="sxs-lookup"><span data-stu-id="27752-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="27752-139">Если вы &quot;предпочитаете&quot; подход, выбираемый, украсьте класс атрибутом **DataContract.**</span><span class="sxs-lookup"><span data-stu-id="27752-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="27752-140">При наличии этого атрибута участники игнорируются, если у них нет **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="27752-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="27752-141">Вы также можете использовать **DataMember** для сериализации частных членов.</span><span class="sxs-lookup"><span data-stu-id="27752-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="27752-142">Только для чтения свойства</span><span class="sxs-lookup"><span data-stu-id="27752-142">Read-Only Properties</span></span>

<span data-ttu-id="27752-143">Свойства только для чтения сериализируются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27752-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="27752-144">даты.</span><span class="sxs-lookup"><span data-stu-id="27752-144">Dates</span></span>

<span data-ttu-id="27752-145">По умолчанию Json.NET пишет даты в формате [ISO 8601.](http://www.w3.org/TR/NOTE-datetime)</span><span class="sxs-lookup"><span data-stu-id="27752-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="27752-146">Даты в UTC (Кооркоорорное универсальное время) написаны суффиксом "я".</span><span class="sxs-lookup"><span data-stu-id="27752-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="27752-147">Даты в местное время включают в себя смещение часового пояса.</span><span class="sxs-lookup"><span data-stu-id="27752-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="27752-148">Пример:</span><span class="sxs-lookup"><span data-stu-id="27752-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="27752-149">По умолчанию Json.NET сохраняет часовой пояс.</span><span class="sxs-lookup"><span data-stu-id="27752-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="27752-150">Вы можете переопределить это, установив свойство DateTime'oneHandling:</span><span class="sxs-lookup"><span data-stu-id="27752-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="27752-151">Если вы предпочитаете использовать формат`"\/Date(ticks)\/"`даты Microsoft [JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) () вместо ISO 8601, установите свойство **DateFormatHandling** на настройках serializer:</span><span class="sxs-lookup"><span data-stu-id="27752-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="27752-152">Отступы</span><span class="sxs-lookup"><span data-stu-id="27752-152">Indenting</span></span>

<span data-ttu-id="27752-153">Чтобы написать отступом JSON, установите настройки **форматирования** на **Formatting.Indented:**</span><span class="sxs-lookup"><span data-stu-id="27752-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="27752-154">Верблюд Касинг</span><span class="sxs-lookup"><span data-stu-id="27752-154">Camel Casing</span></span>

<span data-ttu-id="27752-155">Чтобы написать имена свойств JSON с корпусом верблюда, не изменяя модель данных, установите **CamelCasePropertyNames.**</span><span class="sxs-lookup"><span data-stu-id="27752-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="27752-156">Анонимные и слабо набранные объекты</span><span class="sxs-lookup"><span data-stu-id="27752-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="27752-157">Метод действия может вернуть анонимный объект и сериализировать его в JSON.</span><span class="sxs-lookup"><span data-stu-id="27752-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="27752-158">Пример:</span><span class="sxs-lookup"><span data-stu-id="27752-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="27752-159">Тело сообщения ответа будет содержать следующее JSON:</span><span class="sxs-lookup"><span data-stu-id="27752-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="27752-160">Если ваш веб-aPI получает от клиентов слабо структурированные объекты JSON, можно разработать тело запроса в **типе Newtonsoft.JObject.**</span><span class="sxs-lookup"><span data-stu-id="27752-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="27752-161">Тем не менее, как правило, лучше использовать сильно набранные объекты данных.</span><span class="sxs-lookup"><span data-stu-id="27752-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="27752-162">Тогда вам не нужно анализировать данные самостоятельно, и вы получаете преимущества проверки модели.</span><span class="sxs-lookup"><span data-stu-id="27752-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="27752-163">Серийный xML не поддерживает анонимные типы или экземпляры **JObject.**</span><span class="sxs-lookup"><span data-stu-id="27752-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="27752-164">Если вы используете эти функции для данных JSON, следует удалить из конвейера материал XML, как описано позднее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="27752-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="27752-165">XML Медиа-Тип Formatter</span><span class="sxs-lookup"><span data-stu-id="27752-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="27752-166">Форматирование XML обеспечивается классом **XmlMediaTypeFormatter.**</span><span class="sxs-lookup"><span data-stu-id="27752-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="27752-167">По умолчанию **XmlMediaTypeFormatter** использует класс **DataContractSerializer** для выполнения сериализации.</span><span class="sxs-lookup"><span data-stu-id="27752-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="27752-168">Если вы предпочитаете, вы можете настроить **XmlMediaTypeFormatter** использовать **XmlSerializer** вместо **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="27752-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="27752-169">Чтобы сделать это, установите свойство **UseXmlSerializer** на **истину:**</span><span class="sxs-lookup"><span data-stu-id="27752-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="27752-170">Класс **XmlSerializer** поддерживает более узкий набор типов, чем **DataContractSerializer,** но дает больше контроля над полученным XML.</span><span class="sxs-lookup"><span data-stu-id="27752-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="27752-171">Рассмотрите возможность использования **XmlSerializer,** если вам необходимо сопоставить существующую схему XML.</span><span class="sxs-lookup"><span data-stu-id="27752-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="27752-172">Сериализация XML</span><span class="sxs-lookup"><span data-stu-id="27752-172">XML Serialization</span></span>

<span data-ttu-id="27752-173">В этом разделе описаны некоторые конкретные поведения XML formatter, используя по умолчанию **DataContractSerializer.**</span><span class="sxs-lookup"><span data-stu-id="27752-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="27752-174">По умолчанию DataContractSerializer ведет себя следующим образом:</span><span class="sxs-lookup"><span data-stu-id="27752-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="27752-175">Все свойства чтения/записи общего пользования/записи сериализируются.</span><span class="sxs-lookup"><span data-stu-id="27752-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="27752-176">Чтобы опустить свойство или поле, украсьте его атрибутом **IgnoreDataMember.**</span><span class="sxs-lookup"><span data-stu-id="27752-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="27752-177">Частные и защищенные члены не сериализуются.</span><span class="sxs-lookup"><span data-stu-id="27752-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="27752-178">Свойства только для чтения не сериализируются.</span><span class="sxs-lookup"><span data-stu-id="27752-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="27752-179">(Однако содержимое свойства коллекции только для чтения сериализуется.)</span><span class="sxs-lookup"><span data-stu-id="27752-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="27752-180">Имена классов и членов пишутся в XML точно так же, как они отображаются в декларации класса.</span><span class="sxs-lookup"><span data-stu-id="27752-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="27752-181">Используется пространство имен XML по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27752-181">A default XML namespace is used.</span></span>

<span data-ttu-id="27752-182">Если вам нужно больше контроля над сериализацией, вы можете украсить класс атрибутом **DataContract.**</span><span class="sxs-lookup"><span data-stu-id="27752-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="27752-183">При этом атрибуте класс сериализируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="27752-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="27752-184">&quot;Выберите&quot; подход: Свойства и поля не сериализируются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27752-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="27752-185">Чтобы выставить нанету свойство или поле, украсьте его атрибутом **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="27752-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="27752-186">Чтобы сериализовать частного или защищенного участника, украсьте его атрибутом **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="27752-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="27752-187">Свойства только для чтения не сериализируются.</span><span class="sxs-lookup"><span data-stu-id="27752-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="27752-188">Чтобы изменить отогнание имени класса в XML, установите параметр *имени* в атрибуте **DataContract.**</span><span class="sxs-lookup"><span data-stu-id="27752-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="27752-189">Чтобы изменить отогнание имени участника в XML, установите параметр *имени* в атрибуте **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="27752-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="27752-190">Чтобы изменить пространство имен XML, установите параметр *Namespace* в классе **DataContract.**</span><span class="sxs-lookup"><span data-stu-id="27752-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="27752-191">Только для чтения свойства</span><span class="sxs-lookup"><span data-stu-id="27752-191">Read-Only Properties</span></span>

<span data-ttu-id="27752-192">Свойства только для чтения не сериализируются.</span><span class="sxs-lookup"><span data-stu-id="27752-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="27752-193">Если свойство только для чтения имеет резервное частное поле, можно отметить частное поле атрибутом **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="27752-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="27752-194">Этот подход требует атрибута **DataContract** в классе.</span><span class="sxs-lookup"><span data-stu-id="27752-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="27752-195">даты.</span><span class="sxs-lookup"><span data-stu-id="27752-195">Dates</span></span>

<span data-ttu-id="27752-196">Даты написаны в формате ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="27752-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="27752-197">Например, &quot;2012-05-23T20:21:37.9116538&quot;.</span><span class="sxs-lookup"><span data-stu-id="27752-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="27752-198">Отступы</span><span class="sxs-lookup"><span data-stu-id="27752-198">Indenting</span></span>

<span data-ttu-id="27752-199">Чтобы написать отступ XML, установите свойство **Indent** на **истину:**</span><span class="sxs-lookup"><span data-stu-id="27752-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="27752-200">Установка серизаторов Per-Type XML</span><span class="sxs-lookup"><span data-stu-id="27752-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="27752-201">Можно установить различные серийные XML для различных типов CLR.</span><span class="sxs-lookup"><span data-stu-id="27752-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="27752-202">Например, у вас может быть определенный объект данных, который требует **XmlSerializer** для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="27752-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="27752-203">Вы можете использовать **XmlSerializer** для этого объекта и продолжать использовать **DataContractSerializer** для других типов.</span><span class="sxs-lookup"><span data-stu-id="27752-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="27752-204">Чтобы установить серийный xML для определенного типа, позвоните **SetSerializer.**</span><span class="sxs-lookup"><span data-stu-id="27752-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="27752-205">Вы можете указать **XmlSerializer** или любой объект, который происходит от **XmlObjectSerializer**.</span><span class="sxs-lookup"><span data-stu-id="27752-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="27752-206">Удаление JSON или XML Formatter</span><span class="sxs-lookup"><span data-stu-id="27752-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="27752-207">Вы можете удалить formatter JSON или XML из списка навсегда, если вы не хотите их использовать.</span><span class="sxs-lookup"><span data-stu-id="27752-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="27752-208">Основные причины для этого:</span><span class="sxs-lookup"><span data-stu-id="27752-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="27752-209">Ограничить ваши ответы Web API на определенный тип носителя.</span><span class="sxs-lookup"><span data-stu-id="27752-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="27752-210">Например, можно решить поддерживать только ответы JSON и удалить значение XML.</span><span class="sxs-lookup"><span data-stu-id="27752-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="27752-211">Заменить по умолчанию formatter на пользовательский formatter.</span><span class="sxs-lookup"><span data-stu-id="27752-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="27752-212">Например, можно заменить formatter JSON на собственную пользовательскую реализацию formatter JSON.</span><span class="sxs-lookup"><span data-stu-id="27752-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="27752-213">Следующий код показывает, как удалить предтечи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27752-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="27752-214">Назовите это методом **запуска приложений,\_** определенным в Global.asax.</span><span class="sxs-lookup"><span data-stu-id="27752-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="27752-215">Обработка ссылки на круговые объекты</span><span class="sxs-lookup"><span data-stu-id="27752-215">Handling Circular Object References</span></span>

<span data-ttu-id="27752-216">По умолчанию formatters JSON и XML пишут все объекты как значения.</span><span class="sxs-lookup"><span data-stu-id="27752-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="27752-217">Если два свойства относятся к одному и тому же объекту или если один и тот же объект появляется дважды в коллекции, то значение будет сериализировать объект дважды.</span><span class="sxs-lookup"><span data-stu-id="27752-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="27752-218">Это особая проблема, если график объекта содержит циклы, потому что serializer будет бросать исключение, когда он обнаруживает цикл в графике.</span><span class="sxs-lookup"><span data-stu-id="27752-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="27752-219">Рассмотрим следующие модели объектов и контроллер.</span><span class="sxs-lookup"><span data-stu-id="27752-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="27752-220">Вызов этого действия приведет к тому, что formatter выведет исключение, что переводится клиенту в код статуса 500 (Внутренняя ошибка сервера).</span><span class="sxs-lookup"><span data-stu-id="27752-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="27752-221">Чтобы сохранить ссылки на объекты в JSON, добавьте следующий код в метод **запуска приложений\_** в файлЕ Global.asax:</span><span class="sxs-lookup"><span data-stu-id="27752-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="27752-222">Теперь действие контроллера вернет JSON, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="27752-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="27752-223">Обратите внимание, что &quot;сериалайзер добавляет свойство $id&quot; к обоим объектам.</span><span class="sxs-lookup"><span data-stu-id="27752-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="27752-224">Кроме того, он обнаруживает, что свойство Employee.Department создает цикл, поэтому он&quot;&quot;заменяет значение ссылкой на объект: $ref:&quot;1&quot;.</span><span class="sxs-lookup"><span data-stu-id="27752-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="27752-225">Ссылки на объекты не являются стандартными в JSON.</span><span class="sxs-lookup"><span data-stu-id="27752-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="27752-226">Прежде чем использовать эту функцию, подумайте, смогут ли ваши клиенты разобрать результаты.</span><span class="sxs-lookup"><span data-stu-id="27752-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="27752-227">Возможно, лучше просто удалить циклы с графика.</span><span class="sxs-lookup"><span data-stu-id="27752-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="27752-228">Например, ссылка от сотрудника обратно в отдел на самом деле не требуется в этом примере.</span><span class="sxs-lookup"><span data-stu-id="27752-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="27752-229">Чтобы сохранить ссылки на объекты в XML, у вас есть два варианта.</span><span class="sxs-lookup"><span data-stu-id="27752-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="27752-230">Более простой вариант `[DataContract(IsReference=true)]` заключается в добавлении к классу модели.</span><span class="sxs-lookup"><span data-stu-id="27752-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="27752-231">Параметр *IsReference* позволяет ссылаться на объекты.</span><span class="sxs-lookup"><span data-stu-id="27752-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="27752-232">Помните, что **DataContract** делает сериализацию отказаться, так что вам также нужно будет добавить **атрибуты DataMember** к свойствам:</span><span class="sxs-lookup"><span data-stu-id="27752-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="27752-233">Теперь formatter будет производить XML похож на следующие:</span><span class="sxs-lookup"><span data-stu-id="27752-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="27752-234">Если вы хотите избежать атрибутов в классе моделей, есть еще один вариант: создать новый экземпляр **DataContractSerializer** и установить *preserveObjectСсылки* на **истину** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="27752-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="27752-235">Затем установите этот экземпляр в качестве сериализатора для каждого типа на formatter медиа-типа XML.</span><span class="sxs-lookup"><span data-stu-id="27752-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="27752-236">Следующий код показывает, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="27752-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="27752-237">Тестирование сериализации объектов</span><span class="sxs-lookup"><span data-stu-id="27752-237">Testing Object Serialization</span></span>

<span data-ttu-id="27752-238">При проектировании веб-API полезно проверить, как будут сериализованы объекты данных.</span><span class="sxs-lookup"><span data-stu-id="27752-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="27752-239">Это можно сделать без создания контроллера или вызывая действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="27752-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
