---
title: Шаблон параметров в ASP.NET Core
author: guardrex
description: Узнайте, как использовать шаблон параметров для представления групп связанных параметров в приложениях ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: fundamentals/configuration/options
ms.openlocfilehash: 9566ed75375bdfaa9d6d8bf898b9fb2054356017
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065221"
---
# <a name="options-pattern-in-aspnet-core"></a>Шаблон параметров в ASP.NET Core

Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)

::: moniker range="<= aspnetcore-1.1"

Для версии 1.1 этого раздела скачайте статью [Шаблон параметров в ASP.NET Core (версия 1.1, PDF-файл)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Options_1.1.pdf).

::: moniker-end

Шаблон параметров использует классы для представления групп связанных настроек. Когда [параметры конфигурации](xref:fundamentals/configuration/index) изолируются по сценарию в отдельных классах, в приложениях соблюдаются два важных принципа программной инженерии.

* [Принцип изоляции интерфейсов или инкапсуляция](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation). Сценарии (классы), которые зависят от параметров конфигурации, зависят только от используемых ими параметров конфигурации.
* [Разделение ответственности](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns). Параметры для разных частей приложения не зависят друг от друга и не связаны друг с другом.

В параметрах также предусмотрен механизм для проверки данных конфигурации. Дополнительные сведения см. в разделе [Проверка параметров](#options-validation).

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/samples) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>Предварительные требования

Добавьте ссылку на [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) или добавьте ссылку на пакет в пакет [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/).

## <a name="options-interfaces"></a>Интерфейсы параметров

<xref:Microsoft.Extensions.Options.IOptionsMonitor`1> используется для извлечения параметров и управления уведомлениями о параметрах для экземпляров `TOptions`. <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> поддерживается в следующих сценариях:

* уведомления об изменениях;
* [именованные параметры](#named-options-support-with-iconfigurenamedoptions);
* [перезагружаемые конфигурации](#reload-configuration-data-with-ioptionssnapshot);
* объявление определенных параметров недействительными (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1>).

Сценарии [пост-конфигурации](#options-post-configuration) позволяют задать или изменить параметры после выполнения всех действий настройки с помощью <xref:Microsoft.Extensions.Options.IConfigureOptions`1>.

Интерфейс <xref:Microsoft.Extensions.Options.IOptionsFactory`1> отвечает за создание экземпляров параметров. Он имеет единственный метод <xref:Microsoft.Extensions.Options.IOptionsFactory`1.Create*>. При реализации по умолчанию принимаются все зарегистрированные интерфейсы <xref:Microsoft.Extensions.Options.IConfigureOptions`1> и <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1>. Также сначала выполняются все основные настройки, а затем действия после конфигурации. Она различает интерфейсы <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> и <xref:Microsoft.Extensions.Options.IConfigureOptions`1> и вызывает только соответствующий интерфейс.

<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1> используется интерфейсом <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> для записи экземпляров `TOptions` в кэш. <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1> делает экземпляры параметров в мониторе недействительными, что приводит к повторному вычислению значений (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryRemove*>). Значения можно также вводить вручную с помощью <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryAdd*>. Метод <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.Clear*> используется, если необходимо повторно создать все именованные экземпляры по требованию.

<xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> полезно использовать в сценариях, когда параметры должны заново вычисляться при каждом запросе. Дополнительные сведения см. в разделе [Повторная загрузка данных конфигурации с помощью IOptionsSnapshot](#reload-configuration-data-with-ioptionssnapshot).

<xref:Microsoft.Extensions.Options.IOptions`1> можно использовать, чтобы обеспечить поддержку определенных параметров. Но <xref:Microsoft.Extensions.Options.IOptions`1> не поддерживается в описанных выше сценариях <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>. Вы можете продолжать использовать <xref:Microsoft.Extensions.Options.IOptions`1> в существующих платформах и библиотеках, которые уже используют интерфейс <xref:Microsoft.Extensions.Options.IOptions`1>. В таком случае вам не потребуются сценарии, предоставляемые <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>.

## <a name="general-options-configuration"></a>Конфигурация общих параметров

Конфигурация общих параметров демонстрируется в примере &num;1 в примере приложения.

Класс параметров должен быть неабстрактным с открытым конструктором без параметров. Приведенный ниже класс (`MyOptions`) имеет два свойства: `Option1` и `Option2`. Задавать значения по умолчанию необязательно, однако конструктор класса в этом примере задает значение по умолчанию для `Option1`. Значение по умолчанию для `Option2` устанавливается путем прямой инициализации (*Models/MyOptions.cs*).

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptions.cs?name=snippet1)]

