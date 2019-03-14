---
ms.openlocfilehash: cb9041a466309a400b19cdecd76f653499c6ac4b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053981"
---
Запустите шаблон удостоверений:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Из **обозревателе решений**, правой кнопкой мыши проект > **добавить** > **создать шаблонный элемент**.
* В области слева от **Добавление шаблона** диалоговое окно, выберите **удостоверений** > **добавить**.
* В **удостоверение ADD** диалоговое окно, выберите нужные параметры.
  * Выберите существующий макет страницы или файл макета будет заменен неверные разметки. Если в имеющемся  *\_Layout.cshtml* выбран файл, это **не** перезаписаны.

 Например `~/Pages/Shared/_Layout.cshtml` для Razor Pages `~/Views/Shared/_Layout.cshtml` для проектов MVC
* Чтобы использовать существующий контекста данных, выберите хотя бы один файл для переопределения. Необходимо выбрать по крайней мере один файл, чтобы добавить контекста данных.
  * Выберите класс контекста данных.
  * Выберите **добавить**.
* Для создания нового контекста пользователя и возможно создать пользовательский класс для удостоверения:
  * Выберите **+** кнопку, чтобы создать новый **класс контекста данных**.
  * Выберите **добавить**.

Примечание. Если вы создаете новый контекст пользователя, у вас нет для выбора файла для переопределения.

# <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

Если вы еще не установлен шаблон ASP.NET Core, установите его:

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

Добавьте ссылку на пакет [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) в проект (\*.csproj) файла. Выполните следующую команду в каталоге проекта:

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

Выполните следующую команду, чтобы получить список вариантов шаблон удостоверений:

```cli
dotnet aspnet-codegenerator identity -h
```

В папке проекта запустите шаблон удостоверение с нужные параметры. Например чтобы настроить удостоверение с помощью пользовательского интерфейса по умолчанию и минимальное число файлов, выполните следующую команду. Используется правильное полное доменное имя для вашего контекста базы данных:

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files Account.Register
```

PowerShell используется точка с запятой в качестве разделителя команды. Если вы используете powershell, escape-точка с запятой в списке файлов или поместить в список файлов в двойные кавычки. Пример:

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files "Account.Register;Account.Login;Account.Logout"
```

Если запустить шаблон удостоверений без указания `--files` флаг или `--useDefaultUI` флаг, все доступные страницы удостоверение пользовательского интерфейса будет создан в проекте.

-------------
