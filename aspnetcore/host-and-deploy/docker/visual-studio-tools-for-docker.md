---
title: Использование средств Visual Studio для Docker с ASP.NET Core
author: spboyer
description: Сведения о том, как упаковать в контейнер приложение ASP.NET Core с помощью средств Visual Studio 2017 и Docker для Windows.
ms.author: scaddie
ms.custom: mvc
ms.date: 09/12/2018
uid: host-and-deploy/docker/visual-studio-tools-for-docker
ms.openlocfilehash: 42f8071eadabba3eb8cb738be1720f4c6195808c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038771"
---
# <a name="visual-studio-tools-for-docker-with-aspnet-core"></a><span data-ttu-id="74b65-103">Использование средств Visual Studio для Docker с ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="74b65-103">Visual Studio Tools for Docker with ASP.NET Core</span></span>

<span data-ttu-id="74b65-104">Visual Studio 2017 поддерживает создание, отладку и запуск контейнерных приложений ASP.NET Core, предназначенных для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="74b65-104">Visual Studio 2017 supports building, debugging, and running containerized ASP.NET Core apps targeting .NET Core.</span></span> <span data-ttu-id="74b65-105">Поддерживаются контейнеры Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="74b65-105">Both Windows and Linux containers are supported.</span></span>

<span data-ttu-id="74b65-106">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/docker/visual-studio-tools-for-docker/samples) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="74b65-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/docker/visual-studio-tools-for-docker/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74b65-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="74b65-107">Prerequisites</span></span>

