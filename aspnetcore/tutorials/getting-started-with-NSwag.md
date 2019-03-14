---
title: Начало работы с NSwag и ASP.NET Core
author: zuckerthoben
description: Узнайте, как использовать NSwag для создания документации и страниц справки для веб-API в ASP.NET Core.
ms.author: scaddie
ms.custom: mvc
ms.date: 12/30/2018
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: c03e7513edc3240f3f13f0c190e1ca9480e476af
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037771"
---
# <a name="get-started-with-nswag-and-aspnet-core"></a>Начало работы с NSwag и ASP.NET Core

Авторы: [Кристоф Ниенабер (Christoph Nienaber)](https://twitter.com/zuckerthoben), [Рико Сутер (Rico Suter)](https://rsuter.com) и [Дейв Брок (Dave Brock)](https://twitter.com/daveabrock)

::: moniker range=">= aspnetcore-2.1"

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag) ([как скачивать](xref:index#how-to-download-a-sample))

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag) ([как скачивать](xref:index#how-to-download-a-sample))

::: moniker-end

NSwag обеспечивает следующие возможности:

 * Работу с пользовательским интерфейсом Swagger и генератором Swagger.
 * Создание гибкого кода.

С NSwag отпадает необходимость в существующем API &mdash; вы можете использовать сторонние API, которые содержат Swagger и создают реализацию клиента. NSwag позволяет ускорить цикл разработки и легко адаптироваться к изменениям API.

## <a name="register-the-nswag-middleware"></a>Регистрация ПО промежуточного слоя NSwag

Зарегистрируйте ПО промежуточного слоя NSwag, чтобы выполнять следующие задачи:

 * создавать спецификации Swagger для реализованного веб-API;
 * применять пользовательский интерфейс Swagger для просмотра и тестирования веб-API.

Чтобы использовать ПО промежуточного слоя [NSwag](https://github.com/RSuter/NSwag) для ASP.NET Core, установите пакет NuGet [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/). Этот пакет содержит ПО промежуточного слоя, которое позволяет создавать и использовать спецификацию Swagger, пользовательский интерфейс Swagger (версий 2 и 3) и [пользовательский интерфейс ReDoc](https://github.com/Rebilly/ReDoc).

Чтобы установить пакет NuGet NSwag, воспользуйтесь одним из следующих способов.

### <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* В окне **Консоль диспетчера пакетов**
  * Перейдите в раздел **Представление** > **Другие окна** > **Консоль диспетчера пакетов**
  * Перейдите в каталог, в котором существует файл *TodoApi.csproj*
  * Выполните следующую команду:

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* В диалоговом окне **Управление пакетами NuGet**
  * Щелкните правой кнопкой мыши проект в **обозревателе решений** > **Управление пакетами NuGet**
  * В качестве **источника пакета** выберите "nuget.org".
  * В поле поиска введите "NSwag.AspNetCore"
  * Выберите пакет "NSwag.AspNetCore" на вкладке **Обзор** и нажмите **Установить**

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio для Mac](#tab/visual-studio-mac)

* Щелкните правой кнопкой мыши папку *Пакеты* на **панели решения** > **Добавление пакетов...**.
* В раскрывающемся списке **Источник** в окне **Добавление пакетов** выберите вариант "nuget.org".
* В поле поиска введите "NSwag.AspNetCore"
* В области результатов выберите пакет "NSwag.AspNetCore" и нажмите **Добавить пакет**

### <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code.](#tab/visual-studio-code)

Во **встроенном терминале** выполните следующую команду.

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

Выполните следующую команду:

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a>Добавление и настройка ПО промежуточного слоя Swagger

 Добавьте Swagger в приложение ASP.NET Core и настройте это ПО промежуточного слоя, выполнив следующие действия в классе `Startup`:

* Импортируйте такие пространства имен:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_StartupConfigureImports)]

* Используя метод `ConfigureServices`, зарегистрируйте необходимые службы Swagger:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_ConfigureServices&highlight=8)]

 * В методе `Configure` включите ПО промежуточного слоя для обслуживания созданной спецификации Swagger и пользовательского интерфейса Swagger:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=6-7)]

 * Запустите приложение. Перейдите к:
   * `http://localhost:<port>/swagger` для просмотра пользовательского интерфейса Swagger.
   * `http://localhost:<port>/swagger/v1/swagger.json` для просмотра спецификации Swagger.

