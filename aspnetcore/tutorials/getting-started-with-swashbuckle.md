---
title: Начало работы с Swashbuckle и ASP.NET Core
author: zuckerthoben
description: Дополнительные сведения о добавлении Swashbuckle в проект веб-API ASP.NET Core для интеграции пользовательского интерфейса Swagger.
ms.author: scaddie
ms.custom: mvc
ms.date: 02/06/2019
uid: tutorials/get-started-with-swashbuckle
ms.openlocfilehash: 9239a46889691135dce5c99f8fc9b8c7b38ab457
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043941"
---
# <a name="get-started-with-swashbuckle-and-aspnet-core"></a>Начало работы с Swashbuckle и ASP.NET Core

Авторы: [Шейн Бойер](https://twitter.com/spboyer) (Shayne Boyer) и [Скотт Эдди](https://twitter.com/Scott_Addie) (Scott Addie)

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/) ([как скачивать](xref:index#how-to-download-a-sample))

Swashbuckle включает три основных компонента.

* [Swashbuckle.AspNetCore.Swagger](https://www.nuget.org/packages/Swashbuckle.AspNetCore.Swagger/): объектная модель Swagger и ПО промежуточного слоя для предоставления объектов `SwaggerDocument` как конечных точек JSON.

* [Swashbuckle.AspNetCore.SwaggerGen](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerGen/): генератор Swagger, создающий объекты `SwaggerDocument` непосредственно из ваших маршрутов, контроллеров и моделей. Как правило, он комбинируется с ПО промежуточного слоя конечной точки Swagger и за счет этого предоставляет Swagger JSON автоматически.

* [Swashbuckle.AspNetCore.SwaggerUI](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerUI/): встроенная версия средства пользовательского интерфейса Swagger. Она интерпретирует Swagger JSON и обеспечивает удобную настраиваемую среду для описания функциональности веб-API. Включает встроенные окружения тестов для открытых методов.

## <a name="package-installation"></a>Установка пакета

Swashbuckle можно добавить одним из описанных ниже способов.

### <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* В окне **Консоль диспетчера пакетов**
  * Перейдите в раздел **Представление** > **Другие окна** > **Консоль диспетчера пакетов**
  * Перейдите в каталог, в котором существует файл *TodoApi.csproj*
  * Выполните следующую команду:

    ```powershell
    Install-Package Swashbuckle.AspNetCore
    ```

* В диалоговом окне **Управление пакетами NuGet**
  * Щелкните правой кнопкой мыши проект в **обозревателе решений** > **Управление пакетами NuGet**
  * В качестве **источника пакета** выберите "nuget.org".
  * В поле поиска введите "Swashbuckle.AspNetCore".
  * Выберите пакет "Swashbuckle.AspNetCore" на вкладке **Обзор** и нажмите кнопку **Установить**.

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio для Mac](#tab/visual-studio-mac)

* Щелкните правой кнопкой мыши папку *Пакеты* на **панели решения** > **Добавление пакетов...**.
* В раскрывающемся списке **Источник** в окне **Добавление пакетов** выберите вариант "nuget.org".
* В поле поиска введите "Swashbuckle.AspNetCore".
* В области результатов выберите пакет Swashbuckle.AspNetCore и нажмите кнопку **Добавить пакет**

### <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code.](#tab/visual-studio-code)

Во **встроенном терминале** выполните следующую команду.

```console
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

Выполните следующую команду:

```console
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a>Добавление и настройка ПО промежуточного слоя Swagger

Добавьте генератор Swagger в коллекцию служб в методе `Startup.ConfigureServices`:

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=8-11)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=9-12)]

::: moniker-end

Импортируйте следующие пространства имен для использования в классе `Info`:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_InfoClassNamespace)]

В методе `Startup.Configure` включите ПО промежуточного слоя для обслуживания созданного документа JSON и пользовательского интерфейса Swagger:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_Configure&highlight=4,8-11)]

Предыдущий вызов метода `UseSwaggerUI` включает [ПО промежуточного слоя для статических файлов](xref:fundamentals/static-files). Если код предназначен для .NET Framework или NET Core 1.x, добавьте в проект пакет NuGet [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/).

