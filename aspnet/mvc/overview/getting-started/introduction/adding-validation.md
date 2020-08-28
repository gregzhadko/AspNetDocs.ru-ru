---
uid: mvc/overview/getting-started/introduction/adding-validation
title: Добавление проверки | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 4e2d83cdff8599d74182da1be1aaabd1a431799c
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044354"
---
# <a name="adding-validation"></a>Добавление проверки

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

В этом разделе вы добавите логику проверки в `Movie` модель, и вы убедитесь, что правила проверки применяются каждый раз, когда пользователь попытается создать или изменить фильм с помощью приложения.

## <a name="keeping-things-dry"></a>Поддержание СУХИх вещей

Один из основных принципов проектирования ASP.NET MVC — [сухой](http://en.wikipedia.org/wiki/Don't_repeat_yourself) ( &quot; принцип "не повторяйся" &quot; ). ASP.NET MVC позволяет указать функциональные возможности или поведение только один раз, после чего они будут отражены в любом приложении. Это сокращает объем кода, который необходимо написать, и делает код менее подверженным ошибкам и проще в обслуживании.

Поддержка проверки, предоставляемая ASP.NET MVC и Entity Framework Code First, является хорошим примером принципа сухой в действии. Правила проверки можно декларативно задавать в одном месте (в классе Model), а правила применяются везде в приложении.

Рассмотрим, как можно воспользоваться преимуществами этой поддержки проверки в приложении Movie.

## <a name="adding-validation-rules-to-the-movie-model"></a>Добавление правил проверки к модели фильмов

Начнем с добавления в класс логики проверки `Movie` .

Откройте файл *Movie.cs*. Обратите внимание, что [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) пространство имен не содержит `System.Web` . Аннотации данных предоставляют встроенный набор атрибутов проверки, которые можно декларативно применять к любому классу или свойству. (Он также содержит атрибуты форматирования, такие как [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , которые помогают в форматировании и не обеспечивают проверку.)

Теперь обновите `Movie` класс, чтобы воспользоваться преимуществами встроенных [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) атрибутов, [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)и [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) проверки. Замените `Movie` класс следующим:

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

[`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)Атрибут задает максимальную длину строки и устанавливает это ограничение для базы данных, поэтому схема базы данных изменится. Щелкните правой кнопкой мыши таблицу **фильмов** в **обозревателе сервера** и выберите пункт **Открыть определение таблицы**:

![](adding-validation/_static/image1.png)

На изображении выше можно увидеть, что все строковые поля имеют значение [nvarchar (max)](https://technet.microsoft.com/library/ms186939.aspx). Для обновления схемы мы будем использовать миграции. Выполните сборку решения, а затем откройте окно **консоли диспетчера пакетов** и введите следующие команды:

[!code-console[Main](adding-validation/samples/sample2.cmd)]

По завершении этой команды Visual Studio открывает файл класса, который определяет новый `DbMigration` производный класс с указанным именем ( `DataAnnotations` ), и в `Up` методе можно увидеть код, который обновляет ограничения схемы:

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

`Genre`Поле больше не может быть пустым (то есть необходимо ввести значение). `Rating`Максимальная длина поля равна 5, а `Title` Максимальная длина — 60. Минимальная длина 3 в `Title` и диапазон в `Price` не удалось создать изменения схемы.

Изучите схему фильма:

![](adding-validation/_static/image2.png)

Строковые поля показывают новые ограничения длины и `Genre` больше не проверяются как допускающие значение null.

Атрибуты проверки определяют поведение для свойств модели, к которым они применяются. Атрибуты `Required` и `MinimumLength` указывают, что свойство должно иметь значение. Тем не менее, чтобы удовлетворить требованиям проверки, пользователю достаточно ввести пробел. Атрибут [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) используется для ограничения того, какие символы могут быть введены. В приведенном выше коде в полях `Genre` и `Rating` можно использовать только буквы (пробелы, числа и специальные символы не допускаются). [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)Атрибут ограничивает значение в пределах указанного диапазона. Атрибут `StringLength` позволяет задать максимальную и при необходимости минимальную длину строкового свойства. Типы значений (например, `decimal, int, float, DateTime` ) по сути являются обязательными и не требуют `Required` атрибута.

Code First гарантирует, что правила проверки, указанные в классе модели, будут применены, прежде чем приложение сохранит изменения в базе данных. Например, приведенный ниже код вызывает исключение [дбентитивалидатионексцептион](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) при `SaveChanges` вызове метода, поскольку отсутствуют некоторые обязательные `Movie` значения свойств:

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

Приведенный выше код вызывает следующее исключение:

*Проверка не пройдена для одной или нескольких сущностей. Дополнительные сведения см. в свойстве "Ентитивалидатионеррорс".*

Если правила проверки автоматически принудительно применяются .NET Framework помогает сделать приложение более надежным. Это также гарантирует, что в любом случае будут выполнены все проверки и в базе данных не будут случайно оставлены поврежденные данные.

## <a name="validation-error-ui-in-aspnet-mvc"></a>Пользовательский интерфейс ошибки проверки в ASP.NET MVC

Запустите приложение и перейдите по URL-адресу */Movies* .

Щелкните ссылку **создать** , чтобы добавить новый фильм. Введите в форму какие-либо недопустимые значения. Если функция проверки jQuery на стороне клиента обнаруживает ошибку, сведения о ней отображаются в соответствующем сообщении.

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> для поддержки проверки jQuery для национальных стандартов, отличных от английского, которые используют запятую (",") для десятичной запятой, необходимо включить параметр "глобализация NuGet", как описано выше в этом руководстве.

Обратите внимание, что форма автоматически использовала красный цвет границы для выделения текстовых полей, содержащих недопустимые данные, и выдает соответствующее сообщение об ошибке проверки рядом с каждым из них. Эти ошибки применяются как на стороне клиента (с помощью JavaScript и jQuery), так и на стороне сервера (если пользователь отключает JavaScript).

Настоящим преимуществом является то, что вам не пришлось изменять одну строку кода в `MoviesController` классе или в представлении *Create. cshtml* , чтобы включить этот пользовательский интерфейс проверки. В контроллере и представлениях, создаваемых в рамках этого руководства, автоматически применяются правила проверки, для определения которых к свойствам класса модели `Movie` были применены атрибуты. При проверке с использованием метода действия `Edit` применяются те же правила.

Данные формы передаются на сервер только после того, как будут устранены любые ошибки на стороне клиента. Это можно проверить, поместив точку останова в метод HTTP POST с помощью [средства Fiddler](http://fiddler2.com/fiddler2/)или [средств РАЗРАБОТЧИКА F12](https://msdn.microsoft.com/ie/aa740478)для IE.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Как выполняется проверка в методе создания представления и создания действия

Вам может быть интересно, как пользовательский интерфейс проверки создается без обновления кода контроллера или представлений. В следующем листинге показано, `Create` `MovieController` как выглядят методы в классе. Они не изменяются из того, как вы создали их ранее в этом руководстве.

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

Первый метод действия `Create` (HTTP GET) отображает исходную форму создания. Вторая версия (`[HttpPost]`) обрабатывает передачу формы. Второй `Create` метод ( `HttpPost` версия) проверяет, `ModelState.IsValid` имеются ли в фильме ошибки проверки. При получении этого свойства оцениваются все атрибуты проверки, примененные к объекту. Если объект содержит ошибки проверки, метод повторно `Create` отображает форму. Если ошибок нет, метод сохраняет новый фильм в базе данных. В нашем примере с фильмом **форма не отправляется на сервер при обнаружении ошибок проверки на стороне клиента; второй** `Create` **метод никогда не вызывается**. При отключении JavaScript в браузере проверка клиента отключается, и метод HTTP POST `Create` получает, `ModelState.IsValid` чтобы проверить, имеются ли в фильме ошибки проверки.

Вы можете установить точку останова в метод `HttpPost Create` и убедиться, что он не вызывается и данные формы не передаются, если на стороне клиента присутствуют ошибки проверки. Если отключить JavaScript в браузере и отправить форму с ошибками, будет достигнута точка останова. Без JavaScript вы по-прежнему будете получать полную проверку. На следующем рисунке показано, как отключить JavaScript в Internet Explorer.

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

На следующем рисунке показано, как отключить JavaScript в браузере FireFox.

![](adding-validation/_static/image7.png)

На следующем рисунке показано, как отключить JavaScript в браузере Chrome.

![](adding-validation/_static/image8.png)

Ниже приведен шаблон представления *Create. cshtml* , сформированный ранее в этом руководстве. Он используется в показанных выше методах действия для отображения исходной формы и повторного вывода формы в случае ошибки.

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

Обратите внимание, что код использует `Html.EditorFor` вспомогательный метод для вывода `<input>` элемента для каждого `Movie` Свойства. Рядом с этим вспомогательным методом находится вызов `Html.ValidationMessageFor` вспомогательного метода. Эти два вспомогательных метода работают с объектом модели, который передается контроллером в представление (в данном случае это `Movie` объект). Они автоматически ищут атрибуты проверки, указанные в модели, и отображают сообщения об ошибках соответствующим образом.

Этот подход удобен тем, что ни контроллер, ни шаблон представления `Create` ничего не знают о фактически применяемых правилах проверки или отображаемых сообщениях об ошибках. Правила проверки и строки ошибок указываются только в классе `Movie`. Такие же правила проверки автоматически применяются к представлению `Edit` и любым другим представлениям модели, которые вы можете создавать или редактировать.

Если вы хотите изменить логику проверки позже, это можно сделать в одном месте, добавив атрибуты проверки в модель (в этом примере это `movie` класс). Вам не придется беспокоиться о несогласованности применения правил в различных частях приложения, поскольку вся логика проверки будет определена в одном месте и начнет применяться по всему приложению. Это позволяет максимально оптимизировать код и обеспечить удобство его совершенствования и поддержки. Это означает, что вы будете полностью учитывать принцип *сухой* .

## <a name="using-datatype-attributes"></a>Использование атрибутов DataType

Откройте файл *Movie.cs* и проверьте класс `Movie`. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)В дополнение к встроенному набору атрибутов проверки пространство имен предоставляет атрибуты форматирования. Мы уже применили [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) значение перечисления к дате выпуска и к полям цены. В следующем коде показаны `ReleaseDate` Свойства и `Price` с соответствующим [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) атрибутом.

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) предоставляют подсистеме представления только указания для форматирования данных (и предоставляют атрибуты, например, `<a>` для URL-адресов и `<a href="mailto:EmailAddress.com">` для электронной почты. Для проверки формата данных можно использовать атрибут [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) . Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) используется для указания типа данных, более конкретного, чем внутренний тип базы данных, они ***не*** являются атрибутами проверки. В этом случае требуется отслеживать только дату, а не дату и время. [Перечисление DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) предоставляет множество типов данных, таких как *Date, Time, PhoneNumber, Currency, EmailAddress* и др. Атрибут `DataType` также обеспечивает автоматическое предоставление функций для определенных типов в приложении. Например, `mailto:` можно создать ссылку для [DataType. EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), а также можно указать средство выбора даты для [типа данных. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) в браузерах, поддерживающих [HTML5](http://html5.org/). Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) создают атрибуты HTML 5 [Data-](http://ejohn.org/blog/html-5-data-attributes/) (произносит *штрих данных*), которые могут быть понятны браузерам HTML 5. Атрибуты [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) не обеспечивают никакой проверки.

`DataType.Date` не задает формат отображаемой даты. По умолчанию поле данных отображается в соответствии с форматами по умолчанию, основанными на [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)сервера.

С помощью атрибута `DisplayFormat` можно явно указать формат даты:

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

`ApplyFormatInEditMode`Параметр указывает, что указанное форматирование также должно применяться при отображении значения в текстовом поле для редактирования. (Для некоторых полей, например для денежных значений, может потребоваться не использовать символ валюты в текстовом поле для редактирования.)

Атрибут [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) можно использовать отдельно, но обычно рекомендуется использовать атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) . `DataType`Атрибут передает *семантику* данных, в отличие от того, как она отображается на экране, и предоставляет следующие преимущества, которые не получаются `DisplayFormat` .

- Браузер может включить функции HTML5 (например, отобразить элемент управления "Календарь", соответствующий языковой стандарт символ валюты, ссылки электронной почты и т. д.).
- По умолчанию браузер будет отображать данные с использованием правильного формата в зависимости от [языкового стандарта](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- С помощью атрибута [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) можно выбрать подходящий шаблон поля для подготовки к просмотру данных ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , если он используется, использует строковый шаблон). Дополнительные сведения см. в статье о [шаблонах ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)Михаил Уилсон (. (Хотя написано для MVC 2, эта статья по-прежнему применяется к текущей версии ASP.NET MVC.)

При использовании `DataType` атрибута с полем даты необходимо `DisplayFormat` также указать атрибут, чтобы обеспечить правильное отображение поля в браузерах Chrome. Дополнительные сведения см. в [этом потоке StackOverflow](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

> [!NOTE]
> проверка jQuery не работает с атрибутом [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) и [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx). Например, следующий код всегда приводит к возникновению ошибки проверки на стороне клиента, даже если дата попадает в указанный диапазон:
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> Необходимо отключить проверку даты jQuery, чтобы использовать атрибут [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) с [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx). Обычно не рекомендуется компилировать жесткие даты в моделях, поэтому использование атрибута [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) и [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) не рекомендуется.

В следующем коде демонстрируется объединение атрибутов в одной строке:

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

В следующей части этой серии мы рассмотрим приложение и внесем ряд изменений в автоматически создаваемые методы `Details` и `Delete`.

> [!div class="step-by-step"]
> [Назад](adding-a-new-field.md)
> [Вперед](examining-the-details-and-delete-methods.md)
