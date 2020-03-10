---
uid: web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
title: '[Инструкции:] Использовать условный UpdateMode элемента UpdatePanel? | Документы Майкрософт'
author: JoeStagner
description: UpdatePanel ASP.NET AJAX включает свойство UpdateMode, которое может иметь значение "Always" или "Conditional". Значение по умолчанию всегда равно, в этом случае Упдатепан...
ms.author: riande
ms.date: 08/01/2007
ms.assetid: 10b5bad3-4c18-464f-9454-0b3e60b7b8be
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
msc.type: video
ms.openlocfilehash: c05d4f262d56dfba858443b830d72ff0520b65d7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510126"
---
# <a name="how-do-i-use-the-conditional-updatemode-of-the-updatepanel"></a><span data-ttu-id="b5102-105">[Инструкции:] Использовать условный UpdateMode элемента UpdatePanel?</span><span class="sxs-lookup"><span data-stu-id="b5102-105">[How Do I:] Use the Conditional UpdateMode of the UpdatePanel?</span></span>

<span data-ttu-id="b5102-106">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="b5102-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="b5102-107">UpdatePanel ASP.NET AJAX включает свойство UpdateMode, которое может иметь значение "Always" или "Conditional".</span><span class="sxs-lookup"><span data-stu-id="b5102-107">The ASP.NET AJAX UpdatePanel includes an UpdateMode property that may be set to 'Always' or 'Conditional'.</span></span> <span data-ttu-id="b5102-108">Значение по умолчанию всегда равно, в этом случае UpdatePanel всегда будет обновлять свое содержимое во время асинхронной обратной передачи.</span><span class="sxs-lookup"><span data-stu-id="b5102-108">The default is Always, in which case the UpdatePanel will always update its content during an asynchronous postback.</span></span> <span data-ttu-id="b5102-109">В этом видеоролике мы рассмотрим, как можно задать для параметра UpdateMode значение Conditional. в этом случае UpdatePanel будет обновлять содержимое только тогда, когда наш код на стороне сервера вызовет свой метод Update.</span><span class="sxs-lookup"><span data-stu-id="b5102-109">In this video we learn how we can set the UpdateMode to Conditional, in which case the UpdatePanel will only update its content when our server-side code calls its Update method.</span></span> <span data-ttu-id="b5102-110">Это позволяет использовать условную логику в коде C# или Visual Basic, чтобы определить, будет ли элемент UpdatePanel обновлять свое содержимое во время текущей асинхронной обратной передачи.</span><span class="sxs-lookup"><span data-stu-id="b5102-110">This allows you to use conditional logic in your C# or Visual Basic code to determine whether the UpdatePanel will update its content during the current asynchronous postback.</span></span>

[<span data-ttu-id="b5102-111">&#9654;Смотреть видео (13 минут)</span><span class="sxs-lookup"><span data-stu-id="b5102-111">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-conditional-updatemode-of-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="b5102-112">[Назад](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
> [Вперед](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span><span class="sxs-lookup"><span data-stu-id="b5102-112">[Previous](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
[Next](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span></span>
