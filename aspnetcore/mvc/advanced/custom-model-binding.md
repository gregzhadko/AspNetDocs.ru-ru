---
title: Пользовательская привязка модели в ASP.NET Core
author: ardalis
description: Узнайте, как привязка модели позволяет действиям контроллера работать непосредственно с типами модели в ASP.NET Core.
ms.author: riande
ms.date: 11/13/2018
uid: mvc/advanced/custom-model-binding
ms.openlocfilehash: 33551c9fc22561b992b4a09a4c7187ade136c09c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057081"
---
# <a name="custom-model-binding-in-aspnet-core"></a>Пользовательская привязка модели в ASP.NET Core

Автор: [Стив Смит](https://ardalis.com/) (Steve Smith)

Привязка модели позволяет действиям контроллера работать непосредственно с типами моделей (передаваемыми в качестве аргументов метода), а не с HTTP-запросами. Сопоставление между данными входящего запроса и моделями приложений обрабатывается связывателями моделей. Разработчики могут расширить функциональность привязки встроенных модели путем реализации настраиваемых связывателей (хотя обычно создавать собственный поставщик не требуется).

[Просмотреть или скачать образец с GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-model-binding/)

## <a name="default-model-binder-limitations"></a>Ограничения для связывателя модели по умолчанию

Связыватели моделей по умолчанию поддерживают значительную часть распространенных типов данных .NET Core и должны соответствовать большинству требований разработчиков. Ожидается, что они будут привязывать текстовые входные данные из запроса непосредственно к типам моделей. Перед привязкой может потребоваться преобразовать входные данные. Например, у вас есть ключ, используемый для поиска данных модели. Для выборки данных на основе ключа можно воспользоваться настраиваемым связывателем модели.

## <a name="model-binding-review"></a>Обзор привязки модели

Для типов, с которыми работает привязка данных, используются специальные определения. *Простой тип* преобразуется из одной строки во входных данных. *Сложный тип* преобразуется из нескольких входных значений. Платформа определяет их различие в зависимости от наличия `TypeConverter`. Если у вас есть простое сопоставление `string` -> `SomeType`, не требующее внешних ресурсов, рекомендуется создать преобразователь типов.

Прежде чем создавать собственный настраиваемый связыватель модели, следует понять реализацию существующих связывателей моделей. Рассмотрим класс [ByteArrayModelBinder](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinder), который используется для преобразования строк в кодировке Base64 в массивы байтов. Массивы байтов часто хранятся в виде файлов или полей больших двоичных объектов базы данных.

### <a name="working-with-the-bytearraymodelbinder"></a>Работа с классом ByteArrayModelBinder

Строки в кодировке Base64 можно использовать для представления двоичных данных. Например, приведенное ниже изображение можно закодировать в виде строки.

![бот dotnet](custom-model-binding/images/bot.png "бот dotnet")

На следующем рисунке показана небольшая часть закодированной строки:

![закодированный бот dotnet](custom-model-binding/images/encoded-bot.png "закодированный бот dotnet")

Чтобы преобразовать строку в кодировке Base64 в файл, следуйте инструкциям в [файле README](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/advanced/custom-model-binding/sample/CustomModelBindingSample/README.md).

ASP.NET Core MVC может принимать строки в кодировке Base64 и использовать `ByteArrayModelBinder` для их преобразования в массив байтов. Класс [ByteArrayModelBinderProvider](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinderprovider), реализующий интерфейс [IModelBinderProvider](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.imodelbinderprovider), сопоставляет аргументы `byte[]` с `ByteArrayModelBinder`:

```csharp
public IModelBinder GetBinder(ModelBinderProviderContext context)
{
    if (context == null)
    {
        throw new ArgumentNullException(nameof(context));
    }

    if (context.Metadata.ModelType == typeof(byte[]))
    {
        return new ByteArrayModelBinder();
    }

    return null;
}
```

При создании собственного настраиваемого связывателя модели можно реализовать собственный тип `IModelBinderProvider` или воспользоваться [ModelBinderAttribute](/dotnet/api/microsoft.aspnetcore.mvc.modelbinderattribute).

В следующем примере показано, как использовать `ByteArrayModelBinder` для преобразования строки в кодировке Base64 в `byte[]` и сохранить результат в файл:

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/ImageController.cs?name=post1&highlight=3)]

Строку в кодировке Base64 можно отправить (POST) в этот метод API с помощью такого средства, как [Postman](https://www.getpostman.com/):

![postman](custom-model-binding/images/postman.png "postman")

Привязка модели успешно выполняется до тех пор, пока связыватель может привязывать данные запроса к свойствам или аргументам с соответствующими именами. В приведенном ниже примере показано, как использовать `ByteArrayModelBinder` с моделью представления.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/ImageController.cs?name=post2&highlight=2)]

