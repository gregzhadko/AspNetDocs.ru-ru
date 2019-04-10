---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[Инструкции] Отправка сообщения электронной почты, асинхронно с помощью ASP.NET | Документация Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показано, как использовать классы System.Net.Mail в ASP.NET для отправки сообщения электронной почты асинхронной. Во-первых см. в разделе Настройка веб-сайт...
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421372"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a>[Инструкции] Отправка сообщения электронной почты, асинхронно с помощью ASP.NET

по [Крис Пелз](https://twitter.com/chrispels)

В этом видео Крис Пелз показано, как использовать классы System.Net.Mail в ASP.NET для отправки сообщения электронной почты асинхронной. Во-первых, см. в разделе Настройка веб-сайта для отправки электронной почты с помощью &lt;mailSettings&gt; в файле web.config. Создайте простой пользовательский интерфейс для ввода данных электронной почты. Затем вы научитесь создавать класс MailMessage используется для создания сообщения электронной почты в коде программной части для страницы. В рамках этого процесса, создайте обработчик событий для асинхронный обратный вызов после отправки сообщения электронной почты. В событии обработчик см. в разделе способа использования экземпляра класса AsynchCompletedEventArgs, который предоставляет сведения о отправки электронной почты, процесс. Наконец отправить тестовое электронное сообщение асинхронно, выполнив действия, описанные в режиме отладки и Просмотр фактического сообщения, полученные из процесса.

[&#9654;Просмотрите видео (18 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
