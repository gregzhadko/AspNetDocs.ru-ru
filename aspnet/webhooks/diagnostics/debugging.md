---
uid: webhooks/diagnostics/debugging
title: отладка WebHooks ASP.NET веб-хуков (ru) Документы Майкрософт
author: rick-anderson
description: Как отладить ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675367"
---
# <a name="aspnet-webhooks-debugging"></a>отладка WebHooks ASP.NET

## <a name="debugging-in-azure"></a>Отладка в Azure

Чтобы отладить веб-приложение во время работы в Azure, пожалуйста, смотрите учебник [Troubleshoot веб-приложение в Azure App Service с помощью Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="debugging-with-source-and-symbols"></a>Отладка с источником и символами

В дополнение к отладке собственного кода, можно отладить непосредственно в Microsoft ASP.NET WebHooks, а на самом деле все .NET. Это работает независимо от того, отлажоните локально или удаленно. Во-первых, настроить Visual Studio, чтобы найти источник и символы, перейдя к **Отуга,** а затем **параметры и настройки.** Установите параметры следующим образом:

![Параметры и настройки](_static/SourceSymbols.png)

Затем добавьте ссылку на [symbolsource.org](http://symbolsource.org) для загрузки источника и символов. Перейдите на вкладку **Символы** меню выше и добавьте следующее в качестве символа местоположения:

```
http://srv.symbolsource.org/pdb/Public
```

Кроме того, убедитесь, что каталог кэша имеет короткое имя; в противном случае имена файлов могут получить слишком долго, что приведет к символам, чтобы не загружаться. Путь образца:

```
C:\SymCache
```

Настройки должны выглядеть так же, как это:

![Пример расположения файла символа опций](_static/SymSource.png)
