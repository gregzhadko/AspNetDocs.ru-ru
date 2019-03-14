---
title: Непрерывная интеграция и развертывание — DevOps с помощью ASP.NET Core и Azure
author: CamSoper
description: Непрерывная интеграция и развертывание в DevOps с помощью ASP.NET Core и Azure
ms.author: scaddie
ms.date: 10/24/2018
ms.custom: seodec18
uid: azure/devops/cicd
ms.openlocfilehash: e5bddde41291c9573f58d749bbf830de9ea9319d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039331"
---
# <a name="continuous-integration-and-deployment"></a><span data-ttu-id="70906-103">Непрерывная интеграция и развертывание</span><span class="sxs-lookup"><span data-stu-id="70906-103">Continuous integration and deployment</span></span>

<span data-ttu-id="70906-104">В предыдущей главе вы создали локальный репозиторий Git для приложения для чтения простого веб-канала.</span><span class="sxs-lookup"><span data-stu-id="70906-104">In the previous chapter, you created a local Git repository for the Simple Feed Reader app.</span></span> <span data-ttu-id="70906-105">В этой главе будут публиковать этого кода в репозитории GitHub, а также создание конвейере DevOps служб Azure с помощью конвейеров в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-105">In this chapter, you'll publish that code to a GitHub repository and construct an Azure DevOps Services pipeline using Azure Pipelines.</span></span> <span data-ttu-id="70906-106">Конвейер позволяет непрерывного выполнения сборки и развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-106">The pipeline enables continuous builds and deployments of the app.</span></span> <span data-ttu-id="70906-107">Любой фиксации в репозиторий GitHub активирует сборку и развертывание в промежуточный слот веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-107">Any commit to the GitHub repository triggers a build and a deployment to the Azure Web App's staging slot.</span></span>

<span data-ttu-id="70906-108">В этом разделе вы выполните следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="70906-108">In this section, you'll complete the following tasks:</span></span>

* <span data-ttu-id="70906-109">Публикация в код приложения на GitHub</span><span class="sxs-lookup"><span data-stu-id="70906-109">Publish the app's code to GitHub</span></span>
* <span data-ttu-id="70906-110">Отключить развертывание локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="70906-110">Disconnect local Git deployment</span></span>
* <span data-ttu-id="70906-111">Создать организацию Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="70906-111">Create an Azure DevOps organization</span></span>
* <span data-ttu-id="70906-112">Создание командного проекта в службах Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="70906-112">Create a team project in Azure DevOps Services</span></span>
* <span data-ttu-id="70906-113">Создание определения построения</span><span class="sxs-lookup"><span data-stu-id="70906-113">Create a build definition</span></span>
* <span data-ttu-id="70906-114">Создать конвейер выпуска</span><span class="sxs-lookup"><span data-stu-id="70906-114">Create a release pipeline</span></span>
* <span data-ttu-id="70906-115">Зафиксировать изменения в GitHub и автоматически развернуть в Azure</span><span class="sxs-lookup"><span data-stu-id="70906-115">Commit changes to GitHub and automatically deploy to Azure</span></span>
* <span data-ttu-id="70906-116">Изучите Azure конвейеры конвейера</span><span class="sxs-lookup"><span data-stu-id="70906-116">Examine the Azure Pipelines pipeline</span></span>

## <a name="publish-the-apps-code-to-github"></a><span data-ttu-id="70906-117">Публикация в код приложения на GitHub</span><span class="sxs-lookup"><span data-stu-id="70906-117">Publish the app's code to GitHub</span></span>

1. <span data-ttu-id="70906-118">Откройте окно браузера и перейдите к `https://github.com`.</span><span class="sxs-lookup"><span data-stu-id="70906-118">Open a browser window, and navigate to `https://github.com`.</span></span>
1. <span data-ttu-id="70906-119">Нажмите кнопку **+** раскрывающегося списка в заголовке, а затем выберите **новый репозиторий**:</span><span class="sxs-lookup"><span data-stu-id="70906-119">Click the **+** drop-down in the header, and select **New repository**:</span></span>

    ![Параметр новый репозиторий GitHub](media/cicd/github-new-repo.png)

1. <span data-ttu-id="70906-121">Выберите свою учетную запись в **владельца** в раскрывающемся списке и введите *чтения simple потоков* в **имя репозитория** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="70906-121">Select your account in the **Owner** drop-down, and enter *simple-feed-reader* in the **Repository name** textbox.</span></span>
1. <span data-ttu-id="70906-122">Нажмите кнопку **Создать репозиторий** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-122">Click the **Create repository** button.</span></span>
1. <span data-ttu-id="70906-123">Откройте командную оболочку локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="70906-123">Open your local machine's command shell.</span></span> <span data-ttu-id="70906-124">Перейдите в каталог, в котором *чтения simple потоков* хранится репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="70906-124">Navigate to the directory in which the *simple-feed-reader* Git repository is stored.</span></span>
1. <span data-ttu-id="70906-125">Переименуйте существующий *origin* удаленное подключение к *вышестоящего*.</span><span class="sxs-lookup"><span data-stu-id="70906-125">Rename the existing *origin* remote to *upstream*.</span></span> <span data-ttu-id="70906-126">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="70906-126">Execute the following command:</span></span>
    ```console
    git remote rename origin upstream
    ```
1. <span data-ttu-id="70906-127">Добавьте новый *origin* удаленного указывает на копию репозитория на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-127">Add a new *origin* remote pointing to your copy of the repository on GitHub.</span></span> <span data-ttu-id="70906-128">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="70906-128">Execute the following command:</span></span>
    ```console
    git remote add origin https://github.com/<GitHub_username>/simple-feed-reader/
    ```
1. <span data-ttu-id="70906-129">Публикация локального репозитория Git на только что созданный репозиторий GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-129">Publish your local Git repository to the newly created GitHub repository.</span></span> <span data-ttu-id="70906-130">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="70906-130">Execute the following command:</span></span>
    ```console
    git push -u origin master
    ```
1. <span data-ttu-id="70906-131">Откройте окно браузера и перейдите к `https://github.com/<GitHub_username>/simple-feed-reader/`.</span><span class="sxs-lookup"><span data-stu-id="70906-131">Open a browser window, and navigate to `https://github.com/<GitHub_username>/simple-feed-reader/`.</span></span> <span data-ttu-id="70906-132">Проверьте, что ваш код отображается в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-132">Validate that your code appears in the GitHub repository.</span></span>

