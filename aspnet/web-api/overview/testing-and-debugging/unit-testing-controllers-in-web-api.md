---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: Контроллеры модульного тестирования в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: В этом разделе описываются некоторые методы, связанные с контроллерами модульного тестирования в веб-API 2. Перед прочтением этой статьи вы можете прочитать раздел учебника...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: ee933cfc736a07b91c8f7feea2c4a2c64d200942
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240655"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>Контроллеры модульного тестирования в ASP.NET веб-API 2

по [Майк Уоссон](https://github.com/MikeWasson)

> В этом разделе описываются некоторые методы, связанные с контроллерами модульного тестирования в веб-API 2. Перед прочтением этой статьи вы можете прочитать руководство [модульное тестирование веб-API ASP.NET 2](unit-testing-with-aspnet-web-api.md), в котором показано, как добавить проект модульного теста в решение.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Веб-API 2
> - [MOQ](https://github.com/Moq) 4.5.30

> [!NOTE]
> Я использовал MOQ, но та же идея применяется к любой инфраструктуре макетирования. MOQ 4.5.30 (и более поздние версии) поддерживает Visual Studio 2017, Roslyn и .NET 4,5 и более поздние версии.

Распространенный шаблон в модульных тестах — это оператор « &quot; организовать-акт-утверждение» &quot; :

- Расположение. Настройте все необходимые компоненты для выполнения теста.
- Акт: выполните тест.
- Assert: Проверка успешности теста.

На этапе упорядочивания часто используются объекты макета или заглушки. Это позволяет максимально сокращать количество зависимостей, поэтому тестирование посвящено тестированию одной вещи.

Ниже приведены некоторые вещи, которые следует выполнять при модульном тестировании на контроллерах веб-API.

- Действие возвращает правильный тип ответа.
- Недопустимые параметры возвращают правильный ответ об ошибке.
- Действие вызывает правильный метод в репозитории или слое служб.
- Если ответ содержит модель предметной области, проверьте тип модели.

Это некоторые из общих моментов тестирования, но конкретные особенности зависят от реализации контроллера. В частности, это значительно отличается от того, возвращают ли действия контроллера **HttpResponseMessage** или **ихттпактионресулт**. Дополнительные сведения об этих типах результатов см. [в разделе результаты действий в веб-API 2](../getting-started-with-aspnet-web-api/action-results.md).

## <a name="testing-actions-that-return-httpresponsemessage"></a>Тестирование действий, возвращающих HttpResponseMessage

Ниже приведен пример контроллера, действия которого возвращают **HttpResponseMessage**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

Обратите внимание, что контроллер использует внедрение зависимостей для внедрения `IProductRepository` . Это делает контроллер более пригодным для тестирования, так как вы можете внедрить макет репозитория. Следующий модульный тест проверяет, что `Get` метод записывает в `Product` текст ответа. Предположим, что `repository` является макетом `IProductRepository` .

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

Важно установить **запрос** и **конфигурацию** на контроллере. В противном случае тест завершится ошибкой с **ArgumentNullException** или **InvalidOperationException**.

## <a name="testing-link-generation"></a>Тестирование создания ссылки

`Post`Метод вызывает **Урлхелпер. Link** для создания ссылок в ответе. Для этого требуется немного больше настроек модульного теста.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

Классу **урлхелпер** требуется URL-адрес запроса и данные маршрута, поэтому тесту необходимо задать значения для них. Другой вариант — макет или заглушка **урлхелпер**. При таком подходе вы замените значение по умолчанию [ApiController. URL](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) на макет или версию заглушки, которая возвращает фиксированное значение.

Давайте перепишем тест с помощью платформы [MOQ](https://github.com/Moq) . Установите `Moq` пакет NuGet в тестовом проекте.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

В этой версии не нужно настраивать данные маршрута, так как макет **урлхелпер** Возвращает константную строку.

## <a name="testing-actions-that-return-ihttpactionresult"></a>Тестирование действий, возвращающих Ихттпактионресулт

В веб-API 2 действие контроллера может вернуть **ихттпактионресулт**, что аналогично **ACTIONRESULT** в ASP.NET MVC. Интерфейс **ихттпактионресулт** определяет шаблон команды для создания HTTP-ответов. Вместо создания ответа напрямую контроллер возвращает **ихттпактионресулт**. Позже конвейер вызывает **ихттпактионресулт** для создания ответа. Такой подход упрощает написание модульных тестов, поскольку можно пропустить множество настроек, необходимых для **HttpResponseMessage**.

Ниже приведен пример контроллера, действия которого возвращают **ихттпактионресулт**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

В этом примере показаны некоторые распространенные шаблоны, использующие **ихттпактионресулт**. Давайте посмотрим, как выполнять модульное тестирование.

### <a name="action-returns-200-ok-with-a-response-body"></a>Действие возвращает 200 (ОК) с текстом ответа.

`Get`Метод вызывает, `Ok(product)` Если продукт найден. В модульном тесте убедитесь, что возвращаемый тип — **окнеготиатедконтентресулт** , а возвращенный продукт имеет правильный идентификатор.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

Обратите внимание, что модульный тест не выполняет результат действия. Можно предположить, что результат действия правильно создает ответ HTTP. (Вот почему у платформы веб-API есть собственные модульные тесты!)

### <a name="action-returns-404-not-found"></a>Действие возвращает 404 (не найдено)

`Get`Метод вызывает, `NotFound()` Если продукт не найден. В этом случае модульный тест просто проверяет, является ли возвращаемый тип **нотфаундресулт**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>Действие возвращает 200 (ОК) без текста ответа

`Delete`Вызов метода `Ok()` возвращает пустой ответ HTTP 200. Как и в предыдущем примере, модульный тест проверяет возвращаемый тип, в данном случае **окресулт**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>Действие возвращает 201 (создано) с заголовком Location.

`Post`Вызов метода `CreatedAtRoute` ВОЗВРАЩАЕТ ответ HTTP 201 с URI в заголовке Location. В модульном тесте убедитесь, что действие задает правильные значения маршрутизации.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>Действие возвращает другой 2xx с текстом ответа

`Put`Вызов метода `Content` ВОЗВРАЩАЕТ ответ HTTP 202 (принято) с текстом ответа. Этот случай аналогичен возврату 200 (ОК), но модульный тест должен также проверять код состояния.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Имитация Entity Framework при модульном тестировании веб-API ASP.NET 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [Написание тестов для службы веб-API ASP.NET](https://docs.microsoft.com/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service) (запись блога с помощью йоуссеф мауссаауи).
- [Debugging ASP.NET Web API with Route Debugger (Отладка веб-API ASP.NET с помощью Route Debugger)](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
