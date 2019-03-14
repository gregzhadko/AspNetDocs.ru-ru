---
title: Разработка приложений ASP.NET Core с использованием наблюдателя файлов
author: rick-anderson
description: В этом руководстве показано, как установить и использовать наблюдатель за файлами .NET Core CLI (dotnet watch) в приложении ASP.NET Core.
ms.author: riande
ms.date: 05/31/2018
uid: tutorials/dotnet-watch
ms.openlocfilehash: f1e0d91b27df4af7cbfb6f2547c94c0370c65d0d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029591"
---
# <a name="develop-aspnet-core-apps-using-a-file-watcher"></a>Разработка приложений ASP.NET Core с использованием наблюдателя файлов

Авторы: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Виктор Хурдугачи](https://twitter.com/victorhurdugaci) (Victor Hurdugaci)

`dotnet watch` — это средство, которое запускает команду [.NET Core CLI](/dotnet/core/tools) при изменении исходных файлов. Например, в результате изменения файла может выполняться компиляция, тестирование или развертывание.

В этом руководстве используется уже существующее приложение веб-API с двумя конечными точками, одна из которых возвращает сумму, а другая — произведение. В методе произведения есть ошибка, которая исправлена в этом руководстве.

Скачайте [образец приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample). Он содержит два проекта: *WebApp* (веб-API ASP.NET Core) и *WebAppTests* (модульные тесты для веб-API).

В командной оболочке перейдите в папку *WebApp*. Выполните следующую команду:

```console
dotnet run
```

В выходных данных в консоли будут показаны аналогичные следующим сообщения, которые свидетельствуют о том, что приложение выполняется и ожидает запросов:

```console
$ dotnet run
Hosting environment: Development
Content root path: C:/Docs/aspnetcore/tutorials/dotnet-watch/sample/WebApp
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

В браузере перейдите на адрес `http://localhost:<port number>/api/math/sum?a=4&b=5`. Должен появиться результат `9`.

Перейдите к API продукта (`http://localhost:<port number>/api/math/product?a=4&b=5`). Он возвращает `9`, а не `20`, как ожидалось. Эта проблема устраняется далее в этом руководстве.

::: moniker range="<= aspnetcore-2.0"

## <a name="add-dotnet-watch-to-a-project"></a>Добавление `dotnet watch` в проект

Средство наблюдения за файлами `dotnet watch` входит в версию 2.1.300 пакета SDK для .NET Core. Выполните следующие действия при использовании более ранней версии пакета SDK для .NET Core.

1. Добавьте ссылку на пакет `Microsoft.DotNet.Watcher.Tools` в *CSPROJ*-файл:

    ```xml
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup>
    ```

1. Установите пакет `Microsoft.DotNet.Watcher.Tools`, запустив следующую команду:

    ```console
    dotnet restore
    ```

::: moniker-end

## <a name="run-net-core-cli-commands-using-dotnet-watch"></a>Запуск команд .NET Core CLI с помощью `dotnet watch`

Любую [команду .NET Core CLI](/dotnet/core/tools#cli-commands) можно запустить с `dotnet watch`. Пример:

| Команда | Команда с контрольным значением |
| ---- | ----- |
| dotnet run | dotnet watch run |
| dotnet run -f netcoreapp2.0 | dotnet watch run -f netcoreapp2.0 |
| dotnet run -f netcoreapp2.0 -- --arg1 | dotnet watch run -f netcoreapp2.0 -- --arg1 |
| dotnet test | dotnet watch test |

Запустите `dotnet watch run` в папке *WebApp*. В выходных данных консоли будет указано, что запущен `watch`.

## <a name="make-changes-with-dotnet-watch"></a>Изменения с помощью `dotnet watch`

Убедитесь, что `dotnet watch` выполняется.

Исправьте ошибку в методе `Product` для *MathController.cs* так, чтобы он возвращал произведение, а не сумму чисел.

```csharp
public static int Product(int a, int b)
{
  return a * b;
}
```

Сохраните файл. В выходных данных консоли будет показано, что `dotnet watch` обнаружил изменение файла и перезапустил приложение.

Убедитесь, что `http://localhost:<port number>/api/math/product?a=4&b=5` возвращает правильный результат.

## <a name="run-tests-using-dotnet-watch"></a>Тестирование с помощью `dotnet watch`

1. Снова измените метод `Product` для *MathController.cs* так, чтобы он возвращал сумму чисел. Сохраните файл.
1. В командной оболочке перейдите в папку *WebAppTests*.
1. Запустите [dotnet restore](/dotnet/core/tools/dotnet-restore).
1. Запустите `dotnet watch test`. В выходных данных будет указано, что проверка не пройдена и наблюдатель ожидает изменений в файле:

     ```console
     Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
     Test Run Failed.
     ```

1. Исправьте код метода `Product` так, чтобы он возвращал произведение. Сохраните файл.

`dotnet watch` обнаруживает изменения в файле и повторно запускает тесты. В выходных данных консоли будет указано, что проверка пройдена.

## <a name="customize-files-list-to-watch"></a>Настройка списка файлов для наблюдения

По умолчанию `dotnet-watch` отслеживает все файлы, соответствующие следующим стандартным маскам:

* `**/*.cs`
* `*.csproj`
* `**/*.resx`

Можно добавить в список наблюдения еще элементы, отредактировав файл *.csproj*. Элементы можно указывать по отдельности или с помощью стандартной маски.

```xml
<ItemGroup>
    <!-- extends watching group to include *.js files -->
    <Watch Include="**\*.js" Exclude="node_modules\**\*;**\*.js.map;obj\**\*;bin\**\*" />
</ItemGroup>
```

## <a name="opt-out-of-files-to-be-watched"></a>Удаление файлов из списка наблюдения

Можно настроить `dotnet-watch` так, чтобы игнорировать параметры по умолчанию. Чтобы пропускать определенные файлы, добавьте атрибут `Watch="false"` в определение элемента в файле *.csproj*:

```xml
<ItemGroup>
    <!-- exclude Generated.cs from dotnet-watch -->
    <Compile Include="Generated.cs" Watch="false" />

    <!-- exclude Strings.resx from dotnet-watch -->
    <EmbeddedResource Include="Strings.resx" Watch="false" />

    <!-- exclude changes in this referenced project -->
    <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj" Watch="false" />
</ItemGroup>
```

## <a name="custom-watch-projects"></a>Пользовательское наблюдение за проектами

`dotnet-watch` используется не только с проектами C#. Создайте пользовательское наблюдение за проектами для различных ситуаций. Вы можете использовать следующий макет проекта:

* **test/**
  * *UnitTests/UnitTests.csproj*
  * *IntegrationTests/IntegrationTests.csproj*

Если вы хотите наблюдать за обоими проектами, создайте пользовательский файл проекта, настроенный для наблюдения за обоими проектами:

```xml
<Project>
    <ItemGroup>
        <TestProjects Include="**\*.csproj" />
        <Watch Include="**\*.cs" />
    </ItemGroup>

    <Target Name="Test">
        <MSBuild Targets="VSTest" Projects="@(TestProjects)" />
    </Target>

    <Import Project="$(MSBuildExtensionsPath)\Microsoft.Common.targets" />
</Project>
```

Чтобы запустить наблюдение за файлами для обоих проектов, внесите изменения в папку *test*. Выполните следующую команду:

```console
dotnet watch msbuild /t:Test
```

VSTest выполняется при изменении любого файла в любом из тестовых проектов.

## <a name="dotnet-watch-in-github"></a>`dotnet-watch` на GitHub

`dotnet-watch` предоставляется в [репозитории aspnet/AspNetCore](https://github.com/aspnet/AspNetCore/tree/master/src/Tools/dotnet-watch) на GitHub.