## <a name="disconnect-local-git-deployment"></a><span data-ttu-id="70906-133">Отключить развертывание локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="70906-133">Disconnect local Git deployment</span></span>

<span data-ttu-id="70906-134">Удалите локальное развертывание Git, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="70906-134">Remove the local Git deployment with the following steps.</span></span> <span data-ttu-id="70906-135">Конвейеры Azure (службу Azure DevOps) заменяет и расширяет эту функциональность.</span><span class="sxs-lookup"><span data-stu-id="70906-135">Azure Pipelines (an Azure DevOps service) both replaces and augments that functionality.</span></span>

1. <span data-ttu-id="70906-136">Откройте [портала Azure](https://portal.azure.com/)и перейдите к *промежуточных (mywebapp\<unique_number\>/промежуточные)* веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-136">Open the [Azure portal](https://portal.azure.com/), and navigate to the *staging (mywebapp\<unique_number\>/staging)* Web App.</span></span> <span data-ttu-id="70906-137">Веб-приложения можно быстро найти, введя *промежуточных* в поле поиска на портале:</span><span class="sxs-lookup"><span data-stu-id="70906-137">The Web App can be quickly located by entering *staging* in the portal's search box:</span></span>

    ![условие поиска для промежуточного веб-приложения](media/cicd/portal-search-box.png)

1. <span data-ttu-id="70906-139">Нажмите кнопку **варианты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="70906-139">Click **Deployment options**.</span></span> <span data-ttu-id="70906-140">Появится новая панель.</span><span class="sxs-lookup"><span data-stu-id="70906-140">A new panel appears.</span></span> <span data-ttu-id="70906-141">Нажмите кнопку **Disconnect** удалить локальную конфигурацию Git исходного элемента управления, добавленный в предыдущей главе.</span><span class="sxs-lookup"><span data-stu-id="70906-141">Click **Disconnect** to remove the local Git source control configuration that was added in the previous chapter.</span></span> <span data-ttu-id="70906-142">Подтвердить операцию удаления, щелкнув **Да** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-142">Confirm the removal operation by clicking the **Yes** button.</span></span>
1. <span data-ttu-id="70906-143">Перейдите к *mywebapp < unique_number >* службы приложений.</span><span class="sxs-lookup"><span data-stu-id="70906-143">Navigate to the *mywebapp<unique_number>* App Service.</span></span> <span data-ttu-id="70906-144">Напоминаем поле поиска на портале можно использовать для быстрого поиска в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="70906-144">As a reminder, the portal's search box can be used to quickly locate the App Service.</span></span>
1. <span data-ttu-id="70906-145">Нажмите кнопку **варианты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="70906-145">Click **Deployment options**.</span></span> <span data-ttu-id="70906-146">Появится новая панель.</span><span class="sxs-lookup"><span data-stu-id="70906-146">A new panel appears.</span></span> <span data-ttu-id="70906-147">Нажмите кнопку **Disconnect** удалить локальную конфигурацию Git исходного элемента управления, добавленный в предыдущей главе.</span><span class="sxs-lookup"><span data-stu-id="70906-147">Click **Disconnect** to remove the local Git source control configuration that was added in the previous chapter.</span></span> <span data-ttu-id="70906-148">Подтвердить операцию удаления, щелкнув **Да** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-148">Confirm the removal operation by clicking the **Yes** button.</span></span>

## <a name="create-an-azure-devops-organization"></a><span data-ttu-id="70906-149">Создать организацию Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="70906-149">Create an Azure DevOps organization</span></span>

1. <span data-ttu-id="70906-150">Откройте браузер и перейдите к [страницы создания организации Azure DevOps](https://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="70906-150">Open a browser, and navigate to the [Azure DevOps organization creation page](https://go.microsoft.com/fwlink/?LinkId=307137).</span></span>
1. <span data-ttu-id="70906-151">Введите уникальное имя в **выберите запоминающееся имя** textbox для формирования URL-адрес для доступа к вашей организации DevOps в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-151">Type a unique name into the **Pick a memorable name** textbox to form the URL for accessing your Azure DevOps organization.</span></span>
1. <span data-ttu-id="70906-152">Выберите **Git** "переключатель", так как код размещается в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-152">Select the **Git** radio button, since the code is hosted in a GitHub repository.</span></span>
1. <span data-ttu-id="70906-153">Нажмите кнопку **Continue** (Продолжить).</span><span class="sxs-lookup"><span data-stu-id="70906-153">Click the **Continue** button.</span></span> <span data-ttu-id="70906-154">После короткого ожидания, учетную запись и командный проект с именем *MyFirstProject*, создаются.</span><span class="sxs-lookup"><span data-stu-id="70906-154">After a short wait, an account and a team project, named *MyFirstProject*, are created.</span></span>

    ![Страница создания организации Azure DevOps](media/cicd/vsts-account-creation.png)

1. <span data-ttu-id="70906-156">Откройте по электронной почте подтверждение, указывающее на то, что организации DevOps в Azure и проекта будут готовы к использованию.</span><span class="sxs-lookup"><span data-stu-id="70906-156">Open the confirmation email indicating that the Azure DevOps organization and project are ready for use.</span></span> <span data-ttu-id="70906-157">Нажмите кнопку **запустить проект** кнопки:</span><span class="sxs-lookup"><span data-stu-id="70906-157">Click the **Start your project** button:</span></span>

    ![Ваш проект кнопка "Пуск"](media/cicd/vsts-start-project.png)

1. <span data-ttu-id="70906-159">Откроется в браузере  *\<account_name\>. visualstudio.com*.</span><span class="sxs-lookup"><span data-stu-id="70906-159">A browser opens to *\<account_name\>.visualstudio.com*.</span></span> <span data-ttu-id="70906-160">Нажмите кнопку *MyFirstProject* ссылку, чтобы приступить к настройке конвейера DevOps проекта.</span><span class="sxs-lookup"><span data-stu-id="70906-160">Click the *MyFirstProject* link to begin configuring the project's DevOps pipeline.</span></span>

## <a name="configure-the-azure-pipelines-pipeline"></a><span data-ttu-id="70906-161">Настройте конвейер конвейеры Azure</span><span class="sxs-lookup"><span data-stu-id="70906-161">Configure the Azure Pipelines pipeline</span></span>

<span data-ttu-id="70906-162">Существуют состоит из трех шагов для завершения.</span><span class="sxs-lookup"><span data-stu-id="70906-162">There are three distinct steps to complete.</span></span> <span data-ttu-id="70906-163">Выполнив действия, описанные в следующих трех разделов приводит работы конвейера DevOps.</span><span class="sxs-lookup"><span data-stu-id="70906-163">Completing the steps in the following three sections results in an operational DevOps pipeline.</span></span>

### <a name="grant-azure-devops-access-to-the-github-repository"></a><span data-ttu-id="70906-164">Предоставление Azure DevOps доступ к репозиторию GitHub</span><span class="sxs-lookup"><span data-stu-id="70906-164">Grant Azure DevOps access to the GitHub repository</span></span>

1. <span data-ttu-id="70906-165">Разверните **или выполнить сборку кода из внешнего репозитория** accordion.</span><span class="sxs-lookup"><span data-stu-id="70906-165">Expand the **or build code from an external repository** accordion.</span></span> <span data-ttu-id="70906-166">Нажмите кнопку **установки сборки** кнопки:</span><span class="sxs-lookup"><span data-stu-id="70906-166">Click the **Setup Build** button:</span></span>

    ![Кнопка настройки сборки](media/cicd/vsts-setup-build.png)

1. <span data-ttu-id="70906-168">Выберите **GitHub** вариант **выбрать источник** раздел:</span><span class="sxs-lookup"><span data-stu-id="70906-168">Select the **GitHub** option from the **Select a source** section:</span></span>

    ![Выберите источник - GitHub](media/cicd/vsts-select-source.png)

1. <span data-ttu-id="70906-170">Требуется авторизация для доступа к репозиторию GitHub DevOps в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-170">Authorization is required before Azure DevOps can access your GitHub repository.</span></span> <span data-ttu-id="70906-171">Введите *< GitHub_username > подключение GitHub* в **имя подключения** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="70906-171">Enter *<GitHub_username> GitHub connection* in the **Connection name** textbox.</span></span> <span data-ttu-id="70906-172">Пример:</span><span class="sxs-lookup"><span data-stu-id="70906-172">For example:</span></span>

    ![Имя подключения GitHub](media/cicd/vsts-repo-authz.png)

1. <span data-ttu-id="70906-174">Если двухфакторная проверка подлинности будет включен в вашей учетной записи GitHub, личный маркер доступа не требуется.</span><span class="sxs-lookup"><span data-stu-id="70906-174">If two-factor authentication is enabled on your GitHub account, a personal access token is required.</span></span> <span data-ttu-id="70906-175">В этом случае щелкните **авторизовать маркер личного доступа GitHub** ссылку.</span><span class="sxs-lookup"><span data-stu-id="70906-175">In that case, click the **Authorize with a GitHub personal access token** link.</span></span> <span data-ttu-id="70906-176">См. в разделе [официальной документации создания маркера личного доступа GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) для справки.</span><span class="sxs-lookup"><span data-stu-id="70906-176">See the [official GitHub personal access token creation instructions](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) for help.</span></span> <span data-ttu-id="70906-177">Только *репозитория* требуется область разрешений.</span><span class="sxs-lookup"><span data-stu-id="70906-177">Only the *repo* scope of permissions is needed.</span></span> <span data-ttu-id="70906-178">В противном случае нажмите **авторизация выполняется с использованием OAuth** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-178">Otherwise, click the **Authorize using OAuth** button.</span></span>
1. <span data-ttu-id="70906-179">Когда появится запрос, войдите в учетную запись GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-179">When prompted, sign in to your GitHub account.</span></span> <span data-ttu-id="70906-180">Затем выберите авторизовать для предоставления доступа к вашей организации DevOps в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-180">Then select Authorize to grant access to your Azure DevOps organization.</span></span> <span data-ttu-id="70906-181">В случае успешного выполнения создается новая конечная точка службы.</span><span class="sxs-lookup"><span data-stu-id="70906-181">If successful, a new service endpoint is created.</span></span>
1. <span data-ttu-id="70906-182">Нажмите кнопку с многоточием рядом с полем **репозитория** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-182">Click the ellipsis button next to the **Repository** button.</span></span> <span data-ttu-id="70906-183">Выберите *< GitHub_username > / чтения simple потоков* репозитория из списка.</span><span class="sxs-lookup"><span data-stu-id="70906-183">Select the *<GitHub_username>/simple-feed-reader* repository from the list.</span></span> <span data-ttu-id="70906-184">Нажмите кнопку **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-184">Click the **Select** button.</span></span>
1. <span data-ttu-id="70906-185">Выберите *master* ветвь из **ветвь по умолчанию для сборок вручную и по расписанию** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-185">Select the *master* branch from the **Default branch for manual and scheduled builds** drop-down.</span></span> <span data-ttu-id="70906-186">Нажмите кнопку **Continue** (Продолжить).</span><span class="sxs-lookup"><span data-stu-id="70906-186">Click the **Continue** button.</span></span> <span data-ttu-id="70906-187">Откроется страница выбора шаблона.</span><span class="sxs-lookup"><span data-stu-id="70906-187">The template selection page appears.</span></span>

### <a name="create-the-build-definition"></a><span data-ttu-id="70906-188">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="70906-188">Create the build definition</span></span>

1. <span data-ttu-id="70906-189">На странице выбора шаблона, ввести *ASP.NET Core* в поле поиска:</span><span class="sxs-lookup"><span data-stu-id="70906-189">From the template selection page, enter *ASP.NET Core* in the search box:</span></span>

    ![ASP.NET Core поиска на странице шаблона](media/cicd/vsts-template-selection.png)

1. <span data-ttu-id="70906-191">Результаты поиска шаблона отображаются.</span><span class="sxs-lookup"><span data-stu-id="70906-191">The template search results appear.</span></span> <span data-ttu-id="70906-192">Наведите указатель мыши **ASP.NET Core** шаблона и нажмите кнопку **применить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-192">Hover over the **ASP.NET Core** template, and click the **Apply** button.</span></span>
1. <span data-ttu-id="70906-193">**Задачи** появится вкладка определения построения.</span><span class="sxs-lookup"><span data-stu-id="70906-193">The **Tasks** tab of the build definition appears.</span></span> <span data-ttu-id="70906-194">Перейдите на вкладку **Триггеры** .</span><span class="sxs-lookup"><span data-stu-id="70906-194">Click the **Triggers** tab.</span></span>
1. <span data-ttu-id="70906-195">Проверьте **непрерывной интеграции** поле.</span><span class="sxs-lookup"><span data-stu-id="70906-195">Check the **Enable continuous integration** box.</span></span> <span data-ttu-id="70906-196">В разделе **фильтры ветвей** разделе, убедитесь, что **тип** раскрывающегося списка присваивается *Include*.</span><span class="sxs-lookup"><span data-stu-id="70906-196">Under the **Branch filters** section, confirm that the **Type** drop-down is set to *Include*.</span></span> <span data-ttu-id="70906-197">Задайте **спецификация ветви** раскрывающийся список, чтобы *master*.</span><span class="sxs-lookup"><span data-stu-id="70906-197">Set the **Branch specification** drop-down to *master*.</span></span>

    ![Включение параметров непрерывной интеграции](media/cicd/vsts-enable-ci.png)

    <span data-ttu-id="70906-199">Эти параметры предписывают построения для запуска при передаче любое изменение *master* ветвь репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-199">These settings cause a build to trigger when any change is pushed to the *master* branch of the GitHub repository.</span></span> <span data-ttu-id="70906-200">Непрерывная интеграция тестируется в [фиксации изменений в GitHub и автоматическое развертывание в Azure](#commit-changes-to-github-and-automatically-deploy-to-azure) раздел.</span><span class="sxs-lookup"><span data-stu-id="70906-200">Continuous integration is tested in the [Commit changes to GitHub and automatically deploy to Azure](#commit-changes-to-github-and-automatically-deploy-to-azure) section.</span></span>

1. <span data-ttu-id="70906-201">Нажмите кнопку **сохранить и поместить в очередь** и выберите **Сохранить** параметр:</span><span class="sxs-lookup"><span data-stu-id="70906-201">Click the **Save & queue** button, and select the **Save** option:</span></span>

    ![Кнопка "Сохранить"](media/cicd/vsts-save-build.png)

1. <span data-ttu-id="70906-203">Появится следующее модальное диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="70906-203">The following modal dialog appears:</span></span>

    ![Сохраните определение сборки - модальное диалоговое окно](media/cicd/vsts-save-modal.png)

    <span data-ttu-id="70906-205">Использовать папку по умолчанию из *\\* и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-205">Use the default folder of *\\*, and click the **Save** button.</span></span>

### <a name="create-the-release-pipeline"></a><span data-ttu-id="70906-206">Создайте конвейер выпусков</span><span class="sxs-lookup"><span data-stu-id="70906-206">Create the release pipeline</span></span>

1. <span data-ttu-id="70906-207">Нажмите кнопку **выпуски** вкладке командного проекта.</span><span class="sxs-lookup"><span data-stu-id="70906-207">Click the **Releases** tab of your team project.</span></span> <span data-ttu-id="70906-208">Нажмите кнопку **новый конвейер** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-208">Click the **New pipeline** button.</span></span>

    ![Вкладка "выпуски" — Кнопка "Создать определение"](media/cicd/vsts-new-release-definition.png)

    <span data-ttu-id="70906-210">Откроется панель выбора шаблона.</span><span class="sxs-lookup"><span data-stu-id="70906-210">The template selection pane appears.</span></span>

1. <span data-ttu-id="70906-211">На странице выбора шаблона, ввести *службы приложений* в поле поиска:</span><span class="sxs-lookup"><span data-stu-id="70906-211">From the template selection page, enter *App Service* in the search box:</span></span>

    ![Поле поиска шаблона конвейер выпуска](media/cicd/vsts-release-template-search.png)

1. <span data-ttu-id="70906-213">Результаты поиска шаблона отображаются.</span><span class="sxs-lookup"><span data-stu-id="70906-213">The template search results appear.</span></span> <span data-ttu-id="70906-214">Наведите указатель мыши **развертывание службы приложений Azure с помощью слота** шаблона и нажмите кнопку **применить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-214">Hover over the **Azure App Service Deployment with Slot** template, and click the **Apply** button.</span></span> <span data-ttu-id="70906-215">**Конвейера** появится вкладка конвейера выпуска.</span><span class="sxs-lookup"><span data-stu-id="70906-215">The **Pipeline** tab of the release pipeline appears.</span></span>

    ![Конвейер выпуска вкладку конвейера](media/cicd/vsts-release-definition-pipeline.png)

1. <span data-ttu-id="70906-217">Нажмите кнопку **добавить** кнопку **артефакты** поле.</span><span class="sxs-lookup"><span data-stu-id="70906-217">Click the **Add** button in the **Artifacts** box.</span></span> <span data-ttu-id="70906-218">**Добавление артефакта** появится панель:</span><span class="sxs-lookup"><span data-stu-id="70906-218">The **Add artifact** panel appears:</span></span>

    ![Конвейер выпуска - артефакта панель добавления](media/cicd/vsts-release-add-artifact.png)

1. <span data-ttu-id="70906-220">Выберите **построения** плитку **типа источника** раздел.</span><span class="sxs-lookup"><span data-stu-id="70906-220">Select the **Build** tile from the **Source type** section.</span></span> <span data-ttu-id="70906-221">Этот тип обеспечивает создание ссылок конвейер выпуска в определение сборки.</span><span class="sxs-lookup"><span data-stu-id="70906-221">This type allows for the linking of the release pipeline to the build definition.</span></span>
1. <span data-ttu-id="70906-222">Выберите *MyFirstProject* из **проекта** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-222">Select *MyFirstProject* from the **Project** drop-down.</span></span>
1. <span data-ttu-id="70906-223">Выберите имя определения построения *MyFirstProject ASP.NET Core-CI*, из **источник (определение сборки)** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-223">Select the build definition name, *MyFirstProject-ASP.NET Core-CI*, from the **Source (Build definition)** drop-down.</span></span>
1. <span data-ttu-id="70906-224">Выберите *последнюю* из **версия по умолчанию** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-224">Select *Latest* from the **Default version** drop-down.</span></span> <span data-ttu-id="70906-225">Этот параметр создает артефакты, созданные последним запуском определения построения.</span><span class="sxs-lookup"><span data-stu-id="70906-225">This option builds the artifacts produced by the latest run of the build definition.</span></span>
1. <span data-ttu-id="70906-226">Замените текст в **псевдоним источника** textbox с *Drop*.</span><span class="sxs-lookup"><span data-stu-id="70906-226">Replace the text in the **Source alias** textbox with *Drop*.</span></span>
1. <span data-ttu-id="70906-227">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="70906-227">Click the **Add** button.</span></span> <span data-ttu-id="70906-228">**Артефакты** разделе обновлений для отображения изменений.</span><span class="sxs-lookup"><span data-stu-id="70906-228">The **Artifacts** section updates to display the changes.</span></span>
1. <span data-ttu-id="70906-229">Щелкните значок с молнией, чтобы включить непрерывное развертывание на:</span><span class="sxs-lookup"><span data-stu-id="70906-229">Click the lightning bolt icon to enable continuous deployments:</span></span>

    ![Артефакты — значок с изображением молнии. конвейер выпуска](media/cicd/vsts-artifacts-lightning-bolt.png)

    <span data-ttu-id="70906-231">Этот параметр включен развертывание происходит каждый раз, когда становится доступной новая сборка.</span><span class="sxs-lookup"><span data-stu-id="70906-231">With this option enabled, a deployment occurs each time a new build is available.</span></span>
1. <span data-ttu-id="70906-232">Объект **триггер непрерывного развертывания** панели справа.</span><span class="sxs-lookup"><span data-stu-id="70906-232">A **Continuous deployment trigger** panel appears to the right.</span></span> <span data-ttu-id="70906-233">Чтобы включить эту функцию, нажмите кнопку переключателя.</span><span class="sxs-lookup"><span data-stu-id="70906-233">Click the toggle button to enable the feature.</span></span> <span data-ttu-id="70906-234">Это необязательно включить **триггер запроса на включение внесенных изменений**.</span><span class="sxs-lookup"><span data-stu-id="70906-234">It isn't necessary to enable the **Pull request trigger**.</span></span>
1. <span data-ttu-id="70906-235">Нажмите кнопку **добавить** раскрывающееся меню в **фильтры ветви сборки** раздел.</span><span class="sxs-lookup"><span data-stu-id="70906-235">Click the **Add** drop-down in the **Build branch filters** section.</span></span> <span data-ttu-id="70906-236">Выберите **ветвь по умолчанию определение построения** параметр.</span><span class="sxs-lookup"><span data-stu-id="70906-236">Choose the **Build Definition's default branch** option.</span></span> <span data-ttu-id="70906-237">Этот фильтр вызывает выпуска для активации только для сборок из репозитория GitHub *master* ветви.</span><span class="sxs-lookup"><span data-stu-id="70906-237">This filter causes the release to trigger only for a build from the GitHub repository's *master* branch.</span></span>
1. <span data-ttu-id="70906-238">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="70906-238">Click the **Save** button.</span></span> <span data-ttu-id="70906-239">Нажмите кнопку **ОК** кнопки в итоговом **Сохранить** модальное диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="70906-239">Click the **OK** button in the resulting **Save** modal dialog.</span></span>
1. <span data-ttu-id="70906-240">Нажмите кнопку **среду 1** поле.</span><span class="sxs-lookup"><span data-stu-id="70906-240">Click the **Environment 1** box.</span></span> <span data-ttu-id="70906-241">**Среды** панели справа.</span><span class="sxs-lookup"><span data-stu-id="70906-241">An **Environment** panel appears to the right.</span></span> <span data-ttu-id="70906-242">Изменение *среду 1* текста в **имя среды** textbox для *рабочей*.</span><span class="sxs-lookup"><span data-stu-id="70906-242">Change the *Environment 1* text in the **Environment name** textbox to *Production*.</span></span>

   ![Конвейер выпуска - текстовое имя среды](media/cicd/vsts-environment-name-textbox.png)

1. <span data-ttu-id="70906-244">Нажмите кнопку **этапа 1, 2 задачи** ссылку в **рабочей** поле:</span><span class="sxs-lookup"><span data-stu-id="70906-244">Click the **1 phase, 2 tasks** link in the **Production** box:</span></span>

    ![Конвейер выпуска - link.png рабочей среды](media/cicd/vsts-production-link.png)

    <span data-ttu-id="70906-246">**Задачи** появится вкладка среды.</span><span class="sxs-lookup"><span data-stu-id="70906-246">The **Tasks** tab of the environment appears.</span></span>
1. <span data-ttu-id="70906-247">Нажмите кнопку **развернуть службу приложений Azure для слота** задачи.</span><span class="sxs-lookup"><span data-stu-id="70906-247">Click the **Deploy Azure App Service to Slot** task.</span></span> <span data-ttu-id="70906-248">Его параметры отображаются на панели справа.</span><span class="sxs-lookup"><span data-stu-id="70906-248">Its settings appear in a panel to the right.</span></span>
1. <span data-ttu-id="70906-249">Выберите подписку Azure, связанные со службой приложений из **подписки Azure** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-249">Select the Azure subscription associated with the App Service from the **Azure subscription** drop-down.</span></span> <span data-ttu-id="70906-250">После выбора нажмите кнопку **Authorize** кнопки.</span><span class="sxs-lookup"><span data-stu-id="70906-250">Once selected, click the **Authorize** button.</span></span>
1. <span data-ttu-id="70906-251">Выберите *веб-приложения* из **тип приложения** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-251">Select *Web App* from the **App type** drop-down.</span></span>
1. <span data-ttu-id="70906-252">Выберите *mywebapp / < unique_number / >* из **имя службы приложений** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-252">Select *mywebapp/<unique_number/>* from the **App service name** drop-down.</span></span>
1. <span data-ttu-id="70906-253">Выберите *AzureTutorial* из **группы ресурсов** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-253">Select *AzureTutorial* from the **Resource group** drop-down.</span></span>
1. <span data-ttu-id="70906-254">Выберите *промежуточных* из **слот** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="70906-254">Select *staging* from the **Slot** drop-down.</span></span>
1. <span data-ttu-id="70906-255">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="70906-255">Click the **Save** button.</span></span>
1. <span data-ttu-id="70906-256">Наведите указатель на имя конвейера выпуска по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="70906-256">Hover over the default release pipeline name.</span></span> <span data-ttu-id="70906-257">Щелкните значок карандаша, чтобы изменить его.</span><span class="sxs-lookup"><span data-stu-id="70906-257">Click the pencil icon to edit it.</span></span> <span data-ttu-id="70906-258">Используйте *MyFirstProject-Core-компакт-ДИСК ASP.NET* как имя.</span><span class="sxs-lookup"><span data-stu-id="70906-258">Use *MyFirstProject-ASP.NET Core-CD* as the name.</span></span>

    ![Имя конвейера выпуска](media/cicd/vsts-release-definition-name.png)

1. <span data-ttu-id="70906-260">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="70906-260">Click the **Save** button.</span></span>

## <a name="commit-changes-to-github-and-automatically-deploy-to-azure"></a><span data-ttu-id="70906-261">Зафиксировать изменения в GitHub и автоматически развернуть в Azure</span><span class="sxs-lookup"><span data-stu-id="70906-261">Commit changes to GitHub and automatically deploy to Azure</span></span>

1. <span data-ttu-id="70906-262">Откройте *SimpleFeedReader.sln* в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70906-262">Open *SimpleFeedReader.sln* in Visual Studio.</span></span>
1. <span data-ttu-id="70906-263">В обозревателе решений откройте *Pages\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="70906-263">In Solution Explorer, open *Pages\Index.cshtml*.</span></span> <span data-ttu-id="70906-264">Изменение `<h2>Simple Feed Reader - V3</h2>` для `<h2>Simple Feed Reader - V4</h2>`.</span><span class="sxs-lookup"><span data-stu-id="70906-264">Change `<h2>Simple Feed Reader - V3</h2>` to `<h2>Simple Feed Reader - V4</h2>`.</span></span>
1. <span data-ttu-id="70906-265">Нажмите клавишу **Ctrl**+**Shift**+**B** для сборки приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-265">Press **Ctrl**+**Shift**+**B** to build the app.</span></span>
1. <span data-ttu-id="70906-266">Зафиксируйте файл в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-266">Commit the file to the GitHub repository.</span></span> <span data-ttu-id="70906-267">Использовать **изменения** страницы в Visual Studio *Team Explorer* вкладку или выполнить следующую процедуру с помощью командной оболочки на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="70906-267">Use either the **Changes** page in Visual Studio's *Team Explorer* tab, or execute the following using the local machine's command shell:</span></span>

    ```console
    git commit -a -m "upgraded to V4"
    ```
1. <span data-ttu-id="70906-268">Отправка изменений *master* ветви *origin* удаленный репозиторий GitHub:</span><span class="sxs-lookup"><span data-stu-id="70906-268">Push the change in the *master* branch to the *origin* remote of your GitHub repository:</span></span>

    ```console
    git push origin master
    ```

    <span data-ttu-id="70906-269">Фиксация появляется в репозитории GitHub *master* ветви:</span><span class="sxs-lookup"><span data-stu-id="70906-269">The commit appears in the GitHub repository's *master* branch:</span></span>

    ![Фиксации GitHub в главной ветви](media/cicd/github-commit.png)

    <span data-ttu-id="70906-271">Сборка запускается, поскольку непрерывной интеграции включена в определении сборки **триггеры** вкладке:</span><span class="sxs-lookup"><span data-stu-id="70906-271">The build is triggered, since continuous integration is enabled in the build definition's **Triggers** tab:</span></span>

    ![включить непрерывную интеграцию](media/cicd/enable-ci.png)

1. <span data-ttu-id="70906-273">Перейдите к **в очереди** вкладке **конвейеры Azure** > **построения** страницы в службах Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="70906-273">Navigate to the **Queued** tab of the **Azure Pipelines** > **Builds** page in Azure DevOps Services.</span></span> <span data-ttu-id="70906-274">Построения в очереди показывает ветви и фиксации, запустившей сборки:</span><span class="sxs-lookup"><span data-stu-id="70906-274">The queued build shows the branch and commit that triggered the build:</span></span>

    ![построения в очереди](media/cicd/build-queued.png)

1. <span data-ttu-id="70906-276">После успешного построения, развертывания в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-276">Once the build succeeds, a deployment to Azure occurs.</span></span> <span data-ttu-id="70906-277">Перейдите к приложению в браузере.</span><span class="sxs-lookup"><span data-stu-id="70906-277">Navigate to the app in the browser.</span></span> <span data-ttu-id="70906-278">Обратите внимание на то, что текст «V4» отображается в заголовке:</span><span class="sxs-lookup"><span data-stu-id="70906-278">Notice that the "V4" text appears in the heading:</span></span>

    ![обновленное приложение](media/cicd/updated-app-v4.png)

## <a name="examine-the-azure-pipelines-pipeline"></a><span data-ttu-id="70906-280">Изучите Azure конвейеры конвейера</span><span class="sxs-lookup"><span data-stu-id="70906-280">Examine the Azure Pipelines pipeline</span></span>

### <a name="build-definition"></a><span data-ttu-id="70906-281">Определение сборки</span><span class="sxs-lookup"><span data-stu-id="70906-281">Build definition</span></span>

<span data-ttu-id="70906-282">Определение сборки был создан с именем *MyFirstProject ASP.NET Core-CI*.</span><span class="sxs-lookup"><span data-stu-id="70906-282">A build definition was created with the name *MyFirstProject-ASP.NET Core-CI*.</span></span> <span data-ttu-id="70906-283">По завершении построения создает *ZIP-файл* файла, включая ресурсы для публикации.</span><span class="sxs-lookup"><span data-stu-id="70906-283">Upon completion, the build produces a *.zip* file including the assets to be published.</span></span> <span data-ttu-id="70906-284">Конвейер выпуска развертывает эти ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-284">The release pipeline deploys those assets to Azure.</span></span>

<span data-ttu-id="70906-285">Определение сборки **задачи** вкладке перечислены отдельных действий.</span><span class="sxs-lookup"><span data-stu-id="70906-285">The build definition's **Tasks** tab lists the individual steps being used.</span></span> <span data-ttu-id="70906-286">Есть пять задач сборки.</span><span class="sxs-lookup"><span data-stu-id="70906-286">There are five build tasks.</span></span>

![задачи определения сборки](media/cicd/build-definition-tasks.png)

1. <span data-ttu-id="70906-288">**Восстановление** &mdash; интерфейсов `dotnet restore` команду, чтобы восстановить пакеты NuGet приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-288">**Restore** &mdash; Executes the `dotnet restore` command to restore the app's NuGet packages.</span></span> <span data-ttu-id="70906-289">Пакет по умолчанию канал, используемый является nuget.org.</span><span class="sxs-lookup"><span data-stu-id="70906-289">The default package feed used is nuget.org.</span></span>
1. <span data-ttu-id="70906-290">**Построение** &mdash; интерфейсов `dotnet build --configuration release` команду для компиляции в код приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-290">**Build** &mdash; Executes the `dotnet build --configuration release` command to compile the app's code.</span></span> <span data-ttu-id="70906-291">Это `--configuration` параметр используется для создания оптимизированной версии кода, который подходит для развертывания в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="70906-291">This `--configuration` option is used to produce an optimized version of the code, which is suitable for deployment to a production environment.</span></span> <span data-ttu-id="70906-292">Изменить *BuildConfiguration* переменных с определением сборки **переменных** вкладку, например, конфигурации отладки при необходимости.</span><span class="sxs-lookup"><span data-stu-id="70906-292">Modify the *BuildConfiguration* variable on the build definition's **Variables** tab if, for example, a debug configuration is needed.</span></span>
1. <span data-ttu-id="70906-293">**Тест** &mdash; интерфейсов `dotnet test --configuration release --logger trx --results-directory <local_path_on_build_agent>` команду для запуска модульных тестов приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-293">**Test** &mdash; Executes the `dotnet test --configuration release --logger trx --results-directory <local_path_on_build_agent>` command to run the app's unit tests.</span></span> <span data-ttu-id="70906-294">Модульные тесты выполняются в рамках любого C# проект сопоставления `**/*Tests/*.csproj` маски.</span><span class="sxs-lookup"><span data-stu-id="70906-294">Unit tests are executed within any C# project matching the `**/*Tests/*.csproj` glob pattern.</span></span> <span data-ttu-id="70906-295">Результаты теста сохраняются в *.trx* файл в расположении, заданном параметром `--results-directory` параметр.</span><span class="sxs-lookup"><span data-stu-id="70906-295">Test results are saved in a *.trx* file at the location specified by the `--results-directory` option.</span></span> <span data-ttu-id="70906-296">Если не все тесты, сборка завершается ошибкой и не был развернут.</span><span class="sxs-lookup"><span data-stu-id="70906-296">If any tests fail, the build fails and isn't deployed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="70906-297">Чтобы проверить работу модульные тесты, измените *SimpleFeedReader.Tests\Services\NewsServiceTests.cs* намеренно прервать один из тестов.</span><span class="sxs-lookup"><span data-stu-id="70906-297">To verify the unit tests work, modify *SimpleFeedReader.Tests\Services\NewsServiceTests.cs* to purposefully break one of the tests.</span></span> <span data-ttu-id="70906-298">Например, измените `Assert.True(result.Count > 0);` для `Assert.False(result.Count > 0);` в `Returns_News_Stories_Given_Valid_Uri` метод.</span><span class="sxs-lookup"><span data-stu-id="70906-298">For example, change `Assert.True(result.Count > 0);` to `Assert.False(result.Count > 0);` in the `Returns_News_Stories_Given_Valid_Uri` method.</span></span> <span data-ttu-id="70906-299">Зафиксируйте и отправьте изменения в GitHub.</span><span class="sxs-lookup"><span data-stu-id="70906-299">Commit and push the change to GitHub.</span></span> <span data-ttu-id="70906-300">Сборка запускается и завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="70906-300">The build is triggered and fails.</span></span> <span data-ttu-id="70906-301">Состояние конвейера сборки меняется на **сбой**.</span><span class="sxs-lookup"><span data-stu-id="70906-301">The build pipeline status changes to **failed**.</span></span> <span data-ttu-id="70906-302">Снова вернуться изменений, фиксации и отправки.</span><span class="sxs-lookup"><span data-stu-id="70906-302">Revert the change, commit, and push again.</span></span> <span data-ttu-id="70906-303">Сборка будет завершена.</span><span class="sxs-lookup"><span data-stu-id="70906-303">The build succeeds.</span></span>

1. <span data-ttu-id="70906-304">**Публикация** &mdash; интерфейсов `dotnet publish --configuration release --output <local_path_on_build_agent>` команду, чтобы создать *ZIP-файл* файл с артефактами, которые должны быть развернуты.</span><span class="sxs-lookup"><span data-stu-id="70906-304">**Publish** &mdash; Executes the `dotnet publish --configuration release --output <local_path_on_build_agent>` command to produce a *.zip* file with the artifacts to be deployed.</span></span> <span data-ttu-id="70906-305">`--output` Параметр указывает расположение публикации *ZIP-файл* файл.</span><span class="sxs-lookup"><span data-stu-id="70906-305">The `--output` option specifies the publish location of the *.zip* file.</span></span> <span data-ttu-id="70906-306">Что расположение задается путем передачи [Предопределенная переменная](/azure/devops/pipelines/build/variables) с именем `$(build.artifactstagingdirectory)`.</span><span class="sxs-lookup"><span data-stu-id="70906-306">That location is specified by passing a [predefined variable](/azure/devops/pipelines/build/variables) named `$(build.artifactstagingdirectory)`.</span></span> <span data-ttu-id="70906-307">Эту переменную при развертывании по локальному пути, такие как *c:\agent\_work\1\a*, на агенте построения.</span><span class="sxs-lookup"><span data-stu-id="70906-307">That variable expands to a local path, such as *c:\agent\_work\1\a*, on the build agent.</span></span>
1. <span data-ttu-id="70906-308">**Публикация артефакта** &mdash; Publishes *ZIP-файл* файлы, созданные функцией **публикации** задачи.</span><span class="sxs-lookup"><span data-stu-id="70906-308">**Publish Artifact** &mdash; Publishes the *.zip* file produced by the **Publish** task.</span></span> <span data-ttu-id="70906-309">Задача принимает *ZIP-файл* расположение в качестве параметра, которое предварительно определенных файла `$(build.artifactstagingdirectory)`.</span><span class="sxs-lookup"><span data-stu-id="70906-309">The task accepts the *.zip* file location as a parameter, which is the predefined variable `$(build.artifactstagingdirectory)`.</span></span> <span data-ttu-id="70906-310">*ZIP-файл* опубликован файл в папку с именем *drop*.</span><span class="sxs-lookup"><span data-stu-id="70906-310">The *.zip* file is published as a folder named *drop*.</span></span>

<span data-ttu-id="70906-311">Выберите определение сборки **Сводка** ссылку, чтобы просмотреть журнал сборок с определением:</span><span class="sxs-lookup"><span data-stu-id="70906-311">Click the build definition's **Summary** link to view a history of builds with the definition:</span></span>

![Снимок экрана: отображение построения определения журнала](media/cicd/build-definition-summary.png)

<span data-ttu-id="70906-313">На соответствующей странице щелкните ссылку, соответствующую уникальный номер:</span><span class="sxs-lookup"><span data-stu-id="70906-313">On the resulting page, click the link corresponding to the unique build number:</span></span>

![Страница сводки определения сборки отображение экрана](media/cicd/build-definition-completed.png)

<span data-ttu-id="70906-315">Отображается сводка этой конкретной сборки.</span><span class="sxs-lookup"><span data-stu-id="70906-315">A summary of this specific build is displayed.</span></span> <span data-ttu-id="70906-316">Нажмите кнопку **артефакты** вкладку и обратите внимание, *drop* указана папка, созданного посредством сборки:</span><span class="sxs-lookup"><span data-stu-id="70906-316">Click the **Artifacts** tab, and notice the *drop* folder produced by the build is listed:</span></span>

![Снимок экрана, показывающий определения артефактов построения - транзитный каталог](media/cicd/build-definition-artifacts.png)

<span data-ttu-id="70906-318">Используйте **загрузить** и **Проводник** ссылки для проверки опубликованного артефакты.</span><span class="sxs-lookup"><span data-stu-id="70906-318">Use the **Download** and **Explore** links to inspect the published artifacts.</span></span>

### <a name="release-pipeline"></a><span data-ttu-id="70906-319">Конвейер выпуска</span><span class="sxs-lookup"><span data-stu-id="70906-319">Release pipeline</span></span>

<span data-ttu-id="70906-320">Конвейер выпуска был создан с именем *MyFirstProject-Core-компакт-ДИСК ASP.NET*:</span><span class="sxs-lookup"><span data-stu-id="70906-320">A release pipeline was created with the name *MyFirstProject-ASP.NET Core-CD*:</span></span>

![Общие сведения о конвейере выпуска отображение экрана](media/cicd/release-definition-overview.png)

<span data-ttu-id="70906-322">Два основных компонента конвейера выпуска **артефакты** и **сред**.</span><span class="sxs-lookup"><span data-stu-id="70906-322">The two major components of the release pipeline are the **Artifacts** and the **Environments**.</span></span> <span data-ttu-id="70906-323">При нажатии блока в **артефакты** раздел показывает следующие панели:</span><span class="sxs-lookup"><span data-stu-id="70906-323">Clicking the box in the **Artifacts** section reveals the following panel:</span></span>

![Снимок экрана: отображение выпуска конвейера артефактов](media/cicd/release-definition-artifacts.png)

<span data-ttu-id="70906-325">**Источник (определение сборки)** значение представляет определение сборки, с которым связан этот конвейер выпуска.</span><span class="sxs-lookup"><span data-stu-id="70906-325">The **Source (Build definition)** value represents the build definition to which this release pipeline is linked.</span></span> <span data-ttu-id="70906-326">*ZIP-файл* предоставляется файл, созданный при успешном выполнении определения построения *рабочей* среду для развертывания в Azure.</span><span class="sxs-lookup"><span data-stu-id="70906-326">The *.zip* file produced by a successful run of the build definition is provided to the *Production* environment for deployment to Azure.</span></span> <span data-ttu-id="70906-327">Нажмите кнопку *этапа 1, 2 задачи* ссылку в *рабочей* "среды" для просмотра задач конвейера выпуска:</span><span class="sxs-lookup"><span data-stu-id="70906-327">Click the *1 phase, 2 tasks* link in the *Production* environment box to view the release pipeline tasks:</span></span>

![Снимок экрана задач конвейер выпуска](media/cicd/release-definition-tasks.png)

<span data-ttu-id="70906-329">Конвейер выпуска состоит из двух задач: *Развертывание службы приложений Azure в слоте* и *управление службе приложений Azure — переключение слотов*.</span><span class="sxs-lookup"><span data-stu-id="70906-329">The release pipeline consists of two tasks: *Deploy Azure App Service to Slot* and *Manage Azure App Service - Slot Swap*.</span></span> <span data-ttu-id="70906-330">Щелкнув первая задача раскрывает конфигурация следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="70906-330">Clicking the first task reveals the following task configuration:</span></span>

![Задача развертывания конвейера выпуска отображение экрана](media/cicd/release-definition-task1.png)

<span data-ttu-id="70906-332">Подписка Azure, тип службы, имя веб-приложения, группу ресурсов и слот развертывания определяются в задачи развертывания.</span><span class="sxs-lookup"><span data-stu-id="70906-332">The Azure subscription, service type, web app name, resource group, and deployment slot are defined in the deployment task.</span></span> <span data-ttu-id="70906-333">**Пакет или папка** содержит текстовое поле *ZIP-файл* путь к файлу, чтобы извлечь и развернуть для *промежуточных* слоте *mywebapp\<уникальный _Число\>*  веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="70906-333">The **Package or folder** textbox holds the *.zip* file path to be extracted and deployed to the *staging* slot of the *mywebapp\<unique_number\>* web app.</span></span>

<span data-ttu-id="70906-334">Щелкнув задачу замены слота раскрывает конфигурация следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="70906-334">Clicking the slot swap task reveals the following task configuration:</span></span>

![Снимок экрана отображение выпуска конвейера слот переключения задач](media/cicd/release-definition-task2.png)

<span data-ttu-id="70906-336">Предоставляются подписки, группы ресурсов, тип службы, имя веб-приложения и сведения о слот развертывания.</span><span class="sxs-lookup"><span data-stu-id="70906-336">The subscription, resource group, service type, web app name, and deployment slot details are provided.</span></span> <span data-ttu-id="70906-337">**Переключить на рабочий слот** будет установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="70906-337">The **Swap with Production** check box is checked.</span></span> <span data-ttu-id="70906-338">Следовательно, биты развертывания *промежуточных* меняются местами слот в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="70906-338">Consequently, the bits deployed to the *staging* slot are swapped into the production environment.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="70906-339">Дополнительные материалы для чтения</span><span class="sxs-lookup"><span data-stu-id="70906-339">Additional reading</span></span>

* [<span data-ttu-id="70906-340">Создание первого конвейера с помощью Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="70906-340">Create your first pipeline with Azure Pipelines</span></span>](/azure/devops/pipelines/get-started-yaml)
* [<span data-ttu-id="70906-341">Проект сборки и .NET Core</span><span class="sxs-lookup"><span data-stu-id="70906-341">Build and .NET Core project</span></span>](/azure/devops/pipelines/languages/dotnet-core)
* [<span data-ttu-id="70906-342">Развертывание веб-приложения с конвейерами Azure</span><span class="sxs-lookup"><span data-stu-id="70906-342">Deploy a web app with Azure Pipelines</span></span>](/azure/devops/pipelines/targets/webapp)
