---
uid: mvc/overview/deployment/docker-aspnetmvc
title: Перенос приложений ASP.NET MVC в контейнеры Windows
description: Узнайте, как запустить существующее приложение ASP.NET MVC в контейнере Windows Docker
keywords: Контейнеры для Windows,Докер,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675184"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="f042f-104">Перенос приложений ASP.NET MVC в контейнеры Windows</span><span class="sxs-lookup"><span data-stu-id="f042f-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="f042f-105">При запуске существующего приложения на основе .NET Framework в контейнере Windows не требуется вносить изменения в приложение.</span><span class="sxs-lookup"><span data-stu-id="f042f-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="f042f-106">Чтобы запустить приложение в контейнере Windows, создайте образ Docker с приложением и запустите контейнер.</span><span class="sxs-lookup"><span data-stu-id="f042f-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="f042f-107">В этом разделе показано, как получить существующее [приложение ASP.NET MVC](http://www.asp.net/mvc) и развернуть его в контейнере Windows.</span><span class="sxs-lookup"><span data-stu-id="f042f-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="f042f-108">Начните с существующего приложения ASP.NET MVC и выполните сборку опубликованных ресурсов с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f042f-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="f042f-109">Docker используется для создания образа, который содержит и запускает ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="f042f-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="f042f-110">Вы перейдете на сайт, запущенный в контейнере Windows, и проверите, работает ли приложение.</span><span class="sxs-lookup"><span data-stu-id="f042f-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="f042f-111">Для работы с этой статьей необходимо знание основных понятий Docker.</span><span class="sxs-lookup"><span data-stu-id="f042f-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="f042f-112">Чтобы ознакомиться с Docker, см. этот [обзор Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="f042f-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="f042f-113">Приложение, которое будет работать в контейнере — это простой веб-сайт, который случайным образом отвечает на вопросы.</span><span class="sxs-lookup"><span data-stu-id="f042f-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="f042f-114">Это базовое приложение MVC без проверки подлинности и хранилища базы данных. Оно позволяет сосредоточиться на перемещении веб-уровня в контейнер.</span><span class="sxs-lookup"><span data-stu-id="f042f-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="f042f-115">В дальнейших темах показано, как перемещать постоянное хранилище и управлять им в контейнерных приложениях.</span><span class="sxs-lookup"><span data-stu-id="f042f-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="f042f-116">Перемещение приложения состоит из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="f042f-116">Moving your application involves these steps:</span></span>

1. <span data-ttu-id="f042f-117">[Создание задачи публикации для сборки ресурсов образа](#publish-script).</span><span class="sxs-lookup"><span data-stu-id="f042f-117">[Creating a publish task to build the assets for an image.](#publish-script)</span></span>
1. <span data-ttu-id="f042f-118">[Создание образа Docker, в котором будет запускаться приложение](#build-the-image).</span><span class="sxs-lookup"><span data-stu-id="f042f-118">[Building a Docker image that will run your application.](#build-the-image)</span></span>
1. <span data-ttu-id="f042f-119">[Запуск контейнера Docker, в котором будет запускаться образ](#start-a-container).</span><span class="sxs-lookup"><span data-stu-id="f042f-119">[Starting a Docker container that runs your image.](#start-a-container)</span></span>
1. <span data-ttu-id="f042f-120">[Проверка приложения с помощью браузера](#verify-in-the-browser).</span><span class="sxs-lookup"><span data-stu-id="f042f-120">[Verifying the application using your browser.](#verify-in-the-browser)</span></span>

<span data-ttu-id="f042f-121">[Готовое приложение](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) находится на GitHub.</span><span class="sxs-lookup"><span data-stu-id="f042f-121">The [finished application](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f042f-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f042f-122">Prerequisites</span></span>

<span data-ttu-id="f042f-123">Машина разработки должна иметь следующее программное обеспечение:</span><span class="sxs-lookup"><span data-stu-id="f042f-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="f042f-124">[Обновление windows 10 Anniversary](https://www.microsoft.com/software-download/windows10/) (или выше) или [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (или выше)</span><span class="sxs-lookup"><span data-stu-id="f042f-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="f042f-125">[Docker для Windows](https://docs.docker.com/docker-for-windows/) — версия Stable 1.13.0 или 1.12 Beta 26 (или более поздние)</span><span class="sxs-lookup"><span data-stu-id="f042f-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="f042f-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f042f-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="f042f-127">При использовании Windows Server 2016 выполните инструкции по [развертыванию узла контейнеров в Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span><span class="sxs-lookup"><span data-stu-id="f042f-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="f042f-128">После установки и запуска Docker щелкните правой кнопкой мыши значок в области уведомлений и выберите **Switch to Windows containers** (Переключиться на контейнеры Windows).</span><span class="sxs-lookup"><span data-stu-id="f042f-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="f042f-129">Это необходимо для запуска образов Docker на базе Windows.</span><span class="sxs-lookup"><span data-stu-id="f042f-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="f042f-130">На выполнение этой команды требуется несколько секунд:</span><span class="sxs-lookup"><span data-stu-id="f042f-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="f042f-131">![Контейнер Windows][windows-container]</span><span class="sxs-lookup"><span data-stu-id="f042f-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="f042f-132">Публикация скрипта</span><span class="sxs-lookup"><span data-stu-id="f042f-132">Publish script</span></span>

<span data-ttu-id="f042f-133">Соберите в одном месте все ресурсы, которые нужно загрузить в образ Docker.</span><span class="sxs-lookup"><span data-stu-id="f042f-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="f042f-134">Для создания профиля публикации приложения в Visual Studio есть команда **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="f042f-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="f042f-135">В этом профиле все ресурсы будут собраны в одном дереве каталогов, которое далее в этом учебнике вам нужно будет скопировать в свой целевой образ.</span><span class="sxs-lookup"><span data-stu-id="f042f-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="f042f-136">**Этапы публикации**</span><span class="sxs-lookup"><span data-stu-id="f042f-136">**Publish Steps**</span></span>

1. <span data-ttu-id="f042f-137">Щелкните правой кнопкой мыши веб-проект в Visual Studio и выберите **Publish** (Публикация).</span><span class="sxs-lookup"><span data-stu-id="f042f-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="f042f-138">Нажмите **кнопку пользовательский профиль,** а затем выберите **файловую систему** в качестве метода.</span><span class="sxs-lookup"><span data-stu-id="f042f-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="f042f-139">Выберите каталог.</span><span class="sxs-lookup"><span data-stu-id="f042f-139">Choose the directory.</span></span> <span data-ttu-id="f042f-140">По правилам загруженный образец использует `bin\Release\PublishOutput`.</span><span class="sxs-lookup"><span data-stu-id="f042f-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="f042f-141">![Публикация: подключение][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="f042f-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="f042f-142">Откройте раздел **Параметры публикации файлов** **вкладки «Настройки.** Выберите **precompile во время публикации**.</span><span class="sxs-lookup"><span data-stu-id="f042f-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="f042f-143">Эта оптимизация означает, что представления не будут компилироваться в контейнере Docker, вместо этого будут копироваться предварительно скомпилированные представления.</span><span class="sxs-lookup"><span data-stu-id="f042f-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="f042f-144">![Настройки публикации][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="f042f-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="f042f-145">Нажмите кнопку **Publish** (Публикация), и Visual Studio скопирует все необходимые ресурсы в целевую папку.</span><span class="sxs-lookup"><span data-stu-id="f042f-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="f042f-146">Создание образа</span><span class="sxs-lookup"><span data-stu-id="f042f-146">Build the image</span></span>

<span data-ttu-id="f042f-147">Создайте новый файл под названием *Dockerfile* для определения изображения Docker.</span><span class="sxs-lookup"><span data-stu-id="f042f-147">Create a new file named *Dockerfile* to define your Docker image.</span></span> <span data-ttu-id="f042f-148">*Dockerfile* содержит инструкции по созданию окончательного изображения и включает в себя любые имена базовых изображений, необходимые компоненты, приложение, которым вы хотите запускать, и другие изображения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f042f-148">*Dockerfile* contains instructions to build the final image and includes any base image names, required components, the app you want to run, and other configuration images.</span></span> <span data-ttu-id="f042f-149">*Dockerfile* — это вход `docker build` в команду, создающий изображение.</span><span class="sxs-lookup"><span data-stu-id="f042f-149">*Dockerfile* is the input to the `docker build` command that creates the image.</span></span>

<span data-ttu-id="f042f-150">Для этого упражнения вы создаме `microsoft/aspnet` изображение на основе изображения, расположенного на [Docker Hub.](https://hub.docker.com/r/microsoft/aspnet/)</span><span class="sxs-lookup"><span data-stu-id="f042f-150">For this exercise, you will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="f042f-151">Базовый образ `microsoft/aspnet` — это образ Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f042f-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="f042f-152">Он содержит ядро сервера Windows, IIS и ASP.NET 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="f042f-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="f042f-153">При запуске этого образа в контейнере он автоматически использует IIS и установленные веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="f042f-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="f042f-154">Dockerfile, который создает образ, выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f042f-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="f042f-155">В этом файле Dockerfile нет команды `ENTRYPOINT`.</span><span class="sxs-lookup"><span data-stu-id="f042f-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="f042f-156">Она не нужна здесь.</span><span class="sxs-lookup"><span data-stu-id="f042f-156">You don't need one.</span></span> <span data-ttu-id="f042f-157">При запуске Windows Server с IIS процесс IIS является точкой входа, которая настроена для запуска в базовом изображении aspnet.</span><span class="sxs-lookup"><span data-stu-id="f042f-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="f042f-158">Выполните команду сборки Docker, чтобы создать образ, который запускает приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f042f-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="f042f-159">Для этого откройте окно PowerShell в каталоге проекта и введите следующую команду в каталоге решений:</span><span class="sxs-lookup"><span data-stu-id="f042f-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="f042f-160">Эта команда будет строить новое изображение, используя инструкции в Dockerfile, называя (т пометки) изображение как mvcrandomanswers.</span><span class="sxs-lookup"><span data-stu-id="f042f-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="f042f-161">Это может включать получение базового образа из [Docker Hub](http://hub.docker.com). После этого в образ будет добавлено приложение.</span><span class="sxs-lookup"><span data-stu-id="f042f-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="f042f-162">После выполнения этой команды можно выполнить команду `docker images` для просмотра сведений о новом образе:</span><span class="sxs-lookup"><span data-stu-id="f042f-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="f042f-163">Идентификатор IMAGE ID на вашем компьютере будет другим.</span><span class="sxs-lookup"><span data-stu-id="f042f-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="f042f-164">Теперь запустим приложение.</span><span class="sxs-lookup"><span data-stu-id="f042f-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="f042f-165">Запуск контейнера</span><span class="sxs-lookup"><span data-stu-id="f042f-165">Start a container</span></span>

<span data-ttu-id="f042f-166">Чтобы запустить контейнер, нужно выполнить следующую команду `docker run`:</span><span class="sxs-lookup"><span data-stu-id="f042f-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="f042f-167">Аргумент `-d` предписывает Docker запустить образ в отсоединенном режиме.</span><span class="sxs-lookup"><span data-stu-id="f042f-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="f042f-168">Это значит, что образ Docker запускается в отрыве от текущей оболочки.</span><span class="sxs-lookup"><span data-stu-id="f042f-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="f042f-169">Во многих примерах докеров можно увидеть -p для картирования контейнеров и портов-хостелей.</span><span class="sxs-lookup"><span data-stu-id="f042f-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="f042f-170">Изображение aspnet по умолчанию уже настроило контейнер для прослушивания на порту 80 и его обнажения.</span><span class="sxs-lookup"><span data-stu-id="f042f-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="f042f-171">Аргумент `--name randomanswers` содержит имя запущенного контейнера.</span><span class="sxs-lookup"><span data-stu-id="f042f-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="f042f-172">Это имя можно использовать вместо идентификатора контейнера в большинстве команд.</span><span class="sxs-lookup"><span data-stu-id="f042f-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="f042f-173">`mvcrandomanswers` — это имя запускаемого образа.</span><span class="sxs-lookup"><span data-stu-id="f042f-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="f042f-174">Проверка в браузере</span><span class="sxs-lookup"><span data-stu-id="f042f-174">Verify in the browser</span></span>

<span data-ttu-id="f042f-175">Как только контейнер запускается, подключитесь к бегущей таре, используя `http://localhost` в приведенном примере.</span><span class="sxs-lookup"><span data-stu-id="f042f-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="f042f-176">Введите этот URL-адрес в адресной строке браузера, и вы увидите работающий сайт.</span><span class="sxs-lookup"><span data-stu-id="f042f-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="f042f-177">Некоторые программы VPN или прокси-серверы могут препятствовать переходу на ваш узел.</span><span class="sxs-lookup"><span data-stu-id="f042f-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="f042f-178">Их можно временно отключить, чтобы убедиться, что контейнер работает.</span><span class="sxs-lookup"><span data-stu-id="f042f-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="f042f-179">Каталог образцов на GitHub содержит [Сценарий PowerShell](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1), который выполняет эти команды за вас.</span><span class="sxs-lookup"><span data-stu-id="f042f-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="f042f-180">Откройте окно PowerShell, перейдите в каталог решения и введите команду:</span><span class="sxs-lookup"><span data-stu-id="f042f-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="f042f-181">Команда выше строит изображение, отображает список изображений на вашей машине, и запускает контейнер.</span><span class="sxs-lookup"><span data-stu-id="f042f-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="f042f-182">Чтобы остановить контейнер, выполните команду `docker stop`:</span><span class="sxs-lookup"><span data-stu-id="f042f-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="f042f-183">Чтобы удалить контейнер, выполните команду `docker rm`:</span><span class="sxs-lookup"><span data-stu-id="f042f-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Переключение на контейнер Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Публикация в файловой системе"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Настройки публикации"
