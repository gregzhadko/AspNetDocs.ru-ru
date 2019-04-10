---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Использование HoverMenu с элементом управления Repeater (C#) | Документация Майкрософт
author: wenz
description: 'Элемент управления HoverMenu в AJAX Control Toolkit предоставляет простое всплывающее окно эффект: При наведении указателя мыши на элемент, в specifi появится всплывающее окно...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f64e90eb2f8f87e2f382cb7897793e7071d305d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384504"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="7d06b-103">Использование HoverMenu с элементом управления Repeater (C#)</span><span class="sxs-lookup"><span data-stu-id="7d06b-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="7d06b-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7d06b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7d06b-105">[Скачать код](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7d06b-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="7d06b-106">Элемент управления HoverMenu в AJAX Control Toolkit предоставляет простое всплывающее окно эффект: При наведении указателя мыши на элемент, появится всплывающее окно, в указанной позиции.</span><span class="sxs-lookup"><span data-stu-id="7d06b-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="7d06b-107">Можно также использовать этот элемент управления в элементе управления repeater.</span><span class="sxs-lookup"><span data-stu-id="7d06b-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="7d06b-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="7d06b-108">Overview</span></span>

<span data-ttu-id="7d06b-109">`HoverMenu` Элемента управления в AJAX Control Toolkit предоставляет простое всплывающее окно эффект: При наведении указателя мыши на элемент, появится всплывающее окно, в указанной позиции.</span><span class="sxs-lookup"><span data-stu-id="7d06b-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="7d06b-110">Можно также использовать этот элемент управления в элементе управления repeater.</span><span class="sxs-lookup"><span data-stu-id="7d06b-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="7d06b-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="7d06b-111">Steps</span></span>

<span data-ttu-id="7d06b-112">Во-первых источником данных является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7d06b-112">First of all, a data source is required.</span></span> <span data-ttu-id="7d06b-113">В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="7d06b-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="7d06b-114">Базы данных является необязательной частью установки Visual Studio (включая экспресс-выпуск), а также доступна для загрузки в разделе [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="7d06b-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="7d06b-115">Базы данных AdventureWorks является частью образцы SQL Server 2005 и образцов баз данных (загрузить в [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="7d06b-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="7d06b-116">Самый простой способ настроить базы данных является использование Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединения `AdventureWorks.mdf` файл базы данных.</span><span class="sxs-lookup"><span data-stu-id="7d06b-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="7d06b-117">В этом примере мы предполагаем, что экземпляр SQL Server 2005 Express Edition называется `SQLEXPRESS` и находится на одном компьютере с веб-сервера; это также настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7d06b-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="7d06b-118">Если настройки отличаются, вам нужно адаптировать сведения о соединении для базы данных.</span><span class="sxs-lookup"><span data-stu-id="7d06b-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="7d06b-119">Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в `<form>` элемента):</span><span class="sxs-lookup"><span data-stu-id="7d06b-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="7d06b-120">Затем добавьте источник данных на страницу.</span><span class="sxs-lookup"><span data-stu-id="7d06b-120">Then, add a data source to the page.</span></span> <span data-ttu-id="7d06b-121">Чтобы использовать ограниченный объем данных, мы выбрать только первые пять записей в таблице поставщиков базы данных AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="7d06b-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="7d06b-122">Если вы используете этот помощник используется Visual Studio для создания источника данных, виду, что ошибки в текущей версии не префикса имени таблицы (`Vendor`) с `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="7d06b-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="7d06b-123">В следующей разметке показан правильный синтаксис:</span><span class="sxs-lookup"><span data-stu-id="7d06b-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="7d06b-124">Добавьте панель, который служит в качестве модального всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="7d06b-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="7d06b-125">Теперь `HoverMenuExtender` вступает в действие.</span><span class="sxs-lookup"><span data-stu-id="7d06b-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="7d06b-126">Таким образом, чтобы каждый элемент в источнике данных получает свой собственный контекстного меню, расширения должны быть размещены в элементе repeater `<ItemTemplate>` раздел.</span><span class="sxs-lookup"><span data-stu-id="7d06b-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="7d06b-127">Ниже приводится пример разметки:</span><span class="sxs-lookup"><span data-stu-id="7d06b-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="7d06b-128">Теперь каждый элемент в источнике данных отображает контекстное меню справа (`PopupPosition` атрибут) с задержкой в 50 мс (`PopDelay` атрибут).</span><span class="sxs-lookup"><span data-stu-id="7d06b-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


[![T<span data-ttu-id="7d06b-129">он меню при наведении указателя мыши отображается рядом с каждым элементом в элементу управления repeater]</span><span class="sxs-lookup"><span data-stu-id="7d06b-129">he hover menu appears next to each item in the repeater]</span></span>(using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

<span data-ttu-id="7d06b-130">Меню при наведении указателя мыши отображается рядом с каждым элементом в элементу управления repeater ([Просмотр полноразмерного изображения](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7d06b-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7d06b-131">Далее</span><span class="sxs-lookup"><span data-stu-id="7d06b-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
