---
title: Использование соглашений веб-API
author: pranavkm
description: Сведения о соглашениях веб-API в ASP.NET Core.
monikerRange: '>= aspnetcore-2.2'
ms.author: scaddie
ms.custom: mvc
ms.date: 12/13/2018
uid: web-api/advanced/conventions
ms.openlocfilehash: 5ae96b213a19464045e1d0b1a76f8eb81089dc5b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029941"
---
# <a name="use-web-api-conventions"></a>Использование соглашений веб-API

Авторы: [Пранав Кришнамурти (Pranav Krishnamoorthy)](https://github.com/pranavkm) и [Скот Эдди (Scott Addie)](https://github.com/scottaddie)

В ASP.NET Core 2.2 и более поздних версий добавлен способ извлечения распространенной [документации по API](xref:tutorials/web-api-help-pages-using-swagger) и ее применения к нескольким действиям, контроллерам или всем контроллерам в рамках сборки. Соглашения веб-API заменяют применение атрибута [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute) к отдельным действиям.

Соглашение позволяет следующее.

* Определять наиболее распространенные типы возврата и коды состояния, возвращаемые из определенного типа действия.
* Выявлять действия, отличающиеся от определенного стандарта.

ASP.NET Core MVC 2.2 и более поздних версий включает в себя набор соглашений по умолчанию в `Microsoft.AspNetCore.Mvc.DefaultApiConventions`. Соглашения основаны на контроллере (*ValuesController.cs*), предоставляемым в шаблоне проекта **API** ASP.NET Core. Если ваши действия соответствуют схеме в шаблоне, вы сможете успешно использовать соглашения по умолчанию. Если соглашения по умолчанию не соответствуют вашим потребностям, см. раздел [Создание соглашений веб-API](#create-web-api-conventions).

Во время выполнения <xref:Microsoft.AspNetCore.Mvc.ApiExplorer> понимает соглашения. `ApiExplorer` является абстракцией MVC для взаимодействия с генераторами документов [OpenAPI](https://www.openapis.org/) (также называется Swagger). Атрибуты из примененного соглашения связываются с действием и включаются в документацию OpenAPI для действия. [Анализаторы API](xref:web-api/advanced/analyzers) также понимают соглашения. Если ваше действие является нестандартным (например, возвращает код состояния, который не задокументирован примененным соглашением), выводится предупреждение, позволяющее задокументировать код состояния.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="apply-web-api-conventions"></a>Применение соглашений веб-API

Соглашения не являются составными, каждое действие может быть связано только с одним соглашением. Более конкретные соглашения имеют приоритет над менее определенными. Если к действию применяются два или более соглашения с одинаковым приоритетом, выбор осуществляется недетерминированным образом. Существуют следующие варианты применения соглашения к действию (от наиболее конкретного до наименее конкретного):

1. `Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; Применяется к отдельным действиям и указывает тип соглашения и применимый метод соглашения.

    В следующем примере метод соглашения `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` типа соглашения по умолчанию применяется к действию `Update`:

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=snippet_ApiConventionMethod&highlight=3)]

    Метод соглашения `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` применяет следующие атрибуты к действию:

    ```csharp
    [ProducesDefaultResponseType]
    [ProducesResponseType(204)]
    [ProducesResponseType(404)]
    [ProducesResponseType(400)]
    ```

Дополнительные сведения о `[ProducesDefaultResponseType]` см. в описании [ответа по умолчанию](https://swagger.io/docs/specification/describing-responses/#default).

1. `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`, примененный к контроллеру &mdash;, применяет определенный тип соглашения ко всем действиям в контроллере. Метод соглашения снабжен указаниями, определяющими действия, к которым применяется метод соглашения. Дополнительные сведения об указаниях см. в разделе [Создание соглашений веб-API](#create-web-api-conventions).

    В следующем примере набор соглашений по умолчанию применяется ко всем действиям в *ContactsConventionController*:

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=snippet_ApiConventionTypeAttribute&highlight=2)]

1. `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`, примененный к сборке &mdash;, применяет определенный тип соглашения ко всем контроллерам в текущей сборке. Атрибуты уровня сборки рекомендуется применять в файле *Startup.cs*.

    В следующем примере набор соглашений по умолчанию применяется ко всем контроллерам в сборке:

    [!code-csharp[](conventions/sample/Startup.cs?name=snippet_ApiConventionTypeAttribute&highlight=1)]

## <a name="create-web-api-conventions"></a>Создание соглашений веб-API

Если соглашения API по умолчанию не соответствуют вашим потребностям, создайте собственные соглашения. Соглашение:

* Это статический тип с методами.
* Может определять [типы ответов](#response-types) и [требования к именованию](#naming-requirements) для действий.

### <a name="response-types"></a>Типы ответов

Эти методы помечаются атрибутами `[ProducesResponseType]` или `[ProducesDefaultResponseType]`. Пример:

```csharp
public static class MyAppConventions
{
    [ProducesResponseType(200)]
    [ProducesResponseType(404)]
    public static void Find(int id)
    {
    }
}
```

Если отсутствуют более конкретные атрибуты метаданных, применение этого соглашения к сборке указывает, что:

* Метод соглашение применяется к любому действию с именем `Find`.
* Параметр с именем `id` присутствует для действия `Find`.

### <a name="naming-requirements"></a>Требования к именованию

Атрибуты `[ApiConventionNameMatch]` и `[ApiConventionTypeMatch]` можно применить к методу соглашения, определяющему действия, к которым они применяются. Пример:

```csharp
[ProducesResponseType(200)]
[ProducesResponseType(404)]
[ApiConventionNameMatch(ApiConventionNameMatchBehavior.Prefix)]
public static void Find(
    [ApiConventionNameMatch(ApiConventionNameMatchBehavior.Suffix)]
    int id)
{ }
```

В предшествующем примере:

* Параметр `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix`, примененный к методу, указывает, что соглашение соответствует любому действию с префиксом Find. Примеры соответствующих действий: `Find`, `FindPet` и `FindById`.
* `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix`, примененный к параметру, указывает, что соглашение соответствует методам только с одним параметром, заканчивающимся на идентификатор суффикса. Это такие параметры, как `id` или `petId`. `ApiConventionTypeMatch` может аналогичным образом применяться к типам для ограничения типа параметра. Аргумент `params[]` указывает на остальные параметры, которым не требуется явное сопоставление.

## <a name="additional-resources"></a>Дополнительные ресурсы

* <xref:web-api/advanced/analyzers>
* <xref:tutorials/web-api-help-pages-using-swagger>
