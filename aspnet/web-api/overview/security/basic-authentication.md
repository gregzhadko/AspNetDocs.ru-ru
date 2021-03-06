---
uid: web-api/overview/security/basic-authentication
title: Обычная проверка подлинности в веб-API ASP.NET | Документация Майкрософт
author: MikeWasson
description: Описывает использование обычной проверки подлинности в веб-API ASP.NET.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447636"
---
# <a name="basic-authentication-in-aspnet-web-api"></a>Обычная проверка подлинности в веб-API ASP.NET

по [Майк Уоссон](https://github.com/MikeWasson)

Обычная проверка подлинности определяется в [RFC 2617, проверка подлинности HTTP: обычная и дайджест-проверка подлинности](http://www.ietf.org/rfc/rfc2617.txt).

Недостатки

- Учетные данные пользователя отправляются в запросе.
- Учетные данные отправляются в виде открытого текста.
- Учетные данные отправляются при каждом запросе.
- Нет способа выйти из сеанса, за исключением случаев, когда завершается сеанс браузера.
- Уязвимо для подделки запросов между сайтами (CSRF); требуются меры по борьбе с CSRF.

Преимущества

- Стандартный Интернет.
- Поддерживается всеми основными браузерами.
- Относительно простой протокол.

Обычная проверка подлинности работает следующим образом.

1. Если для запроса требуется проверка подлинности, сервер возвращает 401 (несанкционированный). Ответ включает заголовок WWW-Authenticate, указывающий, что сервер поддерживает обычную проверку подлинности.
2. Клиент отправляет другой запрос с учетными данными клиента в заголовке авторизации. Учетные данные форматируются как строка "имя: пароль" в кодировке Base64. Учетные данные не шифруются.

Обычная проверка подлинности выполняется в контексте области. Сервер включает имя области в заголовке WWW-Authenticate. Учетные данные пользователя действительны в этой области. Точный диапазон области определяется сервером. Например, можно определить несколько областей для секционирования ресурсов.

![](basic-authentication/_static/image1.png)

Так как учетные данные отправляются незашифрованными, обычная проверка подлинности обеспечивается только по протоколу HTTPS. См. раздел [Работа с SSL в веб-API](working-with-ssl-in-web-api.md).

Обычная проверка подлинности также уязвима для атак CSRF. После того как пользователь введет учетные данные, браузер автоматически отправляет их при последующих запросах к тому же домену в течение сеанса. Сюда входят запросы AJAX. См. раздел [предотвращение атак с подделкой межсайтовых запросов (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).

## <a name="basic-authentication-with-iis"></a>Обычная проверка подлинности в IIS

Службы IIS поддерживают обычную проверку подлинности, но есть ряд предостережений: проверка подлинности пользователя выполняется по учетным данным Windows. Это означает, что пользователь должен иметь учетную запись в домене сервера. Для общедоступного веб-сайта обычно требуется пройти проверку подлинности для поставщика членства ASP.NET.

Чтобы включить обычную проверку подлинности с помощью служб IIS, задайте для режима проверки подлинности значение "Windows" в файле Web. config проекта ASP.NET:

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

В этом режиме службы IIS используют учетные данные Windows для проверки подлинности. Кроме того, необходимо включить обычную проверку подлинности в службах IIS. В диспетчере IIS перейдите в представление "функции", выберите Проверка подлинности и включите обычную проверку подлинности.

![](basic-authentication/_static/image2.png)

В проекте веб-API добавьте атрибут `[Authorize]` для всех действий контроллера, требующих проверки подлинности.

Клиент выполняет проверку подлинности самостоятельно, задавая заголовок авторизации в запросе. Клиенты браузера выполняют этот шаг автоматически. Клиентам, не имеющим браузер, необходимо задать заголовок.

## <a name="basic-authentication-with-custom-membership"></a>Обычная проверка подлинности с пользовательским членством

Как уже упоминалось, обычная проверка подлинности, встроенная в IIS, использует учетные данные Windows. Это означает, что необходимо создать учетные записи для пользователей на сервере размещения. Но для Интернет – учетные записи пользователей обычно хранятся во внешней базе данных.

В следующем коде показано, как модуль HTTP выполняет обычную проверку подлинности. Вы можете легко подключить поставщик членства ASP.NET, заменив метод `CheckPassword`, который является фиктивным методом в этом примере.

В веб-API 2 следует рассмотреть возможность написания [фильтра проверки подлинности](authentication-filters.md) или [OWIN по промежуточного слоя](../../../aspnet/overview/owin-and-katana/index.md), а не HTTP-модуля.

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

Чтобы включить модуль HTTP, добавьте следующий фрагмент в файл Web. config в разделе **System. Web Server** :

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

Замените "Йоурассемблинаме" именем сборки (не включая расширение "DLL").

Следует отключить другие схемы проверки подлинности, например формы или Windows Auth.
