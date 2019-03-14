---
title: Учебник. Использование ASP.NET MVC с EF Core. Функции миграций
description: В этом руководстве вы начинаете использовать функцию миграций EF Core для управления изменениями модели данных в приложении ASP.NET Core MVC.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/04/2019
ms.topic: tutorial
uid: data/ef-mvc/migrations
ms.openlocfilehash: ac924e7d6bee2f02ab11281a5c27f2c94a7183b3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026911"
---
# <a name="tutorial-using-the-migrations-feature---aspnet-mvc-with-ef-core"></a>Учебник. Использование ASP.NET MVC с EF Core. Функции миграций

В этом руководстве вы начинаете использовать функцию миграций EF Core для управления изменениями модели данных. В последующих руководствах вы добавите дополнительные миграции по мере изменения модели данных.

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Дополнительные сведения о миграциях
> * Дополнительные сведения о пакетах миграции NuGet
> * Изменение строки подключения
> * Создание первоначальной миграции
> * Обзор методов Up и Down
> * Дополнительные сведения о моментальном снимке модели данных
> * Применение миграции


## <a name="prerequisites"></a>Предварительные требования

* [Добавление сортировки, фильтрации и разбиения по страницам с использованием EF Core в приложении MVC ASP.NET Core](sort-filter-page.md)

## <a name="about-migrations"></a>Сведения о миграциях

При разработке нового приложения ваша модель данных часто меняется, и при каждом таком изменении она нарушает синхронизацию с базой данных. Вы начали работу с этими руководствами, настроив Entity Framework для создания базы данных, если она еще не существует. Затем при каждом изменении модели данных — добавлении, удалении или изменении классов сущностей или изменении класса DbContext — вы можете удалить базу данных, после чего EF создает новую, которая соответствует данной модели, и заполняет ее тестовыми данными.

Этот способ для обеспечения синхронизации базы данных с моделью данных хорошо работает до развертывания приложения в рабочей среде. Когда приложение выполняется в рабочей среде, оно обычно хранит данные, которые вы хотите сохранить, и вам нежелательно терять все при каждом изменении, например при добавлении нового столбца. Функция миграций EF Core решает эту проблему, позволяя EF обновить схему базы данных вместо создания базы данных.

## <a name="about-nuget-migration-packages"></a>Сведения о пакетах миграции NuGet

Для работы с миграциями можно использовать **консоль диспетчера пакетов** (PMC) или интерфейс командной строки (CLI).  Эти руководства демонстрируют использование команд интерфейса командной строки. Дополнительные сведения о PMC [приведены в конце этого руководства](#pmc).

Средства EF для интерфейса командной строки (CLI) доступны в [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet). Чтобы установить этот пакет, добавьте его в коллекцию `DotNetCliToolReference` в файле *CSPROJ*, как показано ниже. **Примечание.** Необходимо установить этот пакет, изменив файл *.csproj*. Использовать команду `install-package` или графический пользовательский интерфейс диспетчера пакетов нельзя. Вы можете изменить файл *CSPROJ*, щелкнув правой кнопкой мыши имя проекта в **обозревателе решений** и выбрав пункт **Изменить ContosoUniversity.csproj**.

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?range=12-15&highlight=2)]

(На момент написания руководства номера версий в этом примере были актуальными.)

## <a name="change-the-connection-string"></a>Изменение строки подключения

В файле *appsettings.json* измените имя базы данных в строке подключения на ContosoUniversity2 или другое имя, которое вы еще не использовали на компьютере, с которым работаете.

[!code-json[](intro/samples/cu/appsettings2.json?range=1-4)]

Это изменение настраивает проект, чтобы первая миграция создала базу данных. Это необязательно для начала работы с миграциями, но позднее вы поймете, почему так стоит сделать.

> [!NOTE]
> Вместо изменения имени базы данных можно удалить ее. Воспользуйтесь **обозревателем объектов SQL Server** (SSOX) или командой интерфейса командной строки `database drop`:
> ```console
> dotnet ef database drop
> ```
> Следующий раздел описывает выполнение команд интерфейса командной строки.

## <a name="create-an-initial-migration"></a>Создание первоначальной миграции

Сохраните изменения и выполните сборку проекта. После этого откройте командное окно и в папку проекта. Вот как это можно сделать быстро:

* Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите в контекстном меню пункт **Открыть папку в проводнике**.

  ![Элемент меню "Открыть в проводнике"](migrations/_static/open-in-file-explorer.png)

* Введите "cmd" в адресной строке и нажмите клавишу ВВОД.

  ![Открытие командного окна](migrations/_static/open-command-window.png)

Введите в командном окне следующую команду:

```console
dotnet ef migrations add InitialCreate
```

В командном окне отображаются следующие выходные данные:

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

