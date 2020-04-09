---
uid: webhooks/diagnostics/logging
title: ASP.NET журналов WebHooks (ru) Документы Майкрософт
author: rick-anderson
description: Как сделать вход в ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675347"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET журнал webHooks

Корпорация Майкрософт ASP.NET WebHooks использует журналирование как способ отчетности о проблемах и проблемах. По умолчанию журналы пишутся с помощью [System.Diagnostics.Trace,](https://msdn.microsoft.com/library/system.diagnostics.trace) где они могут быть manged с помощью [Trace Listeners,](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) как и любой другой поток журнала.

При развертывании Web-приложения в виде Web App журналы автоматически подбираются и могут управляться вместе с любой другой системой [системы.Диагностика.Trace.](https://msdn.microsoft.com/library/system.diagnostics.trace) Для получения подробной информации, пожалуйста, смотрите [Запись диагностики для веб-приложений в Службе приложений Azure](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Кроме того, журналы могут быть получены прямо изнутри Visual Studio, как описано в [Troubleshoot веб-приложение в Azure App Service с помощью Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="redirecting-logs"></a>Перенаправление журналов

Вместо того, чтобы писать журналы на [System.Diagnostics.Trace,](https://msdn.microsoft.com/library/system.diagnostics.trace)можно предоставить альтернативную реализацию журналов, которая может войти непосредственно в менеджер журнала, такой как [Log4Net](http://logging.apache.org/log4net/) и [NLog.](http://nlog-project.org/) Просто предоставьте реализацию [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) и зарегистрируйте его с движком впрыска зависимости по вашему выбору, и он будет получать взял Microsoft ASP.NET WebHooks. Подробнее о [впрыске зависимостей](https://www.asp.net/web-api/overview/advanced/dependency-injection) можно найти в ASP.NET Web API 2.
