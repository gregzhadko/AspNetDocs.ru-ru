---
uid: mvc/overview/advanced/custom-mvc-templates
title: Пользовательский шаблон MVC | Документация Майкрософт
author: joeloff
description: Создайте шаблон в виде расширения VSIX.
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499602"
---
# <a name="custom-mvc-template"></a>Пользовательский шаблон MVC

по [Жак элоф](https://github.com/joeloff)

В выпуске обновления средств MVC 3 для Visual Studio 2010 появился отдельный мастер проектов для проектов MVC. Изменение было обусловлено двумя факторами. Во первых, появление новых шаблонов в MVC 3 и поддержка дополнительных ядер представлений, таких как Razor Lead, для оверкровдинг диалогового окна Новый проект в Visual Studio. Во вторых, клиенты задавали запрос на точки расширения, и мастер создания проекта MVC даст нам возможность ответить на эти запросы.

Добавление пользовательских шаблонов было трудным процессом, использующим реестр, чтобы сделать новые шаблоны видимыми для мастера проектов MVC. Автор нового шаблона должен заключить его внутрь MSI-файла, чтобы обеспечить создание необходимых записей реестра во время установки. Альтернативой было создание ZIP-файла, содержащего доступный шаблон, и предоставление конечному пользователю возможности вручную создавать необходимые записи реестра.

Ни один из вышеупомянутых подходов не является идеальным решением, поэтому мы решили использовать некоторую существующую инфраструктуру, предоставляемую расширениями [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) , чтобы упростить создание, распространение и установку пользовательских шаблонов MVC, начиная с MVC 4 для Visual Studio 2012. Ниже перечислены некоторые преимущества, предоставляемые этим подходом.

- Расширение VSIX может содержать несколько шаблонов, поддерживающих разные языки (C# и Visual Basic) и несколько ядер ПРЕДСТАВЛЕНИЙ (ASPX и Razor).
- Расширение VSIX может ориентироваться на несколько номеров SKU Visual Studio, включая Экспресс-SKU.
- [Коллекция Visual Studio](https://visualstudiogallery.msdn.microsoft.com/) упрощает распространение расширения для широкой аудитории.
- Расширения VSIX могут быть обновлены, что упрощает создание исправлений и обновлений для пользовательских шаблонов.

## <a name="prerequisites"></a>предварительные требования

- Пользователям необходимо быть знакомы с созданием шаблонов проектов, включая необходимую разметку для файлов VSTEMPLATE и т. д.
- Пользователям потребуется установить Visual Studio Professional и более поздней версии. Express SKU не поддерживает создание проектов VSIX.
- Установлен [пакет SDK для Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30668) .

## <a name="example"></a>Пример

Первым шагом является создание нового проекта VSIX с помощью C# или Visual Basic. Выберите **файл > новый проект**, а затем щелкните **расширяемость** в левой области и выберите **проект VSIX**.

![Создать проект](custom-mvc-templates/_static/image1.jpg)

После создания проекта откроется конструктор VSIX.

![Метаданные конструктора проектов](custom-mvc-templates/_static/image2.jpg)

Конструктор можно использовать для изменения некоторых общих свойств расширения, которые будут отображаться для пользователей при установке расширения или при просмотре установленных расширений в Visual Studio (**средства > расширения и обновления**). Завершив общие сведения, перейдите на **вкладку целевые объекты установки**.

![Целевые объекты установки конструктора проектов](custom-mvc-templates/_static/image3.jpg)

На этой вкладке можно указать номера SKU и версии Visual Studio, поддерживаемые вашим расширением. Установите флажок для **этого VSIX, установленный для всех пользователей** , чтобы включить установку VSIX для каждого компьютера. Нажмите кнопку **создать** справа, чтобы добавить дополнительные номера SKU, например Web Developer Express (vWD).

![Добавить новый целевой объект установки](custom-mvc-templates/_static/image4.jpg)

Если вы собираетесь поддерживать все профессиональные и более высокие номера SKU (Professional, Premium и Ultimate), вам нужно выбрать только минимальный номер SKU в семействе **Microsoft.VisualStudio.Pro**. Не забудьте сохранить все изменения после завершения целей установки.

![Целевые объекты установки конструктора проектов](custom-mvc-templates/_static/image5.jpg)

Вкладка **активы** используется для добавления всех файлов содержимого в VSIX. Так как MVC требует пользовательских метаданных, вы будете редактировать необработанный XML-файл манифеста VSIX вместо использования вкладки " **активы** " для добавления содержимого. Начните с добавления содержимого шаблона в проект VSIX. Важно, чтобы структура папки и ее содержимого были зеркально отражены в структуре проекта. Приведенный ниже пример содержит четыре шаблона проекта, которые были производными от основного проекта MVC. Убедитесь, что все файлы, составляющие шаблон проекта (все, что находится под папкой Прожекттемплатес), добавлены в набор **данных** в файле проекта VSIX и что каждый элемент содержит наборы метаданных **копитуутпутдиректори** и **инклудеинвсикс** , как показано в примере ниже.

&lt;содержимое: =&quot;Прожекттемплатес\мимвквебаппликатионпрожекттемплате.ксаспкс\басиквеб.конфиг&quot;&gt;

&lt;Копитуутпутдиректори&gt;всегда&lt;/Копитуутпутдиректори&gt;

&lt;Инклудеинвсикс&gt;true&lt;/Инклудеинвсикс&gt;

&lt;/контент&gt;

В противном случае интегрированная среда разработки попытается скомпилировать содержимое шаблона при сборке VSIX, и, скорее всего, появится сообщение об ошибке. Файлы кода в шаблонах часто содержат специальные [Параметры шаблона](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) , используемые Visual Studio при создании экземпляра шаблона проекта и, следовательно, не могут быть скомпилированы в интегрированной среде разработки.

![Обозреватель решений](custom-mvc-templates/_static/image6.jpg)

Закройте конструктор VSIX, щелкните правой кнопкой мыши файл **source. extension. manifest** в **Обозреватель решений** и выберите пункт **Открыть с помощью** и выберите пункт **Редактор XML (текстовый)** .

![Открыть с помощью диалогового окна](custom-mvc-templates/_static/image7.jpg)

Создайте элемент **&gt;&lt;Assets** и добавьте элемент **&gt;&lt;** ресурсов для каждого файла, который должен быть добавлен в VSIX. Атрибут **Type** каждого элемента **&gt;ресурса&lt;** должен иметь значение **Microsoft. VisualStudio. MVC. Template**. Это пользовательское пространство имен, понятное только мастеру проектов MVC. Дополнительные сведения о структуре и макете файла манифеста см. в документации по схеме VSIX 2,0.

Просто добавить файлы в VSIX недостаточно для регистрации шаблонов с помощью мастера MVC. В мастере MVC необходимо указать такие сведения, как имя шаблона, описание, Поддерживаемые обработчики представлений и язык программирования. Эти сведения переносятся в пользовательские атрибуты, связанные с элементом **&lt;ресурса&gt;** для каждого файла **VSTEMPLATE** .

&lt;ресурс Д:всикссубпас =&quot;Прожекттемплатес\мимвквебаппликатионпрожекттемплате.ксаспкс&quot;

Type =&quot;Microsoft. VisualStudio. MVC. Template&quot;

Д:саурце = файл&quot;&quot;

Путь =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Language =&quot;C#&quot;

Виевенгине =&quot;&quot; ASPX

TemplateId =&quot;Мимвкаппликатион&quot;

Title =&quot;пользовательские базовые веб-приложения&quot;

Description =&quot;настраиваемый шаблон, производный от базового веб-приложения MVC (Razor)&quot;

Версия =&quot;4,0&quot;/&gt;

Ниже приведено описание настраиваемых атрибутов, которые должны присутствовать:

- Для **ProjectType** должно быть задано значение MVC.
- **Язык** определяет язык разработки, поддерживаемый шаблоном. Допустимые значения: C# или VB.
- **Виевенгине** обозначает подсистему представления, поддерживаемую шаблоном, например ASPX или Razor. Для этого поля можно указать пользовательское значение.
- **TemplateId** используется для группирования шаблонов. Если значение совпадает с существующим ИДЕНТИФИКАТОРом шаблона, он будет переопределять шаблоны, ранее зарегистрированные в мастере MVC.
- **Заголовок** обозначает краткое описание, отображаемое в мастере MVC под каждым шаблоном проекта.
- **Описание** обозначает более подробное описание шаблона.

После добавления всех файлов в манифест и его сохранения вы увидите, что на вкладке **активы** в конструкторе отображаются все файлы, но не настраиваемые атрибуты, добавленные в **&lt;ресурс&gt;** элементы **VSTEMPLATE** .

![Ресурсы конструктора проектов](custom-mvc-templates/_static/image8.jpg)

Теперь все осталось скомпилировать проект VSIX и установить его.

Убедитесь, что все экземпляры Visual Studio закрыты на компьютере, на котором планируется протестировать расширение VSIX. Visual Studio сканирует новые расширения во время запуска, поэтому, если интегрированная среда разработки открыта во время установки VSIX, потребуется перезапустить Visual Studio. В обозревателе дважды щелкните VSIX File, чтобы запустить **установщик VSIX**, нажмите кнопку **установить** , а затем запустите Visual Studio.

![Установщик VSIX](custom-mvc-templates/_static/image9.jpg)

В меню выберите **сервис > расширения и обновления** , чтобы убедиться, что расширение установлено. Если установщик VSIX сообщил об ошибках во время установки расширения, можно просмотреть журнал установщика VSIX для получения дополнительных сведений. Журнал обычно создается в папке **% TEMP%** пользователя, установившего расширение, например **к:\усерс\боб\аппдата\локал\темп**.

![Расширения и обновления](custom-mvc-templates/_static/image10.jpg)

После закрытия окна можно создать проект MVC 4, чтобы узнать, отображаются ли новые шаблоны в мастере MVC.

![Новый проект ASP.NET MVC 4](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>Ограничения

1. Мастер MVC не поддерживает локализованные пользовательские шаблоны.
2. Мастер не будет сообщать об ошибках, если не удается выполнить обнаружение пользовательских шаблонов. Если какой бы то ни было требуемый пользовательский атрибут отсутствует, шаблон будет просто исключен из мастера.
