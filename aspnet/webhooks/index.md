---
uid: webhooks/index
title: ASP.NET веб-хуки Обзор (ru) Документы Майкрософт
author: rick-anderson
description: Введение в ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675431"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="561ea-103">обзор webHooks ASP.NET</span><span class="sxs-lookup"><span data-stu-id="561ea-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="561ea-104">WebHooks представляет собой легкий шаблон HTTP, обеспечивающий простую модель паб/суб для проводки web-aIS и сервисов SaaS.</span><span class="sxs-lookup"><span data-stu-id="561ea-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="561ea-105">Когда событие происходит в службе, уведомление отправляется в виде запроса HTTP POST зарегистрированным абонентам.</span><span class="sxs-lookup"><span data-stu-id="561ea-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="561ea-106">Запрос POST содержит информацию о событии, которая позволяет получателю действовать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="561ea-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="561ea-107">Из-за своей простоты, WebHooks уже подвергаются большое количество услуг, включая [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Полоса](http://www.stripe.com), [Trello](http://www.trello.com/), и многое другое.</span><span class="sxs-lookup"><span data-stu-id="561ea-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="561ea-108">Например, WebHook может указать, что файл изменился в [Dropbox,](http://dropbox.com/)или изменение кода было зафиксировано в GitHub, или платеж был инициирован в [PayPal](http://www.paypal.com/), или карта была создана в [Trello](http://www.trello.com/).</span><span class="sxs-lookup"><span data-stu-id="561ea-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="561ea-109">Возможности безграничны!</span><span class="sxs-lookup"><span data-stu-id="561ea-109">The possibilities are endless!</span></span>

<span data-ttu-id="561ea-110">Корпорация Майкрософт ASP.NET WebHooks упрощает отправку и получение WebHooks как части приложения ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="561ea-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="561ea-111">Что касается принимающей стороны, то она обеспечивает общую модель для приема и обработки WebHooks от любого числа поставщиков WebHook.</span><span class="sxs-lookup"><span data-stu-id="561ea-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="561ea-112">Он выходит из коробки с поддержкой [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) и [Zendesk,](https://www.zendesk.com/) но это легко добавить поддержку для более.</span><span class="sxs-lookup"><span data-stu-id="561ea-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="561ea-113">На стороне отправки он обеспечивает поддержку для управления и хранения подписок, а также для отправки уведомлений о событиях в нужный набор абонентов.</span><span class="sxs-lookup"><span data-stu-id="561ea-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="561ea-114">Это позволяет определить свой собственный набор событий, на которые подписчики могут подписаться, и уведомить их, когда что-то происходит.</span><span class="sxs-lookup"><span data-stu-id="561ea-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="561ea-115">Эти две части могут быть использованы вместе или друг от друга в зависимости от вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="561ea-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="561ea-116">Если вам нужно только получать WebHooks от других служб, то вы можете использовать только часть приемника; если вы только хотите разоблачить WebHooks для других потреблять, то вы можете сделать именно это.</span><span class="sxs-lookup"><span data-stu-id="561ea-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="561ea-117">Код нацелен ASP.NET Web API 2 и ASP.NET MVC 5 и доступен в качестве [OSS на GitHub.](https://github.com/aspnet/WebHooks)</span><span class="sxs-lookup"><span data-stu-id="561ea-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="561ea-118">Обзор WebHooks</span><span class="sxs-lookup"><span data-stu-id="561ea-118">WebHooks Overview</span></span>

<span data-ttu-id="561ea-119">WebHooks — это шаблон, который означает, что он изменяет, как он используется от службы к службе, но основная идея та же.</span><span class="sxs-lookup"><span data-stu-id="561ea-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="561ea-120">Вы можете думать о WebHooks как простой паб / суб-модель, где пользователь может подписаться на события, происходящие в другом месте.</span><span class="sxs-lookup"><span data-stu-id="561ea-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="561ea-121">Уведомления о событии распространяются как запросы HTTP POST, содержащие информацию о самом событии.</span><span class="sxs-lookup"><span data-stu-id="561ea-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="561ea-122">Обычно запрос HTTP POST содержит данные об объекте JSON или HTML-формы, определенные отправителем WebHook, включая информацию о событии, вызывающую срабатывание WebHook.</span><span class="sxs-lookup"><span data-stu-id="561ea-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="561ea-123">Например, тело запроса WebHook POST от [GitHub](https://www.github.com/) выглядит следующим образом в результате открытия новой проблемы в определенном репозитории:</span><span class="sxs-lookup"><span data-stu-id="561ea-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="561ea-124">Чтобы убедиться, что WebHook действительно от предполагаемого отправителя, post запрос защищен в некотором роде, а затем проверить приемник.</span><span class="sxs-lookup"><span data-stu-id="561ea-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="561ea-125">Например, [GitHub WebHooks](https://developer.github.com/webhooks/) включает в себя *заголовок X-Hub-Signature* HTTP с хэшом органа запроса, который проверяется реализацией получателя, так что вам не придется беспокоиться об этом.</span><span class="sxs-lookup"><span data-stu-id="561ea-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="561ea-126">Поток WebHook обычно идет что-то вроде этого:</span><span class="sxs-lookup"><span data-stu-id="561ea-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="561ea-127">Отправитель WebHook предоставляет события, на которые клиент может подписаться.</span><span class="sxs-lookup"><span data-stu-id="561ea-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="561ea-128">События описывают наблюдаемые изменения в системе, например, что был вставлен новый элемент данных, что процесс завершен, или что-то еще.</span><span class="sxs-lookup"><span data-stu-id="561ea-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="561ea-129">Приемник WebHook подписывается, регистрируя WebHook, состоящий из четырех вещей:</span><span class="sxs-lookup"><span data-stu-id="561ea-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="561ea-130">URI, где уведомление о событии должно быть размещено в виде запроса HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="561ea-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="561ea-131">Набор фильтров, описывающих конкретные события, для которых webHook должен быть уволен;</span><span class="sxs-lookup"><span data-stu-id="561ea-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="561ea-132">Секретный ключ, который используется для подписания запроса HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="561ea-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="561ea-133">Дополнительные данные, которые должны быть включены в запрос HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="561ea-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="561ea-134">Это могут быть, например, дополнительные поля заголовка HTTP или свойства, включенные в орган запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="561ea-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="561ea-135">Как только событие происходит, соответствующие регистрации WebHook найдены и http POST запросы представлены.</span><span class="sxs-lookup"><span data-stu-id="561ea-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="561ea-136">Как правило, генерация запросов HTTP POST повторно повторяется несколько раз, если по какой-то причине получатель не отвечает или запрос HTTP POST приводит к ответу на ошибку.</span><span class="sxs-lookup"><span data-stu-id="561ea-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="561ea-137">Конвейер обработки WebHooks</span><span class="sxs-lookup"><span data-stu-id="561ea-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="561ea-138">Конвейер обработки ASP.NET WebHooks для входящих WebHooks выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="561ea-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET конвейер обработки WebHooks](_static/WebHookReceivers.png)

<span data-ttu-id="561ea-140">Двумя ключевыми концепциями здесь являются *приемники* и *обработчики:*</span><span class="sxs-lookup"><span data-stu-id="561ea-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="561ea-141">*Получатели* несут ответственность за обработку конкретного вкуса WebHook от данного отправителя и для обеспечения проверки безопасности, чтобы убедиться, что запрос WebHook действительно от предполагаемого отправителя.</span><span class="sxs-lookup"><span data-stu-id="561ea-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="561ea-142">*Обработчики,* как правило, где пользовательский код работает обработки конкретного WebHook.</span><span class="sxs-lookup"><span data-stu-id="561ea-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="561ea-143">В следующих узлах эти понятия описаны более подробно.</span><span class="sxs-lookup"><span data-stu-id="561ea-143">In the following nodes these concepts are described in more details.</span></span>
