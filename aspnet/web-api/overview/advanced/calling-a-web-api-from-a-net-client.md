---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Вызов веб-API из клиента .NET (C#) — ASP.NET 4. x
author: MikeWasson
description: В этом руководстве показано, как вызвать веб-API из приложения .NET 4. x.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172943"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>Вызов веб-API из клиента .NET (C#)

[Майк Уоссон](https://github.com/MikeWasson) и [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[Скачивание завершенного проекта](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample). [Указания по скачиванию](/aspnet/core/tutorials/#how-to-download-a-sample). 

В этом руководстве показано, как вызвать веб-API из приложения .NET с помощью [System .NET. http. HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)

В этом руководстве написано клиентское приложение, использующее следующий веб-API:

| Действие | Метод HTTP | Относительный URI |
| --- | --- | --- |
| Получение сведений о продукте по идентификатору | GET | *идентификатор* /АПИ/Продуктс/ |
| Создать продукт | POST | /апи/продуктс |
| Обновить продукт | ОТПРАВКА | *идентификатор* /АПИ/Продуктс/ |
| Удалить продукт | DELETE | *идентификатор* /АПИ/Продуктс/ |

Сведения о том, как реализовать этот API с веб-API ASP.NET, см. в разделе [Создание веб-API, поддерживающего операции CRUD](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).

Для простоты клиентское приложение в этом учебнике является консольным приложением Windows. **HttpClient** также поддерживается для приложений Windows Phone и магазина Windows. Дополнительные сведения см. в статье [написание кода клиента веб-API для нескольких платформ с помощью переносимых библиотек](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) .

**Примечание.** При передаче базовых URL-адресов и относительных URI в виде жестко заданных значений следует учитывать правила использования `HttpClient` API. `HttpClient.BaseAddress`Для свойства необходимо задать адрес с завершающей косой чертой ( `/` ). Например, при передаче в метод жестко запрограммированных URI ресурсов `HttpClient.GetAsync` не включайте в начале косую черту вперед. Чтобы получить объект `Product` по идентификатору:

1. Параметр`client.BaseAddress = new Uri("https://localhost:5001/");`
1. Запрос а `Product` . Например, `client.GetAsync<Product>("api/products/4");`.

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>Создание консольного приложения

В Visual Studio создайте новое консольное приложение Windows с именем **хттпклиентсампле** и вставьте следующий код:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

Приведенный выше код является полноценным клиентским приложением.

`RunAsync`выполняется и блокируется до завершения. Большинство методов **HttpClient** являются асинхронными, так как они выполняют сетевые операции ввода-вывода. Все асинхронные задачи выполняются внутри `RunAsync` . Обычно приложение не блокирует основной поток, но это приложение не позволяет никакого взаимодействия.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>Установка клиентских библиотек веб-API

Используйте диспетчер пакетов NuGet для установки пакета клиентских библиотек веб-API.

В меню **Инструменты** выберите **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**. В консоли диспетчера пакетов (PMC) введите следующую команду:

`Install-Package Microsoft.AspNet.WebApi.Client`

Предыдущая команда добавляет в проект следующие пакеты NuGet:

* Microsoft. AspNet. WebApi. Client
* Newtonsoft.Json.

Нетвонсофт. JSON (также называется Json.NET) — это популярная высокопроизводительная платформа JSON для .NET.

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>Добавление класса модели

Проверьте класс `Product`:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

Этот класс соответствует модели данных, используемой веб-API. Приложение может использовать **HttpClient** для чтения `Product` экземпляра из HTTP-ответа. Приложению не нужно писать код десериализации.

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>Создание и инициализация HttpClient

Изучите статическое свойство **HttpClient** :

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient** предназначен для однократного создания и повторного использования в течение всего жизненного цикла приложения. Следующие условия могут привести к ошибкам **SocketException** :

* Создание нового экземпляра **HttpClient** для каждого запроса.
* Сервер при интенсивной нагрузке.

Создание нового экземпляра **HttpClient** для каждого запроса может исчерпать доступные сокеты.

Следующий код инициализирует экземпляр **HttpClient** :

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

Предыдущий код:

* Задает базовый URI для HTTP-запросов. Измените номер порта на порт, используемый в серверном приложении. Приложение не будет работать, если не используется порт для серверного приложения.
* Устанавливает заголовок Accept в значение Application/JSON. Установка этого заголовка сообщает серверу о необходимости отправки данных в формате JSON.

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>Отправка запроса GET для получения ресурса

Следующий код отправляет запрос GET для продукта:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

Метод **Async** ОТПРАВЛЯЕТ запрос HTTP GET. Когда метод завершает работу, он возвращает **HttpResponseMessage** , СОДЕРЖАЩИЙ ответ HTTP. Если код состояния в ответе является кодом успешного выполнения, текст ответа содержит представление JSON продукта. Вызовите **реадасасинк** , чтобы десериализовать полезные данные JSON в `Product` экземпляре. Метод **реадасасинк** является асинхронным, так как текст ответа может быть произвольным большим.

**HttpClient** не создает исключение, если HTTP-ответ содержит код ошибки. Вместо этого свойство **IsSuccessStatusCode** имеет **значение false** , если состояние — код ошибки. Если вы предпочитаете обрабатывать коды ошибок HTTP как исключения, вызовите метод [HttpResponseMessage. енсуресукцессстатускоде](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) для объекта Response. `EnsureSuccessStatusCode`создает исключение, если код состояния находится за пределами диапазона 200 &ndash; 299. Обратите внимание, что **HttpClient** может создавать исключения по другим причинам, например при истечении &mdash; времени ожидания запроса.

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>Модули форматирования типов мультимедиа для десериализации

Когда **реадасасинк** вызывается без параметров, он использует набор *модулей форматирования мультимедиа* по умолчанию для чтения текста ответа. Модули форматирования по умолчанию поддерживают данные JSON, XML и кодируются в формате URL.

Вместо использования модулей форматирования по умолчанию можно предоставить список модулей форматирования для метода **реадасасинк** .  Использование списка модулей форматирования полезно при наличии пользовательского модуля форматирования типа мультимедиа:

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

Дополнительные сведения см. [в разделе модули форматирования мультимедиа в веб-API ASP.NET 2](../formats-and-model-binding/media-formatters.md) .

## <a name="sending-a-post-request-to-create-a-resource"></a>Отправка запроса POST для создания ресурса

Следующий код отправляет запрос POST, содержащий `Product` экземпляр в формате JSON:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

Метод **постасжсонасинк** :

* Сериализует объект в JSON.
* Отправляет полезные данные JSON в запрос POST.

Если запрос будет выполнен, выполните следующие действия:

* Он должен возвращать ответ 201 (создан).
* Ответ должен содержать URL-адрес созданных ресурсов в заголовке Location.

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>Отправка запроса на размещение для обновления ресурса

Следующий код отправляет запрос на размещение для обновления продукта:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

Метод **путасжсонасинк** работает так же, как **постасжсонасинк**, за исключением того, что он отправляет запрос на размещение вместо POST.

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>Отправка запроса на удаление для удаления ресурса

Следующий код отправляет запрос на удаление для удаления продукта:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

Как и в случае GET, запрос на удаление не содержит текст запроса. Не нужно указывать формат JSON или XML с помощью DELETE.

## <a name="test-the-sample"></a>Тестирование примера

Чтобы протестировать клиентское приложение, выполните следующие действия.

1. [Скачайте](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) и запустите серверное приложение. [Указания по скачиванию](/aspnet/core/#how-to-download-a-sample). Убедитесь, что серверное приложение работает. Например, `http://localhost:64195/api/products` должен возвращать список продуктов.
2. Задайте базовый URI для HTTP-запросов. Измените номер порта на порт, используемый в серверном приложении.
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. Запустите клиентское приложение. Выводятся следующие результаты.

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
