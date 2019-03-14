---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: Отображение данных на диаграмме с веб-страниц ASP.NET (Razor) | Документация Майкрософт
author: microsoft
description: В этой главе описываются способы отображения данных в диаграмме. В предыдущих главах вы узнали, как отобразить данные в сетке и вручную. В данной главе объясняется...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 00529355476e88c47ab790121ae77202aa5e7b76
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061101"
---
<a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>Отображение данных на диаграмме с веб-страниц ASP.NET (Razor)
====================
по [Microsoft](https://github.com/microsoft)

> В этой статье объясняется, как использовать диаграмму для отображения данных в на веб-сайте ASP.NET Web Pages (Razor) с помощью `Chart` вспомогательный.
> 
> **Вы узнаете, как**:
> 
> - Способ отображения данных в диаграмме.
> - Как изменить стиль диаграммы, использующие встроенные темы.
> - Способ сохранения диаграммы и способ их кэширования для повышения производительности.
> 
> Ниже перечислены возможности, представленные в этой статье программирования ASP.NET:
> 
> - `Chart` Вспомогательный.
> 
> > [!NOTE]
> > Сведения в этой статье относятся к веб-страниц ASP.NET 1.0 и Web Pages 2.


<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>Вспомогательный метод диаграммы

Если вы хотите отображать данные в графической форме, можно использовать `Chart` вспомогательный. `Chart` Вспомогательный объект может отображать изображения, отображающий данные в различных типов диаграмм. Он поддерживает многие параметры форматирования и добавления меток. `Chart` Вспомогательный объект может отображать более чем 30 типов диаграмм, включая все типы диаграмм, которые могут быть знакомы из Microsoft Excel или других средств &#8212; диаграммы с областями, линейчатые диаграммы, гистограммы, графики и круговые диаграммы, а также многое другое специализированные диаграммы, такие как биржевые диаграммы.

| **Диаграмма с областями** ![Описание: Рисунок для типа диаграммы с областями](7-displaying-data-in-a-chart/_static/image1.jpg) | **Линейчатая диаграмма** ![Описание: Рисунок для типа линейчатой диаграммы](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **Гистограмма** ![Описание: Рисунок для типа диаграммы столбца](7-displaying-data-in-a-chart/_static/image3.jpg) | **График** ![Описание: Рисунок для типа диаграммы «график»](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **Круговая диаграмма** ![Описание: Рисунок для типа круговой диаграммы](7-displaying-data-in-a-chart/_static/image5.jpg) | **Биржевая диаграмма** ![Описание: Рисунок для типа биржевая диаграмма](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Элементы диаграммы

Диаграммы показывают данные и дополнительные элементы, такие как условных обозначений, осей, рядов и т. д. На следующем рисунке показаны многие элементы диаграммы, которые можно настроить при использовании `Chart` вспомогательный. В этой статье показано, как настроить некоторые (но не все) из этих элементов.

![Описание: На рисунке представлены элементы диаграммы](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Создание диаграммы на основе данных

Данные, отображаемые на диаграмме может быть массив, из результатов, возвращаемых из базы данных или данные, содержащиеся в XML-файл.

### <a name="using-an-array"></a>С помощью массива

Как описано в [введение в ASP.NET веб-страниц программирование с использованием синтаксиса Razor](https://go.microsoft.com/fwlink/?LinkId=202890), массив позволяет хранить коллекции схожих элементов в одной переменной. Массивы можно использовать для хранения данных, который требуется включить в диаграмму.

Эта процедура показывает, как вы можно создать диаграмму на основе данных в массивах, с помощью типа диаграммы по умолчанию. Также показано, как для отображения на диаграмме в пределах страницы.

1. Создайте файл с именем *ChartArrayBasic.cshtml*.
2. Замените существующее содержимое следующим: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    Код сначала создает новую диаграмму и задает высоту и ширину. Укажите заголовок диаграммы с помощью `AddTitle` метод. Чтобы добавить данные, используйте `AddSeries` метод. В этом примере используется `name`, `xValue`, и `yValues` параметры `AddSeries` метод. `name` Параметр отображается в условных обозначениях диаграммы. `xValue` Параметр содержит массив данных, отображаемых вдоль горизонтальной оси диаграммы. `yValues` Параметр содержит массив данных, который используется для построения точек диаграммы по вертикали.

    `Write` Метод фактически выполняет визуализацию диаграммы. В этом случае, так как не был указан тип диаграммы, `Chart` вспомогательный визуализирует его по умолчанию диаграммы и гистограммы.
3. Откройте страницу в браузере. В браузере отобразится диаграммы. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>С помощью запроса к базе данных для данных диаграммы

Если в базе данных сведения, которые необходимо построить диаграмму, можно выполнить запрос к базе данных и затем использовать данные из результатов для создания диаграммы. Эта процедура показано, как для чтения и отображения данных из базы данных, созданной в этой статье [введение в работу с базой данных в веб-узлы веб-страниц ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202893).

1. Добавить *приложения\_данных* папку в корневой каталог веб-сайта, если папка не существует.
2. В *приложения\_данных* папки, добавьте файл базы данных, с именем *SmallBakery.sdf* , описанной в [введение в работу с базой данных на сайтах веб-страниц ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202893).
3. Создайте файл с именем *ChartDataQuery.cshtml*.
4. Замените существующее содержимое следующим:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    Код сначала открывает SmallBakery базу данных и присваивает его переменной с именем `db`. Данная переменная представляет `Database` объект, который может использоваться для чтения и записи в базу данных. Затем код выполняется запрос SQL, чтобы получить имя и цену каждого продукта. Код создает новую диаграмму и передает ему запрос к базе данных, вызвав диаграммы `DataBindTable` метод. Этот метод принимает два параметра: `dataSource` параметр предназначен для данных из запроса и `xField` параметр позволяет задать, какой столбец данных используется для оси x диаграммы.

    В качестве альтернативы использованию `DataBindTable` метод, можно использовать `AddSeries` метод `Chart` вспомогательный. `AddSeries` Метод позволяет задать `xValue` и `yValues` параметров. Например, вместо использования `DataBindTable` метод следующим образом:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    Можно использовать `AddSeries` метод следующим образом:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Оба отображают те же результаты. `AddSeries` Метод является более гибким, поскольку можно указать тип диаграммы и данные более явно, но `DataBindTable` метод проще в использовании, если вам не требуется дополнительную гибкость.
5. Откройте страницу в браузере. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>С помощью XML-данных

Третий параметр для построения диаграмм — для использования в XML-файл в качестве данных для диаграммы. Для этого требуется, что XML-файл также содержит файл схемы (*.xsd* файл), описывающий XML-структуру. Эта процедура показано, как считывать данные из XML-файла.

1. В *приложения\_данных* папки, создайте новый файл XML с именем *data.xml*.
2. Замените существующий код XML следующей, которая является данными XML о сотрудниках в вымышленной компании. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. В *приложения\_данных* папки, создайте новый файл XML с именем *data.xsd*. (Обратите внимание, что на этот раз модуль будет *.xsd*.)
4. Замените существующий XML-код следующим кодом: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. В корне веб-сайта, создайте новый файл с именем *ChartDataXML.cshtml*.
6. Замените существующее содержимое следующим: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    Код сначала создает `DataSet` объекта. Этот объект используется для управления данными, которые считываются из XML-файла и организуйте ее работу в соответствии с данными из файла схемы. (Обратите внимание на то, что в верхней части кода имеется инструкция `using SystemData`. Это необходимо, чтобы иметь возможность работать с `DataSet` объекта. Дополнительные сведения см. в разделе [ &quot;Using&quot; инструкций и полные имена](#SB_UsingStatements) далее в этой статье.)

    Затем код создает `DataView` объекта на основе набора данных. Представление данных предоставляет объект, который диаграммы можно привязать к &#8212; т.е чтения и отображения. Диаграмма привязывается к данным с помощью `AddSeries` метод, как вы видели ранее при создание диаграмм данных массива, за исключением случаев, это время `xValue` и `yValues` присвоено `DataView` объекта.

    В этом примере также показано, как для указания определенного типа диаграммы. При добавлении данных в `AddSeries` метода `chartType` также установлено для отображения круговой диаграммы.
7. Откройте страницу в браузере. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>Операторы «Using» и полные имена
> 
> .NET Framework на основе ASP.NET Web Pages с синтаксисом Razor состоит из нескольких тысяч компонентов (классы). Чтобы сделать его неудобно работать с этими классами, они организованы в *пространства имен*, которые представляют собой подобно библиотеки. Например `System.Web` пространство имен содержит классы, поддерживающие связь с браузером и сервером, `System.Xml` пространство имен содержит классы, используемые для создания и чтения файлов XML и `System.Data` пространство имен содержит классы, которые позволяют работать с данными.
> 
> Чтобы получить доступ к каждого конкретного класса, в .NET Framework, код должен знать не только имя класса, но пространство имен, класс находится в. Например, чтобы использовать `Chart` helper, код должен найти `System.Web.Helpers.Chart` класс, который объединяет пространство имен (`System.Web.Helpers`) с именем класса (`Chart`). Этот процесс известен как класс *полное* имя &#8212; его полная и неоднозначная расположения в vastness платформы .NET Framework. В коде это будет выглядеть следующим образом:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> Тем не менее, неудобно (и подвержено ошибкам) чтобы использовать эти имена long, полное каждый раз будет ссылаться на класс или вспомогательный. Таким образом, чтобы его проще использовать имена классов, вы можете *импорта* пространства имен вас интересует, как правило, это является всего лишь несколькими из многих пространств имен в .NET Framework. При импорте пространства имен, можно использовать только имя класса (`Chart`) вместо полное доменное имя (`System.Web.Helpers.Chart`). Когда ваш код выполняется и обнаруживает имя класса, он может выглядеть в только что импортированные для поиска этого класса пространства имен.
> 
> При использовании веб-страниц ASP.NET с синтаксисом Razor для создания веб-страниц, обычно используется тот же набор классов каждый раз, включая `WebPage` класс, различные вспомогательные функции и т. д. Чтобы сохранить работу импорта соответствующего пространства имен, каждый раз при создании веб-сайта, среда ASP.NET настроена, она автоматически импортирует набор пространств имен core для каждого веб-узла. Вот почему еще не приходилось иметь дело с пространства имен или импорт пока; все классы, которые вы уже работали с находятся в пространствах имен, уже импортирована для вас.
> 
> Тем не менее иногда требуется для работы с классом, который не находится в пространстве имен, который автоматически импортируется автоматически. В этом случае вы можете использовать полное доменное имя этого класса, или можно вручную импортировать пространство имен, содержащее класс. Чтобы импортировать пространство имен, используйте `using` инструкции (`import` в Visual Basic), как показано в примере выше статье.
> 
> Например `DataSet` класс находится в `System.Data` пространства имен. `System.Data` Пространство имен не является автоматически доступным для страниц ASP.NET Razor. Таким образом для работы с `DataSet` класса, используя его полное имя, можно использовать следующий код:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> Если необходимо использовать `DataSet` класса несколько раз можно импортировать пространство имен следующим образом и затем использовать только имя класса в коде:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Вы можете добавить `using` инструкций для любой других пространствах имен .NET Framework, если нужно сослаться. Тем не менее, как уже отмечалось, не требуется для этого часто, так как большинство классов, которые вы будете работать в пространствах имен, которые автоматически импортируются в ASP.NET для использования в *.cshtml* и *.vbhtml* страниц.


<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Отображать диаграммы внутри веб-страницы

В примерах вы уже видели, создать диаграмму, а затем отображается диаграмма непосредственно в браузере как графическое изображение. Во многих случаях, вы хотите отобразить диаграмму как часть страницы, не только сама по себе в браузере. Для этого требуется двухэтапный процесс. Первым шагом является создание страницы, которая создает диаграмму, как вы уже видели.

Вторым шагом является отображение полученный образ на другую страницу. Для отображения изображения, используйте HTML `<img>` элемент, в том же так же, чтобы отобразить любое изображение. Тем не менее, вместо ссылки на *.jpg* или *.png* файл, `<img>` ссылок на элементы *.cshtml* файл, содержащий `Chart` вспомогательный, будет создана диаграмма. При запуске отображаемой страницы, `<img>` элемент возвращает выходные данные `Chart` вспомогательный и готовит к просмотру диаграммы.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. Создайте файл с именем *ShowChart.cshtml*.
2. Замените существующее содержимое следующим: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    Код использует `<img>` элемент для отображения на диаграмме, который был создан ранее в *ChartArrayBasic.cshtml* файла.
3. Запуск веб-страницы в браузере. *ShowChart.cshtml* файл отображает изображение диаграммы, в зависимости от кода, содержащегося в *ChartArrayBasic.cshtml* файла.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Стиля диаграммы

`Chart` Вспомогательный поддерживает большое количество параметров, позволяющих настроить внешний вид диаграммы. Можно задать цвета, шрифты, границы и т. д. С легкостью настроить внешний вид диаграммы является использование *темы*. Темы — это коллекции данных, определяющие способ визуализации диаграммы с шрифты, цвета, меток, палитр, границ и эффектов. (Обратите внимание, что стиль диаграммы не указывает тип диаграммы.)

В следующей таблице перечислены встроенные темы.

| Тема | Описание |
| --- | --- |
| `Vanilla` | Отображает красные столбцы на белом фоне. |
| `Blue` | Отображает синий столбцов на синем фоне градиента. |
| `Green` | Отображает синий столбы зеленый градиентным фоном. |
| `Yellow` | Отображаются столбцы, оранжевый цвет на желтый градиентным фоном. |
| `Vanilla3D` | Отображает трехмерной красные столбцы на белом фоне. |

Вы можете указать тему для использования при создании диаграммы.

1. Создайте файл с именем *ChartStyleGreen.cshtml*.
2. Замените существующее содержимое на странице следующее:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Этот код является таким же, как пример выше, который использует базу данных для данных, но добавляет `theme` параметр при создании `Chart` объекта. Ниже приведен измененный код.

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Откройте страницу в браузере. Вы увидите те же данные, но диаграмма выглядит более великолепные: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Для сохранения диаграммы

При использовании `Chart` вспомогательный как вы уже видели в этой статье вспомогательное приложение повторно создает диаграмму с нуля каждый раз, он вызывается. При необходимости код для диаграммы также повторно запрашивает базу данных или повторно считывает XML-файл для получения данных. В некоторых случаях это может быть сложной операции, например если база данных, выполняется запрос велика или XML-файл содержит большой объем данных. Даже если диаграммы не включает большие объемы данных, процесс динамического создания образа будет занимать ресурсы сервера, и если многие пользователи запрашивают страницу или страницы, отображаемых на диаграмме, может существовать влияние на производительность веб-сайта.

Чтобы помочь вам сократить влиять на производительность создания диаграммы, можно создать диаграммы первый раз она необходима и сохраните его. При необходимости диаграммы вместо создания заново, вы можете просто взять сохраненную версию и визуализации, который.

Диаграмму можно сохранить в следующих случаях:

- Кэшировать диаграммы в памяти компьютера (на сервере).
- Сохраните диаграмму в виде файла изображения.
- Сохраните диаграмму как XML-файл. Этот параметр позволяет изменить диаграмму, до его сохранения.

### <a name="caching-a-chart"></a>Кэширование диаграммы

После создания диаграммы, вы можете кэшировать. Кэширование диаграммы, это означает, что он не должен быть создан повторно, если ее необходимо будет снова отобразить. При сохранении диаграммы в кэше, задается ключом, который должен быть уникальным для этой диаграммы.

Диаграммы, сохраненные в кэше может быть удалена, если серверу не хватает памяти. Кроме того кэш очищается при перезапуске приложения по любой причине. Таким образом стандартный способ работы с диаграммой кэшированных заключается в том, чтобы всегда сначала ли он доступен в кэше и в том случае, если это не так, то для создания или повторного создания.

1. В корне веб-сайта, создайте файл с именем *ShowCachedChart.cshtml*.
2. Замените существующее содержимое следующим: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` Тег включает `src` атрибут, указывающий на *ChartSaveToCache.cshtml* файл и передает ключ на страницу как строку запроса. Ключ содержит значения &quot;myChartKey&quot;. *ChartSaveToCache.cshtml* файл содержит `Chart` вспомогательный объект, будет создана диаграмма. Вы создадите эту страницу позже.

    В конце страницы есть ссылка на страницу с именем *ClearCache.cshtml*. Это страница, на которой вы также создадите чуть позже. Вам потребуется *ClearCache.cshtml* только для проверки кэширования в этом примере — это не ссылка или страницы, обычно следует использовать при работе с диаграммами кэшированные.
3. В корне веб-сайта, создайте файл с именем *ChartSaveToCache.cshtml*.
4. Замените существующее содержимое следующим:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    Код сначала проверяет, является ли что-либо был передан в качестве значения ключа в строке запроса. Если таким образом, код пытается считать диаграммы из кэша, вызвав `GetFromCache` метод и передайте ее ключ. Если оказывается, нет ничего в кэше по этому ключу (которая может произойти при первом запросе диаграммы), код создает диаграмму как обычно. По завершении диаграммы код сохраняет его в кэш, вызвав `SaveToCache`. Этот метод требует ключ (поэтому диаграммы можно запросить более поздней версии) и количество времени, диаграммы, которые нужно сохранить в кэше. (Точное время кэшировал диаграммы будет зависеть от как часто вы подумали, что данные, которые она представляет могут измениться.) `SaveToCache` Также требует `slidingExpiration` параметр &#8212; Если задано значение true, время ожидания счетчик сбрасывается каждый раз при обращении к диаграмме. Таким образом он фактически означает, что запись кэша диаграммы срок действия истекает через 2 минуты после последнего обращения к кто-то диаграммы. (Альтернативным методом скользящий срок действия — абсолютный срок действия, это означает, что запись кэша истечет ровно 2 минуты после он был помещен в кэш, независимо от того, как часто он был получен доступ.)

    Наконец, код использует `WriteFromCache` метод для извлечения и отображения диаграммы из кэша. Обратите внимание, что этот метод находится за пределами `if` блок, который проверяет кэш, так как он получит диаграммы из кэша ли диаграммы было принято решение с самого начала или должны были быть создаются и сохраняются в кэше.

    Обратите внимание, что в примере `AddTitle` метод включает метку времени. (Он добавляет текущую дату и время &#8212; `DateTime.Now` &#8212; к заголовку.)
5. Создать новую страницу с именем *ClearCache.cshtml* и замените его содержимое следующим:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Эта страница использует `WebCache` модуля поддержки диаграммы, которые кэшируются в *ChartSaveToCache.cshtml*. Как отмечалось ранее, у вас нет обычным образом, страницы следующим образом. Вы создаете ее здесь только для того, чтобы упростить тестирование кэширования.
6. Запустите *ShowCachedChart.cshtml* веб-страницу в браузере. На странице отображается изображение диаграммы, в зависимости от кода, содержащегося в *ChartSaveToCache.cshtml* файла. Запишите говорит отметка времени в заголовок диаграммы. 

    ![Описание: Рисунок простой диаграммы с меткой времени в заголовок диаграммы](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Закройте браузер.
8. Запустите *ShowCachedChart.cshtml* еще раз. Обратите внимание на то, что отметка времени такая же как и раньше, что означает, что диаграмма не был создан повторно, но вместо этого был считан из кэша.
9. В *ShowCachedChart.cshtml*, нажмите кнопку **очистить кэш** ссылку. Вы перейдете к *ClearCache.cshtml*, который сообщает, что кэш был очищен.
10. Нажмите кнопку **вернуться к ShowCachedChart.cshtml** ссылку, или повторно запустите *ShowCachedChart.cshtml* из WebMatrix. Обратите внимание на то, что это время изменилось метка времени, так, как очистить кэш. Таким образом код должен повторно создать диаграммы и вернуть его в кэш.

### <a name="saving-a-chart-as-an-image-file"></a>Для сохранения диаграммы в файл изображения

Можно также сохранить диаграмму в виде файла изображения (например, как *.jpg* файл) на сервере. Затем можно использовать файл изображения так, как любое другое изображение. Преимущество заключается в хранятся в файл, а не сохранены временного кэша. Можно сохранить новое изображение диаграммы в разное время (например, каждый час) и затем сохраняются постоянно фиксировать изменения, происходящие с течением времени. Обратите внимание, что необходимо убедиться в том, что веб-приложение имеет разрешение на сохранение файла в папку на сервере, где вы хотите поместить файл изображения.

1. В корне веб-сайта, создайте папку с именем  *\_ChartFiles* если он еще не существует.
2. В корне веб-сайта, создайте файл с именем *ChartSave.cshtml*.
3. Замените существующее содержимое следующим:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    Код сначала проверяет, является ли *.jpg* файл существует, вызвав `File.Exists` метод. Если файл не существует, код создает новый `Chart` из массива. Это время, код вызывает метод `Save` и передает `path` параметр, чтобы указать путь к файлу и имя файла для сохранения диаграммы. В основной области страницы `<img>` элемент использует путь, чтобы он указывал *.jpg* файл для отображения.
4. Запустите *ChartSave.cshtml* файла.
5. Вернитесь к WebMatrix. Обратите внимание, что файл изображения с именем *chart01.jpg* была сохранена в  *\_ChartFiles* папки.

### <a name="saving-a-chart-as-an-xml-file"></a>Для сохранения диаграммы в XML-файл

Наконец можно сохранить диаграмму в виде XML-файл на сервере. Преимущество использования этого метода над кэшированием или сохранением диаграммы в файл является то, что можно изменить XML перед выводом диаграммы, если вы хотите. Приложение должно иметь разрешения на чтение и запись для папки на сервере, где вы хотите поместить файл изображения.

1. В корне веб-сайта, создайте файл с именем *ChartSaveXml.cshtml*.
2. Замените существующее содержимое следующим:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Этот код аналогичен коду, обсуждавшейся ранее для хранения диаграммы в кэше, за исключением того, что она использует XML-файл. Код сначала проверяет, существует ли XML-файл, вызвав `File.Exists` метод. Если файл существует, код создает новый `Chart` и передает имя файла как `themePath` параметр. В результате будет создана диаграмма, в зависимости от того, все, что в XML-файле. Если XML-файл еще не существует, код создает диаграмму обычным образом, а затем вызывает `SaveXml` сохранить его. Визуализация диаграммы выполняется с помощью `Write` метод, как вы уже видели.

    Как и в случае со страницей, в котором кэширование, этот код включает метку времени в заголовок диаграммы.
3. Создать новую страницу с именем *ChartDisplayXMLChart.cshtml* и добавьте в него следующую разметку: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. Запустите *ChartDisplayXMLChart.cshtml* страницы. Отображение диаграммы. Запишите метку времени в заголовок диаграммы.
5. Закройте браузер.
6. В WebMatrix, щелкните правой кнопкой мыши  *\_ChartFiles* папку, нажмите кнопку **обновить**и затем откройте папку. *XMLChart.xml* файл в этой папке был создан `Chart` вспомогательный. 

    ![Описание: _ChartFiles папка с файлом XMLChart.xml, созданных вспомогательным диаграммы.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. Запустите *ChartDisplayXMLChart.cshtml* странице еще раз. На диаграмме показано ту же метку времени, как при первом запуске страницы. Том, что диаграмма формируется из XML, сохраненный ранее.
8. В WebMatrix откройте  *\_ChartFiles* папки и delete *XMLChart.xml* файла.
9. Запустите *ChartDisplayXMLChart.cshtml* странице еще раз. На этот раз отметка времени обновляется, так как `Chart` вспомогательный было повторно выполнить XML-файле. Если вы хотите проверить  *\_ChartFiles* папку и обратите внимание, что XML-файл обратно.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Введение в работу с базой данных в ASP.NET Web Pages сайтов](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Использование кэширования в ASP.NET Web Pages сайты для повышения производительности](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Класс диаграммы](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (Справочник по API веб-страницы ASP.NET на сайте MSDN)