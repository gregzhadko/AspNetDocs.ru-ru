---
uid: mvc/mvc5
title: ASP.NET MVC 5 | Документация Майкрософт
author: rick-anderson
description: ASP.NET MVC 5 ASP.NET MVC 5 — это платформа для создания масштабируемых, основанные на стандартах веб-приложений, с помощью хорошо проверенных шаблонах проектирования и мощь AS...
ms.author: riande
ms.date: 10/11/2018
ms.assetid: f79fbf7f-59e5-4279-a832-c1a0294630f4
msc.legacyurl: /mvc/mvc5
msc.type: content
ms.openlocfilehash: ed25b2563f8c3f2d686affbcad4e2844289cb287
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59406760"
---
# <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

## <a name="whats-new-in-aspnet-mvc-5"></a>Новые возможности в ASP.NET MVC 5

### <a name="one-aspnet"></a>One ASP.NET

Шаблоны проектов MVC веб тесно интегрированы с возможностями One ASP.NET. Можно настроить проект MVC и настроить проверку подлинности с помощью мастера создания проекта One ASP.NET. Вводное руководство в ASP.NET MVC 5 можно найти в [Приступая к работе с ASP.NET MVC 5](overview/getting-started/introduction/getting-started.md).

Сведения об обновлении проектов MVC 4 до MVC 5 см. в разделе [обновление ASP.NET MVC 4 и проекта веб-API до ASP.NET MVC 5 и веб-API 2](overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Шаблоны проектов MVC были обновлены для использования ASP.NET Identity для проверки подлинности и управления удостоверениями. Учебник, проверки подлинности Facebook и Google и новый API членства можно найти в [Создание приложения ASP.NET MVC 5 с использованием Facebook и Google OAuth2 и OpenID единого входа](overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) и [развертывание приложения Secure ASP.NET MVC с Членством, OAuth и базы данных SQL на Windows Azure веб-сайт](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

### <a name="bootstrap"></a>Начальная загрузка

Шаблон проекта MVC была обновлена для использования [Bootstrap](http://getbootstrap.com/) для предоставления изящный и отвечает на запросы внешнего вида и поведения, вы можете легко настроить. Дополнительные сведения см. в разделе [начальной загрузки в веб-проекта Visual Studio шаблоны](../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap).

### <a name="authentication-filters"></a>Фильтры проверки подлинности

[Фильтры проверки подлинности](http://www.dotnetcurry.com/showarticle.aspx?ID=957) — это новый тип фильтра в ASP.NET MVC, запустите перед фильтры авторизации в конвейере ASP.NET MVC и позволяют пользователю указать проверки подлинности логики по действиям, конкретного контроллера, или глобально для всех контроллеров. Фильтры проверки подлинности обрабатывают учетные данные в запросе и укажите соответствующий субъект. В ответ на неавторизованные запросы, фильтры проверки подлинности можно также добавить проблемы проверки подлинности. См. в разделе [фильтры проверки подлинности ASP.NET MVC 5](http://www.dotnetcurry.com/showarticle.aspx?ID=957), [фильтры проверки подлинности в ASP.NET MVC 5](http://theshravan.net/blog/authentication-filters-in-asp-net-mvc-5/).

### <a name="filter-overrides"></a>Переопределения фильтра

Теперь можно переопределять, какие фильтры относятся к методу конкретного действия или контроллер, указав [переопределить фильтр](http://www.davidhayden.me/blog/filter-overrides-in-asp-net-mvc-5). Переопределение фильтры задать фильтр типов, которые не должны выполняться для данной области (действий или контроллера). Это позволяет настроить фильтры, которые применяются глобально, но затем исключить определенные глобальные фильтры от применения определенных действий или контроллеров. См. в разделе [новый фильтр переопределяет функцию в ASP.NET MVC 5 и веб-API ASP.NET 2](https://weblogs.asp.net/imranbaloch/archive/2013/09/25/new-filter-overrides-in-asp-net-mvc-5-and-asp-net-web-api-2.aspx), [как использовать ASP.NET MVC 5 переопределяет функцию фильтрации](http://hackwebwith.net/how-to-use-the-asp-net-mvc-5-filter-overrides-feature/), и [переопределения фильтра в ASP.NET MVC 5](http://www.davidhayden.me/blog/filter-overrides-in-asp-net-mvc-5)

### <a name="attribute-routing"></a>Маршрутизация с помощью атрибутов

ASP.NET MVC теперь поддерживает [маршрутизации с помощью атрибутов](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx), благодаря вклад, Тим McCall, автор [AttributeRouting](https://github.com/mccalltd/AttributeRouting). С помощью маршрутизации с помощью атрибутов можно указать свои маршруты добавив аннотации для действия и контроллеры.

## <a name="new-web-project-experience"></a>Новый проект с веб-интерфейсом

Visual Studio улучшенные возможности создания нового веб-проектов, начиная с Visual Studio 2013. В **новый веб-проект ASP.NET** диалоговое окно, можно выбрать тип проекта, настроить любое сочетание технологий (веб-формы, MVC, веб-API), настройки параметров проверки подлинности, добавить поддержку Docker и добавить проект модульного теста.

![Новый проект ASP.NET](mvc5/_static/new-aspnet-web-app-dialog.png)

Диалоговое окно позволяет изменить параметры проверки подлинности по умолчанию для многих из шаблонов. Например при создании проекта веб-форм ASP.NET можно выбрать любой из следующих параметров:

- Без проверки подлинности
- Учетные записи отдельных пользователей (членства ASP.NET или журнал поставщиков социальных сетей в)
- Рабочих или учебных учетных записей (Active Directory в веб-приложение)
- Проверка подлинности Windows (Active Directory в приложении интрасети)

![Параметры проверки подлинности](mvc5/_static/change-authentication-dialog.png)

Дополнительные сведения о процессе создания веб-проектов, см. в разделе [Создание веб-проектов ASP.NET в Visual Studio](../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md). Дополнительные сведения о способах проверки подлинности см. в разделе [ASP.NET Identity](../identity/overview/index.md).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>Формирование шаблонов ASP.NET

Формирование шаблонов ASP.NET — это платформа создания кода для веб-приложений ASP.NET. Он позволяет легко добавлять стандартный код в проект, который взаимодействует с моделью данных.

В версиях Visual Studio до 2013 г. формирование шаблонов был ограничен проекты ASP.NET MVC. Начиная с Visual Studio 2013, можно использовать формирование шаблонов для любого проекта ASP.NET, включая веб-форм. Visual Studio не поддерживает создание страниц для проекта веб-форм, но по-прежнему можно использовать формирование шаблонов веб-формы, Добавление зависимостей MVC в проект. Поддержка создания страниц для веб-формы будет добавлена в будущей версии.

При использовании формирования шаблонов, все необходимые зависимости устанавливаются в проекте. Например если для создания проекта веб-форм ASP.NET, а затем использовать формирование шаблонов, чтобы добавить контроллер веб-API, необходимые пакеты NuGet и ссылки добавляются в проект автоматически.

Чтобы добавить формирование шаблонов MVC в проект веб-форм, добавьте **создать шаблонный элемент** и выберите **зависимостей MVC 5** в диалоговом окне. Существует два варианта для формирования шаблонов MVC; **Минимальные зависимости** и **полный зависимости**. При выборе **минимальные зависимости**, только пакеты NuGet и ссылки для ASP.NET MVC добавляются в проект. При выборе **полный зависимости**, а также содержимого файлов, необходимых для проекта MVC добавляются минимальные зависимости.

![Добавление элемента формирования шаблонов диалогового окна в Visual Studio](overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

Поддержка формирования шаблонов контроллеров async использует возможности асинхронной из Entity Framework 6.

Дополнительные сведения и учебники см. в разделе [Обзор формирование шаблонов ASP.NET](../visual-studio/overview/2013/aspnet-scaffolding-overview.md).

### <a name="get-help-and-report-issues"></a>Получить справку и сообщить о проблеме

- [Известные проблемы и критические изменения списка](../visual-studio/overview/2013/release-notes.md#knownissues)
- Получение справки и обсудить ASP.NET MVC 5 в [форумы](https://forums.asp.net/1146.aspx)
- [Сообщить об ошибке в ASP.NET MVC 5](https://github.com/aspnet/AspNetWebStack/issues)
- [Сделать запрос на функцию](http://aspnet.uservoice.com/forums/41201-asp-net-mvc)

### <a name="upgrade-from-aspnet-mvc-4"></a>Обновление с ASP.NET MVC 4

См. в разделе [как обновление ASP.NET MVC 4 и веб-API проекта ASP.NET MVC 5 и веб-API 2](overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)