* [<span data-ttu-id="74b65-108">Docker для Windows</span><span class="sxs-lookup"><span data-stu-id="74b65-108">Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/install/)
* <span data-ttu-id="74b65-109">[Visual Studio 2017](https://www.visualstudio.com/) с рабочей нагрузкой **Кроссплатформенная разработка .NET Core**</span><span class="sxs-lookup"><span data-stu-id="74b65-109">[Visual Studio 2017](https://www.visualstudio.com/) with the **.NET Core cross-platform development** workload</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="74b65-110">Установка и настройка</span><span class="sxs-lookup"><span data-stu-id="74b65-110">Installation and setup</span></span>

<span data-ttu-id="74b65-111">Для установки Docker, сначала ознакомьтесь с разделом [Docker для Windows: что следует знать перед установкой](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install).</span><span class="sxs-lookup"><span data-stu-id="74b65-111">For Docker installation, first review the information at [Docker for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install).</span></span> <span data-ttu-id="74b65-112">Затем [установите Docker для Windows](https://docs.docker.com/docker-for-windows/install/).</span><span class="sxs-lookup"><span data-stu-id="74b65-112">Next, install [Docker For Windows](https://docs.docker.com/docker-for-windows/install/).</span></span>

<span data-ttu-id="74b65-113">Нужно настроить **[Общие диски](https://docs.docker.com/docker-for-windows/#shared-drives)** в Docker для Windows, чтобы обеспечить поддержку сопоставления тома и отладки.</span><span class="sxs-lookup"><span data-stu-id="74b65-113">**[Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)** in Docker for Windows must be configured to support volume mapping and debugging.</span></span> <span data-ttu-id="74b65-114">Щелкните правой кнопкой мыши значок Docker на панели задач и выберите пункт **Параметры**, а затем — **Общие диски**.</span><span class="sxs-lookup"><span data-stu-id="74b65-114">Right-click the System Tray's Docker icon, select **Settings**, and select **Shared Drives**.</span></span> <span data-ttu-id="74b65-115">Выберите диск, на котором Docker сохраняет файлы.</span><span class="sxs-lookup"><span data-stu-id="74b65-115">Select the drive where Docker stores files.</span></span> <span data-ttu-id="74b65-116">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="74b65-116">Click **Apply**.</span></span>

![Диалоговое окно для выбора общего локального диска C для контейнеров](visual-studio-tools-for-docker/_static/settings-shared-drives-win.png)

> [!TIP]
> <span data-ttu-id="74b65-118">Visual Studio 2017 версии 15.6 и более поздней выдает предупреждение, если **Общие диски** не настроены.</span><span class="sxs-lookup"><span data-stu-id="74b65-118">Visual Studio 2017 versions 15.6 and later prompt when **Shared Drives** aren't configured.</span></span>

## <a name="add-a-project-to-a-docker-container"></a><span data-ttu-id="74b65-119">Добавление проекта в контейнер Docker</span><span class="sxs-lookup"><span data-stu-id="74b65-119">Add a project to a Docker container</span></span>

<span data-ttu-id="74b65-120">Чтобы сделать проект ASP.NET Core контейнерным, этот проект должен быть предназначен для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="74b65-120">To containerize an ASP.NET Core project, the project must target .NET Core.</span></span> <span data-ttu-id="74b65-121">Поддерживаются как контейнеры Linux, так и контейнеры Windows.</span><span class="sxs-lookup"><span data-stu-id="74b65-121">Both Linux and Windows containers are supported.</span></span>

<span data-ttu-id="74b65-122">При добавлении в проект поддержки Docker выберите контейнер Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="74b65-122">When adding Docker support to a project, choose either a Windows or a Linux container.</span></span> <span data-ttu-id="74b65-123">Узел Docker должен работать на контейнерах такого же типа.</span><span class="sxs-lookup"><span data-stu-id="74b65-123">The Docker host must be running the same container type.</span></span> <span data-ttu-id="74b65-124">Чтобы изменить тип контейнера для работающего экземпляра Docker, щелкните правой кнопкой мыши значок Docker в области уведомлений и выберите **Переключение на контейнеры Windows** или **Переключение на контейнеры Linux**.</span><span class="sxs-lookup"><span data-stu-id="74b65-124">To change the container type in the running Docker instance, right-click the System Tray's Docker icon and choose **Switch to Windows containers...** or **Switch to Linux containers...**.</span></span>

### <a name="new-app"></a><span data-ttu-id="74b65-125">Новое приложение</span><span class="sxs-lookup"><span data-stu-id="74b65-125">New app</span></span>

<span data-ttu-id="74b65-126">При создании приложения с помощью шаблонов проектов **веб-приложения ASP.NET Core** установите флажок **Включение поддержки Docker**:</span><span class="sxs-lookup"><span data-stu-id="74b65-126">When creating a new app with the **ASP.NET Core Web Application** project templates, select the **Enable Docker Support** check box:</span></span>

![Флажок "Включение поддержки Docker"](visual-studio-tools-for-docker/_static/enable-docker-support-check-box.png)

<span data-ttu-id="74b65-128">Если целевой платформой является .NET Core, в раскрывающемся списке **ОС** можно выбрать тип контейнера.</span><span class="sxs-lookup"><span data-stu-id="74b65-128">If the target framework is .NET Core, the **OS** drop-down allows for the selection of a container type.</span></span>

### <a name="existing-app"></a><span data-ttu-id="74b65-129">Существующее приложение</span><span class="sxs-lookup"><span data-stu-id="74b65-129">Existing app</span></span>

<span data-ttu-id="74b65-130">Для проектов ASP.NET Core, ориентированных на .NET Core, добавить поддержку Docker через средства можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="74b65-130">For ASP.NET Core projects targeting .NET Core, there are two options for adding Docker support via the tooling.</span></span> <span data-ttu-id="74b65-131">Откройте проект в Visual Studio и выберите один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="74b65-131">Open the project in Visual Studio, and choose one of the following options:</span></span>

* <span data-ttu-id="74b65-132">Выберите пункт **Поддержка Docker** в меню **Проект**.</span><span class="sxs-lookup"><span data-stu-id="74b65-132">Select **Docker Support** from the **Project** menu.</span></span>
* <span data-ttu-id="74b65-133">В **Обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Поддержка Docker**.</span><span class="sxs-lookup"><span data-stu-id="74b65-133">Right-click the project in **Solution Explorer** and select **Add** > **Docker Support**.</span></span>

<span data-ttu-id="74b65-134">Средства Visual Studio для Docker не поддерживают добавление Docker в существующий проект ASP.NET Core, ориентированный на .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="74b65-134">The Visual Studio Tools for Docker don't support adding Docker to an existing ASP.NET Core project targeting .NET Framework.</span></span>

## <a name="dockerfile-overview"></a><span data-ttu-id="74b65-135">Общие сведения о Dockerfile</span><span class="sxs-lookup"><span data-stu-id="74b65-135">Dockerfile overview</span></span>

<span data-ttu-id="74b65-136">*Dockerfile* с инструкциями по созданию окончательного образа Docker добавляется в корень проекта.</span><span class="sxs-lookup"><span data-stu-id="74b65-136">A *Dockerfile*, the recipe for creating a final Docker image, is added to the project root.</span></span> <span data-ttu-id="74b65-137">См. [справочник по Dockerfile](https://docs.docker.com/engine/reference/builder/) для получения сведений о других доступных в нем командах.</span><span class="sxs-lookup"><span data-stu-id="74b65-137">Refer to [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for an understanding of the commands within it.</span></span> <span data-ttu-id="74b65-138">Этот конкретный *Dockerfile* использует [многоэтапную сборку](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) из четырех раздельных именованных этапов:</span><span class="sxs-lookup"><span data-stu-id="74b65-138">This particular *Dockerfile* uses a [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) with four distinct, named build stages:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-dockerfile[](visual-studio-tools-for-docker/samples/2.1/HelloDockerTools/Dockerfile.original?highlight=1,6,14,17)]

<span data-ttu-id="74b65-139">Предыдущий *Dockerfile* основан на образе [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="74b65-139">The preceding *Dockerfile* is based on the [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/) image.</span></span> <span data-ttu-id="74b65-140">Этот базовый образ содержит среду выполнения ASP.NET Core и пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="74b65-140">This base image includes the ASP.NET Core runtime and NuGet packages.</span></span> <span data-ttu-id="74b65-141">Пакеты скомпилированы JIT-компилятором для повышения производительности запуска.</span><span class="sxs-lookup"><span data-stu-id="74b65-141">The packages are just-in-time (JIT) compiled to improve startup performance.</span></span>

<span data-ttu-id="74b65-142">Если в диалоговом окне создания проекта установлен флажок **Configure for HTTP** (Настроить для трафика HTTPS), *Dockerfile* предоставляет два порта.</span><span class="sxs-lookup"><span data-stu-id="74b65-142">When the new project dialog's **Configure for HTTPS** check box is checked, the *Dockerfile* exposes two ports.</span></span> <span data-ttu-id="74b65-143">Один порт используется для трафика HTTP, другой — для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="74b65-143">One port is used for HTTP traffic; the other port is used for HTTPS.</span></span> <span data-ttu-id="74b65-144">Если флажок не установлен, для трафика HTTP предоставляется один порт (80).</span><span class="sxs-lookup"><span data-stu-id="74b65-144">If the check box isn't checked, a single port (80) is exposed for HTTP traffic.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-dockerfile[](visual-studio-tools-for-docker/samples/2.0/HelloDockerTools/Dockerfile?highlight=1,5,13,16)]

<span data-ttu-id="74b65-145">Предыдущий *Dockerfile* основан на образе [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/).</span><span class="sxs-lookup"><span data-stu-id="74b65-145">The preceding *Dockerfile* is based on the [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) image.</span></span> <span data-ttu-id="74b65-146">Этот базовый образ включает пакеты NuGet платформы ASP.NET Core, которые скомпилированы JIT-компилятором для повышения производительности запуска.</span><span class="sxs-lookup"><span data-stu-id="74b65-146">This base image includes the ASP.NET Core NuGet packages, which are just-in-time (JIT) compiled to improve startup performance.</span></span>

::: moniker-end

## <a name="add-container-orchestrator-support-to-an-app"></a><span data-ttu-id="74b65-147">Добавление поддержки оркестратора контейнеров в приложение</span><span class="sxs-lookup"><span data-stu-id="74b65-147">Add container orchestrator support to an app</span></span>

<span data-ttu-id="74b65-148">Visual Studio 2017 версии 15.7 или более ранние версии поддерживают [Docker Compose](https://docs.docker.com/compose/overview/) как единственное решение для оркестрации контейнеров.</span><span class="sxs-lookup"><span data-stu-id="74b65-148">Visual Studio 2017 versions 15.7 or earlier support [Docker Compose](https://docs.docker.com/compose/overview/) as the sole container orchestration solution.</span></span> <span data-ttu-id="74b65-149">Для добавления артефактов Docker Compose необходимо последовательно выбрать **Добавить** > **Поддержка Docker**.</span><span class="sxs-lookup"><span data-stu-id="74b65-149">The Docker Compose artifacts are added via **Add** > **Docker Support**.</span></span>

<span data-ttu-id="74b65-150">Visual Studio 2017 версии 15.8 или более поздние версии поддерживают решение для оркестрации только когда это указано отдельно.</span><span class="sxs-lookup"><span data-stu-id="74b65-150">Visual Studio 2017 versions 15.8 or later add an orchestration solution only when instructed.</span></span> <span data-ttu-id="74b65-151">В **Обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Поддержка оркестратора контейнеров**.</span><span class="sxs-lookup"><span data-stu-id="74b65-151">Right-click the project in **Solution Explorer** and select **Add** > **Container Orchestrator Support**.</span></span> <span data-ttu-id="74b65-152">Предлагается два различных варианта: [Docker Compose](#docker-compose) и [Service Fabric](#service-fabric).</span><span class="sxs-lookup"><span data-stu-id="74b65-152">Two different choices are offered: [Docker Compose](#docker-compose) and [Service Fabric](#service-fabric).</span></span>

### <a name="docker-compose"></a><span data-ttu-id="74b65-153">Docker Compose</span><span class="sxs-lookup"><span data-stu-id="74b65-153">Docker Compose</span></span>

<span data-ttu-id="74b65-154">Средства Visual Studio для Docker добавляют в решение проект *docker-compose* со следующими файлами:</span><span class="sxs-lookup"><span data-stu-id="74b65-154">The Visual Studio Tools for Docker add a *docker-compose* project to the solution with the following files:</span></span>

* <span data-ttu-id="74b65-155">*docker-compose.dcproj* &ndash;. Файл, представляющий проект.</span><span class="sxs-lookup"><span data-stu-id="74b65-155">*docker-compose.dcproj* &ndash; The file representing the project.</span></span> <span data-ttu-id="74b65-156">Включает в себя элемент `<DockerTargetOS>`, указывающий используемую ОС.</span><span class="sxs-lookup"><span data-stu-id="74b65-156">Includes a `<DockerTargetOS>` element specifying the OS to be used.</span></span>
* <span data-ttu-id="74b65-157">*.dockerignore* &ndash;. Содержит список шаблонов файлов и каталогов для исключения при создании контекста сборки.</span><span class="sxs-lookup"><span data-stu-id="74b65-157">*.dockerignore* &ndash; Lists the file and directory patterns to exclude when generating a build context.</span></span>
* <span data-ttu-id="74b65-158">*docker-compose.yml* &ndash;. Базовый файл [Docker Compose](https://docs.docker.com/compose/overview/), который служит для определения коллекции образов, сборка и запуск которых выполняется с помощью команд `docker-compose build` и `docker-compose run` соответственно.</span><span class="sxs-lookup"><span data-stu-id="74b65-158">*docker-compose.yml* &ndash; The base [Docker Compose](https://docs.docker.com/compose/overview/) file used to define the collection of images built and run with `docker-compose build` and `docker-compose run`, respectively.</span></span>
* <span data-ttu-id="74b65-159">*docker-compose.override.yml* &ndash;. Дополнительный файл, считываемый Docker Compose и содержащий переопределения конфигурации для служб.</span><span class="sxs-lookup"><span data-stu-id="74b65-159">*docker-compose.override.yml* &ndash; An optional file, read by Docker Compose, with configuration overrides for services.</span></span> <span data-ttu-id="74b65-160">Visual Studio выполняет `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` для объединения этих файлов.</span><span class="sxs-lookup"><span data-stu-id="74b65-160">Visual Studio executes `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` to merge these files.</span></span>

<span data-ttu-id="74b65-161">Файл *docker-compose.yml* ссылается на имя образа, создаваемого при выполнении проекта:</span><span class="sxs-lookup"><span data-stu-id="74b65-161">The *docker-compose.yml* file references the name of the image that's created when the project runs:</span></span>

[!code-yaml[](visual-studio-tools-for-docker/samples/2.0/docker-compose.yml?highlight=5)]

<span data-ttu-id="74b65-162">В предыдущем примере `image: hellodockertools` создает образ `hellodockertools:dev`, когда приложение выполняется в режиме **отладки**.</span><span class="sxs-lookup"><span data-stu-id="74b65-162">In the preceding example, `image: hellodockertools` generates the image `hellodockertools:dev` when the app runs in **Debug** mode.</span></span> <span data-ttu-id="74b65-163">Образ `hellodockertools:latest` создается, когда приложение запускается в режиме **выпуска**.</span><span class="sxs-lookup"><span data-stu-id="74b65-163">The `hellodockertools:latest` image is generated when the app runs in **Release** mode.</span></span>

<span data-ttu-id="74b65-164">Если образ будет отправляться в реестр, добавьте имя пользователя [центра Docker](https://hub.docker.com/) (например, `dockerhubusername/hellodockertools`) в качестве префикса к имени образа.</span><span class="sxs-lookup"><span data-stu-id="74b65-164">Prefix the image name with the [Docker Hub](https://hub.docker.com/) username (for example, `dockerhubusername/hellodockertools`) if the image is pushed to the registry.</span></span> <span data-ttu-id="74b65-165">Кроме того, в имя образа можно включить URL-адрес частного реестра (например, `privateregistry.domain.com/hellodockertools`) в зависимости от конфигурации.</span><span class="sxs-lookup"><span data-stu-id="74b65-165">Alternatively, change the image name to include the private registry URL (for example, `privateregistry.domain.com/hellodockertools`) depending on the configuration.</span></span>

<span data-ttu-id="74b65-166">Чтобы реализовать разное поведение в зависимости от конфигурации сборки (например, отладка или выпуск), добавьте зависящие от конфигурации файлы *docker-compose*.</span><span class="sxs-lookup"><span data-stu-id="74b65-166">If you want different behavior based on the build configuration (for example, Debug or Release), add configuration-specific *docker-compose* files.</span></span> <span data-ttu-id="74b65-167">Имена файлов должны соответствовать конфигурации сборки (например, *docker-compose.vs.debug.yml* и *docker-compose.vs.release.yml*) и находиться в том же расположении, что и файл *docker-compose-override.yml*.</span><span class="sxs-lookup"><span data-stu-id="74b65-167">The files should be named according to the build configuration (for example, *docker-compose.vs.debug.yml* and *docker-compose.vs.release.yml*) and placed in the same location as the *docker-compose-override.yml* file.</span></span> 

<span data-ttu-id="74b65-168">Используя зависящие от конфигурации файлы переопределения, можно указать различные параметры (например, переменные среды или точки входа) для конфигураций отладки и выпуска.</span><span class="sxs-lookup"><span data-stu-id="74b65-168">Using the configuration-specific override files, you can specify different configuration settings (such as environment variables or entry points) for Debug and Release build configurations.</span></span>

### <a name="service-fabric"></a><span data-ttu-id="74b65-169">Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="74b65-169">Service Fabric</span></span>

<span data-ttu-id="74b65-170">Помимо базовых [Предварительных требований](#prerequisites) для решения по оркестрации [Service Fabric](/azure/service-fabric/) необходимо выполнить следующие предварительные условия:</span><span class="sxs-lookup"><span data-stu-id="74b65-170">In addition to the base [Prerequisites](#prerequisites), the [Service Fabric](/azure/service-fabric/) orchestration solution demands the following prerequisites:</span></span>

* <span data-ttu-id="74b65-171">[Пакет SDK для Microsoft Azure Service Fabric](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK) версии 2.6 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="74b65-171">[Microsoft Azure Service Fabric SDK](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK) version 2.6 or later</span></span>
* <span data-ttu-id="74b65-172">Рабочая нагрузка **Разработка для Azure** Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="74b65-172">Visual Studio 2017's **Azure Development** workload</span></span>

<span data-ttu-id="74b65-173">Service Fabric не поддерживает запуск контейнеров Linux в кластере локальной разработки в Windows.</span><span class="sxs-lookup"><span data-stu-id="74b65-173">Service Fabric doesn't support running Linux containers in the local development cluster on Windows.</span></span> <span data-ttu-id="74b65-174">Если в проекте уже используется контейнер Linux, Visual Studio предложит переключиться на контейнеры Windows.</span><span class="sxs-lookup"><span data-stu-id="74b65-174">If the project is already using a Linux container, Visual Studio prompts to switch to Windows containers.</span></span>

<span data-ttu-id="74b65-175">Средства Visual Studio для Docker позволяют выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="74b65-175">The Visual Studio Tools for Docker do the following tasks:</span></span>

* <span data-ttu-id="74b65-176">добавление проекта **Service Fabric Application** *&lt;имя_проекта&gt;приложение* в решение;</span><span class="sxs-lookup"><span data-stu-id="74b65-176">Adds a *&lt;project_name&gt;Application* **Service Fabric Application** project to the solution.</span></span>
* <span data-ttu-id="74b65-177">добавление *Dockerfile* и файла *.dockerignore* в проект ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="74b65-177">Adds a *Dockerfile* and a *.dockerignore* file to the ASP.NET Core project.</span></span> <span data-ttu-id="74b65-178">Если *Dockerfile* уже существует в проекте ASP.NET Core, он переименовывается в *Dockerfile.original*.</span><span class="sxs-lookup"><span data-stu-id="74b65-178">If a *Dockerfile* already exists in the ASP.NET Core project, it's renamed to *Dockerfile.original*.</span></span> <span data-ttu-id="74b65-179">Создается новый *Dockerfile*, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="74b65-179">A new *Dockerfile*, similar to the following, is created:</span></span>

    [!code-dockerfile[](visual-studio-tools-for-docker/samples/2.1/HelloDockerTools/Dockerfile)]

* <span data-ttu-id="74b65-180">добавляет элемент `<IsServiceFabricServiceProject>` в файл *.csproj* проекта ASP.NET Core;</span><span class="sxs-lookup"><span data-stu-id="74b65-180">Adds an `<IsServiceFabricServiceProject>` element to the ASP.NET Core project's *.csproj* file:</span></span>

    [!code-xml[](visual-studio-tools-for-docker/samples/2.1/HelloDockerTools/HelloDockerTools.csproj?name=snippet_IsServiceFabricServiceProject)]

* <span data-ttu-id="74b65-181">добавляет папку *PackageRoot* в проект ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="74b65-181">Adds a *PackageRoot* folder to the ASP.NET Core project.</span></span> <span data-ttu-id="74b65-182">Папка содержит манифест службы и параметры для новой службы.</span><span class="sxs-lookup"><span data-stu-id="74b65-182">The folder includes the service manifest and settings for the new service.</span></span>

<span data-ttu-id="74b65-183">Дополнительные сведения см. в статье [Руководство по развертыванию приложения .NET в контейнере Windows в Azure Service Fabric](/azure/service-fabric/service-fabric-host-app-in-a-container).</span><span class="sxs-lookup"><span data-stu-id="74b65-183">For more information, see [Deploy a .NET app in a Windows container to Azure Service Fabric](/azure/service-fabric/service-fabric-host-app-in-a-container).</span></span>

## <a name="debug"></a><span data-ttu-id="74b65-184">Отладка</span><span class="sxs-lookup"><span data-stu-id="74b65-184">Debug</span></span>

<span data-ttu-id="74b65-185">Выберите пункт **Docker** в раскрывающемся списке отладки на панели инструментов, чтобы начать отладку приложения.</span><span class="sxs-lookup"><span data-stu-id="74b65-185">Select **Docker** from the debug drop-down in the toolbar, and start debugging the app.</span></span> <span data-ttu-id="74b65-186">Представление **Docker** окна **Выходные данные** показывает следующие выполненные действия:</span><span class="sxs-lookup"><span data-stu-id="74b65-186">The **Docker** view of the **Output** window shows the following actions taking place:</span></span>

::: moniker range=">= aspnetcore-2.1"

* <span data-ttu-id="74b65-187">Получение тега *2.1-aspnetcore-runtime* образа среды выполнения *microsoft/dotnet* (если его еще нет в кэше).</span><span class="sxs-lookup"><span data-stu-id="74b65-187">The *2.1-aspnetcore-runtime* tag of the *microsoft/dotnet* runtime image is acquired (if not already in the cache).</span></span> <span data-ttu-id="74b65-188">Образ устанавливает среды выполнения ASP.NET Core и .NET Core и связанные библиотеки.</span><span class="sxs-lookup"><span data-stu-id="74b65-188">The image installs the ASP.NET Core and .NET Core runtimes and associated libraries.</span></span> <span data-ttu-id="74b65-189">Он оптимизирован для запуска приложений ASP.NET Core в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="74b65-189">It's optimized for running ASP.NET Core apps in production.</span></span>
* <span data-ttu-id="74b65-190">Задание для переменной среды `ASPNETCORE_ENVIRONMENT` значения `Development` внутри контейнера.</span><span class="sxs-lookup"><span data-stu-id="74b65-190">The `ASPNETCORE_ENVIRONMENT` environment variable is set to `Development` within the container.</span></span>
* <span data-ttu-id="74b65-191">Предоставление двух динамически назначенных портов: для трафика HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="74b65-191">Two dynamically assigned ports are exposed: one for HTTP and one for HTTPS.</span></span> <span data-ttu-id="74b65-192">Отправка запроса к порту, назначенному localhost, с помощью команды `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="74b65-192">The port assigned to localhost can be queried with the `docker ps` command.</span></span>
* <span data-ttu-id="74b65-193">Копирование приложения в контейнер.</span><span class="sxs-lookup"><span data-stu-id="74b65-193">The app is copied to the container.</span></span>
* <span data-ttu-id="74b65-194">Запуск браузера по умолчанию с подключенным отладчиком для обращения к контейнеру по динамически назначаемому порту.</span><span class="sxs-lookup"><span data-stu-id="74b65-194">The default browser is launched with the debugger attached to the container using the dynamically assigned port.</span></span>

<span data-ttu-id="74b65-195">Итоговый образ Docker приложения помечается как *dev*.</span><span class="sxs-lookup"><span data-stu-id="74b65-195">The resulting Docker image of the app is tagged as *dev*.</span></span> <span data-ttu-id="74b65-196">Образ основан на теге *2.1-aspnetcore-runtime* базового образа *microsoft/dotnet*.</span><span class="sxs-lookup"><span data-stu-id="74b65-196">The image is based on the *2.1-aspnetcore-runtime* tag of the *microsoft/dotnet* base image.</span></span> <span data-ttu-id="74b65-197">Выполните команду `docker images` в окне **Консоль диспетчера пакетов** (PMC).</span><span class="sxs-lookup"><span data-stu-id="74b65-197">Run the `docker images` command in the **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="74b65-198">На компьютере отобразятся следующие образы:</span><span class="sxs-lookup"><span data-stu-id="74b65-198">The images on the machine are displayed:</span></span>

```console
REPOSITORY        TAG                     IMAGE ID      CREATED         SIZE
hellodockertools  dev                     d72ce0f1dfe7  30 seconds ago  255MB
microsoft/dotnet  2.1-aspnetcore-runtime  fcc3887985bb  6 days ago      255MB
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

* <span data-ttu-id="74b65-199">Получение образа среды выполнения *microsoft/aspnetcore* (если его еще нет в кэше).</span><span class="sxs-lookup"><span data-stu-id="74b65-199">The *microsoft/aspnetcore* runtime image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="74b65-200">Задание для переменной среды `ASPNETCORE_ENVIRONMENT` значения `Development` внутри контейнера.</span><span class="sxs-lookup"><span data-stu-id="74b65-200">The `ASPNETCORE_ENVIRONMENT` environment variable is set to `Development` within the container.</span></span>
* <span data-ttu-id="74b65-201">Порт 80 открыт и сопоставлен с динамически назначаемым портом для localhost.</span><span class="sxs-lookup"><span data-stu-id="74b65-201">Port 80 is exposed and mapped to a dynamically assigned port for localhost.</span></span> <span data-ttu-id="74b65-202">Порт определяется узлом Docker и может запрашиваться с помощью команды `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="74b65-202">The port is determined by the Docker host and can be queried with the `docker ps` command.</span></span>
* <span data-ttu-id="74b65-203">Копирование приложения в контейнер.</span><span class="sxs-lookup"><span data-stu-id="74b65-203">The app is copied to the container.</span></span>
* <span data-ttu-id="74b65-204">Запуск браузера по умолчанию с подключенным отладчиком для обращения к контейнеру по динамически назначаемому порту.</span><span class="sxs-lookup"><span data-stu-id="74b65-204">The default browser is launched with the debugger attached to the container using the dynamically assigned port.</span></span>

<span data-ttu-id="74b65-205">Итоговый образ Docker приложения помечается как *dev*.</span><span class="sxs-lookup"><span data-stu-id="74b65-205">The resulting Docker image of the app is tagged as *dev*.</span></span> <span data-ttu-id="74b65-206">Образ основан на базовом образе *microsoft/aspnetcore*.</span><span class="sxs-lookup"><span data-stu-id="74b65-206">The image is based on the *microsoft/aspnetcore* base image.</span></span> <span data-ttu-id="74b65-207">Выполните команду `docker images` в окне **Консоль диспетчера пакетов** (PMC).</span><span class="sxs-lookup"><span data-stu-id="74b65-207">Run the `docker images` command in the **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="74b65-208">На компьютере отобразятся следующие образы:</span><span class="sxs-lookup"><span data-stu-id="74b65-208">The images on the machine are displayed:</span></span>

```console
REPOSITORY            TAG  IMAGE ID      CREATED        SIZE
hellodockertools      dev  5fafe5d1ad5b  4 minutes ago  347MB
microsoft/aspnetcore  2.0  c69d39472da9  13 days ago    347MB
```

::: moniker-end

> [!NOTE]
> <span data-ttu-id="74b65-209">В образе *dev* нет содержимого приложения, так как конфигурации **Отладки** используют подключение томов для удобства при итеративных процессах отладки.</span><span class="sxs-lookup"><span data-stu-id="74b65-209">The *dev* image lacks the app contents, as **Debug** configurations use volume mounting to provide the iterative experience.</span></span> <span data-ttu-id="74b65-210">Чтобы отправить образ, используйте конфигурацию **выпуска**.</span><span class="sxs-lookup"><span data-stu-id="74b65-210">To push an image, use the **Release** configuration.</span></span>

<span data-ttu-id="74b65-211">Выполните команду `docker ps` в PMC.</span><span class="sxs-lookup"><span data-stu-id="74b65-211">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="74b65-212">Обратите внимание, что приложение выполняется с помощью контейнера:</span><span class="sxs-lookup"><span data-stu-id="74b65-212">Notice the app is running using the container:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="edit-and-continue"></a><span data-ttu-id="74b65-213">Изменение и продолжение</span><span class="sxs-lookup"><span data-stu-id="74b65-213">Edit and continue</span></span>

<span data-ttu-id="74b65-214">Изменения статических полей и представлений Razor применяются автоматически без необходимости выполнять этап компиляции.</span><span class="sxs-lookup"><span data-stu-id="74b65-214">Changes to static files and Razor views are automatically updated without the need for a compilation step.</span></span> <span data-ttu-id="74b65-215">Внесите изменение, сохраните его и перезагрузите страницу в браузере, чтобы увидеть обновление.</span><span class="sxs-lookup"><span data-stu-id="74b65-215">Make the change, save, and refresh the browser to view the update.</span></span>

<span data-ttu-id="74b65-216">Для внесения изменений в файлы кода требуются выполнить компиляцию и перезапуск Kestrel в контейнере.</span><span class="sxs-lookup"><span data-stu-id="74b65-216">Code file modifications require compilation and a restart of Kestrel within the container.</span></span> <span data-ttu-id="74b65-217">После внесения изменения нажмите клавиши `CTRL+F5`, чтобы выполнить процесс и запустить приложение в контейнере.</span><span class="sxs-lookup"><span data-stu-id="74b65-217">After making the change, use `CTRL+F5` to perform the process and start the app within the container.</span></span> <span data-ttu-id="74b65-218">Контейнер Docker не перестраивается и не останавливается.</span><span class="sxs-lookup"><span data-stu-id="74b65-218">The Docker container isn't rebuilt or stopped.</span></span> <span data-ttu-id="74b65-219">Выполните команду `docker ps` в PMC.</span><span class="sxs-lookup"><span data-stu-id="74b65-219">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="74b65-220">Обратите внимание, что исходный контейнер все еще выполняется, как и 10 минут назад:</span><span class="sxs-lookup"><span data-stu-id="74b65-220">Notice the original container is still running as of 10 minutes ago:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   10 minutes ago      Up 10 minutes       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a><span data-ttu-id="74b65-221">Публикация образов Docker</span><span class="sxs-lookup"><span data-stu-id="74b65-221">Publish Docker images</span></span>

<span data-ttu-id="74b65-222">После завершения цикла разработки и отладки приложения используйте Средства Visual Studio для Docker, чтобы создать рабочий образ приложения.</span><span class="sxs-lookup"><span data-stu-id="74b65-222">Once the develop and debug cycle of the app is completed, the Visual Studio Tools for Docker assist in creating the production image of the app.</span></span> <span data-ttu-id="74b65-223">Выберите в раскрывающемся списке конфигурации значение **Выпуск** и выполните сборку приложения.</span><span class="sxs-lookup"><span data-stu-id="74b65-223">Change the configuration drop-down to **Release** and build the app.</span></span> <span data-ttu-id="74b65-224">Инструментарий получает образ компиляции или публикации из центра Docker (если он отсутствует в кэше).</span><span class="sxs-lookup"><span data-stu-id="74b65-224">The tooling acquires the compile/publish image from Docker Hub (if not already in the cache).</span></span> <span data-ttu-id="74b65-225">Образ создается с тегом *latest*, который можно отправить в закрытый реестр или в центр Docker.</span><span class="sxs-lookup"><span data-stu-id="74b65-225">An image is produced with the *latest* tag, which can be pushed to the private registry or Docker Hub.</span></span>

<span data-ttu-id="74b65-226">В PMC выполните команду `docker images`, чтобы просмотреть список образов.</span><span class="sxs-lookup"><span data-stu-id="74b65-226">Run the `docker images` command in PMC to see the list of images.</span></span> <span data-ttu-id="74b65-227">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="74b65-227">Output similar to the following is displayed:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
REPOSITORY        TAG                     IMAGE ID      CREATED             SIZE
hellodockertools  latest                  e3984a64230c  About a minute ago  258MB
hellodockertools  dev                     d72ce0f1dfe7  4 minutes ago       255MB
microsoft/dotnet  2.1-sdk                 9e243db15f91  6 days ago          1.7GB
microsoft/dotnet  2.1-aspnetcore-runtime  fcc3887985bb  6 days ago          255MB
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

```console
REPOSITORY                  TAG     IMAGE ID      CREATED         SIZE
hellodockertools            latest  cd28f0d4abbd  12 seconds ago  349MB
hellodockertools            dev     5fafe5d1ad5b  23 minutes ago  347MB
microsoft/aspnetcore-build  2.0     7fed40fbb647  13 days ago     2.02GB
microsoft/aspnetcore        2.0     c69d39472da9  13 days ago     347MB
```

<span data-ttu-id="74b65-228">Начиная с .NET Core 2.1, образы `microsoft/aspnetcore-build` и `microsoft/aspnetcore`, указанные в предыдущих выходных данных, заменяются образами `microsoft/dotnet`.</span><span class="sxs-lookup"><span data-stu-id="74b65-228">The `microsoft/aspnetcore-build` and `microsoft/aspnetcore` images listed in the preceding output are replaced with `microsoft/dotnet` images as of .NET Core 2.1.</span></span> <span data-ttu-id="74b65-229">Дополнительные сведения см. в [объявлении о миграции репозиториев Docker](https://github.com/aspnet/Announcements/issues/298).</span><span class="sxs-lookup"><span data-stu-id="74b65-229">For more information, see [the Docker repositories migration announcement](https://github.com/aspnet/Announcements/issues/298).</span></span>

::: moniker-end

> [!NOTE]
> <span data-ttu-id="74b65-230">Команда `docker images` возвращает промежуточные образы с именами репозитория и тегами, обозначенными как *\<none>* (не указаны выше).</span><span class="sxs-lookup"><span data-stu-id="74b65-230">The `docker images` command returns intermediary images with repository names and tags identified as *\<none>* (not listed above).</span></span> <span data-ttu-id="74b65-231">Эти неименованные образы создаются *Dockerfile* [многоэтапной сборки](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="74b65-231">These unnamed images are produced by the [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*.</span></span> <span data-ttu-id="74b65-232">Они повышают эффективность сборки окончательного образа &mdash; при изменениях перестраиваются только необходимые слои.</span><span class="sxs-lookup"><span data-stu-id="74b65-232">They improve the efficiency of building the final image&mdash;only the necessary layers are rebuilt when changes occur.</span></span> <span data-ttu-id="74b65-233">Когда промежуточные образы больше не требуются, удалите их с помощью команды [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/).</span><span class="sxs-lookup"><span data-stu-id="74b65-233">When the intermediary images are no longer needed, delete them using the [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) command.</span></span>

<span data-ttu-id="74b65-234">Рабочий образ или образ выпуска может быть меньше по размеру, чем образ *dev*.</span><span class="sxs-lookup"><span data-stu-id="74b65-234">There may be an expectation for the production or release image to be smaller in size by comparison to the *dev* image.</span></span> <span data-ttu-id="74b65-235">Из-за сопоставления томов отладчик и приложение запускались с локального компьютера, а не внутри контейнера.</span><span class="sxs-lookup"><span data-stu-id="74b65-235">Because of the volume mapping, the debugger and app were running from the local machine and not within the container.</span></span> <span data-ttu-id="74b65-236">Образ с тегом *latest* упаковал код приложения, необходимый для запуска приложения на хост-компьютере.</span><span class="sxs-lookup"><span data-stu-id="74b65-236">The *latest* image has packaged the necessary app code to run the app on a host machine.</span></span> <span data-ttu-id="74b65-237">Таким образом, размер изменится на размер кода конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="74b65-237">Therefore, the delta is the size of the app code.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74b65-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="74b65-238">Additional resources</span></span>

* [<span data-ttu-id="74b65-239">Разработка с помощью контейнеров в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74b65-239">Container development with Visual Studio</span></span>](/visualstudio/containers)
* [<span data-ttu-id="74b65-240">Azure Service Fabric: Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="74b65-240">Azure Service Fabric: Prepare your development environment</span></span>](/azure/service-fabric/service-fabric-get-started)
* [<span data-ttu-id="74b65-241">Руководство по развертыванию приложения .NET в контейнере Windows в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="74b65-241">Deploy a .NET app in a Windows container to Azure Service Fabric</span></span>](/azure/service-fabric/service-fabric-host-app-in-a-container)
* [<span data-ttu-id="74b65-242">Устранение неполадок при разработке Visual Studio 2017 с использованием Docker</span><span class="sxs-lookup"><span data-stu-id="74b65-242">Troubleshoot Visual Studio 2017 development with Docker</span></span>](/azure/vs-azure-tools-docker-troubleshooting-docker-errors)
* [<span data-ttu-id="74b65-243">Средства Visual Studio для Docker — репозиторий GitHub</span><span class="sxs-lookup"><span data-stu-id="74b65-243">Visual Studio Tools for Docker GitHub repository</span></span>](https://github.com/Microsoft/DockerTools)
