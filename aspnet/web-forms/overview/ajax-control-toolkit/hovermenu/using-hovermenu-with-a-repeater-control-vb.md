---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: Использование HoverMenu с элементом управления Repeater (VB) | Документация Майкрософт
author: wenz
description: 'Элемент управления HoverMenu в AJAX Control Toolkit предоставляет простое всплывающее окно эффект: При наведении указателя мыши на элемент, в specifi появится всплывающее окно...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: fa9b11ea064bd8181381f8374cc96b8eea6aa72b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127092"
---
# <a name="using-hovermenu-with-a-repeater-control-vb"></a><span data-ttu-id="45ef3-103">Использование HoverMenu с элементом управления Repeater (VB)</span><span class="sxs-lookup"><span data-stu-id="45ef3-103">Using HoverMenu with a Repeater Control (VB)</span></span>

<span data-ttu-id="45ef3-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="45ef3-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="45ef3-105">[Скачать код](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="45ef3-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span></span>

> <span data-ttu-id="45ef3-106">Элемент управления HoverMenu в AJAX Control Toolkit предоставляет простое всплывающее окно эффект: При наведении указателя мыши на элемент, появится всплывающее окно, в указанной позиции.</span><span class="sxs-lookup"><span data-stu-id="45ef3-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="45ef3-107">Можно также использовать этот элемент управления в элементе управления repeater.</span><span class="sxs-lookup"><span data-stu-id="45ef3-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="45ef3-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="45ef3-108">Overview</span></span>

<span data-ttu-id="45ef3-109">`HoverMenu` Элемента управления в AJAX Control Toolkit предоставляет простое всплывающее окно эффект: При наведении указателя мыши на элемент, появится всплывающее окно, в указанной позиции.</span><span class="sxs-lookup"><span data-stu-id="45ef3-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="45ef3-110">Можно также использовать этот элемент управления в элементе управления repeater.</span><span class="sxs-lookup"><span data-stu-id="45ef3-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="45ef3-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="45ef3-111">Steps</span></span>

<span data-ttu-id="45ef3-112">Во-первых источником данных является обязательным.</span><span class="sxs-lookup"><span data-stu-id="45ef3-112">First of all, a data source is required.</span></span> <span data-ttu-id="45ef3-113">В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="45ef3-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="45ef3-114">Базы данных является необязательной частью установки Visual Studio (включая экспресс-выпуск), а также доступна для загрузки в разделе [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="45ef3-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="45ef3-115">Базы данных AdventureWorks является частью образцы SQL Server 2005 и образцов баз данных (загрузить в [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="45ef3-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="45ef3-116">Самый простой способ настроить базы данных является использование Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединения `AdventureWorks.mdf` файл базы данных.</span><span class="sxs-lookup"><span data-stu-id="45ef3-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="45ef3-117">В этом примере мы предполагаем, что экземпляр SQL Server 2005 Express Edition называется `SQLEXPRESS` и находится на одном компьютере с веб-сервера; это также настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="45ef3-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="45ef3-118">Если настройки отличаются, вам нужно адаптировать сведения о соединении для базы данных.</span><span class="sxs-lookup"><span data-stu-id="45ef3-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="45ef3-119">Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в `<form>` элемента):</span><span class="sxs-lookup"><span data-stu-id="45ef3-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="45ef3-120">Затем добавьте источник данных на страницу.</span><span class="sxs-lookup"><span data-stu-id="45ef3-120">Then, add a data source to the page.</span></span> <span data-ttu-id="45ef3-121">Чтобы использовать ограниченный объем данных, мы выбрать только первые пять записей в таблице поставщиков базы данных AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="45ef3-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="45ef3-122">Если вы используете этот помощник используется Visual Studio для создания источника данных, виду, что ошибки в текущей версии не префикса имени таблицы (`Vendor`) с `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="45ef3-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="45ef3-123">В следующей разметке показан правильный синтаксис:</span><span class="sxs-lookup"><span data-stu-id="45ef3-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="45ef3-124">Добавьте панель, который служит в качестве модального всплывающего окна:</span><span class="sxs-lookup"><span data-stu-id="45ef3-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="45ef3-125">Теперь `HoverMenuExtender` вступает в действие.</span><span class="sxs-lookup"><span data-stu-id="45ef3-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="45ef3-126">Таким образом, чтобы каждый элемент в источнике данных получает свой собственный контекстного меню, расширения должны быть размещены в элементе repeater `<ItemTemplate>` раздел.</span><span class="sxs-lookup"><span data-stu-id="45ef3-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="45ef3-127">Ниже приводится пример разметки:</span><span class="sxs-lookup"><span data-stu-id="45ef3-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="45ef3-128">Теперь каждый элемент в источнике данных отображает контекстное меню справа (`PopupPosition` атрибут) с задержкой в 50 мс (`PopDelay` атрибут).</span><span class="sxs-lookup"><span data-stu-id="45ef3-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="45ef3-129">[![Меню при наведении указателя мыши отображается рядом с каждым элементом в элементу управления repeater](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="45ef3-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="45ef3-130">Меню при наведении указателя мыши отображается рядом с каждым элементом в элементу управления repeater ([Просмотр полноразмерного изображения](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="45ef3-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="45ef3-131">Назад</span><span class="sxs-lookup"><span data-stu-id="45ef3-131">Previous</span></span>](using-hovermenu-with-a-repeater-control-cs.md)
