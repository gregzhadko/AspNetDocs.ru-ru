---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Отображение сведений об элементе | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 83f291326307a4964afdd5e8b50f2c375348ed0e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065361"
---
<a name="display-item-details"></a><span data-ttu-id="ca8a8-102">Отображение сведений об элементе</span><span class="sxs-lookup"><span data-stu-id="ca8a8-102">Display Item Details</span></span>
====================
<span data-ttu-id="ca8a8-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ca8a8-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ca8a8-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="ca8a8-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ca8a8-105">В этом разделе вы добавите возможность просматривать подробные сведения о каждой книги.</span><span class="sxs-lookup"><span data-stu-id="ca8a8-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="ca8a8-106">В файле app.js добавьте следующий код, чтобы модель представления:</span><span class="sxs-lookup"><span data-stu-id="ca8a8-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="ca8a8-107">В Views/Home/Index.cshtml добавьте элемент привязки к данным ссылку сведения:</span><span class="sxs-lookup"><span data-stu-id="ca8a8-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="ca8a8-108">Этот код привязывает обработчик щелчка для &lt;&gt; элемент `getBookDetail` функции в модели представления.</span><span class="sxs-lookup"><span data-stu-id="ca8a8-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="ca8a8-109">В этом же файле Замените следующие комментариев:</span><span class="sxs-lookup"><span data-stu-id="ca8a8-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="ca8a8-110">следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ca8a8-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="ca8a8-111">Эта разметка создает таблицу, данные которого привязаны к свойствам `detail` наблюдаемые в модели представления.</span><span class="sxs-lookup"><span data-stu-id="ca8a8-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="ca8a8-112">"&lt;!--Ko--&gt; &quot; синтаксис позволяет включить привязку Knockout вне элемента DOM.</span><span class="sxs-lookup"><span data-stu-id="ca8a8-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="ca8a8-113">В этом случае `if` привязка передает этот раздел разметки для отображения только тогда, когда `details` отлично от NULL.</span><span class="sxs-lookup"><span data-stu-id="ca8a8-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="ca8a8-114">Теперь, если вы запустите приложение и щелкните одну из &quot;подробно&quot; ссылки, приложения, отобразятся сведения о книге.</span><span class="sxs-lookup"><span data-stu-id="ca8a8-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="ca8a8-115">[Назад](part-7.md)
> [Вперед](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="ca8a8-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
