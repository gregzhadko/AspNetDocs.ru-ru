---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[Инструкции] Использование свойства Reponse.Filter для замены HTML на странице ASP.NET | Документация Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показано использование свойства Reponse.Filter для перехвата и изменения HTML, отправляемого на страницу. Во-первых пример страницы создается w...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 0e8ae8b62bbb4ac1fc7e942cf3dd0438383cb510
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065081"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[Инструкции] Использование свойства Reponse.Filter для замены HTML на странице ASP.NET
====================
по [Крис Пелз](https://twitter.com/chrispels)

В этом видео Крис Пелз показано использование свойства Reponse.Filter для перехвата и изменения HTML, отправляемого на страницу. Во-первых пример страницы создается простой текст. Затем создается пользовательский класс Stream, служащий поток замены для текущего потока, отправляемого в браузер пользователя. В этом классе пользовательского потока содержимого страницы извлекаются из потока, изменении и записать в поток ответа. В этот пользовательский класс Stream метод Write настроено таким образом, чтобы заменить код HTML в базовый поток ответа, тем самым изменяя отправки в браузер пользователя. Наконец, новый класс потока назначается свойство Response.Filter на странице\_событию загрузки, тем самым предоставляя механизм для изменения содержимого страницы.

[&#9654;Просмотрите видео (13 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
