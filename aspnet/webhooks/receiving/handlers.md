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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="a737a-103">обработчики ASP.NET WebHooks</span><span class="sxs-lookup"><span data-stu-id="a737a-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="a737a-104">После проверки запросов WebHooks приемником WebHook готов к обработке с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="a737a-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="a737a-105">Это где *обработчики* приходят дюйма</span><span class="sxs-lookup"><span data-stu-id="a737a-105">This is where *handlers* come in.</span></span> <span data-ttu-id="a737a-106">Обработчики вытекают из интерфейса [IWebHookHandler,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) но обычно используют класс [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) вместо того, чтобы выводятся непосредственно из интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a737a-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="a737a-107">Запрос WebHook может быть обработан одним или несколько обработчиками.</span><span class="sxs-lookup"><span data-stu-id="a737a-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="a737a-108">Обработчики называются в порядке, основанном на их соответствующем свойстве *Заказа,* переходяот из самого низкого к самому высокому, где Заказ является простым рядом (предлагается быть между 1 и 100):</span><span class="sxs-lookup"><span data-stu-id="a737a-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![Диаграмма обработчика Обработчика WebHook](_static/Handlers.png)

<span data-ttu-id="a737a-110">Обработчик может дополнительно установить свойство *ответа* на WebHookHandlerContext, что приведет к остановке обработки и отправке ответа обратно в качестве ответа HTTP на WebHook.</span><span class="sxs-lookup"><span data-stu-id="a737a-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="a737a-111">В приведенном выше случае обработчик C не будет вызываться, поскольку он имеет более высокий порядок, чем B и B устанавливает ответ.</span><span class="sxs-lookup"><span data-stu-id="a737a-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="a737a-112">Настройка ответа обычно актуальна только для WebHooks, где ответ может донести информацию до исходного API.</span><span class="sxs-lookup"><span data-stu-id="a737a-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="a737a-113">Это, например, случай с Slack WebHooks, где ответ размещается обратно на канал, откуда пришел WebHook.</span><span class="sxs-lookup"><span data-stu-id="a737a-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="a737a-114">Обработчики могут установить свойство получателя, если они хотят получать WebHooks от этого конкретного получателя.</span><span class="sxs-lookup"><span data-stu-id="a737a-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="a737a-115">Если они не устанавливают приемник, они призваны для всех из них.</span><span class="sxs-lookup"><span data-stu-id="a737a-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="a737a-116">Еще одно распространенное использование ответа заключается в использовании ответа *410 Gone,* чтобы указать, что WebHook больше не активен и никакие дополнительные запросы не должны быть представлены.</span><span class="sxs-lookup"><span data-stu-id="a737a-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="a737a-117">По умолчанию обработчик будет вызываться всеми приемниками WebHook.</span><span class="sxs-lookup"><span data-stu-id="a737a-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="a737a-118">Однако, если свойство *получателя* настроено на имя обработчика, то этот обработчик будет получать запросы WebHook только от этого получателя.</span><span class="sxs-lookup"><span data-stu-id="a737a-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="a737a-119">Обработка WebHook</span><span class="sxs-lookup"><span data-stu-id="a737a-119">Processing a WebHook</span></span>

<span data-ttu-id="a737a-120">При вызове обработчика он получает [WebHookHandlerContext,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) содержащий информацию о запросе WebHook.</span><span class="sxs-lookup"><span data-stu-id="a737a-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="a737a-121">Данные, как правило, орган запроса HTTP, доступны из свойства *данных.*</span><span class="sxs-lookup"><span data-stu-id="a737a-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="a737a-122">Тип данных обычно JSON или HTML-формы данных, но можно отбросить на более конкретный тип при желании.</span><span class="sxs-lookup"><span data-stu-id="a737a-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="a737a-123">Например, пользовательские WebHooks, генерируемые ASP.NET WebHooks, могут быть отброшены в тип [Пользовательских Уведомлений](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a737a-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="a737a-124">Обработка в очереди</span><span class="sxs-lookup"><span data-stu-id="a737a-124">Queued Processing</span></span>

<span data-ttu-id="a737a-125">Большинство отправителей WebHook отправит веб-крюк, если ответ не генерируется в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="a737a-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="a737a-126">Это означает, что обработчик должен завершить обработку в течение этого периода времени, чтобы не вызываться снова.</span><span class="sxs-lookup"><span data-stu-id="a737a-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="a737a-127">Если обработка занимает больше времени или лучше обрабатывать отдельно, то [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) можно использовать для отправки запроса WebHook в очередь, например [очередь хранения Azure.](https://msdn.microsoft.com/library/azure/dd179353.aspx)</span><span class="sxs-lookup"><span data-stu-id="a737a-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="a737a-128">Наброски реализации [WebHook'ue](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)</span><span class="sxs-lookup"><span data-stu-id="a737a-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
