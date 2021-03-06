---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
title: Перенос изменений базы данных в рамках транзакцииC#() | Документация Майкрософт
author: rick-anderson
description: Этот учебник является первым из четырех, в котором рассматривается обновление, удаление и вставка пакетов данных. В этом учебнике мы рассмотрим, как разрешаются транзакции базы данных...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: b45fede3-c53a-4ea1-824b-20200808dbae
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
msc.type: authoredcontent
ms.openlocfilehash: da69e466a5b506b869dc8fc0624f3e6a479199a8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489300"
---
# <a name="wrapping-database-modifications-within-a-transaction-c"></a>Перенос изменений базы данных в транзакции (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_CS.zip) или [скачать PDF](wrapping-database-modifications-within-a-transaction-cs/_static/datatutorial63cs1.pdf)

> Этот учебник является первым из четырех, в котором рассматривается обновление, удаление и вставка пакетов данных. В этом учебнике мы рассмотрим, как транзакции базы данных позволяют выполнять пакетные изменения в рамках атомарной операции, что гарантирует успешное завершение всех шагов или выполнение всех шагов.

## <a name="introduction"></a>Введение

Как мы видели в [обзоре руководства по вставке, обновлению и удалению данных](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) , GridView предоставляет встроенную поддержку редактирования и удаления на уровне строк. С помощью нескольких щелчков мыши можно создать обширный интерфейс изменения данных без написания строки кода, если вы используете редактирование и удаление для отдельных строк. Однако в некоторых сценариях это недостаточно, и необходимо предоставить пользователям возможность изменять или удалять пакет записей.

Например, большинство веб-клиентов электронной почты используют сетку для перечисления каждого сообщения, где каждая строка содержит флажок вместе с информацией электронной почты (тема, отправитель и т. д.). Этот интерфейс позволяет пользователю удалить несколько сообщений, установив их, а затем нажав кнопку Удалить выбранные сообщения. Интерфейс редактирования пакетной службы идеально подходит в ситуациях, когда пользователи часто редактируют множество различных записей. Вместо того чтобы принудительно изменять пользователь, внести изменения, а затем нажать кнопку Обновить для каждой записи, которую необходимо изменить, интерфейс редактирования пакетной службы отображает каждую строку с помощью интерфейса правки. Пользователь может быстро изменить набор строк, которые необходимо изменить, а затем сохранить эти изменения, нажав кнопку Обновить все. В этом наборе руководств мы рассмотрим создание интерфейсов для вставки, изменения и удаления пакетов данных.

При выполнении пакетных операций важно определить, возможно ли успешное выполнение некоторых операций в пакете, в то время как другие завершаются сбоем. Рассмотрим пакетное удаление интерфейса. что должно произойти, если первая выбранная запись успешно удалена, а вторая — нет, скажем, из-за нарушения ограничения внешнего ключа? Следует ли выполнить откат первой записи, а также допустимость удаления первой записи?