Класс `MyOptions` добавляется в контейнер службы с помощью интерфейса <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure*> и привязывается к конфигурации.

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example1)]

В следующей страничной модели применяется [внедрение зависимостей конструктора](xref:mvc/controllers/dependency-injection) с помощью <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> для доступа к параметрам (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example1)]

В файле *appsettings.json* образца задаются значения для свойств `option1` и `option2`:

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=2-3)]

Когда приложение выполняется, метод `OnGet` страничной модели возвращает строку со значениями класса параметров:

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> При использовании настраиваемого компонента <xref:System.Configuration.ConfigurationBuilder> для загрузки конфигурации параметров из файла настроек необходимо убедиться, что базовый путь задан правильно:
>
> ```csharp
> var configBuilder = new ConfigurationBuilder()
>    .SetBasePath(Directory.GetCurrentDirectory())
>    .AddJsonFile("appsettings.json", optional: true);
> var config = configBuilder.Build();
>
> services.Configure<MyOptions>(config);
> ```
>
> При загрузке конфигурации параметров из файла настроек с помощью <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> явно задавать базовый путь не требуется.

## <a name="configure-simple-options-with-a-delegate"></a>Настройка простых параметров с помощью делегата

Настройка простых параметров с помощью делегата демонстрируется в примере &num;2 в примере приложения.

Используйте делегат для задания значений параметров. В образце приложения используется класс `MyOptionsWithDelegateConfig` (*Models/MyOptionsWithDelegateConfig.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

В приведенном ниже коде в контейнер службы добавляется еще одна служба <xref:Microsoft.Extensions.Options.IConfigureOptions`1>. Она использует делегат для настройки привязки к `MyOptionsWithDelegateConfig`:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example2)]

*Index.cshtml.cs*:

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example2)]

Можно добавить несколько поставщиков конфигурации. Поставщики конфигурации доступны в пакетах NuGet и применяются в порядке регистрации. Дополнительные сведения см. в разделе <xref:fundamentals/configuration/index>.

При каждом вызове <xref:Microsoft.Extensions.Options.IConfigureOptions`1.Configure*> служба <xref:Microsoft.Extensions.Options.IConfigureOptions`1> добавляется в контейнер службы. В предыдущем примере значения `Option1` и `Option2` задаются в файле *appsettings.json*, однако значения `Option1` и `Option2` переопределяются настроенным делегатом.

Если включено более одной службы конфигурации, последний источник конфигурации *имеет приоритет* и определяет значение конфигурации. Когда приложение выполняется, метод `OnGet` страничной модели возвращает строку со значениями класса параметров:

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>Конфигурация подпараметров

Конфигурация подпараметров демонстрируется в примере &num;3 в примере приложения.

В приложениях должны создаваться классы приложений, относящиеся к определенным группам сценариев (классам). Части приложения, которым требуются значения конфигурации, должны иметь доступ только к используемым ими значениям конфигурации.

При привязке параметров к конфигурации каждое свойство, относящееся к типу параметров, привязывается к ключу конфигурации в формате `property[:sub-property:]`. Например, свойство `MyOptions.Option1` привязывается к ключу `Option1`, который считывается из свойства `option1` в файле *appsettings.json*.

В приведенном ниже коде в контейнер службы добавляется третья служба <xref:Microsoft.Extensions.Options.IConfigureOptions`1>. Она привязывает `MySubOptions` к разделу `subsection` файла *appsettings.json*.

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example3)]

