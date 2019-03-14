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
# <a name="tools-and-downloads"></a>Средства и файлы для загрузки

Azure имеет несколько интерфейсов для подготовки и управления ресурсами, такими как [портала Azure](https://portal.azure.com), [Azure CLI](/cli/azure/), [Azure PowerShell](/powershell/azure/overview), [облако Azure Оболочка](https://shell.azure.com/bash)и Visual Studio. В этом руководстве принимает минималистский подход и использует Azure Cloud Shell, чтобы уменьшить шаги. Тем не менее портала Azure необходимо использовать для некоторых частей.

## <a name="prerequisites"></a>Предварительные требования

Необходимы следующие подписки:

* Azure &mdash; Если у вас нет учетной записи, [получить бесплатную пробную версию](https://azure.microsoft.com/free/).
* Службы Azure DevOps &mdash; ваша подписка Azure DevOps и организации создается в главе 4.
* GitHub &mdash; Если у вас нет учетной записи, [Подпишитесь на бесплатную версию](https://github.com/join).

Требуются следующие средства:

* [Git](https://git-scm.com/downloads) &mdash; основные сведения об Git рекомендуется использовать в этом руководстве. Просмотрите [документации по Git](https://git-scm.com/doc), в частности [удаленный репозиторий git](https://git-scm.com/docs/git-remote) и [отправку](https://git-scm.com/docs/git-push).
* [Пакет SDK для .NET core](https://www.microsoft.com/net/download/) &mdash; версии 2.1.300 или более поздней версии необходим для построения и запуска примера приложения. Если Visual Studio устанавливается вместе с **кросс Платформенная разработка .NET Core** уже установлена рабочая нагрузка, пакет SDK для .NET Core.

    Проверьте правильность установки пакета SDK для .NET Core. Откройте командную строку и выполните следующую команду:

    ```console
    dotnet --version
    ```

## <a name="recommended-tools-windows-only"></a>Рекомендуемые средства (только Windows)

* [Visual Studio](https://www.visualstudio.com/)в надежные средства Azure предоставляют графический интерфейс пользователя для большинства функций, описанных в этом руководстве. Подойдет любой выпуск Visual Studio, включая бесплатный выпуск Visual Studio Community. Учебники, записываются для демонстрации разработки, развертывания и инструменты DevOps с и без Visual Studio.

  Убедитесь, что Visual Studio имеет следующие [рабочих нагрузок](/visualstudio/install/modify-visual-studio) установлен:

  * ASP.NET и веб-разработка
  * Разработка для Azure
  * Кроссплатформенная разработка .NET Core