Запустите приложение и перейдите к файлу `http://localhost:<port>/swagger/v1/swagger.json`. Появится созданный документ, описывающий конечные точки, как показано в [спецификации Swagger (swagger.json)](xref:tutorials/web-api-help-pages-using-swagger#swagger-specification-swaggerjson).

Пользовательский интерфейс Swagger можно найти по адресу `http://localhost:<port>/swagger`. Изучите API через пользовательский интерфейс Swagger и включите его в другие программы.

> [!TIP]
> Чтобы предоставить пользовательский интерфейс Swagger в корневом каталоге приложения (`http://localhost:<port>/`), установите для свойства `RoutePrefix` пустую строку:
>
> [!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup3.cs?name=snippet_UseSwaggerUI&highlight=4)]

Если вы используете каталоги в службах IIS или на обратном прокси-сервере, задайте для конечной точки Swagger относительный путь с помощью префикса `./`. Например, `./swagger/v1/swagger.json`. `/swagger/v1/swagger.json` указывает, что приложение должно искать JSON-файл в реальном корне URL-адреса (с префиксом маршрута, если он используется). Например, используйте `http://localhost:<port>/<route_prefix>/swagger/v1/swagger.json` вместо `http://localhost:<port>/<virtual_directory>/<route_prefix>/swagger/v1/swagger.json`.

## <a name="customize-and-extend"></a>Настройка и расширение

Swagger предоставляет параметры для документирования объектной модели и настройки пользовательского интерфейса в соответствии с вашим фирменным стилем.

### <a name="api-info-and-description"></a>Данные и описание API

Действие по настройке, передаваемое в метод `AddSwaggerGen`, можно использовать для добавления таких сведений, как автор, лицензия и описание:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup4.cs?name=snippet_AddSwaggerGen)]

Пользовательский интерфейс Swagger отображает сведения о версии:

![Пользовательский интерфейс Swagger с данными версии: описание, автор и ссылка на дополнительные сведения](web-api-help-pages-using-swagger/_static/custom-info.png)

### <a name="xml-comments"></a>XML-комментарии

XML-комментарии можно включить следующим образом.

#### <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

::: moniker range=">= aspnetcore-2.0"

* В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите команду **Изменить <имя_проекта>.csproj**.
* Вручную добавьте выделенные строки в файл *.csproj*:

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Свойства**.
* Установите флажок **Файл XML-документации** в разделе **Вывод** на вкладке **Сборка**.

::: moniker-end

#### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio для Mac](#tab/visual-studio-mac)

::: moniker range=">= aspnetcore-2.0"

* В *панели решения* нажмите **Управление** и выберите имя проекта. Перейдите в раздел **Сервис** > **Изменить файл**.
* Вручную добавьте выделенные строки в файл *.csproj*:

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* Откройте диалоговое окно **Параметры проекта** > **Сборка** > **Компилятор**
* Установите флажок **Сформировать XML-документацию** в разделе **Общие параметры**

::: moniker-end

#### <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code.](#tab/visual-studio-code)

Вручную добавьте выделенные строки в файл *.csproj*:

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=1-2,4)]

::: moniker-end

#### <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

Вручную добавьте выделенные строки в файл *.csproj*:

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=1-2,4)]

::: moniker-end

---

Включение комментариев XML предоставляет отладочную информацию для недокументированных открытых типов и членов. Недокументированные типы и члены указываются в предупреждающем сообщении. Например, следующее сообщение оповещает о нарушении кода предупреждения 1591:

```text
warning CS1591: Missing XML comment for publicly visible type or member 'TodoController.GetAll()'
```

Чтобы отключить предупреждения на уровне всего проекта, определите разделенный точками с запятой список игнорируемых кодов предупреждений в файле проекта. Добавление кодов предупреждений в `$(NoWarn);` также применяется к [значениям C# по умолчанию](https://github.com/dotnet/sdk/blob/2eb6c546931b5bcb92cd3128b93932a980553ea1/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.Sdk.CSharp.props#L16).

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=3)]