## <a name="code-generation"></a>Создание кода

Можно воспользоваться преимуществами создания кода в NSwag, выбрав один из следующих вариантов:

 * [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio) — это классическое приложение Windows для создания клиентского кода API на C# или TypeScript.
 * Пакеты NuGet [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) или [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) для создания кода внутри проекта.
* NSwag из [командной строки](https://github.com/NSwag/NSwag/wiki/CommandLine).
 * Пакет NuGet [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild).


### <a name="generate-code-with-nswagstudio"></a>Создание кода с помощью NSwagStudio

* Установите NSwagStudio, следуя инструкциям из [репозитория NSwagStudio на веб-сайте GitHub](https://github.com/RSuter/NSwag/wiki/NSwagStudio).
 * Запустите NSwagStudio и введите URL-адрес файла *swagger.json* в текстовое поле **Swagger Specification URL** (URL-адрес спецификации Swagger). Например, *http://localhost:44354/swagger/v1/swagger.json*.
* Нажмите кнопку **Create local Copy** (Создать локальную копию), чтобы создать представление JSON своей спецификации Swagger.

  ![Создание локальной копии спецификация Swagger](web-api-help-pages-using-swagger/_static/CreateLocalCopy-NSwagStudio.PNG)

 * В области **Outputs** (Выходные данные) установите флажок **CSharp Client** (Клиент CSharp). В зависимости от проекта вы также можете выбрать **TypeScript Client** (Клиент TypeScript) или **CSharp Web API Controller** (Контроллер веб-API CSharp). Если выбрать **CSharp Web API Controller** (Контроллер веб-API CSharp), служба будет перестроена по спецификации посредством обратного создания.
* Щелкните **Generate Outputs** (Создать выходные данные), чтобы создать полную клиентскую реализацию проекта *TodoApi.NSwag* на языке C#. Откройте вкладку **CSharp Client** (Клиент CSharp), чтобы просмотреть созданный клиентский код.

```csharp
//----------------------
// <auto-generated>
//     Generated using the NSwag toolchain v12.0.9.0 (NJsonSchema v9.13.10.0 (Newtonsoft.Json v11.0.0.0)) (http://NSwag.org)
// </auto-generated>
//----------------------

namespace MyNamespace
{
    #pragma warning disable

    [System.CodeDom.Compiler.GeneratedCode("NSwag", "12.0.9.0 (NJsonSchema v9.13.10.0 (Newtonsoft.Json v11.0.0.0))")]
    public partial class TodoClient 
    {
        private string _baseUrl = "https://localhost:44354";
        private System.Net.Http.HttpClient _httpClient;
        private System.Lazy<Newtonsoft.Json.JsonSerializerSettings> _settings;
    
        public TodoClient(System.Net.Http.HttpClient httpClient)
        {
            _httpClient = httpClient; 
            _settings = new System.Lazy<Newtonsoft.Json.JsonSerializerSettings>(() => 
            {
                var settings = new Newtonsoft.Json.JsonSerializerSettings();
                UpdateJsonSerializerSettings(settings);
                return settings;
            });
        }
    
        public string BaseUrl 
        {
            get { return _baseUrl; }
            set { _baseUrl = value; }
        }

        // code omitted for brevity
```

> [!TIP]
 > Клиентский код на C# создается на основе выбранных параметров на вкладке **Settings** (Параметры). Измените параметры для выполнения таких задач, как переименование пространства имен по умолчанию и создание синхронного метода.

 * Скопируйте созданный код на C# в файл в проекте клиента, который будет использовать API.
* Начните использовать веб-API:

```csharp
 var todoClient = new TodoClient();

// Gets all to-dos from the API
 var allTodos = await todoClient.GetAllAsync();

 // Create a new TodoItem, and save it via the API.
var createdTodo = await todoClient.CreateAsync(new TodoItem());

// Get a single to-do by ID
var foundTodo = await todoClient.GetByIdAsync(1);
```

## <a name="customize-api-documentation"></a>Настройка документирования для API

Swagger предоставляет параметры для документирования объектной модели и упрощения использования веб-API.

### <a name="api-info-and-description"></a>Данные и описание API

В методе `Startup.ConfigureServices` действие по настройке, передаваемое в метод `AddSwaggerDocument`, можно использовать для добавления таких сведений, как автор, лицензия и описание:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup2.cs?name=snippet_AddSwaggerDocument)]

