---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: Введение в ASP.NET MVC 3 (Visual Basic) | Документация Майкрософт
author: Rick-Anderson
description: Этом учебнике описываются основы создания MVC веб-приложения ASP.NET с помощью Microsoft Visual Web Developer 2010 Express пакетом обновления 1, который является...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 47c9d69b9fee4a9e126ef2e889c91fe0bdd479f6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385934"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>Введение в ASP.NET MVC 3 (VB)

по [Рик Андерсон]((https://twitter.com/RickAndMSFT))

> Этом учебнике описываются основы создания MVC веб-приложения ASP.NET с помощью Microsoft Visual Web Developer 2010 Express пакетом обновления 1, которой является бесплатной версии Microsoft Visual Studio. Перед началом работы убедитесь, что вы установили необходимые компоненты, перечисленные ниже. Все из них можно установить, щелкнув следующую ссылку: [Установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того можно установить по отдельности необходимых компонентов, с помощью следующих ссылок:
> 
> - [Необходимые компоненты для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление средств ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(среды выполнения и средства поддержки)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Необходимые компоненты для Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Проект Visual Web Developer с VB.NET исходный код доступен на следующей странице в этом разделе. [Загрузить версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Если вы предпочитаете C#, переключитесь в [C# версии](../cs/intro-to-aspnet-mvc-3.md) работы с этим руководством.


Этом учебнике описываются основы создания MVC веб-приложения ASP.NET с помощью Microsoft Visual Web Developer 2010 Express пакетом обновления 1, которой является бесплатной версии Microsoft Visual Studio. Перед началом работы убедитесь, что вы установили необходимые компоненты, перечисленные ниже. Все из них можно установить, щелкнув следующую ссылку: [Установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того можно установить по отдельности необходимых компонентов, с помощью следующих ссылок:

- [Необходимые компоненты для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [Обновление средств ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(среды выполнения и средства поддержки)

Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Необходимые компоненты для Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

Проект Visual Web Developer с VB исходный код доступен на следующей странице в этом разделе. [Скачивание версии VB здесь](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824). Если вы предпочитаете c#, переключитесь в [версии c#](../cs/intro-to-aspnet-mvc-3.md) работы с этим руководством.

## <a name="what-youll-build"></a>Что вы создадите

Вы реализуете простое приложение списка фильмов, который поддерживает создание, изменение и список фильмов из базы данных. Ниже приведены два снимка экрана приложения, который вам предстоит создать. Он включает страницы, отображающей список фильмов из базы данных:

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

Приложение также позволяет добавить, изменить и удалить фильмов, а также сведения о см. в разделе сведений об отдельных проблемах. Все сценарии ввода данных включают проверку, чтобы гарантировать правильность данных, хранящихся в базе данных.

[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>Навыки, которые вы узнаете

Вот, вы узнаете, как:

- Как создать новый проект ASP.NET MVC
- Как создать новую базу данных с помощью Entity Framework code first
- Как создать ASP.NET MVC контроллеры и представления
- Получение и отображение данных
- Включение проверки данных и изменения данных

## <a name="getting-started"></a>Начало работы

Загрузите с Visual Web Developer 2010 Express («VWD» для краткости), а затем выберите **новый проект** из **запустить** страницы.

Visual Web Developer — это интегрированная среда разработки, или интегрированной среды разработки. Так же, как использовать Microsoft Word для записи документов, вы используете интегрированную среду разработки для создания приложений. В Visual Web Developer имеется панель инструментов в верхней, показывающий различные параметры, доступные для вас. Имеется также меню, которое предоставляет еще один способ выполнения задач в интегрированной среде разработки. (Например, вместо выбора **новый проект** из **запустить** страницы, можно использовать меню и выберите **файл** &gt; **новый проект**.)

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>Создание первого приложения

Можно создавать приложения с помощью Visual Basic или Visual C# в качестве языка программирования. Для этого руководства выберите Visual Basic в левой части, а затем выберите **веб-приложение ASP.NET MVC 3**. Назовите проект «MvcMovie» и нажмите кнопку **ОК**.

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

В **Создание проекта ASP.NET MVC 3** выберите **веб-приложение**. Оставьте **Razor** как обработчик представлений по умолчанию.

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

Нажмите кнопку **ОК**. Visual Web Developer используется шаблон по умолчанию для проекта ASP.NET MVC, который вы только что создали, поэтому у вас есть рабочее приложение прямо сейчас не выполняя никаких действий! Это связано с простых «Hello World!» проекта, а вот отлично подходит для запуска приложения.

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

В меню **Отладка** выберите пункт **Начать отладку**.

![](intro-to-aspnet-mvc-3/_static/image11.png)

Обратите внимание, что сочетание клавиш, чтобы начать отладку F5.

F5 приводит к Visual Web Developer для запуска веб-сервера разработки и выполнения веб-приложения. Затем VWD запускает браузер и откроется домашняя страница приложения. Обратите внимание, что говорит в адресной строке браузера `localhost` и не что-либо типа `example.com`. Это потому, что `localhost` всегда указывает на локальном компьютере, который выполняется, в этом случае приложение, вы только что выполнили. При запуске веб-проекта материалов по VWD для проекта используется случайный порт. В приведенном ниже рисунке случайный номер порта является 43246. Проект, вероятно, будет использовать другой номер порта.

![](intro-to-aspnet-mvc-3/_static/image12.png)

По умолчанию этот шаблон по умолчанию дает вам две страницы посетить и страницу основное имя для входа. Давайте изменить работу этого приложения и немного поговорим об ASP.NET MVC в процессе. Закройте обозреватель и изменим код.

> [!div class="step-by-step"]
> [Далее](adding-a-controller.md)
