---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: Использование элемента управления textboxwatermark с элементами управления проверкиC#() | Документация Майкрософт
author: wenz
description: Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466590"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a>Использование элемента управления TextBoxWatermark с проверяющими элементами управления (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)

> Элемент управления элемента управления textboxwatermark в наборе средств AJAX Control Toolkit расширяет текстовое поле, чтобы текст отображался в поле. Когда пользователь щелкает в поле, он очищается. Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст. Это может конфликтовать с элементами управления проверки ASP.NET на той же странице, но эти проблемы можно преодолеть.

## <a name="overview"></a>Обзор

Элемент управления `TextBoxWatermark` в наборе средств AJAX Control Toolkit расширяет текстовое поле, позволяя отображать текст в поле. Когда пользователь щелкает в поле, он очищается. Если пользователь оставляет поле без ввода текста, заполняется предварительно заполненный текст. Это может конфликтовать с элементами управления проверки ASP.NET на той же странице, но эти проблемы можно преодолеть.

## <a name="steps"></a>Шаги

Базовая настройка образца состоит из следующих элементов: элемент управления `TextBox` с водяным знаком с помощью элемента управления `TextBoxWatermarkExtender`. Кнопка активирует обратную передачу и затем будет использоваться для активации элементов управления проверки на странице. Кроме того, для инициализации ASP.NET AJAX требуется элемент управления `ScriptManager`:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

Теперь добавьте элемент управления `RequiredFieldValidator`, который проверяет, есть ли в поле текст при отправке формы. Свойству `InitialValue` проверяющего элемента управления должно быть присвоено то же значение, которое используется в `TextBoxWatermarkExtender`ном элементе. при отправке формы значение неизмененного текстового поля — это значение водяного знака в нем:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

Однако существует одна проблема, связанная с этим подходом: Если клиент отключает JavaScript, текстовое поле не заполняется текстом водяного знака, поэтому `RequiredFieldValidator` не запускает сообщение об ошибке. Поэтому требуется второй элемент управления `RequiredFieldValidator`, проверяющий наличие пустого текстового поля (без атрибута `InitialValue`).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

Поскольку оба проверяющего элемента управления используют `Display`=`"Dynamic"`, конечный пользователь не может отличить внешний вид, в котором были запущены два проверяющих элемента управления. Вместо этого он выглядит как есть только один из них.

Наконец, добавьте некоторый серверный код для вывода текста в поле, если средство проверки не выдавало сообщение об ошибке:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

[![проверяющей элемент управления сообщает, что в поле нет текста](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

Проверяющий элемент управления сообщает, что в поле нет текста ([щелкните, чтобы просмотреть изображение с полным размером](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-textboxwatermark-in-a-formview-cs.md)
> [Вперед](using-textboxwatermark-in-a-formview-vb.md)
