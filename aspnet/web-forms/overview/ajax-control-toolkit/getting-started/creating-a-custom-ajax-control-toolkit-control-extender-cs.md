---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: Создание пользовательского AJAX Управления Toolkit Расширитель управления (СЗ) Документы Майкрософт
author: rick-anderson
description: Пользовательские расширители позволяют настраивать и расширять возможности управления ASP.NET без создания новых классов.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543032"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>Создание пользовательского управляющего элемента-расширителя для набора элементов управления AJAX (C#)

[корпорацией Майкрософт](https://github.com/microsoft)

> Пользовательские расширители позволяют настраивать и расширять возможности управления ASP.NET без создания новых классов.

В этом учебнике вы узнаете, как создать пользовательский удлинитель управления AJAX Control Toolkit. Мы создаем простой, но полезный новый расширитель, который изменяет состояние кнопки от отключенного к включенной при вводе текста в TextBox. После прочтения этого учебника, вы сможете расширить ASP.NET AJAX Toolkit с вашим собственным удлинителем управления.

Вы можете создать удлинители пользовательского управления с помощью Visual Studio или Visual Web Developer (убедитесь, что у вас есть последняя версия Visual Web Developer).

## <a name="overview-of-the-disabledbutton-extender"></a>Обзор расширителя отключенных кстопок

Наш новый удлинитель управления называется Удлинитель для инвалидов. Этот расширитель будет иметь три свойства:

- TargetControlID - TextBox, что управление расширяется.
- TargetButtonIID - Кнопка, которая отключена или включена.
- DisabledText - текст, который первоначально отображается в кнопке. При запуске ввода кнопка отображает значение свойства Кнопка Текста.

Вы подключите расширитель отключенной кнопки к управлению TextBox и кнопкой. Перед тем, как ввести текст, кнопка отключена, а TextBox и кнопка выглядят следующим образом:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

([Нажмите, чтобы просмотреть полноразмерное изображение](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))

После того, как вы начнете вводить текст, кнопка включена и TextBox и кнопка выглядеть следующим образом:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

([Нажмите, чтобы просмотреть полноразмерное изображение](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))

Чтобы создать наш расширитель управления, нам нужно создать следующие три файла:

- DisabledButtonExtender.cs - этот файл является классом управления на стороне сервера, который будет управлять созданием расширителя и позволит вам установить свойства во время проектирования. Он также определяет свойства, которые могут быть установлены на расширитель. Эти свойства доступны через код и во время проектирования и совпадают свойства, определенные в файле DisableButtonBehavior.js.
- DisabledButtonBehavior.js - Этот файл, где вы добавите все ваши логики сценария клиента.
- DisabledButtonDesigner.cs - Этот класс обеспечивает функциональность времени проектирования. Вам нужен этот класс, если вы хотите, чтобы расширитель управления работал правильно с Visual Studio/Visual Web Developer Designer.

Таким образом, расширитель управления состоит из управления на стороне сервера, поведения клиента и класса конструктора на стороне сервера. Вы узнаете, как создать все три из этих файлов в следующих разделах.

## <a name="creating-the-custom-extender-website-and-project"></a>Создание веб-сайта и проекта Custom Extender

Первым шагом является создание проекта библиотеки классов и веб-сайта в Visual Studio/Visual Web Developer. Мы создадим пользовательский расширитель в проекте библиотеки класса и протестируем пользовательский удлинитель на веб-сайте.

Начнем с веб-сайта. Выполните следующие действия, чтобы создать веб-сайт:

1. Выберите вариант меню **Файл, Новый веб-сайт**.
2. Выберите шаблон **веб-сайта ASP.NET.**
3. Назовите новый веб-сайт *Website1*.
4. Нажмите кнопку **ОК**.

Далее нам нужно создать проект библиотеки класса, который будет содержать код для расширителя управления:

1. Выберите вариант меню **Файл, Добавить, Новый проект**.
2. Выберите шаблон **библиотеки класса.**
3. Назовите новую библиотеку класса с именем **CustomExtenders.**
4. Нажмите кнопку **ОК**.

После выполнения этих шагов окно Solution Explorer должно выглядеть как рисунок 1.

[![Решение с проектом веб-сайта и библиотеки класса](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**Рисунок 01**: Решение с веб-сайтом и проектом библиотеки класса[(Нажмите, чтобы просмотреть полноразмерное изображение](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))

Далее необходимо добавить все необходимые ссылки на сборку в проект библиотеки класса:

1. Нажмите правой кнопкой мыши проекта CustomExtenders и выберите вариант меню **Добавить справку.**
2. Перейдите на вкладку .NET.
3. Добавьте ссылки на следующие сборки:

    1. System.Web.dll.
    2. System.Web.Extensions.dll.
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. Выберите вкладку обзора.
5. Добавьте ссылку на сборку AjaxControlToolkit.dll. Эта сборка находится в папке, где вы загрузили инструмент управления AJAX.

После завершения этих шагов папка «Ссылки на рекомендации по классу» должна выглядеть как рисунок 2.

[![Папка ссылок с требуемыми ссылками](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**Рисунок 02**: Ссылки папку с требуемыми ссылками[(Нажмите, чтобы посмотреть полноразмерное изображение](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>Создание расширителя пользовательского управления

Теперь, когда у нас есть библиотека класса, мы можем начать строить наш расширяемый контроль. Начнем с голых костей пользовательского класса управления расширителем (см. листинг 1).

**Листинг 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

Есть несколько вещей, которые вы заметите о классе диспетчера управления в листинге 1. Во-первых, обратите внимание, что класс наследует от базового класса ExtenderControlBase. Все элементы управления AJAX Toolkit проходят из этого базового класса. Например, базовый класс включает свойство TargetID, которое является обязательным свойством каждого расширителя управления.

Далее обратите внимание, что класс включает в себя следующие два атрибута, связанных со сценарием клиента:

- WebResource - Вызывает включение файла в качестве встроенного ресурса в сборку.
- ClientScriptResource - Вызывает извлечение ресурса скрипта из сборки.

Атрибут WebResource используется для встраиваемого файла MyControlBehavior.js JavaScript в сборку при компилировании пользовательского расширителя. Атрибут ClientScriptResource используется для извлечения скрипта MyControlBehavior.js из сборки, когда пользовательский расширитель используется на веб-странице.

Для того, чтобы атрибуты WebResource и ClientScriptResource работали, необходимо компилировать файл JavaScript в качестве встроенного ресурса. Выберите файл в окне Solution Explorer, откройте лист свойств и присвоите значение *встраиваемого ресурса* в свойство **Build Action.**

Обратите внимание, что расширитель управления также включает атрибут TargetControlType. Этот атрибут используется для определения типа управления, который расширяется расширителем управления. В случае листинга 1, расширитель управления используется для расширения TextBox.

Наконец, обратите внимание, что пользовательский расширитель включает в себя свойство под названием MyProperty. Свойство помечено атрибутом ExtenderControlProperty. Методы GetPropertyValue() и SetPropertyValue() используются для передачи значения свойства от расширителя управления сервером к поведению клиента.

Давайте идти вперед и реализовать код для наших инвалидов Баттон расширитель. Код для этого расширителя можно найти в листинге 2.

**Список 2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

Удлинитель инвалидной кнопки в листинге 2 имеет два свойства под названием TargetButtonID и DisabledText. IDReferenceProperty, применяемый к свойству TargetButtonID, не позволяет назначить этому свойству что-либо, кроме идентификатора управления кнопкой.

Атрибуты WebResource и ClientScriptResource связывают поведение клиента, расположенное в файле под названием DisabledButtonBehavior.js, с этим расширителем. Мы обсуждаем этот файл JavaScript в следующем разделе.

## <a name="creating-the-custom-extender-behavior"></a>Создание пользовательского поведения расширителя

Компонент клиентской стороны расширителя управления называется поведением. Фактическая логика отключения и включения кнопки содержится в поведении disabledButton. Код JavaScript для поведения включен в листинг 3.

**Список 3 - ИнвалидButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

Файл JavaScript в листинге 3 содержит класс на стороне клиента под названием DisabledButtonBehavior. Этот класс, как и его двойник на стороне сервера, включает в\_себя два\_свойства под названием TargetButtonID и DisabledText, к которым можно получить TargetButtonID/set TargetButtonID и получить\_DisabledText/set\_DisabledText.

Метод инициализации () связывает обработчик события ключа с целевым элементом для поведения. Каждый раз, когда вы вводите письмо в TextBox, связанный с этим поведением, обработчик клавиатуры выполняет. Обработчик клавиатуры позволяет или отключает кнопку в зависимости от того, содержит ли TextBox какой-либо текст.

Помните, что вы должны компилировать файл JavaScript в листинге 3 в качестве встроенного ресурса. Выберите файл в окне Solution Explorer, откройте лист свойств и присвоите *встраиваемый ресурс* свойству **«Действие сборки»** (см. рисунок 3). Эта опция доступна как в Visual Studio, так и в визуальном веб-разработчике.

[![Добавление файла JavaScript в качестве встроенного ресурса](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**Рисунок 03**: Добавление файла JavaScript в качестве встроенного ресурса[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)

## <a name="creating-the-custom-extender-designer"></a>Создание пользовательского конструктора расширителя

Существует один последний класс, который мы должны создать, чтобы завершить наш расширитель. Нам нужно создать класс дизайнеров в листинге 4. Этот класс необходим, чтобы расширитель по-веможно еле-то правильно сифицировать студию/дизайнер веб-разработчика Visual Studio.

**Список 4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

Вы связываете дизайнера в листинге 4 с расширителем disabledButton с атрибутом Designer. Вы должны применить атрибут дизайнера к классу DisabledButtonExtender следующим образом:

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>Использование пользовательского расширителя

Теперь, когда мы закончили создание удлинителя управления disabledButton, пришло время использовать его на нашем веб-сайте ASP.NET. Во-первых, нам нужно добавить пользовательский удлинитель в набор инструментов. Выполните следующие действия.

1. Откройте ASP.NET страницу, дважды нажав на страницу в окне Solution Explorer.
2. Нажмите правой кнопкой мыши на набор инструментов и выберите вариант меню **Выберите элементы.**
3. В диалоге «Выберите набор инструментов» просмотрите сборку CustomExtenders.dll.
4. Нажмите кнопку **OK,** чтобы закрыть диалог.

После выполнения этих шагов в наборе инструментов должен появиться расширитель управления отключенной кнопки (см. рисунок 4).

[![Инвалидная кнопка в наборе инструментов](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**Рисунок 04**: Отключенная кнопка в наборе инструментов[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)

Далее нам нужно создать новую страницу ASP.NET. Выполните следующие действия.

1. Создайте новую ASP.NET страницу под названием ShowDisabledButton.aspx.
2. Перетащите scriptManager на страницу.
3. Перетащите элемент управления TextBox на страницу.
4. Перетащите элемент управления кнопкой на страницу.
5. В окне Свойств изменить свойство Идентификатор кнопки на значение <em>btnSave</em> и свойство текста на значение *\*Сохранить.*

Мы создали страницу со стандартным ASP.NET TextBox и кнопки управления.

Далее нам нужно расширить управление TextBox с помощью расширителя инвалидной кнопки:

1. Выберите опцию задачи **Add Extender,** чтобы открыть диалог Мастера расширения (см. рисунок 5). Обратите внимание, что диалог включает в себя наш пользовательский удлинитель инвалида Button.
2. Выберите расширитель инвалидной кнопки и нажмите кнопку **OK.**

[![Диалог Мастера расширения](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**Рисунок 05**: Диалог Мастера расширения[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)

Наконец, мы можем установить свойства расширителя инвалидной кнопки. Вы можете изменить свойства расширителя отключенной кнопки, изменив свойства элемента управления TextBox:

1. Выберите TextBox в конструкторе.
2. В окне Свойств расширьте узло Extenders (см. рисунок 6).
3. Присвоите значение *Сохранить* свойство DisabledText и значение *btnSave* к свойству TargetButtonID.

[![Установка свойств расширителя](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**Рисунок 06**: Установка свойств расширителя[(Нажмите, чтобы просмотреть полноразмерное изображение)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)

При запуске страницы (нажатием F5) управление кнопкой изначально отключено. Как только вы начинаете вводить текст в TextBox, управление кнопкой включено (см. рисунок 7).

[![Удлинитель инвалида в действии](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**Рисунок 07**: Удлинитель инвалида в действии[(Нажмите, чтобы просмотреть полноразмерное изображение](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))

## <a name="summary"></a>Сводка

Цель этого учебника состояла в том, чтобы объяснить, как вы можете расширить AJAX Control Toolkit с пользовательскими элементами управления расширителем. В этом учебнике мы создали простой удлинитель управления disabledButton. Мы внедрили этот расширитель, создав класс DisabledButtonExtender, поведение JavaScript отключенного кнопки и класс DisabledButtonDesigner. Вы следуете за подобным набором шагов когда вы создаете изготовленный на заказ удлинитель управления.

> [!div class="step-by-step"]
> [Назад](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [Вперед](get-started-with-the-ajax-control-toolkit-vb.md)
