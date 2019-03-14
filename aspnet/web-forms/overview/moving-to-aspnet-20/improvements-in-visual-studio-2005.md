---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Усовершенствования в Visual Studio 2005 | Документация Майкрософт
author: microsoft
description: Visual Studio 2005 обеспечивает разработчиков веб-приложений с помощью длинный список улучшений и усовершенствований для веб-проектов.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 60259ceb99de536410aa5f53db64fb2dca68bf66
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037361"
---
<a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="bf88d-103">Усовершенствования в Visual Studio 2005</span><span class="sxs-lookup"><span data-stu-id="bf88d-103">Improvements in Visual Studio 2005</span></span>
====================
<span data-ttu-id="bf88d-104">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bf88d-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="bf88d-105">Visual Studio 2005 обеспечивает разработчиков веб-приложений с помощью длинный список улучшений и усовершенствований для веб-проектов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>


<span data-ttu-id="bf88d-106">Visual Studio 2005 обеспечивает разработчиков веб-приложений с помощью длинный список улучшений и усовершенствований для веб-проектов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="bf88d-107">Столь мощная, как Visual Studio .NET 2002 и 2003, отсутствуют многие жалобы в способе обработки веб-проектов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="bf88d-108">Visual Studio 2005 вносит значительное количество новых функций для решения этих жалоб.</span><span class="sxs-lookup"><span data-stu-id="bf88d-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="bf88d-109">Для тех, кто предпочитает способ обработки компиляции веб-приложений в Visual Studio .NET 2003, см. в разделе [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span><span class="sxs-lookup"><span data-stu-id="bf88d-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="bf88d-110">В этом модуле также рассматриваются методы создания веб-проекта, управления и разработки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="bf88d-111">В более поздних версий модуля также охватывают улучшений в области построения веб-проекты и их развертывания.</span><span class="sxs-lookup"><span data-stu-id="bf88d-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="bf88d-112">Серверные расширения FrontPage</span><span class="sxs-lookup"><span data-stu-id="bf88d-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="bf88d-113">Visual Studio .NET 2002 и 2003 необходимые серверные расширения FrontPage на поле для создания или построения веб-проектов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="bf88d-114">У разработчиков было выбрать между двумя режимами различные права доступа (режим доступа серверных расширений FrontPage или файл), оба использовать серверные расширения FrontPage для выполнения задач, таких как установка корневой каталог приложения в IIS и т. д.</span><span class="sxs-lookup"><span data-stu-id="bf88d-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="bf88d-115">Visual Studio 2005 устраняет зависимость от серверных расширений FrontPage для локальных проектов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="bf88d-116">Visual Studio 2005 теперь получает доступ к метабазе IIS напрямую, а не с помощью серверных расширений FrontPage.</span><span class="sxs-lookup"><span data-stu-id="bf88d-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="bf88d-117">Visual Studio 2005 также добавляет поддержку протокола FTP, который разрешает доступ к удаленному проекту без использования серверных расширений FrontPage.</span><span class="sxs-lookup"><span data-stu-id="bf88d-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="bf88d-118">Для тех разработчиков, которые хотят использовать серверные расширения FrontPage в своих проектах параметр по-прежнему доступен.</span><span class="sxs-lookup"><span data-stu-id="bf88d-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="bf88d-119">Тем не менее основываясь на надежный отзывы сообщества разработчиков ASP.NET, это не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="bf88d-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-120">Серверные расширения FrontPage по-прежнему необходимы для создания удаленного проекта, открытие и т. д.</span><span class="sxs-lookup"><span data-stu-id="bf88d-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>


## <a name="aspnet-development-server"></a><span data-ttu-id="bf88d-121">Сервер ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="bf88d-121">ASP.NET Development Server</span></span>

<span data-ttu-id="bf88d-122">Visual Studio 2005 поставляется с новой веб-сервере ASP.NET Development Server.</span><span class="sxs-lookup"><span data-stu-id="bf88d-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="bf88d-123">(Этот веб-сервер был ранее известен как Cassini.)</span><span class="sxs-lookup"><span data-stu-id="bf88d-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="bf88d-124">Ниже перечислены некоторые преимущества сервера разработки ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bf88d-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="bf88d-125">Теперь существует возможность пользователям без прав администратора для разработки и отладки для веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="bf88d-126">ASP.NET Development Server динамически сопоставляет виртуальные каталоги в любое место в файловой системе, позволяя гибкое расположения.</span><span class="sxs-lookup"><span data-stu-id="bf88d-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="bf88d-127">Пользователей в Windows XP Professional, которые уже используются службы IIS, теперь можно создавать новые веб-приложения, которые не повлияют на структуре файла или папки из их по умолчанию веб-сайт в IIS.</span><span class="sxs-lookup"><span data-stu-id="bf88d-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="bf88d-128">Чтобы воспользоваться преимуществами ASP.NET Development Server требуется специальная настройка.</span><span class="sxs-lookup"><span data-stu-id="bf88d-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="bf88d-129">Если отлаживается или просматривать веб-проект, который размещен в файловой системе, Visual Studio 2005 автоматический запуск экземпляра сервера разработки ASP.NET по случайный порт для обслуживания запроса.</span><span class="sxs-lookup"><span data-stu-id="bf88d-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="bf88d-130">Дополнительные сведения будут рассматриваться с ASP.NET Development Server более поздней версии в этом модуле.</span><span class="sxs-lookup"><span data-stu-id="bf88d-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="bf88d-131">Управление файлами</span><span class="sxs-lookup"><span data-stu-id="bf88d-131">Improved File Management</span></span>

