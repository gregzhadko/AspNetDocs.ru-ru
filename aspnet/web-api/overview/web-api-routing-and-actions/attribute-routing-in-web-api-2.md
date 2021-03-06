---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: АтрибутИрование в ASP.NET Web API 2 Документы Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675386"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>Реукторация атрибутов в ASP.NET Web API 2

[Майк Уоссон](https://github.com/MikeWasson)

*Трассировка* — это то, как Web API соответствует URI действию. Web API 2 поддерживает новый тип трассировки, называемый *размыванием атрибутов.* Как следует из названия, маршрутирование атрибутов использует атрибуты для определения маршрутов. Трассировка атрибутов дает вам больше контроля над URIs в вашем веб-API. Например, можно легко создать УРИ, описывающие иерархии ресурсов.

Более ранний стиль разгрома, называемый реуляционным, по-прежнему полностью поддерживается. На самом деле, вы можете объединить обе техники в одном проекте.

В этой теме показано, как включить разгром атрибутов, и описаны различные параметры для разгрома атрибутов. Для сквозного учебника, использующемся трассировку атрибутов, [см.](create-a-rest-api-with-attribute-routing.md)

## <a name="prerequisites"></a>Предварительные требования

[Визуальная студия 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Сообщество, Профессиональный или Корпоративный выпуск

Кроме того, используйте NuGet Package Manager для установки необходимых пакетов. Из меню **Инструменты** в Visual Studio, выберите **NuGet менеджер пакета**, а затем выберите **консоль менеджер пакетов**. Введите следующую команду в окне консоли менеджера пакетов:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Почему атрибут ирование?

В первом выпуске Web API использовалась реуктора *на основе конвенций.* В этом типе маршрутизации вы определяете один или несколько шаблонов маршрутов, которые в основном являются параметражными строками. Когда фреймворк получает запрос, он сопоставляет URI с шаблоном маршрута. Для получения дополнительной информации о реунетировке на основе конвенций с [ASP.NETм.](routing-in-aspnet-web-api.md)

Одним из преимуществ реуктора на основе конвенций является то, что шаблоны определяются в одном месте, а правила разгрома последовательно применяются во всех контроллерах. К сожалению, на основе конвенций, что затрудняет поддержку некоторых шаблонов URI, которые распространены в RESTful AIS. Например, ресурсы часто содержат детские ресурсы: у клиентов есть заказы, у фильмов есть актеры, у книг есть авторы и так далее. Естественно создавать УРИ, отражающие эти отношения:

`/customers/1/orders`

Этот тип URI трудно создать с помощью конференц-реуктора. Хотя это может быть сделано, результаты не масштабируются хорошо, если у вас есть много контроллеров или типов ресурсов.

При маршрутизаторе атрибутов тривиально определить маршрут для этого URI. Вы просто добавляете атрибут в действие контроллера:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Вот некоторые другие шаблоны, которые атрибут разгрома делает легко.

**Управление версиями API**

В этом примере "/api/v1/products" будет направляться другому контроллеру, чем "/api/v2/products".

`/api/v1/products`
`/api/v2/products`

**Перегруженные сегменты URI**

В этом примере "1" — это номер заказа, но «ожидающий» карты к коллекции.

`/orders/1`
`/orders/pending`

**Несколько типов параметров**

В этом примере "1" является номером заказа, но "2013/06/16" указывает дату.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Включение реуктора атрибутов

Чтобы включить маршрутизирование атрибутов, звоните **MapHttpAttributeRoutes** во время конфигурации. Этот метод расширения определен в классе **System.Web.httpConfigurationExtensions.**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

Реуничная реуктора может быть объединена с реунетировкой [на основе конвенций.](routing-in-aspnet-web-api.md) Чтобы определить маршруты, основанные на конвенциях, позвоните в метод **MapHttpRoute.**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Для получения дополнительной информации о настройке Web API см [ASP.NET.](../advanced/configuring-aspnet-web-api.md)

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Примечание: Миграция из Web API 1

До Web API 2 шаблоны проекта Web API генерировали код следующим образом:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Если возможно расширение реаутирования атрибутов, этот код будет бросать исключение. При обновлении существующего проекта Web API для использования входном атрибутике не забудьте обновить этот код конфигурации до следующего:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Для получения дополнительной информации см [ASP.NET.](../advanced/configuring-aspnet-web-api.md#webhost)

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Добавление атрибутов маршрута

Вот пример маршрута, определяемого с помощью атрибута:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

Строка &quot;клиентов / «customerId»/заказы&quot; является шаблоном URI для маршрута. Web API пытается сопоставить запрос URI с шаблоном. В этом примере "клиенты" и "заказы" являются буквальными сегментами, а "customerId" является переменным параметром. Следующие URIs будут соответствовать этому шаблону:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Можно ограничить соответствие, используя [ограничения,](#constraints)описанные позже в этой теме.

Обратите внимание, что параметр &quot;«customerId»&quot; в шаблоне маршрута соответствует названию параметра *customerId* в методе. Когда Web API вызывает действие контроллера, он пытается связать параметры маршрута. Например, если URI `http://example.com/customers/1/orders`является, Web API пытается связать значение "1" с параметром *customerId* в действии.

Шаблон URI может иметь несколько параметров:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Любые методы контроллера, не имеющие атрибута маршрута, используют маршрутную маршрутизм на основе конвенции. Таким образом, можно объединить оба типа реуктора в одном проекте.

## <a name="http-methods"></a>Методы HTTP

Web API также выбирает действия на основе метода HTTP запроса (GET, POST и т.д.). По умолчанию Web API ищет нечувствительный к нечувствительным совпадение с началом имени метода контроллера. Например, метод контроллера, названный, `PutCustomers` соответствует запросу HTTP PUT.

Вы можете переопределить эту конвенцию, усвоив метод с любыми следующими атрибутами:

- **(HttpDelete)**
- **[HttpGet]**
- **(Httphead)**
- **(HttpOptions)**
- **(Httppatch)**
- **(HttpPost)**
- **(Httpput)**

Следующий пример отображает метод CreateBook для запросов HTTP POST.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Для всех других методов HTTP, включая нестандартные методы, используйте атрибут **AcceptVerbs,** который использует список методов HTTP.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Префиксы маршрута

Часто маршруты в контроллере начинаются с одной и той же префикса. Пример:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

Вы можете установить общую префикс для всего контроллера, используя атрибут **«RoutePrefix»:**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

Используйте tilde (я) на атрибуте метода, чтобы переопределить префикс маршрута:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

Префикс маршрута может включать параметры:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Ограничения маршрута

Ограничения маршрута позволяют ограничить согласование параметров в шаблоне маршрута. Общий синтаксис является &quot;«параметр:ограничение».&quot; Пример:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

Здесь первый маршрут будет выбран только &quot;&quot; в том случае, если сегмент идентификатора URI является бесразмереным. В противном случае будет выбран второй маршрут.

В следующей таблице перечислены ограничения, которые поддерживаются.

| Ограничение | Описание | Пример |
| --- | --- | --- |
| alpha | Матчи верхнего регистра или нижней регистра латинских алфавитных символов (a-z, A-) | х:альфа |
| bool | Соответствует значению Boolean. | (x:bool) |
| DATETIME | Соответствует значению **DateTime.** | время свидания: |
| Decimal | Соответствует десятичное значение. | x:десятичная) |
| double | Соответствует 64-битное значение плавающей точки. | х:двойной) |
| FLOAT | Соответствует 32-битное плавающее значение. | (x:float) |
| guid | Соответствует значению GUID. | (x:guid) |
| INT | Соответствует 32-битное значение. | (x:int) |
| length | Соответствует строке с указанной длиной или в пределах заданного диапазона длин. | x:длина (6) x:длина (1,20) |
| long | Соответствует 64-битное значение. | х:длинный) |
| max | Соответствует ряду с максимальным значением. | х:макс (10) |
| Maxlength | Соответствует строке с максимальной длиной. | x:maxlength (10) |
| Min | Соответствует ряду с минимальным значением. | х:мин (10) |
| миндлина | Соответствует строке с минимальной длиной. | (x:minlength)) |
| range | Соответствует целым числам в пределах диапазона значений. | диапазон (10,50) |
| regex | Соответствует регулярному выражению. | x:regex ('d{3}-d{3}-d{4}$)) |

Обратите внимание, что некоторые &quot;ограничения,&quot;такие как мин, принимают аргументы в скобках. Можно применить несколько ограничений к параметру, разделенному толстой кишка.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Пользовательские ограничения маршрутов

Можно создать пользовательские ограничения маршрута, реализовав интерфейс **IHttpRouteConstraint.** Например, следующее ограничение ограничивает параметр ненулевым значением рядом.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

Следующий код показывает, как зарегистрировать ограничение:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Теперь вы можете применить ограничение в своих маршрутах:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

Вы также можете заменить весь класс **DefaultInlineConstraintResolver,** внедрив интерфейс **IInlineConstraintResolver.** Это заменит все встроенные ограничения, если только реализация **IInlineConstraintResolver** специально не добавит их.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>Дополнительные параметры URI и значения по умолчанию

Можно сделать параметр URI необязательным, добавив вопросительный знак к параметру маршрута. Если параметр маршрута неявляется, необходимо определить значение по умолчанию для параметра метода.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

В этом `/api/books/locale/1033` примере и `/api/books/locale` верните тот же ресурс.

Кроме того, в шаблоне маршрута можно указать значение по умолчанию следующим образом:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

Это почти то же самое, что и в предыдущем примере, но при применении значения по умолчанию существует небольшая разница в поведении.

- В первом примере (""'lcid:int?) значение по умолчанию 1033 присваивается непосредственно параметру метода, поэтому параметр будет иметь это точное значение.
- Во втором примере ("""lcid:int-1033") значение по умолчанию "1033" проходит процесс привязки модели. Модель-связующего по умолчанию преобразует "1033" в числовое значение 1033. Тем не менее, вы можете подключить пользовательские модели связующего, которые могли бы сделать что-то другое.

(В большинстве случаев, если у вас нет пользовательских связующих моделей в конвейере, эти две формы будут эквивалентными.)

<a id="route-names"></a>
## <a name="route-names"></a>Названия маршрутов

В Web API каждый маршрут имеет свое имя. Имена маршрутов полезны для создания ссылок, так что вы можете включить ссылку в ответ HTTP.

Чтобы указать имя маршрута, установите свойство **имени** на атрибуте. В следующем примере показано, как установить имя маршрута, а также как использовать имя маршрута при создании ссылки.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Заказ маршрута

Когда фреймворк пытается сопоставить URI с маршрутом, он оценивает маршруты в определенном порядке. Чтобы указать порядок, установите свойство **Заказа** в атрибуте маршрута. В первую очередь оцениваются более низкие значения. Значение заказа по умолчанию равен нулю.

Вот как определяется общий порядок:

1. Сравните свойство **заказа** атрибута маршрута.
2. Посмотрите на каждый сегмент URI в шаблоне маршрута. Для каждого сегмента закажите следующее:

    1. Литературные сегменты.
    2. Параметры маршрута с ограничениями.
    3. Параметры маршрута без ограничений.
    4. Сегменты параметров Wildcard с ограничениями.
    5. Параметр Wildcard сегментируется без ограничений.
3. В случае галстука маршруты заказываются нечувствительным или нечувствительным сравнением строк ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) шаблона маршрута.

Ниже приведен пример. Предположим, вы определяете следующий контроллер:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Эти маршруты упорядочены следующим образом.

1. заказы/детали
2. заказы/id
3. заказы/«Имя клиента»
4. заказы/дата\*
5. заказы/ожидающие

Обратите внимание, что "детали" является буквальным сегментом и появляется перед "id", но "в ожидании" появляется последним, потому что свойство **Заказа** 1. (Этот пример предполагает, что нет клиентов с именами "подробности" или "в ожидании". В общем, старайтесь избегать неоднозначных маршрутов. В этом примере лучшим `GetByCustomer` шаблоном маршрута является "клиенты /"CustomerName" )
