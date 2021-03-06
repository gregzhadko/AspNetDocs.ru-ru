---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: Использование класса TagBuilder для создания вспомогательных функций HTML (VB) | Документация Майкрософт
author: StephenWalther
description: Стивен Вальтер представляет собой полезный класс служебной программы в платформе ASP.NET MVC, именуемый классом TagBuilder. Для простоты можно использовать класс TagBuilder...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485586"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a>Использование класса TagBuilder для создания вспомогательных функций HTML (VB)

по [Стивен Вальтер](https://github.com/StephenWalther)

> Стивен Вальтер представляет собой полезный класс служебной программы в платформе ASP.NET MVC, именуемый классом TagBuilder. Для легкого создания тегов HTML можно использовать класс TagBuilder.

Платформа ASP.NET MVC содержит полезный служебный класс, именуемый классом TagBuilder, который можно использовать при построении вспомогательных функций HTML. Класс TagBuilder, как предлагается имя класса, позволяет легко создавать теги HTML. В этом кратком руководстве вы получите обзор класса TagBuilder и узнаете, как использовать этот класс при создании простого вспомогательного метода HTML, который визуализирует Теги&gt; HTML &lt;IMG.

## <a name="overview-of-the-tagbuilder-class"></a>Общие сведения о классе TagBuilder

Класс TagBuilder содержится в пространстве имен System. Web. MVC. Он имеет пять методов:

- Аддксскласс () — позволяет добавить в тег новый атрибут *class = ""* .
- Женератеид () — позволяет добавить атрибут ID в тег. Этот метод автоматически замещает точки в идентификаторе (по умолчанию периоды заменяются символами подчеркивания)
- Мержеаттрибуте () — позволяет добавлять атрибуты в тег. Существует несколько перегрузок этого метода.
- Сетиннертекст () — позволяет задать внутренний текст тега. Внутренний текст кодируется автоматически в формате HTML.
- ToString () — позволяет визуализировать тег. Можно указать, следует ли создать стандартный тег, открывающий тег, закрывающий тег или самозакрывающийся тег.

Класс TagBuilder имеет четыре важных свойства:

- Атрибуты — представляет все атрибуты тега.
- Идаттрибутедотреплацемент — представляет символ, используемый методом Женератеид () для замены точек (по умолчанию — символ подчеркивания).
- InnerHTML — представляет внутреннее содержимое тега. Назначение строки этому свойству не *приводит* к кодированию строки в формате HTML.
- TagName — представляет имя тега.

Эти методы и свойства предоставляют все основные методы и свойства, необходимые для создания HTML-тега. Вам не нужно использовать класс TagBuilder. Вместо этого можно использовать класс StringBuilder. Тем не менее, класс TagBuilder немного упрощает вашу жизнь.

## <a name="creating-an-image-html-helper"></a>Создание вспомогательного приложения HTML для изображения

При создании экземпляра класса TagBuilder передается имя тега, который требуется построить в конструкторе TagBuilder. Затем можно вызвать методы, такие как методы Аддксскласс и Мержеаттрибуте (), для изменения атрибутов тега. Наконец, вызывается метод ToString () для отображения тега.

Например, листинг 1 содержит вспомогательный код HTML изображения. Вспомогательный модуль изображения реализуется внутренним образом с TagBuilder, представляющим тег HTML &lt;IMG&gt;.

**Листинг 1 — Хелперс\имажехелпер.ВБ**

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

Модуль в листинге 1 содержит два перегруженных метода с именем Image (). При вызове метода Image () можно передать объект, представляющий набор атрибутов HTML.

Обратите внимание, что метод TagBuilder. Мержеаттрибуте () используется для добавления отдельных атрибутов, таких как атрибут src, в TagBuilder. Кроме того, обратите внимание, как метод TagBuilder. Мержеаттрибутес () используется для добавления коллекции атрибутов в TagBuilder. Метод Мержеаттрибутес () принимает словарь&lt;строку, объект&gt; параметр. Класс Раутевалуедиктионари используется для преобразования объекта, представляющего коллекцию атрибутов, в словарь&lt;строку, объект&gt;.

После создания вспомогательного приложения для изображений можно использовать вспомогательное приложение в представлениях ASP.NET MVC, как и любые другие стандартные вспомогательные методы HTML. Представление в листинге 2 использует вспомогательный метод Image для отображения одного и того же изображения Xbox дважды (см. рис. 1). Вспомогательный объект Image () вызывается как с коллекцией атрибутов HTML, так и без нее.

**Листинг 2 — Хоме\индекс.аспкс**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

[![диалоговом окне «Создание проекта»](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)

**Рис. 01**. Использование вспомогательного приложения Image ([щелкните, чтобы просмотреть изображение с полным размером](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))

Обратите внимание, что необходимо импортировать пространство имен, связанное с вспомогательным модулем изображения, в верхней части представления index. aspx. Вспомогательный модуль импортируется с помощью следующей директивы:

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

В Visual Basicном приложении пространство имен по умолчанию совпадает с именем приложения.

> [!div class="step-by-step"]
> [Назад](creating-custom-html-helpers-vb.md)
> [Вперед](creating-page-layouts-with-view-master-pages-vb.md)
