---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: Создание пользовательских AJAX элемента управления набора средств расширения (C#) | Документация Майкрософт
author: microsoft
description: Пользовательские расширения позволяют настроить и расширить возможности элементов управления ASP.NET без создания новых классов.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 4428ef0a6cec4c348bc48d069b990798508c21d4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391667"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>Создание пользовательского управляющего элемента-расширителя для набора элементов управления AJAX (C#)

по [Microsoft](https://github.com/microsoft)

> Пользовательские расширения позволяют настроить и расширить возможности элементов управления ASP.NET без создания новых классов.


В этом руководстве вы узнаете, как создать пользовательский расширяющий элемент управления AJAX Control Toolkit. Мы создадим простой, но полезное, новый расширитель, который изменяет состояние кнопки из отключенного состояния во включенное при вводе текста в текстовое поле. После изучения этого учебника, можно расширить набор AJAX ASP.NET с помощью собственных управляющих элементов-расширителей.

Можно создать пользовательский элемент управления расширения с помощью Visual Studio или Visual Web Developer (Убедитесь, что у вас есть последняя версия Visual Web Developer).

## <a name="overview-of-the-disabledbutton-extender"></a>Общие сведения о модуле DisabledButton

Наш новый расширитель элемента управления с именем DisabledButton расширителя. Этого расширителя будет иметь три свойства:

- TargetControlID - текстовое поле, которое расширяет элемент управления.
- TargetButtonIID - кнопки, включен или выключен.
- DisabledText - текст, который отображается на кнопке. При вводе, кнопка отображает значение свойства текста кнопки.

Можно подключить расширителя DisabledButton к элементу управления текстового поля и кнопки. Прежде чем ввести любой текст, кнопка отключена, и текстовое поле и кнопку выглядеть следующим образом:


[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))


После запуска ввода текста, доступна кнопка и текстовое поле и кнопку выглядеть следующим образом:


[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))


Чтобы создать наш расширитель элемента управления, необходимо создать следующие три файла:

- DisabledButtonExtender.cs - этот файл является класс серверного элемента управления, который будет управлять Создание медиаприставки и позволяют задавать свойства во время разработки. Он также определяет свойства, которые могут устанавливаться на вашего расширения. Эти свойства, доступны через код, а также во время разработки и соответствуют свойствам, определенным в файле DisableButtonBehavior.js.
- DisabledButtonBehavior.js--Этот файл находится в который записывается вся логика сценария вашего клиента.
- DisabledButtonDesigner.cs - этот класс обеспечивает функциональные возможности времени разработки. Этот класс требуется в том случае, если вы хотите расширитель элемента управления для правильной работы с Visual Studio или Visual Web Developer Designer.

Поэтому управляющего элемента-расширителя состоит из серверного элемента управления, поведения на стороне клиента и класс конструктора на сервере. Вы узнаете, как создать все три эти файлы в следующих разделах.

## <a name="creating-the-custom-extender-website-and-project"></a>Создание настраиваемого расширения веб-сайта и проекта

Первым шагом является создание проекта библиотеки классов и веб-сайта в Visual Studio или Visual Web Developer. Мы ll создания пользовательских расширений в проекте библиотеки классов и проверить пользовательского расширителя на веб-сайте.

Позвольте s начинаются с веб-сайта. Выполните следующие действия для создания веб-сайта.

1. Выберите пункт меню **файл, создать веб-сайт**.
2. Выберите **веб-сайт ASP.NET** шаблона.
3. Назовите новый веб-сайт *Website1*.
4. Нажмите кнопку **ОК** кнопки.

Далее нам нужно создать проект библиотеки классов, который будет содержать код для управляющего элемента-расширителя:

1. Выберите пункт меню **файл, добавить новый проект**.
2. Выберите **библиотеки классов** шаблона.
3. Назовите новую библиотеку классов с именем **CustomExtenders**.
4. Нажмите кнопку **ОК** кнопки.

После выполнения этих действий в окне обозревателя решений должен выглядеть как на рис. 1.


[![Sрешение с проектом библиотеки веб-сайт и класс](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**Рис 01**: Решение с проектом библиотеки веб-сайт и класс ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))


Далее необходимо добавить все ссылки на сборки, необходимые для проекта библиотеки классов:

