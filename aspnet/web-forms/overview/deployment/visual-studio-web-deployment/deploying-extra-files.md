---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'ASP.NET веб-развертывание с помощью Visual Studio: развертывание дополнительных файлов | Документация Майкрософт'
author: tdykstra
description: В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика, Усин...
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441366"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>Веб-развертывание ASP.NET с помощью Visual Studio: развертывание дополнительных файлов

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> В этой серии руководств показано, как развернуть (опубликовать) веб-приложение ASP.NET в веб-приложениях службы приложений Azure или поставщике услуг размещения стороннего поставщика с помощью Visual Studio 2012 или Visual Studio 2010. Сведения о ряде см. в [первом руководстве по ряду](introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве показано, как расширить конвейер веб-публикаций Visual Studio для выполнения дополнительной задачи во время развертывания. Задача заключается в копировании дополнительных файлов, которые отсутствуют в папке проекта, на целевой веб-сайт.

В этом учебнике будет скопирован один дополнительный файл: *robots. txt*. Вы хотите развернуть этот файл в промежуточном развертывании, но не в рабочей среде. В руководстве [развертывание в производство](deploying-to-production.md) вы добавили этот файл в проект и настроили профиль рабочей публикации, чтобы исключить его. В этом учебнике вы увидите альтернативный метод для решения этой ситуации, который будет полезен для любых файлов, которые требуется развернуть, но не нужно включать в проект.

## <a name="move-the-robotstxt-file"></a>Перемещение файла robots. txt

Чтобы подготовиться к другому методу обработки *robots. txt*, в этом разделе руководства вы перемещаете файл в папку, которая не включена в проект, и удаляет *robots. txt* из промежуточной среды. Необходимо удалить файл из промежуточной среды, чтобы можно было убедиться, что новый метод развертывания файла в этой среде работает правильно.

1. В **Обозреватель решений**щелкните правой кнопкой мыши файл *robots. txt* и выберите пункт **исключить из проекта**.
2. С помощью проводника Windows создайте новую папку в папке решения и назовите ее *екстрафилес*.
3. Переместите файл *robots. txt* из папки проекта *ContosoUniversity* в папку *екстрафилес* .

    ![Папка Екстрафилес](deploying-extra-files/_static/image1.png)
4. С помощью средства FTP удалите файл *robots. txt* с промежуточного веб-сайта.

    В качестве альтернативы можно выбрать пункт **удалить дополнительные файлы в месте назначения** в разделе **Параметры публикации файла** на вкладке **Параметры** профиля промежуточной публикации и повторно опубликовать в промежуточном режиме.

## <a name="update-the-publish-profile-file"></a>Обновление файла профиля публикации

В промежуточной среде необходим файл *robots. txt* , поэтому для его развертывания необходимо обновить только профиль публикации.

1. В Visual Studio откройте *промежуточную среду. pubxml*.
2. В конце файла перед закрывающим тегом `</Project>` добавьте следующую разметку:

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    Этот код создает новый *целевой объект* , который будет выполнять собираются дополнительные файлы для развертывания. Целевой объект состоит из одной или нескольких задач, выполняемых MSBuild на основе указанных условий.

    Атрибут `Include` указывает, что папка, в которой следует найти файлы, — это *екстрафилес*, расположенные на том же уровне, что и папка проекта. MSBuild будет собираются все файлы из этой папки и рекурсивно из всех вложенных папок (двойная звездочка указывает рекурсивные вложенные папки). С помощью этого кода можно разместить несколько файлов, а также файлы во вложенных папках в папке *екстрафилес* , при этом будут развернуты все файлы.

    Элемент `DestinationRelativePath` указывает, что папки и файлы должны быть скопированы в корневую папку конечного веб-сайта в том же файле и структуре папок, где они находятся в папке *екстрафилес* . Если вы хотите скопировать саму папку *екстрафилес* , значение `DestinationRelativePath` будет равно *Екстрафилес\%(рекурсиведир)% (имя файла)% (расширение)* .
3. В конце файла перед закрывающим тегом `</Project>` добавьте следующую разметку, указывающую, когда следует выполнять новый целевой объект.

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    Этот код приводит к тому, что новый целевой объект `CustomCollectFiles` будет выполняться при каждом выполнении целевого объекта, который копирует файлы в целевую папку. Для публикации и создания пакета развертывания существует отдельный целевой объект, а новый целевой объект внедряется в обе целевые объекты на случай, если вы решили развернуть их с помощью пакета развертывания вместо публикации.

    Файл *. pubxml* теперь выглядит как в следующем примере:

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. Сохраните и закройте *промежуточный файл. pubxml* .

## <a name="publish-to-staging"></a>Опубликовать в промежуточной среде

С помощью публикации одним щелчком или командной строки опубликуйте приложение с помощью промежуточного профиля.

При использовании публикации одним щелчком можно проверить в окне **предварительного просмотра** , куда будет скопирован файл *robots. txt* . В противном случае используйте средство FTP, чтобы убедиться, что файл *robots. txt* находится в корневой папке веб-сайта после развертывания.

## <a name="summary"></a>Сводка

Эта серия руководств по развертыванию веб-приложения ASP.NET для сторонних поставщиков услуг размещения завершается. Дополнительные сведения о любом из разделов, рассмотренных в этих учебниках, см. на [карте содержимого развертывания ASP.NET](https://go.microsoft.com/fwlink/p/?LinkId=282413).

## <a name="more-information"></a>Дополнительные сведения

Если вы умеете работать с файлами MSBuild, можно автоматизировать многие другие задачи развертывания, написав код в *pubxml* -файлы (для задач конкретного профиля) или файл Project *. wpp. targets* (для задач, которые применяются ко всем профилям). Дополнительные сведения о файлах *pubxml* и *WPP. targets* см. в разделе [как изменить параметры развертывания в файлах профиля публикации (. pubxml) и в файле. wpp. targets в веб-проектах Visual Studio](https://msdn.microsoft.com/library/ff398069). Основные сведения о коде MSBuild см. в разделе **Анатомия файла проекта** в [серии развертывания предприятия: Общие сведения о файле проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Сведения о работе с файлами MSBuild для выполнения задач в собственных сценариях см. в этой книге: в [Microsoft Build Engine: использование MSBuild и Team Foundation Build с помощью](http://msbuildbook.com) Саид Ибрахам Хашими и Уильям барсоломев.

## <a name="acknowledgements"></a>Благодарности

Я хотел бы поблагодарить следующих людей, которые внесли значительные вклады в содержание этой серии руководств:

- [Альберто ПоблаЦион, MVP &amp; MCT, Испания](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Жарод Фергюсон, MVP по разработке платформы данных США
- Харша Миттал, Microsoft
- [Jon Гэллоуэй](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Кристина Олсон, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Майк Поуп, Майкрософт](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Мохит Сривастава, Microsoft
- [Раффаеле Риалди, Италия](http://www.iamraf.net/)
- [Рик Андерсон (, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Саид Хашими, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Скотт Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Скотт Хантер, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Срđан Боžовиć, Сербия](http://msforge.net/blogs/zmajcek/)
- [Вишал Джоши, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [Назад](command-line-deployment.md)
> [Вперед](troubleshooting.md)