Если необходимо, чтобы Пакетная операция считалась [атомарной операцией](http://en.wikipedia.org/wiki/Atomic_operation), в которой либо все шаги выполнены успешно, либо все шаги завершаются ошибкой, уровень доступа к данным должен быть дополнен к включению поддержки [транзакций базы данных](http://en.wikipedia.org/wiki/Database_transaction). Транзакции базы данных гарантируют атомарность для набора инструкций `INSERT`, `UPDATE`и `DELETE`, выполняемых по отношению к транзакции, и являются функцией, поддерживаемой большинством современных систем баз данных.

В этом учебнике мы рассмотрим, как расширить DAL для использования транзакций базы данных. В последующих руководствах рассматривается реализация веб-страниц для пакетной вставки, обновления и удаления интерфейсов. Давайте приступим к работе!

> [!NOTE]
> При изменении данных в пакетной транзакции атомарность не всегда требуется. В некоторых сценариях может быть приемлемым, что некоторые изменения данных будут успешными, и другие в том же пакете завершатся ошибкой, например при удалении набора сообщений электронной почты из Интернет-клиента. Если в процессе удаления произошла ошибка базы данных, вероятно, это приемлемо, что записи, обработанные без ошибок, остаются неизменными. В таких случаях DAL не требуется изменять для поддержки транзакций базы данных. Однако существуют и другие сценарии пакетной операции, где атомарность крайне важна. Когда клиент перемещает свои фонды с одного банковского счета на другой, необходимо выполнить две операции: фонды должны вычитаться из первой учетной записи, а затем добавляться во вторую. В то время как банк может не забывать о том, что первый этап выполнен успешно, но второй шаг не пройден, его клиенты хорошо обеспокоен. Я рекомендую работать с этим руководством и реализовать усовершенствования DAL для поддержки транзакций базы данных, даже если вы не планируете использовать их в пакетной службе вставки, обновления и удаления, которые будут создаваться в следующих трех руководствах.

## <a name="an-overview-of-transactions"></a>Общие сведения о транзакциях

В большинстве баз данных предусмотрена поддержка *транзакций*, что позволяет объединять несколько команд базы данных в одну логическую единицу работы. Команды базы данных, составляющие транзакцию, гарантированно будут атомарными, то есть все команды завершатся сбоем или будут успешными.

Как правило, транзакции реализуются с помощью инструкций SQL в следующем шаблоне:

1. Указывает на начало транзакции.
2. Выполните инструкции SQL, составляющие транзакцию.
3. При возникновении ошибки в одной из инструкций, выполненных на шаге 2, необходимо выполнить откат транзакции.
4. Если все инструкции, выполненные на шаге 2, завершаются без ошибок, зафиксируйте транзакцию.

Инструкции SQL, используемые для создания, фиксации и отката транзакции, можно указать вручную при написании скриптов SQL или при создании хранимых процедур или с помощью программных средств, используя ADO.NET или классы в [пространстве имен`System.Transactions`](https://msdn.microsoft.com/library/system.transactions.aspx). В этом учебнике мы будем анализировать только управление транзакциями с помощью ADO.NET. В следующем учебном курсе мы рассмотрим, как использовать хранимые процедуры на уровне доступа к данным, после чего будут рассмотрены инструкции SQL для создания, отката и фиксации транзакций. В то же время изучите [Управление транзакциями в SQL Server хранимых процедурах](http://www.4guysfromrolla.com/webtech/080305-1.shtml) для получения дополнительных сведений.

> [!NOTE]
> [Класс`TransactionScope`](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx) в пространстве имен `System.Transactions` позволяет разработчикам программно переносить ряд инструкций в области транзакции и включает поддержку сложных транзакций, включающих несколько источников, таких как базы данных и даже разнородные типы хранилищ данных, такие как Microsoft SQL Server база, база данных Oracle и веб-служба. Я решил использовать ADO.NET транзакции для работы с этим руководством, а не класс `TransactionScope`, так как ADO.NET более специфичен для транзакций базы данных и, во многих случаях, намного менее интенсивно использует ресурсы. Кроме того, в некоторых сценариях `TransactionScope` класс использует координатор распределенных транзакций Майкрософт (MSDTC). Проблемы с конфигурацией, реализацией и производительностью, связанные с MSDTC, делают его довольно специализированным и дополнительным разделом, кроме области действия этих учебников.

При работе с поставщиком SqlClient в ADO.NET транзакции инициируются посредством вызова [метода`BeginTransaction`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx) [класса`SqlConnection`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) , который возвращает [объект`SqlTransaction`](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx). Инструкции изменения данных, описывающего транзакцию, помещаются в блок `try...catch`. Если ошибка возникает в инструкции в блоке `try`, выполнение передается в блок `catch`, где можно выполнить откат транзакции с помощью [метода`Rollback`](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)`SqlTransaction` Object s. Если все инструкции успешно завершены, вызов метода `SqlTransaction` Object s [`Commit`](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx) в конце блока `try` фиксирует транзакцию. Этот шаблон показан в следующем фрагменте кода. Дополнительные сведения о синтаксисе и примеры использования транзакций с ADO.NET см. [в разделе поддержание согласованности базы данных с транзакциями](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx) .

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample1.cs)]