1. Щелкните правой кнопкой мыши проект CustomExtenders и выберите пункт меню **добавить ссылку**.
2. Перейдите на вкладку .NET.
3. Добавьте ссылки на следующие сборки:

    1. System.Web.dll.
    2. System.Web.Extensions.dll.
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. Перейдите на вкладку обзора.
5. Добавьте ссылку на файл AjaxControlToolkit.dll сборку. Эта сборка находится в папке, куда вы скачали AJAX Control Toolkit.

После выполнения этих действий, папка ссылок проекта библиотеки классов должен выглядеть как на рис. 2.


[![RСписок диапазонов папка с необходимые ссылки](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**Рис. 02**: Папка ссылок с необходимые ссылки ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))


## <a name="creating-the-custom-control-extender"></a>Создание пользовательского элемента управления расширителя

Теперь, когда у нас есть нашей библиотеки классов, можно приступать к созданию элемента-расширителя. Позвольте s начинаются с кости bare класса расширяющего элемента управления (см. в листинге 1).

**В листинге 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

Существует несколько моментов, которые вы Обратите внимание, что сведения о классе расширитель элемента управления в листинге 1. Во-первых Обратите внимание на то, что класс наследует от базового класса ExtenderControlBase. Все элементы управления расширителя AJAX Control Toolkit, являются производными от этого базового класса. Например базовый класс включает TargetID свойство, которое является обязательным свойством для каждого управляющего элемента-расширителя.

После этого Обратите внимание на то, что класс включает следующие два атрибута, связанные с клиентского скрипта:

- WebResource - вызовет создание файла в качестве внедренного ресурса в сборке.
- ClientScriptResource - приводит к ресурсу скрипта должно быть извлечено из сборки.

Атрибут WebResource используется для внедрения в сборку файла MyControlBehavior.js JavaScript, при компиляции пользовательского расширителя. Атрибут ClientScriptResource используется для получения MyControlBehavior.js скрипт из сборки, при использовании пользовательского расширителя на веб-странице.


Чтобы WebResource и ClientScriptResource атрибуты для работы необходимо скомпилировать файл JavaScript как внедренный ресурс. В окне обозревателя решений выберите файл, откройте окно свойств и назначьте *внедренный ресурс* для **действие при построении** свойство.


Обратите внимание на то, что расширитель элемента управления также включает атрибут TargetControlType. Этот атрибут используется для указания типа элемента управления, который расширен с помощью управляющего элемента-расширителя. В случае листинге 1 расширитель элемента управления используется для расширения текстового поля.

Наконец Обратите внимание, что пользовательские расширения содержит свойство с именем MyProperty. Свойство помечено атрибутом ExtenderControlProperty. Методы GetPropertyValue() и SetPropertyValue() используются для передачи значения свойства из серверного элемента управления расширителя поведения на стороне клиента.

Позвольте s пойти дальше и реализации кода для наших DisabledButton расширителя. Код для данного объекта расширения можно найти в листинге 2.

**В листинге 2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

Расширитель DisabledButton в листинге 2 имеет два свойства с именем TargetButtonID и DisabledText. IDReferenceProperty, примененным к свойству TargetButtonID предотвращает назначение ничего, кроме идентификатор элемента управления "Кнопка" для этого свойства.

Атрибуты WebResource и ClientScriptResource связывание клиентского поведения, в файл с именем DisabledButtonBehavior.js с этого расширителя. Мы обсудим этот файл JavaScript, в следующем разделе.

## <a name="creating-the-custom-extender-behavior"></a>Создание пользовательского расширяющего поведение

Клиентский компонент из управляющего элемента-расширителя называется поведение. В поведении DisabledButton содержится фактическая логика для отключения и включения кнопки. Код JavaScript для поведения включен в листинге 3.

**Листинг 3 - DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

Файл JavaScript в листинге 3 содержит клиентский класс с именем DisabledButtonBehavior. Этот класс, например близнецом на стороне сервера включает в себя два свойства с именем TargetButtonID и получите DisabledText, к которому можно получить с помощью\_TargetButtonID/set\_TargetButtonID и получите\_DisabledText/set\_ DisabledText.

Метод initialize() связывает обработчик событий keyup с целевым элементом для поведения. Каждый раз, введите букву, в текстовое поле, связанного с этим поведением выполнением обработчика keyup. Обработчик keyup включает или отключает кнопку в зависимости от того, содержит ли текстовое поле, связанных с этим поведением любой текст.

