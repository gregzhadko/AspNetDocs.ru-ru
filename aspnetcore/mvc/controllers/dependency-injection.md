---
title: Внедрение зависимостей в контроллеры в ASP.NET Core
author: ardalis
description: Узнайте, как контроллеры MVC ASP.NET Core явным образом запрашивают зависимости с помощью конструкторов с внедрением зависимостей в ASP.NET Core.
ms.author: riande
ms.date: 02/24/2019
uid: mvc/controllers/dependency-injection
ms.openlocfilehash: 898e98f4c5d472ca96c6a8ad07dddd1a4ef54fe9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063981"
---
# <a name="dependency-injection-into-controllers-in-aspnet-core"></a>Внедрение зависимостей в контроллеры в ASP.NET Core

<a name="dependency-injection-controllers"></a>

Авторы: [Shadi Namrouti](https://github.com/shadinamrouti) (Шади Намрути), [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Стив Смит](https://github.com/ardalis) (Steve Smith)

Контроллеры ASP.NET Core MVC запрашивают зависимости явно с помощью конструкторов. ASP.NET Core имеет встроенную поддержку [внедрения зависимостей (DI)](xref:fundamentals/dependency-injection). Внедрение зависимостей упрощает тестирование и поддержку приложений.

[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/dependency-injection/sample) ([как скачивать](xref:index#how-to-download-a-sample))

## <a name="constructor-injection"></a>Внедрение через конструктор

Службы добавляются в качестве параметра конструктора, и среда выполнения разрешает службу из контейнера служб. Службы обычно задаются с помощью интерфейсов. Например, рассмотрим приложение, которому требуется текущее время. Следующие интерфейсы предоставляют службу `IDateTime`:

[!code-csharp[](dependency-injection/sample/ControllerDI/Interfaces/IDateTime.cs?name=snippet)]

В следующем коде реализуется интерфейс `IDateTime`:

[!code-csharp[](dependency-injection/sample/ControllerDI/Services/SystemDateTime.cs?name=snippet)]

Добавьте службу в контейнер службы:

[!code-csharp[](dependency-injection/sample/ControllerDI/Startup1.cs?name=snippet&highlight=3)]

Дополнительные сведения о <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionServiceExtensions.AddSingleton*>, см. в разделе [Время существования службы внедрения зависимости](xref:fundamentals/dependency-injection#service-lifetimes).

Следующий код отображает приветствие пользователю в зависимости от времени дня:

[!code-csharp[](dependency-injection/sample/ControllerDI/Controllers/HomeController.cs?name=snippet)]

Запустите приложение, и в зависимости от времени отобразится сообщение.

## <a name="action-injection-with-fromservices"></a>Внедрение действий с помощью FromServices

<xref:Microsoft.AspNetCore.Mvc.FromServicesAttribute> позволяет внедрять службу непосредственно в метод действия без использования внедрения через конструктор:

[!code-csharp[](dependency-injection/sample/ControllerDI/Controllers/HomeController.cs?name=snippet2)]

## <a name="access-settings-from-a-controller"></a>Доступ к параметрам из контроллера

Доступ к параметрам приложения или конфигурации из контроллера относится к типичным шаблонам. *Шаблон параметров*, описанный в разделе <xref:fundamentals/configuration/options>, является предпочтительным подходом для управления параметрами. Как правило, не следует напрямую внедрять <xref:Microsoft.Extensions.Configuration.IConfiguration> в контроллер.

Создайте класс, представляющий параметры. Пример:

[!code-csharp[](dependency-injection/sample/ControllerDI/Models/SampleWebSettings.cs?name=snippet)]

Добавьте класс конфигурации в коллекцию служб:

[!code-csharp[](dependency-injection/sample/ControllerDI/Startup.cs?highlight=4&name=snippet1)]

Настройте приложение для чтения параметров из файла формата JSON:

[!code-csharp[](dependency-injection/sample/ControllerDI/Program.cs?name=snippet&range=10-15)]

Следующий код запрашивает параметры `IOptions<SampleWebSettings>` из контейнера служб и использует их в методе `Index`:

[!code-csharp[](dependency-injection/sample/ControllerDI/Controllers/SettingsController.cs?name=snippet)]

## <a name="additional-resources"></a>Дополнительные ресурсы

* См. раздел <xref:mvc/controllers/testing>, чтобы узнать, как упростить тестирование кода, явно запросив зависимости у контроллеров.

* [Замените контейнер внедрения зависимостей по умолчанию на стороннюю реализацию](xref:fundamentals/dependency-injection#default-service-container-replacement).
