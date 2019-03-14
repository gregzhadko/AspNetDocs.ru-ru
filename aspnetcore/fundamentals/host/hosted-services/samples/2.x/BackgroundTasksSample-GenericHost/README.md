---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056491"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="015f0-101">Пример фоновых задач в ASP.NET Core (универсальный узел)</span><span class="sxs-lookup"><span data-stu-id="015f0-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="015f0-102">В этом примере демонстрируется использование [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span><span class="sxs-lookup"><span data-stu-id="015f0-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="015f0-103">В этом примере демонстрируются функции, описанные в разделе [Фоновые задачи с размещенными службами в ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services).</span><span class="sxs-lookup"><span data-stu-id="015f0-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="015f0-104">Если этот пример запускается в [Visual Studio Code](https://code.visualstudio.com/), в файле конфигурации консоли *.vscode/launch.json* задайте для параметра **console** значение `externalTerminal` или `integratedTerminal`.</span><span class="sxs-lookup"><span data-stu-id="015f0-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="015f0-105">Значение `internalConsole` несовместимо с вводом данных в консоль через нажатие клавиш, который используется в приложении для постановки в очередь фоновых рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="015f0-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
