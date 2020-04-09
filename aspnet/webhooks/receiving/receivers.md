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
# <a name="aspnet-webhooks-receivers"></a>ASP.NET приемники WebHooks

Получение WebHooks зависит от того, кто является отправителем. Иногда есть дополнительные шаги регистрации WebHook проверки того, что абонент действительно слушает. Некоторые WebHooks предоставляют модель push-to-pull, где запрос HTTP POST содержит только ссылку на информацию о событии, которая затем должна быть извлечена независимо. Часто модель безопасности меняется довольно много.

Цель Microsoft ASP.NET WebHooks — сделать ее проще и последовательнее, чтобы подключить ваш API, не тратя много времени на выяснение того, как обрабатывать какой-либо конкретный вариант WebHooks.

Приемник WebHook отвечает за прием и проверку WebHooks от конкретного отправителя. Приемник WebHook может поддерживать любое количество WebHooks, каждый со своей собственной конфигурацией. Например, приемник GitHub WebHook может принимать WebHooks из любого количества репозиториев GitHub.

## <a name="webhook-receiver-uris"></a>Webhook приемник URIs

Установив Microsoft ASP.NET WebHooks, вы получаете общий контроллер WebHook, который принимает запросы WebHook от открытого количества служб. Когда запрос поступает, он выбирает подходящий приемник, который вы установили для обработки конкретного отправителя WebHook.

URI этого контроллера webHook URI, который вы регистрируете в службе и имеет форму:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

По соображениям безопасности многие приемники WebHook требуют, чтобы URI является *https* URI, а в некоторых случаях он должен также содержать дополнительный параметр запроса, который используется для обеспечения того, чтобы только предназначенная сторона может отправлять WebHooks в URI выше.

Компонент `<receiver>` является имя приемника, например, `github` или `slack`.

*«Id»* — это дополнительный идентификатор, который может быть использован для определения конкретной конфигурации приемника WebHook. Это может быть использовано для регистрации N WebHooks с определенным приемником. Например, следующие три URIs могут быть использованы для регистрации на три независимых WebHooks:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Установка приемника WebHook

Для получения WebHooks с помощью Microsoft ASP.NET WebHooks сначала вы установите пакет Nuget для поставщика WebHook или поставщиков, от которые вы хотите получить WebHooks. Пакеты Nuget называются [Microsoft.AspNet.WebHooks.Receivers.'](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) где последняя часть указывает на поддержку службы. Например.

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) предоставляет поддержку для получения WebHooks от GitHub и [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) обеспечивает поддержку для приема WebHooks, генерируемых ASP.NET WebHooks.

Из коробки вы можете найти поддержку Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello и WordPress, но можно поддерживать любое количество других провайдеров.

## <a name="configuring-a-webhook-receiver"></a>Настройка приемника WebHook

Приемники WebHook настраиваются через inteface [IWebHookReceiverConfig,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) и конкретные реализации этого интерфейса могут быть зарегистрированы с помощью любой модели впрыска зависимостей. Реализация по умолчанию использует настройки приложений, которые могут быть установлены в файле Web.config, либо, при использовании Web Apps Azure, могут быть установлены через [портал Azure.](https://portal.azure.com/)

![Параметры приложения Azure](_static/AzureAppSettings.png)

Формат для ключей настройки приложения:

```
MS_WebHookReceiverSecret_<receiver>
```

Значение представляет собой разделенный на запятую список значений, соответствующих значениям *,id,* для которых были зарегистрированы WebHooks, например:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Инициализация приемника WebHook

Приемники WebHook инициализированы путем их регистрации, как правило, в статическом классе *WebApiConfig,* например:

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
