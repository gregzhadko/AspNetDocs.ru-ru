---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: Использование DynamicPopulate с пользовательским элементом управления и JavaScriptC#() | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет результирующее значение целевым элементом управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: a0e6d04a5f62ab558aceb8302d94d3bf2dc8a39f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497334"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a>Использование DynamicPopulate с пользовательским элементом управления и кодом JavaScript (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)

> Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы. Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента. Однако особое внимание необходимо предпринять, когда расширитель находится в пользовательском элементе управления.

## <a name="overview"></a>Обзор

Элемент управления `DynamicPopulate` в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы. Можно также активировать заполнение с помощью пользовательского кода JavaScript на стороне клиента. Однако особое внимание необходимо предпринять, когда расширитель находится в пользовательском элементе управления.

## <a name="steps"></a>Шаги

Во-первых, вам понадобится ASP.NET Web Service, который реализует метод, вызываемый элементом управления `DynamicPopulateExtender`. Веб-служба реализует метод `getDate()`, который принимает один аргумент типа String, именуемый `contextKey`, поскольку элемент управления `DynamicPopulate` отправляет один фрагмент сведений о контексте при каждом вызове веб-службы. Ниже приведен код (файл `DynamicPopulate.cs.asmx`), который извлекает текущую дату в одном из трех форматов:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

На следующем шаге создайте новый пользовательский элемент управления (`.ascx` файл), обозначенный следующим объявлением в первой строке:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

Для вывода данных, поступающих с сервера, будет использоваться элемент &gt; `label`&lt;.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

Кроме того, в файле пользовательского элемента управления будут использоваться три переключателя, каждая из которых представляет один из трех возможных форматов даты, поддерживаемых веб-службой. Когда пользователь щелкает один из переключателей, браузер выполнит код JavaScript, который выглядит следующим образом:

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

Этот код обращается к `DynamicPopulateExtender` (не беспокойтесь о странном ИДЕНТИФИКАТОРе, он будет рассмотрен позже) и активирует динамическое заполнение данными. В контексте текущего переключателя `this.value` ссылается на его значение, которое `format1`, `format2` или `format3` именно то, что предполагает веб-метод.

Единственным элементом пользовательского элемента управления пока является элемент управления `DynamicPopulateExtender`, который связывает переключатели с веб-службой.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

Опять же, вы можете отметить странный идентификатор, используемый в элементе управления: `mcd1$myDate` вместо `myDate`. Ранее код JavaScript использовал `mcd1_dpe1` для доступа к `DynamicPopulateExtender` вместо `dpe1`. Такая стратегия именования является особой требованием при использовании `DynamicPopulateExtender` в пользовательском элементе управления. Кроме того, необходимо внедрить пользовательский элемент управления, чтобы сделать его все работать. Создайте новую страницу ASP.NET и зарегистрируйте префикс тега для только что реализованного пользовательского элемента управления:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

Затем включите элемент управления `ScriptManager` ASP.NET AJAX на новой странице:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

Наконец, добавьте пользовательский элемент управления на страницу. Необходимо задать только его атрибут `ID` (и `runat="server"`, конечно), но также необходимо задать конкретное имя: `mcd1` так как это префикс, используемый в пользовательском элементе управления для доступа к нему с помощью JavaScript.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

Вот и все! Страница ведет себя ожидаемым образом: пользователь щелкает один из переключателей, элемент управления в наборе инструментов вызывает веб-службу и отображает текущую дату в нужном формате.

[![переключатели находятся в пользовательском элементе управления](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)

Переключатели находятся в пользовательском элементе управления ([щелкните, чтобы просмотреть изображение с полным размером](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](dynamically-populating-a-control-using-javascript-code-cs.md)
> [Вперед](dynamically-populating-a-control-vb.md)
