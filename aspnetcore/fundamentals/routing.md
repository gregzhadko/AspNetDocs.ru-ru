---
title: Маршрутизация в ASP.NET Core
author: rick-anderson
description: Узнайте, как маршрутизация ASP.NET Core отвечает за сопоставление URI запросов с селекторами конечных точек и отправку входящих запросов к конечным точкам.
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: fundamentals/routing
ms.openlocfilehash: 3dbb2d358ec9e3dcdd96c3771576911d906d796f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044671"
---
# <a name="routing-in-aspnet-core"></a>Маршрутизация в ASP.NET Core

Авторы: [Райан Новак](https://github.com/rynowak) (Ryan Nowak), [Стив Смит](https://ardalis.com/) (Steve Smith) и [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

::: moniker range="<= aspnetcore-1.1"

Для версии 1.1 этого раздела скачайте статью [Маршрутизация ASP.NET Core (версия 1.1, PDF-файл)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Routing_1.x.pdf).

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

Маршрутизация отвечает за сопоставление URI запросов с селекторами конечной точки и отправку входящих запросов к конечным точкам. Маршруты определяются в приложении и настраиваются при его запуске. Маршрут может также извлекать значения из содержащегося в запросе URL-адреса, которые затем используются для обработки запроса. С помощью сведений о маршрутах из приложения маршрутизация также может формировать URL-адреса, которые сопоставляются с селекторами конечных точек.

::: moniker-end

::: moniker range="= aspnetcore-2.2"

Чтобы использовать новейшие сценарии маршрутизации в ASP.NET Core 2.2, укажите [совместимую версию](xref:mvc/compatibility-version) для регистрации служб MVC в `Startup.ConfigureServices`:

```csharp
services.AddMvc()
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
```

Параметр <xref:Microsoft.AspNetCore.Mvc.MvcOptions.EnableEndpointRouting> определяет, должна ли маршрутизация внутренне использовать логику, основанную на конечных точках, или логику, основанную на <xref:Microsoft.AspNetCore.Routing.IRouter>, в ASP.NET Core 2.1 или более ранней версии. Если установлена совместимая версия 2.2 или более поздняя, значение по умолчанию — `true`. Задайте значение `false`, чтобы использовать предыдущую логику маршрутизации:

```csharp
// Use the routing logic of ASP.NET Core 2.1 or earlier:
services.AddMvc(options => options.EnableEndpointRouting = false)
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
```

Дополнительные сведения о маршрутизации на основе <xref:Microsoft.AspNetCore.Routing.IRouter> см. в разделе [о версии ASP.NET Core 2.1 в этой статье](/aspnet/core/fundamentals/routing?view=aspnetcore-2.1).

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Маршрутизация отвечает за сопоставление URI запросов с обработчиками маршрутов и отправку входящих запросов. Маршруты определяются в приложении и настраиваются при его запуске. Маршрут может также извлекать значения из содержащегося в запросе URL-адреса, которые затем используются для обработки запроса. С помощью настроенных маршрутов из приложения маршрутизация создает URL-адреса, которые сопоставляются с обработчиками маршрутов.

::: moniker-end

::: moniker range="= aspnetcore-2.1"

Чтобы использовать новейшие сценарии маршрутизации в ASP.NET Core 2.1, укажите [совместимую версию](xref:mvc/compatibility-version) для регистрации служб MVC в `Startup.ConfigureServices`:

```csharp
services.AddMvc()
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
```

::: moniker-end

> [!IMPORTANT]
> В этом документе рассматривается низкоуровневая маршрутизация ASP.NET Core. Сведения о маршрутизации ASP.NET Core MVC см. в разделе <xref:mvc/controllers/routing>. Сведения о соглашениях о маршрутизации в Razor Pages см. в разделе <xref:razor-pages/razor-pages-conventions>.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/routing/samples) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="routing-basics"></a>Основы маршрутизации

Для большинства приложений следует выбрать базовую описательную схему маршрутизации таким образом, чтобы URL-адреса были удобочитаемыми и осмысленными. Традиционный маршрут по умолчанию `{controller=Home}/{action=Index}/{id?}`.

* Поддерживает основную и описательную схемы маршрутизации.
* Является отправной точкой для приложений на базе пользовательского интерфейса.

