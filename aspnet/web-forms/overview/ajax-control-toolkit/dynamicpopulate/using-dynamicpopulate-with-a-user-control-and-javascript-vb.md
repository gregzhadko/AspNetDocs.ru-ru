---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: Использование DynamicPopulate с пользовательского элемента управления и JavaScript (Visual Basic) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: b863cb0045fcec202931148bff5befa7ed62db4d
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2019
ms.locfileid: "58424148"
---
<a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a>Использование DynamicPopulate с пользовательским элементом управления и кодом JavaScript (VB)
====================
по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)

> Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы. Можно также активировать заполнение, с помощью пользовательского кода JavaScript на стороне клиента. Тем не менее, выполняемый при расширителя находится в пользовательский элемент управления имеет особое внимание.


## <a name="overview"></a>Обзор

`DynamicPopulate` Элемента управления в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы. Можно также активировать заполнение, с помощью пользовательского кода JavaScript на стороне клиента. Тем не менее, выполняемый при расширителя находится в пользовательский элемент управления имеет особое внимание.

## <a name="steps"></a>Шаги

Во-первых, необходимо, чтобы к веб-службе ASP.NET, который реализует метод, вызываемый `DynamicPopulateExtender` элемента управления. Веб-служба реализует метод `getDate()` , ожидает один аргумент типа строки, называемой `contextKey`, так как `DynamicPopulate` элемент управления отправляет понимается набор сведений о контексте с каждый вызов веб-службы. Ниже приведен код (файлы `DynamicPopulate.vb.asmx`) который получает текущую дату в одном из трех форматов:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

На следующем шаге, создайте новый пользовательский элемент управления (`.ascx` файл), обозначаемого, следующее объявление в первой строке:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

Объект &lt; `label` &gt; элемент будет использоваться для отображения данных, поступающих с сервера.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

Также в файле параметров пользователя, мы будем использовать три переключателей, каждый из которых представляет одно из трех возможных даты форматов, поддерживаемых веб-службы. Когда пользователь щелкает один из переключателей, браузер выполнит код JavaScript, который выглядит следующим образом:

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

Этот код обращается к `DynamicPopulateExtender` (не волнуйтесь о странный код еще, это будет рассматриваться позже) и активирует динамического заполнения данными. В контексте текущего переключатель `this.value` ссылается на его значение, являющееся `format1`, `format2` или `format3` точно что ожидает веб-метода.

Единственное, что пока отсутствует в пользовательский элемент управления является `DynamicPopulateExtender` элемента управления, которые связывают переключателей с веб-службы.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

Еще раз вы также могли заметить странный код, используемый в элементе управления: `mcd1$myDate` вместо `myDate`. Ранее, код JavaScript, используемый `mcd1_dpe1` для доступа к `DynamicPopulateExtender` вместо `dpe1`. Эта стратегия именования имеет особые требования при использовании `DynamicPopulateExtender` внутри пользовательского элемента управления. Кроме того вам нужно внедрить пользовательский элемент управления определенным образом заставить их работать. Создать новую страницу ASP.NET и зарегистрировать префикс тега для пользовательского элемента управления, который вы только что реализовали:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

Затем включите ASP.NET AJAX `ScriptManager` управления на новой странице:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

Наконец добавьте пользовательский элемент управления на страницу. Необходимо установить его `ID` атрибут (и `runat="server"`, конечно), но необходимо также присвоено определенное имя: `mcd1` так как это префикс, используемый в пользовательский элемент управления для доступа к нему с помощью JavaScript.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

Вот и все! Правильно работает страницы: Пользователь щелкает один из переключателей, элемент управления в наборе средств вызывает веб-службы и отображает текущую дату в нужном формате.


[![Переключатели находятся в пользовательский элемент управления](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)

Переключатели находятся в пользовательский элемент управления ([Просмотр полноразмерного изображения](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](dynamically-populating-a-control-using-javascript-code-vb.md)
