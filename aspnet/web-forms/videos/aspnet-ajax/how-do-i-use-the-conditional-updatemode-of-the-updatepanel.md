---
uid: web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
title: '[Инструкции] Использование условного свойства UpdateMode элемента управления UpdatePanel? | Документы Майкрософт'
author: JoeStagner
description: ASP.NET AJAX UpdatePanel включает в себя свойство UpdateMode, который может иметь значение «Всегда» или «Условный». По умолчанию используется всегда, в этом случае UpdatePan...
ms.author: riande
ms.date: 08/01/2007
ms.assetid: 10b5bad3-4c18-464f-9454-0b3e60b7b8be
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
msc.type: video
ms.openlocfilehash: d1d407863340ad143c9859263ff66d538ca00335
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423836"
---
<a name="how-do-i-use-the-conditional-updatemode-of-the-updatepanel"></a><span data-ttu-id="52e94-105">[Инструкции] Использование условного свойства UpdateMode элемента управления UpdatePanel?</span><span class="sxs-lookup"><span data-stu-id="52e94-105">[How Do I:] Use the Conditional UpdateMode of the UpdatePanel?</span></span>
====================
<span data-ttu-id="52e94-106">по [(Joe Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="52e94-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="52e94-107">ASP.NET AJAX UpdatePanel включает в себя свойство UpdateMode, который может иметь значение «Всегда» или «Условный».</span><span class="sxs-lookup"><span data-stu-id="52e94-107">The ASP.NET AJAX UpdatePanel includes an UpdateMode property that may be set to 'Always' or 'Conditional'.</span></span> <span data-ttu-id="52e94-108">Значение по умолчанию — всегда, в противном случае UpdatePanel всегда будет обновлять его содержимое во время асинхронной обратной передачи.</span><span class="sxs-lookup"><span data-stu-id="52e94-108">The default is Always, in which case the UpdatePanel will always update its content during an asynchronous postback.</span></span> <span data-ttu-id="52e94-109">В этом видео мы Узнайте, как можно задать UpdateMode для условных операций, в котором регистр UpdatePanel только обновит его содержимое при наших серверный код вызывает метод обновления.</span><span class="sxs-lookup"><span data-stu-id="52e94-109">In this video we learn how we can set the UpdateMode to Conditional, in which case the UpdatePanel will only update its content when our server-side code calls its Update method.</span></span> <span data-ttu-id="52e94-110">Это позволяет использовать условную логику в C# или Visual Basic код, чтобы определить, будет ли UpdatePanel обновления его содержимого во время текущей асинхронной обратной передачи.</span><span class="sxs-lookup"><span data-stu-id="52e94-110">This allows you to use conditional logic in your C# or Visual Basic code to determine whether the UpdatePanel will update its content during the current asynchronous postback.</span></span>

[<span data-ttu-id="52e94-111">&#9654;Просмотрите видео (13 минут)</span><span class="sxs-lookup"><span data-stu-id="52e94-111">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-conditional-updatemode-of-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="52e94-112">[Назад](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
> [Вперед](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span><span class="sxs-lookup"><span data-stu-id="52e94-112">[Previous](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
[Next](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span></span>
