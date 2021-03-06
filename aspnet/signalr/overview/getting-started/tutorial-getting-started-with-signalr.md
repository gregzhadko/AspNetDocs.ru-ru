---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: Учебник. чат в режиме реального времени с SignalR 2 | Документация Майкрософт
author: bradygaster
description: В этом учебнике содержатся сведения об использовании SignalR для создания приложения разговора в режиме реального времени. Вы добавляете SignalR в пустое веб-приложение ASP.NET.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431568"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>Учебник. чат в режиме реального времени с SignalR 2

В этом руководстве показано, как использовать SignalR для создания приложения разговора в режиме реального времени. Вы добавляете SignalR в пустое веб-приложение ASP.NET и создаете HTML-страницу для отправки и вывода сообщений.

Изучив это руководство, вы:

> [!div class="checklist"]
> * Настройка проекта
> * Запуск примера
> * Анализ кода

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>предварительные требования

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) с рабочей нагрузкой **ASP.NET и веб-разработка**.

## <a name="set-up-the-project"></a>Настройка проекта

В этом разделе показано, как использовать Visual Studio 2017 и SignalR 2 для создания пустого веб-приложения ASP.NET, добавления SignalR и создания приложения для разговора.

1. В Visual Studio создайте веб-приложение ASP.NET.

    ![Создание веб-сайта](tutorial-getting-started-with-signalr/_static/image2.png)

1. В окне **New ASP.NET Project-сигналрчат** оставьте **пустым** выбранным и нажмите кнопку **ОК**.

1. В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.

1. В окне **Добавить новый элемент — сигналрчат**выберите **установлено** > **Visual C#**  > **Web** > **SignalR** , а затем выберите **класс концентратора SignalR (v2)** .

1. Назовите класс *часуб* и добавьте его в проект.

    На этом шаге создается файл класса *ChatHub.CS* и добавляется набор файлов скриптов и ссылок на сборки, которые поддерживают SignalR в проекте.

1. Замените код в новом файле класса *ChatHub.CS* следующим кодом:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **новый элемент**.

1. В **меню Добавить новый элемент — сигналрчат** выберите **установлено** > **Visual C#**  > **Web** , а затем выберите **класс запуска OWIN**.

1. Присвойте классу имя *запуска* и добавьте его в проект.

1. Замените код по умолчанию в классе *Startup* следующим кодом:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить** > **HTML-страницу**.

1. Назовите новый *индекс* страницы и нажмите кнопку **ОК**.

1. В **Обозреватель решений**щелкните правой кнопкой мыши СОЗДАНную HTML-страницу и выберите **задать в качестве начальной страницы**.

1. Замените код по умолчанию на странице HTML следующим кодом:

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. В **Обозреватель решений**разверните узел **сценарии**.

    Библиотеки скриптов для jQuery и SignalR отображаются в проекте.

    > [!IMPORTANT]
    > Диспетчер пакетов может установить более позднюю версию сценариев SignalR.

1. Убедитесь, что ссылки на скрипты в блоке кода соответствуют версиям файлов скриптов в проекте.

    Создать скрипт для ссылок из исходного блока кода:

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. Если они не совпадают, обновите *HTML-* файл.

1. В строке меню выберите **файл** > **сохранить все**.

## <a name="run-the-sample"></a>Запуск примера

1. На панели инструментов включите **отладку скриптов** , а затем нажмите кнопку Воспроизведение, чтобы запустить пример в режиме отладки.

    ![Введите имя пользователя](tutorial-getting-started-with-signalr/_static/image3.png)

1. Когда откроется браузер, введите имя для удостоверения разговора.

1. Скопируйте URL-адрес из браузера, откройте два других браузера и вставьте URL-адреса в адреса строки.

1. В каждом браузере введите уникальное имя.