::: moniker-end

Чтобы отключить предупреждения только для определенных элементов, поместите код в директивы препроцессора [#pragma warning](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning). Этот подход полезен, если код не должен быть доступен в документации API. В приведенном ниже примере код предупреждения CS1591 игнорируется для всего класса `Program`. Применение кода предупреждения можно восстановить в конце определения класса. Укажите несколько кодов предупреждений в списке, разделив их запятыми.

```csharp
namespace TodoApi
{
#pragma warning disable CS1591
    public class Program
    {
        public static void Main(string[] args) =>
            BuildWebHost(args).Run();

        public static IWebHost BuildWebHost(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseStartup<Startup>()
                .Build();
    }
#pragma warning restore CS1591
}
```

Настройте Swagger на использование созданного XML-файла. В Linux и других операционных системах, отличных от Windows, имена и пути файлов могут быть чувствительны к регистру. Например, файл *ToDoApi.XML* допустим в Windows, но не в CentOS.

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=31-33)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=30-32)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup1x.cs?name=snippet_ConfigureServices&highlight=30-32)]

::: moniker-end

В приведенном выше коде для создания имени XML-файла, соответствующего имени проекта веб-API, используется [отражение](/dotnet/csharp/programming-guide/concepts/reflection). Свойство [AppContext.BaseDirectory](xref:System.AppContext.BaseDirectory*) используется для построения пути к XML-файлу.

Включение в действие комментариев с тройной косой чертой улучшает пользовательский интерфейс Swagger, так как позволяет добавить описание к заголовку раздела. Добавьте элемент [\<summary>](/dotnet/csharp/programming-guide/xmldoc/summary) над действием `Delete`:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Delete&highlight=1-3)]

Пользовательский интерфейс Swagger отображает внутренний текст элемента `<summary>` в приведенном выше коде:

![Пользовательский интерфейс Swagger с XML-комментарием "Удаляет указанный элемент TodoItem" для метода DELETE](web-api-help-pages-using-swagger/_static/triple-slash-comments.png)

Пользовательский интерфейс определяется созданной схемой JSON:

```json
"delete": {
    "tags": [
        "Todo"
    ],
    "summary": "Deletes a specific TodoItem.",
    "operationId": "ApiTodoByIdDelete",
    "consumes": [],
    "produces": [],
    "parameters": [
        {
            "name": "id",
            "in": "path",
            "description": "",
            "required": true,
            "type": "integer",
            "format": "int64"
        }
    ],
    "responses": {
        "200": {
            "description": "Success"
        }
    }
}
```

Добавьте элемент [\<remarks>](/dotnet/csharp/programming-guide/xmldoc/remarks) в документацию по методу действия `Create`. Он дополняет сведения, указанные в элементе `<summary>`, и предоставляет более надежный пользовательский интерфейс Swagger. Содержимое элемента `<remarks>` может включать текст, JSON или XML.

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]

::: moniker-end

Обратите внимание, как эти дополнительные комментарии улучшают пользовательский интерфейс:

![Пользовательский интерфейс Swagger с показанными дополнительными комментариями](web-api-help-pages-using-swagger/_static/xml-comments-extended.png)

### <a name="data-annotations"></a>Заметки к данным

Дополните модель атрибутами из пространства имен [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations), чтобы обеспечить компоненты пользовательского интерфейса Swagger.

Добавьте атрибут `[Required]` к свойству `Name` класса `TodoItem`.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Models/TodoItem.cs?highlight=10)]

Наличие этого атрибута изменяет поведение пользовательского интерфейса и схему базового JSON.

```json
"definitions": {
    "TodoItem": {
        "required": [
            "name"
        ],
        "type": "object",
        "properties": {
            "id": {
                "format": "int64",
                "type": "integer"
            },
            "name": {
                "type": "string"
            },
            "isComplete": {
                "default": false,
                "type": "boolean"
            }
        }
    }
},
```

Добавьте к контроллеру API атрибут `[Produces("application/json")]`. Он позволяет объявить, что действия контроллера поддерживают тип содержимого ответа *application/json*:

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]

