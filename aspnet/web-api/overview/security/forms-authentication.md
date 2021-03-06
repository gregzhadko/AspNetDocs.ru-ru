---
uid: web-api/overview/security/forms-authentication
title: Проверка подлинности с помощью форм в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: Описывает использование проверки подлинности с помощью форм в веб-API ASP.NET.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484380"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>Проверка подлинности с помощью форм в веб-API ASP.NET

по [Майк Уоссон](https://github.com/MikeWasson)

Проверка подлинности с помощью форм использует HTML-форму для отправки учетных данных пользователя на сервер. Он не является стандартом Интернета. Проверка подлинности с помощью форм подходит только для веб-API, которые вызываются из веб-приложения, чтобы пользователь мог взаимодействовать с формой HTML.

| Преимущества | Недостатки |
| --- | --- |
| — Простота реализации: встроена в ASP.NET. — Использует поставщик членства ASP.NET, который упрощает управление учетными записями пользователей. | — Не стандартный механизм проверки подлинности HTTP; использует файлы cookie HTTP вместо стандартного заголовка авторизации. — Требуется клиент браузера. — Учетные данные отправляются в виде открытого текста. — Уязвимые для подделки запросов между сайтами (CSRF); требуются меры по борьбе с CSRF. — Трудно использовать из клиентов, не использующих браузер. Для входа требуется браузер. — Учетные данные пользователя отправляются в запросе. — Некоторые пользователи отключают файлы cookie. |

Вкратце, проверка подлинности с помощью форм в ASP.NET работает следующим образом:

1. Клиент запрашивает ресурс, требующий проверки подлинности.
2. Если пользователь не прошел проверку подлинности, сервер возвращает HTTP 302 (найдено) и перенаправляет его на страницу входа.
3. Пользователь вводит учетные данные и отправляет форму.
4. Сервер возвращает другой HTTP-код 302, который перенаправляется обратно в исходный URI. Этот ответ включает файл cookie проверки подлинности.
5. Клиент снова запрашивает ресурс. Запрос включает файл cookie проверки подлинности, поэтому сервер предоставляет запрос.

![](forms-authentication/_static/image1.png)

Дополнительные сведения см [. в обзоре проверки подлинности с помощью форм.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>Использование проверки подлинности с помощью форм в веб-API

Чтобы создать приложение, использующее проверку подлинности на основе форм, выберите шаблон "Интернет приложение" в мастере проектов MVC 4. Этот шаблон создает контроллеры MVC для управления учетными записями. Можно также использовать шаблон "одностраничное приложение", доступный в обновлении ASP.NET 2012.

В контроллерах веб-API можно ограничить доступ с помощью атрибута `[Authorize]`, как описано в разделе [Использование атрибута [авторизовать]](authentication-and-authorization-in-aspnet-web-api.md#auth3).

Forms — для проверки подлинности запросов используется файл cookie сеанса. Браузеры автоматически отправляют все соответствующие файлы cookie на конечный веб-сайт. Эта функция делает проверку подлинности с помощью форм, потенциально уязвимой для атак с подделкой межсайтовых запросов (CSRF), и [предотвращает атаки от подделки запросов между сайтами (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).

Проверка подлинности с помощью форм не шифрует учетные данные пользователя. Поэтому проверка подлинности с помощью форм не является безопасной, если не используется SSL. См. раздел [Работа с SSL в веб-API](working-with-ssl-in-web-api.md).
