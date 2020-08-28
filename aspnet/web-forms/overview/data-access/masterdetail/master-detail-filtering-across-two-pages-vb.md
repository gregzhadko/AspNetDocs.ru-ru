---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: Фильтрация "основной/подробности" на двух страницах (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы реализуем этот шаблон с помощью элемента управления GridView для перечисления поставщиков в базе данных. Каждая строка поставщика в GridView будет содержать представление...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 0e30d47a565c3b6cb9f647d54d47c10a418762f4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044978"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>Фильтрация "Основной/подробности" на двух страницах (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) или [Загрузка PDF-файла](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> В этом учебнике мы реализуем этот шаблон с помощью элемента управления GridView для перечисления поставщиков в базе данных. Каждая строка поставщика в элементе управления GridView будет содержать ссылку View Products (Просмотр продуктов), при нажатии которой пользователь перейдет на отдельную страницу со списком продуктов для выбранного поставщика.

## <a name="introduction"></a>Введение

В предыдущих двух учебниках мы увидели, как отображать отчеты «основной/подробности» на одной веб-странице с помощью элементов управления DropDownList для отображения «основных» записей и элемента управления [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) или [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) для отображения «сведений». Другой распространенный шаблон, используемый для отчетов «основной/подробности», состоит в том, чтобы иметь основные записи на одной веб-странице и сведения, показанные на другом. Веб-сайт форума, как и [форумы ASP.NET](https://forums.asp.net/), является хорошим примером этого шаблона на практике. Форумы ASP.NET состоят из различных форумов начало работы, веб-форм, элементов управления для представления данных и т. д. Каждый форум состоит из многих потоков, и каждый поток состоит из нескольких записей. На домашней странице форумов ASP.NET представлены форумы. Щелкнув форум, вы перейти на `ShowForum.aspx` страницу, в которой перечислены потоки для этого форума. Аналогичным образом, щелкнув поток, вы переходите к `ShowPost.aspx` , который отображает записи для потока, который был выбран.

В этом учебнике мы реализуем этот шаблон с помощью элемента управления GridView для перечисления поставщиков в базе данных. Каждая строка поставщика в элементе управления GridView будет содержать ссылку View Products (Просмотр продуктов), при нажатии которой пользователь перейдет на отдельную страницу со списком продуктов для выбранного поставщика.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>Шаг 1. добавление `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` страниц и в `Filtering` папку

При определении макета страницы в третьем руководстве мы добавили несколько начальных страниц в `BasicReporting` `Filtering` папки, и `CustomFormatting` . Однако в это время мы не добавили начальную страницу для этого руководства, поэтому необходимо добавить две новые страницы в `Filtering` папку: `SupplierListMaster.aspx` и `ProductsForSupplierDetails.aspx` . `SupplierListMaster.aspx` Выводит список «основных» записей (поставщиков), при этом `ProductsForSupplierDetails.aspx` выводятся продукты для выбранного поставщика.

При создании этих двух новых страниц необходимо связать их с `Site.master` главной страницей.

![Добавление страниц Супплиерлистмастер. aspx и Продуктсфорсупплиердетаилс. aspx в папку фильтрации](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**Рис. 1**. добавление `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` страниц и в `Filtering` папку

Кроме того, при добавлении новых страниц в проект обязательно обновите файл схемы узла `Web.sitemap` соответствующим образом. В этом учебнике просто добавьте `SupplierListMaster.aspx` страницу в карту узла, используя следующее XML-содержимое в качестве дочернего элемента в элементе Filtered Reports `<siteMapNode>` :

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> Вы можете автоматизировать процесс обновления файла схемы узла при добавлении новых страниц ASP.NET с помощью [макроса Map](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx) [. Скотт Аллен](http://odetocode.com/Blogs/scott/)Free Visual Studio.

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>Шаг 2. Отображение списка поставщиков в`SupplierListMaster.aspx`

`SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` Теперь, когда страницы и созданы, наш следующий шаг — создание элемента управления GridView для поставщиков в `SupplierListMaster.aspx` . Добавьте элемент управления GridView на страницу и привяжите его к новому элементу ObjectDataSource. Этот элемент управления ObjectDataSource должен использовать `SuppliersBLL` `GetSuppliers()` метод класса для возврата всех поставщиков.

[![Выберите класс Супплиерсблл](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**Рис. 2**. Выбор `SuppliersBLL` класса ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image4.png))

[![Настройка ObjectDataSource для использования метода-поставщика ()](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**Рис. 3**. Настройка ObjectDataSource для использования `GetSuppliers()` метода ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image7.png))

Необходимо включить ссылку с названием Просмотр продуктов в каждой строке GridView, при нажатии которой пользователь перенесет `ProductsForSupplierDetails.aspx` значение выбранной строки `SupplierID` через строку запроса. Например, если пользователь щелкает ссылку View Products (Просмотр продуктов) для поставщика Токио компании (со `SupplierID` значением 4), они должны быть отправлены в `ProductsForSupplierDetails.aspx?SupplierID=4` .

Для этого добавьте [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) в GridView, который добавляет гиперссылку в каждую строку GridView. Для начала щелкните ссылку Edit Columns (изменить столбцы) в смарт-теге GridView. Затем выберите HyperLinkField из списка в левом верхнем углу и нажмите кнопку Добавить, чтобы включить HyperLinkField в список полей GridView.

[![Добавление HyperLinkField в GridView](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**Рис. 4**. Добавление элемента HyperLinkField в элемент управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image10.png))

HyperLinkField может быть настроен на использование одинаковых значений текста или URL-адресов ссылкой в каждой строке GridView или может основывать эти значения на значениях данных, привязанных к каждой конкретной строке. Чтобы задать статическое значение во всех строках, используйте `Text` свойства или HyperLinkField `NavigateUrl` . Поскольку текст ссылки должен быть одинаковым для всех строк, установите `Text` свойство HyperLinkField для просмотра продуктов.

[![Задание свойства Text HyperLinkField для просмотра продуктов](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**Рис. 5**. Задание свойства HyperLinkField `Text` для просмотра продуктов ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image13.png))

Чтобы задать значения текста или URL-адреса, основанные на базовых данных, привязанных к строке GridView, укажите поля данных, из которых должны быть извлечены значения текста или URL-адреса в `DataTextField` `DataNavigateUrlFields` свойствах или. `DataTextField` можно задать только одно поле данных. `DataNavigateUrlFields`однако можно задать разделенный запятыми список полей данных. Часто требуется, чтобы текст или URL-адрес был основан на комбинации значения поля данных текущей строки и некоторой статической разметки. В этом руководстве, например, нам нужен URL-адрес ссылок HyperLinkField `ProductsForSupplierDetails.aspx?SupplierID=supplierID` , где *`supplierID`* — это значение ров'с для каждого элемента GridView `SupplierID` . Обратите внимание, что нам нужны как статические, так и управляемые данными значения: `ProductsForSupplierDetails.aspx?SupplierID=` часть URL-адреса ссылки является статической, а *`supplierID`* часть — управляемой данными, так как ее значение является собственным значением каждой строки `SupplierID` .

Чтобы указать сочетание статических и управляемых данными значений, используйте `DataTextFormatString` `DataNavigateUrlFormatString` Свойства и. В этих свойствах при необходимости введите статическую разметку, а затем используйте маркер, в `{0}` котором должно отображаться значение поля, указанного в `DataTextField` `DataNavigateUrlFields` свойствах или. Если в `DataNavigateUrlFields` свойстве указано несколько полей `{0}` , используйте место, где должно быть вставлено первое поле, `{1}` для значения второго поля и т. д.

Применяя этот способ к нашему руководству, нам нужно задать `DataNavigateUrlFields` для свойства `SupplierID` значение, поскольку это поле данных, для которого необходимо настроить значения для каждой строки, а `DataNavigateUrlFormatString` свойство — в `ProductsForSupplierDetails.aspx?SupplierID={0}` .

[![Настройка HyperLinkField для включения правильного URL-адреса ссылки на основе поля "КодПоставщика"](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**Рис. 6**. Настройка HyperLinkField для включения правильного URL-адреса ссылки на основе `SupplierID` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image16.png))

После добавления HyperLinkField вы можете настроить и изменить порядок полей GridView. Следующая разметка показывает GridView после внесения некоторых незначительных настроек уровня поля.

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

Уделите время просмотру страницы в `SupplierListMaster.aspx` браузере. Как показано на рис. 7, в настоящее время на странице перечислены все поставщики, включая ссылку «Просмотр продуктов». Щелкнув ссылку Просмотреть продукты, вы перейдете по ссылке `ProductsForSupplierDetails.aspx` поставщика `SupplierID` в строке запроса.

[![Каждая строка «поставщик» содержит ссылку «Просмотр продуктов»](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**Рис. 7**. Каждая строка «поставщик» содержит ссылку «Просмотр продуктов» ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image19.png)).

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>Шаг 3. Перечисление продуктов поставщика в`ProductsForSupplierDetails.aspx`

На этом этапе `SupplierListMaster.aspx` страница отправляет пользователей в `ProductsForSupplierDetails.aspx` , передавая выбранного поставщика `SupplierID` в строку запроса. Заключительный этап учебника — отображение продуктов в элементе управления GridView, `ProductsForSupplierDetails.aspx` где `SupplierID` равно `SupplierID` переданному через строку запроса. Для этого добавьте GridView на `ProductsForSupplierDetails.aspx` страницу, используя новый элемент управления ObjectDataSource с именем `ProductsBySupplierDataSource` , который вызывает `GetProductsBySupplierID(supplierID)` метод из `ProductsBLL` класса.

[![Добавить новый элемент управления ObjectDataSource с именем Продуктсбисупплиердатасаурце](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**Рис. 8**. Добавление нового элемента управления ObjectDataSource `ProductsBySupplierDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image22.png))

[![Выберите класс ProductsBLL](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**Рис. 9**. Выбор `ProductsBLL` класса ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image25.png))

[![Вызов ObjectDataSource вызова метода Жетпродуктсбисупплиерид (КодПоставщика)](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**Рис. 10**. вызов `GetProductsBySupplierID(supplierID)` метода ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image28.png))

На последнем шаге мастера настройки источника данных предлагается указать источник `GetProductsBySupplierID(supplierID)` *`supplierID`* параметра метода. Чтобы использовать значение строки запроса, задайте для свойства Источник параметра значение QueryString и введите имя значения QueryString, которое будет использоваться в текстовом поле QueryStringField ( `SupplierID` ).

[![Заполнить значение параметра "КодПоставщика" из значения строки "КодПоставщика"](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**Рис. 11**. Заполнение *`supplierID`* значения параметра из `SupplierID` значения строки запроса ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image31.png))

Вот и все! На рис. 12 показана `ProductsForSupplierDetails.aspx` страница при посещении щелчком по ссылке Токио Traders FROM `SupplierListMaster.aspx` .

[![Показаны продукты, предоставляемые в Токио Traders.](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**Рис. 12**. отображаются продукты, предоставленные в компании Токио ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image34.png)).

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>Отображение сведений о поставщиках в`ProductsForSupplierDetails.aspx`

Как показано на рис. 12, на `ProductsForSupplierDetails.aspx` странице просто перечислены продукты, предоставляемые `SupplierID` указанным в строке запроса. Тем не менее, кто-то посылает на эту страницу напрямую, не знает, что на рис. 12 показаны продукты в Токио. Чтобы устранить эту проблему, можно также отобразить сведения о поставщике на этой странице.

Начните с добавления элемента управления FormView над элементом GridView продуктов. Создайте новый элемент управления ObjectDataSource с именем `SuppliersDataSource` , который вызывает `SuppliersBLL` метод класса `GetSupplierBySupplierID(supplierID)` .

[![Выберите класс Супплиерсблл](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**Рис. 13**. Выбор `SuppliersBLL` класса ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image37.png))

[![Вызов ObjectDataSource вызова метода Жетсупплиербисупплиерид (КодПоставщика)](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**Рис. 14**. вызов `GetSupplierBySupplierID(supplierID)` метода ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image40.png))

Как и в `ProductsBySupplierDataSource` , *`supplierID`* параметру необходимо присвоить значение `SupplierID` строки запроса.

[![Заполнить значение параметра "КодПоставщика" из значения строки "КодПоставщика"](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**Рис. 15**. Заполнение *`supplierID`* значения параметра из `SupplierID` значения строки запроса ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image43.png))

При привязке FormView к ObjectDataSource в представление конструирования Visual Studio автоматически создает `ItemTemplate` `InsertItemTemplate` `EditItemTemplate` элементы управления, и с метками и TextBox для каждого поля данных, возвращаемого ObjectDataSource. Так как мы просто хотим отобразить сведения о поставщиках, вы можете удалить `InsertItemTemplate` и `EditItemTemplate` . Затем измените ItemTemplate так, чтобы в нем отображалось название компании поставщика в `<h3>` элементе и адрес, город, страна и номер телефона под названием компании. Кроме того, можно вручную задать FormView `DataSourceID` и создать `ItemTemplate` разметку, как это было сделано в учебнике «[Отображение данных с помощью ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)».

После этих изменений декларативная разметка FormView должна выглядеть следующим образом:

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

На рис. 16 показан снимок экрана `ProductsForSupplierDetails.aspx` страницы после включения подробных сведений о поставщике.

[![Список продуктов содержит сводку о поставщике](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**Рис. 16**. список продуктов содержит сводку о поставщике ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image46.png))

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>Применение заключительных отприкосновений к `ProductsForSupplierDetails.aspx` пользовательскому интерфейсу

Чтобы улучшить взаимодействие с пользователем для этого отчета, необходимо внести несколько дополнений на `ProductsForSupplierDetails.aspx` страницу. В настоящее время пользователь может перейти со `ProductsForSupplierDetails.aspx` страницы назад к списку поставщиков, щелкнув кнопку назад в браузере. Давайте добавим на страницу элемент управления HyperLink, `ProductsForSupplierDetails.aspx` который обратно связывается с `SupplierListMaster.aspx` , предоставляя другой способ возврата пользователю в главный список.

[![Добавление элемента управления HyperLink для возврата пользователя к Супплиерлистмастер. aspx](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**Рис. 17**. Добавление элемента управления HyperLink для возврата пользователю `SupplierListMaster.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image49.png))

Если пользователь щелкнет ссылку View Products (Просмотр продуктов) для поставщика, у которого нет продуктов, то `ProductsBySupplierDataSource` ObjectDataSource в `ProductsForSupplierDetails.aspx` не вернет никаких результатов. Элемент управления GridView, привязанный к ObjectDataSource, не будет обрабатывать разметку, что приводит к пустой области на странице в браузере пользователя. Чтобы более четко взаимодействовать с пользователем, что нет продуктов, связанных с выбранным поставщиком, мы можем задать `EmptyDataText` для свойства GridView сообщение, которое должно отображаться при возникновении такой ситуации. Я установил для этого свойства значение "отсутствуют продукты, предоставленные этим поставщиком".

По умолчанию все поставщики в базе данных Northwind содержат по крайней мере один продукт. Однако в этом руководстве я вручную изменил `Products` таблицу, чтобы поставщик Escargots Nouveaux больше не был связан с какими-либо продуктами. На рис. 18 показана страница сведений для Escargots Nouveaux после внесения этого изменения.

[![Пользователи сообщают о том, что поставщик не предоставляет продукты](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**Рис. 18**. пользователи сообщают о том, что поставщик не предоставляет какие-либо продукты ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-vb/_static/image52.png))

## <a name="summary"></a>Сводка

В то время как отчеты «основной/подробности» могут отображать как основные, так и подробные записи на одной странице, во многих веб-сайтах они разделяются на две веб-страницы. В этом учебнике мы рассмотрели, как реализовать такой отчет «основной/подробности», применяя поставщиков, перечисленных в элементе управления GridView на главной веб-странице, и связанных продуктов, перечисленных на странице «сведения». Каждая строка поставщика на главной веб-странице содержала ссылку на страницу сведений, переданную по `SupplierID` значению строки. Такие ссылки, относящиеся к строкам, можно легко добавить с помощью HyperLinkField GridView.

На странице сведений получение этих продуктов для указанного поставщика была выполнена путем вызова `ProductsBLL` `GetProductsBySupplierID(supplierID)` метода класса. *`supplierID`* Значение параметра было указано декларативно с помощью строки запроса в качестве источника параметра. Мы также рассмотрели, как отобразить сведения о поставщике на странице сведений с помощью FormView.

[Следующий учебник](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) является последним в отчетах «основной/подробности». Мы рассмотрим, как отобразить список продуктов в элементе управления GridView, где у каждой строки есть кнопка выбора. Если нажать кнопку Выбрать, сведения о продукте будут отображаться в элементе управления DetailsView на той же странице.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, удалите строку в [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-filtering-with-two-dropdownlists-vb.md)
> [Вперед](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
