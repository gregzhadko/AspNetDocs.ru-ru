---
title: Поставщики файлов в ASP.NET Core
author: guardrex
description: Сведения о том, как ASP.NET Core абстрагирует доступ к файловой системе с помощью поставщиков файлов.
ms.author: riande
ms.custom: mvc
ms.date: 08/01/2018
uid: fundamentals/file-providers
ms.openlocfilehash: 5d0d46ba82cd84e48e5a9b23d6d330d8888beb41
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042721"
---
# <a name="file-providers-in-aspnet-core"></a>Поставщики файлов в ASP.NET Core

Авторы: [Стив Смит](https://ardalis.com/) (Steve Smith) и [Люк Лэтем](https://github.com/guardrex) (Luke Latham)

ASP.NET Core абстрагирует доступ к файловой системе с помощью поставщиков файлов. В рамках платформы ASP.NET Core используются поставщики файлов.

* [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) предоставляет корневой каталог содержимого приложения и корневой каталог веб-сайта в виде типов `IFileProvider`.
* [ПО промежуточного слоя для статических файлов](xref:fundamentals/static-files) использует поставщики файлов для поиска статических файлов.
* [Razor](xref:mvc/views/razor) использует поставщики файлов для поиска страниц и представлений.
* Инструменты .NET Core используют поставщики файлов и стандартные маски, чтобы указать файлы для публикации.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/samples) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="file-provider-interfaces"></a>Интерфейсы поставщика файлов

Основным интерфейсом является [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider). `IFileProvider` предоставляет методы для следующих действий:

* получение сведений о файле ([IFileInfo](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo));
* получение сведений о каталоге ([IDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.idirectorycontents));
* настройка уведомлений об изменениях (с помощью [IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken));

`IFileInfo` предоставляет методы и свойства для работы с файлами:

* [Exists](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.exists) (существует);
* [IsDirectory](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.isdirectory) (является каталогом);
* [Name](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.name)
* [Length](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.length) (длина в байтах);
* [LastModified](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.lastmodified) (дата последнего изменения).

Данные из файла можно считывать с помощью метода [IFileInfo.CreateReadStream](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.createreadstream).

Пример приложения демонстрирует, как настроить в `Startup.ConfigureServices` поставщике файлов, чтобы использовать его в приложении путем [внедрения зависимостей](xref:fundamentals/dependency-injection).

## <a name="file-provider-implementations"></a>Реализации поставщиков файлов

Доступны три реализации `IFileProvider`.

::: moniker range=">= aspnetcore-2.0"

