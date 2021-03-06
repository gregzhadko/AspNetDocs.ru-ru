---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: Часть 1. Обзор и файл-> новый проект | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 1 охватывает общие сведения и файловый > новый проект.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451284"
---
# <a name="part-1-overview-and-file-new-project"></a>Часть 1. Обзор и файл > новый проект

[Джон Гэллоуэй](https://github.com/jongalloway)

> Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.  
>   
> Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.  
>   
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 1 охватывает общие сведения и файловый&gt;новый проект.

## <a name="overview"></a>Обзор

Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Web Developer для разработки веб-приложений. Мы будем замедленнее, так что веб-разработка на уровне "новичок" работает.

Приложение, которое мы будем создавать, — это простое музыкальное хранилище. Приложение состоит из трех основных частей: покупки, извлечения и администрирования.

![](mvc-music-store-part-1/_static/image1.jpg)

Посетители могут просматривать альбомы по жанрам:

![](mvc-music-store-part-1/_static/image2.jpg)

Они могут просматривать один альбом и добавлять его в корзину:

![](mvc-music-store-part-1/_static/image3.jpg)

Они могут просматривать свою корзину, удаляя все ненужные элементы:

![](mvc-music-store-part-1/_static/image4.jpg)

При переходе к извлечению будут предложены вход в систему или регистрация для учетной записи пользователя.

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

После создания учетной записи она может выполнить заказ, заполнив сведения о доставке и оплате. Для простоты мы используем неудивительное продвижение: все это бесплатное, если ввести код продвижения "FREE"!

![](mvc-music-store-part-1/_static/image5.jpg)

После упорядочения они видят простой экран подтверждения:

![](mvc-music-store-part-1/_static/image6.jpg)

Помимо страниц, предназначенных для клиентов, мы также создадим раздел администратора со списком альбомов, из которых администраторы могут создавать, изменять и удалять альбомы.

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. файл-&gt; новый проект

### <a name="installing-the-software"></a>Установка программного обеспечения

В этом руководстве мы начнем с создания нового проекта ASP.NET MVC 3 с помощью бесплатного выпуска Visual Web Developer 2010 Express (бесплатное), а затем постепенно добавим компоненты для создания полноценного приложения. Кроме того, мы будем охватывать доступ к базам данных, сценарии разнесения форм, проверку данных, использование главных страниц для согласованного макета страниц, использование AJAX для обновления страниц и проверки, входа пользователей и т. д.

Вы можете следовать пошаговым инструкциям или скачать готовое приложение из [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).

Для создания приложения можно использовать Visual Studio 2010 с пакетом обновления 1 (SP1) или Visual Web Developer 2010 Express с пакетом обновления 1 (SP1) (бесплатная версия Visual Studio 2010). Мы будем использовать SQL Server Compact (также бесплатный) для размещения базы данных. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже.

- [Предварительные требования для Visual Studio Web Developer Express SP1]
- [ASP.NET MVC 3 Tools Update]
- [SQL Server Compact 4,0] — включая поддержку среды выполнения и средств

### <a name="creating-a-new-aspnet-mvc-3-project"></a>Создание нового проекта ASP.NET MVC 3

Начнем с выбора пункта "создать проект" в меню "файл" в Visual Web Developer. Откроется диалоговое окно Новый проект.

![](mvc-music-store-part-1/_static/image5.png)

Мы выберем группу веб C# -шаблонов Visual&gt; слева, а затем выбираете шаблон "веб-приложение ASP.NET MVC 3" в центральном столбце. Присвойте проекту имя Мвкмусиксторе и нажмите кнопку ОК.

![](mvc-music-store-part-1/_static/image8.jpg)

При этом отобразится вторичное диалоговое окно, которое позволит нам внести в проект определенные параметры MVC. Выберите следующее:

Шаблон проекта — выберите пустой

Просмотр подсистемы — выбор Razor

Использовать семантическую разметку HTML5 — проверяется

Проверьте параметры, как показано ниже, а затем нажмите кнопку ОК.

![](mvc-music-store-part-1/_static/image9.jpg)

Будет создан наш проект. Давайте взглянем на папки, добавленные в наше приложение в обозреватель решений с правой стороны.

![](mvc-music-store-part-1/_static/image10.jpg)

Пустой шаблон MVC 3 не полностью пуст — он добавляет простую структуру папок:

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC использует некоторые основные соглашения об именовании имен папок:

| **Папка** | **Назначение** |
| --- | --- |
| **/контроллерс** | Контроллеры реагируют на входные данные из браузера, решают, что делать с ним и возвращают ответ пользователю. |
| **/Views** | Представления содержат шаблоны пользовательского интерфейса |
| **/моделс** | Модели хранят данные и манипулируют ими |
| **/контент** | Эта папка содержит наши образы, CSS и любые другие статические материалы |
| **/Scripts** | В этой папке содержатся файлы JavaScript |

Эти папки включаются даже в пустое приложение MVC ASP.NET, поскольку платформа ASP.NET MVC по умолчанию использует подход "соглашение по конфигурации" и делает некоторые предположения по умолчанию на основе соглашений об именовании папок. Например, контроллеры ищут представления в папке Views по умолчанию без явного указания этого значения в коде. При использовании соглашений по умолчанию уменьшается объем кода, который необходимо написать, а также может облегчить другим разработчикам понимание проекта. Мы объясним эти соглашения более подробно, как мы создаем наше приложение.

> [!div class="step-by-step"]
> [Дальше](mvc-music-store-part-2.md)