Пользовательский интерфейс Swagger отображает сведения о версии:

![Пользовательский интерфейс Swagger с информацией о версии](web-api-help-pages-using-swagger/_static/custom-info-nswag.png)

### <a name="xml-comments"></a>XML-комментарии

 Чтобы включить комментарии XML, выполните следующие действия:

# <a name="visual-studiotabvisual-studio-xml"></a>[Visual Studio](#tab/visual-studio-xml/)

::: moniker range=">= aspnetcore-2.0"

* В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите команду **Изменить <имя_проекта>.csproj**.
* Вручную добавьте выделенные строки в файл *.csproj*:

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Свойства**.
* Установите флажок **Файл XML-документации** в разделе **Вывод** на вкладке **Сборка**

::: moniker-end

# <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[Visual Studio для Mac](#tab/visual-studio-mac-xml/)

::: moniker range=">= aspnetcore-2.0"

* В *панели решения* нажмите **Управление** и выберите имя проекта. Перейдите в раздел **Сервис** > **Изменить файл**.
* Вручную добавьте выделенные строки в файл *.csproj*:

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* Откройте диалоговое окно **Параметры проекта** > **Сборка** > **Компилятор**
* Установите флажок **Сформировать XML-документацию** в разделе **Общие параметры**

::: moniker-end

# <a name="visual-studio-codetabvisual-studio-code-xml"></a>[Visual Studio Code.](#tab/visual-studio-code-xml/)

Вручную добавьте выделенные строки в файл *.csproj*:

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

---

### <a name="data-annotations"></a>Заметки к данным

::: moniker range="<= aspnetcore-2.0"

 Так как NSwag использует [отражение](/dotnet/csharp/programming-guide/concepts/reflection), а рекомендуемый тип возвращаемого значения для действий веб-API — это [IActionResult](xref:Microsoft.AspNetCore.Mvc.IActionResult), NSwag не может определить что выполняет ваше действие и что оно возвращает.

Рассмотрим следующий пример.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]

 Предыдущее действие возвращает `IActionResult`, но внутри действия возвращается [CreatedAtRoute](xref:System.Web.Http.ApiController.CreatedAtRoute*) или [BadRequest](xref:System.Web.Http.ApiController.BadRequest*). Используйте заметки к данным для сообщения клиентам о том, какие коды состояний HTTP возвращает это действие. Добавьте к действию следующие атрибуты:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

 Так как NSwag использует [отражение](/dotnet/csharp/programming-guide/concepts/reflection), а рекомендуемый тип возвращаемого значения для действий веб-API — это [IActionResult\<T >](xref:Microsoft.AspNetCore.Mvc.ActionResult`1), NSwag может определить только тип возвращаемого значения, задаваемый `T`. Невозможно автоматически определить другие возможные типы возвращаемого значения. 

Рассмотрим следующий пример.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]

Предыдущее действие возвращает `ActionResult<T>`. Внутри действия оно возвращает [CreatedAtRoute](xref:System.Web.Http.ApiController.CreatedAtRoute*). Поскольку контроллер дополнен атрибутом [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute), ответ [BadRequest](xref:System.Web.Http.ApiController.BadRequest*) также возможен. Дополнительные сведения см. в разделе [Автоматические отклики HTTP 400](xref:web-api/index#automatic-http-400-responses). Используйте заметки к данным для сообщения клиентам о том, какие коды состояний HTTP возвращает это действие. Добавьте к действию следующие атрибуты:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]

В ASP.NET Core 2.2 или более поздней версии можно использовать соглашения вместо явного добавления `[ProducesResponseType]` к отдельным действиям. Дополнительные сведения см. в разделе <xref:web-api/advanced/conventions>.

::: moniker-end

 Генератор Swagger теперь может точно описать это действие, и созданные клиенты знают, что они получают при вызове конечной точки. Рекомендуется добавлять эти атрибуты ко всем действиям. 

Рекомендации о том, какие ответы HTTP должны возвращать ваши действия API, см. в [спецификации RFC 7231](https://tools.ietf.org/html/rfc7231#section-4.3).
