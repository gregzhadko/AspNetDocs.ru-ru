---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: Введение веб-страницы ASP.NET публикации сайта с помощью WebMatrix | Документация Майкрософт
author: Rick-Anderson
description: Это руководство является окончательным выпуском в наборе руководств, в котором представлены веб-страницы ASP.NET и Microsoft WebMatrix. В нем обсуждается Публикация сайта t...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240584"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>Введение веб-страницы ASP.NET публикации сайта с помощью WebMatrix

; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)

> Это руководство является окончательным выпуском в наборе руководств, в котором представлены веб-страницы ASP.NET и Microsoft WebMatrix. В нем обсуждается Публикация сайта в Интернете, чтобы другие пользователи могли работать с ним. Предполагается, что вы выполнили серию, [создав единообразный вид для веб-страницы ASP.NET сайтов](https://go.microsoft.com/fwlink/?LinkId=251585).
> 
> Вы узнаете, как опубликовать сайт с помощью:
> 
> - Microsoft Azure.
> - Организация веб-хостинга

## <a name="about-publishing-your-site"></a>Сведения о публикации сайта

До этого момента вы выполнили всю работу на локальном компьютере, включая тестирование страниц. Для запуска страниц<em>. cshtml</em> вы использовали веб-сервер, встроенный в WebMatrix, а именно IIS Express. Но, конечно, никто не сможет увидеть созданный вами сайт, за исключением вас. Чтобы разрешить другим пользователям работать с сайтом, его необходимо опубликовать в Интернете.

Если у вас уже нет доступа к общедоступному веб-серверу, публикация означает, что у вас должна быть учетная запись с *облачной платформой* или *поставщиком услуг размещения*. Облачная платформа, например Microsoft Azure, предоставляет инфраструктуру по запросу для приложений. Поставщик услуг размещения — это компания, которая владеет общедоступными веб-серверами и будет сдавать место для вашего сайта. Планы размещения выполняются через несколько долларов в месяц (или даже бесплатно) для небольших сайтов на множество сотен долларов в месяц для высокопроизводительных коммерческих веб-сайтов.

> [!NOTE]
> У вас может быть доступ к общедоступному веб-серверу через поставщика услуг Интернета (ISP), который используется для получения домашней службы Интернета. Однако поставщик услуг размещения должен поддерживать веб-страницы ASP.NET. Многие поставщики услуг Интернета не имеют, но всегда стоит проверять.

В этом учебнике мы предоставим обзор публикации. Нецелесообразно предоставлять точные сведения обо всем, так как процесс для каждого поставщика услуг размещения немного различается. Но вы получите хорошее представление о том, как работает этот процесс.

Этот учебник содержит четыре раздела:

1. [Настройка страницы по умолчанию](#defaultpage)
2. Публикация (выберите один из следующих элементов)  
 а. [Публикация сайта в Microsoft Azure](#azure)  
 b. [Публикация веб-узла в компании для размещения в Интернете](#host)
3. [Обновление действующего сайта: Повторная публикация](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>Настройка страницы по умолчанию

Когда пользователь переходит по базовому адресу веб-сайта, пользователю отображается страница по умолчанию для сайта. Например, если *Default.htm* установлен в качестве страницы по умолчанию для сайта в `www.contoso.com` , то переход к будет `www.contoso.com` таким же, как и при переходе к `www.contoso.com/Default.htm` .

В настоящее время ваш сайт использует **Default. cshtml** в качестве страницы по умолчанию. Эта страница подходит для страницы по умолчанию, но в этом учебнике вы не добавили содержимое на эту страницу, чтобы отображалась пустая страница. Откройте Default. cshtml и замените содержимое следующим кодом.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

Теперь ваш сайт готов к публикации. Во-первых, вы узнаете, как развернуть сайт в Azure, а затем развернуть его в компании для размещения в Интернете. Любой из вариантов подходит для вашего веб-сайта, и вам нужно только один из вариантов развертывания.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Публикация сайта в Microsoft Azure

В этом учебнике сначала будет показано, как развернуть сайт на Microsoft Azure. Войдя с помощью учетная запись Майкрософт, вы можете создать до 10 бесплатных сайтов в Azure. Эти бесплатные сайты предоставляют удобный способ тестирования сайтов. Вы всегда можете удалить этот пример сайта позже, чтобы не использовать все бесплатные сайты. Вы можете создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/dotnet/).

На ленте WebMatrix нажмите кнопку **опубликовать** .

![Кнопка "опубликовать" на ленте WebMatrix](publishing/_static/image1.png)

Откроется диалоговое окно **Публикация сайта** . Если вы не вошли в учетная запись Майкрософт, в диалоговом окне будет содержаться ссылка начало **работы с Azure** . Щелкните эту ссылку.

![Публикация сайта](publishing/_static/image2.png)

Если вы не вошли в учетная запись Майкрософт, вам снова присвоена возможность войти в систему. Для публикации сайта в Azure необходимо войти в учетная запись Майкрософт.

![войти](publishing/_static/image3.png)

После входа в учетная запись Майкрософт диалоговое окно содержит ссылки для создания нового сайта в Azure или подключения к одному из существующих сайтов в Azure.

![Создать новый сайт](publishing/_static/image4.png)

Выберите **создать новый сайт**.

Если вы назвали проект **вебпажесмовиес**, имя сайта по умолчанию будет **webpagesmovies.azurewebsites.NET**. Это имя по умолчанию, скорее всего, недоступно, как показано красным восклицательным знаком.

![имя веб-сайта по умолчанию](publishing/_static/image5.png)

Измените имя сайта на доступное, а затем выберите расположение, близкое к Вашему расположению.

![измененное имя сайта](publishing/_static/image6.png)

Нажмите кнопку **ОК**.

WebMatrix выполняет проверку, чтобы определить, совместим ли сервер с вашим сайтом.

![тест совместимости](publishing/_static/image7.png)

Выберите **Continue** (Продолжить).

Отобразятся результаты теста совместимости.

![результат совместимости](publishing/_static/image8.png)

Выберите **Continue** (Продолжить).

WebMatrix отображает файлы и базы данных, которые будут опубликованы на сайте. Так как это первая публикация сайта, отображаются все файлы. Вы можете снять флажок с файла, который не готов к публикации. В последующих публикациях будут отображены только измененные файлы. См. статью [обновление действующего сайта: Повторная публикация](#update).

![Просмотр публикации](publishing/_static/image9.png)

Выберите **Continue** (Продолжить).

После развертывания сайта в Azure появится сообщение, указывающее, что развертывание завершено.

![Публикация завершена](publishing/_static/image10.png)

Ваш сайт и база данных опубликованы в Azure и теперь доступны для общего доступа. Щелкните ссылку в сообщении о завершении публикации, и вы увидите развернутый сайт. Вы или любой пользователь с доступом к Интернету может добавлять или изменять записи в базе данных.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>Публикация веб-узла в компании для размещения в Интернете

Если вы решили не публиковать в Azure, вы можете опубликовать свой сайт в компании для размещения в Интернете.

Щелкните ссылку **найти веб-** узел.

![Кнопка "найти веб-размещение" в диалоговом окне "Параметры публикации"](publishing/_static/image12.png)

Перейдите на страницу сайта Майкрософт со списком поставщиков услуг размещения, поддерживающих ASP.NET.

![Страница на сайте Майкрософт со списком поставщиков услуг размещения](publishing/_static/image13.png)

Очевидно, что теперь может быть трудно знать, какие именно функции размещения могут потребоваться в долгосрочной перспективе. Вот несколько моментов, которые следует учитывать:

- В целях сайта Вебпажесмовиес вам не нужно иметь отдельную надстройку для SQL Server, которая часто избавляет от затрат. На вашем сайте вы используете SQL Server Compact Edition, который является автономным. Однако для некоторых будущих рабочих веб-сайтов может потребоваться SQL Server доступ. Если вы считаете, что можете добавить SQL Server возможность позже.
- Проверьте, поддерживает ли поставщик услуг размещения Протокол публикации веб-развертывание. Можно выполнить публикацию с помощью протокола FTP, но удобнее использовать веб-развертывание.

Некоторые сайты предлагают бесплатный пробный период. Бесплатная пробная версия — хороший способ попробовать публикацию и размещение, пока вы все еще поэкспериментируем с WebMatrix и веб-страницы ASP.NET.

Выберите нужный. В рамках этого руководства мы выбрали DiscountASP.NET, так как во время создания учебника эта компания имела специальное предложение, которое позволит пользователям размещать сайт бесплатно в течение нескольких месяцев.

> [!NOTE]
> Наш вариант поставщика услуг размещения для этого учебника не должен интерпретироваться как одобрение этой компании. Но нам пришлось бы выбрать один из них для иллюстрации, а DiscountASP.NET — одна из многих компаний, которые поддерживают веб-страницы ASP.NET и веб-развертывание протокол для публикации.

Как правило, после регистрации в поставщике услуг хостинга компания отправляет вам сообщение электронной почты с именем пользователя и паролем, URL-адресом веб – сервера и т. д. Если компания размещения поддерживает протокол веб-развертывание, они могут отправить вам файл, содержащий параметры публикации, или загрузить его. Файл параметров публикации упрощает процесс.

После регистрации и готовности к публикации нажмите кнопку **опубликовать** на ленте WebMatrix. Откроется диалоговое окно « **Параметры публикации** ».

Если поставщик услуг размещения отправил вам файл параметров публикации, щелкните ссылку **Импорт параметров публикации** и импортируйте файл. Если у вас нет файла параметров публикации, заполните поля, используя значения, которые компания размещения послала вам по электронной почте. Вот как может выглядеть диалоговое окно **Параметры публикации** после завершения работы:

![Параметры публикации, заданные в диалоговом окне «Параметры публикации»](publishing/_static/image14.png)

Щелкните **проверить подключение**. Если все правильно, диалоговое окно сообщает об **успешном соединении**, что означает, что он может взаимодействовать с сервером поставщика услуг размещения.

![Сообщение об успешном выполнении, если параметры публикации верны](publishing/_static/image15.png)

Если возникла проблема, WebMatrix поможет узнать, что именно из себя представляет проблема:

![Сообщение об ошибке при наличии проблем с параметрами публикации](publishing/_static/image16.png)

Нажмите кнопку **Save** (Сохранить), чтобы сохранить настройки. WebMatrix предлагает выполнить тест, чтобы убедиться, что он может правильно взаимодействовать с сайтом размещения.

![Предложение сообщения для выполнения тестирования процесса публикации](publishing/_static/image17.png)

Нажмите кнопку **Да**. WebMatrix передает некоторые примеры файлов поставщику услуг размещения. По завершении теста совместимости WebMatrix сообщает о результатах:

![Результаты теста публикации](publishing/_static/image18.png)

Если вы готовы приступить к работе, нажмите кнопку **продолжить** , чтобы начать процесс публикации в реальном времени. WebMatrix определяет, какие файлы находятся на вашем сайте и уже находятся на основном сервере (нет) и предоставляет предварительную версию процесса публикации:

![Предварительный просмотр файлов, которые будут отправлены процессом публикации](publishing/_static/image19.png)

Список публикуемых файлов включает веб-страницы, которые вы создали как *movies. cshtml*. Список также содержит файлы для вспомогательных служб, которые вы установили, файлы для запуска SQL Server Compact выпуска для базы данных и т. д. В результате первоначальный процесс публикации может быть значительным.

Нажмите кнопку **Continue**(Продолжить). WebMatrix копирует файлы на сервер поставщика услуг размещения. По завершении в строке состояния будут выведены результаты:

![Сообщение в строке состояния после успешного завершения процесса публикации](publishing/_static/image20.png)

Чтобы просмотреть активный сайт, щелкните ссылку в строке состояния. Добавьте в URL-адрес *фильмы* , и вы увидите созданный файл *movies. cshtml* :

![Активный сайт с изображением страницы "фильмы"](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>Обновление действующего сайта: Повторная публикация

После публикации сайта (в Azure или компании для размещения веб-узлов) на компьютере будут установлены две копии &mdash; этой версии и версия поставщика услуг. Вы, вероятно, захотите продолжить разработку сайта (если это не так, как часть следующего набора руководств). В этом случае необходимо повторно опубликовать сайт, чтобы скопировать изменения с компьютера в поставщика услуг. Процесс публикации в WebMatrix может определить, какие файлы были изменены на сайте, и опубликовать только эти файлы.

Чтобы увидеть, как работает повторная публикация, откройте сайт *movies. cshtml* , внесите небольшое изменение, а затем сохраните файл. Например, измените заголовок на `Movies - Updated` .

Нажмите кнопку **опубликовать** на ленте. WebMatrix определяет, что изменилось, и отображает Предварительный просмотр файлов, которые он будет публиковать.

![Диалоговое окно "публикация", в котором отображаются измененные файлы, готовые к повторной публикации](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> По умолчанию WebMatrix публикует вашу базу данных (*SDF* -файл) только при первой публикации сайта. После публикации сайта и взаимодействия пользователей с веб-сайтом база данных на активном сайте обычно содержит реальные данные сайта. Необходимо быть очень осторожным, чтобы не перезаписать динамическую базу данных с *SDF* -файлом на вашем компьютере, который обычно содержит только тестовые данные. Вот почему вы видите, что при **публикации предупреждений все удаленные базы данных будут перезаписаны**, и почему флажок для *вебпажесмовиес. sdf* по умолчанию снят.

Нажмите кнопку **Continue**(Продолжить). WebMatrix публикует измененные файлы и отображает сообщение об успешном выполнении, как при первой публикации.

Перейдите на активный сайт (можно щелкнуть ссылку в сообщении об успешном выполнении, если она все еще отображается) и убедиться, что изменения опубликованы.

> [!TIP] 
> 
> **Удаленное изменение файлов**
> 
> В качестве альтернативы изменению сайта и последующей повторной публикации можно изменить удаленные файлы непосредственно в WebMatrix. В этом сценарии вы откроете файл, который является поставщиком службы, а WebMatrix загрузит его копию для изменения. Каждый раз при сохранении файла WebMatrix отправляет изменения на сайт.
> 
> Удаленное редактирование — это простой способ внесения изменений в активный сайт. Однако изменения, вносимые таким способом, не синхронизируются с файлами на локальном сайте. Чтобы синхронизировать локальные файлы с удаленным сайтом, можно скачать удаленные файлы. Этот процесс работает во многом подобно публикации, за исключением обратных.
> 
> Мы не будем описывать дополнительные возможности удаленного редактирования и удаленной загрузки WebMatrix здесь. Они весьма полезны, если несколько пользователей должны работать на одном и том же сайте на разных компьютерах. Дополнительные сведения см. в статье [Публикация и изменение удаленного сайта с помощью бета-версии WebMatrix 2](https://go.microsoft.com/fwlink/?LinkId=251591).

## <a name="additional-resources"></a>Дополнительные ресурсы

- [ASP.NET WebMatrix веб-страницы ASP.NET Forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)— отличное место для размещения вопросов и получения ответов.

> [!div class="step-by-step"]
> [Назад](layouts.md)