Методу расширения `GetSection` требуется пакет NuGet [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/). Если приложение использует [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 или более поздней версии), пакет включается автоматически.

В файле *appsettings.json* образца определяется член `subsection` с ключами для `suboption1` и `suboption2`.

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=4-7)]

Класс `MySubOptions` определяет свойства `SubOption1` и `SubOption2` для хранения значений параметров (*Models/MySubOptions.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MySubOptions.cs?name=snippet1)]

Метод `OnGet` страничной модели возвращает строку со значениями параметров (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example3)]

Когда приложение выполняется, метод `OnGet` возвращает строку со значениями класса подпараметров:

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>Параметры, предоставляемые моделью представления или посредством прямого внедрения представления

Параметры, предоставляемые моделью представления или посредством прямого внедрения представления, демонстрируются в примере &num;4 в примере приложения.

Параметры могут передаваться в модель представления или путем внедрения <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> непосредственно в представление (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example4)]

В примере приложения показано, как внедрить `IOptionsMonitor<MyOptions>` с директивой `@inject`.

[!code-cshtml[](options/samples/2.x/OptionsSample/Pages/Index.cshtml?range=1-10&highlight=4)]

Когда запускается приложение, значения параметров появляются на отображаемой странице:

![Значения параметров Option1: value1_from_json и Option2: –1 загружаются из модели и путем внедрения в представление.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>Повторная загрузка данных конфигурации с помощью IOptionsSnapshot

Повторная загрузка данных конфигурации с помощью <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> демонстрируется в примере &num;5 в примере приложения.

Интерфейс <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> поддерживает повторную загрузку параметров с минимальными затратами на обработку.

Параметры вычисляются один раз на каждый запрос при обращении к ним и кэшируются на все время существования запроса.

В приведенном ниже примере демонстрируется создание экземпляра <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> после изменения файла *appsettings.json* (*Pages/Index.cshtml.cs*). Несколько запросов к серверу возвращают константные значения, предоставляемые файлом *appsettings.json*, пока файл не изменится и конфигурация не загрузится повторно.

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example5)]

Ниже показаны начальные значения `option1` и `option2`, загруженные из файла *appsettings.json*.

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

Измените значения в файле *appsettings.json* на `value1_from_json UPDATED` и `200`. Сохраните файл *appsettings.json*. Обновите окно браузера, чтобы увидеть обновленные значения параметров:

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a>Поддержка именованных параметров в IConfigureNamedOptions

Включение поддержки именованных параметров в <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> демонстрируется в примере &num;6 в примере приложения.

