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
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="62a74-103">отладка WebHooks ASP.NET</span><span class="sxs-lookup"><span data-stu-id="62a74-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="62a74-104">Отладка в Azure</span><span class="sxs-lookup"><span data-stu-id="62a74-104">Debugging in Azure</span></span>

<span data-ttu-id="62a74-105">Чтобы отладить веб-приложение во время работы в Azure, пожалуйста, смотрите учебник [Troubleshoot веб-приложение в Azure App Service с помощью Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="62a74-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="62a74-106">Отладка с источником и символами</span><span class="sxs-lookup"><span data-stu-id="62a74-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="62a74-107">В дополнение к отладке собственного кода, можно отладить непосредственно в Microsoft ASP.NET WebHooks, а на самом деле все .NET.</span><span class="sxs-lookup"><span data-stu-id="62a74-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="62a74-108">Это работает независимо от того, отлажоните локально или удаленно.</span><span class="sxs-lookup"><span data-stu-id="62a74-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="62a74-109">Во-первых, настроить Visual Studio, чтобы найти источник и символы, перейдя к **Отуга,** а затем **параметры и настройки.**</span><span class="sxs-lookup"><span data-stu-id="62a74-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="62a74-110">Установите параметры следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62a74-110">Set the options like this:</span></span>

![Параметры и настройки](_static/SourceSymbols.png)

<span data-ttu-id="62a74-112">Затем добавьте ссылку на [symbolsource.org](http://symbolsource.org) для загрузки источника и символов.</span><span class="sxs-lookup"><span data-stu-id="62a74-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="62a74-113">Перейдите на вкладку **Символы** меню выше и добавьте следующее в качестве символа местоположения:</span><span class="sxs-lookup"><span data-stu-id="62a74-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="62a74-114">Кроме того, убедитесь, что каталог кэша имеет короткое имя; в противном случае имена файлов могут получить слишком долго, что приведет к символам, чтобы не загружаться.</span><span class="sxs-lookup"><span data-stu-id="62a74-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="62a74-115">Путь образца:</span><span class="sxs-lookup"><span data-stu-id="62a74-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="62a74-116">Настройки должны выглядеть так же, как это:</span><span class="sxs-lookup"><span data-stu-id="62a74-116">The settings should look similar to this:</span></span>

![Пример расположения файла символа опций](_static/SymSource.png)
