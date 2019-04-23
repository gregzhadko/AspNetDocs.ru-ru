---
uid: overview
title: Общие сведения о ASP.NET | Документация Майкрософт
author: rick-anderson
description: Введение в ASP.NET — это бесплатная платформа для создания веб-сайтов, веб-приложений и веб-API.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 03/12/2010
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 1ab51453913b387ffecf898536eb55b7418b0285
ms.sourcegitcommit: 2d53ed9e4c8b19d3526cbc689bfa8394c9449cec
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905635"
---
# <a name="aspnet-overview"></a>Обзор ASP.NET

ASP.NET — бесплатная интернет-платформа для создания замечательных веб-сайтов и веб-приложений с помощью HTML, CSS и JavaScript. Также можно создавать веб-API и использовать технологии реального времени, такие как веб-сокеты.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) является альтернативой ASP.NET.  Смотрите [рекомендации по выбору между ASP.NET и ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).

## <a name="get-started"></a>Начало работы

Установка [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community edition, это бесплатная интегрированная среда разработки для ASP.NET в Windows.

## <a name="websites-and-web-applications"></a>Веб-сайтов и веб-приложений

 ASP.NET предоставляет три платформы для создания веб-приложений. Веб-форм ASP.NET MVC и веб-страниц ASP.NET. Все три платформы стабильны и полноценны: замечательные веб-приложения можно создать с помощью любой из них. Независимо от того, какую платформу выберете, вы везде получите все преимущества и возможности ASP.NET.

Каждая платформа предназначена для определенного стиля разработки. Ваш выбор зависит от сочетания навыков программирования (знаний, опыта разработки), типа создаваемого приложения и удобного вам подхода к разработке.

Ниже приведен обзор каждой из платформ и некоторые идеи о выборе между ними. Если предпочитаете видео с введением, смотрите [Making Websites with ASP.NET (Создание веб-сайтов с ASP.NET)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) и [What is Web Tools? (Возможности веб-инструментов)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | Если у вас есть опыт | Стиль разработки | Опыт |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Веб-формы | Win Forms, WPF, .NET | Быстрая разработка с помощью широких возможностей библиотеки элементов управления, которые инкапсулируют разметку HTML | RAD среднего уровня, продвинутый уровень |
| MVC       | Ruby on Rails, .NET  | Полный контроль над разметкой HTML, код и разметка разделены, упрощенное написание тестов. Лучший выбор для мобильных устройств и одностраничных приложений (SPA). | Средний и продвинутый уровень |
| Веб-страницы  | Классический ASP, PHP     | HTML-разметка и код вместе в одном файле | Новый, среднего уровня |

### <a name="web-forms"></a>Веб-формы

С веб-формами ASP.NET можно создавать динамические веб-сайты, используя знакомую модель перетаскивания, управляемую событиями. Область конструирования и сотни элементов управления и компонентов позволяют быстро создавать комплексные сайты с эффективным пользовательским интерфейсом и доступом к данным.

[Дополнительные сведения о веб-формах](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC предлагает эффективный, основанный на шаблонах способ создания динамических веб-сайтов, который позволяет четко разделять проблемы и дает полный контроль над разметкой для увлекательных и гибких разработок. ASP.NET MVC содержит множество функций, позволяющих вести быструю TDD-совместимую разработку для создания сложных приложений, использующих новейшие веб-стандарты.

[Дополнительные сведения о MVC](mvc/index.md)

### <a name="aspnet-web-pages"></a>Веб-страницы ASP.NET

Веб-страницы ASP.NET и синтаксис Razor обеспечивают быстрый, понятный и простой способ объединения серверного кода с HTML для создания динамического веб-содержимого. Подключайтесь к базам данных, добавляйте видео, ссылки на сайты социальных сетей и множество других дополнительных функций, чтобы создавать прекрасные сайты, которые соответствуют новейшим веб-стандартам.

[Дополнительные сведения о веб-страницах](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Примечания о веб-формах, MVC и веб-страницах

Все три платформы ASP.NET основаны на платформе .NET Framework и используют основные функциональные возможности .NET и ASP.NET. Например, все три платформы предоставляют модель безопасности аутентификации, основанную на членстве, а также все три располагают одинаковыми возможностями для управления запросами, обработки сеансов и всех других основных функций ASP.NET.

Кроме того три платформы не полностью независимы и выбрав один не исключает с помощью другого. Так как платформы могут сосуществовать в одном веб-приложении, не часто можно увидеть отдельные компоненты приложения, написанные с использованием различных платформ. Например для клиентов части приложения могут разрабатываться в MVC для оптимизации разметки во время администрирования фрагменты и доступа к данным разрабатываются в веб-форм, чтобы воспользоваться преимуществами элементы управления данными и доступ к данным простой.

## <a name="web-apis"></a>Веб-API

Веб-API ASP.NET — это платформа, которая позволяет легко создавать HTTP-службы для широкого диапазона клиентов, включая браузеры и мобильные устройства. ASP.NET Web API - это идеальная платформа для сборки REST-приложений на базе .NET Framework.

[Дополнительные сведения о веб-API](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>Технологии реального времени

ASP.NET SignalR представляет новую библиотеку для разработчиков ASP.NET, которая упрощает разработку функций в режиме реального времени. SignalR позволяет двусторонний обмен информацией между сервером и клиентом. Серверы могут отправлять содержимое мгновенно предоставлять подключенным клиентам, так как она станет доступной. SignalR поддерживает веб-сокеты и переключается на другие совместимые методы для старых браузерах. SignalR включает API-интерфейсы для управления подключениями (например, подключения и события отключения), группирования подключений и авторизации.

[Дополнительные сведения о SignalR](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>Мобильные приложения и сайты

ASP.NET могут улучшить собственных мобильных приложений с внутренним веб-API, а также мобильные веб-сайтов, с помощью единообразие платформ, таких как Twitter Bootstrap. Если вы создаете собственное мобильное приложение, это легко создавать на основе JSON веб-API для доступа к данным дескриптором проверки подлинности и Push-уведомления для приложения. При создании быстрые сайтов для мобильных устройств, можно использовать любой CSS framework или откройте сетку системы вы предпочитаете, или выберите мощных мобильных систем как jQuery Mobile или Sencha и качественные мобильные приложения с помощью PhoneGap.

[Дополнительные сведения о разработке мобильных приложений и узла приложений](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>Приложения с одной страницей

Одностраничные приложения ASP.NET (SPA) позволяют создавать приложения, включающие значительное взаимодействие на стороне клиента, с использованием HTML 5, CSS 3 и JavaScript. Visual Studio включает шаблон для создания одностраничных приложений с помощью knockout.js и веб-API ASP.NET. Помимо встроенного шаблона SPA-шаблоны, созданные сообществом разработчиков, также доступны для загрузки.

[Узнайте больше о разработке одностраничного приложения](single-page-application/index.md)

## <a name="webhooks"></a>WebHooks

Веб-перехватчик — это упрощенный HTTP-шаблон, обеспечивающий простую модель подписки для связи друг с другом веб-API и SaaS-служб. Когда в службе происходит событие, зарегистрированным подписчикам отправляется уведомление в форме POST HTTP-запроса. Запрос POST содержит сведения о событии, благодаря чему получатель может выполнить соответствующие действия.

Веб-перехватчики используются в большом количестве служб, включая Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello и многих других. Например, веб-перехватчик может указывать, что файл был изменен в Dropbox, изменение кода зафиксировано в GitHub, платеж был инициализирован в PayPal или была создана карточка в Trello.

[Дополнительные сведения о веб-перехватчиков](webhooks/index.md)





<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
