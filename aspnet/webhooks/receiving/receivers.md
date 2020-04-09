---
uid: webhooks/receiving/receivers
title: ASP.NET приемники WebHooks Документы Майкрософт
author: rick-anderson
description: ASP.NET приемники WebHooks
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675165"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="12ae7-103">ASP.NET приемники WebHooks</span><span class="sxs-lookup"><span data-stu-id="12ae7-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="12ae7-104">Получение WebHooks зависит от того, кто является отправителем.</span><span class="sxs-lookup"><span data-stu-id="12ae7-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="12ae7-105">Иногда есть дополнительные шаги регистрации WebHook проверки того, что абонент действительно слушает.</span><span class="sxs-lookup"><span data-stu-id="12ae7-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="12ae7-106">Некоторые WebHooks предоставляют модель push-to-pull, где запрос HTTP POST содержит только ссылку на информацию о событии, которая затем должна быть извлечена независимо.</span><span class="sxs-lookup"><span data-stu-id="12ae7-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="12ae7-107">Часто модель безопасности меняется довольно много.</span><span class="sxs-lookup"><span data-stu-id="12ae7-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="12ae7-108">Цель Microsoft ASP.NET WebHooks — сделать ее проще и последовательнее, чтобы подключить ваш API, не тратя много времени на выяснение того, как обрабатывать какой-либо конкретный вариант WebHooks.</span><span class="sxs-lookup"><span data-stu-id="12ae7-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="12ae7-109">Приемник WebHook отвечает за прием и проверку WebHooks от конкретного отправителя.</span><span class="sxs-lookup"><span data-stu-id="12ae7-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="12ae7-110">Приемник WebHook может поддерживать любое количество WebHooks, каждый со своей собственной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="12ae7-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="12ae7-111">Например, приемник GitHub WebHook может принимать WebHooks из любого количества репозиториев GitHub.</span><span class="sxs-lookup"><span data-stu-id="12ae7-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="12ae7-112">Webhook приемник URIs</span><span class="sxs-lookup"><span data-stu-id="12ae7-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="12ae7-113">Установив Microsoft ASP.NET WebHooks, вы получаете общий контроллер WebHook, который принимает запросы WebHook от открытого количества служб.</span><span class="sxs-lookup"><span data-stu-id="12ae7-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="12ae7-114">Когда запрос поступает, он выбирает подходящий приемник, который вы установили для обработки конкретного отправителя WebHook.</span><span class="sxs-lookup"><span data-stu-id="12ae7-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="12ae7-115">URI этого контроллера webHook URI, который вы регистрируете в службе и имеет форму:</span><span class="sxs-lookup"><span data-stu-id="12ae7-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="12ae7-116">По соображениям безопасности многие приемники WebHook требуют, чтобы URI является *https* URI, а в некоторых случаях он должен также содержать дополнительный параметр запроса, который используется для обеспечения того, чтобы только предназначенная сторона может отправлять WebHooks в URI выше.</span><span class="sxs-lookup"><span data-stu-id="12ae7-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="12ae7-117">Компонент `<receiver>` является имя приемника, например, `github` или `slack`.</span><span class="sxs-lookup"><span data-stu-id="12ae7-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="12ae7-118">*«Id»* — это дополнительный идентификатор, который может быть использован для определения конкретной конфигурации приемника WebHook.</span><span class="sxs-lookup"><span data-stu-id="12ae7-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="12ae7-119">Это может быть использовано для регистрации N WebHooks с определенным приемником.</span><span class="sxs-lookup"><span data-stu-id="12ae7-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="12ae7-120">Например, следующие три URIs могут быть использованы для регистрации на три независимых WebHooks:</span><span class="sxs-lookup"><span data-stu-id="12ae7-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="12ae7-121">Установка приемника WebHook</span><span class="sxs-lookup"><span data-stu-id="12ae7-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="12ae7-122">Для получения WebHooks с помощью Microsoft ASP.NET WebHooks сначала вы установите пакет Nuget для поставщика WebHook или поставщиков, от которые вы хотите получить WebHooks.</span><span class="sxs-lookup"><span data-stu-id="12ae7-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="12ae7-123">Пакеты Nuget называются [Microsoft.AspNet.WebHooks.Receivers.'](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) где последняя часть указывает на поддержку службы.</span><span class="sxs-lookup"><span data-stu-id="12ae7-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="12ae7-124">Например.</span><span class="sxs-lookup"><span data-stu-id="12ae7-124">For example</span></span>

<span data-ttu-id="12ae7-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) предоставляет поддержку для получения WebHooks от GitHub и [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) обеспечивает поддержку для приема WebHooks, генерируемых ASP.NET WebHooks.</span><span class="sxs-lookup"><span data-stu-id="12ae7-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="12ae7-126">Из коробки вы можете найти поддержку Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello и WordPress, но можно поддерживать любое количество других провайдеров.</span><span class="sxs-lookup"><span data-stu-id="12ae7-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="12ae7-127">Настройка приемника WebHook</span><span class="sxs-lookup"><span data-stu-id="12ae7-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="12ae7-128">Приемники WebHook настраиваются через inteface [IWebHookReceiverConfig,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) и конкретные реализации этого интерфейса могут быть зарегистрированы с помощью любой модели впрыска зависимостей.</span><span class="sxs-lookup"><span data-stu-id="12ae7-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="12ae7-129">Реализация по умолчанию использует настройки приложений, которые могут быть установлены в файле Web.config, либо, при использовании Web Apps Azure, могут быть установлены через [портал Azure.](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="12ae7-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Параметры приложения Azure](_static/AzureAppSettings.png)

<span data-ttu-id="12ae7-131">Формат для ключей настройки приложения:</span><span class="sxs-lookup"><span data-stu-id="12ae7-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="12ae7-132">Значение представляет собой разделенный на запятую список значений, соответствующих значениям *,id,* для которых были зарегистрированы WebHooks, например:</span><span class="sxs-lookup"><span data-stu-id="12ae7-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="12ae7-133">Инициализация приемника WebHook</span><span class="sxs-lookup"><span data-stu-id="12ae7-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="12ae7-134">Приемники WebHook инициализированы путем их регистрации, как правило, в статическом классе *WebApiConfig,* например:</span><span class="sxs-lookup"><span data-stu-id="12ae7-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
