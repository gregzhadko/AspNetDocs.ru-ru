---
uid: ajax/cdn/overview
title: Сеть доставки содержимого Microsoft AJAX | Документация Майкрософт
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 9eebe0e52af2a0fca967a51afb58c7db174d9fdb
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702924"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="0b17f-102">Сеть доставки содержимого Microsoft Ajax</span><span class="sxs-lookup"><span data-stu-id="0b17f-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="0b17f-103">Рабочие приложения не должны иметь жесткой зависимости от ресурсов CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="0b17f-104">Приложения должны проверить наличие упоминаемого ресурса CDN и использовать резервный ресурс, если сеть CDN недоступна.</span><span class="sxs-lookup"><span data-stu-id="0b17f-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="0b17f-105">У сети CDN Microsoft Ajax нет соглашения об уровне обслуживания, чем при использовании Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="0b17f-106">Используйте [эту проблему GitHub](https://github.com/dotnet/AspNetDocs/issues/116) , чтобы сообщить о проблемах с CDN Microsoft AJAX.</span><span class="sxs-lookup"><span data-stu-id="0b17f-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="0b17f-107">Оглавление</span><span class="sxs-lookup"><span data-stu-id="0b17f-107">Table of Contents</span></span>

<span data-ttu-id="0b17f-108">**[ajax.microsoft.com переименован в ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="0b17f-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="0b17f-109">**[Поддержка Visual Studio. всдок](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="0b17f-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="0b17f-110">**[Использование ASP.NET AJAX из CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="0b17f-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="0b17f-111">**[Использование jQuery из CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="0b17f-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="0b17f-112">**[Использование пользовательского интерфейса jQuery из CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="0b17f-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="0b17f-113">**[Сторонние файлы в сети CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="0b17f-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="0b17f-114">выпуски jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="0b17f-115">Миграция в jQuery выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="0b17f-116">выпуски пользовательского интерфейса jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="0b17f-117">выпуски проверки jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="0b17f-118">Мобильные выпуски jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="0b17f-119">выпуски шаблонов jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="0b17f-120">Циклические выпуски jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="0b17f-121">Таблицы данных jQuery выпуски в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="0b17f-122">Modernizr выпуски в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="0b17f-123">Жшинт выпуски в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="0b17f-124">Маскирование выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="0b17f-125">Глобализация выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="0b17f-126">Реагирование на выпуски CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="0b17f-127">Начальные версии в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="0b17f-128">Начальная загрузка выпусков Таучкараусел в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="0b17f-129">Hammer.js выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="0b17f-130">ASP.NET веб-формы и выпуски AJAX в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="0b17f-131">Выпуски MVC ASP.NET в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="0b17f-132">Выпуски SignalR ASP.NET в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="0b17f-133">Сеть доставки содержимого (CDN) Microsoft AJAX содержит популярные сторонние библиотеки JavaScript, такие как jQuery, и позволяет легко добавлять их в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0b17f-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="0b17f-134">Например, можно начать использовать jQuery, размещенный в этой сети CDN, просто добавив &lt; тег скрипта &gt; на страницу, указывающий на AJAX.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="0b17f-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="0b17f-135">Используя преимущества CDN, можно значительно повысить производительность приложений AJAX.</span><span class="sxs-lookup"><span data-stu-id="0b17f-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="0b17f-136">Содержимое CDN кэшируется на серверах, расположенных по всему миру.</span><span class="sxs-lookup"><span data-stu-id="0b17f-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="0b17f-137">Кроме того, CDN позволяет браузерам повторно использовать кэшированные сторонние файлы JavaScript для веб-сайтов, расположенных в разных доменах.</span><span class="sxs-lookup"><span data-stu-id="0b17f-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="0b17f-138">CDN поддерживает протокол SSL (HTTPS), если необходимо обслуживать веб-страницу с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="0b17f-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="0b17f-139">В CDN размещаются следующие библиотеки сценариев сторонних производителей, которые были отправлены и лицензированы вам владельцами этих библиотек:</span><span class="sxs-lookup"><span data-stu-id="0b17f-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="0b17f-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="0b17f-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="0b17f-141">Пользовательский интерфейс jQuery (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="0b17f-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="0b17f-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="0b17f-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="0b17f-143">Проверка jQuery (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="0b17f-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="0b17f-144">Цикл jQuery (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="0b17f-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="0b17f-145">Таблицы данных jQuery (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="0b17f-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="0b17f-146">Сеть CDN Microsoft Ajax также включает следующие библиотеки, которые были переданы корпорацией Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="0b17f-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="0b17f-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="0b17f-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="0b17f-148">Файлы JavaScript ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0b17f-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="0b17f-149">Файлы JavaScript SignalR ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0b17f-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="0b17f-150">Корпорация Майкрософт не заказывает владение какими-либо сторонними библиотеками, размещенными в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="0b17f-151">Владельцы авторских прав библиотек являются лицензированием этих библиотек.</span><span class="sxs-lookup"><span data-stu-id="0b17f-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="0b17f-152">Все права, которые могут потребоваться для загрузки и использования этих библиотек, предоставляются только соответствующим владельцам авторских прав.</span><span class="sxs-lookup"><span data-stu-id="0b17f-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="0b17f-153">Так как это не библиотеки Майкрософт, корпорация Майкрософт не предоставляет никаких гарантий или лицензий на права интеллектуальной собственности (включая неявные патентные права) для библиотек сторонних производителей, размещенных в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="0b17f-154">Если вы хотите отправить библиотеку JavaScript, а ваша библиотека является одной из основных библиотек JavaScript (как указано в списке http://trends.builtwith.com) или расширений/подключаемых модулей для этих библиотек, которые являются популярными, или (б) для использования в ASP.NET, обратитесь к AjaxCDNSubmission@Microsoft.com .</span><span class="sxs-lookup"><span data-stu-id="0b17f-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="0b17f-155">ajax.microsoft.com переименован в ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="0b17f-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="0b17f-156">CDN, используемый для использования доменного имени microsoft.com, был изменен на использование доменного имени aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="0b17f-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="0b17f-157">Это изменение было внесено для повышения производительности, так как когда браузер ссылался на домен microsoft.com, он будет передавать файлы cookie из этого домена по сети при каждом запросе.</span><span class="sxs-lookup"><span data-stu-id="0b17f-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="0b17f-158">Переименование в доменное имя, отличное от microsoft.com, может увеличиться на 25%.</span><span class="sxs-lookup"><span data-stu-id="0b17f-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="0b17f-159">Примечание. ajax.microsoft.com будет продолжать работать, но рекомендуется ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="0b17f-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="0b17f-160">Старый формат: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="0b17f-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="0b17f-161">Новый формат: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="0b17f-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="0b17f-162">Поддержка Visual Studio. всдок</span><span class="sxs-lookup"><span data-stu-id="0b17f-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="0b17f-163">Чтобы правильно использовать всдок файлы в Visual Studio 2008, необходимо убедиться в наличии установленного пакета VS 2008 SP1 и исправления для файлов всдок.</span><span class="sxs-lookup"><span data-stu-id="0b17f-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="0b17f-164">Их можно получить здесь:</span><span class="sxs-lookup"><span data-stu-id="0b17f-164">You can get these from here:</span></span>

- <span data-ttu-id="0b17f-165">[Загрузка пакета обновления 1 (SP1) для Visual Studio 2008](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Загрузка пакета обновления 1 (SP1) для Visual Studio 2008")</span><span class="sxs-lookup"><span data-stu-id="0b17f-165">[Download Visual Studio 2008 SP1](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Download Visual Studio 2008 SP1")</span></span>
- [<span data-ttu-id="0b17f-166">Скачать всдок исправление для Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="0b17f-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Скачать всдок исправление для Visual Studio 2008 SP1")

<span data-ttu-id="0b17f-167">Visual Studio 2010 поддерживает файлы всдок без дополнительных исправлений.</span><span class="sxs-lookup"><span data-stu-id="0b17f-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="0b17f-168">Использование ASP.NET AJAX из CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="0b17f-169">При использовании ASP.NET 4 можно перенаправить все запросы на скрипты ASP.NET Framework в CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="0b17f-170">Получение скриптов из CDN вместо локального веб-сервера может значительно повысить производительность общедоступных веб-сайтов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0b17f-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="0b17f-171">Используйте свойство ScriptManager Енаблекдн, чтобы перенаправить все запросы сценариев ASP.NET Framework в сеть CDN Microsoft Ajax:</span><span class="sxs-lookup"><span data-stu-id="0b17f-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="0b17f-172">Использование jQuery из CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="0b17f-173">Вы можете использовать скрипты jQuery, размещенные в CDN, в веб-приложении, добавив следующий элемент скрипта на страницу:</span><span class="sxs-lookup"><span data-stu-id="0b17f-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="0b17f-174">CDN также включает версию минифицированные скрипта jQuery, которую можно получить с помощью следующего элемента:</span><span class="sxs-lookup"><span data-stu-id="0b17f-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="0b17f-175">Чтобы разрешить странице переход на загрузку jQuery из локального пути на вашем веб-сайте, если сеть CDN недоступна, добавьте следующий элемент сразу после элемента, ссылающегося на CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="0b17f-176">На следующем образце страницы используется версия CDN библиотеки jQuery (с резервной копией на локальную копию) для вывода содержимого элемента div при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="0b17f-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="0b17f-177">Дополнительные сведения о jQuery и скачивании локальной копии jQuery можно получить на веб-сайте [jQuery](http://jquery.com/) .</span><span class="sxs-lookup"><span data-stu-id="0b17f-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="0b17f-178">Использование пользовательского интерфейса jQuery из CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="0b17f-179">В CDN также размещается библиотека пользовательского интерфейса jQuery.</span><span class="sxs-lookup"><span data-stu-id="0b17f-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="0b17f-180">Библиотека пользовательского интерфейса jQuery содержит обширный набор мини-приложений и эффектов, которые можно использовать в приложениях ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0b17f-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="0b17f-181">Например, на следующей странице показано, как можно использовать DatePicker пользовательского интерфейса jQuery в контексте приложения ASP.NET Web Forms для отображения всплывающего календаря:</span><span class="sxs-lookup"><span data-stu-id="0b17f-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="0b17f-182">При перемещении фокуса на текстовое поле с помощью клавиатуры отображается календарь:</span><span class="sxs-lookup"><span data-stu-id="0b17f-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Всплывающий календарь, созданный с помощью DatePicker](overview/_static/image1.png)

<span data-ttu-id="0b17f-184">Обратите внимание, что в приведенном выше коде необходимо включить три файла из CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="0b17f-185">Библиотека JQuery библиотеки &mdash; пользовательского интерфейса jQuery зависит от библиотеки jQuery.</span><span class="sxs-lookup"><span data-stu-id="0b17f-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="0b17f-186">Перед добавлением библиотеки пользовательского интерфейса jQuery необходимо добавить библиотеку jQuery на страницу.</span><span class="sxs-lookup"><span data-stu-id="0b17f-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="0b17f-187">Библиотека пользовательского интерфейса jQuery &mdash; Библиотека пользовательского интерфейса jQuery содержит все эффекты и мини-приложения для пользовательского интерфейса jQuery, такие как мини-приложение DatePicker, используемое на странице выше.</span><span class="sxs-lookup"><span data-stu-id="0b17f-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="0b17f-188">Тема пользовательского интерфейса jQuery &mdash; . Пользовательский интерфейс jQuery поддерживает различные темы.</span><span class="sxs-lookup"><span data-stu-id="0b17f-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="0b17f-189">На приведенной выше странице содержится ссылка на CSS-файл для импорта темы Redmond.</span><span class="sxs-lookup"><span data-stu-id="0b17f-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="0b17f-190">Все стандартные темы пользовательского интерфейса jQuery размещаются в CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="0b17f-191">[Посетите эту страницу](jquery-ui/cdnjqueryui1910.md "Пользовательский интерфейс jQuery 1.8.10 в сети доставки содержимого Microsoft Ajax") , чтобы просмотреть эскизы для каждой темы.</span><span class="sxs-lookup"><span data-stu-id="0b17f-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="0b17f-192">Дополнительные сведения о библиотеке UI jQuery см. на официальном [веб-сайте интерфейса jQuery](http://jQueryUI.com "веб-сайт пользовательского интерфейса jQuery").</span><span class="sxs-lookup"><span data-stu-id="0b17f-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="0b17f-193">Сторонние файлы в сети CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="0b17f-194">В CDN размещаются некоторые из наиболее популярных библиотек JavaScript сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="0b17f-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="0b17f-195">Корпорация Майкрософт не заказывает владение какими-либо сторонними библиотеками, размещенными в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="0b17f-196">Владельцы авторских прав библиотек являются лицензированием этих библиотек.</span><span class="sxs-lookup"><span data-stu-id="0b17f-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="0b17f-197">Все права, которые могут потребоваться для загрузки и использования этих библиотек, предоставляются только соответствующим владельцам авторских прав.</span><span class="sxs-lookup"><span data-stu-id="0b17f-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="0b17f-198">Так как это не библиотеки Майкрософт, корпорация Майкрософт не предоставляет никаких гарантий или лицензий на права интеллектуальной собственности (включая неявные патентные права) для библиотек сторонних производителей, размещенных в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="0b17f-199">выпуски jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="0b17f-200">Следующие выпуски jQuery размещаются в CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-351"></a><span data-ttu-id="0b17f-201">jQuery версии 3.5.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-201">jQuery version 3.5.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.min.map

#### <a name="jquery-version-350"></a><span data-ttu-id="0b17f-202">jQuery версии 3.5.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-202">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="0b17f-203">jQuery версии 3.4.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-203">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="0b17f-204">jQuery версии 3.4.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-204">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="0b17f-205">jQuery версии 3.3.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-205">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="0b17f-206">jQuery версии 3.2.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-206">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="0b17f-207">jQuery версии 3.2.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-207">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="0b17f-208">jQuery версии 3.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-208">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="0b17f-209">jQuery версии 3.1.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-209">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="0b17f-210">jQuery версии 3.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-210">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="0b17f-211">jQuery версии 2.2.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-211">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="0b17f-212">jQuery версии 2.2.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-212">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="0b17f-213">jQuery версии 2.2.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-213">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="0b17f-214">jQuery версии 2.2.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-214">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="0b17f-215">jQuery версии 2.2.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-215">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="0b17f-216">jQuery версии 2.1.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-216">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="0b17f-217">jQuery версии 2.1.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-217">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="0b17f-218">jQuery версии 2.1.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-218">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="0b17f-219">jQuery версии, версия</span><span class="sxs-lookup"><span data-stu-id="0b17f-219">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="0b17f-220">jQuery версии 2.1.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-220">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="0b17f-221">jQuery версии 2.0.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-221">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="0b17f-222">jQuery версии 2.0.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-222">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="0b17f-223">jQuery версии 2.0.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-223">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="0b17f-224">jQuery версии 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-224">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="0b17f-225">jQuery версии 1.12.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-225">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="0b17f-226">jQuery версии 1.12.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-226">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="0b17f-227">jQuery версии 1.12.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-227">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="0b17f-228">jQuery версии 1.12.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-228">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="0b17f-229">jQuery версии 1.12.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-229">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="0b17f-230">jQuery версии 1.11.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-230">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="0b17f-231">jQuery версии 1.11.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-231">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="0b17f-232">jQuery версии 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-232">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="0b17f-233">jQuery версии 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-233">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="0b17f-234">jQuery версии 1.10.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-234">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="0b17f-235">jQuery версии 1.10.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-235">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="0b17f-236">jQuery версии 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-236">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="0b17f-237">jQuery версии 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-237">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="0b17f-238">jQuery версии 1.9.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-238">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="0b17f-239">jQuery версии 1.8.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-239">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="0b17f-240">jQuery версии 1.8.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-240">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="0b17f-241">jQuery версии 1.8.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-241">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="0b17f-242">jQuery версии 1.8.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-242">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="0b17f-243">jQuery версии 1.7.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-243">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="0b17f-244">jQuery версии 1.7.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-244">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="0b17f-245">jQuery версии 1,7</span><span class="sxs-lookup"><span data-stu-id="0b17f-245">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="0b17f-246">jQuery версии 1.6.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-246">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="0b17f-247">jQuery версии 1.6.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-247">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="0b17f-248">jQuery версии 1.6.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-248">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="0b17f-249">jQuery версии 1.6.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-249">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="0b17f-250">jQuery версии 1,6</span><span class="sxs-lookup"><span data-stu-id="0b17f-250">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="0b17f-251">jQuery версии 1.5.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-251">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="0b17f-252">jQuery версии 1.5.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-252">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="0b17f-253">jQuery версии 1,5</span><span class="sxs-lookup"><span data-stu-id="0b17f-253">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="0b17f-254">jQuery версии 1.4.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-254">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="0b17f-255">jQuery версии 1.4.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-255">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="0b17f-256">jQuery версии 1.4.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-256">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="0b17f-257">jQuery версии 1.4.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-257">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="0b17f-258">jQuery версии 1,4</span><span class="sxs-lookup"><span data-stu-id="0b17f-258">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="0b17f-259">jQuery версии 1.3.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-259">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="0b17f-260">Миграция в jQuery выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-260">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="0b17f-261">Следующие выпуски jQuery Migrate размещены в сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-261">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="0b17f-262">Миграция jQuery версии 3.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-262">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="0b17f-263">Миграция jQuery версии 1.2.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-263">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="0b17f-264">Миграция jQuery версии 1.2.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-264">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="0b17f-265">Миграция jQuery версии 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-265">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="0b17f-266">Миграция jQuery версии 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-266">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="0b17f-267">Миграция jQuery версии 1.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-267">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="0b17f-268">выпуски пользовательского интерфейса jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-268">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="0b17f-269">Следующие выпуски библиотеки пользовательского интерфейса jQuery размещаются в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-269">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="0b17f-270">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-270">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-271">1.12.1 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-271">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Пользовательский интерфейс jQuery 1.12.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-272">1.12.0 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-272">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Пользовательский интерфейс jQuery 1.12.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-273">1.11.4 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-273">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Пользовательский интерфейс jQuery 1.11.4 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-274">1.11.3 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-274">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Пользовательский интерфейс jQuery 1.11.3 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-275">1.11.2 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-275">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Пользовательский интерфейс jQuery 1.11.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-276">1.11.1 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-276">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Пользовательский интерфейс jQuery 1.11.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-277">1.11.0 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-277">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Пользовательский интерфейс jQuery 1.11.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-278">1.10.4 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-278">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Пользовательский интерфейс jQuery 1.10.4 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-279">1.10.3 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-279">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Пользовательский интерфейс jQuery 1.10.3 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-280">1.10.2 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-280">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Пользовательский интерфейс jQuery 1.10.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-281">1.10.1 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-281">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Пользовательский интерфейс jQuery 1.10.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-282">1.10.0 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-282">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Пользовательский интерфейс jQuery 1.10.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-283">1.9.2 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-283">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Пользовательский интерфейс jQuery 1.9.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-284">1.9.1 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-284">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Пользовательский интерфейс jQuery 1.9.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-285">1.9.0 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-285">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Пользовательский интерфейс jQuery 1.9.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-286">1.8.24 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-286">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Пользовательский интерфейс jQuery 1.8.24 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-287">1.8.23 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-287">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Пользовательский интерфейс jQuery 1.8.23 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-288">1.8.22 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-288">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Пользовательский интерфейс jQuery 1.8.22 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-289">1.8.21 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-289">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Пользовательский интерфейс jQuery 1.8.21 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-290">1.8.20 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-290">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Пользовательский интерфейс jQuery 1.8.20 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-291">1.8.19 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-291">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Пользовательский интерфейс jQuery 1.8.19 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-292">1.8.18 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-292">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Пользовательский интерфейс jQuery 1.8.18 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-293">1.8.17 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-293">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Пользовательский интерфейс jQuery 1.8.17 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-294">1.8.16 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-294">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Пользовательский интерфейс jQuery 1.8.16 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-295">1.8.15 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-295">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Пользовательский интерфейс jQuery 1.8.15 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-296">1.8.14 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-296">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Пользовательский интерфейс jQuery 1.8.14 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-297">1.8.13 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-297">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Пользовательский интерфейс jQuery 1.8.13 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-298">1.8.12 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-298">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Пользовательский интерфейс jQuery 1.8.12 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-299">jQuery UI 1.8.11.</span><span class="sxs-lookup"><span data-stu-id="0b17f-299">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Пользовательский интерфейс jQuery 1.8.11 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-300">1.8.10 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-300">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Пользовательский интерфейс jQuery 1.8.10 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-301">1.8.9 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-301">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Пользовательский интерфейс jQuery 1.8.9 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-302">1.8.8 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-302">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Пользовательский интерфейс jQuery 1.8.8 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-303">1.8.7 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-303">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Пользовательский интерфейс jQuery 1.8.7 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-304">1.8.6 пользовательского интерфейса jQuery</span><span class="sxs-lookup"><span data-stu-id="0b17f-304">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Пользовательский интерфейс jQuery 1.8.6 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-305">Пользовательский интерфейс jQuery 1.8.5</span><span class="sxs-lookup"><span data-stu-id="0b17f-305">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "Пользовательский интерфейс jQuery 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="0b17f-306">выпуски проверки jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-306">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="0b17f-307">Следующие выпуски подключаемого модуля [проверки JQuery](https://jqueryvalidation.org/ "Подключаемый модуль проверки jQuery") размещаются в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-307">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b17f-308">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-308">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-309">jQuery проверить 1.19.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-309">jQuery Validate 1.19.2</span></span>](jquery-validate/cdnjqueryvalidate1192.md "1.19.2 проверки jQuery")
- [<span data-ttu-id="0b17f-310">jQuery проверить 1.19.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-310">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "1.19.1 проверки jQuery")
- [<span data-ttu-id="0b17f-311">jQuery проверить 1.19.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-311">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "1.19.0 проверки jQuery")
- [<span data-ttu-id="0b17f-312">jQuery проверить 1.17.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-312">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "1.17.0 проверки jQuery")
- [<span data-ttu-id="0b17f-313">jQuery проверить 1.16.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-313">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="0b17f-314">jQuery проверить 1.15.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-314">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="0b17f-315">jQuery проверить 1.15.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-315">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="0b17f-316">jQuery проверить 1.14.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-316">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="0b17f-317">jQuery проверить 1.13.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-317">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="0b17f-318">jQuery проверить 1.13.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-318">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validate 1.13.0")
- [<span data-ttu-id="0b17f-319">jQuery проверить 1.12.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-319">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validate 1.12.0")
- [<span data-ttu-id="0b17f-320">jQuery проверить 1.11.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-320">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validate 1.11.1")
- [<span data-ttu-id="0b17f-321">jQuery проверить 1.11.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-321">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validate 1.11.0")
- [<span data-ttu-id="0b17f-322">jQuery проверить 1.10.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-322">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validate 1.10.0")
- [<span data-ttu-id="0b17f-323">jQuery Validate 1,9</span><span class="sxs-lookup"><span data-stu-id="0b17f-323">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate версии 1.9")
- [<span data-ttu-id="0b17f-324">jQuery проверить 1.8.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-324">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate версии 1.8.1")
- [<span data-ttu-id="0b17f-325">jQuery Validate 1,8</span><span class="sxs-lookup"><span data-stu-id="0b17f-325">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate версии 1.8")
- [<span data-ttu-id="0b17f-326">jQuery Validate 1,7</span><span class="sxs-lookup"><span data-stu-id="0b17f-326">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate версии 1.7")
- [<span data-ttu-id="0b17f-327">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="0b17f-327">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="0b17f-328">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="0b17f-328">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="0b17f-329">Мобильные выпуски jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-329">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="0b17f-330">Следующие выпуски мобильной библиотеки jQuery размещены в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-330">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="0b17f-331">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-331">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-332">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="0b17f-332">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-333">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-333">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-334">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-334">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-335">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-335">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-336">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-336">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-337">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-337">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-338">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-338">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-339">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-339">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-340">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-340">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-341">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-341">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-342">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-342">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-343">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="0b17f-343">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-344">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-344">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-345">jQuery Mobile 1,0</span><span class="sxs-lookup"><span data-stu-id="0b17f-345">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-346">jQuery Mobile 1,0 RC 2</span><span class="sxs-lookup"><span data-stu-id="0b17f-346">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-347">jQuery Mobile 1,0 RC 1</span><span class="sxs-lookup"><span data-stu-id="0b17f-347">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="0b17f-348">jQuery Mobile 1,0, бета-версия 3</span><span class="sxs-lookup"><span data-stu-id="0b17f-348">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 бета-версии 3 в сети доставки содержимого Microsoft Ajax")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="0b17f-349">выпуски шаблонов jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-349">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="0b17f-350">Следующие выпуски подключаемого модуля шаблонов jQuery размещаются в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-350">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b17f-351">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-351">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-352">jQuery Templates, бета-версия 1</span><span class="sxs-lookup"><span data-stu-id="0b17f-352">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates, бета-версия 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="0b17f-353">Циклические выпуски jQuery в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-353">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="0b17f-354">Следующие выпуски подключаемого модуля jQuery Cycle размещены в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-354">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b17f-355">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-355">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-356">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="0b17f-356">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="0b17f-357">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="0b17f-357">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="0b17f-358">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="0b17f-358">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="0b17f-359">Таблицы данных jQuery выпуски в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-359">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="0b17f-360">Следующие выпуски подключаемого модуля таблиц данных jQuery размещаются в этой сети CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-360">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="0b17f-361">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-361">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-362">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="0b17f-362">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="0b17f-363">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-363">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="0b17f-364">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-364">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="0b17f-365">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-365">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="0b17f-366">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-366">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="0b17f-367">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-367">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="0b17f-368">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-368">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="0b17f-369">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-369">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="0b17f-370">Modernizr выпуски в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-370">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="0b17f-371">Следующие выпуски [Modernizr](http://www.modernizr.com "Modernizr") размещаются в CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-371">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="0b17f-372">Жшинт выпуски в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-372">JSHint Releases on the CDN</span></span>

<span data-ttu-id="0b17f-373">Следующие выпуски [жшинт](http://www.jshint.com "жшинт") размещаются в CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-373">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="0b17f-374">Маскирование выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-374">Knockout Releases on the CDN</span></span>

<span data-ttu-id="0b17f-375">Следующие выпуски [маскирования](http://www.knockoutjs.com "Выход") размещаются в CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-375">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="0b17f-376">Глобализация выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-376">Globalize Releases on the CDN</span></span>

<span data-ttu-id="0b17f-377">Следующие выпуски [глобализации](https://github.com/jquery/globalize "Глобализации") размещаются в CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-377">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="0b17f-378">Глобализация версии 1.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-378">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="0b17f-379">Глобализация версии 0.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-379">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="0b17f-380">Все языки и региональные параметры</span><span class="sxs-lookup"><span data-stu-id="0b17f-380">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="0b17f-381">Замените "{Culture-Code}" требуемым кодом языка и региональных параметров, например globalize.culture.en-GB.js= = Microsoft Files in the CDN = = эти библиотеки были переданы корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0b17f-381">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="0b17f-382">Реагирование на выпуски CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-382">Respond Releases on the CDN</span></span>

<span data-ttu-id="0b17f-383">Следующие выпуски [ответов](https://github.com/scottjehl/Respond "Устранение") размещаются в сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-383">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="0b17f-384">Отклик версии 1.4.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-384">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="0b17f-385">Отклик версии 1.4.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-385">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="0b17f-386">Отклик версии 1.4.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-386">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="0b17f-387">Отклик версии 1.3.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-387">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="0b17f-388">Отклик версии 1.2.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-388">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="0b17f-389">Начальные версии в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-389">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="0b17f-390">Следующие выпуски [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") начальной загрузки размещаются в сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-390">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-452"></a><span data-ttu-id="0b17f-391">Версия начальной загрузки 4.5.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-391">Bootstrap version 4.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-450"></a><span data-ttu-id="0b17f-392">Версия начальной загрузки 4.5.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-392">Bootstrap version 4.5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-441"></a><span data-ttu-id="0b17f-393">Версия начальной загрузки 4.4.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-393">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="0b17f-394">Версия начальной загрузки 4.3.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-394">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="0b17f-395">Версия начальной загрузки 4.2.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-395">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="0b17f-396">Версия начальной загрузки 4.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-396">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="0b17f-397">Версия начальной загрузки 4.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-397">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="0b17f-398">Версия начальной загрузки 3.4.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-398">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="0b17f-399">Версия начальной загрузки 3.4.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-399">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="0b17f-400">Версия начальной загрузки 3.3.7</span><span class="sxs-lookup"><span data-stu-id="0b17f-400">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="0b17f-401">Версия начальной загрузки 3.3.6</span><span class="sxs-lookup"><span data-stu-id="0b17f-401">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="0b17f-402">Версия начальной загрузки 3.3.5</span><span class="sxs-lookup"><span data-stu-id="0b17f-402">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="0b17f-403">Версия начальной загрузки 3.3.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-403">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="0b17f-404">Версия начальной загрузки 3.3.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-404">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="0b17f-405">Версия начальной загрузки 3.3.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-405">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="0b17f-406">Версия начальной загрузки 3.3.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-406">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="0b17f-407">Версия начальной загрузки 3.2.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-407">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="0b17f-408">Версия начальной загрузки 3.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-408">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="0b17f-409">Версия начальной загрузки 3.1.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-409">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="0b17f-410">Версия начальной загрузки 3.0.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-410">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="0b17f-411">Версия начальной загрузки 3.0.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-411">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="0b17f-412">Версия начальной загрузки 3.0.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-412">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="0b17f-413">Версия начальной загрузки 3.0.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-413">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="0b17f-414">Версия начальной загрузки 2.3.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-414">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="0b17f-415">Начальная версия 2.3.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-415">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="0b17f-416">Начальная загрузка выпусков Таучкараусел в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-416">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="0b17f-417">Следующие выпуски [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") таучкараусел выпусков начальной загрузки размещены в сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-417">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="0b17f-418">Таучкараусел начальной загрузки версии 0.8.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-418">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="0b17f-419">Hammer.js выпусков в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-419">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="0b17f-420">Следующие выпуски [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js выпусков размещаются в сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-420">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="0b17f-421">Версия Hammer.js 2.0.4</span><span class="sxs-lookup"><span data-stu-id="0b17f-421">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="0b17f-422">ASP.NET веб-формы и выпуски AJAX в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-422">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="0b17f-423">Следующие выпуски библиотеки ASP.NET AJAX размещаются в CDN.</span><span class="sxs-lookup"><span data-stu-id="0b17f-423">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="0b17f-424">Щелкните каждую ссылку, чтобы просмотреть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="0b17f-424">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="0b17f-425">Веб-формы ASP.NET и AJAX версии 4.5.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-425">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "Веб-формы ASP.NET и Ajax 4.5.2")
- [<span data-ttu-id="0b17f-426">Веб-формы ASP.NET и AJAX версии 4</span><span class="sxs-lookup"><span data-stu-id="0b17f-426">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "Веб-формы ASP.NET и Ajax 4")
- [<span data-ttu-id="0b17f-427">ASP.NET AJAX версии 3,5</span><span class="sxs-lookup"><span data-stu-id="0b17f-427">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="0b17f-428">Выпуски MVC ASP.NET в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-428">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="0b17f-429">Следующие файлы JavaScript ASP.NET MVC размещаются в этой сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-429">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="0b17f-430">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="0b17f-430">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="0b17f-431">ASP.NET MVC 5,1</span><span class="sxs-lookup"><span data-stu-id="0b17f-431">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="0b17f-432">ASP.NET MVC 5,0</span><span class="sxs-lookup"><span data-stu-id="0b17f-432">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="0b17f-433">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-433">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="0b17f-434">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="0b17f-434">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="0b17f-435">ASP.NET MVC 2,0</span><span class="sxs-lookup"><span data-stu-id="0b17f-435">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="0b17f-436">ASP.NET MVC 1,0</span><span class="sxs-lookup"><span data-stu-id="0b17f-436">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="0b17f-437">Выпуски SignalR ASP.NET в CDN</span><span class="sxs-lookup"><span data-stu-id="0b17f-437">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="0b17f-438">Следующие файлы JavaScript ASP.NET SignalR размещаются в этой сети CDN:</span><span class="sxs-lookup"><span data-stu-id="0b17f-438">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="0b17f-439">2.2.2 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-439">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="0b17f-440">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-440">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="0b17f-441">2.2.0 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-441">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="0b17f-442">2.1.0 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-442">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="0b17f-443">2.0.3 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-443">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="0b17f-444">2.0.2 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-444">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="0b17f-445">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-445">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="0b17f-446">2.0.0 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-446">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="0b17f-447">1.1.3 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-447">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="0b17f-448">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="0b17f-448">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="0b17f-449">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0b17f-449">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="0b17f-450">1.1.0 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-450">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="0b17f-451">1.0.1 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0b17f-451">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="0b17f-452">Сведения об условиях использования сети CDN см. в [статье условия использования для Microsoft Ajax CDN](https://www.asp.net/terms-of-use "Условия использования Microsoft Ajax CDN").</span><span class="sxs-lookup"><span data-stu-id="0b17f-452">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
