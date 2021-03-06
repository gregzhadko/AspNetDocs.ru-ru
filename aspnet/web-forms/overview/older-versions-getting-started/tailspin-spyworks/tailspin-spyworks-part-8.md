---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: Часть 8. окончательные страницы, обработка исключений и заключение | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 8 добавляется страница контактов, страница About и исключение...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474342"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>Часть 8. Последние страницы, обработка исключений и заключение

кем [Джо Stagner)](https://github.com/JoeStagner)

> В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET. Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.
> 
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 8 добавляется страница контактов, сведения о странице и обработке исключений. Это заключение серии.

## <a id="_Toc260221680"></a>Страница "Контакты" (отправка электронной почты с ASP.NET)

Создание новой страницы с именем Контактус. aspx

С помощью конструктора создайте следующую форму, затратив особую заметку для включения Тулкитскриптманажер и элемента управления редактора из Ажаксконтролтулкит. .

![](tailspin-spyworks-part-8/_static/image1.jpg)

Дважды щелкните кнопку "Отправить", чтобы создать обработчик событий щелчка в файле кода программной части и реализовать метод отправки контактных данных в виде сообщения электронной почты.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

Этот код требует, чтобы файл Web. config содержал запись в разделе конфигурации, в которой указан SMTP-сервер, используемый для отправки почты.

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>Сведения о странице

Создайте страницу с именем AboutUs. aspx и добавьте любое нужное содержимое.

## <a id="_Toc260221682"></a>Глобальный обработчик исключений

Наконец, в рамках приложения мы выдавали исключения, и существуют непредвиденные обстоятельства, которые могут вызвать необработанные исключения в веб-приложении.

Никогда не нужно, чтобы необработанное исключение отображалось посетителю веб-узла.

![](tailspin-spyworks-part-8/_static/image2.jpg)

Помимо плохой необработанных исключений пользователь может быть проблемой безопасности.

Для решения этой проблемы будет реализован глобальный обработчик исключений.

Для этого откройте файл Global. asax и обратите внимание на следующий предварительно созданный обработчик событий.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

Добавьте код для реализации приложения\_обработчик ошибок следующим образом.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

Затем добавьте страницу с именем Error. aspx в решение и добавьте этот фрагмент кода разметки.

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

Теперь в обработчике событий "страница\_загрузки" извлекаются сообщения об ошибках из объекта запроса.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>Завершен

Мы увидели, что ASP.NET WebForms упрощает создание сложного веб-сайта с доступом к базе данных, членством, AJAX и т. д. очень быстро.

Надеюсь, в этом учебнике вы предоставили вам средства, необходимые для начала создания собственных приложений ASP.NET WebForms.

> [!div class="step-by-step"]
> [Назад](tailspin-spyworks-part-7.md)
