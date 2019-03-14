---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: Использование ASP.NET MVC с разными версиями служб IIS (C#) | Документация Майкрософт
author: microsoft
description: В этом руководстве вы узнаете, как использовать ASP.NET MVC и маршрутизация URL-адресов, с разными версиями служб IIS. Вы узнаете, различные стратегии...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: aa7d00c0f54212d495f48929ed2a453942a1ed7d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039671"
---
<a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>Использование ASP.NET MVC с разными версиями служб IIS (C#)
====================
по [Microsoft](https://github.com/microsoft)

> В этом руководстве вы узнаете, как использовать ASP.NET MVC и маршрутизация URL-адресов, с разными версиями служб IIS. Вы узнаете, различные стратегии по использованию ASP.NET MVC с IIS 7.0 (классический режим), IIS 6.0 и более ранних версий IIS.


Платформа ASP.NET MVC зависит от маршрутизация ASP.NET перенаправлять запросы браузера к действиям контроллера. Чтобы воспользоваться преимуществами маршрутизации ASP.NET, может потребоваться выполнить дополнительные действия по настройке веб-сервера. Все зависит от версии Internet Information Services (IIS) и режим для приложения обработки запроса.

Вот краткий перечень различных версиях IIS:

- IIS 7.0 (интегрированный режим) — без специальной настройки, необходимые для использования маршрутизации ASP.NET.
- IIS 7.0 (классический режим) — необходимо выполнить специальную конфигурацию для использования маршрутизации ASP.NET.
- IIS 6.0 или ниже - необходимо выполнить специальную конфигурацию для использования маршрутизации ASP.NET.

Последнюю версию служб IIS версии 7.5 (в Windows 7). IIS 7 IIS, включенные в Windows Server 2008 и VISTA/SP1 и более поздних версий. IIS 7.0 можно установить в любой версии операционной системы Vista, кроме Home Basic (см. в разделе [ https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx ](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).

IIS 7.0 поддерживает два режима для обработки запросов. Можно использовать в режиме интеграции с или классическом режиме. Не нужно ничего делать, специальной настройки при использовании IIS 7.0 в интегрированном режиме. Тем не менее необходимо выполнить дополнительную настройку, при использовании IIS 7.0 в классическом режиме.

Microsoft Windows Server 2003 включает в себя IIS 6.0. При использовании операционной системы Windows Server 2003 невозможно обновить IIS 6.0 на IIS 7.0. При использовании IIS 6.0, необходимо выполнить дополнительные действия по настройке.

Microsoft Windows XP Professional включает в себя IIS 5.1. При использовании IIS 5.1, необходимо выполнить дополнительные действия по настройке.

Наконец Microsoft Windows 2000 и Microsoft Windows 2000 Professional включает в себя IIS 5.0. При использовании IIS 5.0 необходимо выполнить дополнительные действия по настройке.

## <a name="integrated-versus-classic-mode"></a>Интегрированные и классический режим

IIS 7.0, может обрабатывать запросы с помощью двух режимов обработки других запросов: интегрированный и классический. В режиме интеграции с обеспечивает более высокую производительность и дополнительные функции. Классический режим включена для обеспечения обратной совместимости с предыдущими версиями служб IIS.

Режим обработки запроса определяется пула приложений. Можно определить, какой режим обработки используется веб-приложение путем определения пула приложений, связанных с приложением. Выполните следующие действия.

1. Запустите диспетчер служб IIS
2. В окне подключения выберите приложение
3. В окне «действия» выберите **основные параметры** ссылку, чтобы открыть диалоговое окно Изменение приложения (см. рис. 1)
4. Запишите выбранного пула приложений.

По умолчанию службы IIS настроены для поддержки два пула приложений: **DefaultAppPool** и **классический пул приложений .NET**. Если выбран DefaultAppPool, приложение работает в режиме. Если выбран Classic .NET AppPool, приложение запущено в режиме классического запрос обработки.

[![В диалоговом окне нового проекта](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**Рис. 1**: Обнаружение режима обработки запроса ([Просмотр полноразмерного изображения](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))

Обратите внимание на то, что можно изменить режим обработки запроса в диалоговом окне Изменение приложения. Нажмите кнопку Выбрать и изменить пул приложений, связанный с приложением. Учтите, что существуют проблемы совместимости при изменении приложения ASP.NET из классической модели развертывания в режиме интеграции с. Дополнительные сведения см. в следующих статьях:

- Обновление ASP.NET 1.1 в IIS 7.0 на Windows Vista и Windows Server 2008 — [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- Интеграция ASP.NET с IIS 7.0: [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

Если приложение ASP.NET использует DefaultAppPool, не нужно выполнять никакие дополнительные действия, чтобы получить маршрутизация ASP.NET (и, следовательно ASP.NET MVC) для работы. Тем не менее если приложение ASP.NET настроено использовать на Classic .NET AppPool, а затем продолжите чтение, у вас есть больше работы.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>С помощью ASP.NET MVC с более ранними версиями служб IIS

Если вам нужно использовать ASP.NET MVC с помощью более старой версии IIS до IIS 7.0, или необходимо использовать IIS 7.0 в классическом режиме, затем можно двумя способами. Во-первых можно изменить в таблице маршрутов для использования расширений файлов. Например вместо запроса URL-адресу вида /Store/Details, необходимо запросить URL-адресу вида /Store.aspx/Details.

Второй вариант — создать так называемую *сопоставления*. Сопоставления позволяет сопоставить каждый запрос в платформу ASP.NET.

Если у вас нет доступа к веб-серверу (например, your ASP.NET MVC приложение размещается поставщиком услуг Интернета) необходимо использовать первый вариант. Если вы не хотите изменять внешний вид URL-адреса, и у вас есть доступ к веб-серверу, можно использовать второй вариант.

Мы рассмотрим каждый параметр подробно в следующих разделах.

## <a name="adding-extensions-to-the-route-table"></a>Добавление расширений в таблицу маршрутов

Для получения маршрутизация ASP.NET для работы с более ранними версиями служб IIS проще изменить свою таблицу маршрутов в файле Global.asax. Значение по умолчанию и неизмененный файл Global.asax в листинге 1 настраивает один маршрут с именем маршрут по умолчанию.

**В листинге 1 - Global.asax (без изменений)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

Маршрут по умолчанию, настроенный в листинге 1 позволяет указать URL-адреса маршрута, которые выглядят следующим образом:

/ Home/Index

/ Продукта/сведения/3

/ Продукта

К сожалению более старых версиях IIS не будет передавать эти запросы к платформе ASP.NET. Таким образом эти запросы не будут направляться к контроллеру. Например если запрос браузера для URL-адрес/Home/Index затем вы получите страницы ошибки на рис. 2.

[![В диалоговом окне нового проекта](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**Рис. 2**: Сообщение об ошибке 404 не найдено ([Просмотр полноразмерного изображения](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))

Более старых версиях IIS сопоставить только определенных запросов для платформы ASP.NET. Запрос должен быть URL-адрес с расширением правый файл. Например запрос /SomePage.aspx получает сопоставляются с платформы ASP.NET. Тем не менее запрос /SomePage.htm не поддерживает.

Таким образом Чтобы получить маршрутизации ASP.NET, мы необходимо изменить маршрут по умолчанию, таким образом, чтобы он включал расширение файла, который сопоставляется с платформы ASP.NET.

Это делается с помощью сценария с именем `registermvc.wsf`. Он был включен с выпуском ASP.NET MVC 1 в `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, но начиная с ASP.NET 2 этот сценарий был перемещен в ASP.NET Futures, найти по адресу [ http://aspnet.codeplex.com/releases/view/39978 ](http://aspnet.codeplex.com/releases/view/39978).

Регистрирует новый модуль MVC было связано со службами IIS для выполнения этого сценария. После регистрации расширения MVC было связано, можно изменить свои маршруты в файле Global.asax, маршруты использовать расширения MVC было связано.

Измененный файл Global.asax в листинге 2 работает с более ранними версиями служб IIS.

**В листинге 2 - Global.asax (изменено с расширениями)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**Важные**: помните, для построения приложения MVC ASP.NET после изменения файла Global.asax.

Существует два важных изменения в файл Global.asax в листинге 2. Теперь имеется два маршрута, определенный в файле Global.asax. Шаблон URL-адреса для маршрута по умолчанию первый маршрут, теперь выглядит как:

{controller}.mvc/{action}/{id}

Добавление расширения MVC было связано изменяет тип файлов, которые перехватывает модуль маршрутизации ASP.NET. Благодаря этому изменению приложение ASP.NET MVC теперь направляет запросы следующим образом:

/Home.mvc/Index/

/Product.MVC/Details/3

/Product.MVC/

Второй маршрут корневого маршрута является новым. Этот шаблон URL-адреса для корневого маршрута является пустой строкой. Этот маршрут необходим для сопоставления запросов, сделанных к корню приложения. Например корневого маршрута будут соответствовать запросу, который выглядит следующим образом:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

После внесения этих изменений в свою таблицу маршрутов, необходимо убедиться, что все ссылки в приложении, совместимы с этих новых шаблонов URL-адрес. Другими словами убедитесь, что все ссылки расширение MVC было связано. Если используется вспомогательный метод Html.ActionLink() для создания ссылок, то нет необходимости вносить изменения.

Вместо того чтобы использовать скрипт registermvc.wcf, можно добавить новое расширение для IIS, который сопоставляется с ASP.NET framework вручную. При добавлении нового расширения самостоятельно, убедитесь, что флажок с меткой **проверка наличия файла** не проверяется.

## <a name="hosted-server"></a>Размещенный сервер

Не всегда имеется доступ к веб-серверу. Например при размещении приложения ASP.NET MVC с помощью поставщика размещения Интернета, затем вы не обязательно доступ к службам IIS.

В этом случае следует использовать одно из существующих расширений файлов, которые сопоставляются с платформы ASP.NET. Расширения файлов, которые сопоставляются с ASP.NET примеры aspx, .axd и .ashx расширения.

Например измененный файл Global.asax в листинге 3 использует расширение .aspx вместо расширения MVC было связано.

**Листинг 3 - Global.asax (изменено с расширениями .aspx)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

Файл Global.asax в листинге 3 именно так же, как предыдущий файл Global.asax, за тем исключением, что он использует расширение .aspx вместо расширения MVC было связано. У вас нет выполнение настройки удаленного веб-сервера для работы с расширением .aspx.

## <a name="creating-a-wildcard-script-map"></a>Создание карты сценария с подстановочными знаками

Если вы не хотите изменять URL-адреса для своего приложения ASP.NET MVC, и у вас есть доступ к веб-серверу, доступны дополнительные параметры. Можно создать сопоставления, сопоставляет все запросы на веб-сервер для ASP.NET framework. Таким образом, можно использовать значение по умолчанию таблица маршрутов ASP.NET MVC с IIS 7.0 (в классическом режиме) или IIS 6.0.

Имейте в виду, что этот параметр вызывает завершение службы IIS, чтобы перехватывать каждый запрос к веб-сервера. Сюда входят запросы для изображений, классических страниц ASP и HTML-страницы. Таким образом Включение подстановочного знака карты скриптов для ASP.NET негативно влиять на производительность.

Вот, как включить сопоставления для IIS 7.0:

1. Выберите приложение из окна "подключения"
2. Убедитесь, что **функции** выбрано представление
3. Дважды щелкните **сопоставления обработчика** кнопки
4. Нажмите кнопку **Добавление сопоставления сценария с подстановочными знаками** связи (см. рис. 3)
5. Введите путь к aspnet\_isapi.dll файл (можно скопировать этот путь из сопоставления сценария PageHandlerFactory)
6. Введите имя MVC
7. Нажмите кнопку **ОК** кнопки

[![В диалоговом окне нового проекта](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**Рис. 3**: Создание сопоставления с помощью IIS 7.0 ([Просмотр полноразмерного изображения](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))

Выполните следующие действия, чтобы создать сопоставления с IIS 6.0.

1. Щелкните правой кнопкой мыши веб-сайт и выберите свойства
2. Выберите **домашний каталог** вкладку
3. Нажмите кнопку **конфигурации** кнопки
4. Выберите **сопоставления** вкладку
5. Нажмите кнопку **вставить** кнопку (см. рис. 4)
6. Вставьте путь для aspnet\_isapi.dll в поле исполняемого файла (из карты скриптов для ASPX-файлов можно скопировать этот путь)
7. Снимите флажок **убедитесь, что файл существует**
8. Нажмите кнопку **ОК** кнопки

[![В диалоговом окне нового проекта](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**Рис. 4**: Создание сопоставления с IIS 6.0 ([Просмотр полноразмерного изображения](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))

После включения универсальных сопоставлений, необходимо внести изменения в таблице маршрутов в файле Global.asax, таким образом, чтобы он включал корневого маршрута. В противном случае вы получите страницы ошибки на рис. 5 при создании запроса для корневой страницы приложения. Можно использовать измененный файл Global.asax в листинге 4.

[![В диалоговом окне нового проекта](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**Рис. 5**: Отсутствует корневая ошибка маршрута ([Просмотр полноразмерного изображения](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))

**Листинг 4 - Global.asax (изменено с корневого маршрута)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

После включения сопоставления для IIS 7.0 или IIS 6.0, можно выполнять запросы, которые работают с таблицей маршрутов по умолчанию, которые выглядят следующим образом:

/

/ Home/Index

/ Продукта/сведения/3

/ Продукта

## <a name="summary"></a>Сводка

Цель этого учебника было объяснить, как использовать ASP.NET MVC при использовании более старой версии IIS (или IIS 7.0 в классическом режиме). Мы рассмотрели два метода получения, маршрутизация ASP.NET для работы с более старых версиях IIS: Изменить таблицу маршрутов по умолчанию или создать сопоставления.

Первый вариант необходимо изменить URL-адреса, используемые в приложении ASP.NET MVC. Один очень значительное преимущество, этот первый параметр является то, что вам не нужен доступ к веб-сервера для изменения таблицы маршрутов. Это означает, что даже в том случае, при размещении приложения ASP.NET MVC в Интернете, можно использовать этот первый вариант хостинга.

Второй вариант — создать сопоставления. Из второй вариант удобен тем, что не нужно изменять URL-адреса. Недостатком второго варианта является то, что может повлиять на производительность приложения ASP.NET MVC.

> [!div class="step-by-step"]
> [Вперед](using-asp-net-mvc-with-different-versions-of-iis-vb.md)