## <a name="custom-model-binder-sample"></a>Образец настраиваемого связывателя модели

В этом разделе будет реализован настраиваемый связыватель модели, который выполняет следующий действия:

- преобразует данные входящего запроса в строго типизированные аргументы ключа;
- использует Entity Framework Core для получения связанной сущности;
- передает связанную сущность в качестве аргумента в метод действия.

В следующем примере используется атрибут `ModelBinder` в модели `Author`:

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Data/Author.cs?highlight=10)]

В приведенном выше коде атрибут `ModelBinder` указывает тип `IModelBinder`, который следует использовать для привязки параметров действия `Author`.

Следующий класс `AuthorEntityBinder` привязывает параметр `Author` путем получения сущности из источника данных с помощью Entity Framework Core и `authorId`:

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Binders/AuthorEntityBinder.cs?name=demo)]

> [!NOTE]
> Предыдущий класс `AuthorEntityBinder` предназначен для демонстрации пользовательского связывателя модели. Класс не предназначен для демонстрации рекомендаций для использования сценария просмотра. Чтобы выполнить просмотр, привяжите `authorId` и отправьте запрос к базе данных в методе действия. Этот подход отделяет ошибки привязки модели от вариантов `NotFound`.

В следующем примере кода демонстрируется использование `AuthorEntityBinder` в методе действия.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/BoundAuthorsController.cs?name=demo2&highlight=2)]

С помощью атрибута `ModelBinder` можно применять `AuthorEntityBinder` к параметрам, которые не используют соглашения по умолчанию:

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/BoundAuthorsController.cs?name=demo1&highlight=2)]

Поскольку в этом примере имя аргумента не является `authorId` по умолчанию, оно указывается в параметре с помощью атрибута `ModelBinder`. Обратите внимание, что функционал контроллера и метода действия упрощен по сравнению с поиском сущности в методе действия. Логика для выборки автора с использованием Entity Framework Core перемещается в связыватель модели. Такой подход позволит существенно упростить работу, если у вас есть несколько методов для привязки к модели `Author`.

Чтобы указать определенный связыватель модели или имя только для данного типа или действия, можно применить атрибут `ModelBinder` к свойствам отдельной модели (таким как viewmodel) или к параметрам метода действия.

### <a name="implementing-a-modelbinderprovider"></a>Реализация класса ModelBinderProvider

Вместо применения атрибута можно реализовать класс `IModelBinderProvider`. Таким образом реализуются встроенные связыватели платформы. При указании типа, с которым работает связыватель, определяется тип создаваемого им аргумента, а **не** принимаемые им входные данные. Следующий поставщик связывателей работает с `AuthorEntityBinder`. Если он добавляется в коллекцию поставщиков MVC, не нужно использовать атрибут `ModelBinder` в типизированных параметрах `Author` или `Author`.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Binders/AuthorEntityBinderProvider.cs?highlight=17-20)]

> Примечание. Приведенный выше код возвращает `BinderTypeModelBinder`. `BinderTypeModelBinder` выступает в качестве фабрики для связывателей моделей и обеспечивает внедрение зависимостей (DI). Для доступа к EF Core классу `AuthorEntityBinder` требуется внедрение зависимостей. Если связывателю модели необходимы службы из DI, используйте класс `BinderTypeModelBinder`.

Чтобы начать работу с настраиваемым поставщиком связывателей моделей, добавьте его в `ConfigureServices`:

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Startup.cs?name=callout&highlight=5-9)]

При оценке связывателей моделей коллекция поставщиков проверяется в определенном порядке. Используется первый поставщик, который возвращает связыватель.

На следующем рисунке показаны заданные по умолчанию связыватели моделей из отладчика.

![связыватели моделей по умолчанию](custom-model-binding/images/default-model-binders.png "связыватели моделей по умолчанию")

Добавление поставщика в конец коллекции может привести к вызову встроенного связывателя модели раньше, чем будет вызван ваш собственный настраиваемый связыватель. В этом примере настраиваемый поставщик добавляется в начало коллекции, чтобы использоваться для аргументов действия `Author`.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Startup.cs?name=callout&highlight=5-9)]

## <a name="recommendations-and-best-practices"></a>Рекомендации и советы

Ниже приведены рекомендации относительно настраиваемых связывателей моделей.

- Связыватели моделей не следует использовать для установки кодов состояния или возвращаемых результатов (например, "404 — не найдено"). При сбое привязки модели обрабатывать ошибку должен сам [фильтр действий](xref:mvc/controllers/filters) или логика в самом методе действия.
- Связыватели наиболее полезны в сценариях исключения повторяющихся частей кода и решения взаимосвязанных проблем с методами действий.
- Как правило, связыватели не следует использовать для преобразования строки в пользовательский тип. Лучшим вариантом обычно является [`TypeConverter`](/dotnet/api/system.componentmodel.typeconverter).