Помните, что необходимо скомпилировать файл JavaScript в листинге 3 как внедренный ресурс. В окне обозревателя решений выберите файл, откройте окно свойств и назначьте *внедренный ресурс* для **действие при построении** свойство (см. рис. 3). Этот параметр доступен в Visual Studio и Visual Web Developer.


[![Adding файл JavaScript в качестве внедренного ресурса](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**Рис 03**: Добавление файла JavaScript как внедренный ресурс ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))


## <a name="creating-the-custom-extender-designer"></a>Создание пользовательского расширяющего конструктора

Есть один последний класс, который нам необходимо создать для выполнения наших расширителя. Нам нужно создать класс конструктора в листинге 4. Этот класс обязательно расширителя правильно работать с Visual Studio или Visual Web Developer Designer.

**Листинг 4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

Конструктор в листинге 4 связать с DisabledButton расширитель с помощью атрибута конструктора. Необходимо применить атрибут конструктор в класс DisabledButtonExtender следующим образом:

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>С помощью пользовательского расширителя

Теперь, когда мы завершения создания DisabledButton управляющего элемента-расширителя, настала пора использовать ее в нашем веб-сайте ASP.NET. Во-первых нам нужно добавить на панель инструментов пользовательского расширителя. Выполните следующие действия.

1. Откройте страницу ASP.NET, щелкнув в окне обозревателя решений.
2. Щелкните правой кнопкой мыши панель и выберите пункт меню **Выбор элементов**.
3. В диалоговом окне Выбор элементов панели элементов перейдите к сборке CustomExtenders.dll.
4. Нажмите кнопку **ОК** кнопку, чтобы закрыть диалоговое окно.

После выполнения этих действий DisabledButton управляющего элемента-расширителя появляется в области элементов (см. рис. 4).


[![DisabledButton в области элементов](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**Рис. 04**: DisabledButton в области элементов ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))


Далее нам нужно создать новую страницу ASP.NET. Выполните следующие действия.

1. Создайте новую страницу ASP.NET с именем ShowDisabledButton.aspx.
2. ScriptManager перетащите на страницу.
3. Перетащите элемент управления TextBox на страницу.
4. Перетащите элемент управления на страницу.
5. В окне «Свойства» измените значение свойства ИД кнопки <em>btnSave</em> и свойство Text значение *Сохранить\**.
  

Мы создали страницу, с помощью стандартного элемента управления ASP.NET TextBox и кнопки.

Далее нам нужно расширить элемент управления TextBox со DisabledButton расширителя:

1. Выберите **Добавить расширитель** задач, чтобы открыть диалоговое окно мастера расширений (см. рис. 5). Обратите внимание на то, что у диалогового окна есть наш пользовательский расширяющий DisabledButton.
2. Выберите расширитель DisabledButton и нажмите кнопку **ОК** кнопки.


[![Tдиалоговое окно мастера расширитель HE](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**05 рис**: Диалоговое окно мастера расширитель ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))


Наконец можно установить свойства расширителя DisabledButton. Свойства расширителя DisabledButton можно изменить, изменив свойства элемента управления TextBox:

1. Выберите текстовое поле в конструкторе.
2. В окне «Свойства» разверните узел расширения (см. рис. 6).
3. Назначьте *Сохранить* DisabledText свойство и значение *btnSave* TargetButtonID свойству.


[![Sсвойства расширителя выполнение](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**Рис 06**: Задание свойств расширителя ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))


При запуске страницы (, нажав клавишу F5), изначально отключен элемент управления Button. Сразу же начать ввод текста в текстовое поле, кнопку, элемент управления включен (см. рис. 7).


[![Tрасширитель DisabledButton HE в действии](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**07 рис**: Расширитель DisabledButton в действии ([Просмотр полноразмерного изображения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))


## <a name="summary"></a>Сводка

Цель этого учебника было объяснить, как можно расширить с помощью элементов управления пользовательского расширителя AJAX Control Toolkit. В этом руководстве мы создали простой DisabledButton управляющего элемента-расширителя. Мы реализовали этого расширителя путем создания класса DisabledButtonExtender, поведение DisabledButtonBehavior JavaScript и класс DisabledButtonDesigner. Выполните аналогичный набор шагов, каждый раз при создании пользовательского элемента управления расширителя.

> [!div class="step-by-step"]
> [Назад](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [Вперед](get-started-with-the-ajax-control-toolkit-vb.md)
