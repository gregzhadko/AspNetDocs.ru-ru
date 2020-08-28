---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: Создание хранимых процедур и определяемых пользователем функций с помощью управляемого кода (VB) | Документация Майкрософт
author: rick-anderson
description: Microsoft SQL Server 2005 интегрируется с общеязыковой средой выполнения .NET и позволяет разработчикам создавать объекты базы данных с помощью управляемого кода. Этот учебник...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 30c37750d89ff3503ead32c0b2a9708b99d785ff
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045290"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>Создание хранимых процедур и определяемых пользователем функций с помощью управляемого кода (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip) или [скачать PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 интегрируется с общеязыковой средой выполнения .NET и позволяет разработчикам создавать объекты базы данных с помощью управляемого кода. В этом руководстве показано, как создавать управляемые хранимые процедуры и управляемые определяемые пользователем функции с помощью кода Visual Basic или C#. Также показано, как эти выпуски Visual Studio позволяют отлаживать такие управляемые объекты базы данных.

## <a name="introduction"></a>Введение

Базы данных, например Microsoft s SQL Server 2005, используют [Transact-язык SQL (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) для вставки, изменения и извлечения данных. Большинство систем баз данных включают конструкции для группирования ряда инструкций SQL, которые затем можно выполнять в виде одной многократно используемой единицы. Хранимые процедуры являются одним из примеров. Другой — *определяемые пользователем функции*(UDF) — конструкция, которая будет рассмотрена более подробно на шаге 9.

По сути, SQL предназначен для работы с наборами данных. `SELECT`Инструкции, `UPDATE` и по `DELETE` сути применяются ко всем записям в соответствующей таблице и ограничиваются только их `WHERE` предложениями. Однако существует множество функций языка, предназначенных для работы с одной записью за раз и для манипулирования скалярными данными. [ `CURSOR` позволяют выполнять](http://www.sqlteam.com/item.asp?ItemID=553) циклический перебор набора записей за один раз. Функции обработки строк, такие как `LEFT` , `CHARINDEX` и, `PATINDEX` работающие с скалярными данными. SQL также включает в себя инструкции потока управления, такие как `IF` и `WHILE` .

До Microsoft SQL Server 2005 хранимые процедуры и определяемые пользователем функции можно определить только как коллекцию инструкций T-SQL. Однако SQL Server 2005 была разработана для интеграции [со средой CLR, которая](https://msdn.microsoft.com/netframework/aa497266.aspx)является средой выполнения, используемой всеми сборками .NET. Следовательно, хранимые процедуры и UDF в базе данных SQL Server 2005 можно создать с помощью управляемого кода. То есть хранимую процедуру или определяемую пользователем функцию можно создать как метод в классе Visual Basic. Это позволяет этим хранимым процедурам и функциям UDF использовать функции в .NET Framework и из собственных пользовательских классов.

В этом учебнике мы рассмотрим, как создавать управляемые хранимые процедуры и определяемые пользователем функции и как интегрировать их в базу данных Northwind. Давайте приступим к работе!

> [!NOTE]
> Управляемые объекты базы данных имеют некоторые преимущества по сравнению с аналогами SQL. Основные преимущества языка и возможности повторного использования существующего кода и логики. Однако управляемые объекты базы данных, скорее всего, будут менее эффективными при работе с наборами данных, которые не требуют значительной процедурной логики. Более подробное обсуждение преимуществ использования управляемого кода и T-SQL см. в статье [преимущества использования управляемого кода для создания объектов базы данных](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx).

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>Шаг 1. Перемещение базы данных Northwind из`App_Data`

Все наши учебники, таким образом, использовали файл базы данных Microsoft SQL Server 2005 Express Edition в папке Web Applications `App_Data` . Размещение базы данных в `App_Data` упрощенном распределении и запуске этих учебников, так как все файлы были размещены в одном каталоге и не требуют дополнительных действий по настройке для тестирования учебника.

Тем не менее, в этом руководстве мы добавим базу данных Northwind из базы данных `App_Data` и явно зарегистрируйте ее в SQL Server 2005, Экспресс-выпуск экземпляре. Хотя мы можем выполнить действия, описанные в этом учебнике, с базой данных в `App_Data` папке, выполнение ряда шагов значительно упрощается путем явной регистрации базы данных с SQL Server 2005, Экспресс-выпуск экземпляром базы данных.

В загружаемом файле для этого учебника есть два файла базы данных: `NORTHWND.MDF` и `NORTHWND_log.LDF` находятся в папке с именем `DataFiles` . Если вы используете собственную реализацию руководств, закройте Visual Studio и переместите `NORTHWND.MDF` `NORTHWND_log.LDF` файлы и из папки веб-сайта s `App_Data` в папку за пределами веб-сайта. После перемещения файлов базы данных в другую папку необходимо зарегистрировать базу данных Northwind в экземпляре базы данных SQL Server 2005, экспресс-выпуск. Это можно сделать в SQL Server Management Studio. Если на компьютере установлен выпуск, отличный от Express, SQL Server 2005, вероятно, у вас уже установлена Management Studio. Если на компьютере имеется только SQL Server 2005, экспресс-выпуск, загрузите и установите [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Запустите среду SQL Server Management Studio. Как показано на рис. 1, Management Studio начинается с запроса сервера, к которому нужно подключиться. Введите Локалхост\склекспресс в поле имя сервера, выберите Проверка подлинности Windows в раскрывающемся списке Проверка подлинности и нажмите кнопку Подключить.

![Подключение к соответствующему экземпляру базы данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**Рис. 1**. подключение к соответствующему экземпляру базы данных

После подключения в окне обозревателя объектов будут перечислены сведения об экземпляре базы данных SQL Server 2005, экспресс-выпуск, включая его базы данных, сведения о безопасности, параметры управления и т. д.

Необходимо присоединить базу данных Northwind в `DataFiles` папке (или в любом месте, где она была перемещена) в экземпляр базы данных SQL Server 2005, Экспресс-выпуск. Щелкните правой кнопкой мыши папку базы данных и выберите пункт Присоединить в контекстном меню. Откроется диалоговое окно Присоединение баз данных. Нажмите кнопку "Добавить", выполните детализацию до соответствующего `NORTHWND.MDF` файла и нажмите кнопку "ОК". На этом этапе экран должен выглядеть примерно так, как показано на рис. 2.

[![Подключение к соответствующему экземпляру базы данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**Рис. 2**. подключение к соответствующему экземпляру базы данных ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png))

> [!NOTE]
> При подключении к экземпляру SQL Server 2005, экспресс-выпуск через Management Studio диалоговое окно Присоединение баз данных не позволяет выполнять детализацию в каталогах профилей пользователей, таких как мои документы. Поэтому не забудьте поместить `NORTHWND.MDF` `NORTHWND_log.LDF` файлы и в каталог профиля, не относящийся к пользователю.

Нажмите кнопку ОК, чтобы присоединить базу данных. Диалоговое окно Присоединение баз данных закроется, и в обозревателе объектов появится список только что подключенной базы данных. Скорее всего, база данных Northwind имеет такое имя, как `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` . Переименуйте базу данных в Northwind, щелкнув ее правой кнопкой мыши и выбрав пункт Переименовать.

![Переименование базы данных в Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**Рис. 3**. Переименование базы данных в Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>Шаг 2. Создание нового решения и SQL Server проекта в Visual Studio

Для создания управляемых хранимых процедур или определяемых пользователем функций в SQL Server 2005 мы будем писать хранимую процедуру и логику UDF как Visual Basic код в классе. После написания кода необходимо скомпилировать этот класс в сборку ( `.dll` файл), зарегистрировать сборку в SQL Server базе данных, а затем создать хранимую процедуру или объект UDF в базе данных, указывающей на соответствующий метод в сборке. Эти действия можно выполнить вручную. Мы можем создать код в любом текстовом редакторе, скомпилировать его из командной строки с помощью Visual Basic компилятора ( `vbc.exe` ), зарегистрировать его в базе данных с помощью [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) команды или из Management Studio и добавить хранимую процедуру или объект UDF с помощью аналогичных средств. К счастью, в версии Professional и Team Systems Visual Studio входит SQL Server тип проекта, который автоматизирует эти задачи. В этом учебнике мы рассмотрим использование типа проекта SQL Server для создания управляемой хранимой процедуры и определяемой пользователем функции.

> [!NOTE]
> Если вы используете Visual Web Developer или стандартный выпуск Visual Studio, то вместо этого придется использовать ручной подход. На шаге 13 приведены подробные инструкции по выполнению этих шагов вручную. Я рекомендую прочесть шаги с 2 по 12, прежде чем считывать шаг 13, так как эти шаги содержат важные SQL Server инструкции по настройке, которые необходимо применить независимо от используемой версии Visual Studio.

Для начала откройте Visual Studio. В меню Файл выберите пункт Создать проект, чтобы открыть диалоговое окно Новый проект (см. рис. 4). Выполните детализацию до типа проекта базы данных, а затем в шаблонах, перечисленных справа, выберите Создание нового SQL Server проекта. Я выбрал имя этого проекта `ManagedDatabaseConstructs` и поместил его в решение с именем `Tutorial75` .

[![Создание нового проекта SQL Server](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**Рис. 4**. Создание нового проекта SQL Server ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))

Нажмите кнопку ОК в диалоговом окне Новый проект, чтобы создать решение и SQL Server проект.

Проект SQL Server привязан к определенной базе данных. Следовательно, после создания нового проекта SQL Server мы сразу же запросили указать эти сведения. На рис. 5 показано диалоговое окно Создание ссылки на базу данных, которое было заполнено, чтобы указать базу данных Northwind, зарегистрированную в SQL Server 2005, экспресс-выпуск экземпляре базы данных на шаге 1.

![Связывание проекта SQL Server с базой данных "Борей"](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**Рис. 5**. связывание SQL Server проекта с базой данных «Борей»

Чтобы выполнить отладку управляемых хранимых процедур и определяемых пользователем функций, которые будут созданы в рамках этого проекта, необходимо включить поддержку отладки SQL/CLR для подключения. При каждом связывании SQL Server проекта с новой базой данных (как мы делали на рис. 5) Visual Studio запрашивает у нас необходимость включить отладку SQL/CLR для подключения (см. рис. 6). Нажмите кнопку "Да".

![Включить отладку SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**Рис. 6**. Включение отладки SQL/CLR

На этом этапе в решение добавлен новый проект SQL Server. Он содержит папку с именем `Test Scripts` `Test.sql` и файлом, который используется для отладки управляемых объектов базы данных, созданных в проекте. Мы рассмотрим отладку на шаге 12.

Теперь мы можем добавить в этот проект новые управляемые хранимые процедуры и определяемые пользователем функции, но перед тем как мы добавим в решение существующее веб-приложение. В меню Файл выберите пункт Добавить и выберите существующий веб-сайт. Перейдите к соответствующей папке веб-сайта и нажмите кнопку ОК. Как показано на рис. 7, это приведет к обновлению решения для включения двух проектов: веб-сайта и `ManagedDatabaseConstructs` проекта SQL Server.

![обозреватель решений теперь содержит два проекта](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**Рис. 7**. Обозреватель решений теперь содержит два проекта

`NORTHWNDConnectionString`Значение в `Web.config` данный момент ссылается на `NORTHWND.MDF` файл в `App_Data` папке. Так как мы удалили эту базу данных из `App_Data` и явно зарегистрировали ее в SQL Server 2005, Экспресс-выпуск экземпляре базы данных, необходимо соответствующим образом обновить `NORTHWNDConnectionString` значение. Откройте `Web.config` файл на веб-сайте и измените `NORTHWNDConnectionString` значение таким образом, чтобы строка подключения была прочитана: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` . После этого изменения `<connectionStrings>` раздел в `Web.config` должен выглядеть следующим образом:

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> Как обсуждалось в [предыдущем руководстве](debugging-stored-procedures-vb.md), при отладке SQL Server объекта из клиентского приложения, например веб-сайта ASP.NET, необходимо отключить пулы подключений. Приведенная выше строка подключения отключает пулы соединений ( `Pooling=false` ). Если вы не планируете выполнять отладку управляемых хранимых процедур и определяемых пользователем функций с веб-сайта ASP.NET, включите пулы подключений.

## <a name="step-3-creating-a-managed-stored-procedure"></a>Шаг 3. Создание управляемой хранимой процедуры

Чтобы добавить управляемую хранимую процедуру в базу данных Northwind, сначала необходимо создать хранимую процедуру как метод в проекте SQL Server. В обозреватель решений щелкните правой кнопкой мыши `ManagedDatabaseConstructs` имя проекта и выберите Добавить новый элемент. Откроется диалоговое окно Добавление нового элемента, в котором перечислены типы управляемых объектов базы данных, которые могут быть добавлены в проект. Как показано на рис. 8, сюда входят хранимые процедуры и определяемые пользователем функции, а также другие.

Начнем с добавления хранимой процедуры, которая просто возвращает все продукты, которые больше не поддерживаются. Назовите новый файл хранимой процедуры `GetDiscontinuedProducts.vb` .

[![Добавьте новую хранимую процедуру с именем Жетдисконтинуедпродуктс. vb.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**Рис. 8**. Добавление новой хранимой процедуры с именем `GetDiscontinuedProducts.vb` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png))

Будет создан новый файл класса Visual Basic со следующим содержимым:

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

Обратите внимание, что хранимая процедура реализована в виде `Shared` метода в `Partial` файле класса с именем `StoredProcedures` . Более того, `GetDiscontinuedProducts` метод снабжен [ `SqlProcedure` атрибутом](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx), который помечает метод как хранимую процедуру.

Следующий код создает `SqlCommand` объект и задает `CommandText` для него `SELECT` запрос, возвращающий все столбцы из `Products` таблицы Products, чье `Discontinued` поле равно 1. Затем он выполняет команду и отправляет результаты обратно клиентскому приложению. Добавьте этот код в `GetDiscontinuedProducts` метод.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

Все управляемые объекты базы данных имеют доступ к [ `SqlContext` объекту](https://msdn.microsoft.com/library/ms131108.aspx) , который представляет контекст вызывающего объекта. `SqlContext`Предоставляет доступ к [ `SqlPipe` объекту](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) через его [ `Pipe` свойство](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx). Этот `SqlPipe` объект используется для паром информации между базой данных SQL Server и вызывающим приложением. Как следует из названия, [ `ExecuteAndSend` метод](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) выполняет переданный `SqlCommand` объект и отправляет результаты обратно клиентскому приложению.

> [!NOTE]
> Управляемые объекты базы данных лучше всего подходят для хранимых процедур и пользовательских функций, использующих процедурную логику, а не логику на основе наборов. Процедурная логика включает в себя работу с наборами данных на основе строк или работу с скалярными данными. `GetDiscontinuedProducts`Однако только что созданный метод не требует процедурной логики. Таким образом, в идеале он будет реализован как хранимая процедура T-SQL. Он реализуется как управляемая хранимая процедура для демонстрации действий, необходимых для создания и развертывания управляемых хранимых процедур.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>Шаг 4. Развертывание управляемой хранимой процедуры

После выполнения этого кода мы готовы к развертыванию в базе данных Northwind. Развертывание SQL Server проекта компилирует код в сборку, регистрирует сборку в базе данных и создает соответствующие объекты в базе данных, связывая их с соответствующими методами в сборке. Точный набор задач, выполняемых при развертывании, более точно написан на шаге 13. Щелкните правой кнопкой мыши `ManagedDatabaseConstructs` имя проекта в Обозреватель решений и выберите пункт Развернуть. Однако развертывание завершается сбоем со следующей ошибкой: неправильный синтаксис рядом с "EXTERNAL". Возможно, следует установить более высокий уровень совместимости для текущей базы данных, чтобы включить эту функцию. См. справку по хранимой процедуре `sp_dbcmptlevel` .

Это сообщение об ошибке возникает при попытке зарегистрировать сборку в базе данных Northwind. Чтобы зарегистрировать сборку в базе данных SQL Server 2005, уровень совместимости Database s должен быть равен 90. По умолчанию новые базы данных SQL Server 2005 имеют уровень совместимости 90. Однако базы данных, созданные с помощью Microsoft SQL Server 2000, имеют уровень совместимости по умолчанию 80. Так как база данных Northwind изначально была базой данных Microsoft SQL Server 2000, ее уровень совместимости в настоящее время равен 80, и поэтому его необходимо увеличить до 90, чтобы зарегистрировать управляемые объекты базы данных.

Чтобы обновить уровень совместимости базы данных, откройте новое окно запроса в Management Studio и введите:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

Щелкните значок выполнить на панели инструментов, чтобы выполнить приведенный выше запрос.

[![Обновление уровня совместимости базы данных "Борей"](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**Рис. 9**. обновление уровня совместимости базы данных Northwind ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png))

После обновления уровня совместимости повторно разверните проект SQL Server. На этот раз развертывание должно завершиться без ошибок.

Вернитесь в SQL Server Management Studio, щелкните правой кнопкой мыши базу данных Northwind в обозревателе объектов и выберите команду Обновить. Далее перейдите в папку Программирование, а затем разверните папку сборки. Как показано на рис. 10, база данных Northwind теперь включает сборку, созданную `ManagedDatabaseConstructs` проектом.

![Сборка Манажеддатабасеконструктс теперь зарегистрирована в базе данных "Борей"](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**Рис. 10**. `ManagedDatabaseConstructs` Теперь сборка зарегистрирована в базе данных Northwind

Также разверните папку Хранимые процедуры. Там вы увидите хранимую процедуру с именем `GetDiscontinuedProducts` . Эта хранимая процедура была создана процессом развертывания и указывает на `GetDiscontinuedProducts` метод в `ManagedDatabaseConstructs` сборке. При `GetDiscontinuedProducts` выполнении хранимой процедуры она, в свою очередь, выполняет `GetDiscontinuedProducts` метод. Поскольку это управляемая хранимая процедура, ее нельзя изменить с помощью Management Studio (следовательно, значок блокировки рядом с именем хранимой процедуры).

![Хранимая процедура Жетдисконтинуедпродуктс указана в папке хранимых процедур.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**Рис. 11**. `GetDiscontinuedProducts` хранимая процедура указана в папке хранимых процедур

Прежде чем можно будет вызвать управляемую хранимую процедуру, необходимо преодолеть еще одно препятствие: база данных настроена для предотвращения выполнения управляемого кода. Проверьте это, открыв новое окно запроса и выполнив `GetDiscontinuedProducts` хранимую процедуру. Вы получите следующее сообщение об ошибке: выполнение пользовательского кода в .NET Framework отключено. Включите параметр конфигурации "clr enabled".

Чтобы просмотреть сведения о конфигурации базы данных Northwind, введите и выполните команду `exec sp_configure` в окне запроса. Это показывает, что параметр clr enabled в настоящее время имеет значение 0.

[![Параметр clr enabled в настоящее время имеет значение 0](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**Рис. 12**. в настоящее время параметр clr enabled имеет значение 0 ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png))

Обратите внимание, что каждый параметр конфигурации на рис. 12 имеет следующие четыре значения: минимальное и максимальное значения, а также конфигурации и значения запуска. Чтобы обновить значение конфигурации для параметра Enabled CLR, выполните следующую команду:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

При повторном запуске `exec sp_configure` вы увидите, что приведенная выше инструкция обновила параметр конфигурации s Enabled CLR в значение 1, но значение запуска по-прежнему равно 0. Чтобы это изменение конфигурации вступило в силу, необходимо выполнить [ `RECONFIGURE` команду](https://msdn.microsoft.com/library/ms176069.aspx), которая установит значение Run в текущее значение конфигурации. Просто введите `RECONFIGURE` в окне запроса и щелкните значок выполнить на панели инструментов. Если вы запустите его, `exec sp_configure` вы увидите значение 1 для параметров config и Run в CLR Enabled.

После завершения настройки с включенной средой CLR мы готовы к запуску управляемой `GetDiscontinuedProducts` хранимой процедуры. В окне запроса введите и выполните команду `exec` `GetDiscontinuedProducts` . Вызов хранимой процедуры приводит к выполнению соответствующего управляемого кода в `GetDiscontinuedProducts` методе. Этот код создает `SELECT` запрос, возвращающий все продукты, которые больше не поддерживаются, и возвращает эти данные вызывающему приложению, которое SQL Server Management Studio в этом экземпляре. Management Studio получает эти результаты и отображает их в окне результатов.

[![Хранимая процедура Жетдисконтинуедпродуктс возвращает все неподдерживаемые продукты.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**Рис. 13**. `GetDiscontinuedProducts` хранимая процедура возвращает все неподдерживаемые продукты ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png))

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>Шаг 5. Создание управляемых хранимых процедур, принимающих входные параметры

Многие из запросов и хранимых процедур, созданных в рамках этих учебников, используют *Параметры*. Например, в учебнике [Создание новых хранимых процедур для адаптеров TableAdapter типизированного набора данных](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) мы создали хранимую процедуру с именем `GetProductsByCategoryID` , которая принимает входной параметр с именем `@CategoryID` . Затем хранимая процедура возвращает все продукты, `CategoryID` поле которых соответствует значению заданного `@CategoryID` параметра.

Чтобы создать управляемую хранимую процедуру, которая принимает входные параметры, просто укажите эти параметры в определении метода. Чтобы проиллюстрировать это, добавим в проект другую управляемую хранимую процедуру `ManagedDatabaseConstructs` с именем `GetProductsWithPriceLessThan` . Эта управляемая хранимая процедура принимает входной параметр, указывающий цену, и возвращает все продукты, `UnitPrice` поле которых меньше значения параметра s.

Чтобы добавить в проект новую хранимую процедуру, щелкните правой кнопкой мыши `ManagedDatabaseConstructs` имя проекта и выберите команду Добавить новую хранимую процедуру. Задайте файлу имя `GetProductsWithPriceLessThan.vb`. Как было показано на шаге 3, в результате будет создан новый файл Visual Basic класса с методом, названным `GetProductsWithPriceLessThan` в `Partial` классе `StoredProcedures` .

Обновите `GetProductsWithPriceLessThan` Определение метода, чтобы он принимал [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) входной параметр с именем `price` и написал код для выполнения и возвращал результаты запроса:

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

`GetProductsWithPriceLessThan`Определение метода и код в точности напоминает определение и код `GetDiscontinuedProducts` метода, созданного на шаге 3. Единственное отличие заключается в том, что `GetProductsWithPriceLessThan` метод принимает в качестве входного параметра ( `price` ), `SqlCommand` запрос s включает параметр ( `@MaxPrice` ), а в коллекцию s добавляется параметр, `SqlCommand` `Parameters` которому присваивается значение `price` переменной.

После добавления этого кода повторно разверните проект SQL Server. Затем вернитесь к SQL Server Management Studio и обновите папку хранимых процедур. Вы увидите новую запись `GetProductsWithPriceLessThan` . В окне запроса введите и выполните команду `exec GetProductsWithPriceLessThan 25` , в которой будут перечислены все продукты, размер которых меньше $25, как показано на рис. 14.

[![Отображаются продукты под управлением $25](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**Рис. 14**. отображаются продукты под $25 ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png))

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>Шаг 6. вызов управляемой хранимой процедуры из уровня доступа к данным

На этом этапе мы добавили в `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` проект управляемые хранимые процедуры и `ManagedDatabaseConstructs` зарегистрировали их в базе данных Northwind SQL Server. Эти управляемые хранимые процедуры также вызываются из SQL Server Management Studio (см. рис. 13 и 14). Однако, чтобы приложение ASP.NET использовало эти управляемые хранимые процедуры, необходимо добавить их к уровням доступа к данным и бизнес-логики в архитектуре. На этом шаге мы добавим два новых метода в `ProductsTableAdapter` в `NorthwindWithSprocs` типизированном наборе данных, который изначально был создан в руководстве [Создание новых хранимых процедур для адаптеров TableAdapter типизированного набора данных](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) . На шаге 7 в BLL будут добавлены соответствующие методы.

Откройте `NorthwindWithSprocs` типизированный набор данных в Visual Studio и начните с добавления нового метода к `ProductsTableAdapter` именованному `GetDiscontinuedProducts` . Чтобы добавить новый метод в TableAdapter, щелкните имя TableAdapter в конструкторе правой кнопкой мыши и выберите пункт Добавить запрос в контекстном меню.

> [!NOTE]
> Так как мы переместили базу данных Northwind из `App_Data` папки в экземпляр базы данных SQL Server 2005, Экспресс-выпуск, крайне важно, чтобы соответствующая строка подключения в Web.config была обновлена в соответствии с этим изменением. На шаге 2 мы обсуждали обновление `NORTHWNDConnectionString` значения в `Web.config` . Если вы забыли внести это обновление, появится сообщение об ошибке не удалось добавить запрос. Не удается найти соединение `NORTHWNDConnectionString` для объекта `Web.config` в диалоговом окне при попытке добавить новый метод в TableAdapter. Чтобы устранить эту ошибку, нажмите кнопку ОК, а затем перейдите на страницу `Web.config` и обновите `NORTHWNDConnectionString` значение, как описано на шаге 2. Затем попробуйте повторно добавить метод в TableAdapter. На этот раз она должна работать без ошибок.

При добавлении нового метода запускается мастер настройки запросов TableAdapter, который мы использовали много раз в прошлых учебных курсах. На первом шаге мы предложим указать, как TableAdapter должен обращаться к базе данных: через специальный оператор SQL или с помощью новой или существующей хранимой процедуры. Так как мы уже создали и зарегистрировали `GetDiscontinuedProducts` управляемую хранимую процедуру с базой данных, выберите параметр использовать существующую хранимую процедуру и нажмите кнопку Далее.

[![Выбор параметра "использовать существующую хранимую процедуру"](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**Рис. 15**. Выбор параметра использовать существующую хранимую процедуру ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png))

На следующем экране запрашивается хранимая процедура, которую вызовет метод. Выберите `GetDiscontinuedProducts` управляемую хранимую процедуру из раскрывающегося списка и нажмите кнопку Далее.

[![Выбор управляемой хранимой процедуры Жетдисконтинуедпродуктс](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**Рис. 16**. Выбор `GetDiscontinuedProducts` управляемой хранимой процедуры ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png))

Затем будет предложено указать, возвращает ли хранимая процедура строки, одно значение или ничего. Поскольку `GetDiscontinuedProducts` возвращает набор неподдерживаемых строк продукта, выберите первый параметр (табличные данные) и нажмите кнопку Далее.

[![Выбор параметра табличных данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**Рис. 17**. Выбор параметра табличных данных ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png))

На последнем экране мастера можно указать используемые шаблоны доступа к данным и имена результирующих методов. Оставьте флажки установленными и назовите методы `FillByDiscontinued` и `GetDiscontinuedProducts` . Чтобы завершить работу мастера, нажмите кнопку Готово.

[![Назовите методы Филлбидисконтинуед и Жетдисконтинуедпродуктс](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**Рис. 18**. Именование методов `FillByDiscontinued` и `GetDiscontinuedProducts` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png))

Повторите эти шаги, чтобы создать методы с именами `FillByPriceLessThan` и `GetProductsWithPriceLessThan` в `ProductsTableAdapter` для `GetProductsWithPriceLessThan` управляемой хранимой процедуры.

На рис. 19 показан снимок экрана конструктора набора данных после добавления методов в `ProductsTableAdapter` для `GetDiscontinuedProducts` и `GetProductsWithPriceLessThan` управляемых хранимых процедур.

[![Продуктстаблеадаптер включает новые методы, добавленные на этом шаге.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**Рис. 19**. `ProductsTableAdapter` включает новые методы, добавленные на этом шаге ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png)).

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>Шаг 7. Добавление соответствующих методов на уровень бизнес-логики

Теперь, когда уровень доступа к данным обновлен, чтобы включить методы для вызова управляемых хранимых процедур, добавленных в шагах 4 и 5, необходимо добавить соответствующие методы к уровню бизнес-логики. Добавьте в класс следующие два метода `ProductsBLLWithSprocs` :

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

Оба метода просто вызывают соответствующий метод DAL и возвращают `ProductsDataTable` экземпляр. `DataObjectMethodAttribute`Разметка выше каждого метода приводит к тому, что эти методы включаются в раскрывающийся список на вкладке Выбор мастера настройки источника данных ObjectDataSource.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>Шаг 8. вызов управляемых хранимых процедур из уровня представления

Благодаря бизнес-логике и слоям доступа к данным, дополненным к включению поддержки вызова `GetDiscontinuedProducts` и `GetProductsWithPriceLessThan` управляемых хранимых процедур, можно отобразить результаты этих хранимых процедур на странице ASP.NET.

Откройте `ManagedFunctionsAndSprocs.aspx` страницу в `AdvancedDAL` папке и в области элементов перетащите элемент управления GridView на конструктор. Присвойте свойству GridView s значение `ID` `DiscontinuedProducts` и, используя его смарт-тег, привяжите его к новому ObjectDataSource с именем `DiscontinuedProductsDataSource` . Настройте ObjectDataSource для извлечения данных из `ProductsBLLWithSprocs` метода класса s `GetDiscontinuedProducts` .

[![Настройка ObjectDataSource для использования класса Продуктсбллвисспрокс](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**Рис. 20**. Настройка ObjectDataSource для использования `ProductsBLLWithSprocs` класса ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png))

[![Выберите метод Жетдисконтинуедпродуктс из раскрывающегося списка на вкладке Выбор.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**Рис. 21**. Выбор `GetDiscontinuedProducts` метода из раскрывающегося списка на вкладке «Выбор» ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png))

Поскольку эта сетка будет использоваться для просто вывода сведений о продукте, установите в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет), а затем нажмите кнопку Готово.

После завершения работы мастера Visual Studio автоматически добавит BoundField или CheckBoxField для каждого поля данных в `ProductsDataTable` . Удалите все эти поля за исключением `ProductName` и `Discontinued` , после чего декларативная разметка GridView и ObjectDataSource s должна выглядеть следующим образом:

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

Уделите несколько минут для просмотра этой страницы в браузере. При посещении страницы ObjectDataSource вызывает `ProductsBLLWithSprocs` метод Class s `GetDiscontinuedProducts` . Как было показано на шаге 7, этот метод вызывает `ProductsDataTable` метод класса DAL s `GetDiscontinuedProducts` , который вызывает `GetDiscontinuedProducts` хранимую процедуру. Эта хранимая процедура является управляемой хранимой процедурой и выполняет код, созданный на шаге 3 и возвращающий Неподдерживаемые продукты.

Результаты, возвращаемые управляемой хранимой процедурой, упаковываются в `ProductsDataTable` компонент DAL, а затем возвращаются в слой BLL, который затем возвращает их на уровень представления, где они привязаны к GridView и отображаются. Как и ожидалось, в сетке перечислены продукты, которые больше не поддерживаются.

[![Указаны Неподдерживаемые продукты](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**Рис. 22**. список неподдерживаемых продуктов ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png))

Для получения дополнительных рекомендаций добавьте на страницу текстовое поле и другой элемент управления GridView. В этом элементе GridView отображаются продукты, меньшие, чем сумма, введенная в текстовое поле, путем вызова `ProductsBLLWithSprocs` метода класса s `GetProductsWithPriceLessThan` .

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>Шаг 9. Создание и вызов пользовательских функций T-SQL

Определяемые пользователем функции (UDF) — это объекты базы данных, которые точно имитируют семантику функций в языках программирования. Как и функция в Visual Basic, UDF может включать переменное число входных параметров и возвращать значение определенного типа. Определяемая пользователем функция может возвращать скалярные данные — строку, целое число и так далее или табличные данные. Давайте посмотрим на оба типа UDF, начиная с определяемой пользователем функции, возвращающей скалярный тип данных.

Следующая определяемая пользователем функция вычисляет оценочное значение инвентаризации для конкретного продукта. Для этого используются три входных параметра: `UnitPrice` `UnitsInStock` значения, и `Discontinued` для конкретного продукта — и возвращает значение типа `money` . Он вычисляет оценочное значение инвентаризации путем умножения на `UnitPrice` `UnitsInStock` . Для неподдерживаемых элементов это значение является половиной.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

После добавления этой определяемой пользователем функции в базу данных ее можно найти с помощью Management Studio, развернув папку Программирование, затем функции и затем функции скалярного значения. Его можно использовать в `SELECT` запросе следующим образом:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

Пользователь добавил `udf_ComputeInventoryValue` определяемую пользователем функцию в базу данных Northwind; На рис. 23 показаны выходные данные указанного выше `SELECT` запроса при просмотре с помощью Management Studio. Также обратите внимание, что определяемая пользователем функция указана в папке функции скалярных значений в обозревателе объектов.

[![Все значения инвентаризации продуктов перечислены](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**Рис. 23**. список значений инвентаризации продуктов ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png))

Пользовательские функции могут также возвращать табличные данные. Например, можно создать определяемую пользователем функцию, которая возвращает продукты, принадлежащие к определенной категории:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID`UDF принимает `@CategoryID` входной параметр и возвращает результаты указанного `SELECT` запроса. После создания на эту определяемую пользователем функцию можно ссылаться в `FROM` `JOIN` предложении (или) `SELECT` запроса. В следующем примере возвращаются `ProductID` `ProductName` значения, и `CategoryID` для каждого из напитков.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

Пользователь добавил `udf_GetProductsByCategoryID` определяемую пользователем функцию в базу данных Northwind; На рис. 24 показаны выходные данные приведенного выше `SELECT` запроса при просмотре с помощью Management Studio. Определяемые пользователем функции, возвращающие табличные данные, можно найти в папке функции "Таблица-значение" обозревателя объектов.

[![ProductID, ProductName и CategoryID указаны для каждого из напитков.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**Рис. 24**. `ProductID` `ProductName` `CategoryID` перечисляются, и для каждого из напитков ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png)).

> [!NOTE]
> Дополнительные сведения о создании и использовании [определяемых пользователем функций](http://www.sqlteam.com/item.asp?ItemID=1955)см. в этой записи. Также ознакомьтесь [с преимуществами и недостатками определяемых пользователем функций](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1).

## <a name="step-10-creating-a-managed-udf"></a>Шаг 10. Создание управляемой определяемой пользователем функции

`udf_ComputeInventoryValue`Пользовательские функции и, `udf_GetProductsByCategoryID` созданные в приведенных выше примерах, являются объектами базы данных T-SQL. SQL Server 2005 также поддерживает управляемые определяемые пользователем функции, которые можно добавить в `ManagedDatabaseConstructs` проект так же, как и управляемые хранимые процедуры из шагов 3 и 5. Для этого шага Давайте рассмотрим реализацию `udf_ComputeInventoryValue` определяемой пользователем функции в управляемом коде.

Чтобы добавить управляемую определяемую пользователем функцию в `ManagedDatabaseConstructs` проект, щелкните правой кнопкой мыши имя проекта в Обозреватель решений и выберите Добавить новый элемент. Выберите определяемый пользователем шаблон в диалоговом окне Добавление нового элемента и назовите новый файл UDF `udf_ComputeInventoryValue_Managed.vb` .

[![Добавление новой управляемой определяемой пользователем функции в проект Манажеддатабасеконструктс](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**Рис. 25**. Добавление в проект новой управляемой определяемой пользователем функции `ManagedDatabaseConstructs` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png))

Шаблон определяемой пользователем функции создает `Partial` класс `UserDefinedFunctions` с именем с методом, имя которого совпадает с именем файла класса ( `udf_ComputeInventoryValue_Managed` , в данном экземпляре). Этот метод декорирован с помощью [ `SqlFunction` атрибута](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), который помечает метод как управляемую определяемую пользователем функцию.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

В `udf_ComputeInventoryValue` настоящее время метод возвращает [ `SqlString` объект](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) и не принимает входные параметры. Необходимо обновить определение метода таким образом, чтобы оно принимало три входных параметра — `UnitPrice` , `UnitsInStock` и, и `Discontinued` возвращает `SqlMoney` объект. Логика для вычисления значения инвентаризации идентична той, что указана в UDF T-SQL `udf_ComputeInventoryValue` .

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

Обратите внимание, что входные параметры метода UDF имеют соответствующие типы SQL: `SqlMoney` для `UnitPrice` поля, [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) для `UnitsInStock` и [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) для `Discontinued` . Эти типы данных соответствуют типам, определенным в `Products` таблице: `UnitPrice` столбец имеет тип `money` , `UnitsInStock` столбец типа `smallint` и `Discontinued` столбец типа `bit` .

Код начинается с создания `SqlMoney` экземпляра с именем `inventoryValue` , которому присваивается значение 0. `Products`Таблица позволяет `NULL` значениям базы данных в `UnitsInPrice` `UnitsInStock` столбцах и. Поэтому сначала необходимо проверить, содержат ли эти значения `NULL` s, что мы делаем через `SqlMoney` [ `IsNull` свойство](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)Objects. Если `UnitPrice` и `UnitsInStock` , и содержат `NULL` значения, отличные от значений, то мы вычислим, что `inventoryValue` является произведением двух. Затем, если `Discontinued` имеет значение true, то значение будет вдвое меньше.

> [!NOTE]
> `SqlMoney`Объект допускает `SqlMoney` одновременное умножение двух экземпляров. Он не позволяет `SqlMoney` умножить экземпляр на литеральное число с плавающей запятой. Таким образом, чтобы сократить объем `inventoryValue` , умножьте его на новый `SqlMoney` экземпляр, имеющий значение 0,5.

## <a name="step-11-deploying-the-managed-udf"></a>Шаг 11. Развертывание управляемой определяемой пользователем функции

Теперь, когда создана управляемая определяемая пользователем функция, мы готовы к развертыванию ее в базе данных Northwind. Как было показано на шаге 4, управляемые объекты в проекте SQL Server развертываются, если щелкнуть правой кнопкой мыши имя проекта в обозреватель решений и выбрать пункт Развертывание в контекстном меню.

После развертывания проекта вернитесь в SQL Server Management Studio и обновите папку "функции с скалярными значениями". Теперь вы увидите две записи:

- `dbo.udf_ComputeInventoryValue` — ОПРЕДЕЛЯЕМая пользователем функция T-SQL, созданная на шаге 9, и
- `dbo.udf ComputeInventoryValue_Managed` — управляемая определяемая пользователем функция, созданная на шаге 10, которая была только что развернута.

Чтобы протестировать управляемую определяемую пользователем функцию, выполните следующий запрос в Management Studio:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

Эта команда использует управляемую `udf ComputeInventoryValue_Managed` определяемую пользователем функцию вместо определяемой пользователем функции T-SQL `udf_ComputeInventoryValue` , но выходные данные одинаковы. Чтобы увидеть снимок экрана с выходными данными UDF, вернитесь на рис. 23.

## <a name="step-12-debugging-the-managed-database-objects"></a>Шаг 12. Отладка объектов управляемой базы данных

В учебнике [Отладка хранимых процедур](debugging-stored-procedures-vb.md) мы обсуждали три варианта отладки SQL Server с помощью Visual Studio: Непосредственная отладка базы данных, отладка приложений и отладка из проекта SQL Server. Управляемые объекты базы данных не могут быть отлажены с помощью прямой отладки базы данных, но могут быть отлаживаться из клиентского приложения и непосредственно из проекта SQL Server. Чтобы отладка работала, однако база данных SQL Server 2005 должна разрешать отладку SQL/CLR. Вспомним, что при первоначальном создании `ManagedDatabaseConstructs` проекта Visual Studio запросил бы включить отладку SQL/CLR (см. рис. 6 на шаге 2). Этот параметр можно изменить, щелкнув правой кнопкой мыши базу данных в окне обозреватель сервера.

![Убедитесь, что база данных разрешает отладку SQL/CLR.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**Рис. 26**. Проверка того, что база данных разрешает отладку SQL/CLR

Представьте, что нам нужно отладить `GetProductsWithPriceLessThan` управляемую хранимую процедуру. Начнем с установки точки останова в коде `GetProductsWithPriceLessThan` метода.

[![Установка точки останова в методе Жетпродуктсвисприцелесссан](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**Рис. 27**. Задание точки останова в `GetProductsWithPriceLessThan` методе ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png))

Давайте сначала рассмотрим отладку управляемых объектов базы данных из проекта SQL Server. Так как наше решение включает два проекта: `ManagedDatabaseConstructs` проект SQL Server вместе с нашим веб-сайтом — для отладки из проекта SQL Server необходимо указать Visual Studio запустить `ManagedDatabaseConstructs` проект SQL Server при запуске отладки. Щелкните правой кнопкой мыши `ManagedDatabaseConstructs` проект в Обозреватель решений и выберите в контекстном меню пункт Назначить запускаемым проектом.

При `ManagedDatabaseConstructs` запуске проекта из отладчика он выполняет инструкции SQL в `Test.sql` файле, который находится в `Test Scripts` папке. Например, чтобы протестировать `GetProductsWithPriceLessThan` управляемую хранимую процедуру, замените имеющееся `Test.sql` содержимое файла следующей инструкцией, которая вызывает `GetProductsWithPriceLessThan` передачу управляемой хранимой процедуры в `@CategoryID` значение 14,95:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

После того как вы введете приведенный выше скрипт в `Test.sql` , начните отладку, перейдя в меню Отладка и выбрав начать отладку или нажав клавишу F5 или зеленым значком воспроизведения на панели инструментов. Это приведет к построению проектов в решении, развертыванию объектов управляемой базы данных в базе данных Northwind, а затем выполнению `Test.sql` скрипта. На этом этапе будет достигнута точка останова, и мы можем пошагово выполнить `GetProductsWithPriceLessThan` метод, проверить значения входных параметров и т. д.

[![Была нажата точка останова в методе Жетпродуктсвисприцелесссан](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**Рис. 28**. попадание в точку останова в `GetProductsWithPriceLessThan` методе ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png))

Чтобы объект базы данных SQL можно было отлаживать через клиентское приложение, необходимо настроить для базы данных поддержку отладки приложений. Щелкните правой кнопкой мыши базу данных в обозреватель сервера и убедитесь, что установлен флажок Отладка приложения. Кроме того, необходимо настроить приложение ASP.NET для интеграции с отладчиком SQL и отключения пулов соединений. Эти действия подробно описаны на шаге 2 учебника по [хранимым процедурам отладки](debugging-stored-procedures-vb.md) .

После настройки приложения и базы данных ASP.NET установите в качестве запускаемого проекта веб-сайт ASP.NET и начните отладку. При посещении страницы, вызывающей один из управляемых объектов с точкой останова, приложение будет остановлено, а Управление будет включено в отладчик, где можно выполнить код по шагам, как показано на рис. 28.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>Шаг 13. Компиляция и развертывание управляемых объектов базы данных вручную

SQL Server проекты упрощают создание, компиляцию и развертывание управляемых объектов базы данных. К сожалению, SQL Server проекты доступны только в выпусках Visual Studio Professional и Team Systems. Если вы используете Visual Web Developer или стандартный выпуск Visual Studio и хотите использовать управляемые объекты базы данных, необходимо вручную создать и развернуть их. Это включает в себя четыре шага:

1. Создайте файл, содержащий исходный код для управляемого объекта базы данных.
2. Скомпилируйте объект в сборку,
3. Зарегистрируйте сборку в базе данных SQL Server 2005 и
4. Создайте объект базы данных в SQL Server, указывающий на соответствующий метод в сборке.

Чтобы проиллюстрировать эти задачи, давайте создадим новую управляемую хранимую процедуру, которая возвращает те продукты, `UnitPrice` значение которых больше указанного. Создайте новый файл на компьютере с именем `GetProductsWithPriceGreaterThan.vb` и введите в него следующий код (для этого можно использовать Visual Studio, Notepad или любой текстовый редактор):

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

Этот код практически идентичен `GetProductsWithPriceLessThan` методу метода, созданному на шаге 5. Единственным отличием являются имена методов, `WHERE` предложение и имя параметра, используемого в запросе. Вернувшись в `GetProductsWithPriceLessThan` метод, `WHERE` предложение Read: `WHERE UnitPrice < @MaxPrice` . Здесь в `GetProductsWithPriceGreaterThan` мы используем: `WHERE UnitPrice > @MinPrice` .

Теперь необходимо скомпилировать этот класс в сборку. В командной строке перейдите в каталог, где был сохранен `GetProductsWithPriceGreaterThan.vb` файл, и используйте компилятор C# ( `csc.exe` ) для компиляции файла класса в сборку:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

Если папка, содержащая v `bc.exe` , не находится в системе `PATH` , необходимо полностью ссылаться на путь, `%WINDOWS%\Microsoft.NET\Framework\version\` следующим образом:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]

[![Компиляция Жетпродуктсвисприцегреатерсан. vb в сборку](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**Рис. 29**. Компиляция `GetProductsWithPriceGreaterThan.vb` в сборку ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png))

`/t`Флаг указывает, что Visual Basic файл класса должен быть скомпилирован в библиотеку DLL (а не на исполняемый объект). `/out`Флаг задает имя результирующей сборки.

> [!NOTE]
> Вместо компиляции `GetProductsWithPriceGreaterThan.vb` файла класса из командной строки можно также использовать [Visual Basic Express Edition](https://msdn.microsoft.com/vstudio/express/vb/) или создать отдельный проект библиотеки классов в выпуске Visual Studio Standard Edition. S REN Джейкоб Лауритсен предоставляет такой проект Visual Basic Express Edition с кодом для `GetProductsWithPriceGreaterThan` хранимой процедуры и двумя управляемыми хранимыми процедурами и UDF, созданными в шагах 3, 5 и 10. Проект REN s также включает команды T-SQL, необходимые для добавления соответствующих объектов базы данных.

В коде, скомпилированном в сборку, мы готовы зарегистрировать сборку в базе данных SQL Server 2005. Это можно выполнить с помощью команды T-SQL, используя команду `CREATE ASSEMBLY` или SQL Server Management Studio. Давайте рассмотрим использование Management Studio.

В Management Studio разверните папку Программирование в базе данных Northwind. Одна из его вложенных папок — сборки. Чтобы вручную добавить новую сборку в базу данных, щелкните правой кнопкой мыши папку сборки и выберите в контекстном меню пункт Создать сборку. Откроется диалоговое окно Новая сборка (см. рис. 30). Нажмите кнопку Обзор, выберите `ManuallyCreatedDBObjects.dll` только что скомпилированную сборку и нажмите кнопку ОК, чтобы добавить сборку в базу данных. Сборка не должна отображаться `ManuallyCreatedDBObjects.dll` в обозревателе объектов.

[![Добавление ManuallyCreatedDBObjects.dll сборки в базу данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**Рис. 30**. добавление `ManuallyCreatedDBObjects.dll` сборки в базу данных ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png))

![ManuallyCreatedDBObjects.dll отображается в обозревателе объектов.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**Рис. 31**. отображается `ManuallyCreatedDBObjects.dll` в обозревателе объектов

Хотя мы добавили сборку в базу данных Northwind, мы еще не связываем хранимую процедуру с `GetProductsWithPriceGreaterThan` методом в сборке. Для этого откройте новое окно запроса и выполните следующий скрипт:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

При этом создается новая хранимая процедура в базе данных Northwind с именем, которая `GetProductsWithPriceGreaterThan` связывается с управляемым методом `GetProductsWithPriceGreaterThan` (который находится в классе `StoredProcedures` , который находится в сборке `ManuallyCreatedDBObjects` ).

После выполнения приведенного выше скрипта обновите папку хранимых процедур в обозревателе объектов. Вы должны увидеть новую запись хранимой процедуры `GetProductsWithPriceGreaterThan` , у которой рядом с ней находится значок замка. Чтобы протестировать эту хранимую процедуру, введите и выполните следующий скрипт в окне запроса:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

Как показано на рисунке 32, приведенная выше команда отображает сведения о продуктах с более `UnitPrice` чем $24,95.

[![ManuallyCreatedDBObjects.dll отображается в обозревателе объектов.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**Рис. 32**. `ManuallyCreatedDBObjects.dll` список отображается в обозревателе объектов ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png))

## <a name="summary"></a>Сводка

Microsoft SQL Server 2005 обеспечивает интеграцию со средой CLR, которая позволяет создавать объекты базы данных с помощью управляемого кода. Ранее эти объекты базы данных могли быть созданы только с помощью T-SQL, но теперь мы можем создавать эти объекты с помощью языков программирования .NET, таких как Visual Basic. В этом руководстве мы создали две управляемые хранимые процедуры и управляемую определяемую пользователем функцию.

Visual Studio s SQL Server тип проекта упрощает создание, компиляцию и развертывание управляемых объектов базы данных. Более того, он предлагает широкие возможности отладки. Однако SQL Server типы проектов доступны только в выпусках Visual Studio Professional и Team Systems. Для тех, кто использует Visual Web Developer или стандартный выпуск Visual Studio, шаги создания, компиляции и развертывания необходимо выполнять вручную, как было показано на шаге 13.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Преимущества и недостатки определяемых пользователем функций](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Создание объектов SQL Server 2005 в управляемом коде](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Создание триггеров с помощью управляемого кода в SQL Server 2005](http://www.15seconds.com/issue/041006.htm)
- [Инструкции. Создание и запуск хранимой процедуры CLR SQL Server](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Как создать и запустить определяемую пользователем функцию CLR SQL Server](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Инструкции. изменение `Test.sql` скрипта для запуска объектов SQL](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Введение в определяемые пользователем функции](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Управляемый код и SQL Server 2005 (видео)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Справочник по Transact-SQL](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [Пошаговое руководство. Создание хранимой процедуры в управляемом коде](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалистом по интересу для этого учебника был режим REN Джейкоб Лауритсен. Помимо просмотра этой статьи, REN также создал проект Visual C# Express Edition, который входит в эту статью, чтобы вручную скомпилировать управляемые объекты базы данных. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, удалите строку в [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](debugging-stored-procedures-vb.md)
