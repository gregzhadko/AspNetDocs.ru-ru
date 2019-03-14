---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Резидентного размещения ASP.NET веб-API 1 (C#) | Документация Майкрософт
author: MikeWasson
description: Веб-API ASP.NET не требуются службы IIS. Вы можете самостоятельно размещать веб-API в свои собственные хост-процессе. Этот учебник показывает, как для размещения веб-API внутри консоли рабоче...
ms.author: riande
ms.date: 01/26/2012
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 63d192a6fa2aafef3770d5b0b97ec32e001b69db
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040761"
---
<a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="337a0-105">Резидентного размещения ASP.NET веб-API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="337a0-105">Self-Host ASP.NET Web API 1 (C#)</span></span>
====================
<span data-ttu-id="337a0-106">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="337a0-106">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="337a0-107">Веб-API ASP.NET не требуются службы IIS.</span><span class="sxs-lookup"><span data-stu-id="337a0-107">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="337a0-108">Вы можете самостоятельно размещать веб-API в свои собственные хост-процессе.</span><span class="sxs-lookup"><span data-stu-id="337a0-108">You can self-host a web API in your own host process.</span></span> <span data-ttu-id="337a0-109">Этом руководстве показано, как разместить веб-API внутри консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="337a0-109">This tutorial shows how to host a web API inside a console application.</span></span>
> 
> <span data-ttu-id="337a0-110">**Новые приложения должны использовать OWIN для резидентного размещения веб-API.**</span><span class="sxs-lookup"><span data-stu-id="337a0-110">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="337a0-111">См. в разделе [использовать OWIN для резидентного размещения веб-API 2 ASP.NET](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="337a0-111">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="337a0-112">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="337a0-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="337a0-113">Веб-API 1</span><span class="sxs-lookup"><span data-stu-id="337a0-113">Web API 1</span></span>
> - <span data-ttu-id="337a0-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="337a0-114">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="337a0-115">Создайте проект консольного приложения</span><span class="sxs-lookup"><span data-stu-id="337a0-115">Create the Console Application Project</span></span>

<span data-ttu-id="337a0-116">Запустите Visual Studio и выберите **новый проект** из **запустить** страницы.</span><span class="sxs-lookup"><span data-stu-id="337a0-116">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="337a0-117">Или с **файл** меню, выберите **New** и затем **проекта**.</span><span class="sxs-lookup"><span data-stu-id="337a0-117">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="337a0-118">В **шаблоны** области выберите **установленные шаблоны** и разверните **Visual C#** узла.</span><span class="sxs-lookup"><span data-stu-id="337a0-118">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="337a0-119">В разделе **Visual C#** выберите **Windows**.</span><span class="sxs-lookup"><span data-stu-id="337a0-119">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="337a0-120">В списке шаблонов проектов выберите **консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="337a0-120">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="337a0-121">Назовите проект &quot;SelfHost&quot; и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="337a0-121">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="337a0-122">Задать целевую платформу (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="337a0-122">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="337a0-123">Если вы используете Visual Studio 2010, измените целевую платформу .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="337a0-123">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="337a0-124">(По умолчанию, которой предназначен шаблон проекта [профиль .net Framework клиента](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="337a0-124">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="337a0-125">В обозревателе решений щелкните правой кнопкой мыши проект и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="337a0-125">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="337a0-126">В **требуемой версии .NET framework** раскрывающемся списке, изменить целевую платформу .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="337a0-126">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="337a0-127">Для применения изменений нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="337a0-127">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="337a0-128">Установить диспетчер пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="337a0-128">Install NuGet Package Manager</span></span>

<span data-ttu-id="337a0-129">Диспетчер пакетов NuGet — это самый простой способ добавить сборки веб-API в проект не ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="337a0-129">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="337a0-130">Чтобы проверить, установлен ли диспетчер пакетов NuGet, щелкните **средства** меню в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="337a0-130">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="337a0-131">Если вы видите пункт меню **диспетчер пакетов NuGet**, то у вас есть диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="337a0-131">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="337a0-132">Чтобы установить диспетчер пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="337a0-132">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="337a0-133">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="337a0-133">Start Visual Studio.</span></span>
2. <span data-ttu-id="337a0-134">Из **средства** меню, выберите **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="337a0-134">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="337a0-135">В **расширения и обновления** диалоговом окне выберите **Online**.</span><span class="sxs-lookup"><span data-stu-id="337a0-135">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="337a0-136">Если вы не видите «диспетчер пакетов NuGet», введите «Диспетчер пакетов nuget» в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="337a0-136">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="337a0-137">Выберите диспетчер пакетов NuGet и нажмите кнопку **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="337a0-137">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="337a0-138">После завершения загрузки, вам будет предложено установить.</span><span class="sxs-lookup"><span data-stu-id="337a0-138">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="337a0-139">После завершения установки может быть предложено перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="337a0-139">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="337a0-140">Добавление веб-пакета NuGet для API</span><span class="sxs-lookup"><span data-stu-id="337a0-140">Add the Web API NuGet Package</span></span>

<span data-ttu-id="337a0-141">После установки диспетчер пакетов NuGet, добавьте пакет Web API Self-Host в проект.</span><span class="sxs-lookup"><span data-stu-id="337a0-141">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="337a0-142">Из **средства** меню, выберите **диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="337a0-142">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="337a0-143">*Примечание*. Если вы не видите это меню товара, убедитесь, что диспетчер пакетов NuGet, неправильно установлен.</span><span class="sxs-lookup"><span data-stu-id="337a0-143">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="337a0-144">Выберите **управление пакетами NuGet для решения**</span><span class="sxs-lookup"><span data-stu-id="337a0-144">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="337a0-145">В **управление пакетами NugGet** диалоговом окне выберите **Online**.</span><span class="sxs-lookup"><span data-stu-id="337a0-145">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="337a0-146">В поле поиска введите &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span><span class="sxs-lookup"><span data-stu-id="337a0-146">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="337a0-147">Выберите пакет API Self ASP.NET веб-узел и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="337a0-147">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="337a0-148">После установки пакета, нажмите кнопку **закрыть** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="337a0-148">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="337a0-149">Убедитесь в том, что для установки пакета с именем Microsoft.AspNet.WebApi.SelfHost, не AspNetWebApi.SelfHost.</span><span class="sxs-lookup"><span data-stu-id="337a0-149">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="337a0-150">Создание модели и контроллера</span><span class="sxs-lookup"><span data-stu-id="337a0-150">Create the Model and Controller</span></span>

<span data-ttu-id="337a0-151">В этом учебнике используется те же классы модели и контроллера, как [Приступая к работе](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="337a0-151">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="337a0-152">Добавьте открытый класс с именем `Product`.</span><span class="sxs-lookup"><span data-stu-id="337a0-152">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="337a0-153">Добавьте открытый класс с именем `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="337a0-153">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="337a0-154">Этот класс из **System.Web.Http.ApiController**.</span><span class="sxs-lookup"><span data-stu-id="337a0-154">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="337a0-155">Дополнительные сведения о коде в этом контроллере, см. в разделе [Приступая к работе](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="337a0-155">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="337a0-156">Этот контроллер определяет три действия GET:</span><span class="sxs-lookup"><span data-stu-id="337a0-156">This controller defines three GET actions:</span></span>

| <span data-ttu-id="337a0-157">URI</span><span class="sxs-lookup"><span data-stu-id="337a0-157">URI</span></span> | <span data-ttu-id="337a0-158">Описание</span><span class="sxs-lookup"><span data-stu-id="337a0-158">Description</span></span> |
| --- | --- |
| <span data-ttu-id="337a0-159">/ api/продуктов</span><span class="sxs-lookup"><span data-stu-id="337a0-159">/api/products</span></span> | <span data-ttu-id="337a0-160">Получение списка всех продуктов.</span><span class="sxs-lookup"><span data-stu-id="337a0-160">Get a list of all products.</span></span> |
| <span data-ttu-id="337a0-161">/API/продукты/*идентификатор*</span><span class="sxs-lookup"><span data-stu-id="337a0-161">/api/products/*id*</span></span> | <span data-ttu-id="337a0-162">Получить продукт по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="337a0-162">Get a product by ID.</span></span> |
| <span data-ttu-id="337a0-163">/api/products/?category=*category*</span><span class="sxs-lookup"><span data-stu-id="337a0-163">/api/products/?category=*category*</span></span> | <span data-ttu-id="337a0-164">Получение списка продуктов по категориям.</span><span class="sxs-lookup"><span data-stu-id="337a0-164">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="337a0-165">Размещение веб-API</span><span class="sxs-lookup"><span data-stu-id="337a0-165">Host the Web API</span></span>

<span data-ttu-id="337a0-166">Откройте файл Program.cs и добавьте следующие операторы using:</span><span class="sxs-lookup"><span data-stu-id="337a0-166">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="337a0-167">Добавьте следующий код, чтобы **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="337a0-167">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="337a0-168">(Необязательно) Добавить резервирование пространства имен URL-адрес HTTP</span><span class="sxs-lookup"><span data-stu-id="337a0-168">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="337a0-169">Это приложение прослушивает `http://localhost:8080/`.</span><span class="sxs-lookup"><span data-stu-id="337a0-169">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="337a0-170">По умолчанию ожидающей передачи данных по конкретному адресу HTTP требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="337a0-170">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="337a0-171">При запуске учебника, таким образом, может появиться следующая ошибка: «HTTP не удалось зарегистрировать URL-адрес http://+:8080/» существует два способа, чтобы избежать этой ошибки:</span><span class="sxs-lookup"><span data-stu-id="337a0-171">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="337a0-172">Запуск Visual Studio с повышенными полномочиями администратора, или</span><span class="sxs-lookup"><span data-stu-id="337a0-172">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="337a0-173">Используйте Netsh.exe для предоставления разрешений учетной записи для резервирования URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="337a0-173">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="337a0-174">Чтобы использовать Netsh.exe, откройте командную строку с правами администратора и введите следующую команду: следующее:</span><span class="sxs-lookup"><span data-stu-id="337a0-174">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="337a0-175">где *компьютер\имя_пользователя* является учетная запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="337a0-175">where *machine\username* is your user account.</span></span>

<span data-ttu-id="337a0-176">По завершении размещения на собственном сервере, не забудьте удалить резервирование:</span><span class="sxs-lookup"><span data-stu-id="337a0-176">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="337a0-177">Вызов веб-API из клиентского приложения (C#)</span><span class="sxs-lookup"><span data-stu-id="337a0-177">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="337a0-178">Давайте напишем простое консольное приложение, вызывающее веб-API.</span><span class="sxs-lookup"><span data-stu-id="337a0-178">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="337a0-179">Добавьте новый проект консольного приложения в решение:</span><span class="sxs-lookup"><span data-stu-id="337a0-179">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="337a0-180">В обозревателе решений щелкните решение правой кнопкой мыши и выберите **Добавление нового проекта**.</span><span class="sxs-lookup"><span data-stu-id="337a0-180">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="337a0-181">Создайте новое консольное приложение с именем &quot;ClientApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="337a0-181">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="337a0-182">С помощью диспетчера пакетов NuGet для добавления пакета ASP.NET Web API основных библиотек:</span><span class="sxs-lookup"><span data-stu-id="337a0-182">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="337a0-183">В меню "Сервис" выберите **диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="337a0-183">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="337a0-184">Выберите **управление пакетами NuGet для решения**</span><span class="sxs-lookup"><span data-stu-id="337a0-184">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="337a0-185">В **управление пакетами NuGet** диалоговом окне выберите **Online**.</span><span class="sxs-lookup"><span data-stu-id="337a0-185">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="337a0-186">В поле поиска введите &quot;Microsoft.AspNet.WebApi.Client&quot;.</span><span class="sxs-lookup"><span data-stu-id="337a0-186">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="337a0-187">Выберите пакет Microsoft ASP.NET Web API клиентских библиотек и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="337a0-187">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="337a0-188">Добавьте ссылку в ClientApp SelfHost проект:</span><span class="sxs-lookup"><span data-stu-id="337a0-188">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="337a0-189">В обозревателе решений щелкните правой кнопкой мыши проект ClientApp.</span><span class="sxs-lookup"><span data-stu-id="337a0-189">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="337a0-190">Выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="337a0-190">Select **Add Reference**.</span></span>
- <span data-ttu-id="337a0-191">В **диспетчер ссылок** диалогового окна в разделе **решение**выберите **проекты**.</span><span class="sxs-lookup"><span data-stu-id="337a0-191">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="337a0-192">Выберите проект SelfHost.</span><span class="sxs-lookup"><span data-stu-id="337a0-192">Select the SelfHost project.</span></span>
- <span data-ttu-id="337a0-193">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="337a0-193">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="337a0-194">Откройте файл Client/Program.cs.</span><span class="sxs-lookup"><span data-stu-id="337a0-194">Open the Client/Program.cs file.</span></span> <span data-ttu-id="337a0-195">Добавьте следующий **с помощью** инструкции:</span><span class="sxs-lookup"><span data-stu-id="337a0-195">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="337a0-196">Добавить статический **HttpClient** экземпляр:</span><span class="sxs-lookup"><span data-stu-id="337a0-196">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="337a0-197">Добавьте следующие методы для получения списка всех продуктов, список продуктов по Идентификатору и перечислены продукты по категориям.</span><span class="sxs-lookup"><span data-stu-id="337a0-197">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="337a0-198">Каждый из этих методов следует той же схеме:</span><span class="sxs-lookup"><span data-stu-id="337a0-198">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="337a0-199">Вызовите **HttpClient.GetAsync** для отправки запроса GET с соответствующим URI.</span><span class="sxs-lookup"><span data-stu-id="337a0-199">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="337a0-200">Вызовите **HttpResponseMessage.EnsureSuccessStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="337a0-200">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="337a0-201">Этот метод создает исключение, если состояние ответа HTTP является кодом ошибки.</span><span class="sxs-lookup"><span data-stu-id="337a0-201">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="337a0-202">Вызовите **ReadAsAsync&lt;T&gt;**  десериализовать тип среды CLR из HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="337a0-202">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="337a0-203">Этот метод является методом расширения, определенные в **System.Net.Http.HttpContentExtensions**.</span><span class="sxs-lookup"><span data-stu-id="337a0-203">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="337a0-204">**GetAsync** и **ReadAsAsync** методы являются как асинхронные.</span><span class="sxs-lookup"><span data-stu-id="337a0-204">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="337a0-205">Они возвращают **задачи** объекты, представляющие асинхронной операции.</span><span class="sxs-lookup"><span data-stu-id="337a0-205">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="337a0-206">Начало **результат** оно блокирует поток до завершения операции.</span><span class="sxs-lookup"><span data-stu-id="337a0-206">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="337a0-207">Дополнительные сведения об использовании HttpClient, включая вызов без блокировки, см. в разделе [вызова Web API из клиента .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="337a0-207">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="337a0-208">Прежде чем выполнять эти методы, свойства BaseAddress на экземпляре HttpClient "`http://localhost:8080`«.</span><span class="sxs-lookup"><span data-stu-id="337a0-208">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="337a0-209">Пример:</span><span class="sxs-lookup"><span data-stu-id="337a0-209">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="337a0-210">Это должен отобразиться следующий результат.</span><span class="sxs-lookup"><span data-stu-id="337a0-210">This should output the following.</span></span> <span data-ttu-id="337a0-211">(Не забудьте сначала запустить SelfHost приложение.)</span><span class="sxs-lookup"><span data-stu-id="337a0-211">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
