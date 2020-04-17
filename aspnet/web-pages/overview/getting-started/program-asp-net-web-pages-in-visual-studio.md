---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Программирование ASP.NET веб-страниц (Razor) с помощью визуальной студии (ru) Документы Майкрософт
author: Rick-Anderson
description: В этом приложении объясняется, как можно использовать Visual Studio 2010 или Visual Web Developer 2010 Express для программы ASP.NET веб-страниц с помощью синтаксиса Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542902"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Программирование ASP.NET веб-страниц (Razor) с помощью визуальной студии

; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)

> В этой статье объясняется, как можно использовать Visual Studio или Visual Web Developer Express для программы ASP.NET веб-страниц (Razor) веб-сайтов.
>
> Что вы узнаете
>
> - Что нужно установить (если что) для работы с веб-страницами ASP.NET в вашей версии Visual Studio.
> - Как добавить поддержку для веб-страниц ASP.NET Visual Web Developer 2010 Express.
> - Как использовать функции в Visual Studio для работы с ASP.NET страниц, включая IntelliSense и отладчик.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в учебнике
>
>
> - ASP.NET веб-страниц (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Этот учебник также работает с ASP.NET web Pages 2, Visual Studio 2012, Visual Studio 2010 и WebMatrix 2.

Вы можете запрограммировать ASP.NET веб-страниц с помощью синтаксиса Razor с помощью WebMatrix или многих других редакторов кода. Вы также можете использовать Microsoft Visual Studio, которая является полнофункциональным интегрированной средой разработки (IDE), которая обеспечивает мощный набор инструментов для создания многих типов приложений (а не только веб-сайтов). Для работы с ASP.NET страниц razor, вы можете использовать [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

Две особенно полезные функции, которые Visual Studio предоставляет для программирования с ASP.NET веб-страниц Razor являются:

- *IntelliSense*. Функция IntelliSense, встроенная в Visual Studio, более полная, чем IntelliSense в WebMatrix.
- *Дебудгер*. Отладчик позволяет устранить неполадки, остановив программу во время ее работы, изучая переменные и перешагнув строку кода по строке.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Использование Visual Studio с различными версиями ASP.NET веб-страниц

Для разработки ASP.NET веб-приложений в Visual Studio 2017, установите рабочую нагрузку **ASP.NET и веб-разработки.**

Visual Studio 2012 и Visual Studio 2013 включают поддержку ASP.NET веб-страниц. (Пакеты, необходимые для поддержки ASP.NET веб-страниц, устанавливаются при установке Visual Studio.)

Visual Studio 2010 не включает поддержку по умолчанию для ASP.NET web Pages. Чтобы использовать ASP.NET веб-страницсы с Visual Studio 2010, необходимо установить пакет mVC ASP.NET. Чтобы получить ASP.NET веб-страниц 2, вы установите ASP.NET MVC 4.

В следующей таблице кратко излагается поддержка веб-страниц ASP.NET в различных версиях Visual Studio.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **Веб-страницы ASP.NET 2** | Установка ASP.NET MVC 4 | (Включено) | (Включено) |
| **Веб-страницы ASP.NET 3** |  | Обновление для ASP.NET веб-страниц 3 через NuGet | (Включено) |

Для работы с Visual Studio 2010, см [Установка поддержки для ASP.NET веб-страниц в Visual Studio 2010](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>Запуск визуальной студии от WebMatrix

Если вы начали проект в WebMatrix и хотите перейти на Visual Studio, WebMatrix предоставляет кнопку, чтобы легко открыть проект в Visual Studio. Для включения этой кнопки на компьютере должна быть установлена Visual Studio. Следующее изображение показывает кнопку в WebMatrix.

![запуск Визуальной студии](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

При нажатии кнопки проект открывается в Visual Studio. Вы можете переключаться между WebMatrix и Visual Studio без каких-либо проблем. Вы будете уведомлены, если какие-либо файлы изменились в другой среде и должны быть перезагружены, чтобы получить последние изменения.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Создание сайта ASP.NET Razor в визуальной студии

Чтобы создать веб-сайт ASP.NET Razor в Visual Studio:

1. Запустите Visual Studio.
2. В меню **файла** нажмите **новый веб-сайт**.

    ![создать новый веб-сайт](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. В новом диалоговом окне **веб-сайта** выберите язык для использования (Visual C или Visual Basic).
4. Выберите шаблон **веб-сайта ASP.NET (Razor).**

    ![razor сайт](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. Нажмите кнопку **ОК**.

Ваш новый проект существует и населен некоторыми веб-страницами по умолчанию, которые помогут вам начать работу.

### <a name="using-intellisense"></a>Using IntelliSense

Теперь, когда вы создали сайт, вы можете увидеть, как работает IntelliSense в Visual Studio.

1. На сайте, который вы только что создали, откройте страницу *Default.cshtml.*
2. После `<h3>` тегов на странице `@ServerInfo.` введите (включая точку). Обратите внимание, как IntelliSense отображает `ServerInfo` доступные методы для помощника в списке выпадающих.

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Выберите `GetHtml` метод из списка, а затем нажмите Enter. IntelliSense автоматически заполняет метод. (Как и в случае с любым `()` методом в C, вы должны добавить символы после метода.) Завершенный код `GetHtml` для метода выглядит следующим примером:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Нажмите ctrl-F5, чтобы запустить страницу. Вот как выглядит страница при отображении в браузере:

    ![страница по умолчанию в браузере](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Закройте браузер.

### <a name="using-the-debugger"></a>Использование debugger

1. В верхней части страницы *Default.cshtml,* после `Page.Title`строки, которая начинается с, добавьте следующую строку кода:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. В сером крае редактора слева от кода нажмите рядом с этой новой строкой, чтобы добавить *точку разрыва.* Точка разрыва — это маркер, который говорит отладчику прекратить запуск программы в этот момент, чтобы вы могли видеть, что происходит.

    ![установка точки останова](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Удалите вызов `ServerInfo.GetHtml` методу и добавьте `@myTime` вызов к переменной на своем месте. Этот вызов отображает текущее значение времени, возвращенное новой строкой кода.
4. Нажмите F5, чтобы запустить страницу в отладчике. Страница останавливается на точке разрыва, которую вы установили. Следующее изображение показывает, как выглядит страница в редакторе с точкой разрыва (желтым цветом).

    ![точка разрыва отладки](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. В панели инструментов Debug нажмите кнопку **«Шаг в»** (или нажмите F11), чтобы запустить следующую строку кода. Каждый раз, когда вы нажимаете на эту кнопку, вы продвигаете выполнение к следующей строке кода.

    ![Шаг в кнопку](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Изучите значение `myTime` переменной, удерживая указатель мыши над ней или проверяя значения, отображаемые в окнах **Locals** и **Call Stack.** Visual Studio отображает значение переменной.

    ![значение времени показа](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Когда вы закончите изучение переменной и прохождение кода, нажмите F5, чтобы продолжить работу страницы, не останавливаясь на каждой строке. Когда вы закончите шаг через весь код, браузер отображает страницу.

Чтобы узнать больше об отладчике и о том, как отладить код в Visual Studio, смотрите [Walkthrough: Отладка веб-страниц в визуальном веб-разработчике.](https://msdn.microsoft.com/library/z9e7w6cs.aspx)

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Использование Razor в ASP.NET проектов MVC с Visual Studio

Синтаксис Razor также широко используется в ASP.NET проектах MVC. MVC — это мощный способ создания динамических веб-сайтов на основе шаблонов. Если ваш ASP.NET веб-страницу становится трудно поддерживать, можно рассмотреть возможность его преобразования в ASP.NET приложение MVC. Например, при создании приложения MVC см. [Начало работы с ASP.NET MVC 5.](../../../mvc/overview/getting-started/introduction/getting-started.md)

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Установка поддержки для веб-страниц ASP.NET в визуальной студии 2010

В этом разделе показано, как установить Visual Web Developer Express 2010 и ASP.NET веб-страниц инструменты для визуальной студии.

1. Если у вас еще нет web-платформы Установщик, загрузите его из следующего URL:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Выполнить веб-платформы Установки.
3. Нажмите на вкладку **«Продукты».**

    ![Вкладка Продуктов WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. Поиск **ASP.NET MVC 4** (для ASP.NET веб-страниц 2), а затем нажмите **Добавить**. Эти продукты включают в себя инструменты Visual Studio для создания ASP.NET веб-сайтов Razor.

    ![Параметры установки WebPi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Нажмите **Установить** для завершения установки.
