---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Отображение сведений об элементе | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389054"
---
# <a name="display-item-details"></a>Отображение сведений об элементе

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://github.com/MikeWasson/BookService)

В этом разделе вы добавите возможность просматривать подробные сведения о каждой книги. В файле app.js добавьте следующий код, чтобы модель представления:

[!code-javascript[Main](part-8/samples/sample1.js)]

В Views/Home/Index.cshtml добавьте элемент привязки к данным ссылку сведения:

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

Этот код привязывает обработчик щелчка для &lt;&gt; элемент `getBookDetail` функции в модели представления.

В этом же файле Замените следующие комментариев:

[!code-html[Main](part-8/samples/sample3.html)]

следующим кодом:

[!code-html[Main](part-8/samples/sample4.html)]

Эта разметка создает таблицу, данные которого привязаны к свойствам `detail` наблюдаемые в модели представления.

"&lt;!--Ko--&gt; &quot; синтаксис позволяет включить привязку Knockout вне элемента DOM. В этом случае `if` привязка передает этот раздел разметки для отображения только тогда, когда `details` отлично от NULL.

[!code-html[Main](part-8/samples/sample5.html)]

Теперь, если вы запустите приложение и щелкните одну из &quot;подробно&quot; ссылки, приложения, отобразятся сведения о книге.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [Назад](part-7.md)
> [Вперед](part-9.md)
