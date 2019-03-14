---
title: Различия между SignalR и ASP.NET Core SignalR
author: bradygaster
description: Различия между SignalR и ASP.NET Core SignalR
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.date: 11/14/2018
uid: signalr/version-differences
ms.openlocfilehash: 091fc44fccf820a394e7c6f775700c85bebc9101
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046901"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a>Различия между ASP.NET SignalR и ASP.NET Core SignalR

ASP.NET Core SignalR несовместим с клиентами или серверами для ASP.NET SignalR. В этой статье описаны возможности, которые были удалены или изменены в ASP.NET Core SignalR.

## <a name="how-to-identify-the-signalr-version"></a>Как определить версию SignalR

|                      | ASP.NET SignalR | ASP.NET Core SignalR |
| -------------------- | --------------- | -------------------- |
| Пакет NuGet Server | [Microsoft.AspNet.SignalR](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)<br>[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework) |
| Клиентские пакеты NuGet | [Microsoft.AspNet.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[Microsoft.AspNet.SignalR.JS](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [Microsoft.AspNetCore.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| Клиент npm пакета | [SignalR](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| Клиент Java | [Репозиторий GitHub](https://github.com/SignalR/java-client) (устаревшая версия)  | Пакет maven [com.microsoft.signalr](https://search.maven.org/artifact/com.microsoft.signalr/signalr) |
| Тип сервера приложений | ASP.NET (System.Web) или тестированием OWIN | ASP.NET Core |
| Поддерживаемые серверные платформы | .NET framework 4.5 или более поздней версии | .NET Framework 4.6.1 или более поздней версии<br>.NET core 2.1 или более поздней версии |

## <a name="feature-differences"></a>Различия в функциях

### <a name="automatic-reconnects"></a>Автоматическое повторных подключений

Автоматическое повторных подключений не поддерживаются в ASP.NET Core SignalR. При отключении клиента, необходимо явным образом запустить новое соединение для повторного подключения. В ASP.NET SignalR SignalR пытается подключиться к серверу, если соединение разорвано. 

### <a name="protocol-support"></a>Поддержка протоколов

ASP.NET Core SignalR поддерживает JSON, а также новый двоичный протокол, основанный на [MessagePack](xref:signalr/messagepackhubprotocol). Кроме того можно создать пользовательские протоколы.

### <a name="transports"></a>Транспорты

Транспорт навсегда кадров не поддерживается в ASP.NET Core SignalR.

## <a name="differences-on-the-server"></a>Различия на сервере

Серверные библиотеки ASP.NET Core SignalR, включаются в [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) пакет, который является частью **веб-приложение ASP.NET Core** шаблона MVC и Razor проекты.

ASP.NET Core SignalR — по промежуточного слоя ASP.NET Core, поэтому он должен быть настроен путем вызова [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) в `Startup.ConfigureServices`.

```csharp
services.AddSignalR()
```

Чтобы настроить маршрутизацию, сопоставляются с маршруты концентраторов внутри [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) вызов метода `Startup.Configure` метод.

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a>Прикрепленные сеансы

Модель горизонтального масштабирования для ASP.NET SignalR позволяет клиентам подключение и отправку сообщений на любой сервер в ферме. В ASP.NET Core SignalR клиент должен взаимодействовать с тот же сервер в течение всего соединения. Для горизонтального масштабирования с помощью Redis, это означает, что прикрепленные сеансы являются обязательными. Для горизонтального масштабирования с помощью [служба Azure SignalR](/azure/azure-signalr/), прикрепленные сеансы не требуются, так как служба обрабатывает подключения к клиентам. 

### <a name="single-hub-per-connection"></a>Единый центр на соединение

В ASP.NET Core SignalR упрощена модель соединения. Соединения устанавливаются непосредственно в одном центре, а не одного соединения, используемого для общий доступ для нескольких центров.

### <a name="streaming"></a>Потоковые операторы

ASP.NET Core SignalR теперь поддерживает [потоковой передачи данных](xref:signalr/streaming) от концентратора клиенту.

### <a name="state"></a>Регион

Возможность передавать произвольное состояние между клиентами и концентратор (часто называемые HubState) был удален, а также поддержка сообщения о ходе выполнения. На данный момент нет не существовал центра учетных записей-посредников.

### <a name="persistentconnection-removal"></a>Удаление PersistentConnection

В ASP.NET Core SignalR [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118)) класс был удален. 

### <a name="globalhost"></a>GlobalHost

ASP.NET Core имеет внедрение зависимостей (DI), встроенные в платформу. Службы могут использовать внедрение Зависимостей для доступа к [HubContext](xref:signalr/hubcontext). `GlobalHost` Объект, который используется в ASP.NET SignalR для получения `HubContext` не существует в ASP.NET Core SignalR.

### <a name="hubpipeline"></a>HubPipeline

ASP.NET Core SignalR не поддерживает `HubPipeline` модулей.

## <a name="differences-on-the-client"></a>Различия на стороне клиента

### <a name="typescript"></a>TypeScript

ASP.NET Core SignalR клиента создается на языке [TypeScript](https://www.typescriptlang.org/). Можно написать на языке JavaScript или TypeScript при использовании [клиента JavaScript](xref:signalr/javascript-client).

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>Клиент JavaScript размещается в [npm](https://www.npmjs.com/)

В предыдущих версиях клиента JavaScript был получен через пакет NuGet в Visual Studio. Для версий ядра [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) пакет npm содержит библиотеки JavaScript. Этот пакет не входит в **веб-приложение ASP.NET Core** шаблона. Получить и установить с помощью npm `@aspnet/signalr` пакета npm.

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

Зависимость от jQuery был удален, однако проекты по-прежнему можете использовать jQuery.

### <a name="internet-explorer-support"></a>Поддержка Internet Explorer

ASP.NET Core SignalR требуется Microsoft Internet Explorer 11 или более поздней версии (ASP.NET SignalR поддерживается Microsoft Internet Explorer 8 и более поздние версии).

### <a name="javascript-client-method-syntax"></a>Синтаксис метода клиента JavaScript

Синтаксис JavaScript был изменен с предыдущей версии SignalR. Вместо использования `$connection` следует создать соединения с помощью [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

Используйте [на](/javascript/api/@aspnet/signalr/HubConnection#on) метод для указания клиентских методов, которые могут вызывать концентратора.

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

После создания метода клиента, запустите подключение концентратора. Цепочка [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) метод входа или обработки ошибок.

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>Центр учетных записей-посредников

Больше не будет автоматически создаются прокси концентратора. Вместо этого передается имя метода [вызова](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API как строка.

### <a name="net-and-other-clients"></a>.NET и других клиентов

`Microsoft.AspNetCore.SignalR.Client` Пакет NuGet содержит клиентские библиотеки .NET для ASP.NET Core SignalR.

Используйте [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) Создание и построение экземпляр подключения к концентратору.

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a>Различия горизонтального масштабирования

ASP.NET SignalR поддерживает SQL Server и Redis. ASP.NET Core SignalR поддерживает служба Azure SignalR и Redis.

### <a name="aspnet"></a>ASP.NET

* [Масштабирование SignalR с помощью служебной шины Azure](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [Масштабирование SignalR с помощью Redis](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [Масштабирование SignalR с помощью SQL Server](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a>ASP.NET Core

* [Служба Azure SignalR](/azure/azure-signalr/)

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Центры](xref:signalr/hubs)
* [Клиент JavaScript](xref:signalr/javascript-client)
* [Клиент .NET](xref:signalr/dotnet-client)
* [Поддерживаемые платформы](xref:signalr/supported-platforms)
