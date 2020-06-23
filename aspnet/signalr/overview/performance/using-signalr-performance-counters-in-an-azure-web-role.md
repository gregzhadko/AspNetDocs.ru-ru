---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Использование счетчиков производительности SignalR в веб-роли Azure | Документация Майкрософт
author: guardrex
description: Установка и использование счетчиков производительности SignalR в веб-роли Azure.
keywords: ASP. NET, SignalR, счетчик производительности, веб-роль Azure
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240636"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Использование счетчиков производительности SignalR в веб-роли Azure

Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Счетчики производительности SignalR используются для мониторинга производительности приложения в веб-роли Azure. Счетчики фиксируются система диагностики Microsoft Azure. Вы устанавливаете счетчики производительности SignalR в Azure, используя *signalr.exe*, то же средство, которое используется для автономных или локальных приложений. Так как роли Azure являются временными, вы настраиваете приложение для установки и регистрации счетчиков производительности SignalR при запуске.

## <a name="prerequisites"></a>Предварительные требования

* Visual Studio 2015 или [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [Microsoft Azure SDK для Visual Studio](https://azure.microsoft.com/downloads/) **Примечание. Перезагрузите компьютер после установки пакета SDK.**
* Подписка Microsoft Azure. чтобы зарегистрироваться для получения бесплатной пробной учетной записи Azure, см. статью [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/dotnet/).

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>Создание приложения веб-роли Azure, предоставляющего счетчики производительности SignalR

1. Запустите Visual Studio.

2. В Visual Studio выберите **Файл** > **Создать** > **Проект**.

3. В диалоговом окне **Новый проект** выберите категорию облако **Visual C#**  >  **Cloud** слева, а затем выберите шаблон **облачная служба Azure** . Присвойте приложению имя **сигналрперфкаунтерс** и нажмите кнопку **ОК**.

   ![Новое облачное приложение](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > Если вы не видите категорию шаблон **облака** или шаблон **облачной службы Azure** , необходимо установить рабочую нагрузку **разработки Azure** для Visual Studio 2017. Щелкните ссылку **открыть Visual Studio Installer** в нижней левой части диалогового окна **Новый проект** , чтобы открыть Visual Studio Installer. Выберите рабочую нагрузку **Разработка Azure** и нажмите кнопку **изменить** , чтобы начать установку рабочей нагрузки.
   >
   > ![Рабочая нагрузка разработки Azure в Visual Studio Installer](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. В диалоговом окне **создание Microsoft Azure облачной службы** выберите **веб-роль ASP.NET** и нажмите кнопку >, чтобы добавить роль в проект. Щелкните **ОК**.

   ![Добавить веб-роль ASP.NET](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. В диалоговом окне **Создание веб-приложения ASP.NET — WebRole1** выберите шаблон **MVC** и нажмите кнопку **ОК**.

   ![Добавление MVC и веб-API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. В **Обозреватель решений**откройте файл *Diagnostics. Wadcfgx* в разделе **WebRole1**.

   ![Обозреватель решений Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. Замените содержимое файла следующей конфигурацией и сохраните файл:

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. Откройте **консоль диспетчера пакетов** из **меню Инструменты**  >  **Диспетчер пакетов NuGet**. Введите следующие команды для установки последней версии SignalR и пакета служебных программ SignalR:

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. Настройте приложение для установки счетчиков производительности SignalR в экземпляр роли при запуске или перезапуске. В **Обозреватель решений**щелкните правой кнопкой мыши проект **WebRole1** и выберите команду **добавить**  >  **новую папку**. Назовите новую папку *Startup*.

   ![Добавить папку автозагрузки](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. Скопируйте файл *signalr.exe* (добавленный с пакетом **Microsoft. AspNet. SignalR. utils** ) из \<project folder> /сигналрперфкаунтерс/паккажес/Микрософт.АСПнет.сигналр.утилс. \<version> /тулс в папку *Startup* , созданную на предыдущем шаге.

11. В **Обозреватель решений**щелкните правой кнопкой мыши папку *Startup* и выберите команду **добавить**  >  **существующий элемент**. В появившемся диалоговом окне выберите *signalr.exe* и нажмите кнопку **Добавить**.

    ![Добавление signalr.exe в проект](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. Щелкните правой кнопкой мыши созданную папку *автозагрузки* . Выберите **Добавить**  >  **новый элемент**. Выберите узел **Общие** , выберите **текстовый файл**и назовите новый элемент *сигналрперфкаунтеринсталл. cmd*. Этот командный файл установит счетчики производительности SignalR в веб-роль.

    ![Создать пакетный файл установки счетчика производительности SignalR](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Когда Visual Studio создаст файл *сигналрперфкаунтеринсталл. cmd* , он будет автоматически открыт в главном окне. Замените содержимое файла следующим скриптом, а затем сохраните и закройте файл. Этот скрипт выполняет *signalr.exe*, который добавляет счетчики производительности SignalR в экземпляр роли.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. Выберите файл *signalr.exe* в **Обозреватель решений**. В **свойствах**файла задайте для параметра **Копировать в выходной каталог** значение **всегда копировать**.

    ![Установите для параметра Копировать в выходной каталог значение всегда копировать.](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. Повторите предыдущий шаг для файла *сигналрперфкаунтеринсталл. cmd* .

16. Щелкните правой кнопкой мыши файл *сигналрперфкаунтеринсталл. cmd* и выберите команду **Открыть с помощью**. В появившемся диалоговом окне выберите **двоичный редактор** и нажмите кнопку **ОК**.

    ![Открыть с помощью двоичного редактора](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. В двоичном редакторе выберите все начальные байты в файле и удалите их. Сохраните файл и закройте его.

    ![Удалить начальные байты](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. Откройте *ServiceDefinition. csdef* и добавьте задачу запуска, которая выполняет файл *сигналрперфкаунтеринсталл. cmd* при запуске службы:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. Откройте `Views/Shared/_Layout.cshtml` и удалите скрипт пакета jQuery из конца файла.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. Добавьте клиент JavaScript, который постоянно вызывает `increment` метод на сервере. Откройте `Views/Home/Index.cshtml` и замените содержимое следующим кодом:

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. Создайте новую папку в проекте **WebRole1** *с именем*Hubs. Щелкните правой кнопкой мыши папку *концентраторы* в **Обозреватель решений** и выберите команду **добавить**  >  **новый элемент**. В диалоговом окне **Добавление нового элемента** выберите категорию **веб-**  >  **SignalR** и выберите шаблон элемента **класс концентратора SignalR (v2)** . Присвойте новому концентратору имя *MyHub.CS* и выберите **Добавить**.

    ![Добавление класса концентратора SignalR в папку "концентраторы" в диалоговом окне "Добавление нового элемента"](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.CS* будет автоматически открываться в главном окне. Замените содержимое следующим кодом, а затем сохраните и закройте файл:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* — это средство тестирования плотности подключений, предоставляемое с базой кода SignalR. Так как для погромче требуется постоянное подключение, вы добавляете его на сайт для использования при тестировании. Добавьте новую папку в проект **WebRole1** с именем *персистентконнектионс*. Щелкните правой кнопкой мыши эту папку и выберите команду **Добавить**  >  **класс**. Назовите новый файл класса *MyPersistentConnections.CS* и выберите **Добавить**.

24. Visual Studio откроет файл *MyPersistentConnections.CS* в главном окне. Замените содержимое следующим кодом, а затем сохраните и закройте файл:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. С помощью `Startup` класса объекты SignalR запускаются при запуске OWIN. Откройте или создайте *Startup.CS* и замените содержимое следующим кодом:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    В приведенном выше коде `OwinStartup` атрибут помечает этот класс для запуска OWIN. `Configuration`Метод запускает SignalR.

26. Протестируйте приложение в эмулятор Microsoft Azure, нажав клавишу **F5**.

    > [!NOTE]
    > Если вы столкнулись с **FileLoadException** по адресу **мапсигналр**, измените перенаправления привязки в *web.config* следующим образом:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. Подождите примерно одну минуту. Откройте окно инструментов Cloud Explorer в Visual Studio (**View**  >  **Cloud Explorer**) и разверните путь `(Local)/Storage Accounts/(Development)/Tables` . Дважды щелкните **WADPerformanceCountersTable**. Счетчики SignalR должны отображаться в табличных данных. Если таблица не отображается, может потребоваться повторно ввести учетные данные службы хранилища Azure. Может потребоваться нажать кнопку **Обновить** , чтобы просмотреть таблицу в **Cloud Explorer** или нажать кнопку **Обновить** в окне Открытие таблицы, чтобы просмотреть данные в таблице.

    ![Выбор таблицы счетчиков производительности WAD в Visual Studio Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![Отображение счетчиков, собранных в таблице счетчиков производительности WAD](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. Чтобы протестировать приложение в облаке, обновите файл **ServiceConfiguration. Cloud. cscfg** и задайте `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` для него допустимую строку подключения к учетной записи хранения Azure.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. Разверните приложение в подписке Azure. Дополнительные сведения о развертывании приложения в Azure см. в статье [Создание и развертывание облачной службы](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).

30. Подождите несколько минут. В **Cloud Explorer**найдите учетную запись хранения, настроенную выше, и найдите `WADPerformanceCountersTable` в ней таблицу. Счетчики SignalR должны отображаться в табличных данных. Если таблица не отображается, может потребоваться повторно ввести учетные данные службы хранилища Azure. Может потребоваться нажать кнопку **Обновить** , чтобы просмотреть таблицу в **Cloud Explorer** или нажать кнопку **Обновить** в окне Открытие таблицы, чтобы просмотреть данные в таблице.

Для первоначального содержимого, используемого в этом учебнике, особое внимание [соследуется](https://social.msdn.microsoft.com/profile/Martin+Richard) спасибо.
