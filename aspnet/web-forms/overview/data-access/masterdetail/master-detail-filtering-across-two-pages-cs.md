---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: Фильтрация "основной/подробности" на двухC#страницах () | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы реализуем этот шаблон с помощью элемента управления GridView для перечисления поставщиков в базе данных. Каждая строка поставщика в GridView будет содержать представление...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: ccb3bfa5f215ba6e65b8a10b40041d5c2896c7e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424878"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>Фильтрация "Основной/подробности" на двух страницах (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe) или [Загрузка PDF-файла](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> В этом учебнике мы реализуем этот шаблон с помощью элемента управления GridView для перечисления поставщиков в базе данных. Каждая строка поставщика в элементе управления GridView будет содержать ссылку View Products (Просмотр продуктов), при нажатии которой пользователь перейдет на отдельную страницу со списком продуктов для выбранного поставщика.

## <a name="introduction"></a>Введение

В предыдущих двух учебниках мы увидели, как [отображать отчеты «основной/подробности» на одной веб-странице с помощью элементов управления DropDownList](master-detail-filtering-with-a-dropdownlist-cs.md) для [отображения «основных» записей и элемента управления GridView или DetailsView](master-detail-filtering-with-two-dropdownlists-cs.md) для отображения «сведений». Другой распространенный шаблон, используемый для отчетов «основной/подробности», состоит в том, чтобы иметь основные записи на одной веб-странице и сведения, показанные на другом. Веб-сайт форума, как и [форумы ASP.NET](https://forums.asp.net/), является хорошим примером этого шаблона на практике. Форумы ASP.NET состоят из различных форумов начало работы, веб-форм, элементов управления для представления данных и т. д. Каждый форум состоит из многих потоков, и каждый поток состоит из нескольких записей. На домашней странице форумов ASP.NET представлены форумы. Щелкнув форум, вы перейти на страницу `ShowForum.aspx`, в которой перечислены потоки для этого форума. Аналогичным образом, если щелкнуть поток, откроется `ShowPost.aspx`, в котором отображаются записи для потока, который был выбран.

В этом учебнике мы реализуем этот шаблон с помощью элемента управления GridView для перечисления поставщиков в базе данных. Каждая строка поставщика в элементе управления GridView будет содержать ссылку View Products (Просмотр продуктов), при нажатии которой пользователь перейдет на отдельную страницу со списком продуктов для выбранного поставщика.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>Шаг 1. Добавление`SupplierListMaster.aspx`и`ProductsForSupplierDetails.aspx`страниц в папку`Filtering`

При определении макета страницы в третьем руководстве мы добавили ряд "начальных" страниц в `BasicReporting`, `Filtering`и папках `CustomFormatting`. Однако в это время мы не добавили начальную страницу для этого руководства, поэтому необходимо добавить две новые страницы в папку `Filtering`: `SupplierListMaster.aspx` и `ProductsForSupplierDetails.aspx`. в `SupplierListMaster.aspx` будут перечислены «главные» записи (поставщики), тогда как `ProductsForSupplierDetails.aspx` будут отображать продукты для выбранного поставщика.

При создании этих двух новых страниц необходимо связать их с главной страницей `Site.master`.

![Добавление страниц Супплиерлистмастер. aspx и Продуктсфорсупплиердетаилс. aspx в папку фильтрации](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**Рис. 1**. Добавление `SupplierListMaster.aspx` и `ProductsForSupplierDetails.aspx` страниц в папку `Filtering`

Кроме того, при добавлении новых страниц в проект обязательно обновите файл схемы узла, `Web.sitemap`соответствующим образом. Для работы с этим руководством просто добавьте страницу `SupplierListMaster.aspx` на карту узла, используя следующее XML-содержимое в качестве дочернего элемента в элементе Filtering Reports `<siteMapNode>`.

[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> Вы можете автоматизировать процесс обновления файла схемы узла при добавлении новых страниц ASP.NET с помощью [макроса Map](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx) [. Скотт Аллен](http://odetocode.com/Blogs/scott/)Free Visual Studio.

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>Шаг 2. Отображение списка поставщиков в`SupplierListMaster.aspx`

После создания страниц `SupplierListMaster.aspx` и `ProductsForSupplierDetails.aspx` наш следующий шаг — создание элемента управления GridView для поставщиков в `SupplierListMaster.aspx`. Добавьте элемент управления GridView на страницу и привяжите его к новому элементу ObjectDataSource. Для возврата всех поставщиков этот элемент управления ObjectDataSource должен использовать метод `GetSuppliers()` класса `SuppliersBLL`.

[![выберите класс Супплиерсблл](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**Рис. 2**. выбор класса `SuppliersBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image4.png))

[![настроить ObjectDataSource для использования метода-поставщика ()](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**Рис. 3**. Настройка ObjectDataSource для использования метода `GetSuppliers()` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image7.png))

Необходимо включить ссылку с названием Просмотр продуктов в каждой строке GridView, при нажатии которой пользователь получает `ProductsForSupplierDetails.aspx` передать значение `SupplierID` выбранной строки через строку запроса. Например, если пользователь щелкнет ссылку View Products (Просмотр продуктов) для поставщика Токио (который имеет значение `SupplierID` 4), то его следует отправить на `ProductsForSupplierDetails.aspx?SupplierID=4`.

Для этого добавьте [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) в GridView, который добавляет гиперссылку в каждую строку GridView. Для начала щелкните ссылку Edit Columns (изменить столбцы) в смарт-теге GridView. Затем выберите HyperLinkField из списка в левом верхнем углу и нажмите кнопку Добавить, чтобы включить HyperLinkField в список полей GridView.

[![добавить HyperLinkField в GridView](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**Рис. 4**. Добавление элемента HyperLinkField в элемент управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image10.png))

HyperLinkField может быть настроен на использование одинаковых значений текста или URL-адресов ссылкой в каждой строке GridView или может основывать эти значения на значениях данных, привязанных к каждой конкретной строке. Чтобы указать статическое значение во всех строках, используйте свойства `Text` или `NavigateUrl` HyperLinkField. Поскольку текст ссылки должен быть одинаковым для всех строк, установите свойство `Text` HyperLinkField для просмотра продуктов.

[![задать свойство Text HyperLinkField для просмотра продуктов](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**Рис. 5**. задание свойства `Text` HyperLinkField для просмотра продуктов ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image13.png))

Чтобы задать значения текста или URL-адреса, основанные на базовых данных, привязанных к строке GridView, укажите поля данных, из которых должны быть извлечены значения текста или URL-адреса в свойствах `DataTextField` или `DataNavigateUrlFields`. `DataTextField` можно задать только одно поле данных; Однако `DataNavigateUrlFields`может быть задан разделенный запятыми список полей данных. Часто требуется, чтобы текст или URL-адрес был основан на комбинации значения поля данных текущей строки и некоторой статической разметки. Например, в этом руководстве мы хотим, чтобы URL-адрес HyperLinkField ссылок был `ProductsForSupplierDetails.aspx?SupplierID=supplierID`, где *`supplierID`* — это значение `SupplierID` ров'с GridView. Обратите внимание на то, что нам нужны как статические, так и управляемые данными значения: `ProductsForSupplierDetails.aspx?SupplierID=` часть URL-адреса ссылки является статической, а *`supplierID`* часть — управляемой данными, так как ее значение является значением `SupplierID` каждой строки.

Чтобы указать сочетание статических и управляемых данными значений, используйте свойства `DataTextFormatString` и `DataNavigateUrlFormatString`. В этих свойствах при необходимости введите статическую разметку, а затем используйте маркер `{0}` в том месте, где должно отображаться значение поля, указанного в свойствах `DataTextField` или `DataNavigateUrlFields`. Если в свойстве `DataNavigateUrlFields` задано несколько полей, используйте `{0}`, где необходимо вставить значение первого поля, `{1}` для второго значения поля и т. д.

Применяя это к нашему руководству, нам нужно установить свойство `DataNavigateUrlFields` равным `SupplierID`, поскольку это поле данных, значение которого необходимо настроить для каждой строки, а свойство `DataNavigateUrlFormatString` — `ProductsForSupplierDetails.aspx?SupplierID={0}`.

[![настроить HyperLinkField для включения правильного URL-адреса ссылки на основе поля «КодПоставщика»](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**Рис. 6**. Настройка HyperLinkField для включения соответствующего URL-адреса ссылки на `SupplierID` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image16.png))

После добавления HyperLinkField вы можете настроить и изменить порядок полей GridView. Следующая разметка показывает GridView после внесения некоторых незначительных настроек уровня поля.

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

Уделите время просмотру страницы `SupplierListMaster.aspx` в браузере. Как показано на рис. 7, в настоящее время на странице перечислены все поставщики, включая ссылку «Просмотр продуктов». Щелкнув ссылку View Products (просмотреть продукты), вы перейдете к `ProductsForSupplierDetails.aspx`, передав `SupplierID` поставщика в строке запроса.

[![каждая строка поставщика содержит ссылку View Products (Просмотр продуктов)](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**Рис. 7**. Каждая строка «поставщик» содержит ссылку «Просмотр продуктов» ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image19.png)).

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>Шаг 3. Перечисление продуктов поставщика в`ProductsForSupplierDetails.aspx`

На этом этапе `SupplierListMaster.aspx` страница отправляет пользователям `ProductsForSupplierDetails.aspx`, передавая `SupplierID` выбранного поставщика в строке запроса. Заключительный этап учебника состоит в том, чтобы отобразить продукты в элементе управления GridView в `ProductsForSupplierDetails.aspx`, `SupplierID` равно `SupplierID`, переданному через строку запроса. Для этого добавьте GridView на страницу `ProductsForSupplierDetails.aspx`, используя новый элемент управления ObjectDataSource с именем `ProductsBySupplierDataSource`, который вызывает метод `GetProductsBySupplierID(supplierID)` из класса `ProductsBLL`.

[![добавить новый элемент управления ObjectDataSource с именем Продуктсбисупплиердатасаурце](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**Рис. 8**. Добавление нового элемента управления ObjectDataSource с именем `ProductsBySupplierDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image22.png))

[![выберите класс ProductsBLL](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**Рис. 9**. выбор класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image25.png))

[![, что ObjectDataSource вызывает метод Жетпродуктсбисупплиерид (КодПоставщика)](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**Рис. 10**. вызов метода `GetProductsBySupplierID(supplierID)` ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image28.png))

На последнем шаге мастера настройки источника данных предлагается указать источник параметра *`supplierID`* метода `GetProductsBySupplierID(supplierID)`. Чтобы использовать значение строки запроса, задайте для свойства Источник параметра значение QueryString и введите имя значения QueryString, которое будет использоваться в текстовом поле QueryStringField (`SupplierID`).

[![заполнить значение параметра «КодПоставщика» из значения строки «КодПоставщика»](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**Рис. 11**. Заполнение значения параметра *`supplierID`* из значения строки запроса `SupplierID` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image31.png))

Это все. На рис. 12 показана страница `ProductsForSupplierDetails.aspx` при посещении щелчком по ссылке Токио Traders (`SupplierListMaster.aspx`).

[![отображаются продукты, предоставленные в Токио Traders.](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**Рис. 12**. отображаются продукты, предоставленные в компании Токио ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image34.png)).

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>Отображение сведений о поставщике в`ProductsForSupplierDetails.aspx`

Как показано на рис. 12, на странице `ProductsForSupplierDetails.aspx` просто перечислены продукты, предоставляемые `SupplierID`, указанным в строке запроса. Тем не менее, кто-то посылает на эту страницу напрямую, не знает, что на рис. 12 показаны продукты в Токио. Чтобы устранить эту проблему, можно также отобразить сведения о поставщике на этой странице.

Начните с добавления элемента управления FormView над элементом GridView продуктов. Создайте новый элемент управления ObjectDataSource с именем `SuppliersDataSource`, который вызывает метод `GetSupplierBySupplierID(supplierID)` класса `SuppliersBLL`.

[![выберите класс Супплиерсблл](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**Рис. 13**. выбор класса `SuppliersBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image37.png))

[![, что ObjectDataSource вызывает метод Жетсупплиербисупплиерид (КодПоставщика)](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**Рис. 14**. вызов метода `GetSupplierBySupplierID(supplierID)` ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image40.png))

Как и в случае с `ProductsBySupplierDataSource`, параметру *`supplierID`* присваивается значение `SupplierID` строки запроса.

[![заполнить значение параметра «КодПоставщика» из значения строки «КодПоставщика»](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**Рис. 15**. Заполнение значения параметра *`supplierID`* из значения строки запроса `SupplierID` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image43.png))

При привязке FormView к ObjectDataSource в представление конструирования Visual Studio автоматически создает `ItemTemplate`, `InsertItemTemplate`и `EditItemTemplate` FormView с элементами управления Label и TextBox для каждого поля данных, возвращаемого ObjectDataSource. Поскольку мы просто хотим отобразить сведения о поставщиках, вы можете удалить `InsertItemTemplate` и `EditItemTemplate`. Затем измените ItemTemplate так, чтобы он отображал название компании поставщика в элементе `<h3>` и адрес, город, страна и номер телефона под названием компании. Кроме того, можно вручную задать `DataSourceID` FormView и создать `ItemTemplate` разметку, как это было сделано в учебнике «[Отображение данных с помощью ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)».

После этих изменений декларативная разметка FormView должна выглядеть следующим образом:

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

На рис. 16 показан снимок экрана `ProductsForSupplierDetails.aspx` странице после включения сведений о поставщике, описанных выше.

[![список продуктов содержит сводку о поставщике](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**Рис. 16**. список продуктов содержит сводку о поставщике ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image46.png))

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>Применение последних касаний для пользовательского интерфейса`ProductsForSupplierDetails.aspx`

Чтобы улучшить взаимодействие с пользователем для этого отчета, необходимо внести несколько дополнений на страницу `ProductsForSupplierDetails.aspx`. В настоящее время пользователь может перейти со страницы `ProductsForSupplierDetails.aspx` назад в список поставщиков, щелкнув кнопку назад в браузере. Давайте добавим элемент управления HyperLink на страницу `ProductsForSupplierDetails.aspx`, которая связывается с `SupplierListMaster.aspx`, предоставляя другой способ возврата пользователю в главный список.

[![добавить элемент управления HyperLink, чтобы вернуть пользователя к Супплиерлистмастер. aspx.](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**Рис. 17**. Добавление элемента управления HyperLink для возврата пользователя к `SupplierListMaster.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image49.png))

Если пользователь щелкает ссылку View Products (Просмотр продуктов) для поставщика, у которого нет продуктов, `ProductsBySupplierDataSource` ObjectDataSource в `ProductsForSupplierDetails.aspx` не возвращает никаких результатов. Элемент управления GridView, привязанный к ObjectDataSource, не будет обрабатывать разметку, что приводит к пустой области на странице в браузере пользователя. Чтобы более ясно взаимодействовать с пользователем, что нет продуктов, связанных с выбранным поставщиком, мы можем задать для свойства `EmptyDataText` GridView сообщение, которое должно отображаться при возникновении такой ситуации. Я установил для этого свойства значение "отсутствуют продукты, предоставленные этим поставщиком"

По умолчанию все поставщики в базе данных Northwind содержат по крайней мере один продукт. Однако в этом руководстве я вручную изменил таблицу `Products`, чтобы поставщик Escargots Nouveaux больше не был связан с какими-либо продуктами. На рис. 18 показана страница сведений для Escargots Nouveaux после внесения этого изменения.

[![пользователи сообщают, что поставщик не предоставляет продукты](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**Рис. 18**. пользователи сообщают о том, что поставщик не предоставляет какие-либо продукты ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-across-two-pages-cs/_static/image52.png))

## <a name="summary"></a>Сводка

В то время как отчеты «основной/подробности» могут отображать как основные, так и подробные записи на одной странице, во многих веб-сайтах они разделяются на две веб-страницы. В этом учебнике мы рассмотрели, как реализовать такой отчет «основной/подробности», применяя поставщиков, перечисленных в элементе управления GridView на главной веб-странице, и связанных продуктов, перечисленных на странице «сведения». Каждая строка поставщика на главной веб-странице содержала ссылку на страницу сведений, переданную по значению `SupplierID` строки. Такие ссылки, относящиеся к строкам, можно легко добавить с помощью HyperLinkField GridView.

На странице сведений получение этих продуктов для указанного поставщика была выполнена путем вызова метода `GetProductsBySupplierID(supplierID)` класса `ProductsBLL`. Значение параметра *`supplierID`* было указано декларативно с помощью строки запроса в качестве источника параметра. Мы также рассмотрели, как отобразить сведения о поставщике на странице сведений с помощью FormView.

[Следующий учебник](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) является последним в отчетах «основной/подробности». Мы рассмотрим, как отобразить список продуктов в элементе управления GridView, где у каждой строки есть кнопка выбора. Если нажать кнопку Выбрать, сведения о продукте будут отображаться в элементе управления DetailsView на той же странице.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-filtering-with-two-dropdownlists-cs.md)
> [Вперед](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