По умолчанию адаптеры таблиц в типизированном наборе данных не используют транзакции. Чтобы обеспечить поддержку транзакций, необходимо дополнить классы TableAdapter, чтобы включить дополнительные методы, использующие приведенный выше шаблон для выполнения ряда инструкций изменения данных в области транзакции. На этапе 2 мы посмотрим, как использовать разделяемые классы для добавления этих методов.

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>Шаг 1. Создание работы с пакетными веб-страницами данных

Прежде чем приступить к изучению способов расширения DAL для поддержки транзакций базы данных, давайте сначала создадим веб-страницы ASP.NET, которые понадобятся для работы с этим руководством, и три следующих. Начните с добавления новой папки с именем `BatchData`, а затем добавьте следующие страницы ASP.NET, связав каждую страницу с главной страницей `Site.master`.

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![Добавление страниц ASP.NET для учебников, связанных с SqlDataSource](wrapping-database-modifications-within-a-transaction-cs/_static/image1.gif)

**Рис. 1**. добавление страниц ASP.NET для учебников, связанных с SqlDataSource

Как и в других папках, `Default.aspx` будет использовать пользовательский элемент управления `SectionLevelTutorialListing.ascx` для составления списка руководств в своем разделе. Таким образом, добавьте этот пользовательский элемент управления в `Default.aspx`, перетащив его из обозреватель решений на страницу s представление конструирования.

