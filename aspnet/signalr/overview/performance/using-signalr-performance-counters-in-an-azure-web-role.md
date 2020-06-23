---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Использование счетчиков производительности SignalR в веб-роли Azure | Документация Майкрософт
author: guardrex
description: Установка и использование счетчиков производительности SignalR в веб-роли Azure.
keywords: ASP. NET, SignalR, счетчик производительности, веб-роль Azure
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240636"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="84306-104">Использование счетчиков производительности SignalR в веб-роли Azure</span><span class="sxs-lookup"><span data-stu-id="84306-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="84306-105">Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)</span><span class="sxs-lookup"><span data-stu-id="84306-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="84306-106">Счетчики производительности SignalR используются для мониторинга производительности приложения в веб-роли Azure.</span><span class="sxs-lookup"><span data-stu-id="84306-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="84306-107">Счетчики фиксируются система диагностики Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84306-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="84306-108">Вы устанавливаете счетчики производительности SignalR в Azure, используя *signalr.exe*, то же средство, которое используется для автономных или локальных приложений.</span><span class="sxs-lookup"><span data-stu-id="84306-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="84306-109">Так как роли Azure являются временными, вы настраиваете приложение для установки и регистрации счетчиков производительности SignalR при запуске.</span><span class="sxs-lookup"><span data-stu-id="84306-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84306-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84306-110">Prerequisites</span></span>

