---
title: Открытый веб-интерфейс для .NET (OWIN) в ASP.NET Core
author: ardalis
description: Сведения о том, как ASP.NET Core поддерживает открытый веб-интерфейс для .NET (OWIN), позволяющий ослабить связь веб-приложений с веб-серверами.
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 12/18/2018
uid: fundamentals/owin
ms.openlocfilehash: 51982c7ebc4f66c2b0b73bf425d9ecbd0bf37826
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065061"
---
# <a name="open-web-interface-for-net-owin-with-aspnet-core"></a>Открытый веб-интерфейс для .NET (OWIN) в ASP.NET Core

Авторы: [Стив Смит (Steve Smith)](https://ardalis.com/) и [Рик Андерсон (Rick Anderson)](https://twitter.com/RickAndMSFT)

ASP.NET Core поддерживает открытый веб-интерфейс для .NET (OWIN). OWIN позволяет ослабить зависимость веб-приложений от веб-сервера. Он определяет стандартный способ использования ПО промежуточного в конвейере для обработки запросов и связанных с ними откликов. Приложения ASP.NET Core и ПО промежуточного слоя могут взаимодействовать с приложениями, серверами и ПО промежуточного слоя, основанными на OWIN.

OWIN обеспечивает разделительный уровень, позволяющий совместно использовать две платформы с разнородными объектными моделями. Пакет `Microsoft.AspNetCore.Owin` содержит две реализации адаптера:

* ASP.NET Core в OWIN 
* OWIN в ASP.NET Core

Это позволяет размещать ASP.NET Core поверх сервера или узла, совместимого с OWIN, а также запускать другие совместимые с OWIN компоненты поверх ASP.NET Core.

> [!NOTE]
> Использование этих адаптеров сопряжено с потерями производительности. Приложениям, использующим только компоненты ASP.NET Core, не следует использовать адаптеры или пакет `Microsoft.AspNetCore.Owin`.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="running-owin-middleware-in-the-aspnet-core-pipeline"></a>Выполнение ПО промежуточного слоя OWIN в конвейере ASP.NET Core

Поддержка OWIN для ASP.NET Core развертывается в составе пакета `Microsoft.AspNetCore.Owin`. Вы можете импортировать поддержку OWIN в проект, установив этот пакет.

ПО промежуточного слоя OWIN соответствует [спецификации OWIN](http://owin.org/spec/spec/owin-1.0.0.html), где требуется задать интерфейс `Func<IDictionary<string, object>, Task>` и определенные ключи (такие как `owin.ResponseBody`). Следующее простое ПО промежуточного слоя OWIN отображает сообщение "Hello World":

```csharp
public Task OwinHello(IDictionary<string, object> environment)
{
    string responseText = "Hello World via OWIN";
    byte[] responseBytes = Encoding.UTF8.GetBytes(responseText);

    // OWIN Environment Keys: http://owin.org/spec/spec/owin-1.0.0.html
    var responseStream = (Stream)environment["owin.ResponseBody"];
    var responseHeaders = (IDictionary<string, string[]>)environment["owin.ResponseHeaders"];

    responseHeaders["Content-Length"] = new string[] { responseBytes.Length.ToString(CultureInfo.InvariantCulture) };
    responseHeaders["Content-Type"] = new string[] { "text/plain" };

    return responseStream.WriteAsync(responseBytes, 0, responseBytes.Length);
}
```

Сигнатура примера возвращает `Task` и принимает `IDictionary<string, object>`, как того требует OWIN.

Приведенный ниже код показывает, как добавить ПО промежуточного слоя `OwinHello` (показано выше) в конвейер ASP.NET Core с помощью метода расширения `UseOwin`.

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseOwin(pipeline =>
    {
        pipeline(next => OwinHello);
    });
}
```

В конвейере OWIN можно настроить и другие действия.

> [!NOTE]
> Заголовки отклика можно изменять только до первой записи в поток отклика.

> [!NOTE]
> Из соображений производительности не рекомендуется выполнять несколько вызовов `UseOwin`. Компоненты OWIN лучше всего работают, когда сгруппированы друг с другом.

```csharp
app.UseOwin(pipeline =>
{
    pipeline(async (next) =>
    {
        // do something before
        await OwinHello(new OwinEnvironment(HttpContext));
        // do something after
    });
});
```

<a name="hosting-on-owin"></a>

## <a name="using-aspnet-core-hosting-on-an-owin-based-server"></a>Использование размещения ASP.NET Core на сервере OWIN

На основанных на OWIN серверах можно размещать приложения ASP.NET Core. Одним из них является веб-сервер OWIN для .NET с именем [Nowin](https://github.com/Bobris/Nowin). В пример для этой статьи я включил проект, который ссылается на Nowin и использует его для создания `IServer`, способного самостоятельно размещать ASP.NET Core.

[!code-csharp[](owin/sample/src/NowinSample/Program.cs?highlight=15)]

`IServer` — это интерфейс, которому нужно свойство `Features` и метод `Start`.

`Start` отвечает за настройку и запуск сервера, что в данном случае осуществляется с помощью ряда вызовов текучего API, которые задают адреса, полученные из IServerAddressesFeature путем анализа. Обратите внимание, что текучая конфигурация переменной `_builder` указывает, что запросы будут обрабатывать `appFunc`, определенной ранее в этом методе. Эта `Func` вызывается при каждом запросе на обработку входящих запросов.

Мы также добавим расширение `IWebHostBuilder`, чтобы упростить добавление и настройку сервера Nowin.

```csharp
using System;
using Microsoft.AspNetCore.Hosting.Server;
using Microsoft.Extensions.DependencyInjection;
using Nowin;
using NowinSample;

namespace Microsoft.AspNetCore.Hosting
{
    public static class NowinWebHostBuilderExtensions
    {
        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder)
        {
            return builder.ConfigureServices(services =>
            {
                services.AddSingleton<IServer, NowinServer>();
            });
        }

        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder, Action<ServerBuilder> configure)
        {
            builder.ConfigureServices(services =>
            {
                services.Configure(configure);
            });
            return builder.UseNowin();
        }
    }
}
```

Благодаря ему вы сможете вызвать расширение в *Program.cs* для запуска приложения ASP.NET Core с помощью этого пользовательского сервера:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Hosting;

namespace NowinSample
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseNowin()
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();

            host.Run();
        }
    }
}
```

