---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: Новые возможности ASP.NET MVC 2 | Документация Майкрософт
author: rick-anderson
description: В этом документе описаны новые функции и усовершенствования, появившиеся в ASP.NET MVC 2. Этот документ также доступен для загрузки.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045043"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>Новые возможности ASP.NET MVC 2

> В этом документе описаны новые функции и усовершенствования, появившиеся в ASP.NET MVC 2. Этот документ также доступен для [загрузки](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)

[Общие](#_TOC1)   
[Обновление проекта ASP.NET MVC 1,0 до ASP.NET MVC 2](#_TOC2)   
[Новые возможности](#_TOC3)   
[Шаблоны вспомогательных функций](#_TOC3_1)   
[Зон](#_TOC3_2)   
[Поддержка асинхронных контроллеров](#_TOC3_3)   
[Поддержка DefaultValueAttribute в параметрах метода действия](#_TOC3_4)   
[Поддержка привязки двоичных данных с помощью связывателей моделей](#_TOC3_5)   
[Классы ModelMetadata и Моделметадатапровидер](#_TOC3_6)   
[Поддержка атрибутов заметок к заметкам](#_TOC3_7)   
[Поставщики проверки модели](#_TOC3_8)   
[Проверка на стороне клиента](#_TOC3_9)   
[Новые фрагменты кода для Visual Studio 2010](#_TOC3_10)   
[Новый фильтр действий Рекуирехттпсаттрибуте](#_TOC3_11)   
[Переопределение глагола метода HTTP](#_TOC3_12)   
[Новый класс Хидденинпутаттрибуте для шаблонов вспомогательных функций](#_TOC3_13)   
[Вспомогательный метод HTML. ValidationSummary может отображать ошибки уровня модели](#_TOC3_14)   
[Шаблоны T4 в Visual Studio создают код, относящийся к целевой версии](#_TOC3_15)[улучшений API](#_TOC4) .NET Framework  
[Критические изменения](#_TOC5)  
[Отказ от ответственности](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  Общие

ASP.NET MVC 2 строится на ASP.NET MVC 1,0 и содержит большой набор усовершенствований и функций, которые нацелены на повышение производительности. Этот выпуск совместим с ASP.NET MVC 1,0, поэтому все ваши знания, навыки, код и расширения для ASP.NET MVC 1,0 продолжают действовать.

Дополнительные сведения о ASP.NET MVC см. в следующих ресурсах:

- [Документация по ASP.NET MVC на MSDN](https://go.microsoft.com/fwlink/?LinkId=159758)
- [Веб-сайт ASP.NET MVC](https://asp.net/mvc/)
- [Форумы ASP.NET MVC](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  Обновление проекта ASP.NET MVC 1,0 до ASP.NET MVC 2

ASP.NET MVC 2 может быть установлен параллельно с ASP.NET MVC 1,0 на том же сервере, что дает разработчикам возможность гибко выбирать время обновления приложения ASP.NET MVC 1,0 до ASP.NET MVC 2. Сведения о том, как выполнить обновление, см. в документе [Обновление приложения ASP.NET mvc 1,0 до ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).

## <a name="new-features"></a><a id="_TOC3"></a>  Новые возможности

В этом разделе описаны функции, которые появились в выпуске MVC 2.

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  Шаблоны вспомогательных функций

Шаблонные вспомогательные методы позволяют автоматически связывать элементы HTML для редактирования и вывода с типами данных. Например, если данные типа System. DateTime отображаются в представлении, элемент пользовательского интерфейса средства выбора даты может быть автоматически визуализирован. Это похоже на то, как шаблоны полей работают в ASP.NET платформа динамических данных. Дополнительные сведения см. в разделе [Использование шаблонов вспомогательных функций для вывода данных](https://go.microsoft.com/fwlink/?LinkId=159062) на веб-сайте MSDN.

### <a name="areas"></a><a id="_TOC3_2"></a>  Зон

Области позволяют организовать большой проект в несколько меньших разделов, чтобы управлять сложностью больших веб-приложений. Каждый раздел ("область") обычно представляет отдельный раздел крупного веб-узла и используется для группирования связанных наборов контроллеров и представлений. Дополнительные сведения см. в разделе [Пошаговое руководство. упорядочение приложения ASP.NET MVC по областям](https://go.microsoft.com/fwlink/?LinkId=158978) на веб-сайте MSDN.

Чтобы создать новую область, в обозреватель решений щелкните правой кнопкой мыши проект, выберите Добавить, а затем щелкните область. Откроется диалоговое окно с предложением ввести имя области. После ввода имени области Visual Studio добавит новую область в проект.

На следующем рисунке показан пример макета для проекта с двумя областями, администратором и блогами.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

При создании области Visual Studio добавляет класс, производный от AreaRegistration, к каждой области. Этот класс необходим для регистрации области и ее маршрутов, как показано в следующем примере:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

Шаблон проекта по умолчанию для ASP.NET MVC 2 включает вызов метода Регистераллареас в коде для файла Global. asax. Этот метод регистрирует каждую область проекта, ищут все типы, производные от класса AreaRegistration, создавая экземпляр типа, а затем вызывая метод Регистерареа в экземпляре. В следующем примере показано, как это сделать.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

Если не указать пространство имен в методе Регистерареа, вызвав контекст. Пространства имен. Add метод. по умолчанию используется пространство имен класса регистрации.

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  Поддержка асинхронных контроллеров

ASP.NET MVC 2 теперь позволяет контроллерам обрабатывать запросы асинхронно. Это может привести к повышению производительности, позволяя серверам, которые часто вызывают блокирующие операции (например, сетевые запросы), вызывать вместо них неблокирующие аналоги. Дополнительные сведения см. в разделе [Использование асинхронного контроллера в ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) в MSDN.

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  Поддержка DefaultValueAttribute в параметрах метода действия

Класс System. ComponentModel. DefaultValueAttribute позволяет предоставить значение по умолчанию для параметра-аргумента методу действия. Например, предположим, что определен следующий маршрут по умолчанию:

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

Также предположим, что определен следующий контроллер и метод действия:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

Любой из следующих URL-адресов запроса вызовет метод действия представления, определенный в предыдущем примере.

- /Article/View/123
- /Article/View/123? Page = 1 (фактически аналогично предыдущему запросу)
- /Article/View/123? стр. 2

Без атрибута DefaultValueAttribute первый URL-адрес из предыдущего списка не будет работать, поскольку аргумент Page является типом значения, не допускающим значения NULL, значение которого не было предоставлено.

Если код написан на Visual Basic 2010 или Visual C# 2010, можно использовать необязательные параметры вместо атрибута DefaultValueAttribute, как показано в следующем примере:

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  Поддержка привязки двоичных данных с помощью связывателей моделей

Существует две новые перегрузки вспомогательного метода HTML. Hidden, который кодирует двоичные значения в строки в кодировке Base-64:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

Обычно используется для встраивания отметки времени для объекта в представлении. Например, приложение может включать следующий объект Product:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

Форма редактирования может отображать свойство TimeStamp в форме, как показано в следующем примере:

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

Эта разметка визуализирует скрытый элемент ввода со значением timestamp как строку в кодировке Base-64, которая напоминает следующий пример:

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

Эта форма может быть отправлена в метод действия, имеющий аргумент типа Product, как показано в следующем примере:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

В методе действия свойство TimeStamp заполняется правильно, так как переданная строка Base-64-Encoded преобразуется в массив байтов.

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  Классы ModelMetadata и Моделметадатапровидер

Класс Моделметадатапровидер предоставляет абстракцию для получения метаданных для модели в представлении. MVC 2 включает поставщик по умолчанию, который делает доступными метаданные, предоставляемые атрибутами в пространстве имен System. ComponentModel. аннотации. Можно создать поставщики метаданных, предоставляющие метаданные из других хранилищ данных, таких как базы данных или XML-файлы.

Класс ViewDataDictionary предоставляет объект ModelMetadata, который содержит метаданные, извлеченные из модели классом Моделметадатапровидер. Это позволяет шаблонным вспомогательным разработчикам использовать эти метаданные и соответствующим образом скорректировать их выходные данные.

Дополнительные сведения см. в документации по классам [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) и [моделметадатапровидер](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) .

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  Поддержка атрибутов заметок к заметкам

ASP.NET MVC 2 поддерживает использование атрибутов проверки Ранжеаттрибуте, RequiredAttribute, Стрингленгсаттрибуте и Режексаттрибуте (определенных в пространстве имен System. ComponentModel. аннотации) при привязке к модели с целью обеспечения проверки входных данных.

Дополнительные сведения см. в разделе [инструкции. Проверка данных модели с помощью атрибутов примечаний](https://go.microsoft.com/fwlink/?LinkId=159063) на веб-сайте MSDN. Пример проекта, иллюстрирующий использование этих атрибутов, доступен для загрузки по адресу [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) .

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  Поставщики проверки модели

Класс поставщика проверки модели представляет абстракцию, которая предоставляет логику проверки для модели. ASP.NET MVC включает поставщик по умолчанию на основе атрибутов проверки, включенных в пространство имен System. ComponentModel. аннотации. Вы также можете создавать собственные поставщики проверки, определяющие пользовательские правила проверки и пользовательские сопоставления правил проверки для модели. Дополнительные сведения см. в документации по классу [моделвалидаторпровидер](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) .

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  Проверка на стороне клиента

Класс поставщика проверяющего элемента управления модели предоставляет браузеру метаданные проверки в виде сериализованных данных JSON, которые могут использоваться библиотекой проверки на стороне клиента. ASP.NET MVC 2 включает библиотеку проверки клиента и адаптер, которые поддерживают атрибуты проверки пространства имен, указанные ранее. Класс поставщика также позволяет использовать другие библиотеки проверки клиента путем записи адаптера, обрабатывающего данные JSON, и вызова в альтернативную библиотеку.

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  Новые фрагменты кода для Visual Studio 2010

Набор фрагментов кода HTML для ASP.NET MVC 2 устанавливается вместе с Visual Studio 2010. Чтобы просмотреть список этих фрагментов, в меню Сервис выберите пункт Диспетчер фрагментов кода. Для этого языка выберите HTML, а в поле Расположение выберите ASP.NET MVC 2. Дополнительные сведения об использовании фрагментов кода см. в документации по Visual Studio.

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  Новый фильтр действий Рекуирехттпсаттрибуте

ASP.NET MVC 2 включает новый класс Рекуирехттпсаттрибуте, который можно применять к методам действий и контроллерам. По умолчанию фильтр перенаправляет запрос, не использующий протокол SSL (HTTP), в эквивалент SSL-(HTTPS).

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  Переопределение глагола метода HTTP

При создании веб-сайта с использованием общеархитектурного стиля команды HTTP используются для определения действия, выполняемого для ресурса. Для работы службы RESTFUL требуется, чтобы приложения поддерживали полный спектр общих HTTP-команд, включая GET, WHERE, POST и DELETE.

ASP.NET MVC 2 включает новые атрибуты, которые можно применять к методам действий и синтаксису Compact Feature. Эти атрибуты позволяют ASP.NET MVC выбирать метод действия на основе HTTP-команды. В следующем примере запрос POST вызовет первый метод действия, а запрос размещения вызовет второй метод действия.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

В более ранних версиях ASP.NET MVC эти методы действия требовали более подробного синтаксиса, как показано в следующем примере:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

Так как браузеры поддерживают только HTTP-команды GET и POST, невозможно выполнить запись в действие, для которого требуется другая команда. Поэтому невозможно изначально поддерживать все запросы RESTFUL.

Однако для поддержки запросов RESTFUL во время операций POST в ASP.NET MVC 2 появился новый вспомогательный метод Хттпмесодоверриде HTML. Этот метод визуализирует скрытый элемент ввода, который заставляет форму эффективно эмулировать любой метод HTTP. Например, с помощью вспомогательного метода HTML Хттпмесодоверриде можно отправить форму с запросом на размещение или удаление. Поведение Хттпмесодоверриде влияет на следующие атрибуты:

- хттппостаттрибуте
- хттппутаттрибуте
- хттпжетаттрибуте
- хттпделетеаттрибуте
- акцептвербсаттрибуте

У скрытого элемента ввода имя X-HTTP-Method-reoverride и его значение задано для команды HTTP для эмуляции. Значение переопределения также можно указать в заголовке HTTP или в значении строки запроса в виде пары "имя-значение".

Переопределение можно использовать, только если реальный запрос является запросом POST. Значение переопределения будет проигнорировано для запросов, использующих любую другую команду HTTP.

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  Новый класс Хидденинпутаттрибуте для шаблонов вспомогательных функций

Можно применить новый атрибут Хидденинпутаттрибуте к свойству модели, чтобы указать, должен ли быть визуализирован скрытый элемент ввода при отображении модели в шаблоне редактора. (Атрибут задает неявное значение UIHint Хидденинпут). Свойство Дисплайвалуе атрибута позволяет указать, будет ли значение отображаться в редакторе и режимах отображения. Если Дисплайвалуе имеет значение false, ничего не отображается, а не в виде HTML-разметки, которая обычно окружает поле. Значение по умолчанию для Дисплайвалуе — true.

Атрибут Хидденинпутаттрибуте можно использовать в следующих сценариях:

- Когда представление позволяет пользователям изменять идентификатор объекта, необходимо отобразить значение, а также предоставить скрытый элемент ввода, содержащий старый идентификатор, чтобы его можно было передать обратно в контроллер.
- Если представление позволяет пользователям изменять двоичное свойство, которое никогда не должно отображаться, например свойство timestamp. В этом случае значение и окружающая разметка HTML (например, метка и значение) не отображаются.

В следующем примере показано, как использовать класс Хидденинпутаттрибуте.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

Если для атрибута задано значение true (или не указан параметр), происходит следующее:

- В шаблонах отображения отображается метка и отображается значение для пользователя.
- В шаблонах редактора отображается метка, а значение отображается в скрытом элементе ввода.

Если атрибут имеет значение false, происходит следующее:

- В шаблонах отображения для этого поля ничего не отображается.
- В шаблонах редактора метка не отображается, и значение отображается в скрытом элементе ввода.

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  Вспомогательный метод HTML. ValidationSummary может отображать ошибки уровня модели

Вместо того чтобы всегда отображать все ошибки проверки, вспомогательный метод HTML. ValidationSummary имеет новый параметр для отображения только ошибок уровня модели. Это позволяет отображать ошибки уровня модели в сводке проверки и ошибки, относящиеся к полям, которые должны отображаться рядом с каждым полем.

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  Шаблоны T4 в Visual Studio создают код, относящийся к целевой версии .NET Framework

Новое свойство доступно для файлов T4 из узла T4 ASP.NET MVC, указывающего версию .NET Framework, используемую приложением. Это позволяет шаблонам T4 формировать код и разметку, характерные для версии .NET Framework. В Visual Studio 2008 значение всегда равно .NET 3,5. В Visual Studio 2010 значением является либо .NET 3,5, либо .NET 4.

## <a name="api-improvements"></a><a id="_TOC4"></a>  Улучшения API

В этом разделе описываются изменения существующих типов и членов MVC ASP.NET.

- Добавлен защищенный виртуальный метод Креатеактионинвокер в классе Controller. Этот метод вызывается свойством Актионинвокер контроллера и обеспечивает Отложенное создание экземпляра вызывающего объекта, если не задано ни одного вызова.
- Добавлен защищенный виртуальный метод Хандлеунаусоризедрекуест в класс AuthorizeAttribute. Это позволяет фильтрам, производным от AuthorizeAttribute, управлять поведением при сбое авторизации.
- В класс Валуепровидердиктионари добавлен метод Add (строковый ключ, значение объекта). Это позволяет использовать синтаксис инициализатора словаря для Валуепровидердиктионари, как показано в следующем примере:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- Добавлен метод получения \_ объекта в класс sys. MVC. ажаксконтекст. Это метод JavaScript, аналогичный \_ методу get Data, но если тип содержимого ответа — Application/JSON, командлет Get \_ Object ВОЗВРАЩАЕТ объект JSON.
- Добавлено свойство Актиондескриптор в класс AuthorizationContext.
- Добавлен маркер Урлпараметер. Optional, который можно использовать для решения проблем при привязке к модели, содержащей свойство ID, если свойство отсутствует в записи формы. Дополнительные сведения см. в записи [ASP.NET MVC 2 Optional URL-параметры](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) в блоге Фил Хаак.

## <a name="breaking-changes"></a><a id="_TOC5"></a>  Критические изменения

Следующие изменения могут вызвать ошибки в существующих приложениях ASP.NET MVC 1,0.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>Изменение поведения проверки свойства для классов, реализующих IDataErrorInfo

Для объектов модели, использующих IDataErrorInfo для выполнения проверки, проверяется каждое свойство, независимо от того, было ли установлено новое значение. В ASP.NET MVC 1,0 были проверены только свойства, для которых были установлены новые значения. В ASP.NET MVC 2 свойство Error объекта IDataErrorInfo вызывается только в том случае, если все проверяющие элементы управления были успешными.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>Скрипт сопоставления сценариев IIS больше не доступен в установщике

Скрипт сопоставления сценариев IIS — это сценарий командной строки, который используется для настройки сопоставлений сценариев для IIS 6 и IIS 7 в классическом режиме. Сценарий сопоставления скриптов не требуется при использовании Visual Studio Development Server или при использовании IIS 7 в интегрированном режиме. Сценарии доступны в виде отдельного неподдерживаемого скачивания в [ASP.NET](https://github.com/aspnet/AspNetWebStack).

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>Вспомогательный метод HTML. reзамены в MVC Futures больше не доступен

Из-за изменений в работе обработчиков представлений MVC HTML. замещающий вспомогательный метод не работает и был удален.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>Интерфейс Ивалуепровидер заменяет все используемые IDictionary

Каждое свойство или аргумент метода, которые приняли значение IDictionary в MVC 1,0, теперь принимают Ивалуепровидер. Это изменение затрагивает только те приложения, которые содержат пользовательские поставщики значений или связыватели настраиваемых моделей. Примеры свойств и методов, затрагиваемых этим изменением, включают следующее.

- Свойство значение valueprovider классов ControllerBase и Моделбиндингконтекст.
- Методы Трюпдатемодел класса Controller.

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>В файл Site. CSS добавлены новые классы CSS

Файл Site. CSS в шаблонах проекта ASP.NET MVC был обновлен для включения новых стилей, используемых функцией проверки и шаблонными вспомогательными функциями.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Вспомогательные объекты теперь возвращают объект Мвчтмлстринг

Чтобы воспользоваться преимуществами нового синтаксиса выражений HTML-кодирования в ASP.NET 4, возвращаемый тип для вспомогательных функций HTML теперь Мвчтмлстринг вместо строки. Если вы используете ASP.NET MVC 2 и новые вспомогательные методы в ASP.NET 3,5, вы не сможете воспользоваться преимуществами синтаксиса HTML-кодирования. Новый синтаксис доступен только при запуске ASP.NET MVC 2 на ASP.NET 4.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult теперь реагирует только на запросы HTTP POST.

Чтобы устранить атаки, приводящие к захвату JSON, которые потенциально могут раскрытие информации, класс JsonResult теперь отвечает только на запросы HTTP POST. Вызовы AJAX GET к методам действий, которые возвращают объект JsonResult, следует изменить для использования вместо этого метода POST. При необходимости можно переопределить это поведение, задав новое свойство Жсонрекуестбехавиор объекта JsonResult. Дополнительные сведения о потенциальной атаке см. в блоге записи блога о [захвате JSON](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) в блоге по Фил Хаак.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>Методы задания свойств Model и ModelType в Моделбиндингконтекст устарели

В класс Моделбиндингконтекст было добавлено новое устанавливаемое свойство ModelMetadata. Новое свойство инкапсулирует как модель, так и свойства ModelType. Несмотря на то что свойства Model и ModelType устарели, для обратной совместимости методы получения свойств все еще работают. Они делегируют свойство ModelMetadata для получения значения.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>Изменения в классе Дефаултконтроллерфактори нарушают фабрики пользовательских контроллеров, производные от нее

Класс Дефаултконтроллерфактори был исправлен путем удаления свойства RequestContext. Вместо этого свойства экземпляр контекста запроса передается защищенным виртуальным методам Жетконтроллеринстанце и Жетконтроллертипе. Это изменение влияет на пользовательские фабрики контроллеров, производные от Дефаултконтроллерфактори.

Фабрики пользовательских контроллеров часто используются для обеспечения внедрения зависимостей для приложений ASP.NET MVC. Чтобы обновить фабрики настраиваемых контроллеров для поддержки ASP.NET MVC 2, измените сигнатуру метода или сигнатуры в соответствии с новыми сигнатурами и используйте параметр контекста запроса вместо свойства.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Область" теперь является зарезервированным ключом "маршрут-значение"

Строка "Area" в значениях маршрута теперь имеет особое значение в ASP.NET MVC таким же образом, как и "Controller" и "Action". Одно следствие заключается в том, что если вспомогательные методы HTML содержат словарь значений маршрута, содержащий "область", вспомогательные методы больше не будут добавлять "область" в строке запроса.

Если вы используете функцию "области", не используйте {Area} в качестве части URL-адреса маршрута.

## <a name="disclaimer"></a><a id="_TOC6"></a>  Заявление об отказе

Это предварительный документ, он может быть существенно изменен до выхода окончательного коммерческого выпуска описанного здесь программного обеспечения.

Информация, содержащаяся в этом документе, являет собой текущее представление корпорации Майкрософт о вопросах, которые обсуждались на момент публикации. Поскольку корпорация Майкрософт должна реагировать на изменение рыночных условий, эта информация не должна рассматриваться как обязательство корпорации Майкрософт. Корпорация Майкрософт не может гарантировать достоверность информации, предоставленной после момента публикации.

Данный технический документ предназначен только для ознакомительных целей. МАЙКРОСОФТ НЕ ПРЕДОСТАВЛЯЕТ НИКАКИХ ГАРАНТИЙ, ЯВНЫХ ИЛИ ПРЕДУСМОТРЕННЫХ ЗАКОНОДАТЕЛЬСТВОМ, ОТНОСИТЕЛЬНО СВЕДЕНИЙ, СОДЕРЖАЩИХСЯ В ДАННОМ ДОКУМЕНТЕ.

Ответственность за соблюдение всех авторских прав и прав на интеллектуальную собственность целиком и полностью несет пользователь. Без ограничения авторских прав ни одна из частей этого документа не может быть воспроизведена, сохранена или использована в системах поиска либо передана в любой форме, любыми способами (электронными, механическими, в виде фотокопии, в виде записи или любыми другими) и для любых целей без письменного разрешения корпорации Майкрософт.

Корпорация Майкрософт может иметь патенты, патентные заявки, охраняемые товарные знаки, авторские или другие права на интеллектуальную собственность применительно к содержимому этого документа. Без письменного разрешения корпорации Майкрософт данный документ не дает лицензии на эти патенты, охраняемые товарные знаки, авторские права и другую интеллектуальную собственность.

Если не указано иное, примеры компаний, организаций, продуктов, доменных имен, адресов электронной почты, логотипов, людей, мест и событий являются вымышленными, и никакой связи с реальными компаниями, организациями, продуктами, именами доменов, адресами электронной почты, логотипами, лицами, местами и событиями является случайным образом.

© 2010 Корпорация Майкрософт. Все права защищены.

Microsoft и Windows являются охраняемыми товарными знаками корпорации Майкрософт в США и других странах.

Названия фактических компаний и продуктов, упомянутые здесь, могут являться охраняемыми товарными знаками соответствующих владельцев.