<span data-ttu-id="bf88d-132">В Visual Studio 2002 и 2003 файл проекта (с расширением VBPROJ для VB.NET) и .csproj для C# хранятся сведения для всех файлов в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bf88d-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="bf88d-133">Отображение обозревателя решений основана на сведения о файле в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="bf88d-134">По этой причине в обозревателе решений будет часто отображаются неверные сведения в случаях, где использовались внешних редакторов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="bf88d-135">Visual Studio 2002 и 2003 будет часто перезаписи изменений файла или отображает самую последнюю версию файлов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="bf88d-136">Visual Studio 2005 немедленно выполняет с файлом проекта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="bf88d-137">Вместо этого она считывает данные файлов и папок непосредственно с диска, приводит к точное отображение файлов в проекте.</span><span class="sxs-lookup"><span data-stu-id="bf88d-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="bf88d-138">Так как в папке "ссылки" в Visual Studio 2002 и 2003 не представляет фактический папку веб-приложения, Visual Studio 2005 также удаляет папку ссылки из обозревателя решений.</span><span class="sxs-lookup"><span data-stu-id="bf88d-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="bf88d-139">Чтобы получить доступ к ссылок проекта в Visual Studio 2005, следует использовать на страницах свойств для проекта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="bf88d-140">Создание веб-проектов</span><span class="sxs-lookup"><span data-stu-id="bf88d-140">Creating Web Projects</span></span>

<span data-ttu-id="bf88d-141">Веб-разработчики не множество новых возможностей, доступных для создания проекта в Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="bf88d-142">Веб-сайты могут теперь создаваться в любом месте в файловой системе и затем можно отлаживать или просматриваться с помощью ASP.NET Development Server.</span><span class="sxs-lookup"><span data-stu-id="bf88d-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="bf88d-143">Разработчики также могут создавать новые веб-сайты, с помощью протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="bf88d-144">Щелкните здесь, чтобы просмотреть пошаговое видео создания веб-проектов в Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>


![](improvements-in-visual-studio-2005/_static/image1.png)


