---
uid: webhooks/receiving/receivers
title: Приемники ASP.NET веб-перехватчиков | Документация Майкрософт
author: rick-anderson
description: Приемники веб-перехватчики ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038981"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="69e08-103">Приемники веб-перехватчики ASP.NET</span><span class="sxs-lookup"><span data-stu-id="69e08-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="69e08-104">Получение веб-перехватчики зависит от того, кто является отправителем.</span><span class="sxs-lookup"><span data-stu-id="69e08-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="69e08-105">Иногда возникают дополнительные действия, регистрация веб-перехватчика, проверка того, что действительно ожидает передачи данных подписчика.</span><span class="sxs-lookup"><span data-stu-id="69e08-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="69e08-106">Некоторые веб-перехватчики предоставляют модель push-to-pull, где запрос HTTP POST только содержит ссылку на сведения о событии, которое затем требуется извлечь независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="69e08-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="69e08-107">Зачастую модель безопасности довольно зависит.</span><span class="sxs-lookup"><span data-stu-id="69e08-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="69e08-108">Веб-перехватчики Microsoft ASP.NET предназначена для того, чтобы сделать его более простой и более согласованным для подключения к API без тратит слишком много времени, разбираясь способ обработки какой-либо определенный вариант веб-перехватчики.</span><span class="sxs-lookup"><span data-stu-id="69e08-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="69e08-109">Получатель веб-перехватчика несет ответственность за принятие и проверку веб-перехватчики конкретного отправителя.</span><span class="sxs-lookup"><span data-stu-id="69e08-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="69e08-110">Получатель веб-перехватчика может поддерживать любое количество веб-перехватчики, каждый из которых свою собственную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="69e08-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="69e08-111">Например получатель веб-перехватчика GitHub может принимать веб-перехватчиков из любое количество репозиториев GitHub.</span><span class="sxs-lookup"><span data-stu-id="69e08-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="69e08-112">Идентификаторы URI приемника веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="69e08-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="69e08-113">Установка веб-перехватчики Microsoft ASP.NET обеспечивает общие контроллер веб-перехватчика, который принимает запросы веб-перехватчика из неограниченного числа служб.</span><span class="sxs-lookup"><span data-stu-id="69e08-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="69e08-114">Когда запрос прибывает, он выбирает соответствующий получатель, который вы установили для обработки конкретного отправителя веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="69e08-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="69e08-115">URI этого контроллера — URI веб-перехватчика, который можно зарегистрировать в службе и имеет вид:</span><span class="sxs-lookup"><span data-stu-id="69e08-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="69e08-116">По соображениям безопасности многих приемники веб-перехватчика требуют URI *https* URI и в некоторых случаях он также должен содержать параметр дополнительный запрос, который используется для принудительного применения, что только они предназначались можно отправлять выше URI веб-перехватчиков .</span><span class="sxs-lookup"><span data-stu-id="69e08-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="69e08-117">`<receiver>` Компонент является имя получателя, например `github` или `slack`.</span><span class="sxs-lookup"><span data-stu-id="69e08-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="69e08-118">*{Id}* является необязательным идентификатором, который может использоваться для идентификации конкретной конфигурации приемника веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="69e08-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="69e08-119">Это можно использовать для регистрации N веб-перехватчиков с определенной получателем.</span><span class="sxs-lookup"><span data-stu-id="69e08-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="69e08-120">Например следующие три URI можно использовать для регистрации для трех независимых веб-перехватчиков:</span><span class="sxs-lookup"><span data-stu-id="69e08-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="69e08-121">Установка получатель веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="69e08-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="69e08-122">Для получения веб-перехватчики, с помощью веб-перехватчики Microsoft ASP.NET, сначала установите пакет Nuget для поставщика веб-перехватчика или вы хотите получать веб-перехватчиков из поставщиков.</span><span class="sxs-lookup"><span data-stu-id="69e08-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="69e08-123">Пакеты Nuget именуются [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) где последняя часть указывает службе, поддерживаемой.</span><span class="sxs-lookup"><span data-stu-id="69e08-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="69e08-124">Пример</span><span class="sxs-lookup"><span data-stu-id="69e08-124">For example</span></span>

<span data-ttu-id="69e08-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) обеспечивает поддержку для получения веб-перехватчиков из GitHub и [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) обеспечивает поддержку для получения веб-перехватчиков, созданных ASP. Веб-перехватчики NET.</span><span class="sxs-lookup"><span data-stu-id="69e08-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="69e08-126">Без дополнительной настройки можно получить поддержку для Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello и WordPress, но можно поддерживать любое количество других поставщиков.</span><span class="sxs-lookup"><span data-stu-id="69e08-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="69e08-127">Настройки приемника веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="69e08-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="69e08-128">Приемники веб-перехватчика настраиваются через [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) интерфейсу и конкретной реализации этого интерфейса могут быть зарегистрированы с помощью любой модели внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="69e08-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="69e08-129">Реализация по умолчанию использует параметры приложения, который может быть установлено либо в файле Web.config или, если с помощью веб-приложений Azure, можно задать с помощью [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="69e08-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Параметры приложения Azure](_static/AzureAppSettings.png)

<span data-ttu-id="69e08-131">Ниже приведен формат для параметра приложения ключей:</span><span class="sxs-lookup"><span data-stu-id="69e08-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="69e08-132">Значение — разделенный запятыми список значений, соответствующих *{id}* значения, для которых веб-перехватчиков зарегистрированных, например:</span><span class="sxs-lookup"><span data-stu-id="69e08-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="69e08-133">Инициализация получатель веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="69e08-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="69e08-134">Приемники веб-перехватчика инициализируются зарегистрировав их, обычно в *WebApiConfig* статического класса, например:</span><span class="sxs-lookup"><span data-stu-id="69e08-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
