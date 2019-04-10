---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: С помощью элементов набора элементов управления AJAX и управляющих элементов-расширителей (VB) | Документация Майкрософт
author: microsoft
description: Сведения о добавлении элементов управления AJAX Control Toolkit и расширителей для страниц ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: f3371165a30018c8096da8b6b9de567ed6fe6365
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382632"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>Использование элементов управления из набора элементов AJAX и управляющих элементов-расширителей (VB)

по [Microsoft](https://github.com/microsoft)

> Сведения о добавлении элементов управления AJAX Control Toolkit и расширителей для страниц ASP.NET.


AJAX Control Toolkit содержит набор элементов управления и управляющих элементов-расширителей. Из этого краткого руководства вы узнаете, как добавить элементы управления и управляющих элементов-расширителей для страницы ASP.NET.

> [!NOTE] 
> 
> Инструкции по установке AJAX Control Toolkit и добавление AJAX Control Toolkit на панель элементов Visual Studio или Visual Web Developer, см. в этом руководстве [приступить к работе с AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).


## <a name="using-ajax-control-toolkit-controls"></a>С помощью элементов набора элементов управления AJAX

Элемент управления AJAX Control Toolkit работает так же, как обычный элемент управления ASP.NET. Можно перетащить элемент управления из панели элементов на странице ASP.NET. Элемент управления можно добавить на страницу в режиме конструктора или представление источника.

Нет одного особые требования при использовании элементов управления AJAX Control Toolkit. Страница должна содержать элемент управления ScriptManager. Элемент управления ScriptManager отвечает за включение все необходимые JavaScript, необходимую элементам управления AJAX Control Toolkit.

Например на вкладке AJAX Control Toolkit включает элемент управления с именем редактирующего элемента управления. Этот элемент управления отображает мощный HTML редактор. Выполните следующие действия, чтобы добавить на страницу элемент управления редактора.

1. Создать новую страницу ASP.NET с именем ShowEditor.aspx
2. Выберите элемент управления ScriptManager from beneath вкладки AJAX-расширения в области элементов и перетащите элемент управления на страницу.
3. Выберите элемент управления редактора from beneath вкладке AJAX Control Toolkit на панели элементов и перетащите элемент управления на страницу (см. рис. 1). Конструктор должен выглядеть как на рис. 2.
4. Запустите веб-сайт, выбрав вариант меню **отладка, начать отладку** или нажмите клавишу F5.
5. Вы увидите страницу, на рис. 3.


[![SОтказ от элемент управления редактора HTML](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**Рис 01**: Выбрав элемент управления редактора HTML ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))


[![Visual Studio конструктора с элементом управления ScriptManager и редактирования](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**Рис. 02**: Конструктор Visual Studio с помощью элемента управления ScriptManager и редактирования ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))


[![Tстраница DisplayEditor.aspx HE](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**Рис 03**: На странице DisplayEditor.aspx ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))


## <a name="using-ajax-control-toolkit-control-extenders"></a>С помощью набора средств управляющих элементов-расширителей элементов управления AJAX

AJAX Control Toolkit также содержит управляющих элементов-расширителей. Как предполагает имя, управляющего элемента-расширителя расширяет функциональность существующего элемента управления. Например элемент управления средства расширения ConfirmButton расширяет стандартный элемент управления ASP.NET Button. Расширитель изменяет поведение кнопки элемента управления s, чтобы кнопка отображает диалоговое окно подтверждения, если щелкнуть его.

Расширитель элемента управления, так же, как элемент управления AJAX Control Toolkit, необходим элемент управления ScriptManager. Перед началом использования расширителей элементов управления на странице, необходимо добавить элемент управления ScriptManager к странице.

Выполните следующие действия для использования средства расширения ConfirmButton элемента управления.

1. Создать новую страницу ASP.NET с именем ShowConfirmButton.aspx
2. Добавьте элемент управления ScriptManager к странице, перетащив элемент управления на странице from beneath вкладки AJAX-расширения.
3. Добавление стандартного элемента управления кнопки на страницу, перетащив кнопку from beneath вкладке «Стандартные» на панели элементов в область конструктора.
4. Нажмите кнопку **Добавить расширитель** параметр задачи (см. рис. 4).
5. В диалоговом окне выберите расширитель выберите ConfirmButtonExtender (см. рис. 5) и нажмите кнопку "ОК".
6. Выберите элемент управления в конструкторе и разверните средств расширения, Button1\_ConfirmButtonExtender узла в окне «Свойства» (см. рис. 6). Назначьте *действительно?* ConfirmText свойству.
7. Откройте страницу, выбрав параметр меню **отладка, начать отладку** или нажмите клавишу F5.


[![Tон параметр задачи Добавить расширитель](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**Рис. 04**: Параметр задачи Добавить расширитель ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))


[![SОтказ от средства расширения ConfirmButton управления](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**05 рис**: Выбрав элемент управления средства расширения ConfirmButton ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))


[![Sвыполнение свойство ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**Рис 06**: Задание свойства ConfirmButton ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))


При открытии страницы вы увидите кнопку. При нажатии кнопки появляется диалоговое окно подтверждения на рис. 7.


[![Displaying диалоговое окно подтверждения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**07 рис**: Отображение диалоговое окно подтверждения ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))


Обратите внимание на то, что обычно не перетащить расширитель элемента управления на страницу. Вместо этого использовать **Добавить расширитель** задач параметр, чтобы добавить расширение к элементу управления, уже добавленных на страницу. Обратите внимание на то, кроме того, настройте элемент управления свойства расширителя, открыв окно свойств для расширяемого элемента управления.

Один элемент управления ASP.NET может быть расширена путем нескольких управляющих элементов-расширителей. Окно свойств для расширяемого элемента управления будут перечислены все расширителей элементов управления, связанные с элементом управления.

> [!div class="step-by-step"]
> [Назад](get-started-with-the-ajax-control-toolkit-vb.md)
> [Вперед](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
