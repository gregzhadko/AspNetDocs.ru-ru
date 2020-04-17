---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Выпуск Заметки для ASP.NET и веб-инструменты 2013.1 для визуальной студии 2012 Документы Майкрософт
author: rick-anderson
description: В этом документе описывается выпуск ASP.NET и Web Tools 2013.1 для Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543578"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Заметки о выпуске ASP.NET and Web Tools 2013.1 для Visual Studio 2012

[корпорацией Майкрософт](https://github.com/microsoft)

> В этом документе описывается выпуск ASP.NET и Web Tools 2013.1 для Visual Studio 2012.

## <a name="contents"></a>Содержимое

- [Примечания к установке](#install)
- [Требования к программному обеспечению](#requirements)
- Новые возможности в ASP.NET и веб-инструменты 2013.1 для визуальной студии 2012

    - [Bootstrap](#bootstrap)
    - [Шаблоны](#templates)

        - [ASP.NET mVC 5 шаблон](#mvc5template)
        - [шаблон web API 2 ASP.NET](#apitemplate)
        - [Шаблоны элементов](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET Леса](#scaffold)
    - [Редактор бритвы](#razor)
    - [NuGet 2.7](#nuget)
- Известные проблемы и ломая изменения

    - [ASP.NET Леса](#issuescaffolding)

        - [MVC и Web API Scaffolding - HTTP 404, не найдена ошибка](#404issue)
        - [Visual Studio Express 2012 для Веб перестает работать после добавления эшафот пункт](#expressissue)
    - [ASP.NET бритва 3](#issuerazor)

        - [Просмотр файла cshtml с помощью Browse With или F5 вызывает ошибку сервера](#browseissue)
        - [Урл Переписать и Тильде (яп.)](#rewriteissue)
    - [Шаблоны](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Замечания по установке

[Установка](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET и web Tools 2013.1 для Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>Требования к программному обеспечению

Вы должны иметь либо Visual Studio 2012 или Visual Studio Express 2012 для Интернета.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Новые возможности в ASP.NET и веб-инструменты 2013.1 для визуальной студии 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Начальная загрузка

Когда вы подмостки MVC 5 контроллеров и представлений, разметка для представлений использует [Bootstrap](http://getbootstrap.com/).

<a id="templates"></a>
### <a name="templates"></a>Шаблоны

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET mVC 5 шаблон

Мы добавили новый шаблон MVC 5. Он ссылается на последние пакеты MVC 5 NuGet, и вы можете использовать строительные леса, чтобы добавить контроллеры и представления.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>шаблон web API 2 ASP.NET

Мы добавили новый шаблон Web API 2. Он ссылается на последние web API 2 NuGet пакеты, и вы можете использовать леса, чтобы добавить контроллеры и представления.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Шаблоны элементов

Мы добавили новые шаблоны элементов для просмотров MVC 5, веб-страниц (Razor 3) и контроллеров Web API 2. Они устанавливают связанные пакеты NuGet в проект при добавлении новых элементов.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Когда вы подмостки MVC или веб-контроллер API с помощью Entity Framework, мы используем Framework 6. Для получения дополнительной информации [Entity Framework Version History](https://msdn.com/data/jj574253)о рамочной системе сущностей см.

Вы также можете скачать и установить Entity Framework 6 Инструменты для визуальной студии 2012. Посмотреть [рамочную программу Get Entity.](https://msdn.com/data/ee712906#tooling)

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Леса

ASP.NET Scaffolding — это платформа для генерации кода для ASP.NET веб-приложений. Это упрощает добавление шаблонного кода в проект, который взаимодействует с моделью данных.

В предыдущих версиях Visual Studio строительные леса ограничивались ASP.NET проектами MVC. С помощью этого обновления теперь можно использовать строительные леса для любого ASP.NET проекта, включая веб-формы. Это обновление не поддерживает генерацию страниц для проекта Web Forms, но вы все равно можете использовать строительные леса с веб-формами, добавляя в проект зависимости MVC. Поддержка создания страниц для веб-форм будет добавлена в будущем обновлении.

При использовании строительных лесов мы гарантируем, что все необходимые зависимости установлены в проекте. Например, если вы начинаете с проекта ASP.NET web Forms, а затем используете строительные леса для добавления контроллера Web API, необходимые пакеты и ссылки NuGet добавляются в ваш проект автоматически.

Чтобы добавить строительные леса MVC в проект Web Forms, добавьте **новый элемент Scaffolded** и выберите **MVC 5 Зависимости** в окне диалога. Есть два варианта для строительных лесов MVC; Минимальный и полный. Если вы выберете Minimal, в проект добавляются только пакеты и ссылки NuGet для ASP.NET MVC. При выборе опции Full добавлены минимальные зависимости, а также необходимые файлы содержимого для проекта MVC.

Поддержка контроллеров асин для строительных лесов использует новые функции async из Entity Framework 6.

Для получения дополнительной информации и учебников, см [ASP.NET Scaffolding Обзор](../2013/aspnet-scaffolding-overview.md). Эти учебники показывают леса с Visual Studio 2013, но они также применимы к ASP.NET и Web Tools 2013.1 для Visual Studio 2012.

<a id="razor"></a>
### <a name="razor-editor"></a>Редактор бритвы

С этим обновлением, Visual Studio 2012 теперь поддерживает Razor 3 инструментария / редактирования.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 включает в себя богатый набор новых функций, которые подробно описаны на [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Эта версия NuGet устраняет необходимость для пользователей явно разрешить NuGet восстановить недостающие пакеты. При установке NuGet 2.7 пользователи косвенно соглашаются на автоматическое восстановление недостающих пакетов. Пользователи могут отказаться от восстановления пакета через настройки NuGet в Visual Studio. Это изменение упрощает работу восстановления пакетов.

## <a name="known-issues-and-breaking-changes"></a>Известные проблемы и ломая изменения

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Леса

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC и Web API Scaffolding - HTTP 404, не найдена ошибка

Если вы столкнулись с ошибкой при добавлении элемента с эшафотом в проект, возможно, ваш проект останется в несогласованном состоянии. Некоторые изменения, внесенные в строительные леса, будут отброшены назад, но другие изменения, такие как установленные пакеты NuGet, не будут отброшены назад. Если изменения конфигурации реаутинга откатываются, пользователи получат ошибку HTTP 404 при навигации по эшафотным элементам.

Чтобы исправить эту ошибку для MVC, добавьте новый элемент леса и выберите MVC 5 зависимостей (минимальные или полные). Этот процесс добавит все необходимые изменения в проект.

Чтобы исправить эту ошибку для Web API:

1. Добавьте в проект следующий класс WebApiConfig.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Нанастройка WebApiConfig.Register\_в методе запуска приложений в Global.asax следующим образом:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 для Веб перестает работать после добавления эшафот пункт

Если Visual Studio Express 2012 для Web перестанет работать после добавления эшафота элемента с Entity Framework (например, Web API 2 Контроллер с действиями, используя Entity Framework), возможно, что Visual Studio Express не удалось загрузить родной образ сборки зависит от System.Web.Extensions.

Чтобы исправить эту проблему, настройте Visual Studio Express для работы с MSIL изображением System.Web.Extensions:

1. Open Command Prompt в режиме администратора.
2. Перейдите к %ProgramFiles% -Microsoft Visual Studio 11.0-Common7-IDE или %ProgramFiles (x86)% -Microsoft Visual Studio 11.0"Common7'IDE (для 64-битной Windows).
3. Открыть VWDExpress.exe.config в текстовом редакторе.
4. Добавьте следующую &lt;строку&gt; под элементом времени выполнения конфигурации:&gt;/&lt;  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Перезапуск Visual Studio Express 2012 для Интернета.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET бритва 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Просмотр файла cshtml с помощью Browse With или F5 вызывает ошибку сервера

При создании проекта MVC 5 в Visual Studio 2012 (или открыть в Visual Studio 2012 проект MVC 5, который был создан в Visual Studio 2013) и попытаться просмотреть файл cshtml с помощью Browse With или F5, вы получите ошибку, которая гласит - **Ошибка сервера в '/' Приложение**. Сервер пытается перейти к`http://localhost:XXXX/Views/../XXXX.cshtml`

Чтобы решить эту проблему, измените настройку **start Action** в проекте на **конкретную страницу.** Вам не нужно предоставлять значение для страницы.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

После внесения этого изменения, выбрав F5 переходит`http://localhost:XXXX`к корню приложения ( ). Это поведение не то же самое, что поведение для проектов MVC 5 в Visual Studio 2013, где **настройка текущей страницы** запускает открытую страницу.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Урл Переписать и Тильде (яп.)

После обновления до ASP.NET Razor 3 или ASP.NET MVC 5, нотация tilde может больше не работать правильно, если вы используете перезаписи URL. Перезапись URL-адреса влияет на нотацию tilde (я)&gt; &lt;в&gt;HTML-элементах, таких как &lt; &lt;A/ SCRIPT/ , LINK/&gt;, и в результате tilde больше не отображает карты в корневом каталоге.

Например, если вы переписываете запросы на **asp.net/content** **asp.net,** &lt;атрибут href в&gt; A href'/content/"/ **/** разрешает **/content/content/** вместо . Чтобы подавить это изменение, можно настроить контекст **IIS\_WasUrlRewritten** на ложный на каждой веб-странице или в **\_Application BeginRequest** в Global.asax.

<a id="templateissue"></a>
### <a name="templates"></a>Шаблоны

При создании ASP.NET проектов MVC с Visual Studio 2012 на Windows 8.1 или Windows Server 2012 R2, Visual Studio отображает сообщение об ошибке, в которое говорится: «Настройка Web для ASP.NET 4.5 не удалось».

![ошибка конфигурации](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Вы видите эту ошибку, потому что Visual Studio 2012 не включает функцию ASP.NET 4.5 при установке на эти релизы Windows. Для включения или выключения ASP.NET 4.5 выполняйте действия, описанные в [функциях Включайте или выключаемого.](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)

![Включать или выключать функции Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Кроме того, можно включить ASP.NET 4.5 через командную строку.

1. Open Command Prompt в режиме администратора.
2. Выполнить следующую команду, чтобы включить ASP.NET 4.5.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
