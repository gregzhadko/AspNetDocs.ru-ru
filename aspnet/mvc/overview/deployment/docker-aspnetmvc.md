---
uid: mvc/overview/deployment/docker
title: Перенос приложений ASP.NET MVC в контейнеры Windows
description: Узнайте, как запустить существующее приложение ASP.NET MVC в контейнере Windows Docker
keywords: Контейнеры Windows, Docker, ASP. NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: ef184f4256c20e2a66de8fd2d4f8e67f07d9a086
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471552"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>Перенос приложений ASP.NET MVC в контейнеры Windows

При запуске существующего приложения на основе .NET Framework в контейнере Windows не требуется вносить изменения в приложение. Чтобы запустить приложение в контейнере Windows, создайте образ Docker с приложением и запустите контейнер. В этом разделе показано, как получить существующее [приложение ASP.NET MVC](http://www.asp.net/mvc) и развернуть его в контейнере Windows.

Начните с существующего приложения ASP.NET MVC и выполните сборку опубликованных ресурсов с помощью Visual Studio. Docker используется для создания образа, который содержит и запускает ваше приложение. Вы перейдете на сайт, запущенный в контейнере Windows, и проверите, работает ли приложение.

Для работы с этой статьей необходимо знание основных понятий Docker. Чтобы ознакомиться с Docker, см. этот [обзор Docker](https://docs.docker.com/engine/understanding-docker/).

Приложение, которое будет работать в контейнере — это простой веб-сайт, который случайным образом отвечает на вопросы. Это базовое приложение MVC без проверки подлинности и хранилища базы данных. Оно позволяет сосредоточиться на перемещении веб-уровня в контейнер. В дальнейших темах показано, как перемещать постоянное хранилище и управлять им в контейнерных приложениях.

Перемещение приложения состоит из следующих действий.

1. [Создание задачи публикации для сборки ресурсов образа](#publish-script).
1. [Создание образа Docker, в котором будет запускаться приложение](#build-the-image).
1. [Запуск контейнера Docker, в котором будет запускаться образ](#start-a-container).
1. [Проверка приложения с помощью браузера](#verify-in-the-browser).

[Готовое приложение](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) находится на GitHub.

## <a name="prerequisites"></a>предварительные требования

На компьютере разработчика должно быть установлено следующее программное обеспечение:

- [Юбилейное обновление Windows 10](https://www.microsoft.com/software-download/windows10/) (или более поздняя версия) или [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (или более поздней версии)
- [Docker для Windows](https://docs.docker.com/docker-for-windows/) — версия Stable 1.13.0 или 1.12 Beta 26 (или более поздние)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> При использовании Windows Server 2016 выполните инструкции по [развертыванию узла контейнеров в Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).

После установки и запуска Docker щелкните правой кнопкой мыши значок в области уведомлений и выберите **Switch to Windows containers** (Переключиться на контейнеры Windows). Это необходимо для запуска образов Docker на базе Windows. На выполнение этой команды требуется несколько секунд:

![Контейнер Windows][windows-container]

## <a name="publish-script"></a>Публикация скрипта

Соберите в одном месте все ресурсы, которые нужно загрузить в образ Docker. Для создания профиля публикации приложения в Visual Studio есть команда **Опубликовать**. В этом профиле все ресурсы будут собраны в одном дереве каталогов, которое далее в этом учебнике вам нужно будет скопировать в свой целевой образ.

**Этапы публикации**

1. Щелкните правой кнопкой мыши веб-проект в Visual Studio и выберите **Publish** (Публикация).
1. Нажмите кнопку **Пользовательский профиль**, а затем выберите **Файловая система** в качестве метода.
1. Выберите каталог. По правилам загруженный образец использует `bin\Release\PublishOutput`.

![Публикация: подключение][publish-connection]

Откройте раздел **Параметры публикации файла** на вкладке **Параметры** . Выберите **Предварительная компиляция во время публикации**. Эта оптимизация означает, что представления не будут компилироваться в контейнере Docker, вместо этого будут копироваться предварительно скомпилированные представления.

![Публикация: параметры][publish-settings]

Нажмите кнопку **Publish** (Публикация), и Visual Studio скопирует все необходимые ресурсы в целевую папку.

## <a name="build-the-image"></a>Создание образа

Создайте новый файл с именем *Dockerfile* , чтобы определить образ DOCKER. *Dockerfile* содержит инструкции по созданию окончательного образа и включает все базовые имена образов, необходимые компоненты, приложение, которое требуется запустить, и другие образы конфигурации. *Dockerfile* — это входные данные для команды `docker build`, которая создает образ.

В этом упражнении будет построен образ на основе образа `microsoft/aspnet`, расположенного в [DOCKER Hub](https://hub.docker.com/r/microsoft/aspnet/).
Базовый образ `microsoft/aspnet` — это образ Windows Server. Он содержит Windows Server Core, IIS и ASP.NET 4.7.2. При запуске этого образа в контейнере он автоматически использует IIS и установленные веб-сайты.

Dockerfile, который создает образ, выглядит следующим образом:

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

В этом файле Dockerfile нет команды `ENTRYPOINT`. Она не нужна здесь. При использовании Windows Server с IIS процесс IIS — это точка входа, которая настроена для запуска в базовом образе ASPNET.

Выполните команду сборки Docker, чтобы создать образ, который запускает приложение ASP.NET. Для этого откройте окно PowerShell в каталоге проекта и введите следующую команду в каталог решения:

```console
docker build -t mvcrandomanswers .
```

Эта команда создает новый образ, следуя инструкциям в Dockerfile, именование (-t тегирования) образа как мвкрандомансверс. Это может включать получение базового образа из [Docker Hub](http://hub.docker.com). После этого в образ будет добавлено приложение.

После выполнения этой команды можно выполнить команду `docker images` для просмотра сведений о новом образе:

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

Идентификатор IMAGE ID на вашем компьютере будет другим. Теперь запустим приложение.

## <a name="start-a-container"></a>Запуск контейнера

Чтобы запустить контейнер, нужно выполнить следующую команду `docker run`:

```console
docker run -d --name randomanswers mvcrandomanswers
```

Аргумент `-d` предписывает Docker запустить образ в отсоединенном режиме. Это значит, что образ Docker запускается в отрыве от текущей оболочки.

Во многих примерах DOCKER вы можете увидеть-p, чтобы отобразить контейнер и порты узлов. В образе ASPNET по умолчанию уже настроен контейнер для прослушивания порта 80 и его предоставление.

Аргумент `--name randomanswers` содержит имя запущенного контейнера. Это имя можно использовать вместо идентификатора контейнера в большинстве команд.

`mvcrandomanswers` — это имя запускаемого образа.

## <a name="verify-in-the-browser"></a>Проверка в браузере

После запуска контейнера подключитесь к выполняющемуся контейнеру, используя `http://localhost` в приведенном примере. Введите этот URL-адрес в адресной строке браузера, и вы увидите работающий сайт.

> [!NOTE]
> Некоторые программы VPN или прокси-серверы могут препятствовать переходу на ваш узел.
> Их можно временно отключить, чтобы убедиться, что контейнер работает.

Каталог образцов на GitHub содержит [Сценарий PowerShell](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1), который выполняет эти команды за вас. Откройте окно PowerShell, перейдите в каталог решения и введите команду:

```console
./run.ps1
```

Приведенная выше команда создает образ, отображает список образов на компьютере и запускает контейнер.

Чтобы остановить контейнер, выполните команду `docker stop`:

```console
docker stop randomanswers
```

Чтобы удалить контейнер, выполните команду `docker rm`:

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Переключение на контейнер Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Публикация в файловой системе"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Публикация: параметры"
