---
uid: webhooks/source
title: ASP.NET исходный код WebHooks и пакеты NuGet Документы Майкрософт
author: rick-anderson
description: Ссылки на исходный код ASP.NET WebHooks и пакеты NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675326"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET исходный код WebHooks и пакеты NuGet

Microsoft ASP.NET WebHooks является частью семейства модулей Microsoft ASP.NET и размещается в качестве [проекта с открытым исходным кодом на GitHub](https://github.com/aspnet/WebHooks). Это означает, что мы принимаем взносы, но, пожалуйста, посмотрите на [Рекомендации](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) по вкладу, прежде чем подавать запрос на вытягивание.

Эта онлайн-документация, которую вы читаете сейчас, также размещается как [Открытый исходный код на GitHub,](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) а также принимает взносы.

## <a name="nuget-packages"></a>Пакеты NuGet

[Пакеты NuGet разделены](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) на три части:

* [Общие](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Общий пакет, который совместно между отправителями и получателями.

* [Отправитель](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Набор пакетов, поддерживающих отправку собственных WebHooks другим пользователям. Функциональность для отправки WebHooks описана более подробно в [Отправке WebHooks](sending/senders.md).

* [Приемники](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Набор пакетов, поддерживающих получение WebHooks от других. Функциональность для получения WebHooks описана более подробно в [Receiving WebHooks](receiving/index.md).