1. Теперь добавьте комментарий и выберите **Отправить**. Повторите эти действия в других браузерах. Комментарии отображаются в режиме реального времени.

    > [!NOTE]
    > Это простое приложение разговора не поддерживает контекст обсуждения на сервере. Центр передает комментарии всем текущим пользователям. Пользователи, которые присоединяются к обсуждению позже, увидят сообщения, добавленные с момента присоединение.

    Узнайте, как работает приложение разговора в трех разных браузерах. При отправке сообщений Tom, Анандом и Ирина все браузеры обновляются в режиме реального времени:

    ![Все три браузера отображают один и тот же журнал разговора](tutorial-getting-started-with-signalr/_static/image4.png)

1. В **Обозреватель решений**просмотрите узел **документы скрипта** для работающего приложения. Существует файл скрипта *с именем* Hubs, формируемый библиотекой SignalR во время выполнения. Этот файл управляет обменом данными между скриптом jQuery и кодом на стороне сервера.

    ![автоматически сформированный скрипт концентраторов в узле "документы скриптов"](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>Изучение кода

Приложение Сигналрчат демонстрирует две основные задачи разработки SignalR. В нем показано, как создать центр. Сервер использует этот центр в качестве основного объекта координации. Концентратор использует библиотеку jQuery SignalR для отправки и получения сообщений.

### <a name="signalr-hubs-in-the-chathubcs"></a>Концентраторы SignalR в ChatHub.cs

В приведенном выше примере кода класс `ChatHub` является производным от класса `Microsoft.AspNet.SignalR.Hub`. Наследование от класса `Hub` является удобным способом создания приложения SignalR. Вы можете создать открытые методы в классе Hub, а затем использовать эти методы, вызвав их из скриптов на веб-странице.

В коде разговора клиенты вызывают метод `ChatHub.Send` для отправки нового сообщения. Затем концентратор отправляет сообщение всем клиентам, вызывая `Clients.All.broadcastMessage`.

Метод `Send` демонстрирует несколько основных понятий:

* Объявите открытые методы в концентраторе, чтобы клиенты могли их вызывать.

* Используйте динамическое свойство `Microsoft.AspNet.SignalR.Hub.Clients` для взаимодействия со всеми клиентами, подключенными к этому концентратору.

* Вызовите функцию клиента (например, функцию `broadcastMessage`) для обновления клиентов.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>SignalR и jQuery в index. HTML

На странице *index. HTML* в образце кода показано, как использовать библиотеку jQuery SignalR для взаимодействия с концентратором SignalR. Код содержит множество важных задач. Он объявляет прокси-сервер для ссылки на центр, объявляет функцию, которую сервер может вызывать для отправки содержимого клиентам, и начинает подключение для отправки сообщений в концентратор.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> В JavaScript ссылка на серверный класс и его члены должны быть camelCase. Пример кода ссылается C# на класс *часуб* в JavaScript как `chatHub`.

В этом блоке кода вы создадите функцию обратного вызова в скрипте.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

Класс концентратора на сервере вызывает эту функцию для отправки обновлений содержимого на каждый клиент. Две строки, которые кодирует содержимое в формате HTML перед отображением, являются необязательными и показывают хороший способ предотвратить внедрение скрипта.

Этот код открывает подключение к концентратору.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> Такой подход гарантирует, что код установит соединение перед выполнением обработчика событий.

Код запускает соединение, а затем передает ему функцию для управления событием щелчка на кнопке **Send** на странице HTML.

## <a name="get-the-code"></a>Получение кода

[Скачать завершенный проект](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>Дополнительные ресурсы

Дополнительные сведения о SignalR см. в следующих ресурсах:

* [Проект SignalR](http://signalr.net)

* [GitHub и примеры SignalR](https://github.com/SignalR/SignalR)

* [Вики-сайт SignalR](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы выполните следующие действия.

> [!div class="checklist"]
> * Настройка проекта
> * Запустили пример
> * Анализ кода

Перейдите к следующей статье, чтобы узнать, как использовать SignalR и MVC 5.
> [!div class="nextstepaction"]
> [SignalR 2 и MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)