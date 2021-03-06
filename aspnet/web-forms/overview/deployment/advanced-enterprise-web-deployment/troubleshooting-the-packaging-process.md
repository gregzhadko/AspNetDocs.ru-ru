---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: Устранение неполадок процесса упаковки | Документация Майкрософт
author: jrjlee
description: В этом разделе описывается, как можно получить подробные сведения о процессе упаковки с помощью свойства Енаблепаккажепроцесслоггингандассерт в M...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509754"
---
# <a name="troubleshooting-the-packaging-process"></a>Устранение неполадок в процессе упаковки

кто [Джейсон Иванов](https://github.com/jrjlee)

[Скачать в формате PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> В этом разделе описывается, как можно собираются подробные сведения о процессе упаковки с помощью свойства **енаблепаккажепроцесслоггингандассерт** в Microsoft Build Engine (MSBuild).
> 
> Если для свойства **енаблепаккажепроцесслоггингандассерт** задано **значение true**, MSBuild будет выполнять следующие действия:
> 
> - Добавьте дополнительные сведения о процессе упаковки в журналы сборки.
> - Регистрация ошибок при определенных условиях, например, если в списке упаковки найдены дублирующиеся файлы.
> - Создайте каталог журнала в папке пакета *имяпроекта*\_и используйте его для записи сведений о файлах, которые вы собираетесь упаковать.
> 
> Если в процессе упаковки произошел сбой или пакеты веб-развертывания не содержат нужных файлов, эти сведения можно использовать для устранения неполадок, а также определить, где происходит проблема.
> 
> > [!NOTE]
> > Свойство **енаблепаккажепроцесслоггингандассерт** работает только при сборке проекта с помощью конфигурации **отладки** . Свойство не учитывается в других конфигурациях.

Этот раздел является частью серии руководств, основанных на требованиях Enterprise к развертыванию вымышленной компании Fabrikam, Inc. В этой серии руководств используется пример решения&#x2014; [диспетчера контактов](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;для представления веб-приложения с реалистичным уровнем сложности, включая приложение ASP.NET MVC 3, службу Windows Communication Foundation (WCF) и проект базы данных.

Метод развертывания в сердце этих учебников основан на подходе к файлам проекта Split, описанному в разделе [понимание файла проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md), в котором процесс сборки управляется двумя файлами&#x2014;проекта, содержащими инструкции по сборке, которые применяются к каждой целевой среде, и одна содержит параметры сборки и развертывания, относящиеся к конкретной среде. Во время сборки файл проекта, зависящий от среды, объединяется в файл проекта независимо от среды, чтобы сформировать полный набор инструкций по сборке.

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>Основные сведения о свойстве Енаблепаккажепроцесслоггингандассерт

[Сборка и упаковка проектов веб-приложений](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) описывает, как конвейер веб-публикаций (WPP) предоставляет набор целевых объектов MSBuild, расширяющих функциональные возможности MSBuild и позволяющий его интегрировать с помощью средства веб-развертывания службы IIS (IIS) (веб-развертывание). При упаковке проекта веб-приложения вы вызываете цели WPP.

Многие из этих целевых объектов WPP включают условную логику, которая регистрирует дополнительные сведения, если свойство **енаблепаккажепроцесслоггингандассерт** имеет значение **true**. Например, если просмотреть целевой объект **пакета** , можно увидеть, что он создает дополнительный каталог журналов и записывает список файлов в текстовый файл, если **енаблепаккажепроцесслоггингандассерт** равен **true**.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> Цели WPP определены в файле *Microsoft. Web. Publishing. targets* в папке% ProgramFiles (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web. Вы можете открыть этот файл и проверить целевые объекты в Visual Studio 2010 или любом редакторе XML. Следите за тем, чтобы не изменять содержимое файла.

## <a name="enabling-the-additional-logging"></a>Включение дополнительного ведения журнала

Значение для свойства **енаблепаккажепроцесслоггингандассерт** можно указать различными способами в зависимости от способа построения проекта.

При построении проекта из командной строки можно указать значение свойства **енаблепаккажепроцесслоггингандассерт** в качестве аргумента командной строки:

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

Если вы используете пользовательский файл проекта для построения проектов, можно включить значение **енаблепаккажепроцесслоггингандассерт** в атрибут **Properties** задачи **MSBuild** :

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

Если вы используете определение сборки Team Foundation Server (TFS) для построения проектов, вы можете указать значение для свойства **енаблепаккажепроцесслоггингандассерт** в строке **аргументов MSBuild** :![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> Дополнительные сведения о создании и настройке определений сборки см. в разделе [Создание определения сборки, поддерживающего развертывание](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).

Кроме того, если необходимо включить пакет в каждую сборку, можно изменить файл проекта для проекта веб-приложения, чтобы установить для свойства **енаблепаккажепроцесслоггингандассерт** значение **true**. Необходимо добавить свойство к первому элементу **PropertyGroup** в файле. csproj или. vbproj.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>Просмотр файлов журнала

При сборке и упаковке проекта веб-приложения с параметром **енаблепаккажепроцесслоггингандассерт** , для которого задано **значение true**, MSBuild создает дополнительную папку с именем log в папке пакета *имяПроекта*\_. Папка журнала содержит различные файлы:

![](troubleshooting-the-packaging-process/_static/image2.png)

Список отображаемых файлов зависит от того, что в проекте и в процессе сборки. Однако эти файлы обычно используются для записи списка файлов, собираемых в КОНВЕЙЕРе для упаковки, на различных этапах процесса:

- В файле *приксклудепипелинеколлектфилесфасефилелист. txt* перечислены файлы, которые MSBuild собирает для упаковки, прежде чем будут удалены все файлы, указанные для исключения.
- Файл *афтерексклудефилесфилеслист. txt* содержит измененный список файлов после удаления всех файлов, указанных для исключения.

    > [!NOTE]
    > Дополнительные сведения об исключении файлов и папок из процесса упаковки см. в разделе [исключение файлов и папок из развертывания](excluding-files-and-folders-from-deployment.md).
- Файл *афтертрансформвебконфиг. txt* содержит список файлов, собранных для упаковки после выполнения всех преобразований *Web. config* . В этом списке все файлы преобразования *Web. config* для конкретной конфигурации, такие как *Web. Debug. config* и *Web. Release. config*, исключаются из списка файлов для упаковки. В свое место включается один преобразованный *файл Web. config* .
- Файл *постаутопараметеризатионвебконфигконнектионстрингс. txt* содержит список файлов после параметризации строк подключения в файле *Web. config* . Это процесс, который позволяет заменить строки подключения правильными параметрами целевой среды при развертывании пакета.
- Файл предварительной версии *. txt* содержит окончательный список файлов, предваряющих сборку, которые будут включены в пакет.

> [!NOTE]
> Имена дополнительных файлов журналов обычно соответствуют целевым объектам WPP. Эти целевые объекты можно проверить, изучив файл *Microsoft. Web. Publishing. targets* в папке% ProgramFiles (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web.

Если содержимое веб-пакета не соответствует ожидаемому, просмотр этих файлов может оказаться полезным способом определить, в какой точке процесса произошла ошибка.

## <a name="conclusion"></a>Заключение

В этом разделе описано, как можно использовать свойство **енаблепаккажепроцесслоггингандассерт** в MSBuild для устранения неполадок в процессе упаковки. В нем объясняются различные способы предоставления значения свойства процессу сборки и описаны дополнительные сведения, которые записываются при установке свойства в **значение true**.

## <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения об использовании пользовательских файлов проекта MSBuild для управления процессом развертывания см. в разделе [Основные сведения о файле проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md) и [понимании процесса сборки](../web-deployment-in-the-enterprise/understanding-the-build-process.md). Дополнительные сведения о конвейере WPP и управлении процессом упаковки см. в разделе [Создание и упаковка проектов веб-приложений](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md). Инструкции по исключению конкретных файлов и папок из пакетов веб-развертывания см. в разделе [исключение файлов и папок из развертывания](excluding-files-and-folders-from-deployment.md).

> [!div class="step-by-step"]
> [Назад](running-windows-powershell-scripts-from-msbuild-project-files.md)
