---
uid: web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
title: '[Инструкции] Внедрение изображения в сообщение электронной почты с помощью ASP.NET | Документация Майкрософт'
author: rick-anderson
description: Крис Пелз показано, как внедрить изображение в сообщение электронной почты с помощью ASP.NET. Он создает веб-форму (с полями для, из тему и текст), использует AlternateView...
ms.author: riande
ms.date: 11/06/2008
ms.assetid: 424788ac-0a43-4063-99e7-db5aa4c66a9d
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
msc.type: video
ms.openlocfilehash: fce565c7746acaa10ef1cf68e3ed98e052cca43e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59407280"
---
# <a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a><span data-ttu-id="d80cf-104">[Инструкции] Внедрение изображения в сообщение электронной почты с помощью ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d80cf-104">[How Do I:] Embed an Image in an Email with ASP.NET</span></span>

<span data-ttu-id="d80cf-105">по [Крис Пелз](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d80cf-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d80cf-106">Крис Пелз показано, как внедрить изображение в сообщение электронной почты с помощью ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d80cf-106">Chris Pels shows how to embed an image in an email with ASP.NET.</span></span> <span data-ttu-id="d80cf-107">Он создает веб-форму (с полями для, из тему и текст), для создания текста и HTML версиях сообщение электронной почты использует класса AlternateView, изображение хранится в экземпляре класса LinkedResource, он внедряется в HTML AlternateView.</span><span class="sxs-lookup"><span data-stu-id="d80cf-107">He creates a web form (with fields for To, From, Subject, and Body), uses the AlternateView class to create text and HTML versions of an email, stores an image in a LinkedResource class instance, embeds it in the HTML AlternateView.</span></span> <span data-ttu-id="d80cf-108">Затем он добавляет в объект MailMessage обе версии и дважды, отправляет сообщение электронной почты, сначала с HTML-получения возможностей, а затем как доступное только для текста.</span><span class="sxs-lookup"><span data-stu-id="d80cf-108">He then adds both versions to the MailMessage object and sends the email twice, first with HTML-receiving capabilities enabled and then as text-only.</span></span> <span data-ttu-id="d80cf-109">В Outlook отображается как сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="d80cf-109">Both email messages appear in Outlook.</span></span> <span data-ttu-id="d80cf-110">HTML-версия показывает внедренные изображения. Текстовая версия — нет.</span><span class="sxs-lookup"><span data-stu-id="d80cf-110">The HTML version shows the embedded image; the text version does not.</span></span>

[<span data-ttu-id="d80cf-111">&#9654;Просмотрите видео (19 минут)</span><span class="sxs-lookup"><span data-stu-id="d80cf-111">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)