> [!NOTE]
> Если отображается сообщение об ошибке *No executable found matching command "dotnet-ef"* (Не найден исполняемый файл, соответствующий команде "dotnet-ef"), сведения об устранении проблемы см. в [этой записи блога](http://thedatafarm.com/data-access/no-executable-found-matching-command-dotnet-ef/).

Если отображается сообщение об ошибке "*Доступ к файлу... ContosoUniversity.dll невозможен, так как файл используется другим процессом*", найдите значок IIS Express в области уведомлений Windows, щелкните его правой кнопкой мыши, а затем выберите **ContosoUniversity > Остановить сайт**.

## <a name="examine-up-and-down-methods"></a>Обзор методов Up и Down

При выполнении команды `migrations add` система EF сформировала код, который создаст базу данных с нуля. Этот код находится в файле *\<метка_времени>_InitialCreate.cs* внутри папки *Migrations*. Метод `Up` класса `InitialCreate` создает таблицы базы данных, которые соответствуют наборам сущностей модели данных, а метод `Down` удаляет их, как показано в следующем примере.

[!code-csharp[](intro/samples/cu/Migrations/20170215220724_InitialCreate.cs?range=92-118)]

Функция миграций вызывает метод `Up`, чтобы реализовать изменения модели данных для миграции. При вводе команды для отката обновления функция миграций вызывает метод `Down`.

Этот пример кода предназначен для первоначальной миграции, созданной при вводе команды `migrations add InitialCreate`. Параметр имени миграции (в примере это "InitialCreate") используется в качестве имени файла и может быть любым. Рекомендуется выбрать слово или фразу, которые кратко описывают назначение миграции. Например, последнюю миграцию можно назвать "AddDepartmentTable".

Если вы создали первоначальную миграцию, когда база данных уже существовала, код для создания базы данных формируется, но выполнять его не требуется, так как база данных уже соответствует модели данных. Однако при развертывании приложения в другой среде, где база данных еще не существует, этот код будет выполняться для создания базы данных, поэтому рекомендуется сначала его протестировать. Вот почему ранее вы изменили имя базы данных в строке подключения — это позволяет функции миграций создать базу данных с нуля.

## <a name="the-data-model-snapshot"></a>Моментальный снимок модели данных

Функция миграций создает *моментальный снимок* текущей схемы базы данных в *Migrations/SchoolContextModelSnapshot.cs*. При добавлении миграции EF определяет, что именно изменилось, сравнивая модель данных с файлом моментального снимка.

При удалении миграции используйте команду [dotnet ef migrations remove](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove). `dotnet ef migrations remove` удаляет миграцию и гарантирует корректный сброс моментального снимка.

Дополнительные сведения об использовании файла моментального снимка см. в разделе [Миграции Core EF в средах групп](/ef/core/managing-schemas/migrations/teams).

## <a name="apply-the-migration"></a>Применение миграции

Введите следующую команду в командном окне, чтобы создать базу данных и таблицы в ней.

```console
dotnet ef database update
```

Выходные данные команды аналогичны команде `migrations add`, за исключением того, что вы видите журналы для команд SQL, настраивающих базу данных. В приведенном ниже примере выходных данных большинство журналов опущено. Если вам не нужен такой уровень детализации сообщений журнала, можно изменить уровень ведения журнала в файле *appsettings.Development.json*. Дополнительные сведения см. в разделе <xref:fundamentals/logging/index>.

```text
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (467ms) [Parameters=[], CommandType='Text', CommandTimeout='60']
      CREATE DATABASE [ContosoUniversity2];
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (20ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );

<logs omitted for brevity>

info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (3ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      INSERT INTO [__EFMigrationsHistory] ([MigrationId], [ProductVersion])
      VALUES (N'20170816151242_InitialCreate', N'2.0.0-rtm-26452');
Done.
```

Используйте **обозреватель объектов SQL Server** для проверки базы данных, как описано в первом руководстве.  Вы заметите добавление таблицы \_\_EFMigrationsHistory, отслеживающей миграции, которые были применены к базе данных. Просмотрев данные в этой таблице, вы увидите одну строку для первой миграции. (Последний журнал в предыдущем примере выходных данных интерфейса командной строки показывает оператор INSERT, создающий эту строку.)

Запустите приложение, чтобы убедиться, что все работает, как и раньше.

![Страница указателя учащихся](migrations/_static/students-index.png)

<a id="pmc"></a>

## <a name="compare-cli-and-pmc"></a>Сравнение CLI и PMC

Средства EF для управления миграциями доступны в виде команд интерфейса командной строки .NET Core или командлетов PowerShell в окне **консоли диспетчера пакетов** Visual Studio. Это руководство описывает использование интерфейса командной строки, но вы можете использовать и консоль диспетчера пакетов.

Команды EF для команд консоли диспетчера пакетов находятся в пакете [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools). Этот пакет входит в [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app), поэтому если приложение уже содержит ссылку на пакет `Microsoft.AspNetCore.App`, добавлять ссылку на пакет не нужно.

**Внимание!** Это не тот же пакет, который вы устанавливаете для CLI, изменив файл *.csproj*. Его имя заканчивается на `Tools`, а имя пакета интерфейса командной строки — на `Tools.DotNet`.

Дополнительные сведения о командах интерфейса командной строки см. в разделе [.NET Core CLI](/ef/core/miscellaneous/cli/dotnet).

Дополнительные сведения о командах консоли диспетчера пакетов см. в разделе [Консоль диспетчера пакетов (Visual Studio)](/ef/core/miscellaneous/cli/powershell).

## <a name="get-the-code"></a>Получение кода

[Скачайте или ознакомьтесь с готовым приложением.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-step"></a>Дальнейшие действия

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Дополнительные сведения о миграциях
> * Дополнительные сведения о пакетах миграции NuGet
> * Изменение строки подключения
> * Создание первоначальной миграции
> * Обзор методов Up и Down
> * Дополнительные сведения о моментальном снимке модели данных
> * Применение миграции

В следующем руководстве описаны более сложные вопросы, связанные с развертыванием модели данных. Попутно вы создадите и примените дополнительные миграции.
> [!div class="nextstepaction"]
> [Создание и применение дополнительных миграций](complex-data-model.md)