Как правило, в зонах приложения с высоким трафиком и в особых случаях (например, конечные точки блога, интернет-магазина) добавляются дополнительные краткие маршруты с использованием [маршрутизации с помощью атрибутов](xref:mvc/controllers/routing#attribute-routing) или выделенные традиционные маршруты.

Веб-интерфейсы API должны использовать маршрутизацию с помощью атрибутов, чтобы моделировать функциональность приложения в качестве набора ресурсов, где операции представлены с помощью команд HTTP. Это означает, что многие операции (например, GET, POST) на одном логическом ресурсе будут использовать одинаковый URL-адрес. Маршрутизация с помощью атрибутов обеспечивает необходимый уровень контроля, позволяющий тщательно разработать схему общедоступных конечных точек API-интерфейса.

Приложения Razor Pages используют стандартную маршрутизацию по умолчанию для предоставления именованных ресурсов в папке *Pages* приложения. Доступны дополнительные соглашения, которые позволяют настроить поведение маршрутизации Razor Pages. Дополнительные сведения см. в разделах <xref:razor-pages/index> и <xref:razor-pages/razor-pages-conventions>.

Благодаря поддержке создания URL-адресов приложение можно разрабатывать без жесткого программирования URL-адресов для связывания компонентов приложения. Это обеспечивает начало работы с основной конфигурацией маршрутизации и изменение маршрутов после определения схемы ресурсов приложения.

::: moniker range=">= aspnetcore-2.2"

Маршрутизация использует *конечные точки* (`Endpoint`) для представления логических конечных точек в приложении.

Конечная точка определяет делегат для обработки запросов и коллекцию произвольных метаданных. Метаданные используются для реализации сквозной функциональности на основе политик и конфигурации каждой конечной точки.

Система маршрутизации обладает следующими характеристиками:

* Синтаксис шаблона маршрута используется для определения маршрутов с помощью параметров размеченного маршрута.
* Допускается конфигурация конечной точки в стандартном стиле и с атрибутами.
* <xref:Microsoft.AspNetCore.Routing.IRouteConstraint> используется для определения того, содержит ли параметр URL-адреса допустимое значение для ограничения заданной конечной точки.
* Модели приложения, такие как MVC и Razor Pages, регистрируют все свои конечные точки, имеющие предсказуемую реализацию сценариев маршрутизации.
* Реализация маршрутизации принимает решения о маршрутизации в нужном месте конвейера ПО промежуточного слоя.
* ПО промежуточного слоя, которое появляется после ПО промежуточного слоя маршрутизации, может проверить результат принятия решений о конечной точке, принятое ПО промежуточного слоя маршрутизации для заданного URI запроса.
* Можно перечислить все конечные точки в приложении в любом месте конвейера ПО промежуточного слоя.
* Приложение может использовать маршрутизацию для формирования URL-адресов (например, для перенаправления или ссылок) на основе сведений о конечной точке, что позволяет избежать жесткого задания URL-адресов и упрощает поддержку.
* Формирование URL-адреса основано на адресах, которые поддерживают произвольную расширяемость:

  * API генератора ссылок (<xref:Microsoft.AspNetCore.Routing.LinkGenerator>) может быть разрешено в любом месте с помощью [внедрения зависимостей (DI)](xref:fundamentals/dependency-injection) для формирования URL-адреса.
  * Если API генератора ссылок недоступно через внедрение зависимостей, <xref:Microsoft.AspNetCore.Mvc.IUrlHelper> предлагает методы для создания URL-адреса.

> [!NOTE]
> С появлением маршрутизации по конечным точкам в ASP.NET Core 2.2 связывание конечных точек стало ограничено действиями и страницами MVC и Razor Pages. Расширение функций связывания конечных точек планируется в будущих выпусках.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Маршрутизация использует *маршруты* (реализации интерфейса <xref:Microsoft.AspNetCore.Routing.IRouter>) в следующих целях:

* для сопоставления входящих запросов с *обработчиками маршрутов*;
* для создания URL-адресов, используемых в ответах.

По умолчанию приложение имеет одну коллекцию маршрутов. Когда запрос прибывает, маршруты в коллекции обрабатываются в порядке, в котором они существуют в коллекции. Платформа пытается сопоставить URL-адрес входящего запроса с маршрутом в коллекции, вызывая метод <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*> для каждого маршрута в коллекции. Отклик может использовать маршрутизацию для формирования URL-адресов (например, для перенаправления или ссылок) на основе сведений о маршруте, что позволяет избежать жесткого задания URL-адресов и упрощает поддержку.

Система маршрутизации обладает следующими характеристиками:

* Синтаксис шаблона маршрута используется для определения маршрутов с помощью параметров размеченного маршрута.
* Допускается конфигурация конечной точки в стандартном стиле и с атрибутами.
* <xref:Microsoft.AspNetCore.Routing.IRouteConstraint> используется для определения того, содержит ли параметр URL-адреса допустимое значение для ограничения заданной конечной точки.
* Модели приложения, такие как MVC и Razor Pages, регистрируют все свои маршруты, имеющие предсказуемую реализацию сценариев маршрутизации.
* Отклик может использовать маршрутизацию для формирования URL-адресов (например, для перенаправления или ссылок) на основе сведений о маршруте, что позволяет избежать жесткого задания URL-адресов и упрощает поддержку.
* Формирование URL-адреса основано на маршрутах, которые поддерживают произвольную расширяемость. <xref:Microsoft.AspNetCore.Mvc.IUrlHelper> предоставляет методы для создания URL-адресов.

::: moniker-end

Функция маршрутизации подключается к конвейеру [ПО промежуточного слоя](xref:fundamentals/middleware/index) с помощью класса <xref:Microsoft.AspNetCore.Builder.RouterMiddleware>. [ASP.NET Core MVC](xref:mvc/overview) добавляет функцию маршрутизации в конвейер ПО промежуточного слоя в процессе настройки и обрабатывает маршрутизацию в приложениях MVC и Razor Pages. Сведения об использовании маршрутизации в виде отдельного компонента см. в руководстве по [использованию ПО промежуточного слоя маршрутизации](#use-routing-middleware).

### <a name="url-matching"></a>Соответствие URL-адресов

::: moniker range=">= aspnetcore-2.2"

Сопоставление URL-адресов — это процесс, с помощью которого функция маршрутизации отправляет входящий запрос в *конечную точку*. Этот процесс основывается на данных в пути URL-адреса, но может быть расширен для учета любых данных в запросе. Возможность отправки запросов в отдельные обработчики имеет первостепенное значение для масштабирования размера и сложности приложения.

Система маршрутизации в маршрутизации по конечным точкам принимает все решения об отправке. Так как ПО промежуточного слоя применяет политики в зависимости от выбранной конечной точки, очень важно, чтобы любое решение, которое может повлиять на отправку или применение политик безопасности, принималось внутри системы маршрутизации.

Когда делегат конечной точки выполняется, свойствам [RouteContext.RouteData](xref:Microsoft.AspNetCore.Routing.RouteContext.RouteData) присваиваются значения с учетом уже выполненной на текущий момент обработки.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Соответствие URL-адресов — это процесс, с помощью которого функция маршрутизации отправляет входящий запрос в *обработчик*. Этот процесс основывается на данных в пути URL-адреса, но может быть расширен для учета любых данных в запросе. Возможность отправки запросов в отдельные обработчики имеет первостепенное значение для масштабирования размера и сложности приложения.

Входящие запросы поступают в объект <xref:Microsoft.AspNetCore.Builder.RouterMiddleware>, который вызывает метод <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*> для каждого маршрута по порядку. Экземпляр <xref:Microsoft.AspNetCore.Routing.IRouter> решает, следует ли *обрабатывать* запрос, присваивая свойству [RouteContext.Handler](xref:Microsoft.AspNetCore.Routing.RouteContext.Handler*) значение <xref:Microsoft.AspNetCore.Http.RequestDelegate>, отличное от NULL. Если маршрут задает обработчик для запроса, обработка маршрутов останавливается и обработчик вызывается для обработки запроса. Если обработчик маршрута для обработки запроса не найден, ПО промежуточного слоя передает запрос следующему ПО промежуточного слоя в конвейере запросов.

Основные входные данные метода <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*> — это объект [RouteContext.HttpContext](xref:Microsoft.AspNetCore.Routing.RouteContext.HttpContext*), связанный с текущим запросом. [RouteContext.Handler](xref:Microsoft.AspNetCore.Routing.RouteContext.Handler) и [RouteContext.RouteData](xref:Microsoft.AspNetCore.Routing.RouteContext.RouteData*) — это выходные значения, заданные после нахождения соответствующего маршрута.

При нахождении соответствия, которое вызывает <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*>, свойствам [RouteContext.RouteData](xref:Microsoft.AspNetCore.Routing.RouteContext.RouteData) также присваиваются значения с учетом уже выполненной на текущий момент обработки.

::: moniker-end

[RouteData.Values](xref:Microsoft.AspNetCore.Routing.RouteData.Values*) — это словарь *значений маршрута*, полученных из маршрута. Как правило, эти значения определяются путем разбивки URL-адреса на сегменты и могут использоваться для принятия входных данных пользователя или принятия дальнейших решений об отправке в приложении.

[RouteData.DataTokens](xref:Microsoft.AspNetCore.Routing.RouteData.DataTokens*) — это контейнер свойств с дополнительными данными, связанными с соответствующим маршрутом. Свойства <xref:Microsoft.AspNetCore.Routing.RouteData.DataTokens*> обеспечивают связывание данных состояния с каждым маршрутом, что позволяет приложению принимать решения в зависимости от соответствующего маршрута. Эти значения определяются разработчиком и никоим образом **не** влияют на поведение маршрутизации. Кроме того, значения, спрятанные в токенах [RouteData.DataToken](xref:Microsoft.AspNetCore.Routing.RouteData.DataTokens*), могут быть любого типа в отличие от значений [RouteData.Value](xref:Microsoft.AspNetCore.Routing.RouteData.Values), которые должны легко преобразовываться в строки и из строк.

[RouteData.Routers](xref:Microsoft.AspNetCore.Routing.RouteData.Routers) — это список маршрутов, которые участвовали в успешном сопоставлении с запросом. Маршруты могут быть вложены друг в друга. Свойство <xref:Microsoft.AspNetCore.Routing.RouteData.Routers> отражает путь по логическому дереву маршрутов, который привел к совпадению. Как правило, первый элемент в свойстве <xref:Microsoft.AspNetCore.Routing.RouteData.Routers> — это коллекция маршрутов, используемая для формирования URL-адресов. Последний элемент в свойстве <xref:Microsoft.AspNetCore.Routing.RouteData.Routers> — это соответствующий обработчик маршрутов.

### <a name="url-generation"></a>Формирование URL-адреса

::: moniker range=">= aspnetcore-2.2"

Формирование URL-адреса — это процесс создания пути URL-адреса функцией маршрутизации на основе набора значений маршрута. Он обеспечивает логическое разделение конечных точек и URL-адресов, по которым к ним осуществляется доступ.

Маршрутизация по конечным точкам включает в себя API генератора ссылок (<xref:Microsoft.AspNetCore.Routing.LinkGenerator>). <xref:Microsoft.AspNetCore.Routing.LinkGenerator> — это отдельная служба, которую можно получить посредством внедрения зависимостей. API можно использовать вне контекста выполнения запроса. <xref:Microsoft.AspNetCore.Mvc.IUrlHelper> MVC и сценарии, которые зависят от <xref:Microsoft.AspNetCore.Mvc.IUrlHelper>, такие как [вспомогательные функции тегов](xref:mvc/views/tag-helpers/intro), вспомогательные методы HTML и [результаты действий](xref:mvc/controllers/actions), используют генератор ссылок для предоставления возможностей создания ссылок.

Генератор ссылок использует концепции *адреса* и *схем адресов*. Схема адресов — это способ определения конечных точек, которые должны рассматриваться для создания ссылки. Например, сценарии с именем маршрута и значениями маршрута, с которыми многие пользователи знакомы по MVC и Razor Pages, реализуются как схема адресов.

Генератор ссылок может установить связь с действиями и страницами MVC и Razor Pages с помощью следующих методов расширения:

* <xref:Microsoft.AspNetCore.Routing.ControllerLinkGeneratorExtensions.GetPathByAction*>
* <xref:Microsoft.AspNetCore.Routing.ControllerLinkGeneratorExtensions.GetUriByAction*>
* <xref:Microsoft.AspNetCore.Routing.PageLinkGeneratorExtensions.GetPathByPage*>
* <xref:Microsoft.AspNetCore.Routing.PageLinkGeneratorExtensions.GetUriByPage*>

Перегрузка этих методов принимает аргументы, которые включают `HttpContext`. Эти методы являются функциональными эквивалентами `Url.Action` и `Url.Page`, но предлагают дополнительную гибкость и параметры.

Методы `GetPath*` наиболее схожи с `Url.Action` и `Url.Page` в том, что создают URI, содержащий абсолютный путь. Методы `GetUri*` всегда создают абсолютный URI, содержащий схему и узел. Методы, которые принимают `HttpContext`, создают URI в контексте выполнения запроса. Используются значения окружения маршрута, базовый URL-адрес, схема и узел из выполняющегося запроса, если не указано иное.

<xref:Microsoft.AspNetCore.Routing.LinkGenerator> вызывается с адресом. Создание URI происходит в два этапа:

1. Адрес привязан к списку конечных точек, соответствующих адресу.
1. `RoutePattern` конечной точки вычисляется, пока не будет найден шаблон маршрута, который соответствует предоставленным значениям. Полученный результат объединяется с другими частями URI, предоставленными генератору ссылок и возвращенными.

Методы, предоставляемые <xref:Microsoft.AspNetCore.Routing.LinkGenerator>, поддерживают стандартные возможности создания ссылки для любого типа адреса. Самый удобный способ использовать генератор ссылки — через методы расширения, которые выполняют операции для определенного типа адреса.

| Метод расширения   | Описание:                                                         |
| ------------------ | ------------------------------------------------------------------- |
| <xref:Microsoft.AspNetCore.Routing.LinkGenerator.GetPathByAddress*> | Создает URI с абсолютным путем на основе предоставленных значений. |
| <xref:Microsoft.AspNetCore.Routing.LinkGenerator.GetUriByAddress*> | Создает абсолютный URI на основе предоставленных значений.             |

> [!WARNING]
> Обратите внимание на следующие последствия вызова методов <xref:Microsoft.AspNetCore.Routing.LinkGenerator>:
>
> * Используйте методы расширения `GetUri*` с осторожностью в конфигурации приложения, которая не проверяет заголовок входящих запросов `Host`. Если не проверить заголовок входящих запросов `Host`, входные данные в запросе без доверия могут отправляться обратно клиенту в URI в представлении или странице. Рекомендуется, чтобы все рабочие приложения настраивали свой сервер на проверку заголовка `Host` относительно известных допустимых значений.
>
> * Используйте <xref:Microsoft.AspNetCore.Routing.LinkGenerator> с осторожностью в ПО промежуточного слоя в сочетании с `Map` или `MapWhen`. `Map*` изменяет базовый путь выполняющегося запроса, что влияет на выходные данные создания ссылки. Все API <xref:Microsoft.AspNetCore.Routing.LinkGenerator> разрешают указание базового пути. Всегда указывайте пустой базовый путь для отмены влияния `Map*` на создание ссылок.

## <a name="differences-from-earlier-versions-of-routing"></a>Отличия от более ранних версий маршрутизации

Существует несколько различий между маршрутизацией по конечным точкам в ASP.NET Core 2.2 или более поздней версии и более ранними версиями маршрутизации в ASP.NET Core:

* Система маршрутизации по конечным точкам не поддерживает расширяемость на основе <xref:Microsoft.AspNetCore.Routing.IRouter>, включая наследование от <xref:Microsoft.AspNetCore.Routing.Route>.

* Маршрутизация по конечным точкам не поддерживает [WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim). Используйте [совместимую версию](xref:mvc/compatibility-version) 2.1 (`.SetCompatibilityVersion(CompatibilityVersion.Version_2_1)`), чтобы продолжить использование оболочек совместимости.

* Маршрутизация по конечным точкам иначе обрабатывает регистр созданных URI при использовании стандартных маршрутов.

  Рассмотрим следующий шаблон маршрута по умолчанию:

  ```csharp
  app.UseMvc(routes =>
  {
      routes.MapRoute("default", "{controller=Home}/{action=Index}/{id?}");
  });
  ```

  Предположим, вы создаете ссылку на действие с помощью следующего маршрута:

  ```csharp
  var link = Url.Action("ReadPost", "blog", new { id = 17, });
  ```

  С помощью маршрутизации на основе <xref:Microsoft.AspNetCore.Routing.IRouter> этот код создает URI из `/blog/ReadPost/17`, который учитывает регистр предоставленного значения маршрута. Маршрутизация по конечным точкам в ASP.NET Core 2.2 или более поздней версии создает `/Blog/ReadPost/17` ("Blog" — с прописной буквы). Маршрутизация по конечным точкам предоставляет интерфейс `IOutboundParameterTransformer`, который можно использовать для настройки этого поведения на глобальном уровне или применения других соглашения для сопоставления URL-адресов.

  Дополнительные сведения см. в разделе [Справочник по преобразователям параметров](#parameter-transformer-reference).

* Создание ссылок, используемых MVC и Razor Pages со стандартными маршрутами, работает иначе при попытке сослаться на контроллер/действие или страницу, которые не существуют.

  Рассмотрим следующий шаблон маршрута по умолчанию:

  ```csharp
  app.UseMvc(routes =>
  {
      routes.MapRoute("default", "{controller=Home}/{action=Index}/{id?}");
  });
  ```

  Предположим, вы создаете ссылку на действие с помощью шаблона по умолчанию:

  ```csharp
  var link = Url.Action("ReadPost", "Blog", new { id = 17, });
  ```

  С маршрутизацией на основе `IRouter` результатом всегда будет `/Blog/ReadPost/17`, даже если `BlogController` не существует или не имеет метода действия `ReadPost`. Как и ожидалось, маршрутизация по конечным точкам в ASP.NET Core 2.2 или более поздней версии создает `/Blog/ReadPost/17`, если метод действия существует. *Но маршрутизация по конечным точкам создает пустую строку, если действие не существует.* По существу, маршрутизация по конечным точкам не предполагает, что конечная точка существует, если действие не существует.

* *Алгоритм отмены значения окружения* при создании ссылок работает иначе при маршрутизации по конечным точкам.

  *Отмена значения окружения* — это алгоритм, который решает, какие значения маршрута из текущего выполняемого запроса (значения окружения) могут использоваться в операции создания ссылки. Стандартная маршрутизация всегда отменяет лишние значения маршрута при привязке к другому действию. Маршрутизация с помощью атрибутов работала иначе до выпуска ASP.NET Core 2.2. В более ранних версиях ASP.NET Core ссылки на другое действие, которые используют те же имена параметров маршрута, приводили к ошибкам создания ссылки. В ASP.NET Core 2.2 или более поздней версии обе формы маршрутизации отменяют значения при привязке к другому действию.

  Рассмотрим следующий пример в ASP.NET Core 2.1 или более ранней версии. При привязке к другому действию (или странице) значения маршрута могут использоваться повторно нежелательным образом.

  В */Pages/Store/Product.cshtml*:

  ```cshtml
  @page "{id}"
  @Url.Page("/Login")
  ```

  В */Pages/Login.cshtml*:

  ```cshtml
  @page "{id?}"
  ```

  Если URI — `/Store/Product/18` в ASP.NET Core 2.1 или более ранней версии, ссылка, созданная на странице Store/Info с помощью `@Url.Page("/Login")` — `/Login/18`. Значение `id` 18 используется повторно, хотя конечный объект ссылки является совсем другой частью приложения. Значение маршрута `id` в контексте страницы `/Login`, вероятно, является значением идентификатора пользователя, а не кодом хранимого продукта.

  При маршрутизации по конечным точкам в ASP.NET Core 2.2 или более поздней версии результатом является `/Login`. Значения окружения не используются повторно, если конечный объект ссылки является другим действием или страницей.

* Синтаксис параметра кругового маршрута: символы прямой косой черты не кодируются при использовании синтаксиса универсального параметра с двумя звездочками (`**`).

  Во время создания ссылки система маршрутизации кодирует значение, записанное в универсальном параметре с двумя звездочками (`**`) (например, `{**myparametername}`), за исключением прямой косой черты. Универсальный параметр с двумя звездочками поддерживается в маршрутизации на основе `IRouter` в ASP.NET Core 2.2 или более поздней версии.

  Синтаксис универсального параметра с одной звездочкой в предыдущих версиях ASP.NET Core (`{*myparametername}`) поддерживается, и прямая косая черта кодируется.

  | Маршрут              | Ссылка, созданная с помощью<br>`Url.Action(new { category = "admin/products" })`&hellip; |
  | ------------------ | --------------------------------------------------------------------- |
  | `/search/{*page}`  | `/search/admin%2Fproducts` (прямая косая черта кодируется)             |
  | `/search/{**page}` | `/search/admin/products`                                              |

### <a name="middleware-example"></a>Пример ПО промежуточного слоя

В следующем примере ПО промежуточного слоя использует API <xref:Microsoft.AspNetCore.Routing.LinkGenerator>, чтобы создать ссылку на метод действия, который перечисляет хранимые продукты. Использование генератора ссылок путем его внедрения в класс и вызова `GenerateLink` доступно для любого класса в приложении.

```csharp
using Microsoft.AspNetCore.Routing;

public class ProductsLinkMiddleware
{
    private readonly LinkGenerator _linkGenerator;

    public ProductsLinkMiddleware(RequestDelegate next, LinkGenerator linkGenerator)
    {
        _linkGenerator = linkGenerator;
    }

    public async Task InvokeAsync(HttpContext httpContext)
    {
        var url = _linkGenerator.GetPathByAction("ListProducts", "Store");

        httpContext.Response.ContentType = "text/plain";

        await httpContext.Response.WriteAsync($"Go to {url} to see our products.");
    }
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Формирование URL-адреса — это процесс создания пути URL-адреса функцией маршрутизации на основе набора значений маршрута. Он обеспечивает логическое разделение обработчиков маршрутов и URL-адресов, которые получают к ним доступ.

Формирование URL-адреса — это итеративный процесс, который начинается с того, что пользовательский код или код платформы вызывает метод <xref:Microsoft.AspNetCore.Routing.IRouter.GetVirtualPath*> коллекции маршрутов. Метод <xref:Microsoft.AspNetCore.Routing.IRouter.GetVirtualPath*> каждого *маршрута* вызывается по очереди, пока не будет возвращен объект <xref:Microsoft.AspNetCore.Routing.VirtualPathData>, отличный от NULL.

Основные входные параметры метода <xref:Microsoft.AspNetCore.Routing.IRouter.GetVirtualPath*>:

* [VirtualPathContext.HttpContext](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.HttpContext)
* [VirtualPathContext.Values](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.Values)
* [VirtualPathContext.AmbientValues](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.AmbientValues)

Для определения возможности создания URL-адреса и включаемых значений в первую очередь используются значения, передаваемые в свойствах <xref:Microsoft.AspNetCore.Routing.VirtualPathContext.Values> и <xref:Microsoft.AspNetCore.Routing.VirtualPathContext.AmbientValues>. <xref:Microsoft.AspNetCore.Routing.VirtualPathContext.AmbientValues> — это набор значений маршрута, полученных в результате сопоставления текущего запроса. В свою очередь, <xref:Microsoft.AspNetCore.Routing.VirtualPathContext.Values> — это значения, определяющие способ создания нужного URL-адреса для текущей операции. <xref:Microsoft.AspNetCore.Routing.VirtualPathContext.HttpContext> предоставляется в том случае, если маршруту необходимо получить службы или дополнительные данные, связанные с текущим контекстом.

> [!TIP]
> Можно рассматривать [VirtualPathContext.Values](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.Values*) как набор переопределений для [VirtualPathContext.AmbientValues](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.AmbientValues*). При формировании URL-адреса производится попытка повторного использования значений маршрута из текущего запроса для создания URL-адресов для ссылок с помощью того же маршрута или значений маршрута.

Выходные данные метода <xref:Microsoft.AspNetCore.Routing.IRouter.GetVirtualPath*> содержатся в объекте <xref:Microsoft.AspNetCore.Routing.VirtualPathData>. Объект <xref:Microsoft.AspNetCore.Routing.VirtualPathData> аналогичен <xref:Microsoft.AspNetCore.Routing.RouteData>. <xref:Microsoft.AspNetCore.Routing.VirtualPathData> содержит <xref:Microsoft.AspNetCore.Routing.VirtualPathData.VirtualPath> для выходного URL-адреса, а также ряд дополнительных свойств, которые должны быть заданы маршрутом.

Свойство [VirtualPathData.VirtualPath](xref:Microsoft.AspNetCore.Routing.VirtualPathData.VirtualPath*) содержит *виртуальный путь*, создаваемый маршрутом. В зависимости от ситуации путь может требовать дальнейшей обработки. Чтобы представить созданный URL-адрес в формате HTML, добавьте в его начало базовый путь приложения.

[VirtualPathData.Router](xref:Microsoft.AspNetCore.Routing.VirtualPathData.Router*) — это ссылка на маршрут, который успешно создал URL-адрес.

Свойства [VirtualPathData.DataTokens](xref:Microsoft.AspNetCore.Routing.VirtualPathData.DataTokens*) представляют собой словарь дополнительных данных, связанных с маршрутом, который создал URL-адрес. Это эквивалент объекта [RouteData.DataTokens](xref:Microsoft.AspNetCore.Routing.RouteData.DataTokens*).

::: moniker-end

### <a name="create-routes"></a>Создание маршрутов

::: moniker range="< aspnetcore-2.2"

Маршрутизация предоставляет класс <xref:Microsoft.AspNetCore.Routing.Route> в качестве стандартной реализации <xref:Microsoft.AspNetCore.Routing.IRouter>. Класс <xref:Microsoft.AspNetCore.Routing.Route> использует синтаксис *шаблона маршрута* для определения шаблонов, которые будут сопоставляться с путем URL-адреса при вызове метода <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*>. При вызове метода <xref:Microsoft.AspNetCore.Routing.IRouter.GetVirtualPath*> объект <xref:Microsoft.AspNetCore.Routing.Route> будет использовать тот же шаблон маршрута для создания URL-адреса.

::: moniker-end

Большинство приложений создают маршруты, вызывая метод <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> или один из аналогичных методов расширения, определенных в интерфейсе <xref:Microsoft.AspNetCore.Routing.IRouteBuilder>. Все методы расширения <xref:Microsoft.AspNetCore.Routing.IRouteBuilder> создают экземпляр <xref:Microsoft.AspNetCore.Routing.Route> и добавляют его в коллекцию маршрутов.

::: moniker range=">= aspnetcore-2.2"

<xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> не принимает параметр обработчика маршрутов. <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> только добавляет маршруты, которые обрабатываются <xref:Microsoft.AspNetCore.Routing.RouteBuilder.DefaultHandler*>. Дополнительные сведения о маршрутизации в MVC см. в разделе <xref:mvc/controllers/routing>.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> не принимает параметр обработчика маршрутов. <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> только добавляет маршруты, которые обрабатываются <xref:Microsoft.AspNetCore.Routing.RouteBuilder.DefaultHandler*>. Обработчиком по умолчанию является `IRouter`, и обработчик может не обработать запрос. Например, ASP.NET Core MVC обычно настраивается в качестве обработчика по умолчанию, который обрабатывает только те запросы, которые соответствуют доступным контроллеру и действию. Дополнительные сведения о маршрутизации в MVC см. в разделе <xref:mvc/controllers/routing>.

::: moniker-end

В следующем коде приводится пример вызова <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*>, используемого в типичном определении маршрута ASP.NET Core MVC:

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
```

Этот шаблон соответствует пути URL-адреса и извлекает значения маршрута. Например, путь `/Products/Details/17` создает следующие значения маршрута: `{ controller = Products, action = Details, id = 17 }`.

Значения маршрута определяются с помощью разделения пути URL-адреса на сегменты и сопоставления каждого сегмента с именем *параметра маршрута* в шаблоне маршрута. Параметры маршрута являются именованными. Параметры определяются путем заключения имени параметра в фигурные скобки `{ ... }`.

Приведенный выше шаблон может также соответствовать пути URL-адреса `/`. В этом случае он предоставляет значения `{ controller = Home, action = Index }`. Связано это с тем, что параметры маршрута `{controller}` и `{action}` имеют значения по умолчанию, а параметр маршрута `id` является необязательным. Значение по умолчанию для параметра маршрута определяется с помощью знака равенства (`=`), за которым следует значение после имени параметра. Вопросительный знак (`?`) после имени параметра маршрута определяет параметр как необязательный.

Параметры маршрута со значением по умолчанию *всегда* предоставляют значения маршрута при совпадении маршрута. Необязательные параметры не предоставляют значение маршрута, если нет соответствующего сегмента пути URL-адреса. Подробное описание сценариев и синтаксиса шаблона маршрута см. в разделе [Справочник по шаблонам маршрутов](#route-template-reference).

В следующем примере в определении параметра маршрута `{id:int}` определяется [ограничение маршрута](#route-constraint-reference) для параметра маршрута `id`:

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id:int}");
```

Этот шаблон соответствует такому пути URL-адреса, как `/Products/Details/17`, но не `/Products/Details/Apples`. Ограничения маршрута реализуют интерфейс <xref:Microsoft.AspNetCore.Routing.IRouteConstraint> и проверяют значения маршрута. В этом примере значение маршрута `id` должно иметь возможность преобразования в целое число. Более подробное описание ограничений маршрутов, предоставляемых платформой, см. в разделе [Справочник по ограничениям маршрутов](#route-constraint-reference).

Дополнительные перегрузки <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> принимают значения для параметров `constraints`, `dataTokens` и `defaults`. Типичное применение этих параметров состоит в передаче анонимно типизированного объекта, причем имена свойств анонимного типа соответствуют именам параметров маршрута.

В следующих примерах <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> создаются эквивалентные маршруты:

```csharp
routes.MapRoute(
    name: "default_route",
    template: "{controller}/{action}/{id?}",
    defaults: new { controller = "Home", action = "Index" });

routes.MapRoute(
    name: "default_route",
    template: "{controller=Home}/{action=Index}/{id?}");
```

> [!TIP]
> Встроенный синтаксис определения ограничений и значений по умолчанию может быть удобнее для простых маршрутов. Однако некоторые сценарии, например токены данных, не поддерживаются встроенным синтаксисом.

В следующем примере показано еще несколько сценариев:

::: moniker range=">= aspnetcore-2.2"

```csharp
routes.MapRoute(
    name: "blog",
    template: "Blog/{**article}",
    defaults: new { controller = "Blog", action = "ReadArticle" });
```

Предыдущий шаблон соответствует такому пути URL-адреса, как `/Blog/All-About-Routing/Introduction`, и извлекает значения `{ controller = Blog, action = ReadArticle, article = All-About-Routing/Introduction }`. Значения маршрута по умолчанию для `controller` и `action` предоставляются маршрутом несмотря на то, что в шаблоне нет соответствующих параметров маршрута. Значения по умолчанию можно указать в шаблоне маршрута. Параметр маршрута `article` определяется как *универсальный* с помощью двух звездочек (`**`) перед именем. Универсальные параметры маршрута служат для фиксации оставшейся части пути URL-адреса, а также могут соответствовать пустой строке.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```csharp
routes.MapRoute(
    name: "blog",
    template: "Blog/{*article}",
    defaults: new { controller = "Blog", action = "ReadArticle" });
```

Предыдущий шаблон соответствует такому пути URL-адреса, как `/Blog/All-About-Routing/Introduction`, и извлекает значения `{ controller = Blog, action = ReadArticle, article = All-About-Routing/Introduction }`. Значения маршрута по умолчанию для `controller` и `action` предоставляются маршрутом несмотря на то, что в шаблоне нет соответствующих параметров маршрута. Значения по умолчанию можно указать в шаблоне маршрута. Параметр маршрута `article` определяется как *универсальный* с помощью звездочки (`*`) перед его именем. Универсальные параметры маршрута служат для фиксации оставшейся части пути URL-адреса, а также могут соответствовать пустой строке.

::: moniker-end

В следующем примере добавляются ограничения маршрута и токены данных:

```csharp
routes.MapRoute(
    name: "us_english_products",
    template: "en-US/Products/{id}",
    defaults: new { controller = "Products", action = "Details" },
    constraints: new { id = new IntRouteConstraint() },
    dataTokens: new { locale = "en-US" });
```

Предыдущий шаблон будет соответствовать такому пути URL-адреса, как `/en-US/Products/5`, и будет извлекать значения `{ controller = Products, action = Details, id = 5 }` и токены данных `{ locale = en-US }`.

![Токены в окне "Локальные"](routing/_static/tokens.png)

### <a name="route-class-url-generation"></a>Формирование URL-адреса класса маршрута

Класс <xref:Microsoft.AspNetCore.Routing.Route> может также формировать URL-адрес, объединяя набор значений маршрута с шаблоном маршрута. С логической точки зрения, этот процесс обратен сопоставлению пути URL-адреса.

> [!TIP]
> Чтобы лучше понять процесс формирования URL-адреса, представьте себе, какой URL-адрес нужно создать, а затем подумайте, как шаблон маршрута будет сопоставляться с этим URL-адресом. Какие значения будут получены? Примерно так производится формирование URL-адреса в классе <xref:Microsoft.AspNetCore.Routing.Route>.

В следующем примере используется общий маршрут по умолчанию ASP.NET Core MVC:

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
```

При значениях маршрута `{ controller = Products, action = List }` создается URL-адрес `/Products/List`. Значения маршрута заменяются на соответствующие параметры маршрута для образования пути URL-адреса. Так как `id` является необязательным параметром маршрута, URL-адрес успешно создается без значения для `id`.

При значениях маршрута `{ controller = Home, action = Index }` создается URL-адрес `/`. Предоставленные значения маршрута соответствуют значениям по умолчанию, поэтому сегменты, соответствующие значениям по умолчанию, можно спокойно опустить.

Оба созданных URL-адреса будут совершать круговой путь с таким же определением маршрута (`/Home/Index` и `/`) и предоставлять те же значения маршрута, которые использовались для формирования URL-адреса.

> [!NOTE]
> Приложение, использующее платформу ASP.NET Core MVC, должно создавать URL-адреса с помощью объекта <xref:Microsoft.AspNetCore.Mvc.Routing.UrlHelper>, а не вызывать маршрутизацию напрямую.

Дополнительные сведения о формировании URL-адресов см. в [справочнике по формированию URL-адресов](#url-generation-reference).

## <a name="use-routing-middleware"></a>Использование ПО промежуточного слоя маршрутизации

Ссылка на [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) в файле проекта приложения.

Добавьте маршрутизацию в контейнер службы в файле `Startup.ConfigureServices`:

[!code-csharp[](routing/samples/2.x/RoutingSample/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

Маршруты должны настраиваться в методе `Startup.Configure`. В этом примере приложения используются следующие API:

* <xref:Microsoft.AspNetCore.Routing.RouteBuilder>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapGet*> &ndash; — соответствует только HTTP-запросам GET.
* <xref:Microsoft.AspNetCore.Builder.RoutingBuilderExtensions.UseRouter*>

[!code-csharp[](routing/samples/2.x/RoutingSample/Startup.cs?name=snippet_RouteHandler)]

В таблице ниже приведены ответы с данными универсальными кодами ресурсов (URI).

| URI                    | Ответ                                          |
| ---------------------- | ------------------------------------------------- |
| `/package/create/3`    | Hello! Значения маршрута: [operation, create], [id, 3] |
| `/package/track/-3`    | Hello! Значения маршрута: [operation, track], [id, -3] |
| `/package/track/-3/`   | Hello! Значения маршрута: [operation, track], [id, -3] |
| `/package/track/`      | Запрос не дал результата, нет совпадений.              |
| `GET /hello/Joe`       | Hi, Joe!                                          |
| `POST /hello/Joe`      | Запрос не дал результата, совпадение только с HTTP GET. |
| `GET /hello/Joe/Smith` | Запрос не дал результата, нет совпадений.              |

::: moniker range="< aspnetcore-2.2"

Если вы настраиваете один маршрут, вызовите <xref:Microsoft.AspNetCore.Builder.RoutingBuilderExtensions.UseRouter*>, передав экземпляр `IRouter`. Использовать <xref:Microsoft.AspNetCore.Routing.RouteBuilder> не нужно.

::: moniker-end

Платформа предоставляет наборов методов расширения для создания маршрутов (<xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions>):

* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapDelete*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapGet*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapMiddlewareDelete*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapMiddlewareGet*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapMiddlewarePost*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapMiddlewarePut*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapMiddlewareRoute*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapMiddlewareVerb*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapPost*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapPut*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapRoute*>
* <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapVerb*>

::: moniker range="< aspnetcore-2.2"

Некоторые из перечисленных методов, такие как <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapGet*>, требуют <xref:Microsoft.AspNetCore.Http.RequestDelegate>. <xref:Microsoft.AspNetCore.Http.RequestDelegate> используется в качестве *обработчика маршрутов* при совпадении маршрута. Другие методы из этого семейства позволяют настраивать конвейер ПО промежуточного слоя, который будет использоваться в качестве обработчика маршрутов. Если метод `Map*` не принимает обработчик, например <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapRoute*>, он будет использовать объект <xref:Microsoft.AspNetCore.Routing.RouteBuilder.DefaultHandler*>.

::: moniker-end

Методы `Map[Verb]` используют ограничения, чтобы ограничить маршрут к HTTP-команде в имени метода. Например, см. класс <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapGet*> и тип <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapVerb*>.

## <a name="route-template-reference"></a>Справочник по шаблону маршрута

Токены в фигурных скобках (`{ ... }`) определяют *параметры маршрута*, которые будут привязаны при совпадении маршрута. В сегменте маршрута можно определить несколько параметров маршрута, но они должны разделяться литеральным значением. Например, `{controller=Home}{action=Index}` будет недопустимым маршрутом, так как между `{controller}` и `{action}` нет литерального значения. Эти параметры маршрута должны иметь имена, и для них могут быть определены дополнительные атрибуты.

Весь текст, кроме параметров маршрута (например, `{id}`) и разделителя пути `/`, должен соответствовать тексту в URL-адресе. Сопоставление текста производится без учета регистра на основе декодированного представления путь URL-адреса. Для сопоставления с литеральным разделителем параметров маршрута (`{` или `}`) разделитель следует экранировать путем повтора символа (`{{` или `}}`).

Шаблоны URL-адресов, которые пытаются получить имя файла с необязательным расширением, имеют свои особенности. Например, рассмотрим шаблон `files/{filename}.{ext?}`. Когда значения для `filename` и `ext` существуют, заполняются оба значения. Если в URL-адресе есть только значение для `filename`, маршрут совпадает, так как точка в конце (`.`) является необязательной. Следующие URL-адреса соответствуют этому маршруту:

* `/files/myFile.txt`
* `/files/myFile`

::: moniker range=">= aspnetcore-2.2"

Вы можете использовать звездочку (`*`) или две звездочки (`**`) в качестве префикса параметра маршрута для привязки к остальной части URI. Такие параметры называются *универсальными*. Например, `blog/{**slug}` соответствует любому URI, начинающемуся с сегмента `/blog`, за которым следует любое значение, присваиваемое в качестве значения маршрута `slug`. Универсальные параметры также могут соответствовать пустой строке.

Универсальный параметр экранирует соответствующие символы, если маршрут использует для формирования URL-адрес, включая символы разделителей пути (`/`). Например, маршрут `foo/{*path}` со значениями маршрутов `{ path = "my/path" }` формирует `foo/my%2Fpath`. Обратите внимание на экранированный знак косой черты. В качестве символов разделителя кругового пути используйте префикс параметра маршрута `**`. Маршрут `foo/{**path}` с `{ path = "my/path" }` формирует `foo/my/path`.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Вы можете использовать звездочку (`*`) в качестве префикса параметра маршрута для привязки к остальной части URI. Такой параметр называется *универсальным*. Например, `blog/{*slug}` соответствует любому URI, начинающемуся с сегмента `/blog`, за которым следует любое значение, присваиваемое в качестве значения маршрута `slug`. Универсальные параметры также могут соответствовать пустой строке.

Универсальный параметр экранирует соответствующие символы, если маршрут использует для формирования URL-адрес, включая символы разделителей пути (`/`). Например, маршрут `foo/{*path}` со значениями маршрутов `{ path = "my/path" }` формирует `foo/my%2Fpath`. Обратите внимание на экранированный знак косой черты.

::: moniker-end

Параметры маршрута могут иметь *значения по умолчанию*. Они указываются после имени параметра и знака равенства (`=`). Например, `{controller=Home}` определяет `Home` в качестве значения по умолчанию для `controller`. Значение по умолчанию используется, если для параметра нет значения в URL-адресе. Параметры маршрута могут быть необязательными (для этого необходимо добавить вопросительный знак (`?`) в конец имени параметра, например `id?`). Различие между необязательными параметрами и параметрами маршрута по умолчанию в том, что вторые всегда имеют значения &mdash; необязательный параметр имеет значение, только если оно предоставлено URL-адресом запроса.

Параметры маршрута могут иметь ограничения, которые должны соответствовать значению маршрута из URL-адреса. Добавив двоеточие (`:`) и имя ограничения после имени параметра маршрута, можно указать *встроенные ограничения* для параметра маршрута. Если для ограничения требуются аргументы, они указываются в скобках (`(...)`) после имени ограничения. Чтобы указать несколько встроенных ограничений, добавьте еще одно двоеточие (`:`) и имя ограничения.

Имя и аргументы ограничения передаются в службу <xref:Microsoft.AspNetCore.Routing.IInlineConstraintResolver> для создания экземпляра интерфейса <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>, который будет использоваться при обработке URL-адреса. Например, в шаблоне маршрута `blog/{article:minlength(10)}` определяется ограничение `minlength` с аргументом `10`. Более подробное описание ограничений маршрутов и список ограничений, предоставляемых платформой, см. в разделе [Справочник по ограничениям маршрутов](#route-constraint-reference).

::: moniker range=">= aspnetcore-2.2"

Параметры маршрута также могут иметь преобразователи параметров, которые преобразуют значение параметра при создании ссылок и сопоставлении действий и страниц с URL-адресами. Как и ограничения, преобразователи параметров можно включать в параметр маршрута, добавив двоеточие (`:`) и имя преобразователя после имени параметра маршрута. Например, шаблон маршрута `blog/{article:slugify}` задает преобразователь `slugify`. Дополнительные сведения о преобразователях параметров см. в разделе [Справочник по преобразователям параметров](#parameter-transformer-reference).

::: moniker-end

В приведенной ниже таблице показаны некоторые примеры шаблонов маршрутов и их поведение.

| Шаблон маршрута                           | Пример соответствующего URI    | URI запроса&hellip;                                                    |
| ---------------------------------------- | ----------------------- | -------------------------------------------------------------------------- |
| `hello`                                  | `/hello`                | Соответствует только одному пути `/hello`.                                     |
| `{Page=Home}`                            | `/`                     | Соответствует и задает для параметра `Page` значение `Home`.                                         |
| `{Page=Home}`                            | `/Contact`              | Соответствует и задает для параметра `Page` значение `Contact`.                                      |
| `{controller}/{action}/{id?}`            | `/Products/List`        | Сопоставляется с контроллером `Products` и действием `List`.                       |
| `{controller}/{action}/{id?}`            | `/Products/Details/123` | Сопоставляется с контроллером `Products` и действием `Details` (`id` имеет значение 123). |
| `{controller=Home}/{action=Index}/{id?`} | `/`                     | Сопоставляется с контроллером `Home` и методом `Index` (`id` пропускается).        |

Использование шаблона — это, как правило, самый простой подход к маршрутизации. Ограничения и значения по умолчанию также могут указываться вне шаблона маршрута.

> [!TIP]
> Чтобы увидеть, как встроенные реализации маршрутизации, такие как <xref:Microsoft.AspNetCore.Routing.Route>, сопоставляются с запросами, включите [ведение журнала](xref:fundamentals/logging/index).

## <a name="reserved-routing-names"></a>Зарезервированные имена маршрутизации

Следующие ключевые слова являются зарезервированными именами и не могут использоваться как имена маршрутов или параметры:

* `action`
* `area`
* `controller`
* `handler`
* `page`

## <a name="route-constraint-reference"></a>Справочник по ограничениям маршрутов

Ограничения маршрута применяются, когда найдено соответствие входящему URL-адресу и путь URL-адреса был разобран на значения маршрута. Как правило, ограничения маршрута служат для проверки значения маршрута, связанного посредством шаблона маршрута, и принятия решения касательно того, является ли значение приемлемым (да или нет). Некоторые ограничения маршрута используют данные, не относящиеся к значению маршрута, для определения возможности маршрутизации запроса. Например, <xref:Microsoft.AspNetCore.Routing.Constraints.HttpMethodRouteConstraint> может принимать или отклонять запрос в зависимости от HTTP-команды. Ограничения используются в маршрутизации запросов и создании ссылок.

> [!WARNING]
> Не используйте ограничения для **проверки входных данных**. Если ограничения используются для **проверки входных данных**, недопустимые входные данные будут вызывать ошибку *404 (не найдено)* вместо ошибки *400 (неверный запрос)* с соответствующим сообщением. Ограничения маршрутов следует использовать для **разрешения неоднозначности** похожих маршрутов, а не для проверки входных данных определенного маршрута.

В приведенной ниже таблице показаны примеры ограничения маршрутов и их ожидаемое поведение.

| ограничение | Пример | Примеры совпадений | Примечания |
| ---------- | ------- | --------------- | ----- |
| `int` | `{id:int}` | `123456789`, `-123456789` | Соответствует любому целому числу |
| `bool` | `{active:bool}` | `true`, `FALSE` | Соответствует `true` или `false` (без учета регистра) |
| `datetime` | `{dob:datetime}` | `2016-12-31`, `2016-12-31 7:32pm` | Соответствует допустимому значению `DateTime` (для инвариантного языка и региональных параметров — см. предупреждение) |
| `decimal` | `{price:decimal}` | `49.99`, `-1,000.01` | Соответствует допустимому значению `decimal` (для инвариантного языка и региональных параметров — см. предупреждение) |
| `double` | `{weight:double}` | `1.234`, `-1,001.01e8` | Соответствует допустимому значению `double` (для инвариантного языка и региональных параметров — см. предупреждение) |
| `float` | `{weight:float}` | `1.234`, `-1,001.01e8` | Соответствует допустимому значению `float` (для инвариантного языка и региональных параметров — см. предупреждение) |
| `guid` | `{id:guid}` | `CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | Соответствует допустимому значению `Guid` |
| `long` | `{ticks:long}` | `123456789`, `-123456789` | Соответствует допустимому значению `long` |
| `minlength(value)` | `{username:minlength(4)}` | `Rick` | Строка должна содержать не менее 4 символов |
| `maxlength(value)` | `{filename:maxlength(8)}` | `Richard` | Строка должна содержать не более 8 символов |
| `length(length)` | `{filename:length(12)}` | `somefile.txt` | Длина строки должна составлять ровно 12 символов |
| `length(min,max)` | `{filename:length(8,16)}` | `somefile.txt` | Строка должна содержать от 8 до 16 символов |
| `min(value)` | `{age:min(18)}` | `19` | Целочисленное значение не меньше 18 |
| `max(value)` | `{age:max(120)}` | `91` | Целочисленное значение не больше 120 |
| `range(min,max)` | `{age:range(18,120)}` | `91` | Целочисленное значение от 18 до 120 |
| `alpha` | `{name:alpha}` | `Rick` | Строка должна состоять из одной или нескольких букв (`a`-`z`, без учета регистра) |
| `regex(expression)` | `{ssn:regex(^\\d{{3}}-\\d{{2}}-\\d{{4}}$)}` | `123-45-6789` | Строка должна соответствовать регулярному выражению (см. советы по определению регулярного выражения) |
| `required` | `{name:required}` | `Rick` | Определяет обязательное наличие значения, не относящегося к параметру, во время формирования URL-адреса |

К одному параметру может применяться несколько разделенных запятой ограничений. Например, следующее ограничение ограничивает параметр целочисленным значением 1 или больше:

```csharp
[Route("users/{id:int:min(1)}")]
public User GetUserById(int id) { }
```

> [!WARNING]
> Ограничения маршрута, которые проверяют URL-адрес и могут быть преобразованы в тип CLR (например, `int` или `DateTime`), всегда используют инвариантные язык и региональные параметры. Эти ограничения предполагают, что URL-адрес является нелокализуемым. Предоставляемые платформой ограничения маршрутов не изменяют значения, хранящиеся в значениях маршрута. Все значения маршрута, переданные из URL-адреса, сохраняются как строки. Например, ограничение `float` пытается преобразовать значение маршрута в число с плавающей запятой, но преобразованное значение служит только для проверки возможности такого преобразования.

## <a name="regular-expressions"></a>Регулярные выражения

В платформе ASP.NET Core в конструктор регулярных выражений добавляются члены `RegexOptions.IgnoreCase | RegexOptions.Compiled | RegexOptions.CultureInvariant`. Описание этих членов см. в разделе <xref:System.Text.RegularExpressions.RegexOptions>.

В регулярных выражениях применяются разделители и токены, аналогичные используемым функцией маршрутизации и в языке C#. Токены регулярного выражения должны быть экранированы. Чтобы использовать регулярное выражение `^\d{3}-\d{2}-\d{4}$` при маршрутизации, выражение должно иметь символы `\` (обратная косая черта), представленные в строке в виде символов `\\` (двойная обратная косая черта) в исходном файле C#, для экранирования escape-символов строки `\` (если не используются [буквальные строковые литералы](/dotnet/csharp/language-reference/keywords/string)). Чтобы экранировать символы разделения параметров маршрутизации (`{`, `}`, `[`, `]`), используйте их дважды в выражении (`{{`, `}`, `[[`, `]]`). В следующей таблице показаны регулярные выражения и их экранированные варианты.

| Регулярное выражение    | Экранированное регулярное выражение     |
| --------------------- | ------------------------------ |
| `^\d{3}-\d{2}-\d{4}$` | `^\\d{{3}}-\\d{{2}}-\\d{{4}}$` |
| `^[a-z]{2}$`          | `^[[a-z]]{{2}}$`               |

Регулярные выражения, используемые при маршрутизации, часто начинаются с символа карета (`^`) и соответствуют начальной позиции строки. Выражения часто заканчиваются знаком доллара (`$`) и соответствуют концу строки. Благодаря символам `^` и `$` регулярное выражение сопоставляется со всем значением параметра маршрута. Если символы `^` и `$` отсутствуют, регулярное выражение сопоставляется с любой подстрокой внутри строки, что обычно нежелательно. В следующей таблице представлен ряд примеров и объясняются причины соответствия или несоответствия.

| Выражение   | String    | Соответствие | Комментарий               |
| ------------ | --------- | :---: |  -------------------- |
| `[a-z]{2}`   | hello     | Да   | Соответствие подстроки     |
| `[a-z]{2}`   | 123abc456 | Да   | Соответствие подстроки     |
| `[a-z]{2}`   | mz        | Да   | Соответствует выражению    |
| `[a-z]{2}`   | MZ        | Да   | Без учета регистра    |
| `^[a-z]{2}$` | hello     | Нет    | См. замечания, касающиеся символов `^` и `$`, выше |
| `^[a-z]{2}$` | 123abc456 | Нет    | См. замечания, касающиеся символов `^` и `$`, выше |

Дополнительные сведения о синтаксисе регулярных выражений см. в статье [Регулярные выражения в .NET Framework](/dotnet/standard/base-types/regular-expression-language-quick-reference).

Чтобы ограничить возможные значения параметра набором известных значений, используйте регулярное выражение. Например, при использовании выражения `{action:regex(^(list|get|create)$)}` значение маршрута `action` будет соответствовать только `list`, `get` или `create`. При передаче в словарь ограничений строка `^(list|get|create)$` будет эквивалентной. Ограничения, которые передаются в словарь ограничений (то есть не являются встроенными ограничениями шаблона) и не соответствуют одному из известных ограничений, также рассматриваются как регулярные выражения.

## <a name="custom-route-constraints"></a>Пользовательские ограничения маршрутов

Помимо встроенных ограничений маршрутов пользовательские ограничения маршрутов можно создать путем внедрения интерфейса <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>. Интерфейс <xref:Microsoft.AspNetCore.Routing.IRouteConstraint> содержит один метод, `Match`, который возвращает `true`, если ограничение удовлетворяется, и `false` — если нет.

Чтобы применить пользовательский метод <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>, тип ограничения маршрута необходимо зарегистрировать с помощью <xref:Microsoft.AspNetCore.Routing.RouteOptions.ConstraintMap> приложения в контейнере службы приложения. Объект <xref:Microsoft.AspNetCore.Routing.RouteOptions.ConstraintMap> — это словарь, который сопоставляет ключи ограничений пути с реализациями <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>, которые проверяют эти ограничения. <xref:Microsoft.AspNetCore.Routing.RouteOptions.ConstraintMap> приложения можно преобразовать в `Startup.ConfigureServices` как часть вызова [services.AddRouting](xref:Microsoft.Extensions.DependencyInjection.RoutingServiceCollectionExtensions.AddRouting*) или путем настройки <xref:Microsoft.AspNetCore.Routing.RouteOptions> непосредственно с помощью `services.Configure<RouteOptions>`. Пример:

```csharp
services.AddRouting(options =>
{
    options.ConstraintMap.Add("customName", typeof(MyCustomConstraint));
});
```

Ограничения могут применяться к маршрутам обычным способом с использованием имени, указанного при регистрации типа ограничения. Пример:

```csharp
[HttpGet("{id:customName}")]
public ActionResult<string> Get(string id)
```

::: moniker range=">= aspnetcore-2.2"

## <a name="parameter-transformer-reference"></a>Справочник по преобразователям параметров

Преобразователи параметров:

* Выполняются при формировании ссылки для <xref:Microsoft.AspNetCore.Routing.Route>.
* Реализуйте расширение `Microsoft.AspNetCore.Routing.IOutboundParameterTransformer`.
* Настраиваются с помощью <xref:Microsoft.AspNetCore.Routing.RouteOptions.ConstraintMap>.
* Принимают значение маршрута параметра и изменяют его на новое строковое значение.
* Приводят к использованию преобразованного значения в сформированной ссылке.

Например, пользовательский преобразователь параметра `slugify` в шаблоне маршрута `blog\{article:slugify}` с `Url.Action(new { article = "MyTestArticle" })` формирует значение `blog\my-test-article`.

Чтобы использовать преобразователь параметров в шаблоне маршрута, сначала настройте его с помощью <xref:Microsoft.AspNetCore.Routing.RouteOptions.ConstraintMap> в `Startup.ConfigureServices`:

```csharp
services.AddRouting(options =>
{
    // Replace the type and the name used to refer to it with your own
    // IOutboundParameterTransformer implementation
    options.ConstraintMap["slugify"] = typeof(SlugifyParameterTransformer);
});
```

Преобразователи параметров также используются платформами для преобразования URI, где разрешается конечная точка. Например, ASP.NET Core MVC с помощью преобразователей параметров преобразует значение маршрута, используемое для сопоставления `area`, `controller`, `action` и `page`.

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller:slugify=Home}/{action:slugify=Index}/{id?}");
```

С помощью предыдущего маршрута действие `SubscriptionManagementController.GetAll()` сопоставляется с URI `/subscription-management/get-all`. Преобразователь параметра не изменяет значения маршрута, используемые для формирования ссылки. Например, `Url.Action("GetAll", "SubscriptionManagement")` выводит `/subscription-management/get-all`.

ASP.NET Core предоставляет соглашения об API для использования преобразователей параметров со сформированными маршрутами:

* ASP.NET Core MVC поддерживает соглашение об API `Microsoft.AspNetCore.Mvc.ApplicationModels.RouteTokenTransformerConvention`. Это соглашение применяет указанный преобразователь параметров ко всем маршрутам атрибутов в приложении. Преобразователь параметров преобразует маркеры маршрутов атрибутов по мере их замены. Дополнительные сведения см. в разделе об [использовании преобразователя параметров для настройки замены маркеров](/aspnet/core/mvc/controllers/routing#use-a-parameter-transformer-to-customize-token-replacement).
* Razor Pages поддерживает соглашение об API `Microsoft.AspNetCore.Mvc.ApplicationModels.PageRouteTransformerConvention`. Это соглашение применяет указанный преобразователь параметров ко всем автоматически обнаруженным страницам Razor Pages. Преобразователь параметров преобразует сегменты папок и имен файлов маршрутов Razor Pages. Дополнительные сведения см. в разделе об [использовании преобразователя параметров для настройки маршрутов страниц](/aspnet/core/razor-pages/razor-pages-conventions#use-a-parameter-transformer-to-customize-page-routes).

::: moniker-end

## <a name="url-generation-reference"></a>Справочник по формированию URL-адресов

В приведенном ниже примере показано, как создать ссылку на маршрут с использованием словаря значений маршрута и коллекции <xref:Microsoft.AspNetCore.Routing.RouteCollection>.

[!code-csharp[](routing/samples/2.x/RoutingSample/Startup.cs?name=snippet_Dictionary)]

В результате приведенного выше примера создается <xref:Microsoft.AspNetCore.Routing.VirtualPathData.VirtualPath> со значением `/package/create/123`. Словарь предоставляет значения маршрута `operation` и `id` шаблона "Отслеживание маршрута пакета", `package/{operation}/{id}`. Дополнительные сведения см. в примере кода в разделе [Использование ПО промежуточного слоя маршрутизации](#use-routing-middleware) или в [примере приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/routing/samples).

Второй параметр конструктора <xref:Microsoft.AspNetCore.Routing.VirtualPathContext> — это коллекция *значений окружения*. Значения окружения упрощают разработку, ограничивая число значений, которые необходимо указывать в определенном контексте запроса. Текущие значения маршрута текущего запроса считаются значениями окружения для создания ссылки. В приложении ASP.NET MVC в действии `About` контроллера `HomeController` не нужно задавать значение маршрута контроллера, указывающее на действие `Index` &mdash; используется значение окружения `Home`.

Значения окружения, которые не соответствуют параметру, игнорируются. Значения окружения также не учитываются, когда явно указанное значение переопределяет значение окружения. Сопоставление выполняется слева направо в URL-адресе.

Явно предоставленные значения, которые не соответствуют сегменту маршрута, добавляются в строку запроса. В приведенной ниже таблице показан результат использования шаблона маршрута `{controller}/{action}/{id?}`.

| Значения окружения                     | Явные значения                        | Результат                  |
| ---------------------------------- | -------------------------------------- | ----------------------- |
| controller = "Home"                | action = "About"                       | `/Home/About`           |
| controller = "Home"                | controller = "Order", action = "About" | `/Order/About`          |
| controller = "Home", color = "Red" | action = "About"                       | `/Home/About`           |
| controller = "Home"                | action = "About", color = "Red"        | `/Home/About?color=Red` |

Если маршрут имеет значение по умолчанию, которое не соответствует параметру, и это значение предоставлено явным образом, оно должно соответствовать значению по умолчанию:

```csharp
routes.MapRoute("blog_route", "blog/{*slug}",
    defaults: new { controller = "Blog", action = "ReadPost" });
```

Для этого маршрута ссылка будет создана только в том случае, если предоставлены соответствующие значения для `controller` и `action`.

## <a name="complex-segments"></a>Сложные сегменты

Сложные сегменты (например, `[Route("/x{token}y")]`) обрабатываются путем "нежадного" сопоставления литералов справа налево. Подробные сведения о сопоставлении сложных сегментов см. в [этом коде](https://github.com/aspnet/AspNetCore/blob/release/2.2/src/Http/Routing/src/Patterns/RoutePatternMatcher.cs#L293). [Пример кода](https://github.com/aspnet/AspNetCore/blob/release/2.2/src/Http/Routing/src/Patterns/RoutePatternMatcher.cs#L293) не используется в ASP.NET Core, но он предоставляет подробное объяснение сложных сегментов.
<!-- While that code is no longer used by ASP.NET Core for complex segment matching, it provides a good match to the current algorithm. The [current code](https://github.com/aspnet/AspNetCore/blob/91514c9af7e0f4c44029b51f05a01c6fe4c96e4c/src/Http/Routing/src/Matching/DfaMatcherBuilder.cs#L227-L244) is too abstracted from matching to be useful for understanding complex segment matching.
-->
