---
uid: ajax/cdn/overview
title: Сеть доставки контента Microsoft Ajax (ru) Документы Майкрософт
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540211"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="32185-102">Сеть доставки содержимого Microsoft Ajax</span><span class="sxs-lookup"><span data-stu-id="32185-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="32185-103">Производственные приложения не должны сильно зависеть от активов CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="32185-104">Приложения должны тестировать на упомянутый актив CDN и использовать запасной актив, когда CDN недоступен.</span><span class="sxs-lookup"><span data-stu-id="32185-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="32185-105">Microsoft Ajax CDN не имеет SLA сверх использования Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="32185-106">Используйте [эту проблему GitHub,](https://github.com/dotnet/AspNetDocs/issues/116) чтобы сообщить о проблемах с Microsoft Ajax CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="32185-107">Оглавление</span><span class="sxs-lookup"><span data-stu-id="32185-107">Table of Contents</span></span>

<span data-ttu-id="32185-108">**[ajax.microsoft.com переименован в ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="32185-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="32185-109">**[Визуальная студия .vsdoc Поддержка](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="32185-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="32185-110">**[Использование ASP.NET Ajax от CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="32185-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="32185-111">**[Использование j'query от CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="32185-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="32185-112">**[Используя uI j'ury от CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="32185-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="32185-113">**[Файлы третьих сторон на CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="32185-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="32185-114">J'ери релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="32185-115">j'емикрировать релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="32185-116">J'ury UI Релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="32185-117">J'cиер Валидация Релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="32185-118">j's'ry Мобильные релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="32185-119">J'ери шаблоны релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="32185-120">J'ери Цикл релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="32185-121">J'ери DataTables релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="32185-122">Модернизр релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="32185-123">JSHint релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="32185-124">Релизы нокаутов на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="32185-125">Глобализация релизов на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="32185-126">Ответные релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="32185-127">Bootstrap релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="32185-128">Bootstrap TouchCarousel релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="32185-129">Hammer.js релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="32185-130">ASP.NET веб-формы и Ajax релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="32185-131">ASP.NET релизы MVC на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="32185-132">ASP.NET SignalR релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="32185-133">В сети доставки контента Microsoft Ajax (CDN) размещены популярные сторонние библиотеки JavaScript, такие как j'ery, и вы можете легко добавлять их в свои веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="32185-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="32185-134">Например, вы можете начать использовать j'sry, который размещается на этом CDN, просто добавив тег &lt;скрипта&gt; на страницу, который указывает на ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="32185-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="32185-135">Воспользовавшись CDN, вы можете значительно повысить производительность ваших приложений Ajax.</span><span class="sxs-lookup"><span data-stu-id="32185-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="32185-136">Содержимое CDN кэшируются на серверах, расположенных по всему миру.</span><span class="sxs-lookup"><span data-stu-id="32185-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="32185-137">Кроме того, CDN позволяет браузерам повторно использовать кэшированные файлы JavaScript для веб-сайтов, расположенных в разных доменах.</span><span class="sxs-lookup"><span data-stu-id="32185-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="32185-138">CDN поддерживает SSL (HTTPS) в случае необходимости обслуживания веб-страницы с помощью слоя безопасных розеток.</span><span class="sxs-lookup"><span data-stu-id="32185-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="32185-139">CDN размещает следующие библиотеки сценариев третьих сторон, которые были загружены, и лицензированы для вас, владельцами этих библиотек:</span><span class="sxs-lookup"><span data-stu-id="32185-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="32185-140">J'Ery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="32185-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="32185-141">J'ury UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="32185-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="32185-142">J'ery Мобильный (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="32185-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="32185-143">Проверка j'ee (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="32185-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="32185-144">цикл j'e (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="32185-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="32185-145">J'eery DataTables (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="32185-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="32185-146">Microsoft Ajax CDN также включает в себя следующие библиотеки, которые были загружены Microsoft:</span><span class="sxs-lookup"><span data-stu-id="32185-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="32185-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="32185-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="32185-148">ASP.NET файлов MVC JavaScript</span><span class="sxs-lookup"><span data-stu-id="32185-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="32185-149">ASP.NET файлы SignalR JavaScript</span><span class="sxs-lookup"><span data-stu-id="32185-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="32185-150">Корпорация Майкрософт не претендует на право собственности на какие-либо сторонние библиотеки, размещенные на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="32185-151">Владельцы библиотек, обладающих авторскими правами, лицензируют эти библиотеки.</span><span class="sxs-lookup"><span data-stu-id="32185-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="32185-152">Любые права, которые вы, возможно, придется загружать и использовать такие библиотеки предоставляются исключительно соответствующими владельцами авторских прав.</span><span class="sxs-lookup"><span data-stu-id="32185-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="32185-153">Поскольку это не библиотеки Microsoft, корпорация Майкрософт не предоставляет никаких гарантий или лицензий на права интеллектуальной собственности (включая отсутствие подразумеваемых патентных прав) для библиотек третьих сторон, размещенных на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="32185-154">Если вы хотите отправить свою библиотеку JavaScript и ваша библиотека является http://trends.builtwith.com) одним из лучших библиотек JavaScript (как указано на или расширения / плагины AjaxCDNSubmission@Microsoft.comв этих библиотеках, которые (а) популярны; или (б) полезно для использования на ASP.NET, пожалуйста, свяжитесь с .</span><span class="sxs-lookup"><span data-stu-id="32185-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="32185-155">ajax.microsoft.com переименован в ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="32185-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="32185-156">CDN используется для использования доменного имени microsoft.com и был изменен на использование aspnetcdn.com доменное имя.</span><span class="sxs-lookup"><span data-stu-id="32185-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="32185-157">Это изменение было сделано для повышения производительности, потому что, когда браузер ссылается на microsoft.com домена он будет отправлять любые файлы cookie из этого домена через провод с каждым запросом.</span><span class="sxs-lookup"><span data-stu-id="32185-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="32185-158">При переименовании доменного имени, кроме microsoft.com производительность может быть увеличена на целых 25%.</span><span class="sxs-lookup"><span data-stu-id="32185-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="32185-159">Обратите внимание, ajax.microsoft.com будет продолжать функционировать, но ajax.aspnetcdn.com рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="32185-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="32185-160">Старый формат:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="32185-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="32185-161">Новый формат:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="32185-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="32185-162">Визуальная студия .vsdoc Поддержка</span><span class="sxs-lookup"><span data-stu-id="32185-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="32185-163">Чтобы использовать файлы .vsdoc должным образом с Visual Studio 2008 вы должны убедиться, что у вас есть VS 2008 SP1 установлен и hotfix для vsdoc файлы установлены.</span><span class="sxs-lookup"><span data-stu-id="32185-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="32185-164">Вы можете получить эти отсюда:</span><span class="sxs-lookup"><span data-stu-id="32185-164">You can get these from here:</span></span>

- [<span data-ttu-id="32185-165">Скачать Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="32185-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Скачать Visual Studio 2008 SP1")
- [<span data-ttu-id="32185-166">Скачать .vsdoc hotfix для Визуальной студии 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="32185-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Скачать .vsdoc hotfix для Визуальной студии 2008 SP1")

<span data-ttu-id="32185-167">Visual Studio 2010 поддерживает файлы .vsdoc без каких-либо дополнительных исправлений.</span><span class="sxs-lookup"><span data-stu-id="32185-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="32185-168">Использование ASP.NET Ajax от CDN</span><span class="sxs-lookup"><span data-stu-id="32185-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="32185-169">При использовании ASP.NET 4 можно перенаправить все запросы на ASP.NET фреймворков на CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="32185-170">Получение скриптов с CDN вместо локального веб-сервера может существенно повысить производительность общедоступных ASP.NET веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="32185-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="32185-171">Используйте свойство ScriptManager EnableCDN для перенаправления всех запросов ASP.NET рамочных скриптов на Microsoft Ajax CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="32185-172">Использование j'query от CDN</span><span class="sxs-lookup"><span data-stu-id="32185-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="32185-173">Вы можете использовать скрипты j'ru, размещенные на CDN, в веб-приложении, добавив следующий элемент скрипта на страницу:</span><span class="sxs-lookup"><span data-stu-id="32185-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="32185-174">CDN также включает в себя minified версию сценария j'ru, который вы можете получить с помощью следующего элемента:</span><span class="sxs-lookup"><span data-stu-id="32185-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="32185-175">Чтобы позволить вашей странице откатиться к загрузке j'srery с локального пути на вашем собственном веб-сайте, если CDN оказывается недоступен, добавьте следующий элемент сразу после элемента, ссылающегося на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="32185-176">Следующая страница образца использует cdN-версию библиотеки j'ery (с запасом к локальной копии) для отображения содержимого элемента div при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="32185-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="32185-177">Вы можете узнать больше о j'ery и скачать местную копию j'ery, посетив веб-узел [j'ery.](http://jquery.com/)</span><span class="sxs-lookup"><span data-stu-id="32185-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="32185-178">Используя uI j'ury от CDN</span><span class="sxs-lookup"><span data-stu-id="32185-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="32185-179">В CDN также находится библиотека uI j'ury.</span><span class="sxs-lookup"><span data-stu-id="32185-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="32185-180">Библиотека ui j'ury включает в себя богатый набор виджетов и эффектов, которые можно использовать в ASP.NET приложениях.</span><span class="sxs-lookup"><span data-stu-id="32185-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="32185-181">Например, следующая страница иллюстрирует, как можно использовать данный вопрос о j'ury Datepicker в контексте приложения ASP.NET Web Forms для отображения всплывающем календаря:</span><span class="sxs-lookup"><span data-stu-id="32185-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="32185-182">При перемещении фокуса на TextBox с помощью клавиатуры отображается календарь:</span><span class="sxs-lookup"><span data-stu-id="32185-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Всплывающий календарь, созданный с помощью Datepicker](overview/_static/image1.png)

<span data-ttu-id="32185-184">Обратите внимание, что вы должны включить три файла из CDN в приведенном выше коде:</span><span class="sxs-lookup"><span data-stu-id="32185-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="32185-185">Библиотека j'ury &mdash; Библиотека J'ury uI зависит от библиотеки j'ury.</span><span class="sxs-lookup"><span data-stu-id="32185-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="32185-186">Перед добавлением библиотеки j'ury необходимо добавить библиотеку j'ury на свою страницу.</span><span class="sxs-lookup"><span data-stu-id="32185-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="32185-187">Библиотека &mdash; j'ueri UI Библиотека J'ury содержит все эффекты и виджеты j'ury, такие как виджет Datepicker, используемый на странице выше.</span><span class="sxs-lookup"><span data-stu-id="32185-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="32185-188">Тема &mdash; j'u'ry UI J'ury поддерживает различные темы.</span><span class="sxs-lookup"><span data-stu-id="32185-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="32185-189">На странице выше содержится ссылка на файл CSS для импорта темы Редмонда.</span><span class="sxs-lookup"><span data-stu-id="32185-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="32185-190">Все стандартные темы j'u'ry UI размещаются на CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="32185-191">[Посетите эту страницу,](jquery-ui/cdnjqueryui1910.md "Пользовательский интерфейс jQuery 1.8.10 в сети доставки содержимого Microsoft Ajax") чтобы просмотреть эскизы для каждой темы.</span><span class="sxs-lookup"><span data-stu-id="32185-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="32185-192">Чтобы узнать больше о библиотеке j'ury UI, посетите официальный [веб-сайт j'ury UI](http://jQueryUI.com "J'ury UI веб-сайт").</span><span class="sxs-lookup"><span data-stu-id="32185-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="32185-193">Файлы третьих сторон на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="32185-194">CDN размещает одни из самых популярных сторонних библиотек JavaScript.</span><span class="sxs-lookup"><span data-stu-id="32185-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="32185-195">Корпорация Майкрософт не претендует на право собственности на какие-либо сторонние библиотеки, размещенные на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="32185-196">Владельцы библиотек, обладающих авторскими правами, лицензируют эти библиотеки.</span><span class="sxs-lookup"><span data-stu-id="32185-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="32185-197">Любые права, которые вы, возможно, придется загружать и использовать такие библиотеки предоставляются исключительно соответствующими владельцами авторских прав.</span><span class="sxs-lookup"><span data-stu-id="32185-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="32185-198">Поскольку это не библиотеки Microsoft, корпорация Майкрософт не предоставляет никаких гарантий или лицензий на права интеллектуальной собственности (включая отсутствие подразумеваемых патентных прав) для библиотек третьих сторон, размещенных на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="32185-199">J'ери релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="32185-200">Следующие релизы j'query размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="32185-201">j'ери версия 3.5.0</span><span class="sxs-lookup"><span data-stu-id="32185-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="32185-202">J'ери версия 3.4.1</span><span class="sxs-lookup"><span data-stu-id="32185-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="32185-203">J'ери версия 3.4.0</span><span class="sxs-lookup"><span data-stu-id="32185-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="32185-204">J'ери версия 3.3.1</span><span class="sxs-lookup"><span data-stu-id="32185-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="32185-205">J'ери версия 3.2.1</span><span class="sxs-lookup"><span data-stu-id="32185-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="32185-206">J'ери версия 3.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="32185-207">j'ери версия 3.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="32185-208">j'ери версия 3.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="32185-209">J'ери версия 3.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="32185-210">j'ери версия 2.2.4</span><span class="sxs-lookup"><span data-stu-id="32185-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="32185-211">J'ери версия 2.2.3</span><span class="sxs-lookup"><span data-stu-id="32185-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="32185-212">j'ери версия 2.2.2</span><span class="sxs-lookup"><span data-stu-id="32185-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="32185-213">j'ери версия 2.2.1</span><span class="sxs-lookup"><span data-stu-id="32185-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="32185-214">j'ери версия 2.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="32185-215">j'ери версия 2.1.4</span><span class="sxs-lookup"><span data-stu-id="32185-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="32185-216">j'ери версия 2.1.3</span><span class="sxs-lookup"><span data-stu-id="32185-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="32185-217">j'ери версия 2.1.2</span><span class="sxs-lookup"><span data-stu-id="32185-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="32185-218">j'ери версия 2.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="32185-219">j'ери версия 2.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="32185-220">j'еry версия 2.0.3</span><span class="sxs-lookup"><span data-stu-id="32185-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="32185-221">j'еry версия 2.0.2</span><span class="sxs-lookup"><span data-stu-id="32185-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="32185-222">j'еry версия 2.0.1</span><span class="sxs-lookup"><span data-stu-id="32185-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="32185-223">j'ери версия 2.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="32185-224">j-ури версия 1.12.4</span><span class="sxs-lookup"><span data-stu-id="32185-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="32185-225">j-ури версия 1.12.3</span><span class="sxs-lookup"><span data-stu-id="32185-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="32185-226">j-ури версия 1.12.2</span><span class="sxs-lookup"><span data-stu-id="32185-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="32185-227">j-ури версия 1.12.1</span><span class="sxs-lookup"><span data-stu-id="32185-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="32185-228">j-ури версия 1.12.0</span><span class="sxs-lookup"><span data-stu-id="32185-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="32185-229">j-ури версия 1.11.3</span><span class="sxs-lookup"><span data-stu-id="32185-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="32185-230">j-ури версия 1.11.2</span><span class="sxs-lookup"><span data-stu-id="32185-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="32185-231">j-ури версия 1.11.1</span><span class="sxs-lookup"><span data-stu-id="32185-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="32185-232">j-ури версия 1.11.0</span><span class="sxs-lookup"><span data-stu-id="32185-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="32185-233">j-ури версия 1.10.2</span><span class="sxs-lookup"><span data-stu-id="32185-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="32185-234">j-ури версия 1.10.1</span><span class="sxs-lookup"><span data-stu-id="32185-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="32185-235">j-ури версия 1.10.0</span><span class="sxs-lookup"><span data-stu-id="32185-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="32185-236">j'ери версия 1.9.1</span><span class="sxs-lookup"><span data-stu-id="32185-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="32185-237">j'ери версия 1.9.0</span><span class="sxs-lookup"><span data-stu-id="32185-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="32185-238">J'ери версия 1.8.3</span><span class="sxs-lookup"><span data-stu-id="32185-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="32185-239">J'ери версия 1.8.2</span><span class="sxs-lookup"><span data-stu-id="32185-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="32185-240">j'ери версия 1.8.1</span><span class="sxs-lookup"><span data-stu-id="32185-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="32185-241">j-ури версия 1.8.0</span><span class="sxs-lookup"><span data-stu-id="32185-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="32185-242">j'ери версия 1.7.2</span><span class="sxs-lookup"><span data-stu-id="32185-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="32185-243">j'ери версия 1.7.1</span><span class="sxs-lookup"><span data-stu-id="32185-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="32185-244">j'ери версия 1.7</span><span class="sxs-lookup"><span data-stu-id="32185-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="32185-245">j'ери версия 1.6.4</span><span class="sxs-lookup"><span data-stu-id="32185-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="32185-246">j'ери версия 1.6.3</span><span class="sxs-lookup"><span data-stu-id="32185-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="32185-247">j'ери версия 1.6.2</span><span class="sxs-lookup"><span data-stu-id="32185-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="32185-248">j'ери версия 1.6.1</span><span class="sxs-lookup"><span data-stu-id="32185-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="32185-249">j'ери версия 1.6</span><span class="sxs-lookup"><span data-stu-id="32185-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="32185-250">j'ери версия 1.5.2</span><span class="sxs-lookup"><span data-stu-id="32185-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="32185-251">j'ери версия 1.5.1</span><span class="sxs-lookup"><span data-stu-id="32185-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="32185-252">j'ери версия 1.5</span><span class="sxs-lookup"><span data-stu-id="32185-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="32185-253">j'ери версия 1.4.4</span><span class="sxs-lookup"><span data-stu-id="32185-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="32185-254">j-ури версия 1.4.3</span><span class="sxs-lookup"><span data-stu-id="32185-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="32185-255">j-ури версия 1.4.2</span><span class="sxs-lookup"><span data-stu-id="32185-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="32185-256">j-ури версия 1.4.1</span><span class="sxs-lookup"><span data-stu-id="32185-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="32185-257">j'ери версия 1.4</span><span class="sxs-lookup"><span data-stu-id="32185-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="32185-258">j'ери версия 1.3.2</span><span class="sxs-lookup"><span data-stu-id="32185-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="32185-259">j'емикрировать релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="32185-260">Следующие релизы j's'query Migrate размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="32185-261">J'егриверсия версия 3.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="32185-262">J'егриверсия версия 1.2.1</span><span class="sxs-lookup"><span data-stu-id="32185-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="32185-263">J'егриверсия версия 1.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="32185-264">J'егриверсия версия 1.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="32185-265">J'егриверсия версия 1.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="32185-266">J'егриверсия версия 1.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="32185-267">J'ury UI Релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="32185-268">Следующие релизы библиотеки j'ury UI размещаются на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="32185-269">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-270">j'ury UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="32185-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Пользовательский интерфейс jQuery 1.12.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-271">j'ury UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="32185-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Пользовательский интерфейс jQuery 1.12.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-272">j'ury UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="32185-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Пользовательский интерфейс jQuery 1.11.4 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-273">j'ury UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="32185-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Пользовательский интерфейс jQuery 1.11.3 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-274">j'ury UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="32185-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Пользовательский интерфейс jQuery 1.11.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-275">j'ury UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="32185-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Пользовательский интерфейс jQuery 1.11.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-276">j'ury UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="32185-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Пользовательский интерфейс jQuery 1.11.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-277">j'ury UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="32185-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Пользовательский интерфейс jQuery 1.10.4 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-278">j'ury UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="32185-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Пользовательский интерфейс jQuery 1.10.3 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-279">j'ury UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="32185-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Пользовательский интерфейс jQuery 1.10.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-280">j'ury UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="32185-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Пользовательский интерфейс jQuery 1.10.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-281">j'ury UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="32185-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Пользовательский интерфейс jQuery 1.10.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-282">j'ury UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="32185-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Пользовательский интерфейс jQuery 1.9.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-283">j'ury UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="32185-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Пользовательский интерфейс jQuery 1.9.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-284">j'ury UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="32185-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Пользовательский интерфейс jQuery 1.9.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-285">J'ury UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="32185-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Пользовательский интерфейс jQuery 1.8.24 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-286">j'ury UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="32185-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Пользовательский интерфейс jQuery 1.8.23 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-287">J'ury UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="32185-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Пользовательский интерфейс jQuery 1.8.22 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-288">j'ury UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="32185-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Пользовательский интерфейс jQuery 1.8.21 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-289">J'ury UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="32185-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Пользовательский интерфейс jQuery 1.8.20 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-290">j'ury UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="32185-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Пользовательский интерфейс jQuery 1.8.19 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-291">j'ury UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="32185-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Пользовательский интерфейс jQuery 1.8.18 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-292">j'ury UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="32185-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Пользовательский интерфейс jQuery 1.8.17 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-293">j'ury UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="32185-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Пользовательский интерфейс jQuery 1.8.16 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-294">J'ury UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="32185-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Пользовательский интерфейс jQuery 1.8.15 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-295">J'ury UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="32185-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Пользовательский интерфейс jQuery 1.8.14 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-296">j'ury UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="32185-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Пользовательский интерфейс jQuery 1.8.13 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-297">J'ury UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="32185-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Пользовательский интерфейс jQuery 1.8.12 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-298">jQuery UI 1.8.11.</span><span class="sxs-lookup"><span data-stu-id="32185-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Пользовательский интерфейс jQuery 1.8.11 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-299">J'ury UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="32185-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Пользовательский интерфейс jQuery 1.8.10 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-300">j'ury UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="32185-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Пользовательский интерфейс jQuery 1.8.9 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-301">j'ury UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="32185-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Пользовательский интерфейс jQuery 1.8.8 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-302">j'ury UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="32185-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Пользовательский интерфейс jQuery 1.8.7 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-303">j'ury UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="32185-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Пользовательский интерфейс jQuery 1.8.6 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-304">Пользовательский интерфейс jQuery 1.8.5</span><span class="sxs-lookup"><span data-stu-id="32185-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "Пользовательский интерфейс jQuery 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="32185-305">J'cиер Валидация Релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="32185-306">Следующие релизы плагина [j'query Validation](https://jqueryvalidation.org/ "j'ери Проверка Плагин") размещаются на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="32185-307">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-308">j'ери Проверка 1.19.1</span><span class="sxs-lookup"><span data-stu-id="32185-308">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "Проверка J'ера 1.19.1")
- [<span data-ttu-id="32185-309">J'ери Проверка 1.19.0</span><span class="sxs-lookup"><span data-stu-id="32185-309">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "Проверка J'ера 1.19.0")
- [<span data-ttu-id="32185-310">j'ери Проверка 1.17.0</span><span class="sxs-lookup"><span data-stu-id="32185-310">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "Проверка J'ера 1.17.0")
- [<span data-ttu-id="32185-311">J'ери Проверка 1.16.0</span><span class="sxs-lookup"><span data-stu-id="32185-311">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="32185-312">j'ери Проверка 1.15.1</span><span class="sxs-lookup"><span data-stu-id="32185-312">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="32185-313">J'ери Проверка 1.15.0</span><span class="sxs-lookup"><span data-stu-id="32185-313">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="32185-314">J'ери Проверка 1.14.0</span><span class="sxs-lookup"><span data-stu-id="32185-314">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="32185-315">j'ери Проверка 1.13.1</span><span class="sxs-lookup"><span data-stu-id="32185-315">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="32185-316">J'ери Проверка 1.13.0</span><span class="sxs-lookup"><span data-stu-id="32185-316">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validate 1.13.0")
- [<span data-ttu-id="32185-317">J'ери Проверка 1.12.0</span><span class="sxs-lookup"><span data-stu-id="32185-317">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validate 1.12.0")
- [<span data-ttu-id="32185-318">j'ери Проверка 1.11.1</span><span class="sxs-lookup"><span data-stu-id="32185-318">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validate 1.11.1")
- [<span data-ttu-id="32185-319">j'ери Проверка 1.11.0</span><span class="sxs-lookup"><span data-stu-id="32185-319">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validate 1.11.0")
- [<span data-ttu-id="32185-320">J'ери Проверка 1.10.0</span><span class="sxs-lookup"><span data-stu-id="32185-320">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validate 1.10.0")
- [<span data-ttu-id="32185-321">j'ери Проверка 1.9</span><span class="sxs-lookup"><span data-stu-id="32185-321">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate версии 1.9")
- [<span data-ttu-id="32185-322">j'ери Проверка 1.8.1</span><span class="sxs-lookup"><span data-stu-id="32185-322">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate версии 1.8.1")
- [<span data-ttu-id="32185-323">j'ери Проверка 1.8</span><span class="sxs-lookup"><span data-stu-id="32185-323">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate версии 1.8")
- [<span data-ttu-id="32185-324">j'ери Проверка 1.7</span><span class="sxs-lookup"><span data-stu-id="32185-324">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate версии 1.7")
- [<span data-ttu-id="32185-325">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="32185-325">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="32185-326">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="32185-326">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="32185-327">j's'ry Мобильные релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-327">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="32185-328">Следующие релизы библиотеки j'sry Mobile размещаются на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-328">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="32185-329">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-329">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-330">J'ури Мобильный 1.4.5</span><span class="sxs-lookup"><span data-stu-id="32185-330">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-331">J'ури Мобильный 1.4.2</span><span class="sxs-lookup"><span data-stu-id="32185-331">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-332">J''образМобильный 1.4.1</span><span class="sxs-lookup"><span data-stu-id="32185-332">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-333">J'ури Мобильный 1.4.0</span><span class="sxs-lookup"><span data-stu-id="32185-333">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-334">J''образМобильный 1.3.2</span><span class="sxs-lookup"><span data-stu-id="32185-334">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-335">J''образМобильный 1.3.1</span><span class="sxs-lookup"><span data-stu-id="32185-335">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-336">J'ури Мобильный 1.3.0</span><span class="sxs-lookup"><span data-stu-id="32185-336">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-337">J'ури Мобильный 1.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-337">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-338">J''ей Мобильный 1.1.2</span><span class="sxs-lookup"><span data-stu-id="32185-338">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-339">j''s Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-339">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-340">J'ури Мобильный 1.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-340">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-341">J'ури Мобильный 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="32185-341">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-342">J''образМобильный 1.0.1</span><span class="sxs-lookup"><span data-stu-id="32185-342">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-343">J'ури Мобильный 1.0</span><span class="sxs-lookup"><span data-stu-id="32185-343">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-344">J'ури Мобильный 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="32185-344">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-345">J'ури Мобильный 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="32185-345">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 в сети доставки содержимого Microsoft Ajax")
- [<span data-ttu-id="32185-346">j'sMobile 1.0 бета 3</span><span class="sxs-lookup"><span data-stu-id="32185-346">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 бета-версии 3 в сети доставки содержимого Microsoft Ajax")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="32185-347">J'ери шаблоны релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-347">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="32185-348">Следующие релизы плагина j's Templates размещаются на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-348">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="32185-349">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-350">jQuery Templates, бета-версия 1</span><span class="sxs-lookup"><span data-stu-id="32185-350">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates, бета-версия 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="32185-351">J'ери Цикл релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-351">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="32185-352">Следующие релизы плагина j'sry Cycle размещаются на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-352">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="32185-353">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-353">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-354">J'ери Цикл 2.99</span><span class="sxs-lookup"><span data-stu-id="32185-354">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="32185-355">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="32185-355">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="32185-356">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="32185-356">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="32185-357">J'ери DataTables релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-357">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="32185-358">Следующие релизы плагина j'sData DataTables размещаются на этом CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-358">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="32185-359">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-359">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-360">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="32185-360">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="32185-361">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="32185-361">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="32185-362">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="32185-362">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="32185-363">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="32185-363">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="32185-364">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="32185-364">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="32185-365">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="32185-365">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="32185-366">J'ери DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="32185-366">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="32185-367">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="32185-367">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="32185-368">Модернизр релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-368">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="32185-369">Следующие релизы [Modernizr](http://www.modernizr.com "Modernizr") размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-369">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="32185-370">JSHint релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-370">JSHint Releases on the CDN</span></span>

<span data-ttu-id="32185-371">Следующие релизы [JSHint](http://www.jshint.com "JSHint") размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-371">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="32185-372">Релизы нокаутов на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-372">Knockout Releases on the CDN</span></span>

<span data-ttu-id="32185-373">Следующие релизы [Knockout](http://www.knockoutjs.com "Нокаут") размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-373">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

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

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="32185-374">Глобализация релизов на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-374">Globalize Releases on the CDN</span></span>

<span data-ttu-id="32185-375">Следующие релизы [Globalize](https://github.com/jquery/globalize "Глобализации") размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-375">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="32185-376">Глобализация версии 1.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-376">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="32185-377">Глобализация версии 0.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-377">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="32185-378">всех культур</span><span class="sxs-lookup"><span data-stu-id="32185-378">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="32185-379">Замените «культурный код» на нужный код культуры, например, globalize.culture.en-GB.js» Microsoft Files на CDN »Эти библиотеки были загружены корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="32185-379">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="32185-380">Ответные релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-380">Respond Releases on the CDN</span></span>

<span data-ttu-id="32185-381">Следующие релизы [Respond](https://github.com/scottjehl/Respond "Устранение") размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-381">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="32185-382">Ответная версия 1.4.2</span><span class="sxs-lookup"><span data-stu-id="32185-382">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="32185-383">Ответная версия 1.4.1</span><span class="sxs-lookup"><span data-stu-id="32185-383">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="32185-384">Ответная версия 1.4.0</span><span class="sxs-lookup"><span data-stu-id="32185-384">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="32185-385">Ответная версия 1.3.0</span><span class="sxs-lookup"><span data-stu-id="32185-385">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="32185-386">Ответная версия 1.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-386">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="32185-387">Bootstrap релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-387">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="32185-388">Следующие релизы [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-388">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="32185-389">Версия Для Bootstrap 4.4.1</span><span class="sxs-lookup"><span data-stu-id="32185-389">Bootstrap version 4.4.1</span></span>

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

#### <a name="bootstrap-version-431"></a><span data-ttu-id="32185-390">Бутсрапт версия 4.3.1</span><span class="sxs-lookup"><span data-stu-id="32185-390">Bootstrap version 4.3.1</span></span>

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

#### <a name="bootstrap-version-421"></a><span data-ttu-id="32185-391">Версия для bootstrap 4.2.1</span><span class="sxs-lookup"><span data-stu-id="32185-391">Bootstrap version 4.2.1</span></span>

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

#### <a name="bootstrap-version-411"></a><span data-ttu-id="32185-392">Версия Для Bootstrap 4.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-392">Bootstrap version 4.1.1</span></span>

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

#### <a name="bootstrap-version-400"></a><span data-ttu-id="32185-393">Бутсрапт версия 4.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-393">Bootstrap version 4.0.0</span></span>

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

#### <a name="bootstrap-version-341"></a><span data-ttu-id="32185-394">Версия для bootstrap 3.4.1</span><span class="sxs-lookup"><span data-stu-id="32185-394">Bootstrap version 3.4.1</span></span>

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

#### <a name="bootstrap-version-340"></a><span data-ttu-id="32185-395">Бутсрапт версия 3.4.0</span><span class="sxs-lookup"><span data-stu-id="32185-395">Bootstrap version 3.4.0</span></span>

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

#### <a name="bootstrap-version-337"></a><span data-ttu-id="32185-396">Версия Для bootstrap 3.3.7</span><span class="sxs-lookup"><span data-stu-id="32185-396">Bootstrap version 3.3.7</span></span>

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

#### <a name="bootstrap-version-336"></a><span data-ttu-id="32185-397">Версия Для bootstrap 3.3.6</span><span class="sxs-lookup"><span data-stu-id="32185-397">Bootstrap version 3.3.6</span></span>

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

#### <a name="bootstrap-version-335"></a><span data-ttu-id="32185-398">Версия Для bootstrap 3.3.5</span><span class="sxs-lookup"><span data-stu-id="32185-398">Bootstrap version 3.3.5</span></span>

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

#### <a name="bootstrap-version-334"></a><span data-ttu-id="32185-399">Версия для bootstrap 3.3.4</span><span class="sxs-lookup"><span data-stu-id="32185-399">Bootstrap version 3.3.4</span></span>

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

#### <a name="bootstrap-version-332"></a><span data-ttu-id="32185-400">Версия для bootstrap 3.3.2</span><span class="sxs-lookup"><span data-stu-id="32185-400">Bootstrap version 3.3.2</span></span>

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

#### <a name="bootstrap-version-331"></a><span data-ttu-id="32185-401">Версия для bootstrap 3.3.1</span><span class="sxs-lookup"><span data-stu-id="32185-401">Bootstrap version 3.3.1</span></span>

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

#### <a name="bootstrap-version-330"></a><span data-ttu-id="32185-402">Бутсрапт версия 3.3.0</span><span class="sxs-lookup"><span data-stu-id="32185-402">Bootstrap version 3.3.0</span></span>

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

#### <a name="bootstrap-version-320"></a><span data-ttu-id="32185-403">Бутсрапт версия 3.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-403">Bootstrap version 3.2.0</span></span>

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

#### <a name="bootstrap-version-311"></a><span data-ttu-id="32185-404">Версия Для bootstrap 3.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-404">Bootstrap version 3.1.1</span></span>

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

#### <a name="bootstrap-version-310"></a><span data-ttu-id="32185-405">Бутсрапт версия 3.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-405">Bootstrap version 3.1.0</span></span>

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

#### <a name="bootstrap-version-303"></a><span data-ttu-id="32185-406">Бутсрапт версия 3.0.3</span><span class="sxs-lookup"><span data-stu-id="32185-406">Bootstrap version 3.0.3</span></span>

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

#### <a name="bootstrap-version-302"></a><span data-ttu-id="32185-407">Бутсрапт версия 3.0.2</span><span class="sxs-lookup"><span data-stu-id="32185-407">Bootstrap version 3.0.2</span></span>

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

#### <a name="bootstrap-version-301"></a><span data-ttu-id="32185-408">Бутсрапт версия 3.0.1</span><span class="sxs-lookup"><span data-stu-id="32185-408">Bootstrap version 3.0.1</span></span>

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

#### <a name="bootstrap-version-300"></a><span data-ttu-id="32185-409">Бутсрапт версия 3.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-409">Bootstrap version 3.0.0</span></span>

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

#### <a name="bootstrap-version-232"></a><span data-ttu-id="32185-410">Версия Для bootstrap 2.3.2</span><span class="sxs-lookup"><span data-stu-id="32185-410">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="32185-411">Бутсрапт версия 2.3.1</span><span class="sxs-lookup"><span data-stu-id="32185-411">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="32185-412">Bootstrap TouchCarousel релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-412">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="32185-413">Следующие релизы [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-413">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="32185-414">Bootstrap TouchCarousel версия 0.8.0</span><span class="sxs-lookup"><span data-stu-id="32185-414">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="32185-415">Hammer.js релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-415">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="32185-416">Следующие релизы [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js размещаются на CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-416">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="32185-417">Hammer.js версия 2.0.4</span><span class="sxs-lookup"><span data-stu-id="32185-417">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="32185-418">ASP.NET веб-формы и Ajax релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-418">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="32185-419">Следующие релизы библиотеки ASP.NET Ajax размещаются на CDN.</span><span class="sxs-lookup"><span data-stu-id="32185-419">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="32185-420">Нажмите на каждую ссылку, чтобы увидеть фактический список файлов.</span><span class="sxs-lookup"><span data-stu-id="32185-420">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="32185-421">ASP.NET веб-формы и Ajax версия 4.5.2</span><span class="sxs-lookup"><span data-stu-id="32185-421">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "Веб-формы ASP.NET и Ajax 4.5.2")
- [<span data-ttu-id="32185-422">ASP.NET веб-формы и Ajax версия 4</span><span class="sxs-lookup"><span data-stu-id="32185-422">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "Веб-формы ASP.NET и Ajax 4")
- [<span data-ttu-id="32185-423">ASP.NET версия Ajax 3.5</span><span class="sxs-lookup"><span data-stu-id="32185-423">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="32185-424">ASP.NET релизы MVC на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-424">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="32185-425">Следующие ASP.NET файлов MVC JavaScript размещаются на этом CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-425">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="32185-426">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="32185-426">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="32185-427">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="32185-427">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="32185-428">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="32185-428">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="32185-429">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="32185-429">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="32185-430">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="32185-430">ASP.NET MVC 3.0</span></span>

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

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="32185-431">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="32185-431">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="32185-432">ASP.NET MVC 1,0</span><span class="sxs-lookup"><span data-stu-id="32185-432">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="32185-433">ASP.NET SignalR релизы на CDN</span><span class="sxs-lookup"><span data-stu-id="32185-433">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="32185-434">Следующие ASP.NET файлов SignalR JavaScript размещаются на этом CDN:</span><span class="sxs-lookup"><span data-stu-id="32185-434">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="32185-435">ASP.NET сигнал 2.2.2.2</span><span class="sxs-lookup"><span data-stu-id="32185-435">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="32185-436">ASP.NET сигнал 2.2.1</span><span class="sxs-lookup"><span data-stu-id="32185-436">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="32185-437">ASP.NET СигналR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="32185-437">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="32185-438">ASP.NET СигналR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-438">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="32185-439">ASP.NET сигнал 2.0.3</span><span class="sxs-lookup"><span data-stu-id="32185-439">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="32185-440">ASP.NET сигнал 2.0.2</span><span class="sxs-lookup"><span data-stu-id="32185-440">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="32185-441">ASP.NET сигнал 2.0.1</span><span class="sxs-lookup"><span data-stu-id="32185-441">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="32185-442">ASP.NET СигналR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="32185-442">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="32185-443">ASP.NET сигнал 1.1.3</span><span class="sxs-lookup"><span data-stu-id="32185-443">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="32185-444">ASP.NET СигналЕр 1.1.2</span><span class="sxs-lookup"><span data-stu-id="32185-444">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="32185-445">ASP.NET сигнал 1.1.1</span><span class="sxs-lookup"><span data-stu-id="32185-445">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="32185-446">ASP.NET СигналЕр 1.1.0</span><span class="sxs-lookup"><span data-stu-id="32185-446">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="32185-447">ASP.NET сигнал 1.0.1</span><span class="sxs-lookup"><span data-stu-id="32185-447">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="32185-448">Для получения информации об условиях использования CDN [см.](https://www.asp.net/terms-of-use "Условия использования Microsoft Ajax CDN")</span><span class="sxs-lookup"><span data-stu-id="32185-448">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