Поддержка *именованных параметров* позволяет приложению различать конфигурации именованных параметров. В примере приложения именованные параметры должны быть объявлены с помощью элемента [OptionsServiceCollectionExtensions.Configure](xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.Configure*), который вызывает метод расширения [ConfigureNamedOptions\<TOptions>.Configure](xref:Microsoft.Extensions.Options.ConfigureNamedOptions`1.Configure*):

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example6)]

Пример приложения обращается к именованным параметрам с помощью метода <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1.Get*> (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example6)]

При запуске образца приложения возвращаются именованные параметры:

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

Значения `named_options_1` предоставляются из конфигурации, которая загружается из файла *appsettings.json*. Значения `named_options_2` предоставляются следующим образом:

* Делегатом `named_options_2` в `ConfigureServices` для `Option1`.
* Значение по умолчанию для `Option2` предоставляется классом `MyOptions`.

## <a name="configure-all-options-with-the-configureall-method"></a>Настройка всех параметров с помощью метода ConfigureAll

Настройте все экземпляры параметров с помощью метода <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*>. Приведенный ниже код настраивает `Option1` для всех экземпляров конфигурации с общим значением. Добавьте следующий код в метод `Startup.ConfigureServices` вручную:

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

Если запустить образец приложения после добавления, результат будет следующим:

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> Все параметры являются именованными экземплярами. Существующие экземпляры <xref:Microsoft.Extensions.Options.IConfigureOptions`1> считаются нацеленными на экземпляр `Options.DefaultName`, который имеет значение `string.Empty`. Интерфейс <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> также реализует интерфейс <xref:Microsoft.Extensions.Options.IConfigureOptions`1>. Реализация <xref:Microsoft.Extensions.Options.IOptionsFactory`1> по умолчанию содержит логику для надлежащего использования каждого экземпляра. Именованный параметр `null` предназначен для всех именованных экземпляров, а не для какого-то определенного (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*> и <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*> следуют этому соглашению).

## <a name="optionsbuilder-api"></a>API OptionsBuilder

<xref:Microsoft.Extensions.Options.OptionsBuilder`1> используется для настройки экземпляров `TOptions`. `OptionsBuilder` упрощает создание именованных параметров, так как он является единственным параметром для первоначального вызова `AddOptions<TOptions>(string optionsName)` и не должен появляться во всех последующих вызовах. Проверка параметров и перегрузки `ConfigureOptions`, принимающие зависимости службы, доступны только через `OptionsBuilder`.

```csharp
// Options.DefaultName = "" is used.
services.AddOptions<MyOptions>().Configure(o => o.Property = "default");

services.AddOptions<MyOptions>("optionalName")
    .Configure(o => o.Property = "named");
```

## <a name="use-di-services-to-configure-options"></a>Использование служб внедрения зависимостей для настройки параметров

Вы можете получить доступ к другим службам, доступным в результате внедрения зависимостей при настройке параметров, двумя способами.

* Передайте делегат конфигурации методу [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) в [OptionsBuilder\<TOptions >](xref:Microsoft.Extensions.Options.OptionsBuilder`1). [OptionsBuilder\<TOptions >](xref:Microsoft.Extensions.Options.OptionsBuilder`1) предоставляет перегрузки метода [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*), которые позволяют использовать до пяти служб для настройки параметров:

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<Service1, Service2, Service3, Service4, Service5>(
          (o, s, s2, s3, s4, s5) => 
              o.Property = DoSomethingWith(s, s2, s3, s4, s5));
  ```

* Создайте собственный тип, реализующий <xref:Microsoft.Extensions.Options.IConfigureOptions`1> или <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>, и зарегистрируйте этот тип как службу.

Рекомендуем передать делегат конфигурации методу [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*), так как создать службу сложнее. Создание собственного типа эквивалентно тому, что делает платформа при использовании метода [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*). При вызове метода [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) регистрируется временный универсальный интерфейс <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>, имеющий конструктор, который принимает указанные универсальные типы службы. 

::: moniker range=">= aspnetcore-2.2"

## <a name="options-validation"></a>Проверка параметров

Эта функция позволяет проверить параметры при их настройке. Вызовите `Validate` с использованием метода проверки, который возвращает `true`, если параметры являются допустимыми, и `false`, если они являются недопустимыми:

```csharp
// Registration
services.AddOptions<MyOptions>("optionalOptionsName")
    .Configure(o => { }) // Configure the options
    .Validate(o => YourValidationShouldReturnTrueIfValid(o), 
        "custom error");

// Consumption
var monitor = services.BuildServiceProvider()
    .GetService<IOptionsMonitor<MyOptions>>();
  
try
{
    var options = monitor.Get("optionalOptionsName");
}
catch (OptionsValidationException e) 
{
   // e.OptionsName returns "optionalOptionsName"
   // e.OptionsType returns typeof(MyOptions)
   // e.Failures returns a list of errors, which would contain 
   //     "custom error"
}
```

В предыдущем примере для именованного экземпляра параметров задается `optionalOptionsName`. Экземпляр параметров по умолчанию — `Options.DefaultName`.

Проверка выполняется при создании экземпляра параметров. Экземпляр параметров гарантированно проходит проверку при первом обращении.

> [!IMPORTANT]
> Проверка параметров не защищает от изменений, вносимых после исходной настройки и проверки параметров.

Метод `Validate` принимает `Func<TOptions, bool>`. Чтобы полностью настроить проверку, реализуйте `IValidateOptions<TOptions>`, чтобы:

* выполнить проверку нескольких типов параметров — `class ValidateTwo : IValidateOptions<Option1>, IValidationOptions<Option2>`;
* выполнить проверку, зависящую от другого типа параметра — `public DependsOnAnotherOptionValidator(IOptionsMonitor<AnotherOption> options)`.

`IValidateOptions` проверяет:

* определенный именованный экземпляр параметров;
* все параметры, при которых `name` имеет значение `null`.

Возвращает `ValidateOptionsResult` из реализации интерфейса:

```csharp
public interface IValidateOptions<TOptions> where TOptions : class
{
    ValidateOptionsResult Validate(string name, TOptions options);
}
```

Проверка на основе заметок к данным доступна в пакете [Microsoft.Extensions.Options.DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) с помощью вызова метода `ValidateDataAnnotations` в `OptionsBuilder<TOptions>`. `Microsoft.Extensions.Options.DataAnnotations` входит в состав [метапакета Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) (ASP.NET Core 2.2 или более поздней версии).

```csharp
private class AnnotatedOptions
{
    [Required]
    public string Required { get; set; }

    [StringLength(5, ErrorMessage = "Too long.")]
    public string StringLength { get; set; }

    [Range(-5, 5, ErrorMessage = "Out of range.")]
    public int IntRange { get; set; }
}

[Fact]
public void CanValidateDataAnnotations()
{
    var services = new ServiceCollection();
    services.AddOptions<AnnotatedOptions>()
        .Configure(o =>
        {
            o.StringLength = "111111";
            o.IntRange = 10;
            o.Custom = "nowhere";
        })
        .ValidateDataAnnotations();

    var sp = services.BuildServiceProvider();

    var error = Assert.Throws<OptionsValidationException>(() => 
        sp.GetRequiredService<IOptionsMonitor<AnnotatedOptions>>().Value);
    ValidateFailure<AnnotatedOptions>(error, Options.DefaultName, 1,
        "DataAnnotation validation failed for members Required " +
            "with the error 'The Required field is required.'.",
        "DataAnnotation validation failed for members StringLength " +
            "with the error 'Too long.'.",
        "DataAnnotation validation failed for members IntRange " +
            "with the error 'Out of range.'.");
}
```

Безотложная проверка (быстрое прекращение при запуске) находится на этапе рассмотрения для включения в будущие выпуски.

::: moniker-end

## <a name="options-post-configuration"></a>Пост-конфигурация параметров

Задайте пост-конфигурацию с помощью <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1>. Пост-конфигурация применяется после выполнения всех действий настройки с помощью <xref:Microsoft.Extensions.Options.IConfigureOptions`1>.

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

Для последующей настройки именованных параметров доступен метод <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1.PostConfigure*>.

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

Для последующей настройки всех экземпляров конфигурации служит метод <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*>.

```csharp
services.PostConfigureAll<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="accessing-options-during-startup"></a>Доступ к параметрам во время запуска

<xref:Microsoft.Extensions.Options.IOptions`1> и <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> можно использовать в методе `Startup.Configure`, так как службы создаются до выполнения метода `Configure`.

```csharp
public void Configure(IApplicationBuilder app, IOptionsMonitor<MyOptions> optionsAccessor)
{
    var option1 = optionsAccessor.CurrentValue.Option1;
}
```

Не используйте <xref:Microsoft.Extensions.Options.IOptions`1> или <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> в `Startup.ConfigureServices`. Из-за очередности регистрации служб состояние параметров может быть несогласованным.

## <a name="additional-resources"></a>Дополнительные ресурсы

* <xref:fundamentals/configuration/index>
