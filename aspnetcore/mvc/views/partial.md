---
title: Частичные представления в ASP.NET Core
author: ardalis
description: Узнайте, как с помощью частичных представлений разбить большие файлы разметки на части и предотвратить дублирование стандартных блоков разметки на веб-страницах приложений ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 09/11/2018
uid: mvc/views/partial
ms.openlocfilehash: ff4b99580990edbd768128d77214e664a1e29e56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033301"
---
# <a name="partial-views-in-aspnet-core"></a>Частичные представления в ASP.NET Core

Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith), [Люк Лэтэм](https://github.com/guardrex) (Luke Latham), [Махер Джендуби](https://twitter.com/maherjend) (Maher JENDOUBI), [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Скотт Собер](https://twitter.com/scottsauber) (Scott Sauber).

Частичное представление — это файл разметки [Razor](xref:mvc/views/razor) (*.cshtml*), отображающий выходные данные HTML *внутри* выходных данных другого файла разметки.

::: moniker range=">= aspnetcore-2.1"

Термин *частичное представление* используется при разработке приложения MVC, в котором файлы разметки именуются *представлениями*, или приложения Razor Pages, в котором файлы разметки именуются *страницами*. В этой статье все представления MVC и страницы Razor Pages будут называться *файлами разметки*.

::: moniker-end

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="when-to-use-partial-views"></a>Когда следует использовать частичные представления

Частичные представления позволяют эффективно выполнять следующие задачи:

* Разбить большие файлы разметки на мелкие компоненты.

  Если используется крупный и сложный файл разметки, состоящий из нескольких логических частей, будет удобнее работать с этими частями как с отдельными частичными представлениями. Код в файле разметки сократится до разумного размера и будет содержать только общую структуру страницы и ссылки на частичные представления.
* Сократить дублирование элементов разметки в разных файлах разметки.

  Если во многих файлах разметки используются одинаковые элементы, частичное представление переносит такое дублируемое содержимого в отдельный файл частичного представления. Так, когда частичное представление изменится, автоматически обновятся выводимые данные для всех файлов разметки, использующих это частичное представление.

Частичные представления не следует использовать для выделения стандартных элементов макета. Повторяющиеся элементы макета следует определять в файле [_Layout.cshtml](xref:mvc/views/layout).

Не используйте частичное представление там, где требуется сложная логика визуализации или выполнение кода для визуализации разметки. В этой ситуации лучше применить [компонент представления](xref:mvc/views/view-components).

## <a name="declare-partial-views"></a>Объявление частичных представлений

::: moniker range=">= aspnetcore-2.0"

Частичное представление — это файл разметки *.cshtml*, размещенный в папке *Views* (в модели MVC) или *Pages* (в модели Razor Pages).

В модели ASP.NET Core MVC элемент контроллера <xref:Microsoft.AspNetCore.Mvc.ViewResult> может возвращать представление или частичное представление. Аналогичная возможность будет добавлена для Razor Pages в ASP.NET Core 2.2. В Razor Pages <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> может возвращать <xref:Microsoft.AspNetCore.Mvc.PartialViewResult>. См. дополнительные сведения о [создании ссылок на частичные представления и их отображении](#reference-a-partial-view).

В отличие от представления MVC и отображения страниц, частичное представление не выполняет файл *_ViewStart.cshtml*. Дополнительные сведения о файле *_ViewStart.cshtml*, см. здесь: <xref:mvc/views/layout>.

Имена файлов частичного представления обычно начинаются с символа подчеркивания (`_`). Это соглашение об именовании не является обязательным требованием, но помогает отличать частичные представления от обычных представлений и страниц.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Частичное представление — это файл разметки *.cshtml*, размещенный в папке *Views*.

Элемент контроллера <xref:Microsoft.AspNetCore.Mvc.ViewResult> может возвращать представление или частичное представление.

В отличие от представления MVC, частичное представление не выполняет файл *_ViewStart.cshtml*. Дополнительные сведения о файле *_ViewStart.cshtml*, см. здесь: <xref:mvc/views/layout>.

Имена файлов частичного представления обычно начинаются с символа подчеркивания (`_`). Это соглашение об именовании не является обязательным требованием, но помогает отличать частичные представления от обычных представлений.

::: moniker-end

## <a name="reference-a-partial-view"></a>Ссылка на частичное представление

::: moniker range=">= aspnetcore-2.1"

В файле разметки частичное представление может указываться несколькими способами. Мы рекомендуем использовать в приложениях один из следующих методов асинхронного отображения:

* [Вспомогательная функция тега частичного представления](#partial-tag-helper)
* [Асинхронное вспомогательное приложение HTML](#asynchronous-html-helper)

::: moniker-end

::: moniker range="< aspnetcore-2.1"

В файле разметки частичное представление может указываться двумя способами.

* [Асинхронное вспомогательное приложение HTML](#asynchronous-html-helper)
* [Синхронное вспомогательное приложение HTML](#synchronous-html-helper)

Мы рекомендуем использовать в приложениях [асинхронное вспомогательное приложение HTML](#asynchronous-html-helper).

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a>Вспомогательная функция тега частичного представления

Для [вспомогательной функции тега частичного представления](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper) требуется ASP.NET Core 2.1 или более поздней версии.

Вспомогательная функция тега частичного представления синхронно отображает содержимое, используя близкий к HTML синтаксис:

```cshtml
<partial name="_PartialName" />
```

Если присутствует расширение файла, вспомогательная функция тега ссылается на частичное представление, которое необходимо разместить в той же папке, что и вызывающий его файл разметки:

```cshtml
<partial name="_PartialName.cshtml" />
```

В следующем примере есть ссылка на частичное представление из корня приложения. Пути, начинающиеся с тильды и косой черты (`~/`) или с косой черты (`/`), используют корневой каталог приложения:

**Razor Pages**

```cshtml
<partial name="~/Pages/Folder/_PartialName.cshtml" />
<partial name="/Pages/Folder/_PartialName.cshtml" />
```

**MVC**

```cshtml
<partial name="~/Views/Folder/_PartialName.cshtml" />
<partial name="/Views/Folder/_PartialName.cshtml" />
```

В следующем примере есть ссылка на частичное представление с относительным путем.

```cshtml
<partial name="../Account/_PartialName.cshtml" />
```

Дополнительные сведения см. в разделе <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>.

::: moniker-end

### <a name="asynchronous-html-helper"></a>Асинхронный вспомогательный метод HTML

Если вы используете вспомогательное приложение HTML, мы рекомендуем использовать <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*>. `PartialAsync` возвращает тип <xref:Microsoft.AspNetCore.Html.IHtmlContent> в оболочке <xref:System.Threading.Tasks.Task`1>. Для указания метода имя ожидающего вызова дополняется префиксом `@`.

```cshtml
@await Html.PartialAsync("_PartialName")
```

Если присутствует расширение файла, вспомогательная функция HTML ссылается на частичное представление, которое необходимо разместить в той же папке, что и вызывающий его файл разметки:

```cshtml
@await Html.PartialAsync("_PartialName.cshtml")
```

В следующем примере есть ссылка на частичное представление из корня приложения. Пути, начинающиеся с тильды и косой черты (`~/`) или с косой черты (`/`), используют корневой каталог приложения:

::: moniker range=">= aspnetcore-2.1"

**Razor Pages**

```cshtml
@await Html.PartialAsync("~/Pages/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Pages/Folder/_PartialName.cshtml")
```

**MVC**

::: moniker-end

```cshtml
@await Html.PartialAsync("~/Views/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Views/Folder/_PartialName.cshtml")
```

В следующем примере есть ссылка на частичное представление с относительным путем.

```cshtml
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

Вы также можете выполнить преобразование для просмотра частичного представления с помощью <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*>. Этот метод не возвращает <xref:Microsoft.AspNetCore.Html.IHtmlContent>. Он передает выводимые данные непосредственно в ответ в потоковом режиме. Так как этот метод не возвращает результат, его необходимо вызывать в блоке кода Razor.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

Так как `RenderPartialAsync` выполняет потоковую передачу отображаемого содержимого, его производительность в некоторых сценариях выше. В системах критической важности следует замерить время отображения страницы при использовании двух подходов и использовать тот из них, который создает ответ быстрее.

### <a name="synchronous-html-helper"></a>Синхронный вспомогательный метод HTML

<xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> и <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*> — это синхронные эквиваленты `PartialAsync` и `RenderPartialAsync` соответственно. Мы не рекомендуем использовать синхронные эквиваленты, так как в некоторых случаях они приводят к взаимоблокировке. Синхронные методы будут удалены в будущем выпуске.

> [!IMPORTANT]
> Если вам нужно выполнять код, используйте [компонент представления](xref:mvc/views/view-components) вместо частичного представления.

::: moniker range=">= aspnetcore-2.1"

Вызов `Partial` или `RenderPartial` генерирует предупреждение анализатора Visual Studio. Например, наличие `Partial` приведет к появлению такого сообщения:

> Использование IHtmlHelper.Partial может привести к взаимоблокировкам приложения. Попробуйте использовать &lt;частичное&gt; вспомогательное приложение тега или IHtmlHelper.PartialAsync.

Вместо вызовов `@Html.Partial` используйте `@await Html.PartialAsync` или [вспомогательное приложение тега частичного представления](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper). Дополнительные сведения о переносе вспомогательной функции тега частичного представления см. в разделе [Перенос из вспомогательного метода HTML](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper).

::: moniker-end

## <a name="partial-view-discovery"></a>Обнаружение частичного представления

Если ссылка на частичное представление указывает только имя файла, без расширения, просматриваются следующие расположения в указанном порядке:

::: moniker range=">= aspnetcore-2.1"

**Razor Pages**

1. папка текущей выполняемой страницы;
1. граф каталога на уровень выше папки страницы.
1. `/Shared`
1. `/Pages/Shared`
1. `/Views/Shared`

**MVC**

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`
1. `/Pages/Shared`

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`

::: moniker-end

К обнаружению частичного представления применяются следующие соглашения:

* допускается использовать разные частичные представления с одним именем файла, если они расположены в разных папках;
* если ссылка на частичное представление содержит имя файла без расширения, а частичные представления с таким именем одновременно присутствуют в папке вызывающего объекта и в папке *Shared*, используется частичное представление из папки вызывающего объекта. Если нужное частичное представление отсутствует в папке вызывающего объекта, используется частичное представление из папки *Shared*. Частичных представления в папке *Shared* именуются *общие частичные представления* или *частичные представления по умолчанию*.
* Частичные представления можно вызывать *по цепочке*&mdash;одно частичное представление можно вызвать другое частичное представление, если при этом не создается циклических ссылок. Относительные пути всегда указываются относительно расположения текущего файла, но не корневого или родительского каталога.

> [!NOTE]
> Объект [Razor](xref:mvc/views/razor) `section`, определенный в частичном представлении, невидим для родительских файлов разметки. Объект `section` видим только для частичного представления, в котором он определен.

## <a name="access-data-from-partial-views"></a>Доступ к данным из частичных представлений

Когда создается экземпляр частичного представления, он получает *копию* словаря `ViewData` из родительского представления. Изменения, вносимые в данные в частичном представлении, не сохраняются в родительском представлении. Изменения объекта `ViewData` в частичном представлении утрачиваются при возврате этого представления.

В следующем примере показано, как передать экземпляр [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) в частичное представление:

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

В частичное представление можно передать модель. Модель может являться пользовательским объектом. Модель можно передать с помощью `PartialAsync` (передает блок содержимого вызывающему объекту) или `RenderPartialAsync` (выполняет потоковую передачу содержимого в выходные данные):

```cshtml
@await Html.PartialAsync("_PartialName", model)
```

::: moniker range=">= aspnetcore-2.1"

**Razor Pages**

Следующая разметка для примера приложения взята со страницы *Pages/ArticlesRP/ReadRP.cshtml*. Эта страница содержит два частичных представления. Второе частичное представление передает модель и объект `ViewData` в первое частичное представление. Используйте перегрузку конструктора `ViewDataDictionary`, чтобы передать новый словарь `ViewData` и при этом сохранить существующий словарь `ViewData`.

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/ReadRP.cshtml?name=snippet_ReadPartialViewRP&highlight=5,15-19)]

*Pages/Shared/_AuthorPartialRP.cshtml* — это первое частичное представление, указанное в файле разметки *ReadRP.cshtml*:

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/Shared/_AuthorPartialRP.cshtml)]

*Pages/ArticlesRP/_ArticleSectionRP.cshtml* — это второе частичное представление, указанное в файле разметки *ReadRP.cshtml*:

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/_ArticleSectionRP.cshtml)]

**MVC**

::: moniker-end

В приведенной ниже разметке для примера приложения показано представление *Views/Articles/Read.cshtml*. Это представление содержит два частичных представления. Второе частичное представление передает модель и объект `ViewData` в первое частичное представление. Используйте перегрузку конструктора `ViewDataDictionary`, чтобы передать новый словарь `ViewData` и при этом сохранить существующий словарь `ViewData`.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=5,15-19)]

*Views/Shared/_AuthorPartialRP.cshtml* — это первое частичное представление, указанное в файле разметки *Read.cshtml*:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

*Views/Shared/_ArticleSection.cshtml* — это второе частичное представление, указанное в файле разметки *Read.cshtml*:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

Во время выполнения частичные представления встраиваются в выходные данные родительского представления, которое также преобразовывается для просмотра в общем макете *_Layout.cshtml*. Первое частичное представление отображает имя автора статьи и дату публикации:

> Abraham Lincoln
>
> Это частичное представление из &lt;общего каталога файлов частичного представления&gt;.
> 11/19/1863 12:00:00 AM

Второе частичное представление отображает разделы статьи:

> Раздел один индекс: 0
>
> Four score and seven years ago...
>
> Индекс раздела: 1
>
> Now we are engaged in a great civil war, testing...
>
> Индекс в разделе 3: 2
>
> But, in a larger sense, we can not dedicate...

## <a name="additional-resources"></a>Дополнительные ресурсы

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end
