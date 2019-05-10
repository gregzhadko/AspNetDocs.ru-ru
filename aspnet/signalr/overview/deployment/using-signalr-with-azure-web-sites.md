---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: С помощью SignalR с веб-приложениями в службе приложений Azure | Документация Майкрософт
author: bradygaster
description: В этом документе описываются способы настройки приложения SignalR, которое работает на базе Microsoft Azure. Версии программного обеспечения используется в этом руководстве, Visual Studio 2013 или Vis...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128145"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="9bada-104">Использование SignalR с веб-приложениями в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="9bada-105">по [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="9bada-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="9bada-106">В этом документе описываются способы настройки приложения SignalR, которое работает на базе Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9bada-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9bada-107">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="9bada-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="9bada-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) или Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9bada-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="9bada-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9bada-109">.NET 4.5</span></span>
> - <span data-ttu-id="9bada-110">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="9bada-110">SignalR version 2</span></span>
> - <span data-ttu-id="9bada-111">Пакет Azure SDK 2.3 для Visual Studio 2013 или 2012</span><span class="sxs-lookup"><span data-stu-id="9bada-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="9bada-112">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="9bada-112">Questions and comments</span></span>
>
> <span data-ttu-id="9bada-113">Оставьте свои отзывы на том, как вам понравилось, и этот учебник и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9bada-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="9bada-114">Если у вас есть вопросы, которые не имеют отношения к руководству, их можно разместить [форум по ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), или [форумы Microsoft Azure](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span><span class="sxs-lookup"><span data-stu-id="9bada-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="9bada-115">Содержание</span><span class="sxs-lookup"><span data-stu-id="9bada-115">Table of Contents</span></span>

- [<span data-ttu-id="9bada-116">Введение</span><span class="sxs-lookup"><span data-stu-id="9bada-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="9bada-117">Развертывание SignalR веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="9bada-118">Включение WebSockets в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="9bada-119">Использование объединительной платы кэша redis для Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="9bada-120">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="9bada-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="9bada-121">Вступление</span><span class="sxs-lookup"><span data-stu-id="9bada-121">Introduction</span></span>

<span data-ttu-id="9bada-122">ASP.NET SignalR можно использовать для переноса на новый уровень взаимодействия между серверами "и" веб "или" клиентов .NET.</span><span class="sxs-lookup"><span data-stu-id="9bada-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="9bada-123">При размещении в Azure приложений SignalR можно воспользоваться преимуществами высокой доступности, масштабируемый и предоставляет среду с высокой производительностью, работающее в облаке.</span><span class="sxs-lookup"><span data-stu-id="9bada-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="9bada-124">Развертывание SignalR веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="9bada-125">SignalR не добавляет всяких осложнений, определенного с развертыванием приложения в Azure и развертывание на локальном сервере.</span><span class="sxs-lookup"><span data-stu-id="9bada-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="9bada-126">Приложения, использующего SignalR может размещаться в Azure без изменений в конфигурации и других параметров (хотя поддержка WebSockets, см. в разделе [Включение WebSockets в службе приложений Azure](#websocket) ниже.) В этом руководстве вы развернете приложение, созданное в [Приступая к работе](../getting-started/tutorial-getting-started-with-signalr.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="9bada-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="9bada-127">**Необходимые компоненты**</span><span class="sxs-lookup"><span data-stu-id="9bada-127">**Prerequisites**</span></span>

- <span data-ttu-id="9bada-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9bada-128">Visual Studio 2013.</span></span> <span data-ttu-id="9bada-129">Если у вас нет Visual Studio, Visual Studio 2013 Express для Web входит в состав установки пакета Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="9bada-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="9bada-130">[Пакет Azure SDK 2.3 для Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) или [2.3 пакета Azure SDK для Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span><span class="sxs-lookup"><span data-stu-id="9bada-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="9bada-131">Для работы с этим руководством требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9bada-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="9bada-132">Вы можете [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), или [зарегистрироваться для получения пробной подписки](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bada-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="9bada-133">Развертывание веб-приложения SignalR в Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="9bada-134">Завершить [Приступая к работе](../getting-started/tutorial-getting-started-with-signalr.md), или загрузить готовый проект из [коллекции исходных кодов](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span><span class="sxs-lookup"><span data-stu-id="9bada-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="9bada-135">В Visual Studio выберите **построения**, **публикации SignalR Chat**.</span><span class="sxs-lookup"><span data-stu-id="9bada-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="9bada-136">В диалоговом окне «Публикация веб-сайта» выберите «веб-сайтов Windows Azure».</span><span class="sxs-lookup"><span data-stu-id="9bada-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Выберите веб-сайты Azure](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="9bada-138">Если вы не вошли учетную запись Майкрософт, нажмите кнопку **вход...**  в диалоговое окно «выберите существующий веб-сайт» и входа.</span><span class="sxs-lookup"><span data-stu-id="9bada-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![Выберите существующий веб-сайт](using-signalr-with-azure-web-sites/_static/image2.png)    ![Вход в Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="9bada-141">В диалоговом окне «выберите существующий веб-сайт» нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="9bada-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![Новый веб-сайт](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="9bada-143">В диалоговом окне «Создание сайта в Windows Azure» введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="9bada-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="9bada-144">Выберите ближайший к вам регион в раскрывающемся списке регион.</span><span class="sxs-lookup"><span data-stu-id="9bada-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="9bada-145">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bada-145">Click **Create**.</span></span>

    ![Создание сайта в Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="9bada-147">В диалоговом окне «Публикация веб-сайта» щелкните **публикации**.</span><span class="sxs-lookup"><span data-stu-id="9bada-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![Опубликовать сайт](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="9bada-149">После завершения публикации приложения чата SignalR приложение, размещенное в веб-приложениях службы приложений Azure откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="9bada-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![Узел, открыв в браузере](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="9bada-151">Включение WebSockets в веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="9bada-152">WebSockets необходимо явно включить в веб-приложения для использования в приложении SignalR; в противном случае будет использоваться другие протоколы (см. в разделе [транспорта и в случае ошибки](../getting-started/introduction-to-signalr.md#transports) сведения).</span><span class="sxs-lookup"><span data-stu-id="9bada-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="9bada-153">Чтобы использовать WebSocket в веб-приложениях службы приложений Azure, включите его в разделе конфигурации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9bada-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="9bada-154">Чтобы сделать это, откройте веб-приложение в [портала управления Azure](https://manage.windowsazure.com/)и выберите «настроить».</span><span class="sxs-lookup"><span data-stu-id="9bada-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![Вкладка "Настройка"](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="9bada-156">В верхней части страницы конфигурации убедитесь, что для веб-приложения используется .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="9bada-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET framework версии 4.5 параметр](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="9bada-158">На странице «Конфигурация» в **WebSockets** выберите **на**.</span><span class="sxs-lookup"><span data-stu-id="9bada-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Параметр WebSockets: включить](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="9bada-160">В нижней части страницы конфигурации, выберите **Сохранить** для сохранения изменений.</span><span class="sxs-lookup"><span data-stu-id="9bada-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![Сохранить параметры](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="9bada-162">Использование объединительной платы кэша redis для Azure</span><span class="sxs-lookup"><span data-stu-id="9bada-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="9bada-163">Если используется несколько экземпляров для веб-приложения и пользователи этих экземпляров должны взаимодействовать друг с другом (позволяя, например, сообщения чата, созданные в одном экземпляре обращаться пользователей, подключенных к другим экземплярам), [кэша Redis для Azure Задняя панель](../performance/scaleout-with-redis.md) должен быть реализован в приложении.</span><span class="sxs-lookup"><span data-stu-id="9bada-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="9bada-164">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="9bada-164">Next Steps</span></span>

<span data-ttu-id="9bada-165">Дополнительные сведения о веб-приложений в службе приложений Azure, см. в разделе [Обзор веб-приложений](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span><span class="sxs-lookup"><span data-stu-id="9bada-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