[<span data-ttu-id="bf88d-145">Открыть весь экран</span><span class="sxs-lookup"><span data-stu-id="bf88d-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)


### <a name="file-system-projects"></a><span data-ttu-id="bf88d-146">Файл системы проектов</span><span class="sxs-lookup"><span data-stu-id="bf88d-146">File System Projects</span></span>

<span data-ttu-id="bf88d-147">Как было показано в видео Пошаговое руководство, вы можете создавать веб-сайты в файловой системе на локальном компьютере или в удаленном расположении через файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="bf88d-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="bf88d-148">Веб-сайты, которые создаются в файловой системе просматривать и отлажены с помощью сервера разработки ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bf88d-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-149">Сервер разработки ASP.NET может вызвать некоторую путаницу e для клиентов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="bf88d-150">Если веб-проект создается в файловой системе в структуре каталогов IISs (т. е. c:/inetpub/wwwroot), веб-сайт будет по-прежнему просматривать через ASP.NET Development Server при запуске из Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="bf88d-151">Таким образом любой конфигурации IIS (т. е. методов проверки подлинности) не применяется.</span><span class="sxs-lookup"><span data-stu-id="bf88d-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>


<span data-ttu-id="bf88d-152">Веб-проекта по умолчанию также удаляет много служебных данных, включает только страницы Default.aspx, файл default.cs и в папку приложения/_Data.</span><span class="sxs-lookup"><span data-stu-id="bf88d-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="bf88d-153">Файл web.config и специальные папки (т. е. приложение/фра_гменты) добавляются по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="bf88d-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="bf88d-154">Веб-проект включает только файлы и папки, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="bf88d-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="bf88d-155">Проекты HTTP</span><span class="sxs-lookup"><span data-stu-id="bf88d-155">HTTP Projects</span></span>

<span data-ttu-id="bf88d-156">Проекты HTTP может быть проектах, созданных на локальном веб-узла IIS или на удаленный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="bf88d-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="bf88d-157">Расположение проекта по умолчанию является `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="bf88d-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="bf88d-158">Если щелкнуть кнопку обзора, двумя способами HTTP: Локальный сервер IIS и удаленный сайт.</span><span class="sxs-lookup"><span data-stu-id="bf88d-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="bf88d-159">Основное различие в этих двух вариантов — это метод, в котором отображается текст веб-сайта, в диалоговом окне Выбор расположения и в том, как файлы копируются на веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="bf88d-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="bf88d-160">Параметр локальный сервер IIS считывает данные сайта из метабазы на локальном компьютере и файлы копируются в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="bf88d-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="bf88d-161">Параметр удаленного сайта используются серверные расширения FrontPage и данные сайта и файлы копируются с помощью протокола HTTP и вызовы RPC расширений сервера FrontPage.</span><span class="sxs-lookup"><span data-stu-id="bf88d-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-162">Файл vs###/_tmp.htm и get/_aspx/_ver.aspx больше не используются для определения сведений о версии.</span><span class="sxs-lookup"><span data-stu-id="bf88d-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>


<span data-ttu-id="bf88d-163">Параметр HTTP по умолчанию — локальный сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="bf88d-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="bf88d-164">Этот параметр считывает метабазу IIS, чтобы определить, какие сайты доступны и расположение, в котором для создания содержимого.</span><span class="sxs-lookup"><span data-stu-id="bf88d-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="bf88d-165">Можно выбрать другую папку или виртуальный каталог, выбрав его в представлении в виде дерева.</span><span class="sxs-lookup"><span data-stu-id="bf88d-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="bf88d-166">Вы можете также создание нового виртуального каталога, пометить папки как приложения, а также удалить существующие виртуальные каталоги в этом диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="bf88d-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>


![Выберите расположение](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="bf88d-168">**Рис. 1**: Выберите расположение</span><span class="sxs-lookup"><span data-stu-id="bf88d-168">**Figure 1**: The Choose Location Dialog</span></span>


<span data-ttu-id="bf88d-169">В отличие от более ранних версий Visual Studio, если вы проверите **использовать протокол SSL** флажок и SSL-сертификат не соответствует URL-адрес, вы подключаетесь, вам будет предложена предупреждение безопасности диалоговое окно с запросом, если бы Например продолжить.</span><span class="sxs-lookup"><span data-stu-id="bf88d-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="bf88d-170">С помощью Visual Studio .NET 2003, если сертификат не был сопоставления один, Создание проекта завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="bf88d-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>


![Безопасность предупреждений о SSL-сертификата](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="bf88d-172">**Рис. 2**: Безопасность предупреждений о SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="bf88d-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>


### <a name="note-on-host-headers"></a><span data-ttu-id="bf88d-173">Обратите внимание на заголовки узлов</span><span class="sxs-lookup"><span data-stu-id="bf88d-173">Note on Host Headers</span></span>

<span data-ttu-id="bf88d-174">Если вы создаете веб-приложения на узел, привязанный к конкретный IP-адрес, необходимо будет убедитесь, что заголовок узла.</span><span class="sxs-lookup"><span data-stu-id="bf88d-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="bf88d-175">В противном случае Visual Studio создаст на узле по адресу `http://localhost`, но IP-адрес не будут разрешены правильно, когда узел просматривать или отладки из интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="bf88d-176">Если выбран параметр удаленного сайта, чтобы можно было ввести URL-адрес назначения для нового веб-сайта изменяет диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bf88d-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="bf88d-177">Этот URL-адрес должен быть на сервере, где включены серверные расширения FrontPage.</span><span class="sxs-lookup"><span data-stu-id="bf88d-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="bf88d-178">Если вы хотите работать с локального веб-сервера с помощью серверных расширений FrontPage, можно использовать параметр удаленного сайта и указать локальный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bf88d-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>


![Создание веб-сайта на удаленном сервере](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="bf88d-180">**Рис. 3**: Создание веб-сайта на удаленном сервере</span><span class="sxs-lookup"><span data-stu-id="bf88d-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>


<span data-ttu-id="bf88d-181">При создании приложения в удаленном расположении через SSL, если SSL-сертификат не совпадает, диалоговое окно подтверждения, немного отличается от диалогового окна, отображаемого при использовании параметра локальный сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="bf88d-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>


![Оповещение системы безопасности удаленного сайта](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="bf88d-183">**Рис. 4**: Оповещение системы безопасности удаленного сайта</span><span class="sxs-lookup"><span data-stu-id="bf88d-183">**Figure 4**: The Remote Site Security Alert</span></span>


<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="bf88d-184">FTP</span><span class="sxs-lookup"><span data-stu-id="bf88d-184">FTP</span></span>

<span data-ttu-id="bf88d-185">Visual Studio 2005 предоставляет возможность создавать веб-сайты через FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="bf88d-186">При использовании этого параметра, IDE создает файлы локально в временную папку пользователя, а затем использует FTP для перемещения файлов в каталоге FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-187">Расположение временной папки — c:/Documents and Settings /&lt;пользователя&gt;/локальные параметры/Temp/VWDWebCache/&lt;Server&gt;/_&lt;имя приложения&gt;</span><span class="sxs-lookup"><span data-stu-id="bf88d-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>


<span data-ttu-id="bf88d-188">При использовании параметра FTP, откроется диалоговое окно Выбор расположения.</span><span class="sxs-lookup"><span data-stu-id="bf88d-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="bf88d-189">Введите необходимые сведения о подключении FTP в этом диалоговом окне, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf88d-189">You enter the required FTP connection information into this dialog as shown below.</span></span>


![Выберите расположение для FTP-сервера](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="bf88d-191">**Рис. 5**: Выберите расположение для FTP-сервера</span><span class="sxs-lookup"><span data-stu-id="bf88d-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>


## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="bf88d-192">Лабораторное занятие. Настройка FTP-сайта и Создание проекта</span><span class="sxs-lookup"><span data-stu-id="bf88d-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="bf88d-193">Далее описана настройка FTP-сайта, таким образом, чтобы у пользователя есть расположение, которое только их можно отправить через FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="bf88d-194">Установить службу FTP</span><span class="sxs-lookup"><span data-stu-id="bf88d-194">Install the FTP Service</span></span>

1. <span data-ttu-id="bf88d-195">Откройте Установка и удаление программ, выберите Добавление и удаление компонентов Windows</span><span class="sxs-lookup"><span data-stu-id="bf88d-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="bf88d-196">Выберите Internet Information Services (сервер приложений в Windows 2003) и нажмите кнопку **сведения**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="bf88d-197">Проверьте **службы протокола передачи файлов (FTP)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="bf88d-198">Нажмите кнопку **Далее** для установки службы FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="bf88d-199">Создайте новую папку для содержимого</span><span class="sxs-lookup"><span data-stu-id="bf88d-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="bf88d-200">В проводнике Windows, создайте новую папку с именем **User1** внутри c:/inetpub/wwwroot.</span><span class="sxs-lookup"><span data-stu-id="bf88d-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="bf88d-201">Настройка папки и разрешения для папок.</span><span class="sxs-lookup"><span data-stu-id="bf88d-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="bf88d-202">Откройте оснастку «Службы IIS» из средств администрирования.</span><span class="sxs-lookup"><span data-stu-id="bf88d-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="bf88d-203">Теперь имеется в папке FTP-узлы в узле имени компьютера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="bf88d-204">Разверните **FTP-узлы**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="bf88d-205">Щелкните правой кнопкой мыши **FTP-сайта по умолчанию**выберите **New**, затем **виртуальный каталог**, затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="bf88d-206">Введите **User1** имя виртуального каталога и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="bf88d-207">Введите **c:/inetpub/wwwroot/User1** путь и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="bf88d-208">Нажмите кнопку **Далее** и затем **Готово** завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="bf88d-209">Щелкните правой кнопкой мыши **User1** виртуальный каталог в FTP-сайта по умолчанию и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="bf88d-210">Проверьте **записи** флажок и нажмите кнопку **ОК** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="bf88d-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="bf88d-211">Щелкните правой кнопкой мыши **FTP-сайта по умолчанию** и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="bf88d-212">На **учетные записи безопасности** вкладке, снимите флажок **Разрешить анонимные подключения**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="bf88d-213">Нажмите кнопку **Да** в диалоговом окне с вопросом, следует ли продолжать.</span><span class="sxs-lookup"><span data-stu-id="bf88d-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="bf88d-214">Нажмите кнопку **ОК** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="bf88d-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="bf88d-215">Разверните **Default Web Site** под **веб-сайтов** узла.</span><span class="sxs-lookup"><span data-stu-id="bf88d-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="bf88d-216">Щелкните правой кнопкой мыши **User1** каталог и выберите **свойства**</span><span class="sxs-lookup"><span data-stu-id="bf88d-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="bf88d-217">В **параметры приложения** щелкните **создать** для пометки папке с приложением.</span><span class="sxs-lookup"><span data-stu-id="bf88d-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="bf88d-218">Нажмите кнопку **ОК** чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="bf88d-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="bf88d-219">Закройте оснастку служб IIS.</span><span class="sxs-lookup"><span data-stu-id="bf88d-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="bf88d-220">Создание веб-проекта</span><span class="sxs-lookup"><span data-stu-id="bf88d-220">Create web project</span></span>

1. <span data-ttu-id="bf88d-221">Откройте Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="bf88d-222">Из **файл** меню, выберите **новый веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="bf88d-223">В **расположение** раскрывающемся списке выберите **FTP**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="bf88d-224">Нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-224">Click **Browse**.</span></span>
5. <span data-ttu-id="bf88d-225">Введите **localhost** в **Server** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="bf88d-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="bf88d-226">Введите **User1** в текстовом поле каталогов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="bf88d-227">Нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-227">Click **Open**.</span></span> <span data-ttu-id="bf88d-228">Расположение FTP вводится в диалоговое окно нового веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="bf88d-229">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-229">Click **OK**.</span></span>
9. <span data-ttu-id="bf88d-230">Снимите флажок **анонимный вход в систему** в диалоговом окне вход в FTP, введите свои учетные данные и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="bf88d-231">Что такое URL-адрес для проекта?</span><span class="sxs-lookup"><span data-stu-id="bf88d-231">What is the URL for the project?</span></span> <span data-ttu-id="bf88d-232">(URL-адрес для проекта отображается в обозревателе решений.)</span><span class="sxs-lookup"><span data-stu-id="bf88d-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="bf88d-233">Из **построения** меню, выберите **построить веб-узел** или **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="bf88d-234">Щелкните правой кнопкой мыши на странице Default.aspx в обозревателе решений и выберите **просмотреть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="bf88d-235">В диалоговом окне требуется URL-адрес веб-сайта, введите `http://localhost/user1` URL-адрес и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bf88d-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-236">Если появится сообщение об ошибке, указывающими на невозможность загрузки /_Default тип, убедитесь, что выполняется ASP.NET 2.0 на веб-сайт и не более ранней версии.</span><span class="sxs-lookup"><span data-stu-id="bf88d-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="bf88d-237">Это можно сделать на вкладке "ASP.NET" в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="bf88d-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>


## <a name="opening-web-projects"></a><span data-ttu-id="bf88d-238">Открытие веб-проектов</span><span class="sxs-lookup"><span data-stu-id="bf88d-238">Opening Web Projects</span></span>

<span data-ttu-id="bf88d-239">Открытие веб-проектов похоже на создание проектов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="bf88d-240">Следующие разделы вызовите областей, чтобы следить за out для непосредственно в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="bf88d-241">Он также рассматривается работа с веб-проектов, с помощью протоколов HTTP и FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="bf88d-242">Чтобы открыть веб-проекта, выберите веб-сайт, откройте меню "файл".</span><span class="sxs-lookup"><span data-stu-id="bf88d-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="bf88d-243">Вас попросят с то же диалоговое окно Выбор расположения, описанные ранее, и имеет те же четыре возможности, доступные пользователю: Файловая система, локальный сервер IIS, FTP и удаленный сайт.</span><span class="sxs-lookup"><span data-stu-id="bf88d-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="bf88d-244">Файловая система</span><span class="sxs-lookup"><span data-stu-id="bf88d-244">File System</span></span>

<span data-ttu-id="bf88d-245">Как указывалось ранее в этом модуле, Visual Studio больше не использует файл проекта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="bf88d-246">Таким образом Если вы решили открыть веб-сайт из файловой системы, вы получаете возможность выбрать любой папки, которое будет применено, даже если выбранную папку не был создан как веб-проекта, изначально в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf88d-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="bf88d-247">Например вы можете открыть папку «Мои документы», как веб-сайта, и Visual Studio к счастью откройте ее и отобразить файлы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf88d-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>


![Мои документы, открытые веб-узел](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="bf88d-249">**Рис. 6**: *Мои документы* открыт как веб-сайта</span><span class="sxs-lookup"><span data-stu-id="bf88d-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>


<span data-ttu-id="bf88d-250">Так как Visual Studio создает только дополнительные файлы и папки, при необходимости, нет дополнительные файлы или папки добавляются в расположение, при их открытии.</span><span class="sxs-lookup"><span data-stu-id="bf88d-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="bf88d-251">Побочным эффектом данной архитектуры является, что предотвращает вложение веб-сайтов в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="bf88d-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="bf88d-252">Например рассмотрим следующую структуру каталогов.</span><span class="sxs-lookup"><span data-stu-id="bf88d-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="bf88d-253">Веб-проект в C:/MyWebSite</span><span class="sxs-lookup"><span data-stu-id="bf88d-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="bf88d-254">Другой веб-проекта в C:/MyWebSite/Nested</span><span class="sxs-lookup"><span data-stu-id="bf88d-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="bf88d-255">При открытии веб-сайте c:/MyWebSite, вложенные папки будут отображаться как вложенную папку приложения.</span><span class="sxs-lookup"><span data-stu-id="bf88d-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="bf88d-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="bf88d-256">HTTP</span></span>

<span data-ttu-id="bf88d-257">При открытии веб-сайтов по протоколу HTTP, параметры считываются из метабазы IIS (локальный сервер IIS) или с помощью серверных расширений FrontPage (удаленный узел). Если вложенные веб-приложений, они также отображаются со значком, который идентифицирует их как приложения.</span><span class="sxs-lookup"><span data-stu-id="bf88d-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="bf88d-258">Если вы знакомы с работой веб-приложений в программе FrontPage, в Visual Studio 2005 работает аналогично.</span><span class="sxs-lookup"><span data-stu-id="bf88d-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="bf88d-259">Несмотря на то, что Visual Studio будет отображаться значок для приложений, которые будут размещены под приложения, которое в настоящее время открыт в интегрированной среде разработки, он не позволит вам развернуть их, чтобы просмотреть их содержимое.</span><span class="sxs-lookup"><span data-stu-id="bf88d-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="bf88d-260">Тем не менее, можно дважды щелкните на них, чтобы открыть их.</span><span class="sxs-lookup"><span data-stu-id="bf88d-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="bf88d-261">При этом вы откроется диалоговое окно, предлагающее либо открыть веб-приложение (и заменить в настоящее время открыть решение) или добавить веб-приложения в текущем решении.</span><span class="sxs-lookup"><span data-stu-id="bf88d-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>


![Дважды щелкнув значок в виде вложенного приложения появится это диалоговое окно](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="bf88d-263">**Рис. 7**: Дважды щелкнув значок в виде вложенного приложения появится это диалоговое окно</span><span class="sxs-lookup"><span data-stu-id="bf88d-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>


<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="bf88d-264">FTP-сайт</span><span class="sxs-lookup"><span data-stu-id="bf88d-264">FTP Site</span></span>

<span data-ttu-id="bf88d-265">При открытии узлу по протоколу FTP, файлы всех копируются локально в папке temp.</span><span class="sxs-lookup"><span data-stu-id="bf88d-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="bf88d-266">Полный путь к папке локального хранилища отображается в панели свойств для проекта и создается в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="bf88d-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="bf88d-267">C:/Documents and Settings /&lt;пользователя&gt;/локальные параметры/Temp/VWDWebCache/&lt;Server&gt;/_&lt;имя приложения&gt;</span><span class="sxs-lookup"><span data-stu-id="bf88d-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="bf88d-268">При использовании FTP, Visual Studio необходимо указать базовый URL-адрес для вашего проекта, чтобы его можно просмотреть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf88d-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="bf88d-269">Если не указать базовый URL-адрес, Visual Studio запросит его при первом просмотре страницы в веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>


![Указание базового URL-адреса, для FTP-сайтов](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="bf88d-271">**Рис. 8**: Указание базового URL-адреса, для FTP-сайтов</span><span class="sxs-lookup"><span data-stu-id="bf88d-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>


## <a name="improvements-in-compilation"></a><span data-ttu-id="bf88d-272">Улучшения в компиляции</span><span class="sxs-lookup"><span data-stu-id="bf88d-272">Improvements in Compilation</span></span>

<span data-ttu-id="bf88d-273">Работа с веб-приложений в Visual Studio 2005 — значительно быстрее, чем предыдущие версии.</span><span class="sxs-lookup"><span data-stu-id="bf88d-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="bf88d-274">Причиной этого является не небольшой части на изменения в архитектуре компиляции.</span><span class="sxs-lookup"><span data-stu-id="bf88d-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="bf88d-275">В Visual Studio 2002 и 2003 веб-приложения были скомпилированы в одну основную сборку, которая находится в папке/Bin.</span><span class="sxs-lookup"><span data-stu-id="bf88d-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="bf88d-276">В Visual Studio 2005 был добавлен в папку приложения/фра_гменты.</span><span class="sxs-lookup"><span data-stu-id="bf88d-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="bf88d-277">Классы и другого кода без пользовательского интерфейса добавляются в папку приложения/фра_гменты.</span><span class="sxs-lookup"><span data-stu-id="bf88d-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="bf88d-278">Когда Visual Studio выполняет сборку проекта, все файлы в папке приложения/фра_гменты компилируются в единый файл App/_Code.dll.</span><span class="sxs-lookup"><span data-stu-id="bf88d-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="bf88d-279">Результатом этого изменения является то, что последующие сборки будут намного быстрее, чем в предыдущих версиях.</span><span class="sxs-lookup"><span data-stu-id="bf88d-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-280">Программу командной строки MSBuild может также использоваться для создания приложений ASP.NET Web.</span><span class="sxs-lookup"><span data-stu-id="bf88d-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="bf88d-281">Это средство будет рассматриваться в модуле 9.</span><span class="sxs-lookup"><span data-stu-id="bf88d-281">That tool will be covered in module 9.</span></span>


<span data-ttu-id="bf88d-282">Другое усовершенствование компиляции является "Создать" Страница "сборка" в меню "сборка".</span><span class="sxs-lookup"><span data-stu-id="bf88d-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="bf88d-283">Эта функция позволяет разработчику для перестроения только текущей страницы (вместе с, курс и зависимостей), чтобы изменения, которые могут компилироваться быстрее.</span><span class="sxs-lookup"><span data-stu-id="bf88d-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="bf88d-284">Так, как C# не предлагает фоновая компиляция для целей обновления IntelliSense, т. д., они смогут воспользоваться чрезвычайно эту функцию, так как он позволяет для IntelliSense, чтобы обновить быстро, просто перестроив на одной странице.</span><span class="sxs-lookup"><span data-stu-id="bf88d-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="bf88d-285">Свойства сборки для проекта дают возможность настраивать тип построения, которое происходит перед выполнением страницы запуска.</span><span class="sxs-lookup"><span data-stu-id="bf88d-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="bf88d-286">Разработчики могут выбрать, что Visual Studio можно запускать отладку приложений быстрее после изменения кода построение только текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="bf88d-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>


![Действие построения страницы запуска](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="bf88d-288">**Рис. 9**: Действие построения страницы запуска</span><span class="sxs-lookup"><span data-stu-id="bf88d-288">**Figure 9**: The Build Page Start Action</span></span>


<span data-ttu-id="bf88d-289">Другое усовершенствование отличный Visual Studio и архитектуре ASP.NET находится в области редактирования и продолжить.</span><span class="sxs-lookup"><span data-stu-id="bf88d-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="bf88d-290">В Visual Studio 2005 разработчики могут начать отладку проекта и вносить изменения кода в проекте без отсоединения отладчика.</span><span class="sxs-lookup"><span data-stu-id="bf88d-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="bf88d-291">На самом деле буквально, можно начать отладку проекта, добавьте новый класс, добавьте код для этого класса, добавьте код для страницы, создает новый экземпляр этого класса и выполнение метода класса, все без отсоединения отладчика.</span><span class="sxs-lookup"><span data-stu-id="bf88d-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="bf88d-292">Новый код выполняется практически так же просто, как обновить браузер!</span><span class="sxs-lookup"><span data-stu-id="bf88d-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="bf88d-293">Щелкните здесь, чтобы просмотреть пошаговое видеоруководство правки и продолжить в Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>


![](improvements-in-visual-studio-2005/_static/image2.png)


[<span data-ttu-id="bf88d-294">Открыть весь экран</span><span class="sxs-lookup"><span data-stu-id="bf88d-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)


<span data-ttu-id="bf88d-295">Надежной изменить и продолжить функциональные возможности в ASP.NET 2.0 и Visual Studio 2005 происходит из-за изменения для приложений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bf88d-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="bf88d-296">В ASP.NET 1.x, приложения, созданные в Visual Studio 2002/2003 были скомпилированы в основную сборку, которая была сохранена в папке/Bin.</span><span class="sxs-lookup"><span data-stu-id="bf88d-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="bf88d-297">Все классы, страниц, т. д. для приложения, были скомпилированных в одной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="bf88d-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="bf88d-298">Затем во время выполнения ASP.NET будет компилировать все элементы управления, разметка и код ASP.NET на страницах и скопируйте эти библиотеки DLL в временной папке ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bf88d-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="bf88d-299">В Visual Studio 2005, с помощью ASP.NET 2.0, две компиляции моделей структуры выше (один для Visual Studio) и один для ASP.NET во время выполнения были объединены в одну модель общих компиляции.</span><span class="sxs-lookup"><span data-stu-id="bf88d-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="bf88d-300">Это означает, что все ошибки компиляции теперь перехватываются во время этапа разработки, а не во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="bf88d-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="bf88d-301">Он также позволяет конструктора и поддержку технологии IntelliSense для функции, такие как пользовательские элементы управления и главные страницы.</span><span class="sxs-lookup"><span data-stu-id="bf88d-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="bf88d-302">Щелкните здесь, чтобы просмотреть пошаговое видео поддержку конструктора для пользовательских элементов управления.</span><span class="sxs-lookup"><span data-stu-id="bf88d-302">Click here to see a video walkthrough of designer support for user controls.</span></span>


![](improvements-in-visual-studio-2005/_static/image3.png)


[<span data-ttu-id="bf88d-303">Открыть весь экран</span><span class="sxs-lookup"><span data-stu-id="bf88d-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)


> [!NOTE]
> <span data-ttu-id="bf88d-304">Когда пользовательский элемент управления удаляется из страницы, @Register директива остается в разметке и должны быть удалены вручную, чтобы избежать ошибок синтаксического анализатора, если пользовательский элемент управления удаляется с веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>


<span data-ttu-id="bf88d-305">Еще одно улучшение в модели компиляции Visual Studio — это функция публикации веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="bf88d-306">Так как функцию публикации предварительная компиляция веб-сайта, разработчики получили доступ добавлена производительность не компилируя ничего по запросу.</span><span class="sxs-lookup"><span data-stu-id="bf88d-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="bf88d-307">Он также выполняет предварительную компиляцию весь исходный код в папке приложения/фра_гменты в библиотеку DLL, чтобы исходный код должен быть развернут.</span><span class="sxs-lookup"><span data-stu-id="bf88d-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>


![Диалоговое окно публикации веб-сайта](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="bf88d-309">**Рис. 10**: Диалоговое окно публикации веб-сайта</span><span class="sxs-lookup"><span data-stu-id="bf88d-309">**Figure 10**: The Publish Web Site Dialog</span></span>


> [!NOTE]
> <span data-ttu-id="bf88d-310">Служебную программу aspnet/_compile.exe может также использоваться для предварительной компиляции веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bf88d-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="bf88d-311">Это средство будет рассматриваться в модуле 9.</span><span class="sxs-lookup"><span data-stu-id="bf88d-311">That tool will be covered in module 9.</span></span>


<span data-ttu-id="bf88d-312">При публикации веб-сайта, предварительно скомпилированные файлы хранятся в папке «Temporary ASP.NET Files», как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf88d-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="bf88d-313">Файлы с *.compiled* расширение файла являются XML-файлы, которые определяют зависимости для определенной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="bf88d-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="bf88d-314">Любой веб-форма или пользовательскими элементами управления компилируются в случайных библиотеки DLL, которые начинаются с *приложения /_Web /_*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="bf88d-315">Если оставить *разрешить этот предварительно скомпилированному сайту быть обновляемым* флажок установлен, разметку внутри вашей веб-форм и пользовательские элементы управления не будет предварительно компилируется в библиотеку DLL, что позволяет вносить изменения после развертывания.</span><span class="sxs-lookup"><span data-stu-id="bf88d-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="bf88d-316">Если вы хотите заблокировать разметку, чтобы не допускаются изменения развернутым содержимым, снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="bf88d-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="bf88d-317">*Использовать фиксированное именование и одной сборки страницы* флажок позволяет отключить пакетную компиляцию, чтобы каждая страница компилируется в сборку с именем исправлена.</span><span class="sxs-lookup"><span data-stu-id="bf88d-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="bf88d-318">Оставить этот флажок снят позволяет воспользоваться преимуществами пакетной компиляции.</span><span class="sxs-lookup"><span data-stu-id="bf88d-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="bf88d-319">*Включить строгое именование в предварительно скомпилированные сборки* флажок позволяет строгим именем вашего предварительно скомпилированных сборках.</span><span class="sxs-lookup"><span data-stu-id="bf88d-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-320">В ASP.NET 1.x, должна была устанавливаться в глобальный кэш сборок (GAC) сборок со строгими именами.</span><span class="sxs-lookup"><span data-stu-id="bf88d-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="bf88d-321">В ASP.NET 2.0 вы не требуются для установки сборок со строгими именами в глобальный кэш СБОРОК.</span><span class="sxs-lookup"><span data-stu-id="bf88d-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>


![В предварительно скомпилированных файлов приложения ASP.NET](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="bf88d-323">**Рис. 11**: В предварительно скомпилированных файлов приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bf88d-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>


> [!NOTE]
> <span data-ttu-id="bf88d-324">В приложении выше файл web.config не было.</span><span class="sxs-lookup"><span data-stu-id="bf88d-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="bf88d-325">Если был установлен, он будет уже были вызваны *PrecompiledApp.config* после выполнения публикации веб-сайта процесса.</span><span class="sxs-lookup"><span data-stu-id="bf88d-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>


## <a name="improvements-in-deployment"></a><span data-ttu-id="bf88d-326">Усовершенствования процедуры развертывания</span><span class="sxs-lookup"><span data-stu-id="bf88d-326">Improvements in Deployment</span></span>

<span data-ttu-id="bf88d-327">Как с помощью Visual Studio 2002 и 2003, Visual Studio 2005 предоставляет возможность Копировать проект.</span><span class="sxs-lookup"><span data-stu-id="bf88d-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="bf88d-328">Тем не менее эта функция была усилена в Visual Studio 2005 и теперь называется копирования веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="bf88d-329">Диалоговое окно копирования веб-сайта состоит из левой и правой части.</span><span class="sxs-lookup"><span data-stu-id="bf88d-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="bf88d-330">Левая часть называется исходного веб-сайта и правой части окна вызывается удаленный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="bf88d-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="bf88d-331">Единственное, что может запутать некоторые разработчики является сайта, отображаемое в правой области не обязательно удаленный сайт.</span><span class="sxs-lookup"><span data-stu-id="bf88d-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="bf88d-332">Это может быть сайта в локальной файловой системе или на локальном экземпляре служб IIS.</span><span class="sxs-lookup"><span data-stu-id="bf88d-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="bf88d-333">Кроме того, сайта, отображаемое в левой части окна не обязательно исходного веб-сайта, так как в диалоговом окне можно публиковать на удаленный веб-сайте *для* исходного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="bf88d-334">При копировании проекта на удаленном веб-сайте, что сайт должен иметь серверные расширения FrontPage, установленными на нем.</span><span class="sxs-lookup"><span data-stu-id="bf88d-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="bf88d-335">Если этого не произошло, необходимо подключиться с помощью протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="bf88d-336">С другой стороны при копировании проекта на локальный экземпляр IIS, серверные расширения FrontPage не являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="bf88d-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-337">Если попытаться создать новый веб-сайт на локальном экземпляре служб IIS и установлены серверные расширения FrontPage 2002 г., вы получите сообщение об ошибке, информирующее о том, что создание веб-сайтов не поддерживается на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bf88d-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="bf88d-338">В этом случае у вас есть возможность установки серверных расширений FrontPage 2000 или удаления серверных расширений FrontPage.</span><span class="sxs-lookup"><span data-stu-id="bf88d-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>


<span data-ttu-id="bf88d-339">Щелкните здесь для видеоруководство средства копирования веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="bf88d-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>


![](improvements-in-visual-studio-2005/_static/image4.png)


[<span data-ttu-id="bf88d-340">Открыть весь экран</span><span class="sxs-lookup"><span data-stu-id="bf88d-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)


## <a name="improvements-in-debugging"></a><span data-ttu-id="bf88d-341">Усовершенствования отладки</span><span class="sxs-lookup"><span data-stu-id="bf88d-341">Improvements in Debugging</span></span>

<span data-ttu-id="bf88d-342">Существуют четыре основные улучшения при отладке в Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="bf88d-343">Отладка локально без прав администратора можно без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="bf88d-344">Атрибута отладки элемента компиляции теперь по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="bf88d-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="bf88d-345">Удаленная отладка и настройка невиданной ранее.</span><span class="sxs-lookup"><span data-stu-id="bf88d-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="bf88d-346">Теперь можно отлаживать веб-сайт открывается с помощью FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="bf88d-347">Отладка без прав администратора</span><span class="sxs-lookup"><span data-stu-id="bf88d-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="bf88d-348">Добавление ASP.NET Development Server позволяет упростить отладку приложений ASP.NET готовые – пользователям без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="bf88d-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="bf88d-349">При отладке приложения ASP.NET, работающего в локальной файловой системе, Visual Studio запускает сервер разработки ASP.NET в контексте пользователя, выполнившего вход.</span><span class="sxs-lookup"><span data-stu-id="bf88d-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="bf88d-350">Этот пользователь можно отлаживать приложения без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="bf88d-351">Отладка имеет значение False по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bf88d-351">Debug is False by Default</span></span>

<span data-ttu-id="bf88d-352">В ASP.NET 1.x, *Отладка* атрибут в *компиляции* задано в файле web.config *true* по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bf88d-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="bf88d-353">Всегда были рекомендуется, чтобы разработчики присвоить этому атрибуту значение *false* перед развертыванием приложения в рабочей среде, но так как большинство разработчиков не вполне понимают последствия оставить значение атрибута отладки значение равно true, они просто оставить его как-является.</span><span class="sxs-lookup"><span data-stu-id="bf88d-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="bf88d-354">Наиболее серьезные проблемы с входящим атрибута отладки значение true — что он отключает ASP.NETs пакетной компиляции модели.</span><span class="sxs-lookup"><span data-stu-id="bf88d-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="bf88d-355">Таким образом каждая страница компилируется в отдельной библиотеке DLL.</span><span class="sxs-lookup"><span data-stu-id="bf88d-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="bf88d-356">Если веб-приложение включает в себя тысячи страниц (не знал по любым способом), это значит, что несколько тысяч небольших библиотек DLL создается этим приложением.</span><span class="sxs-lookup"><span data-stu-id="bf88d-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="bf88d-357">Хотя эти библиотеки DLL и небольшой размер, они не загружены в любой из определенного расположения в памяти.</span><span class="sxs-lookup"><span data-stu-id="bf88d-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="bf88d-358">Таким образом они привести к фрагментации в системной памяти и можно взаимодействовать с OutOfMemoryException вхождений.</span><span class="sxs-lookup"><span data-stu-id="bf88d-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="bf88d-359">В ASP.NET 2.0 атрибута отладки значение false по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bf88d-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="bf88d-360">Как вы уже видели, когда разработчик выполняет отладку приложения ASP.NET в Visual Studio 2005, ему будет предложено добавить файл web.config с включенной отладкой.</span><span class="sxs-lookup"><span data-stu-id="bf88d-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="bf88d-361">Это приводит к тем же недостатки, которые присутствовали в ASP.NET 1.x, но теперь разработчик четко предупреждается о том, что атрибут сбрасывается в значение false перед перемещением приложения в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bf88d-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="bf88d-362">Настройка удаленной отладки и конфигурации</span><span class="sxs-lookup"><span data-stu-id="bf88d-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="bf88d-363">В Visual Studio 2002/2003, удаленная отладка полагались на диспетчера отладки (mdm.exe) и процесс vs7jit.exe.</span><span class="sxs-lookup"><span data-stu-id="bf88d-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="bf88d-364">Из-за этого Устранение неполадок удаленной отладки была часто черного прямоугольника для клиентов, и она не часто гораздо лучше подходит для службы технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="bf88d-365">Visual Studio 2005 устраняет зависимость от mdm.exe и vs7jit.exe процессы.</span><span class="sxs-lookup"><span data-stu-id="bf88d-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="bf88d-366">Вместо этого он теперь использует службу монитор удаленной отладки (msvsmon.exe).</span><span class="sxs-lookup"><span data-stu-id="bf88d-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="bf88d-367">Требования для удаленной отладки в Visual Studio 2005 довольно прост.</span><span class="sxs-lookup"><span data-stu-id="bf88d-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="bf88d-368">Необходимо запустить msvsmon.exe на удаленном сервере до отладки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="bf88d-369">Можно установить монитор удаленной отладки Visual Studio с компакт-диска или просто запустите msvsmon.exe из общей папки без установки на всех веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="bf88d-370">При запуске msvsmon.exe, вполне вероятно, что он выдаст ошибку, о портах, заблокировано для удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="bf88d-371">К счастью можно легко разблокировать порты справа в диалоговое окно с предупреждением, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf88d-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>


![Уведомление о брандмауэр Windows блокирует удаленную отладку](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="bf88d-373">**Рис. 12**: Уведомление о брандмауэр Windows блокирует удаленную отладку</span><span class="sxs-lookup"><span data-stu-id="bf88d-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>


<span data-ttu-id="bf88d-374">После разблокировки порты, необходимые для отладки вы увидите монитор удаленной отладки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf88d-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="bf88d-375">Из этого интерфейса можно отслеживать подключения и изменять, легко разрешение на отладку.</span><span class="sxs-lookup"><span data-stu-id="bf88d-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>


![Монитор удаленной отладки](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="bf88d-377">**Рис. 13**: Монитор удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="bf88d-377">**Figure 13**: The Remote Debugging Monitor</span></span>


<span data-ttu-id="bf88d-378">Можно также удаленная отладка веб-приложения, открывается с помощью FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="bf88d-379">Действия являются такие же, как описано ранее.</span><span class="sxs-lookup"><span data-stu-id="bf88d-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="bf88d-380">Тем не менее необходимо будет указать базовый URL-адрес для просмотра проекта FTP, как описано ранее в этом модуле.</span><span class="sxs-lookup"><span data-stu-id="bf88d-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="bf88d-381">Практическое занятие №2</span><span class="sxs-lookup"><span data-stu-id="bf88d-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="bf88d-382">Удаленная отладка с помощью Visual Studio 2005</span><span class="sxs-lookup"><span data-stu-id="bf88d-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="bf88d-383">Это лабораторное занятие поможет выполнить удаленную отладку с помощью Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="bf88d-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="bf88d-384">Щелкните здесь для видеоруководство для этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bf88d-384">Click here for a video walkthrough of this lab.</span></span>


![](improvements-in-visual-studio-2005/_static/image5.png)


[<span data-ttu-id="bf88d-385">Открыть весь экран</span><span class="sxs-lookup"><span data-stu-id="bf88d-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)


<span data-ttu-id="bf88d-386">Это лабораторное занятие требует наличия двух машин, одной работающей Visual Studio 2005 и других выполнение IIS 5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="bf88d-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="bf88d-387">Откройте Visual Studio 2005 и создайте новый веб-сайт на удаленном сервере.</span><span class="sxs-lookup"><span data-stu-id="bf88d-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="bf88d-388">Можно создать веб-сайт, на удаленном экземпляре служб IIS, либо через FTP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>


1. <span data-ttu-id="bf88d-389">Найдите msvsmon.exe на компьютере разработки, используя UNC-путь удаленного веб-сервера и выполните его.</span><span class="sxs-lookup"><span data-stu-id="bf88d-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="bf88d-390">Местоположение по умолчанию msvsmon.exe — //server/c$/Program файлы/Microsoft Visual Studio 8/Common7/IDE/удаленного отладчика/x86.</span><span class="sxs-lookup"><span data-stu-id="bf88d-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="bf88d-391">Если будет предложено разблокировать порты для удаленной отладки, сделайте это.</span><span class="sxs-lookup"><span data-stu-id="bf88d-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="bf88d-392">На компьютере разработки откройте кода для Default.aspx и установите точку останова в методе страницы/_подсистема.</span><span class="sxs-lookup"><span data-stu-id="bf88d-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="bf88d-393">Запустите отладку на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="bf88d-394">Вы должны достичь точки останова, должным образом.</span><span class="sxs-lookup"><span data-stu-id="bf88d-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="bf88d-395">Сервер ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="bf88d-395">ASP.NET Development Server</span></span>

<span data-ttu-id="bf88d-396">Как уже описано weve Visual Studio 2005 поставляется с веб-сервере ASP.NET Development Server.</span><span class="sxs-lookup"><span data-stu-id="bf88d-396">As weve already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="bf88d-397">(ASP.NET Development Server иногда называется Cassini.) Этот веб-сервер — это удобный способ для просмотра и отладки приложений, работающих в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="bf88d-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="bf88d-398">Сервер разработки ASP.NET является ограниченным доступом веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="bf88d-399">Не поддерживает удаленные соединения, не поддерживает все запросы из любого пользователя, отличного от пользователя, запустившего веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="bf88d-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="bf88d-400">Он также имеет возможность обслуживания страниц ASP.</span><span class="sxs-lookup"><span data-stu-id="bf88d-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="bf88d-401">Обслуживаются только ресурсы по ASP.NET и HTML ресурсов (включая изображения, файлы CSS и др.).</span><span class="sxs-lookup"><span data-stu-id="bf88d-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="bf88d-402">ASP.NET Development Server можно запустить из командной строки, запустив файл WebDev.WebServer.exe, расположенный в папке c:/Windows/Microsoft.NET/Framework/v2.0./*/* /  */*/\*.</span><span class="sxs-lookup"><span data-stu-id="bf88d-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="bf88d-403">Следующее диалоговое окно отображает параметры, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="bf88d-403">The following dialog displays the parameters that are available.</span></span>


![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="bf88d-404">**Рис. 14**</span><span class="sxs-lookup"><span data-stu-id="bf88d-404">**Figure 14**</span></span>


> [!NOTE]
> <span data-ttu-id="bf88d-405">ASP.NET Development Server не поддерживается при запуске явным образом с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="bf88d-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
