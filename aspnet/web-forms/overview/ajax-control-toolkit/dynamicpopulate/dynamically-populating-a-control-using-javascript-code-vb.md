---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: Динамическое заполнение элемента управления, с помощью кода JavaScript (Visual Basic) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 668815d58f2dc9a67cce441dfa267fa043a35091
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387208"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>Динамическое заполнение элемента управления с помощью кода JavaScript (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> Элемент управления DynamicPopulate в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы. Можно также активировать заполнение, с помощью пользовательского кода JavaScript на стороне клиента.


## <a name="overview"></a>Обзор

`DynamicPopulate` Элемента управления в ASP.NET AJAX Control Toolkit вызывает веб-службы (или метод страницы) и заполняет результирующее значение в целевой элемент управления на странице без обновления страницы. Можно также активировать заполнение, с помощью пользовательского кода JavaScript на стороне клиента.

## <a name="steps"></a>Шаги

Во-первых, необходимо, чтобы к веб-службе ASP.NET, который реализует метод, вызываемый `DynamicPopulateExtender` элемента управления. Веб-служба реализует метод `getDate()` , ожидает один аргумент типа строки, называемой `contextKey`, так как `DynamicPopulate` элемент управления отправляет понимается набор сведений о контексте с каждый вызов веб-службы. Ниже приведен код (файл `DynamicPopulate.vb.asmx`) который получает текущую дату в одном из трех форматов:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

На следующем шаге создайте новый сайт ASP.NET и начать с элементом управления ASP.NET AJAX ScriptManager:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

Затем добавьте элемент управления label (например с помощью HTML-элемент управления с тем же именем, или `<asp:Label />` веб-элемент управления) где позже будет показано, результатом вызова веб-службы.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

Далее включите `DynamicPopulateExtender` управление и предоставляют данные веб-службы, целевой элемент управления, но не имя элемента управления, который запускает заполнение, это будет сделано позже с помощью пользовательским кодом JavaScript!

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

Теперь в компонент JavaScript. `$find()` Функции, определенные в библиотеке AJAX для ASP.NET, такие как возвращает ссылку на стороне сервера объекты ASP.NET AJAX Control Toolkit `DynamicPopulateExtender`. В текущем файле `$find("dpe")` возвращает ссылку на `DynamicPopulateExtender` элемента управления на странице. Он предоставляет метод, называемый `populate()` чего начнется процесс динамического заполнения. `populate()` Метод требует один аргумент: контекстный ключ, который будет использоваться в качестве аргумента `getDate()` веб-метод. Например `$find("dpe").populate("format1")` заполнения метку с текущей датой в формате месяц день год.

Чтобы сделать пример более гибкий, пользователь может выбрать один из нескольких форматов даты. Для каждой из них отображается типа "переключатель". Один раз когда пользователь щелкает переключатель, код JavaScript динамически заполняет метку с выбранным форматом даты. Ниже приведены эти переключатели.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

Обратите внимание, что в контексте типа "переключатель", выражение JavaScript `this.value` ссылается на значение «текущий», которая может быть точно те же данные `getDate()` метод может работать с.


[![A Нажмите кнопку извлекает дату с сервера, в формате, заданном](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

Нажмите кнопку извлекает дату с сервера, в формате, заданном ([Просмотр полноразмерного изображения](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](dynamically-populating-a-control-vb.md)
> [Вперед](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
