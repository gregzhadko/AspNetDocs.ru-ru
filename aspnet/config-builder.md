---
uid: config-builder
title: Построители конфигураций для ASP.NET
author: rick-anderson
description: Узнайте, как получить данные конфигурации из источников, отличных от web.config значений из внешних источников.
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424806"
---
# <a name="configuration-builders-for-aspnet"></a>Построители конфигураций для ASP.NET

В [Стивен Моллой](https://github.com/StephenMolloy) и [Рик Андерсон (](https://twitter.com/RickAndMSFT)

Построители конфигураций предоставляют современный и гибкий механизм для ASP.NET приложений с целью получения значений конфигурации из внешних источников.

Построители конфигураций:

* Доступны в .NET Framework 4.7.1 и более поздних версиях.
* Предоставьте гибкий механизм чтения значений конфигурации.
* Устраните некоторые из основных потребностей приложений по мере их перемещения в контейнер и в облачную среду.
* Можно использовать для улучшения защиты данных конфигурации путем рисования из ранее недоступных источников (например, Azure Key Vault и переменных среды) в системе конфигурации .NET.

## <a name="keyvalue-configuration-builders"></a>Построители конфигурации "ключ — значение"

Распространенным сценарием, который может обработать построители конфигураций, является предоставление базового механизма замены ключа и значения для разделов конфигурации, которые следуют шаблону "ключ-значение". .NET Framework концепция ConfigurationBuilders не ограничена конкретными разделами конфигурации или шаблонами. Однако многие построители конфигураций в `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) работают в шаблоне "ключ — значение".

## <a name="keyvalue-configuration-builders-settings"></a>Параметры построителя конфигурации "ключ — значение"

Следующие параметры применяются ко всем сборщикам конфигурации "ключ-значение" в `Microsoft.Configuration.ConfigurationBuilders` .

### <a name="mode"></a>Режим

Построители конфигурации используют внешний источник сведений о ключе и значении для заполнения выбранных элементов "ключ-значение" системы конфигурации. В частности, `<appSettings/>` `<connectionStrings/>` разделы и получают специальную обработку от построителей конфигураций. Построители работают в трех режимах:

* `Strict`— Режим по умолчанию. В этом режиме построитель конфигурации работает только с хорошо известными разделами конфигурации, основанными на ключах и значениях. `Strict`режим перечисляет каждый ключ в разделе. Если в внешнем источнике найден соответствующий ключ:

   * Построители конфигурации заменяют значение в результирующем разделе конфигурации значением из внешнего источника.
* `Greedy`— Этот режим тесно связан с `Strict` режимом. Вместо того чтобы ограничиваться ключами, которые уже существуют в исходной конфигурации:

  * Построители конфигурации добавляют все пары "ключ-значение" из внешнего источника в результирующий раздел конфигурации.

* `Expand`— Работает с необработанным XML до того, как он был проанализирован в объект раздела конфигурации. Его можно рассматривать как расширение токенов в строке. Любая часть необработанной XML-строки, соответствующей шаблону, `${token}` является кандидатом для расширения токена. Если в внешнем источнике не найдено соответствующее значение, токен не изменяется. Построители в этом режиме не ограничиваются `<appSettings/>` `<connectionStrings/>` разделами и.

Следующая разметка из *web.config* включает режим [енвиронментконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) в `Strict` режиме:

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

Следующий код считывает `<appSettings/>` и `<connectionStrings/>` показан в предыдущем *web.config* файле:

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

В приведенном выше коде значения свойств будут заданы следующим образом:

* Значения в файле *web.config* , если ключи не заданы в переменных среды.
* Значения переменной среды, если задано значение.

Например, `ServiceID` будет содержать:

* "ServiceID значение из web.config", если переменная среды `ServiceID` не задана.
* Значение `ServiceID` переменной среды, если оно задано.

На следующем рисунке показаны `<appSettings/>` ключи и значения из предыдущего *web.config* набора файлов в редакторе среды.

![редактор среды](config-builder/static/env.png)

Примечание. для просмотра изменений в переменных среды может потребоваться выйти и перезапустить Visual Studio.

### <a name="prefix-handling"></a>Обработка префиксов

Префиксы ключей позволяют упростить параметры ключей, так как:

* Конфигурация .NET Framework является сложной и вложенной.
* Внешние источники "ключ — значение" обычно являются базовыми и плоскими по природе. Например, переменные среды не являются вложенными.

Используйте любой из следующих подходов, чтобы внедрить `<appSettings/>` и `<connectionStrings/>` в конфигурацию с помощью переменных среды:

* С параметром `EnvironmentConfigBuilder` в режиме по умолчанию `Strict` и соответствующими именами ключей в файле конфигурации. Этот подход используется в приведенном выше коде и разметке. При таком подходе нельзя **использовать одинаковые** именованные ключи как в `<appSettings/>` , так и в `<connectionStrings/>` .
* Используйте два `EnvironmentConfigBuilder` режима s в `Greedy` режиме с разными префиксами и `stripPrefix` . При таком подходе приложение может считывать `<appSettings/>` и `<connectionStrings/>` без необходимости обновлять файл конфигурации. В следующем разделе [стриппрефикс](#stripprefix)показано, как это сделать.
* Используйте два `EnvironmentConfigBuilder` режима s в `Greedy` режиме с разными префиксами. При таком подходе не допускается наличие повторяющихся имен ключей, так как имена ключей должны отличаться по префиксу.  Пример.

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

В предыдущей разметке для заполнения конфигурации двух разных разделов можно использовать один и тот же источник «Плоский ключ/значение».

На следующем рисунке показаны `<appSettings/>` ключи и `<connectionStrings/>` значения из предыдущего *web.config* набора файлов в редакторе среды.

![редактор среды](config-builder/static/prefix.png)

Следующий код считывает `<appSettings/>` `<connectionStrings/>` ключи и значения, содержащиеся в предыдущем *web.config* файле:

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

В приведенном выше коде значения свойств будут заданы следующим образом:

* Значения в файле *web.config* , если ключи не заданы в переменных среды.
* Значения переменной среды, если задано значение.

Например, используя предыдущий *web.config* файл, ключи/значения в предыдущем изображении редактора среды и предыдущий код, задаются следующие значения:

|  Ключ              | Значение |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | AppSetting_ServiceID из переменных env|
|    AppSetting_default            | AppSetting_default значение из env |
|       ConnStr_default         | ConnStr_default Val из env|

### <a name="stripprefix"></a>стриппрефикс

`stripPrefix`: логическое значение, по умолчанию — `false` . 

Предыдущая разметка XML разделяет параметры приложения из строк соединения, но требует, чтобы все ключи в файле *web.config* использовали указанный префикс. Например, префикс `AppSetting` должен быть добавлен к `ServiceID` ключу ("AppSetting_ServiceID"). В параметре `stripPrefix` префикс не используется в файле *web.config* . Префикс является обязательным в источнике построителя конфигураций (например, в среде). Мы ожидаем, что большинство разработчиков будут использовать `stripPrefix` .

Приложения обычно удаляются с префикса. Следующий *web.config* отделяет префикс:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

В предыдущем *web.config* файле `default` ключ находится как в, так и в `<appSettings/>` `<connectionStrings/>` .

На следующем рисунке показаны `<appSettings/>` ключи и `<connectionStrings/>` значения из предыдущего *web.config* набора файлов в редакторе среды.

![редактор среды](config-builder/static/prefix.png)

Следующий код считывает `<appSettings/>` `<connectionStrings/>` ключи и значения, содержащиеся в предыдущем *web.config* файле:

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

В приведенном выше коде значения свойств будут заданы следующим образом:

* Значения в файле *web.config* , если ключи не заданы в переменных среды.
* Значения переменной среды, если задано значение.

Например, используя предыдущий *web.config* файл, ключи/значения в предыдущем изображении редактора среды и предыдущий код, задаются следующие значения:

|  Ключ              | Значение |
| ----------------- | ------------ |
|     ServiceID           | AppSetting_ServiceID из переменных env|
|    значение по умолчанию            | AppSetting_default значение из env |
|    значение по умолчанию         | ConnStr_default Val из env|

### <a name="tokenpattern"></a>токенпаттерн

`tokenPattern`: Строка, по умолчанию —`@"\$\{(\w+)\}"`

`Expand`Поведение построителей посматривает необработанный XML-код для маркеров, которые выглядят как `${token}` . Поиск выполняется с помощью регулярного выражения по умолчанию `@"\$\{(\w+)\}"` . Набор символов, соответствующих, `\w` является более четким, чем XML, и позволяет использовать множество источников конфигурации. Используйте `tokenPattern` `@"\$\{(\w+)\}"` , если в имени токена больше символов, чем требуется.

`tokenPattern`Строка

* Позволяет разработчикам изменять регулярное выражение, используемое для сопоставления маркеров.
* Проверка не выполняется, чтобы убедиться, что это правильно сформированное, неопасное регулярное выражение.
* Он должен содержать группу захвата. Целое регулярное выражение должно соответствовать всему токену. Первая запись должна быть именем токена для поиска в источнике конфигурации.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Построители конфигураций в Microsoft.Configuration.ConfigУратионбуилдерс

### <a name="environmentconfigbuilder"></a>енвиронментконфигбуилдер

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[Енвиронментконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* — Это самая простая из построителей конфигураций.
* Считывает значения из среды.
* Не имеет дополнительных параметров конфигурации.
* `name`Значение атрибута является произвольным.

**Примечание.** В среде контейнера Windows переменные, заданные во время выполнения, вставляются только в среду процесса EntryPoint. Приложения, работающие как службы или процессы, не являющиеся точкой входа, не получают эти переменные, если они не вставляются через механизм в контейнере. Для [IIS](https://github.com/Microsoft/iis-docker/pull/41) / контейнеров, основанных на[ASP.NET](https://github.com/Microsoft/aspnet-docker)IIS, текущая версия [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) обрабатывает это только в *DefaultAppPool* . Другим вариантам контейнеров на основе Windows может потребоваться разработать собственный механизм внедрения для процессов, не относящихся к EntryPoint.

### <a name="usersecretsconfigbuilder"></a>усерсекретсконфигбуилдер

> [!WARNING]
> Никогда не храните пароли, конфиденциальные строки подключения или другие конфиденциальные данные в исходном коде. Рабочие секреты не следует использовать для разработки или тестирования.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

Этот построитель конфигураций предоставляет функцию, аналогичную [ASP.NET Core диспетчере секретов](/aspnet/core/security/app-secrets).

[Усерсекретсконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) можно использовать в проектах .NET Framework, но должен быть указан секретный файл. Кроме того, можно определить `UserSecretsId` свойство в файле проекта и создать необработанный файл секретов в правильном расположении для чтения. Для сохранения внешних зависимостей в проекте секретный файл имеет формат XML. Форматирование XML является подробным описанием реализации, и формат не должен рассчитываться на этот момент. Если необходимо предоставить общий доступ к *secrets.js* файлу с проектами .NET Core, рассмотрите возможность использования [симплежсонконфигбуилдер](#simplejsonconfigbuilder). `SimpleJsonConfigBuilder`Формат для .NET Core также следует рассматривать как сведения о реализации, которые могут быть изменены.

Атрибуты конфигурации для `UserSecretsConfigBuilder` :

* `userSecretsId`— Это предпочтительный метод для определения XML-файла секретов. Он работает аналогично .NET Core, который использует `UserSecretsId` свойство проекта для хранения этого идентификатора. Строка должна быть уникальной, она не должна быть идентификатором GUID. С помощью этого атрибута `UserSecretsConfigBuilder` найдите известное локальное расположение ( `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` ) для секретного файла, принадлежащего этому идентификатору.
* `userSecretsFile`— Необязательный атрибут, указывающий файл, содержащий секреты. `~`Символ может использоваться в начале для ссылки на корень приложения. Необходимо указать этот атрибут или `userSecretsId` атрибут. Если указаны оба значения, `userSecretsFile` имеет приоритет.
* `optional`: Boolean, значение по умолчанию `true` — предотвращает исключение, если не удается найти секретный файл. 
* `name`Значение атрибута является произвольным.

Секретный файл имеет следующий формат:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>азурекэйваултконфигбуилдер

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[Азурекэйваултконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) считывает значения, хранящиеся в [Azure Key Vault](/azure/key-vault/key-vault-whatis).

`vaultName`требуется (имя хранилища или URI-адрес хранилища). Другие атрибуты позволяют управлять тем, к какому хранилищу подключаться, но это необходимо только в том случае, если приложение не выполняется в среде, которая работает с `Microsoft.Azure.Services.AppAuthentication` . Библиотека проверки подлинности служб Azure используется для автоматического выбора сведений о подключении из среды выполнения, если это возможно. Вы можете переопределить автоматическое получение сведений о соединении, предоставив строку подключения.

* `vaultName`— Требуется `uri` , если не предоставлено. Указывает имя хранилища в подписке Azure, из которого считываются пары "ключ-значение".
* `connectionString`— Строка подключения, используемая [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)
* `uri`— Подключается к другим поставщикам Key Vault с указанным `uri` значением. Если этот параметр не указан, Azure ( `vaultName` ) является поставщиком хранилища.
* `version`-Azure Key Vault предоставляет функцию управления версиями для секретов. Если `version` указан параметр, построитель получит только секреты, соответствующие этой версии.
* `preloadSecretNames`— По умолчанию этот конструктор запрашивает **все** имена ключей в хранилище ключей при инициализации. Чтобы запретить чтение всех значений ключа, присвойте этому атрибуту значение `false` . Установка этого параметра для `false` чтения секретов по одному за раз. Чтение секретов по одному может оказаться полезным, если хранилище разрешает доступ "Get", но не "List". **Примечание.** При использовании `Greedy` режима `preloadSecretNames` должен быть `true` (значение по умолчанию).

### <a name="keyperfileconfigbuilder"></a>кэйперфилеконфигбуилдер

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[Кэйперфилеконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) — это базовый построитель конфигураций, в котором файлы каталога используются в качестве источника значений. Имя файла является ключом, а содержимое — значением. Этот построитель конфигурации может быть полезен при работе в управляемой среде контейнера. Такие системы, как DOCKER Swarm и Kubernetes, предоставляют `secrets` своим управляемым контейнерам Windows этот ключ для каждого файла.

Сведения об атрибуте:

* `directoryPath` — обязательный. Указывает путь для поиска значений. Docker для Windows секреты по умолчанию хранятся в каталоге *к:\програмдата\доккер\секретс* .
* `ignorePrefix`— Файлы, начинающиеся с этого префикса, исключаются. Значение по умолчанию — "ignore.".
* `keyDelimiter`— Значение по умолчанию — `null` . Если этот параметр указан, построитель конфигурации проходит по нескольким уровням каталога, создавая имена ключей с помощью этого разделителя. Если это значение равно `null` , построитель конфигурации рассматривает только верхний уровень каталога.
* `optional`— Значение по умолчанию — `false` . Указывает, должны ли построитель конфигурации вызывать ошибки, если исходный каталог не существует.

### <a name="simplejsonconfigbuilder"></a>симплежсонконфигбуилдер

> [!WARNING]
> Никогда не храните пароли, конфиденциальные строки подключения или другие конфиденциальные данные в исходном коде. Рабочие секреты не следует использовать для разработки или тестирования.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

Проекты .NET Core часто используют JSON файлы для настройки. Построитель [симплежсонконфигбуилдер](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) позволяет использовать файлы JSON .NET Core в .NET Framework. Этот построитель конфигураций обеспечивает базовое сопоставление из источника «ключ-значение» с конкретными областями «ключ-значение» .NET Framework конфигурации. Этот построитель конфигураций **не** предоставляет иерархические конфигурации. Резервный файл JSON подобен словарю, а не сложному иерархическому объекту. Можно использовать многоуровневый иерархический файл. Этот поставщик имеет `flatten` глубину, добавляя имя свойства на каждом уровне, используя `:` в качестве разделителя.

Сведения об атрибуте:

* `jsonFile` — обязательный. Указывает JSON файл, из которого производится чтение. `~`Символ может использоваться в начале для ссылки на корень приложения.
* `optional`-Boolean, значение по умолчанию — `true` . Предотвращает создание исключений, если не удается найти JSON файл.
* `jsonMode` - `[Flat|Sectional]`. Значение по умолчанию — `Flat`. Если `jsonMode` имеет значение `Flat` , JSON-файл является одним плоским источником «ключ-значение». `EnvironmentConfigBuilder`И `AzureKeyVaultConfigBuilder` являются также единичными источниками «ключ-значение». Если параметр `SimpleJsonConfigBuilder` настроен в `Sectional` режиме:

  * Файл JSON концептуально делится на несколько словарей только на верхнем уровне.
  * Каждый из словарей применяется только к разделу конфигурации, который соответствует имени свойства верхнего уровня, присоединенному к ним. Пример.

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a>Порядок построителя конфигураций

См. раздел [порядок выполнения ConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) в репозитории GitHub [/микрософтконфигуратионбуилдерс](https://github.com/aspnet/MicrosoftConfigurationBuilders) .

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>Реализация пользовательского построителя конфигурации "ключ — значение"

Если построители конфигураций не соответствуют вашим потребностям, вы можете написать собственный. `KeyValueConfigBuilder`Базовый класс обрабатывает режимы подстановки и большинство проблем с префиксом. Для реализации проекта требуется только:

* Наследование от базового класса и реализация базового источника пар "ключ-значение" с помощью `GetValue` и `GetAllValues` :
* Добавьте [Microsoft.Configuration.Configуратионбуилдерс. base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) в проект.

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`Базовый класс предоставляет большую часть работы и согласованное поведение для построителей конфигурации "ключ-значение".

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Репозиторий GitHub для сборщиков конфигураций](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [Проверка подлинности между службами для Azure Key Vault с помощью .NET](/azure/key-vault/service-to-service-authentication#connection-string-support)