::: moniker-end

В раскрывающемся списке **Тип содержимого ответа** этот тип содержимого выбирается по умолчанию для операций контроллера GET.

![Пользовательский интерфейс Swagger с типом содержимого ответа по умолчанию](web-api-help-pages-using-swagger/_static/json-response-content-type.png)

Чем больше заметок к данным используется в веб-API, тем более содержательными и полезными становятся пользовательский интерфейс и страницы справки по API.

### <a name="describe-response-types"></a>Описание типов ответов

Разработчиков, использующих веб-API, в первую очередь, волнуют возвращаемые данные &mdash; а именно: типы ответов и коды ошибок (если они не стандартны). Типы ответов и коды ошибок обозначаются в комментариях к XML и заметках к данным.

Действие `Create` в случае успеха возвращает код состояния HTTP 201. Код состояния HTTP 400 возвращается в том случае, когда текст отправленного запроса имеет значение NULL. Без надлежащей документации в пользовательском интерфейсе Swagger пользователь не будет знать, чего ожидать. Эту проблему решает добавление строк, выделенных в следующем примере:

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]

::: moniker-end

Теперь пользовательский интерфейс Swagger четко документирует ожидаемые коды HTTP-ответов.

![Пользовательский интерфейс Swagger, показывающий описание класса ответа POST "Возвращает вновь созданный элемент Todo" и "400 — Если элемент имеет значение NULL" для кода состояния и причины в разделе "Сообщения ответов"](web-api-help-pages-using-swagger/_static/data-annotations-response-types.png)

::: moniker range=">= aspnetcore-2.2"

В ASP.NET Core 2.2 или более поздней версии соглашения можно использовать в качестве альтернативы явному добавлению к отдельным действиям элемента `[ProducesResponseType]`. Дополнительные сведения см. в разделе <xref:web-api/advanced/conventions>.

::: moniker-end

### <a name="customize-the-ui"></a>Настройка пользовательского интерфейса

Готовый пользовательский интерфейс отличается функциональностью и презентабельностью. Но на страницах документации по API должна быть представлена ваша фирменная символика или тема. Для оформления компонентов Swashbuckle в фирменном стиле необходимо добавить ресурсы для обслуживания статических файлов, а затем построить структуру папок для их размещения.

Если код предназначен для .NET Framework или NET Core 1.x, добавьте в проект пакет NuGet [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles):

```xml
<PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="2.0.0" />
```

Предыдущий пакет NuGet уже установлен, если код предназначен для .NET Core 2.x и используется [метапакет](xref:fundamentals/metapackage).

Включите ПО промежуточного слоя для статических файлов:

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_Configure&highlight=3)]

Получите содержимое папки *dist* из [репозитория GitHub пользовательского интерфейса Swagger](https://github.com/swagger-api/swagger-ui/tree/master/dist). Эта папка содержит ресурсы, необходимые для страниц пользовательского интерфейса Swagger.

Создайте папку *wwwroot/swagger/ui* и скопируйте в нее содержимое папки *dist*.

Создайте файл *custom.css* в *wwwroot/swagger/ui* со следующим CSS для настройки заголовка страницы:

[!code-css[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/wwwroot/swagger/ui/custom.css)]

Сошлитесь на файл *custom.css* в файле *index.html* после других файлов CSS:

[!code-html[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/wwwroot/swagger/ui/index.html?name=snippet_SwaggerUiCss&highlight=3)]

Перейдите на страницу *index.html* в `http://localhost:<port>/swagger/ui/index.html`. Введите `http://localhost:<port>/swagger/v1/swagger.json` в текстовое поле заголовка и нажмите кнопку **Проводник**. Полученная в итоге страница будет выглядеть следующим образом.

![Пользовательский интерфейс Swagger с настроенным заголовком](web-api-help-pages-using-swagger/_static/custom-header.png)

С этой страницей можно сделать гораздо больше. Все возможности ресурсов пользовательского интерфейса см. в статье о [репозитории GitHub пользовательского интерфейса Swagger](https://github.com/swagger-api/swagger-ui).
