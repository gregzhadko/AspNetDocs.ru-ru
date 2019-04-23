---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: Использование элемента управления TextBoxWatermark в элементе управления FormView (VB) | Документация Майкрософт
author: wenz
description: Элемент управления TextBoxWatermark в AJAX Control Toolkit расширяет текстовое поле для отображения текста в поле. Когда пользователь щелкает в поле, его я...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 056e89b20ccab0e56b1fab422c817d842beff446
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400845"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a>Использование элемента управления TextBoxWatermark в элементе управления FormView (VB)

по [Кристиан Wenz](https://github.com/wenz)

[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> Элемент управления TextBoxWatermark в AJAX Control Toolkit расширяет текстовое поле для отображения текста в поле. Когда пользователь щелкает в поле, оно будет очищено. Если пользователь оставляет поле без ввода текста, заданными текст отображается повторно. Это также возможно в элементе управления FormView.


## <a name="overview"></a>Обзор

`TextBoxWatermark` В AJAX Control Toolkit, расширяет текстовое поле для отображения текста в поле. Когда пользователь щелкает в поле, оно будет очищено. Если пользователь оставляет поле без ввода текста, заданными текст отображается повторно. Это также возможно в рамках `FormView` элемента управления.

## <a name="steps"></a>Шаги

Во-первых источником данных является обязательным. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. Базы данных является необязательной частью установки Visual Studio (включая экспресс-выпуск), а также доступна для загрузки в разделе [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). Базы данных AdventureWorks является частью образцы SQL Server 2005 и образцов баз данных (загрузить в [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базы данных является использование Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединения `AdventureWorks.mdf` файл базы данных.

В этом примере мы предполагаем, что экземпляр SQL Server 2005 Express Edition называется `SQLEXPRESS` и находится на одном компьютере с веб-сервера; это также настройки по умолчанию. Если настройки отличаются, вам нужно адаптировать сведения о соединении для базы данных.

Для активации функции ASP.NET AJAX и Control Toolkit, `ScriptManager` управления необходимо поместить в любом месте на странице (но в `<form>` элемента):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

Затем добавьте источник данных на страницу, которая поддерживает `DELETE`, `INSERT` и `UPDATE` инструкций SQL. Если вы используете этот помощник используется Visual Studio для создания источника данных, виду, что ошибки в текущей версии не префикса имени таблицы (`Vendor`) с `Purchasing`. В следующей разметке показан правильный синтаксис:

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

Запомните название (`ID`) источника данных, так как он будет использоваться в `DataSourceID` свойство `FormView` элемента управления. `<InsertItemTemplate>` Раздел `FormView` содержит поле textbox, которое расширяется за счет `TextBoxWatermarkExtender` элемента управления. Убедитесь, что расширитель находится в шаблоне, но не вне его.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

Теперь когда пользователь изменяет в режим вставки из `FormView` управления текстового поля для нового поставщика автоматически заполняемом выражаем благодарность `TextBoxWatermarkExtender` элемента управления. Щелкните внутри текстового поля позволяет ввода текста наполнения исчезают.


[![Водяной знак в поле поступает из расширения](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

Водяной знак в поле поступает из расширения ([Просмотр полноразмерного изображения](using-textboxwatermark-in-a-formview-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Назад](using-textboxwatermark-with-validation-controls-cs.md)
> [Вперед](using-textboxwatermark-with-validation-controls-vb.md)
