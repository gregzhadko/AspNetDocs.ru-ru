---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Начало работы с AJAX Control Toolkit (C#) | Документация Майкрософт
author: microsoft
description: Узнайте все что нужно знать, чтобы приступить к работе с AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bbbe0c8240a2a77edee8d39a76bf865c95f345e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381098"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="fdf1a-103">Начало работы с набором элементов управления AJAX (C#)</span><span class="sxs-lookup"><span data-stu-id="fdf1a-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="fdf1a-104">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fdf1a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fdf1a-105">Узнайте все что нужно знать, чтобы приступить к работе с AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="fdf1a-106">AJAX Control Toolkit содержит более 30 бесплатные элементы управления, которые можно использовать в приложениях ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="fdf1a-107">В этом руководстве вы узнаете, как скачать AJAX Control Toolkit и добавьте в набор средств элементы управления панели инструментов Visual Studio или Visual Web Developer Express.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="fdf1a-108">Загрузка AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="fdf1a-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="fdf1a-109">[AJAX Control Toolkit](http://devexpress.com/act) — это проект с открытым исходным кодом, разработанная компанией членами сообщества ASP.NET и группа разработчиков ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 


[![D<span data-ttu-id="fdf1a-110">ownloading AJAX Control Toolkit]</span><span class="sxs-lookup"><span data-stu-id="fdf1a-110">ownloading the AJAX Control Toolkit]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

<span data-ttu-id="fdf1a-111">**Рис 01**: Загрузка AJAX Control Toolkit ([Просмотр полноразмерного изображения](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="fdf1a-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>


<span data-ttu-id="fdf1a-112">После загрузки файла, необходимо разблокировать файл.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="fdf1a-113">Щелкните правой кнопкой мыши файл, выберите свойства и нажмите кнопку **Unblock** кнопку (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="fdf1a-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


[![U<span data-ttu-id="fdf1a-114">nblocking набор средств управления AJAX ZIP-файл]</span><span class="sxs-lookup"><span data-stu-id="fdf1a-114">nblocking the AJAX Control Toolkit ZIP file]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

<span data-ttu-id="fdf1a-115">**Рис. 02**: Разблокировка файла ZIP-набор средств управления AJAX ([Просмотр полноразмерного изображения](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="fdf1a-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>


<span data-ttu-id="fdf1a-116">После разблокирования файла можно было распаковать файл: Щелкните правой кнопкой мыши файл и выберите **извлечь все** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="fdf1a-117">Теперь мы готовы для добавления в набор средств для панели элементов Visual Studio или Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="fdf1a-118">Добавление на панель инструментов AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="fdf1a-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="fdf1a-119">— Это самый простой способ использования AJAX Control Toolkit, добавляемый в набор средств панели инструментов Visual Studio или Visual Web Developer (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="fdf1a-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="fdf1a-120">Таким образом, можно просто перетащить элемент управления набора средств на страницу, если вы хотите использовать его.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


[![A<span data-ttu-id="fdf1a-121">JAX Control Toolkit отображается в панели элементов]</span><span class="sxs-lookup"><span data-stu-id="fdf1a-121">JAX Control Toolkit appears in toolbox]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

<span data-ttu-id="fdf1a-122">**Рис 03**: В панели элементов появится AJAX Control Toolkit ([Просмотр полноразмерного изображения](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="fdf1a-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>


<span data-ttu-id="fdf1a-123">Во-первых необходимо добавить на панель инструментов с вкладкой AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="fdf1a-124">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-124">Follow these steps.</span></span>

1. <span data-ttu-id="fdf1a-125">Создайте новый веб-сайт ASP.NET, выбрав пункт меню файл, создать веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="fdf1a-126">Дважды щелкните файл Default.aspx в окне обозревателя решений, чтобы открыть файл в редакторе.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="fdf1a-127">Щелкните правой кнопкой мыши панель под вкладка "Общие" и выберите пункт меню **добавить вкладку** (см. рис. 4).</span><span class="sxs-lookup"><span data-stu-id="fdf1a-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="fdf1a-128">Введите новую вкладку, называемую AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-128">Enter a new tab named AJAX Control Toolkit.</span></span>


[![A<span data-ttu-id="fdf1a-129">dding новую вкладку]</span><span class="sxs-lookup"><span data-stu-id="fdf1a-129">dding a new tab]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

<span data-ttu-id="fdf1a-130">**Рис. 04**: Добавить новую вкладку ([Просмотр полноразмерного изображения](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="fdf1a-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>


<span data-ttu-id="fdf1a-131">Далее необходимо добавить элементы управления AJAX Control Toolkit на новой вкладке. Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="fdf1a-132">Щелкните правой кнопкой мыши под вкладке AJAX Control Toolkit и выбрать пункт меню **Выбор элементов (см. рис. 5)**.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="fdf1a-133">Перейдите в расположение, где вы распаковали AJAX Control Toolkit и выберите сборку файл AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


[![C<span data-ttu-id="fdf1a-134">Выберите элементы для добавления на панель элементов]</span><span class="sxs-lookup"><span data-stu-id="fdf1a-134">hoose items to add to the toolbox]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

<span data-ttu-id="fdf1a-135">**05 рис**: Выберите элементы для добавления на панель инструментов ([Просмотр полноразмерного изображения](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="fdf1a-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>


<span data-ttu-id="fdf1a-136">После выполнения этих действий все элементы набора средств управления будут отображаться в вашем инструментарии.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="fdf1a-137">Обновление до новой версии набора средств</span><span class="sxs-lookup"><span data-stu-id="fdf1a-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="fdf1a-138">Если вы использовали более ранняя версия набора средств и теперь нужно переместить в более поздней версии приведены рекомендуемые действия:</span><span class="sxs-lookup"><span data-stu-id="fdf1a-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="fdf1a-139">Двоичные файлы - удалить старую версию файл AjaxControlToolkit.dll сборки из папки Bin веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="fdf1a-140">Элементы панели элементов - удалить вкладку AJAX Control Toolkit и выполните действия, чтобы повторно создать на вкладке с новой версией сборки, файл AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="fdf1a-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fdf1a-141">Далее</span><span class="sxs-lookup"><span data-stu-id="fdf1a-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
