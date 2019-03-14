---
title: Средства и файлы для загрузки — DevOps с помощью ASP.NET Core и Azure
author: CamSoper
description: Средства и файлы, необходимые для разработки и операций с ASP.NET Core и Azure.
ms.author: casoper
ms.custom: mvc, seodec18
ms.date: 10/24/2018
uid: azure/devops/tools-and-downloads
ms.openlocfilehash: 0c64e723f1b912323103f201a66c1edaeccdcc2d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026191"
---
# <a name="tools-and-downloads"></a><span data-ttu-id="fe7f1-103">Средства и файлы для загрузки</span><span class="sxs-lookup"><span data-stu-id="fe7f1-103">Tools and downloads</span></span>

<span data-ttu-id="fe7f1-104">Azure имеет несколько интерфейсов для подготовки и управления ресурсами, такими как [портала Azure](https://portal.azure.com), [Azure CLI](/cli/azure/), [Azure PowerShell](/powershell/azure/overview), [облако Azure Оболочка](https://shell.azure.com/bash)и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-104">Azure has several interfaces for provisioning and managing resources, such as the [Azure portal](https://portal.azure.com), [Azure CLI](/cli/azure/), [Azure PowerShell](/powershell/azure/overview), [Azure Cloud Shell](https://shell.azure.com/bash), and Visual Studio.</span></span> <span data-ttu-id="fe7f1-105">В этом руководстве принимает минималистский подход и использует Azure Cloud Shell, чтобы уменьшить шаги.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-105">This guide takes a minimalist approach and uses the Azure Cloud Shell whenever possible to reduce the steps required.</span></span> <span data-ttu-id="fe7f1-106">Тем не менее портала Azure необходимо использовать для некоторых частей.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-106">However, the Azure portal must be used for some portions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe7f1-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe7f1-107">Prerequisites</span></span>

<span data-ttu-id="fe7f1-108">Необходимы следующие подписки:</span><span class="sxs-lookup"><span data-stu-id="fe7f1-108">The following subscriptions are required:</span></span>

* <span data-ttu-id="fe7f1-109">Azure &mdash; Если у вас нет учетной записи, [получить бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fe7f1-109">Azure &mdash; If you don't have an account, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="fe7f1-110">Службы Azure DevOps &mdash; ваша подписка Azure DevOps и организации создается в главе 4.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-110">Azure DevOps Services &mdash; your Azure DevOps subscription and organization is created in Chapter 4.</span></span>
* <span data-ttu-id="fe7f1-111">GitHub &mdash; Если у вас нет учетной записи, [Подпишитесь на бесплатную версию](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="fe7f1-111">GitHub &mdash; If you don't have an account, [sign up for free](https://github.com/join).</span></span>

<span data-ttu-id="fe7f1-112">Требуются следующие средства:</span><span class="sxs-lookup"><span data-stu-id="fe7f1-112">The following tools are required:</span></span>

* <span data-ttu-id="fe7f1-113">[Git](https://git-scm.com/downloads) &mdash; основные сведения об Git рекомендуется использовать в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-113">[Git](https://git-scm.com/downloads) &mdash; A fundamental understanding of Git is recommended for this guide.</span></span> <span data-ttu-id="fe7f1-114">Просмотрите [документации по Git](https://git-scm.com/doc), в частности [удаленный репозиторий git](https://git-scm.com/docs/git-remote) и [отправку](https://git-scm.com/docs/git-push).</span><span class="sxs-lookup"><span data-stu-id="fe7f1-114">Review the [Git documentation](https://git-scm.com/doc), specifically [git remote](https://git-scm.com/docs/git-remote) and [git push](https://git-scm.com/docs/git-push).</span></span>
* <span data-ttu-id="fe7f1-115">[Пакет SDK для .NET core](https://www.microsoft.com/net/download/) &mdash; версии 2.1.300 или более поздней версии необходим для построения и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-115">[.NET Core SDK](https://www.microsoft.com/net/download/) &mdash; Version 2.1.300 or later is required to build and run the sample app.</span></span> <span data-ttu-id="fe7f1-116">Если Visual Studio устанавливается вместе с **кросс Платформенная разработка .NET Core** уже установлена рабочая нагрузка, пакет SDK для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-116">If Visual Studio is installed with the **.NET Core cross-platform development** workload, the .NET Core SDK is already installed.</span></span>

    <span data-ttu-id="fe7f1-117">Проверьте правильность установки пакета SDK для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-117">Verify your .NET Core SDK installation.</span></span> <span data-ttu-id="fe7f1-118">Откройте командную строку и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fe7f1-118">Open a command shell, and run the following command:</span></span>

    ```console
    dotnet --version
    ```

## <a name="recommended-tools-windows-only"></a><span data-ttu-id="fe7f1-119">Рекомендуемые средства (только Windows)</span><span class="sxs-lookup"><span data-stu-id="fe7f1-119">Recommended tools (Windows only)</span></span>

* <span data-ttu-id="fe7f1-120">[Visual Studio](https://www.visualstudio.com/)в надежные средства Azure предоставляют графический интерфейс пользователя для большинства функций, описанных в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-120">[Visual Studio](https://www.visualstudio.com/)'s robust Azure tools provide a GUI for most of the functionality described in this guide.</span></span> <span data-ttu-id="fe7f1-121">Подойдет любой выпуск Visual Studio, включая бесплатный выпуск Visual Studio Community.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-121">Any edition of Visual Studio will work, including the free Visual Studio Community Edition.</span></span> <span data-ttu-id="fe7f1-122">Учебники, записываются для демонстрации разработки, развертывания и инструменты DevOps с и без Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe7f1-122">The tutorials are written to demonstrate development, deployment, and DevOps both with and without Visual Studio.</span></span>

  <span data-ttu-id="fe7f1-123">Убедитесь, что Visual Studio имеет следующие [рабочих нагрузок](/visualstudio/install/modify-visual-studio) установлен:</span><span class="sxs-lookup"><span data-stu-id="fe7f1-123">Confirm that Visual Studio has the following [workloads](/visualstudio/install/modify-visual-studio) installed:</span></span>

  * <span data-ttu-id="fe7f1-124">ASP.NET и веб-разработка</span><span class="sxs-lookup"><span data-stu-id="fe7f1-124">ASP.NET and web development</span></span>
  * <span data-ttu-id="fe7f1-125">Разработка для Azure</span><span class="sxs-lookup"><span data-stu-id="fe7f1-125">Azure development</span></span>
  * <span data-ttu-id="fe7f1-126">Кроссплатформенная разработка .NET Core</span><span class="sxs-lookup"><span data-stu-id="fe7f1-126">.NET Core cross-platform development</span></span>