[![добавить пользовательский элемент управления SectionLevelTutorialListing. ascx в Default. aspx](wrapping-database-modifications-within-a-transaction-cs/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image1.png)

**Рис. 2**. Добавление пользовательского элемента управления `SectionLevelTutorialListing.ascx` в `Default.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image2.png))

Наконец, добавьте эти четыре страницы в качестве записей в файл `Web.sitemap`. В частности, добавьте следующую разметку после настройки схемы узла `<siteMapNode>`.

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample2.xml)]

После обновления `Web.sitemap`просмотрите веб-сайт учебников в браузере. В меню слева теперь содержатся элементы для работы с учебниками по пакетным данным.

![Схема узла теперь включает в себя записи для работы с пакетными учебниками по работе с данными](wrapping-database-modifications-within-a-transaction-cs/_static/image3.gif)

**Рис. 3**. схема узла теперь включает в себя записи для работы с пакетными учебниками по работе с данными

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>Шаг 2. обновление уровня доступа к данным для поддержки транзакций базы данных

Как мы обсуждали в первом учебном курсе, [Создание уровня доступа к данным](../introduction/creating-a-data-access-layer-cs.md), типизированный набор данных в нашем DAL состоит из таблиц DataTable и TableAdapter. Таблицы данных содержат данные, а адаптеры таблиц предоставляют функции для чтения данных из базы данных в таблицы DataTable, обновления базы данных с изменениями, внесенными в таблицы DataTable, и т. д. Вспомним, что адаптеры таблиц предоставляют два шаблона для обновления данных, которые я называть пакетным обновлением и прямой базой данных. При использовании шаблона обновления пакетной службы TableAdapter передается набор данных, DataTable или коллекция Rows. Эти данные перечисляются и для каждой вставленной, измененной или удаленной строки выполняется `InsertCommand`, `UpdateCommand`или `DeleteCommand`. При использовании непосредственного шаблона DB TableAdapter передает значения столбцов, необходимых для вставки, обновления или удаления одной записи. Затем метод прямого шаблона базы данных использует переданные значения для выполнения соответствующего оператора `InsertCommand`, `UpdateCommand`или `DeleteCommand`.

Независимо от используемого шаблона обновления, автоматически создаваемые методы TableAdapter не используют транзакции. По умолчанию каждая операция вставки, обновления или удаления, выполняемая адаптером таблицы, обрабатывается как единое дискретное действие. Например, представьте, что непосредственный шаблон DB используется в коде BLL для вставки десяти записей в базу данных. Этот код вызовет метод `Insert` TableAdapter 10 раз. Если первые пять вставок успешны, но шестой из них привела к исключению, первые пять вставленных записей останутся в базе данных. Аналогично, если шаблон пакетного обновления используется для выполнения операций вставки, обновления и удаления для вставленных, измененных и удаленных строк в таблице данных DataTable, если первые несколько изменений были выполнены удачно, а в более поздней — произошла ошибка, эти предыдущие изменения завершено останется в базе данных.

В некоторых сценариях мы хотим обеспечить атомарность в ряде изменений. Для этого необходимо вручную расширить TableAdapter, добавив новые методы, которые выполняют `InsertCommand`, `UpdateCommand`и `DeleteCommand` s под символом-точкой транзакции. При [создании уровня доступа к данным](../introduction/creating-a-data-access-layer-cs.md) мы рассматривали использование [разделяемых классов](http://en.wikipedia.org/wiki/Partial_type) для расширения функциональных возможностей DataTables в типизированном наборе данных. Этот метод также можно использовать с адаптерами таблиц.

Типизированный набор данных `Northwind.xsd` расположен в папке `App_Code` Folders `DAL`. Создайте вложенную папку в папке `DAL` с именем `TransactionSupport` и добавьте новый файл класса с именем `ProductsTableAdapter.TransactionSupport.cs` (см. рис. 4). Этот файл будет содержать частичную реализацию `ProductsTableAdapter`, включающую методы для выполнения изменений данных с помощью транзакции.

![Добавьте папку с именем Трансактионсуппорт и файл класса с именем ProductsTableAdapter.TransactionSupport.cs](wrapping-database-modifications-within-a-transaction-cs/_static/image4.gif)

**Рис. 4**. Добавление папки с именем `TransactionSupport` и файла класса с именем `ProductsTableAdapter.TransactionSupport.cs`

Введите следующий код в файл `ProductsTableAdapter.TransactionSupport.cs`:

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample3.cs)]

Ключевое слово `partial` в объявлении класса указывает компилятору, что члены, добавленные в, должны быть добавлены в класс `ProductsTableAdapter` в пространстве имен `NorthwindTableAdapters`. Обратите внимание на оператор `using System.Data.SqlClient` в верхней части файла. Так как TableAdapter настроен для использования поставщика SqlClient, внутренне он использует объект [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx) , чтобы выдать свои команды в базу данных. Следовательно, необходимо использовать класс `SqlTransaction`, чтобы начать транзакцию, а затем зафиксировать ее или выполнить ее откат. Если используется хранилище данных, отличное от Microsoft SQL Server, необходимо использовать соответствующий поставщик.

Эти методы предоставляют стандартные блоки, необходимые для запуска, отката и фиксации транзакции. Они помечены `public`, что позволяет использовать их из `ProductsTableAdapter`, из другого класса в DAL или из другого слоя в архитектуре, например BLL. `BeginTransaction` открывает внутренние `SqlConnection` TableAdapter (при необходимости), начинает транзакцию и назначает ее свойству `Transaction` и присоединяет транзакцию к внутренним `SqlCommand` объектам `SqlDataAdapter` s. Прежде чем закрывать внутренний объект `Rollback`, `CommitTransaction` и `RollbackTransaction` вызывают `Transaction` объектов `Commit` и `Connection` соответственно.

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>Шаг 3. Добавление методов для обновления и удаления данных по символу-отчасти транзакции

После выполнения этих методов мы повторно готовы к добавлению методов к `ProductsDataTable` или BLL, выполняющему ряд команд под символом-отработкой транзакции. Следующий метод использует шаблон пакетного обновления для обновления `ProductsDataTable` экземпляра с помощью транзакции. Он запускает транзакцию, вызывая метод `BeginTransaction`, а затем использует блок `try...catch` для выполнения инструкций изменения данных. Если вызов метода `Update` `Adapter` Objects приводит к возникновению исключения, выполнение передается в блок `catch`, где будет выполнен откат транзакции, а исключение повторно выбрасывается. Помните, что метод `Update` реализует шаблон пакетного обновления, перечисляя строки предоставленного `ProductsDataTable` и выполняя необходимые `InsertCommand`, `UpdateCommand`и `DeleteCommand` s. Если какая-либо из этих команд приводит к ошибке, выполняется откат транзакции с отменой предыдущих изменений, внесенных в течение времени существования транзакции. Если инструкция `Update` завершена без ошибок, транзакция фиксируется полностью.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample4.cs)]

Добавьте метод `UpdateWithTransaction` в класс `ProductsTableAdapter` с помощью разделяемого класса в `ProductsTableAdapter.TransactionSupport.cs`. Кроме того, этот метод можно добавить в класс `ProductsBLL` уровня бизнес-логики с небольшими синтаксическими изменениями. А именно ключевое слово this в `this.BeginTransaction()`, `this.CommitTransaction()`и `this.RollbackTransaction()` необходимо заменить на `Adapter` (Помните, что `Adapter` — это имя свойства в `ProductsBLL` типа `ProductsTableAdapter`).

В методе `UpdateWithTransaction` используется шаблон пакетного обновления, но в области транзакции можно также использовать ряд прямых вызовов DB, как показано в следующем методе. Метод `DeleteProductsWithTransaction` принимает в качестве входных данных `List<T>` типа `int`, который `ProductID` для удаления. Метод инициирует транзакцию с помощью вызова `BeginTransaction`, а затем в блоке `try` проходит по переданному списку, вызывая метод `Delete` прямого шаблона DB для каждого значения `ProductID`. При сбое любого вызова `Delete` управление передается блоку `catch`, в котором выполняется откат транзакции, и исключение создается повторно. Если все вызовы `Delete` успешно выполнены, транзакция фиксируется. Добавьте этот метод в класс `ProductsBLL`.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample5.cs)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>Применение транзакций для нескольких адаптеров таблиц

Код, связанный с транзакцией, в этом учебнике позволяет обрабатывать несколько инструкций в `ProductsTableAdapter` как атомарная операция. Но что делать, если несколько изменений в разных таблицах базы данных должны выполняться атомарно? Например, при удалении категории мы могли бы сначала переназначить ее текущие продукты другой категории. Эти два действия переназначения продуктов и удаление категории должны выполняться как атомарная операция. Однако `ProductsTableAdapter` включает только методы для изменения таблицы `Products` и `CategoriesTableAdapter` включает только методы изменения таблицы `Categories`. Итак, как транзакция может охватывать оба адаптера таблиц?

Один из вариантов — добавить метод в `CategoriesTableAdapter` с именем `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` и использовать этот метод для вызова хранимой процедуры, которая переназначает продукты и удаляет категорию в области транзакции, определенной в хранимой процедуре. В следующем учебном курсе мы рассмотрим, как начать, зафиксировать и откатить транзакции в хранимых процедурах.

Другой вариант — создать вспомогательный класс в DAL, который содержит метод `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)`. Этот метод создает экземпляр `CategoriesTableAdapter` и `ProductsTableAdapter`, а затем задает для этих двух адаптеров TableAdapter `Connection` свойства одному и тому же экземпляру `SqlConnection`. На этом этапе один из двух адаптеров таблицы TableAdapter инициирует транзакцию вызовом `BeginTransaction`. Методы TableAdapter для повторного назначения продуктов и удаления категории будут вызываться в блоке `try...catch` с фиксацией или откатом транзакции по мере необходимости.

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>Шаг 4. Добавление метода`UpdateWithTransaction`к слою бизнес-логики

На шаге 3 мы добавили метод `UpdateWithTransaction` в `ProductsTableAdapter` DAL. Необходимо добавить соответствующий метод к BLL. Хотя уровень представления данных может вызывать DAL непосредственно для вызова метода `UpdateWithTransaction`, в этих учебниках было предусмотрено определение многоуровневой архитектуры, которая изолирует слой DAL от уровня представления. Поэтому мы наполнения, что мы будем продолжать этот подход.

Откройте файл `ProductsBLL` класса и добавьте метод с именем `UpdateWithTransaction`, который просто вызывает соответствующий метод DAL. В `ProductsBLL`необходимо добавить два новых метода: `UpdateWithTransaction`, которые вы только что добавили, и `DeleteProductsWithTransaction`, которые были добавлены на шаге 3.

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample6.cs)]

> [!NOTE]
> Эти методы не включают атрибут `DataObjectMethodAttribute`, назначенный большинству других методов в классе `ProductsBLL`, так как мы будем вызывать эти методы непосредственно из классов кода программной части страниц ASP.NET. Помните, что `DataObjectMethodAttribute` используется для отметки того, какие методы должны отображаться в мастере настройки источников данных ObjectDataSource и на каких вкладках (выбор, обновление, вставка или удаление). Поскольку в GridView отсутствует встроенная поддержка пакетного редактирования или удаления, нам придется вызывать эти методы программно, а не использовать декларативный подход без кода.

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>Шаг 5. атомарное обновление данных из уровня представления данных

Чтобы проиллюстрировать воздействие транзакции на обновление пакета записей, давайте создадим пользовательский интерфейс, перечисляющий все продукты в GridView и включающий веб-элемент управления Button, который при нажатии переназначает продукты `CategoryID` значения. В частности, переназначение категории будет продолжено, чтобы первым нескольким продуктам было присвоено допустимое `CategoryID` значения, в то время как другим пользователям намеренно назначено несуществующее значение `CategoryID`. При попытке обновить базу данных с помощью продукта, `CategoryID` которого не соответствует существующим категориям `CategoryID`, произойдет нарушение ограничения внешнего ключа и будет вызвано исключение. В этом примере мы увидим, что при использовании транзакции исключение, вызванное нарушением ограничения внешнего ключа, приведет к откату предыдущего допустимого `CategoryID` изменений. Однако если транзакция не используется, изменения в исходных категориях останутся прежними.

Для начала откройте страницу `Transactions.aspx` в папке `BatchData` и перетащите элемент управления GridView с панели инструментов в конструктор. Задайте для его `ID` значение `Products` и, из своего смарт-тега, привяжите его к новому ObjectDataSource с именем `ProductsDataSource`. Настройте ObjectDataSource для извлечения данных из `GetProducts` метода `ProductsBLL` классов. Это будет элемент управления GridView, предназначенный только для чтения, поэтому установите в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет) и нажмите кнопку Готово.

[![рис. 5. Настройка ObjectDataSource для использования метода ProductsBLL класса s](wrapping-database-modifications-within-a-transaction-cs/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image3.png)

**Рис. 5**. рис. 5. Настройка ObjectDataSource для использования метода `ProductsBLL` Class s `GetProducts` ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image4.png))

[![установить в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет)](wrapping-database-modifications-within-a-transaction-cs/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image5.png)

**Рис. 6**. Установка раскрывающихся списков на вкладках «обновить», «вставить» и «удалить» (нет) ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image6.png))

После завершения работы мастера настройки источника данных Visual Studio создаст BoundFields и CheckBoxField для полей данных продукта. Удалите все эти поля, за исключением `ProductID`, `ProductName`, `CategoryID`и `CategoryName` и переименуйте `ProductName` и `CategoryName` свойства BoundFields `HeaderText` на Product и Category соответственно. В смарт-теге установите флажок Включить разбиение на страницы. После внесения этих изменений декларативная разметка GridView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample7.aspx)]

Затем добавьте три веб-элемента управления "Кнопка" над элементом GridView. Задайте для свойства Text в первой кнопке значение обновить сетку, второй — для изменения категорий (с ТРАНЗАКЦИей), а треть — для изменения категорий (без транзакции).

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample8.aspx)]

На этом этапе представление конструирования в Visual Studio должны выглядеть примерно так, как на снимке экрана, показанном на рис. 7.

[![страница содержит элементы управления GridView и три кнопки](wrapping-database-modifications-within-a-transaction-cs/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image7.png)

**Рис. 7**. страница содержит элементы управления GridView и три кнопки ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image8.png))

Создайте обработчики событий для каждой из трех `Click` событий кнопок и используйте следующий код:

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample9.cs)]

Кнопка обновления `Click` обработчик событий просто повторно привязывает данные к GridView, вызвав метод `Products` GridView s `DataBind`.

Второй обработчик событий переназначит продукты `CategoryID` s и использует новый метод транзакции из BLL для обновления базы данных в рамках транзакции. Обратите внимание, что каждый продукт `CategoryID` имеет произвольное значение, равное значению `ProductID`. Это будет прекрасно работать для первых нескольких продуктов, так как эти продукты имеют `ProductID` значения, которые должны быть сопоставлены с допустимыми `CategoryID` s. Но после того, как `ProductID` запустится слишком много, это сокрытие `ProductID` s и `CategoryID` s больше не применяется.

Третий обработчик событий `Click` обновляет продукты `CategoryID` s таким же образом, но отправляет обновление в базу данных с помощью метода `Update` по умолчанию `ProductsTableAdapter` s. Этот метод `Update` не заключает в оболочку ряд команд внутри транзакции, поэтому эти изменения вносятся до первого обнаруженной ошибки нарушения ограничения внешнего ключа.

Чтобы продемонстрировать это поведение, посетите эту страницу в браузере. Сначала должна отобразиться первая страница данных, как показано на рис. 8. Затем нажмите кнопку Изменить категории (с ТРАНЗАКЦИей). Это вызовет обратную передачу и попытается обновить все продукты `CategoryID` значения, но приведет к нарушению ограничения внешнего ключа (см. рис. 9).

[![продукты отображаются в элементе управления GridView с страничным заполнением](wrapping-database-modifications-within-a-transaction-cs/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image9.png)

**Рис. 8**. продукты отображаются в элементе управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image10.png))

[![переназначении категорий приводит к нарушению ограничения внешнего ключа](wrapping-database-modifications-within-a-transaction-cs/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image11.png)

**Рис. 9**. перераспределение категорий приводит к нарушению ограничения внешнего ключа ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image12.png))

Теперь нажмите кнопку "назад" в браузере, а затем щелкните "обновить сетку". После обновления данных вы увидите те же выходные данные, что показаны на рис. 8. То есть несмотря на то, что некоторые продукты `CategoryID` s были изменены на допустимые значения и обновлены в базе данных, они были отменены при нарушении ограничения внешнего ключа.

Теперь попробуйте нажать кнопку Изменить категории (без транзакции). Это приведет к ошибке нарушения ограничения внешнего ключа (см. рис. 9), но на этот раз откат этих продуктов, значения `CategoryID` которых были изменены на допустимое значение, не будет отменено. Нажмите кнопку назад в браузере, а затем кнопку обновить сетку. Как показано на рис. 10, `CategoryID` s первых восьми продуктов были переназначены. Например, на рис. 8 изменено `CategoryID` 1, но на рис. 10 он был переназначен 2.

[![, что значения CategoryID для некоторых продуктов были обновлены, а другие — нет.](wrapping-database-modifications-within-a-transaction-cs/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image13.png)

**Рис. 10**. некоторые продукты `CategoryID` значения были обновлены, а другие — нет ([щелкните, чтобы просмотреть изображение с полным размером](wrapping-database-modifications-within-a-transaction-cs/_static/image14.png))

## <a name="summary"></a>Сводка

По умолчанию методы TableAdapter не заключают выполненные инструкции базы данных в область транзакции, но с небольшой работой мы можем добавить методы, которые будут создавать, фиксировать и откатить транзакцию. В этом руководстве мы создали три таких метода в классе `ProductsTableAdapter`: `BeginTransaction`, `CommitTransaction`и `RollbackTransaction`. Мы увидели, как использовать эти методы вместе с блоком `try...catch`, чтобы сделать ряд инструкций по изменению данных атомарными. В частности, мы создали метод `UpdateWithTransaction` в `ProductsTableAdapter`, который использует шаблон пакетного обновления для внесения необходимых изменений в строки указанного `ProductsDataTable`. Мы также добавили метод `DeleteProductsWithTransaction` в класс `ProductsBLL` в BLL, который принимает в качестве входных данных `List` `ProductID` значений и вызывает метод непосредственных шаблонов DB `Delete` для каждого `ProductID`. Оба метода начинаются с создания транзакции и последующего исполнения инструкций модификации данных в блоке `try...catch`. При возникновении исключения транзакция откатывается, в противном случае она фиксируется.

На шаге 5 показан эффект транзакционных пакетных обновлений и пакетных обновлений, которые не используют транзакцию. В следующих трех руководствах мы создадим основу, описанную в этом руководстве, и создадим пользовательские интерфейсы для выполнения пакетных обновлений, удалений и вставок.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Поддержание согласованности базы данных с транзакциями](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [Управление транзакциями в SQL Server хранимых процедурах](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [Простые транзакции: `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope и адаптеры](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [Использование Oracle Databaseных транзакций в .NET](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства: Дейв Гарднер, Хилтон Гизнау и Терезой Мерфи. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Дальше](batch-updating-cs.md)