Дополнительные сведения о [серверах ASP.NET Core](xref:fundamentals/servers/index).

## <a name="run-aspnet-core-on-an-owin-based-server-and-use-its-websockets-support"></a>Запуск ASP.NET Core на основанном на OWIN сервере и использование его поддержки WebSocket

Другим примером того, как ASP.NET Core может использовать функции сервера на основе OWIN, является доступ к таким функциям, как WebSocket. Веб-сервер OWIN .NET, используемый в предыдущем примере, имеет встроенную поддержку веб-сокетов, что может использовать приложение ASP.NET Core. Приведенный ниже пример показывает простое веб-приложение, которое поддерживает веб-сокеты и выводит обратно все данные, отправляемые на сервер через WebSocket.

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            if (context.WebSockets.IsWebSocketRequest)
            {
                WebSocket webSocket = await context.WebSockets.AcceptWebSocketAsync();
                await EchoWebSocket(webSocket);
            }
            else
            {
                await next();
            }
        });

        app.Run(context =>
        {
            return context.Response.WriteAsync("Hello World");
        });
    }

    private async Task EchoWebSocket(WebSocket webSocket)
    {
        byte[] buffer = new byte[1024];
        WebSocketReceiveResult received = await webSocket.ReceiveAsync(
            new ArraySegment<byte>(buffer), CancellationToken.None);

        while (!webSocket.CloseStatus.HasValue)
        {
            // Echo anything we receive
            await webSocket.SendAsync(new ArraySegment<byte>(buffer, 0, received.Count), 
                received.MessageType, received.EndOfMessage, CancellationToken.None);

            received = await webSocket.ReceiveAsync(new ArraySegment<byte>(buffer), 
                CancellationToken.None);
        }

        await webSocket.CloseAsync(webSocket.CloseStatus.Value, 
            webSocket.CloseStatusDescription, CancellationToken.None);
    }
}
```

Этот [пример](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) настроен с использованием того же `NowinServer`, что и предыдущий. Единственное различие заключается в том, как приложение настроено в его методе `Configure`. Тест, использующий [простой клиент WebSocket](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en), демонстрирует работу приложения:

![Тестовый клиент WebSocket](owin/_static/websocket-test.png)

## <a name="owin-environment"></a>Среда OWIN

Вы можете создать среду OWIN с помощью `HttpContext`.

```csharp

   var environment = new OwinEnvironment(HttpContext);
   var features = new OwinFeatureCollection(environment);
   ```

## <a name="owin-keys"></a>Ключи OWIN

OWIN использует объект `IDictionary<string,object>` для передачи сведений через систему обмена запросами и откликами HTTP. ASP.NET Core реализует указанные ниже ключи. См. [основную спецификацию, расширения](http://owin.org/#spec), а также статью [Рекомендации по ключам OWIN и общие ключи](http://owin.org/spec/spec/CommonKeys.html).

### <a name="request-data-owin-v100"></a>Данные запроса (OWIN версии 1.0.0)

| Ключ               | Значение (тип) | Описание: |
| ----------------- | ------------ | ----------- |
| owin.RequestScheme | `String` |  |
| owin.RequestMethod  | `String` | |    
| owin.RequestPathBase  | `String` | |    
| owin.RequestPath | `String` | |     
| owin.RequestQueryString  | `String` | |    
| owin.RequestProtocol  | `String` | |    
| owin.RequestHeaders | `IDictionary<string,string[]>`  | |
| owin.RequestBody | `Stream`  | |

### <a name="request-data-owin-v110"></a>Данные запроса (OWIN версии 1.1.0)

| Ключ               | Значение (тип) | Описание: |
| ----------------- | ------------ | ----------- |
| owin.RequestId | `String` | Optional |

### <a name="response-data-owin-v100"></a>Данные отклика (OWIN версии 1.0.0)

| Ключ               | Значение (тип) | Описание: |
| ----------------- | ------------ | ----------- |
| owin.ResponseStatusCode | `int` | Optional |
| owin.ResponseReasonPhrase | `String` | Optional |
| owin.ResponseHeaders | `IDictionary<string,string[]>`  | |
| owin.ResponseBody | `Stream`  | |


### <a name="other-data-owin-v100"></a>Другие данные (OWIN версии 1.0.0)

| Ключ               | Значение (тип) | Описание: |
| ----------------- | ------------ | ----------- |
| owin.CallCancelled | `CancellationToken` |  |
| owin.Version  | `String` | |   


### <a name="common-keys"></a>Общие ключи

| Ключ               | Значение (тип) | Описание |
| ----------------- | ------------ | ----------- |
| ssl.ClientCertificate | `X509Certificate` |  |
| ssl.LoadClientCertAsync  | `Func<Task>` | |    
| server.RemoteIpAddress  | `String` | |    
| server.RemotePort | `String` | |     
| server.LocalIpAddress  | `String` | |    
| server.LocalPort  | `String` | |    
| server.IsLocal  | `bool` | |    
| server.OnSendingHeaders  | `Action<Action<object>,object>` | |


### <a name="sendfiles-v030"></a>SendFiles версии 0.3.0

| Ключ               | Значение (тип) | Описание: |
| ----------------- | ------------ | ----------- |
| sendfile.SendAsync | См. описание [сигнатуры делегата](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) | Для каждого запроса |


### <a name="opaque-v030"></a>Opaque версии 0.3.0

| Ключ               | Значение (тип) | Описание |
| ----------------- | ------------ | ----------- |
| opaque.Version | `String` |  |
| opaque.Upgrade | `OpaqueUpgrade` | См. описание [сигнатуры делегата](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) |
| opaque.Stream | `Stream` |  |
| opaque.CallCancelled | `CancellationToken` |  |


### <a name="websocket-v030"></a>WebSocket версии 0.3.0

| Ключ               | Значение (тип) | Описание |
| ----------------- | ------------ | ----------- |
| websocket.Version | `String` |  |
| websocket.Accept | `WebSocketAccept` | См. описание [сигнатуры делегата](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) |
| websocket.AcceptAlt |  | Нет в спецификации |
| websocket.SubProtocol | `String` | См. [раздел 4.2.2 RFC6455](https://tools.ietf.org/html/rfc6455#section-4.2.2), шаг 5.5 |
| websocket.SendAsync | `WebSocketSendAsync` | См. описание [сигнатуры делегата](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)  |
| websocket.ReceiveAsync | `WebSocketReceiveAsync` | См. описание [сигнатуры делегата](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)  |
| websocket.CloseAsync | `WebSocketCloseAsync` | См. описание [сигнатуры делегата](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)  |
| websocket.CallCancelled | `CancellationToken` |  |
| websocket.ClientCloseStatus | `int` | Optional |
| websocket.ClientCloseDescription | `String` | Optional |

## <a name="additional-resources"></a>Дополнительные ресурсы

* [ПО промежуточного слоя](xref:fundamentals/middleware/index)
* [Серверы](xref:fundamentals/servers/index)