| Реализация | Описание: |
| -------------- | ----------- |
| [PhysicalFileProvider](#physicalfileprovider) | Физический поставщик используется для доступа к физическим файлам системы. |
| [ManifestEmbeddedFileProvider](#manifestembeddedfileprovider) | Поставщик внедренных манифестов используется для доступа к файлам, внедренным в сборки. |
| [CompositeFileProvider](#compositefileprovider) | Составной поставщик используется для предоставления комбинированного доступа к файлам и каталогам из одного или нескольких поставщиков. |

::: moniker-end

::: moniker range="< aspnetcore-2.0"

| Реализация | Описание: |
| -------------- | ----------- |
| [PhysicalFileProvider](#physicalfileprovider) | Физический поставщик используется для доступа к физическим файлам системы. |
| [EmbeddedFileProvider](#embeddedfileprovider) | Внедренный поставщик используется для доступа к файлам, внедренным в сборки. |
| [CompositeFileProvider](#compositefileprovider) | Составной поставщик используется для предоставления комбинированного доступа к файлам и каталогам из одного или нескольких поставщиков. |

::: moniker-end

### <a name="physicalfileprovider"></a>PhysicalFileProvider

[PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) предоставляет доступ к физической файловой системе. `PhysicalFileProvider` использует тип [System.IO.File](/dotnet/api/system.io.file) (для физического поставщика), устанавливая для всех путей область каталога и его дочерних элементов. Такая привязка к области защищает от доступа к файловой системе за пределами указанного каталога и его дочерних элементов. При создании экземпляра этого поставщика нужно указать путь к каталогу, который станет базовым путем для всех запросов, выполненных с помощью этого поставщика. Вы можете создать экземпляр поставщика `PhysicalFileProvider` напрямую или вызвать `IFileProvider` в конструкторе путем [внедрения зависимостей](xref:fundamentals/dependency-injection).

**Статические типы**

Следующий пример кода демонстрирует, как создать и использовать `PhysicalFileProvider` для получения содержимого каталога и сведений о файлах:

```csharp
var provider = new PhysicalFileProvider(applicationRoot);
var contents = provider.GetDirectoryContents(string.Empty);
var fileInfo = provider.GetFileInfo("wwwroot/js/site.js");
```

В предшествующем примере используются следующие типы:

* `provider` является `IFileProvider`.
* `contents` является `IDirectoryContents`.
* `fileInfo` является `IFileInfo`.

С помощью поставщика файлов вы можете выполнить итерацию по каталогу, указанному в параметре `applicationRoot`, или вызвать `GetFileInfo` для получения сведений о файлах. Поставщик файлов не имеет доступ к каталогам за пределами `applicationRoot`.

Этот пример приложения создает поставщик для приложения в классе `Startup.ConfigureServices`, используя [IHostingEnvironment.ContentRootFileProvider](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.contentrootfileprovider):

```csharp
var physicalProvider = _env.ContentRootFileProvider;
```

**Получение типов поставщика файлов путем внедрения зависимостей**

Вы можете внедрить провайдер в конструктор любого класса и назначить его локальному полю. Используйте это поле в методах класса для доступа к файлам.

::: moniker range=">= aspnetcore-2.0"

В нашем примере приложения класс `IndexModel` получает экземпляр `IFileProvider` для извлечения содержимого из основного каталога приложения.

*Pages/Index.cshtml.cs*:

[!code-csharp[](file-providers/samples/2.x/FileProviderSample/Pages/Index.cshtml.cs?name=snippet1)]

На этой странице выполняется итерация `IDirectoryContents`.

*Pages/Index.cshtml*:

[!code-cshtml[](file-providers/samples/2.x/FileProviderSample/Pages/Index.cshtml?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

В нашем примере приложения класс `HomeController` получает экземпляр `IFileProvider` для извлечения содержимого из основного каталога приложения.

*Controllers/HomeController.cs*:

[!code-csharp[](file-providers/samples/1.x/FileProviderSample/Controllers/HomeController.cs?name=snippet1)]

В этом представлении выполняется итерация `IDirectoryContents`.

*Views/Home/Index.cshtml*:

[!code-cshtml[](file-providers/samples/1.x/FileProviderSample/Views/Home/Index.cshtml?name=snippet1)]

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

### <a name="manifestembeddedfileprovider"></a>ManifestEmbeddedFileProvider

[ManifestEmbeddedFileProvider](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider) используется для доступа к файлам, внедренным в сборки. `ManifestEmbeddedFileProvider` использует манифест, скомпилированный в сборку, для воссоздания исходных путей для внедренных файлов.

> [!NOTE]
> `ManifestEmbeddedFileProvider` доступно в ASP.NET Core 2.1 и более поздних версий. Чтобы получить доступ к файлам, внедренным в сборки, из ASP.NET Core 2.0 или более ранних версий см. в [версии этой статьи для ASP.NET Core 1.x](/aspnet/core/fundamentals/file-providers?view=aspnetcore-1.1).

Чтобы создать манифест для внедренных файлов, задайте для свойства `<GenerateEmbeddedFilesManifest>` значение `true`. Выберите файлы для внедрения с помощью [&lt;EmbeddedResource&gt;](/dotnet/core/tools/csproj#default-compilation-includes-in-net-core-projects):

[!code-csharp[](file-providers/samples/2.x/FileProviderSample/FileProviderSample.csproj?highlight=5,13)]

Используйте [стандартные маски](#glob-patterns) для указания одного или нескольких файлов, которые вы хотите внедрить в сборку.

Наш пример приложения создает `ManifestEmbeddedFileProvider` и передает в соответствующий конструктор текущую выполняемую сборку.

*Startup.cs*:

```csharp
var manifestEmbeddedProvider = 
    new ManifestEmbeddedFileProvider(Assembly.GetEntryAssembly());
```

Дополнительные перегрузки позволяют сделать следующее:

* указать относительный путь к файлу;
* ограничить файлы по дате последнего изменения;
* указать имя внедренного ресурса, содержащего внедренный файл манифеста.

| Перегрузка | Описание |
| -------- | ----------- |
| [ManifestEmbeddedFileProvider(Assembly, String)](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_ManifestEmbeddedFileProvider__ctor_System_Reflection_Assembly_System_String_) | Принимает необязательный параметр `root` со значением относительного пути. Укажите `root`, чтобы ограничить вызовы [GetDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.getdirectorycontents) только ресурсами по указанному пути. |
| [ManifestEmbeddedFileProvider(Assembly, String, DateTimeOffset)](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_ManifestEmbeddedFileProvider__ctor_System_Reflection_Assembly_System_String_System_DateTimeOffset_) | Принимает необязательный параметр `root` со значением относительного пути и дату `lastModified` в параметре [DateTimeOffset](/dotnet/api/system.datetimeoffset). Дата `lastModified` ограничивает дату последнего изменения для экземпляров [IFileInfo](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo), возвращаемых функцией [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider). |
| [ManifestEmbeddedFileProvider(Assembly, String, String, DateTimeOffset)](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_ManifestEmbeddedFileProvider__ctor_System_Reflection_Assembly_System_String_System_String_System_DateTimeOffset_) | Принимает необязательный параметр `root` со значением относительного пути, дату `lastModified` и параметры `manifestName`. `manifestName` здесь представляет имя встроенного ресурса, содержащего манифест. |

::: moniker-end

::: moniker range="< aspnetcore-2.0"

### <a name="embeddedfileprovider"></a>EmbeddedFileProvider

[EmbeddedFileProvider](/dotnet/api/microsoft.extensions.fileproviders.embeddedfileprovider) используется для доступа к файлам, внедренным в сборки. Укажите файлы для внедрения с помощью свойства [&lt;EmbeddedResource&gt;](/dotnet/core/tools/csproj#default-compilation-includes-in-net-core-projects) в файле проекта:

```xml
<ItemGroup>
  <EmbeddedResource Include="Resource.txt" />
</ItemGroup>
```

Используйте [стандартные маски](#glob-patterns) для указания одного или нескольких файлов, которые вы хотите внедрить в сборку.

Наш пример приложения создает `EmbeddedFileProvider` и передает в соответствующий конструктор текущую выполняемую сборку.

*Startup.cs*:

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

Внедренные ресурсы не предоставляют каталоги. Вместо этого путь к ресурсу (через пространство имен) внедряется в имя файла с помощью разделителей `.`. В нашем примере приложения `baseNamespace` имеет значение `FileProviderSample.`.

Конструктор [EmbeddedFileProvider(Assembly, String)](/dotnet/api/microsoft.extensions.fileproviders.embeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_EmbeddedFileProvider__ctor_System_Reflection_Assembly_) принимает необязательный параметр `baseNamespace`. Укажите базовое пространство имен, чтобы ограничить вызовы [GetDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.getdirectorycontents) только ресурсами в указанном пространстве имен.

::: moniker-end

### <a name="compositefileprovider"></a>CompositeFileProvider

[CompositeFileProvider](/dotnet/api/microsoft.extensions.fileproviders.compositefileprovider) объединяет экземпляры `IFileProvider`, предоставляя единый интерфейс для работы с файлами от нескольких поставщиков. При создании `CompositeFileProvider` передайте в соответствующий конструктор один или несколько экземпляров `IFileProvider`:

::: moniker range=">= aspnetcore-2.0"

В нашем примере приложения `PhysicalFileProvider` и `ManifestEmbeddedFileProvider` предоставляют файлы для `CompositeFileProvider` с регистрацией в контейнере служб приложения:

[!code-csharp[](file-providers/samples/2.x/FileProviderSample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

В нашем примере приложения `PhysicalFileProvider` и `EmbeddedFileProvider` предоставляют файлы для `CompositeFileProvider` с регистрацией в контейнере служб приложения:

[!code-csharp[](file-providers/samples/1.x/FileProviderSample/Startup.cs?name=snippet1)]

::: moniker-end

## <a name="watch-for-changes"></a>Отслеживание изменений

Метод [IFileProvider.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) позволяет контролировать изменения в одном или нескольких файлах или каталогах. `Watch` принимает строку пути, которая можно использовать [стандартные маски](#glob-patterns) для указания нескольких файлов. `Watch` возвращает [IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken). Этот токен изменений предоставляет следующие свойства:

* [HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged): Свойство, которое может быть проверен для определения того, если произошло изменение.
* [RegisterChangeCallback](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback): Вызывается при обнаружении изменений для указанной строки пути. Каждый токен изменения выполняет соответствующий обратный вызов только в ответ на отдельное изменение. Чтобы реализовать постоянное наблюдение, используйте [TaskCompletionSource](/dotnet/api/system.threading.tasks.taskcompletionsource-1), как показано ниже, или повторно создавайте экземпляры `IChangeToken` в ответ на изменения.

В нашем примере консольное приложение *WatchConsole* будет отображать сообщение при изменении текстового файла:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](file-providers/samples/2.x/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](file-providers/samples/1.x/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

::: moniker-end

Некоторые файловые системы, такие как контейнеры Docker и сетевые папки, не могут надежно отправлять уведомления об изменениях. Задайте для переменной среды `DOTNET_USE_POLLING_FILE_WATCHER` значение `1` или `true`, чтобы опрашивать файловую систему на предмет изменений каждые 4 секунды (это значение нельзя изменить).

## <a name="glob-patterns"></a>Стандартные маски

В путях файловой системы используются шаблоны подстановочных знаков, которые называются *стандартными масками*. Эти маски позволяют указывать группы файлов. Поддерживаются два подстановочных знака — `*` и `**`.

**`*`**  
Совпадает с любым элементом на текущем уровне папок, любым именем или расширением файла. Совпадения завершаются символами `/` и `.` в пути файла.

**`**`**  
Совпадает со всем содержимым на разных уровнях каталогов. Может использоваться для рекурсивного сопоставления множества файлов в иерархии каталогов.

**Примеры стандартных масок**

**`directory/file.txt`**  
Соответствует конкретному файлу в заданном каталоге.

**`directory/*.txt`**  
Соответствует всем файлам с расширением *.txt* в заданном каталоге.

**`directory/*/appsettings.json`**  
Соответствует всем файлам `appsettings.json` в любом каталоге, расположенном ровно на один уровень ниже каталога *directory*.

**`directory/**/*.txt`**  
Соответствует всем файлам с расширением *.txt*, находящимся на любом уровне ниже каталога *directory*.