* <span data-ttu-id="84306-111">Visual Studio 2015 или [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="84306-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="84306-112">[Microsoft Azure SDK для Visual Studio](https://azure.microsoft.com/downloads/) **Примечание. Перезагрузите компьютер после установки пакета SDK.**</span><span class="sxs-lookup"><span data-stu-id="84306-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="84306-113">Подписка Microsoft Azure. чтобы зарегистрироваться для получения бесплатной пробной учетной записи Azure, см. статью [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="84306-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="84306-114">Создание приложения веб-роли Azure, предоставляющего счетчики производительности SignalR</span><span class="sxs-lookup"><span data-stu-id="84306-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="84306-115">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84306-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="84306-116">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="84306-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="84306-117">В диалоговом окне **Новый проект** выберите категорию облако **Visual C#**  >  **Cloud** слева, а затем выберите шаблон **облачная служба Azure** .</span><span class="sxs-lookup"><span data-stu-id="84306-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="84306-118">Присвойте приложению имя **сигналрперфкаунтерс** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84306-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![Новое облачное приложение](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="84306-120">Если вы не видите категорию шаблон **облака** или шаблон **облачной службы Azure** , необходимо установить рабочую нагрузку **разработки Azure** для Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="84306-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="84306-121">Щелкните ссылку **открыть Visual Studio Installer** в нижней левой части диалогового окна **Новый проект** , чтобы открыть Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="84306-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="84306-122">Выберите рабочую нагрузку **Разработка Azure** и нажмите кнопку **изменить** , чтобы начать установку рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="84306-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Рабочая нагрузка разработки Azure в Visual Studio Installer](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="84306-124">В диалоговом окне **создание Microsoft Azure облачной службы** выберите **веб-роль ASP.NET** и нажмите кнопку >, чтобы добавить роль в проект.</span><span class="sxs-lookup"><span data-stu-id="84306-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="84306-125">Щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84306-125">Select **OK**.</span></span>

   ![Добавить веб-роль ASP.NET](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="84306-127">В диалоговом окне **Создание веб-приложения ASP.NET — WebRole1** выберите шаблон **MVC** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84306-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![Добавление MVC и веб-API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="84306-129">В **Обозреватель решений**откройте файл *Diagnostics. Wadcfgx* в разделе **WebRole1**.</span><span class="sxs-lookup"><span data-stu-id="84306-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![Обозреватель решений Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="84306-131">Замените содержимое файла следующей конфигурацией и сохраните файл:</span><span class="sxs-lookup"><span data-stu-id="84306-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="84306-132">Откройте **консоль диспетчера пакетов** из **меню Инструменты**  >  **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="84306-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="84306-133">Введите следующие команды для установки последней версии SignalR и пакета служебных программ SignalR:</span><span class="sxs-lookup"><span data-stu-id="84306-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="84306-134">Настройте приложение для установки счетчиков производительности SignalR в экземпляр роли при запуске или перезапуске.</span><span class="sxs-lookup"><span data-stu-id="84306-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="84306-135">В **Обозреватель решений**щелкните правой кнопкой мыши проект **WebRole1** и выберите команду **добавить**  >  **новую папку**.</span><span class="sxs-lookup"><span data-stu-id="84306-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="84306-136">Назовите новую папку *Startup*.</span><span class="sxs-lookup"><span data-stu-id="84306-136">Name the new folder *Startup*.</span></span>

   ![Добавить папку автозагрузки](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="84306-138">Скопируйте файл *signalr.exe* (добавленный с пакетом **Microsoft. AspNet. SignalR. utils** ) из \<project folder> /сигналрперфкаунтерс/паккажес/Микрософт.АСПнет.сигналр.утилс. \<version> /тулс в папку *Startup* , созданную на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="84306-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="84306-139">В **Обозреватель решений**щелкните правой кнопкой мыши папку *Startup* и выберите команду **добавить**  >  **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="84306-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="84306-140">В появившемся диалоговом окне выберите *signalr.exe* и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="84306-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![Добавление signalr.exe в проект](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="84306-142">Щелкните правой кнопкой мыши созданную папку *автозагрузки* .</span><span class="sxs-lookup"><span data-stu-id="84306-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="84306-143">Выберите **Добавить**  >  **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="84306-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="84306-144">Выберите узел **Общие** , выберите **текстовый файл**и назовите новый элемент *сигналрперфкаунтеринсталл. cmd*.</span><span class="sxs-lookup"><span data-stu-id="84306-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="84306-145">Этот командный файл установит счетчики производительности SignalR в веб-роль.</span><span class="sxs-lookup"><span data-stu-id="84306-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![Создать пакетный файл установки счетчика производительности SignalR](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="84306-147">Когда Visual Studio создаст файл *сигналрперфкаунтеринсталл. cmd* , он будет автоматически открыт в главном окне.</span><span class="sxs-lookup"><span data-stu-id="84306-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="84306-148">Замените содержимое файла следующим скриптом, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="84306-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="84306-149">Этот скрипт выполняет *signalr.exe*, который добавляет счетчики производительности SignalR в экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="84306-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="84306-150">Выберите файл *signalr.exe* в **Обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="84306-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="84306-151">В **свойствах**файла задайте для параметра **Копировать в выходной каталог** значение **всегда копировать**.</span><span class="sxs-lookup"><span data-stu-id="84306-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![Установите для параметра Копировать в выходной каталог значение всегда копировать.](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="84306-153">Повторите предыдущий шаг для файла *сигналрперфкаунтеринсталл. cmd* .</span><span class="sxs-lookup"><span data-stu-id="84306-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="84306-154">Щелкните правой кнопкой мыши файл *сигналрперфкаунтеринсталл. cmd* и выберите команду **Открыть с помощью**.</span><span class="sxs-lookup"><span data-stu-id="84306-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="84306-155">В появившемся диалоговом окне выберите **двоичный редактор** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84306-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![Открыть с помощью двоичного редактора](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="84306-157">В двоичном редакторе выберите все начальные байты в файле и удалите их.</span><span class="sxs-lookup"><span data-stu-id="84306-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="84306-158">Сохраните файл и закройте его.</span><span class="sxs-lookup"><span data-stu-id="84306-158">Save and close the file.</span></span>

    ![Удалить начальные байты](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="84306-160">Откройте *ServiceDefinition. csdef* и добавьте задачу запуска, которая выполняет файл *сигналрперфкаунтеринсталл. cmd* при запуске службы:</span><span class="sxs-lookup"><span data-stu-id="84306-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="84306-161">Откройте `Views/Shared/_Layout.cshtml` и удалите скрипт пакета jQuery из конца файла.</span><span class="sxs-lookup"><span data-stu-id="84306-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="84306-162">Добавьте клиент JavaScript, который постоянно вызывает `increment` метод на сервере.</span><span class="sxs-lookup"><span data-stu-id="84306-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="84306-163">Откройте `Views/Home/Index.cshtml` и замените содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="84306-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="84306-164">Создайте новую папку в проекте **WebRole1** *с именем*Hubs.</span><span class="sxs-lookup"><span data-stu-id="84306-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="84306-165">Щелкните правой кнопкой мыши папку *концентраторы* в **Обозреватель решений** и выберите команду **добавить**  >  **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="84306-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="84306-166">В диалоговом окне **Добавление нового элемента** выберите категорию **веб-**  >  **SignalR** и выберите шаблон элемента **класс концентратора SignalR (v2)** .</span><span class="sxs-lookup"><span data-stu-id="84306-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="84306-167">Присвойте новому концентратору имя *MyHub.CS* и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="84306-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![Добавление класса концентратора SignalR в папку "концентраторы" в диалоговом окне "Добавление нового элемента"](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="84306-169">*MyHub.CS* будет автоматически открываться в главном окне.</span><span class="sxs-lookup"><span data-stu-id="84306-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="84306-170">Замените содержимое следующим кодом, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="84306-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="84306-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* — это средство тестирования плотности подключений, предоставляемое с базой кода SignalR.</span><span class="sxs-lookup"><span data-stu-id="84306-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="84306-172">Так как для погромче требуется постоянное подключение, вы добавляете его на сайт для использования при тестировании.</span><span class="sxs-lookup"><span data-stu-id="84306-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="84306-173">Добавьте новую папку в проект **WebRole1** с именем *персистентконнектионс*.</span><span class="sxs-lookup"><span data-stu-id="84306-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="84306-174">Щелкните правой кнопкой мыши эту папку и выберите команду **Добавить**  >  **класс**.</span><span class="sxs-lookup"><span data-stu-id="84306-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="84306-175">Назовите новый файл класса *MyPersistentConnections.CS* и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="84306-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="84306-176">Visual Studio откроет файл *MyPersistentConnections.CS* в главном окне.</span><span class="sxs-lookup"><span data-stu-id="84306-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="84306-177">Замените содержимое следующим кодом, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="84306-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="84306-178">С помощью `Startup` класса объекты SignalR запускаются при запуске OWIN.</span><span class="sxs-lookup"><span data-stu-id="84306-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="84306-179">Откройте или создайте *Startup.CS* и замените содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="84306-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="84306-180">В приведенном выше коде `OwinStartup` атрибут помечает этот класс для запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="84306-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="84306-181">`Configuration`Метод запускает SignalR.</span><span class="sxs-lookup"><span data-stu-id="84306-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="84306-182">Протестируйте приложение в эмулятор Microsoft Azure, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="84306-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="84306-183">Если вы столкнулись с **FileLoadException** по адресу **мапсигналр**, измените перенаправления привязки в *web.config* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="84306-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="84306-184">Подождите примерно одну минуту.</span><span class="sxs-lookup"><span data-stu-id="84306-184">Wait about one minute.</span></span> <span data-ttu-id="84306-185">Откройте окно инструментов Cloud Explorer в Visual Studio (**View**  >  **Cloud Explorer**) и разверните путь `(Local)/Storage Accounts/(Development)/Tables` .</span><span class="sxs-lookup"><span data-stu-id="84306-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="84306-186">Дважды щелкните **WADPerformanceCountersTable**.</span><span class="sxs-lookup"><span data-stu-id="84306-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="84306-187">Счетчики SignalR должны отображаться в табличных данных.</span><span class="sxs-lookup"><span data-stu-id="84306-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="84306-188">Если таблица не отображается, может потребоваться повторно ввести учетные данные службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="84306-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="84306-189">Может потребоваться нажать кнопку **Обновить** , чтобы просмотреть таблицу в **Cloud Explorer** или нажать кнопку **Обновить** в окне Открытие таблицы, чтобы просмотреть данные в таблице.</span><span class="sxs-lookup"><span data-stu-id="84306-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Выбор таблицы счетчиков производительности WAD в Visual Studio Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![Отображение счетчиков, собранных в таблице счетчиков производительности WAD](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="84306-192">Чтобы протестировать приложение в облаке, обновите файл **ServiceConfiguration. Cloud. cscfg** и задайте `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` для него допустимую строку подключения к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="84306-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="84306-193">Разверните приложение в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="84306-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="84306-194">Дополнительные сведения о развертывании приложения в Azure см. в статье [Создание и развертывание облачной службы](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="84306-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="84306-195">Подождите несколько минут.</span><span class="sxs-lookup"><span data-stu-id="84306-195">Wait a few minutes.</span></span> <span data-ttu-id="84306-196">В **Cloud Explorer**найдите учетную запись хранения, настроенную выше, и найдите `WADPerformanceCountersTable` в ней таблицу.</span><span class="sxs-lookup"><span data-stu-id="84306-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="84306-197">Счетчики SignalR должны отображаться в табличных данных.</span><span class="sxs-lookup"><span data-stu-id="84306-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="84306-198">Если таблица не отображается, может потребоваться повторно ввести учетные данные службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="84306-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="84306-199">Может потребоваться нажать кнопку **Обновить** , чтобы просмотреть таблицу в **Cloud Explorer** или нажать кнопку **Обновить** в окне Открытие таблицы, чтобы просмотреть данные в таблице.</span><span class="sxs-lookup"><span data-stu-id="84306-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="84306-200">Для первоначального содержимого, используемого в этом учебнике, особое внимание [соследуется](https://social.msdn.microsoft.com/profile/Martin+Richard) спасибо.</span><span class="sxs-lookup"><span data-stu-id="84306-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
