---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Введение в учебнике по NerdDinner | Документация Майкрософт
author: shanselman
description: — Это наилучший способ подробнее узнать это новая платформа для создания чего-то с ним. В этом учебнике описывается создание небольшой, но законченного приложения с помощью ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59392200"
---
# <a name="introducing-the-nerddinner-tutorial"></a>Общие сведения об учебнике по NerdDinner

по [(Scott hanselman)](https://github.com/shanselman)

[Загрузить PDF-файл](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> — Это наилучший способ подробнее узнать это новая платформа для создания чего-то с ним. Этом руководстве описано, как создать небольшой, но завершить приложение с помощью ASP.NET MVC 1 и рассматриваются некоторые основные принципы его.
> 
> Если вы используете ASP.NET MVC 3, рекомендуется следовать [Приступая к работе с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.


## <a name="nerddinner-tutorial"></a>Учебнике по NerdDinner

— Это наилучший способ подробнее узнать это новая платформа для создания чего-то с ним. Этом руководстве описано, как создать небольшой, но завершить приложение с помощью ASP.NET MVC и рассматриваются некоторые основные принципы его.

Приложение, которое мы собираемся строить называется «NerdDinner». NerdDinner предоставляет простой способ для пользователей, для поиска и упорядочения ужинов через Интернет:

![](introducing-the-nerddinner-tutorial/_static/image1.png)

Зарегистрированные пользователи могут создавать, изменять и удалять ужинов NerdDinner. Он содержит согласованный набор проверки и бизнес-правила для приложения:

![](introducing-the-nerddinner-tutorial/_static/image2.png)

Посетители можно использовать карты на основе AJAX, поиск предстоящих ужинов, удерживаемая рядом с ними:

![](introducing-the-nerddinner-tutorial/_static/image3.png)

Компании dinner ведет на страницу подробностей, где они могут узнать больше об этом:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Если они интересуют посещение обед, они могут войти в систему или зарегистрируйтесь на сайте:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

Они затем можно щелкнуть ссылку RSVP на основе AJAX, чтобы принять участие в конференции:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>Реализация NerdDinner

Мы хотим начать наше приложение NerdDinner с помощью файла -&gt;команду Новый проект в Visual Studio, чтобы создать новый проект ASP.NET MVC. Мы будем затем постепенно добавлять функциональность и возможности. Попутно мы обсудим:

1. [Как создать новый проект ASP.NET MVC](create-a-new-aspnet-mvc-project.md)
2. [Создание базы данных](create-a-database.md)
3. [Как создать модель с проверками бизнес-правил](build-a-model-with-business-rule-validations.md)
4. [Практическое использование контроллеров и представлений для реализации списка и сведений пользовательского интерфейса](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [Как обеспечить CRUD (Создание, чтение, обновление и удаление) запись поддержки форм данных](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [Использование ViewData и реализация классов ViewModel](use-viewdata-and-implement-viewmodel-classes.md)
7. [Как повторно использовать пользовательский Интерфейс, с помощью главных страниц и частичных представлений](re-use-ui-using-master-pages-and-partials.md)
8. [Как реализовать эффективный данных разбиение по страницам](implement-efficient-data-paging.md)
9. [Защита приложений с помощью проверки подлинности и авторизации](secure-applications-using-authentication-and-authorization.md)
10. [Использование AJAX для доставки динамических обновлений](use-ajax-to-deliver-dynamic-updates.md)
11. [Использование AJAX для реализации сценариев сопоставления](use-ajax-to-implement-mapping-scenarios.md)
12. [Как включить автоматическое тестирование модулей](enable-automated-unit-testing.md)

Можно создать собственную копию NerdDinner с нуля, выполнив каждый шаг мы пошагового руководства в этой главе. Кроме того можно скачать готовую версию исходного кода, здесь: [NerdDinner на сайте GitHub](https://github.com/AspNetMVPSamples/NerdDinner). Можно также при необходимости также [Загрузите бесплатную версию PDF данного учебника](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) Если вы хотите прочитать руководство в автономном режиме.

Visual Studio 2008 или бесплатный Visual Web Developer 2008 Express можно использовать для построения приложения. Для базы данных можно использовать SQL Server или бесплатная SQL Server Express.

Вы можете установить ASP.NET MVC, Visual Web Developer 2008 Express и SQL Server Express (бесплатно) с помощью версии 2 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>Теперь приступим к работе...

Теперь, когда мы рассмотрели, что такое NerdDinner, давайте наших рукава и написать код.

Начнем с помощью файла -&gt;новый проект в Visual Studio, чтобы создать приложение NerdDinner.

> [!div class="step-by-step"]
> [Вперед](create-a-new-aspnet-mvc-project.md)
