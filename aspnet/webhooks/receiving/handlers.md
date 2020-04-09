---
uid: webhooks/receiving/handlers
title: ASP.NET обработчики WebHooks (ru) Документы Майкрософт
author: rick-anderson
description: Как обрабатывать запросы в ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675216"
---
# <a name="aspnet-webhooks-handlers"></a>обработчики ASP.NET WebHooks

После проверки запросов WebHooks приемником WebHook готов к обработке с помощью пользовательского кода. Это где *обработчики* приходят дюйма Обработчики вытекают из интерфейса [IWebHookHandler,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) но обычно используют класс [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) вместо того, чтобы выводятся непосредственно из интерфейса.

Запрос WebHook может быть обработан одним или несколько обработчиками. Обработчики называются в порядке, основанном на их соответствующем свойстве *Заказа,* переходяот из самого низкого к самому высокому, где Заказ является простым рядом (предлагается быть между 1 и 100):

![Диаграмма обработчика Обработчика WebHook](_static/Handlers.png)

Обработчик может дополнительно установить свойство *ответа* на WebHookHandlerContext, что приведет к остановке обработки и отправке ответа обратно в качестве ответа HTTP на WebHook. В приведенном выше случае обработчик C не будет вызываться, поскольку он имеет более высокий порядок, чем B и B устанавливает ответ.

Настройка ответа обычно актуальна только для WebHooks, где ответ может донести информацию до исходного API. Это, например, случай с Slack WebHooks, где ответ размещается обратно на канал, откуда пришел WebHook. Обработчики могут установить свойство получателя, если они хотят получать WebHooks от этого конкретного получателя. Если они не устанавливают приемник, они призваны для всех из них.

Еще одно распространенное использование ответа заключается в использовании ответа *410 Gone,* чтобы указать, что WebHook больше не активен и никакие дополнительные запросы не должны быть представлены.

По умолчанию обработчик будет вызываться всеми приемниками WebHook. Однако, если свойство *получателя* настроено на имя обработчика, то этот обработчик будет получать запросы WebHook только от этого получателя.

## <a name="processing-a-webhook"></a>Обработка WebHook

При вызове обработчика он получает [WebHookHandlerContext,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) содержащий информацию о запросе WebHook. Данные, как правило, орган запроса HTTP, доступны из свойства *данных.*

Тип данных обычно JSON или HTML-формы данных, но можно отбросить на более конкретный тип при желании. Например, пользовательские WebHooks, генерируемые ASP.NET WebHooks, могут быть отброшены в тип [Пользовательских Уведомлений](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) следующим образом:

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>Обработка в очереди

Большинство отправителей WebHook отправит веб-крюк, если ответ не генерируется в течение нескольких секунд. Это означает, что обработчик должен завершить обработку в течение этого периода времени, чтобы не вызываться снова.

Если обработка занимает больше времени или лучше обрабатывать отдельно, то [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) можно использовать для отправки запроса WebHook в очередь, например [очередь хранения Azure.](https://msdn.microsoft.com/library/azure/dd179353.aspx)

Наброски реализации [WebHook'ue](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
