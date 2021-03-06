---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: Выполнение сценариев Windows PowerShell из файлов проектов MSBuild | Документация Майкрософт
author: jrjlee
description: В этом разделе описывается, как запустить сценарий Windows PowerShell как часть процесса сборки и развертывания. Скрипт можно запустить локально (иными словами, на b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441450"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>Запуск скриптов Windows PowerShell из файлов проекта MSBuild

кто [Джейсон Иванов](https://github.com/jrjlee)

[Скачать в формате PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> В этом разделе описывается, как запустить сценарий Windows PowerShell как часть процесса сборки и развертывания. Скрипт можно запустить локально (иными словами, на сервере сборки) или удаленно, например на целевом веб-сервере или сервере базы данных.
> 
> Существует множество причин, по которым может потребоваться выполнить сценарий Windows PowerShell, выполняемый после развертывания. Например, может понадобиться:
> 
> - Добавьте в реестр пользовательский источник событий.
> - Создает каталог файловой системы для отправки.
> - Очистка каталогов сборки.
> - Запись записей в пользовательский файл журнала.
> - Отправка сообщений электронной почты, приглашающих пользователей в недавно подготовленное веб-приложение.
> - Создайте учетные записи пользователей с соответствующими разрешениями.
> - Настройте репликацию между экземплярами SQL Server.
> 
> В этом разделе показано, как запускать сценарии Windows PowerShell как локально, так и удаленно из пользовательского целевого объекта в файле проекта Microsoft Build Engine (MSBuild).

Этот раздел является частью серии руководств, основанных на требованиях Enterprise к развертыванию вымышленной компании Fabrikam, Inc. В этой серии руководств используется пример решения&#x2014; [диспетчера контактов](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;для представления веб-приложения с реалистичным уровнем сложности, включая приложение ASP.NET MVC 3, службу Windows Communication Foundation (WCF) и проект базы данных.

Метод развертывания в сердце этих учебников основан на подходе к файлам проекта Split, описанному в разделе [понимание файла проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md), в котором процесс сборки управляется двумя файлами&#x2014;проекта, содержащими инструкции по сборке, которые применяются к каждой целевой среде, и одна содержит параметры сборки и развертывания, относящиеся к конкретной среде. Во время сборки файл проекта, зависящий от среды, объединяется в файл проекта независимо от среды, чтобы сформировать полный набор инструкций по сборке.

## <a name="task-overview"></a>Обзор задач

Чтобы запустить сценарий Windows PowerShell в рамках автоматизированного или одноэтапного развертывания, необходимо выполнить следующие задачи высокого уровня:

- Добавьте сценарий Windows PowerShell в решение и в систему управления версиями.
- Создайте команду, вызывающую скрипт Windows PowerShell.
- Экранирование всех зарезервированных символов XML в команде.
- Создайте целевой объект в пользовательском файле проекта MSBuild и используйте задачу **exec** для выполнения команды.

В этом разделе будет показано, как выполнять эти процедуры. В задачах и пошаговых руководствах этого раздела предполагается, что вы уже знакомы с целями и свойствами MSBuild и знаете, как использовать пользовательский файл проекта MSBuild для создания процесса сборки и развертывания. Дополнительные сведения см. в разделе [понимание файла проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md) и [понимание процесса сборки](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

## <a name="creating-and-adding-windows-powershell-scripts"></a>Создание и добавление сценариев Windows PowerShell

В задачах этого раздела используется пример сценария Windows PowerShell с именем **логдеплой. ps1** , иллюстрирующий запуск скриптов из MSBuild. Сценарий **логдеплой. ps1** содержит простую функцию, которая записывает однострочную запись в файл журнала:

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

Сценарий **логдеплой. ps1** принимает два параметра. Первый параметр представляет полный путь к файлу журнала, в который необходимо добавить запись, а второй параметр представляет целевое место развертывания, которое необходимо записать в файл журнала. При выполнении скрипта в файл журнала добавляется строка в следующем формате:

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

Чтобы сделать скрипт **логдеплой. ps1** доступным для MSBuild, необходимо выполнить следующие действия:

- Добавьте скрипт в систему управления версиями.
- Добавьте скрипт в решение в Visual Studio 2010.

Вам не нужно развертывать скрипт вместе с содержимым решения независимо от того, планируется ли запускать сценарий на сервере сборки или на удаленном компьютере. Один из вариантов — добавить скрипт в папку решения. В примере диспетчера контактов, поскольку вы хотите использовать сценарий Windows PowerShell в рамках процесса развертывания, имеет смысл добавить скрипт в папку публикации решения.

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

Содержимое папок решений копируется на серверы сборки в качестве исходных материалов. Однако они не являются частью выходных данных проекта.

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>Выполнение скрипта Windows PowerShell на сервере сборки

В некоторых сценариях может потребоваться запустить сценарии Windows PowerShell на компьютере, который выполняет сборку проектов. Например, сценарий Windows PowerShell можно использовать для очистки папок сборки или записи в пользовательский файл журнала.

С точки зрения синтаксиса запуск скрипта Windows PowerShell из файла проекта MSBuild аналогичен запуску сценария Windows PowerShell из обычной командной строки. Необходимо вызвать исполняемый файл PowerShell. exe и использовать параметр **– Command** для предоставления команд, которые должны запускаться с помощью Windows PowerShell. (В Windows PowerShell версии 2 можно также использовать параметр **– File** ). Команда должна иметь следующий формат:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

Пример:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

Если путь к скрипту содержит пробелы, необходимо заключить путь к файлу в одинарные кавычки перед амперсандом. Нельзя использовать двойные кавычки, так как они уже используются для заключения команды:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

При вызове этой команды из MSBuild необходимо учитывать несколько дополнительных вопросов. Во-первых, следует включить флаг **– Неинтерактивный** , чтобы обеспечить беззвучное выполнение скрипта. Далее следует включить флаг **– ExecutionPolicy** с соответствующим значением аргумента. Это указывает политику выполнения, которую Windows PowerShell будет применять к сценарию, и позволяет переопределить политику выполнения по умолчанию, которая может препятствовать выполнению скрипта. Можно выбрать одно из следующих значений аргумента:

- Неограниченное значение позволяет Windows PowerShell выполнять скрипт независимо от того, подписан ли сценарий.
- Значение **RemoteSigned** позволит Windows PowerShell выполнять неподписанные сценарии, созданные на локальном компьютере. Однако скрипты, созданные в других местах, должны быть подписаны. (На практике вы вряд ли создадите сценарий Windows PowerShell локально на сервере сборки).
- Значение **AllSigned** позволит Windows PowerShell выполнять только подписанные сценарии.

Политика выполнения по умолчанию **ограничена**, что запрещает Windows PowerShell выполнять какие-либо файлы скриптов.

Наконец, необходимо экранировать все зарезервированные символы XML, которые происходят в команде Windows PowerShell:

- Замените одинарные кавычки на **&amp;apos;**
- Замените двойные кавычки на **&amp;quot;**
- Замена амперсандов на **&amp;amp;**

- При внесении этих изменений команда будет выглядеть примерно так:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

В файле пользовательского проекта MSBuild можно создать новый целевой объект и выполнить следующую команду с помощью задачи **exec** :

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

В этом примере обратите внимание на следующее:

- Любые переменные, такие как значения параметров и расположение исполняемого файла Windows PowerShell, объявляются как свойства MSBuild.
- Условия включены, чтобы разрешить пользователям переопределять эти значения из командной строки.
- Свойство **мсдеплойкомпутернаме** объявлено в любом расположении файла проекта.

При выполнении этого целевого объекта в рамках процесса сборки Windows PowerShell выполнит команду и запишет запись журнала в указанный файл.

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>Выполнение сценария Windows PowerShell на удаленном компьютере

Windows PowerShell может выполнять сценарии на удаленных компьютерах с помощью [Служба удаленного управления Windows](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM). Для этого необходимо использовать командлет [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) . Это позволяет выполнить сценарий на одном или нескольких удаленных компьютерах без копирования сценария на удаленные компьютеры. Все результаты возвращаются на локальный компьютер, с которого был выполнен сценарий.

> [!NOTE]
> Перед использованием командлета **Invoke-Command** для выполнения сценариев Windows PowerShell на удаленном компьютере необходимо настроить прослушиватель WinRM для приема удаленных сообщений. Это можно сделать, выполнив команду **winrm quickconfig** на удаленном компьютере. Дополнительные сведения см. в разделе [Установка и настройка для служба удаленного управления Windows](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).

В окне Windows PowerShell этот синтаксис используется для запуска сценария **логдеплой. ps1** на удаленном компьютере:

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> Существует несколько других способов использования **командлета Invoke-Command** для запуска файла скрипта, но этот подход является наиболее простым, если необходимо указать значения параметров и управлять путями с пробелами.

При запуске из командной строки необходимо вызвать исполняемый файл Windows PowerShell и использовать параметр **– Command** для указания инструкций:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

Как и ранее, при выполнении команды из MSBuild необходимо указать некоторые дополнительные параметры и экранировать все зарезервированные символы XML:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

Наконец, как и раньше, можно использовать задачу **exec** в настраиваемом целевом объекте MSBuild для выполнения команды:

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

При выполнении этого целевого объекта в рамках процесса сборки Windows PowerShell запустит сценарий на компьютере, указанном в аргументе **– ComputerName** .

## <a name="conclusion"></a>Заключение

В этом разделе описано, как запустить сценарий Windows PowerShell из файла проекта MSBuild. Этот подход можно использовать для запуска сценария Windows PowerShell либо локально, либо на удаленном компьютере в рамках автоматизированного или одноэтапного процесса сборки и развертывания.

## <a name="further-reading"></a>Дополнительные материалы

Рекомендации по подписыванию сценариев Windows PowerShell и управлению политиками выполнения см. в разделе [выполнение сценариев Windows PowerShell](https://technet.microsoft.com/library/ee176949.aspx). Рекомендации по запуску команд Windows PowerShell с удаленного компьютера см. в разделе [выполнение удаленных команд](https://technet.microsoft.com/library/dd819505.aspx).

Дополнительные сведения об использовании пользовательских файлов проекта MSBuild для управления процессом развертывания см. в разделе [Основные сведения о файле проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md) и [понимании процесса сборки](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

> [!div class="step-by-step"]
> [Назад](taking-web-applications-offline-with-web-deploy.md)
> [Вперед](troubleshooting-the-packaging-process.md)
