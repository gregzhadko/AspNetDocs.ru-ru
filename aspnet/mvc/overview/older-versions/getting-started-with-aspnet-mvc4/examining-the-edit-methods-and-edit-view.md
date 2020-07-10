---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: Проверка методов Edit и режима правки | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "86163057"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Изучение методов Edit и представления Edit

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Обновленная версия этого учебника доступна [здесь](../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.

В этом разделе вы изучите созданные методы действий и представления для контроллера фильмов. Затем вы добавите пользовательскую страницу поиска.

Запустите приложение и перейдите к `Movies` контроллеру, добавив */Movies* в URL-адрес в адресной строке браузера. Наведите указатель мыши на ссылку **Edit (изменить** ), чтобы просмотреть URL-адрес, на который он ссылается.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Ссылка для **редактирования** была создана `Html.ActionLink` методом в представлении *виевс\мовиес\индекс.кштмл* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`Объект является вспомогательным объектом, который предоставляется с помощью свойства в базовом классе [System. Web. MVC. вебвиевпаже](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) . `ActionLink`Метод вспомогательного метода упрощает динамическое создание ГИПЕРССЫЛОК HTML, которые связываются с методами действий на контроллерах. Первым аргументом `ActionLink` метода является текст ссылки для отрисовки (например, `<a>Edit Me</a>` ). Вторым аргументом является имя вызываемого метода действия. Последний аргумент — это [Анонимный объект](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , создающий данные маршрута (в данном случае — идентификатор 4).

Созданная ссылка показана на предыдущем рисунке `http://localhost:xxxxx/Movies/Edit/4` . Маршрут по умолчанию (установленный в *app \_ старт\раутеконфиг.КС*) принимает шаблон URL-адреса `{controller}/{action}/{id}` . Таким образом, ASP.NET преобразует `http://localhost:xxxxx/Movies/Edit/4` запрос к `Edit` методу действия `Movies` контроллера с параметром, `ID` равным 4. Изучите следующий код из *файла \_ старт\раутеконфиг.КС приложения* .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

Можно также передать параметры метода действия с помощью строки запроса. Например, URL-адрес `http://localhost:xxxxx/Movies/Edit?ID=4` также передает параметр `ID` 4 `Edit` методу действия `Movies` контроллера.

![едиткуеристринг](examining-the-edit-methods-and-edit-view/_static/image3.png)

Откройте `Movies` контроллер. `Edit`Ниже показаны два метода действия.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

Обратите внимание на второй метод действия `Edit`, которому предшествует атрибут `HttpPost`. Этот атрибут указывает, что перегрузка `Edit` метода может быть вызвана только для запросов POST. Атрибут можно применить `HttpGet` к первому методу Edit, но это не обязательно, так как это значение по умолчанию. (Мы будем называть методы действий, которым неявно назначается `HttpGet` атрибут в качестве `HttpGet` методов.)

`HttpGet` `Edit` Метод принимает параметр идентификатора фильма, находит фильм с помощью `Find` метода Entity Framework и возвращает выбранный фильм в представление редактирования. Параметр ID задает [значение по умолчанию](https://msdn.microsoft.com/library/dd264739.aspx) , равное нулю, если `Edit` метод вызывается без параметра. Если фильм не удается найти, возвращается [хттпнотфаунд](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) . Если в представлении редактирования создана система формирования шаблонов, она проверяет класс `Movie` и создает код для отображения элементов `<label>` и `<input>` для каждого свойства класса. В следующем примере показано созданное представление изменения:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

Обратите внимание, что в шаблоне представления есть `@model MvcMovie.Models.Movie` оператор в верхней части файла — это указывает, что представление ожидает, что модель шаблона представления будет иметь тип `Movie` .

Сформированный код использует несколько *вспомогательных методов* для упрощения разметки HTML. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Вспомогательное приложение отображает имя поля ( &quot; title &quot; , &quot; ReleaseDate &quot; , &quot; Жанр &quot; или &quot; Price &quot; ). [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Вспомогательный объект визуализирует элемент HTML `<input>` . В [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) вспомогательном модуле отображаются все сообщения проверки, связанные с этим свойством.

Запустите приложение и перейдите по URL-адресу */Movies* . Щелкните ссылку **Edit** (Изменить). Просмотрите исходный код страницы в окне браузера. Ниже показан HTML-код для элемента Form.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`Элементы находятся в ЭЛЕМЕНТЕ HTML, `<form>` атрибут которого `action` имеет значение POST для URL-адреса */мовиес/едит* . Данные формы будут отправлены на сервер при нажатии кнопки " **изменить** ".

## <a name="processing-the-post-request"></a>Обработка запроса POST

В следующем листинге демонстрируется версия `HttpPost` метода действия `Edit`.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[Связыватель модели MVC ASP.NET](https://msdn.microsoft.com/magazine/hh781022.aspx) принимает значения отправленной формы и создает `Movie` объект, который передается в качестве `movie` параметра. Метод `ModelState.IsValid` проверяет, можно ли использовать переданные в форме данные для изменения (редактирования или обновления) объекта `Movie`. Если данные являются допустимыми, данные фильмов сохраняются в `Movies` коллекцию `db(MovieDBContext` экземпляра. Новые данные фильмов сохраняются в базе данных путем вызова `SaveChanges` метода `MovieDBContext` . После сохранения данных код перенаправляет пользователя к `Index` методу действия `MoviesController` класса, который отображает коллекцию фильмов, включая только что внесенные изменения.

Если опубликованные значения не являются допустимыми, они отображаются в форме. `Html.ValidationMessageFor`Вспомогательные методы в шаблоне представления *Edit. cshtml* отвечают за отображение соответствующих сообщений об ошибках.

![абкнотвалид](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> для поддержки проверки jQuery для национальных стандартов, отличных от английского, в которых используется запятая ( &quot; , &quot; ) для десятичной запятой, необходимо включить *globalize.js* и определенные *языки и региональные параметры, globalize.cultures.js* файла (из [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) и JavaScript для использования `Globalize.parseFloat` . В следующем коде показаны изменения в файле Виевс\мовиес\едит.кштмл для работы с &quot; культурой fr-FR &quot; :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Десятичное поле может потребовать запятую, а не десятичную точку. В качестве временного исправления можно добавить элемент Globalization в корневой файл web.config проектов. В следующем коде показан элемент globalization с культурой, заданной США английским.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

Все `HttpGet` методы соответствуют аналогичному шаблону. Они получают объект Movie (или список объектов, в случае использования `Index` ) и передают модель в представление. `Create`Метод передает пустой объект Movie в представление создания. Все методы, которые создают, редактируют, удаляют или иным образом изменяют данные, делают это в перегрузке метода `HttpPost`. Изменение данных в методе HTTP GET является угрозой безопасности, как описано в записи блога [совет ASP.NET #46 — не использовать ссылки DELETE, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Изменение данных в методе GET также нарушает рекомендации по протоколу HTTP и шаблон архитектуры [RESTful](http://en.wikipedia.org/wiki/Representational_State_Transfer) , указывающий, что запросы GET не должны изменять состояние приложения. Другими словами, операция GET должна выполняться безопасным способом, то есть не иметь побочных эффектов и не изменять существующие данные.

## <a name="adding-a-search-method-and-search-view"></a>Добавление метода поиска и представления поиска

В этом разделе вы добавите `SearchIndex` метод действия, позволяющий искать фильмы по жанру или названию. Это будет доступно с помощью URL-адреса */мовиес/сеарчиндекс* . В запросе будет отображаться HTML-форма, содержащая элементы ввода, которые пользователь может ввести для поиска фильма. Когда пользователь отправляет форму, метод действия получает значения поиска, размещенные пользователем, и использует значения для поиска в базе данных.

## <a name="displaying-the-searchindex-form"></a>Отображение формы Сеарчиндекс

Начните с добавления `SearchIndex` метода действия в существующий `MoviesController` класс. Метод вернет представление, содержащее HTML-форму. Вот этот код:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Первая строка `SearchIndex` метода создает следующий запрос [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) для выбора фильмов:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

Запрос определен на этом этапе, но еще не выполнялся в хранилище данных.

Если `searchString` параметр содержит строку, запрос фильмов изменяется для фильтрации по значению строки поиска с помощью следующего кода:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

Приведенный выше код `s => s.Title` представляет собой [лямбда-выражение](https://msdn.microsoft.com/library/bb397687.aspx). Лямбда-выражения используются в запросах [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) на основе методов в качестве аргументов методов стандартных операторов запросов, таких как метод [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) , используемый в приведенном выше коде. Запросы LINQ не выполняются, если они определены или изменяются путем вызова метода, такого как `Where` или `OrderBy` . Вместо этого выполнение запроса откладывается, что означает, что вычисление выражения откладывается до тех пор, пока его реализованное значение фактически не будет перебираться или [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) метод не будет вызван. В этом `SearchIndex` примере запрос выполняется в представлении сеарчиндекс. Дополнительные сведения об отложенном и немедленном выполнении запросов см. в разделе [Выполнение запроса](https://msdn.microsoft.com/library/bb738633.aspx).

Теперь можно реализовать `SearchIndex` представление, которое будет отображать форму для пользователя. Щелкните правой кнопкой мыши внутри `SearchIndex` метода и выберите **Добавить представление**. В диалоговом окне **Добавление представления** укажите, что вы собираетесь передать `Movie` объект в шаблон представления в качестве класса модели. В списке **шаблон формирования шаблона** выберите **Список**, а затем нажмите кнопку **добавить**.

![аддсеарчвиев](examining-the-edit-methods-and-edit-view/_static/image5.png)

При нажатии кнопки **Добавить** создается шаблон представления *виевс\мовиес\сеарчиндекс.кштмл* . Так как в списке **шаблонов шаблонов** был выбран **список** , Visual Studio автоматически создает (обменяется с формированием шаблонов) некоторую разметку по умолчанию в представлении. Формирование шаблонов создало HTML-форму. Он проверил `Movie` класс и создал код для отрисовки `<label>` элементов для каждого свойства класса. В приведенном ниже списке показано созданное представление Create.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

Запустите приложение и перейдите по адресу */мовиес/сеарчиндекс*. Добавьте в URL-адрес строку запроса, например `?searchString=ghost`. Отображаются отфильтрованные фильмы.

![сеарчкристр](examining-the-edit-methods-and-edit-view/_static/image6.png)

Если изменить сигнатуру `SearchIndex` метода для параметра с именем `id` , `id` параметр будет соответствовать `{id}` заполнительу для маршрутов по умолчанию, заданных в файле *Global. asax* .

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

Исходный `SearchIndex` метод выглядит следующим образом:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

Измененный `SearchIndex` метод будет выглядеть следующим образом:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

Теперь можно передать заголовок поиска в качестве данных маршрута (сегмент URL-адреса) вместо значения строки запроса.

![сеарчраутедата](examining-the-edit-methods-and-edit-view/_static/image7.png)

Тем не менее пользователи вряд ли будут каждый раз изменять URL-адрес для поиска фильмов. Итак, теперь вы добавите пользовательский интерфейс, чтобы помочь им фильтровать фильмы. Если вы изменили сигнатуру `SearchIndex` метода, чтобы проверить, как передать параметр идентификатора, привязанного к маршруту, измените его обратно, чтобы метод задавал `SearchIndex` строковый параметр с именем `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

Откройте файл *виевс\мовиес\сеарчиндекс.кштмл* и сразу после `@Html.ActionLink("Create New", "Create")` добавьте следующее:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

В следующем примере показана часть файла *виевс\мовиес\сеарчиндекс.кштмл* с добавленной разметкой фильтрации.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`Вспомогательный объект создает открывающий `<form>` тег. `Html.BeginForm`Вспомогательная функция заставляет форму опубликовать себя, когда пользователь отправит форму, нажав кнопку **Фильтр** .

Запустите приложение и попробуйте найти фильм.

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

`HttpPost`Перегрузка `SearchIndex` метода отсутствует. Это не требуется, так как метод не изменяет состояние приложения, просто отфильтровывая данные.

Можно добавить следующий метод `HttpPost SearchIndex`. В этом случае вызывающий элемент действия будет соответствовать `HttpPost SearchIndex` методу, и `HttpPost SearchIndex` метод будет выполняться, как показано на рисунке ниже.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![сеарчпостгхост](examining-the-edit-methods-and-edit-view/_static/image9.png)

Тем не менее при добавлении этой версии `HttpPost` метода `SearchIndex` существует ограничение на общую реализацию. Допустим, вам необходимо добавить в закладки конкретный поиск или отправить друзьям ссылку, по которой они могут просмотреть аналогичный отфильтрованный список фильмов. Обратите внимание, что URL-адрес запроса HTTP POST совпадает с URL-адресом для запроса GET (localhost: XXXXX/Movies/Сеарчиндекс) — в самом URL-адресе нет сведений для поиска. Сейчас данные строки поиска отправляются на сервер в виде значения поля формы. Это означает, что вы не сможете записать эту информацию для поиска в закладки или отправить друзьям по URL-адресу.

Решение заключается в использовании перегрузки `BeginForm` , указывающей, что запрос POST должен добавить сведения для поиска в URL-адрес и направлять его в HttpGet версию `SearchIndex` метода. Замените существующий `BeginForm` метод без параметров следующим образом:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

Теперь при отправке поиска URL-адрес содержит строку запроса поиска. Поиск также переносится в метод `HttpGet SearchIndex`, даже если у вас определен метод `HttpPost SearchIndex`.

![сеарчиндексвисжетурл](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>Добавление поиска по жанру

Если вы добавили `HttpPost` версию `SearchIndex` метода, удалите ее сейчас.

Далее предстоит добавить функцию, позволяющую пользователям искать фильмы по жанрам. Замените метод `SearchIndex` следующим кодом:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

Эта версия `SearchIndex` метода принимает дополнительный параметр, а именно `movieGenre` . Первые несколько строк кода создают `List` объект для хранения жанров фильмов из базы данных.

Следующий код определяет запрос LINQ, который извлекает все жанры из базы данных.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

Код использует `AddRange` метод универсальной `List` коллекции, чтобы добавить в список все отдельные жанры. (Без `Distinct` модификатора добавляются дубликаты жанров, например, в нашем примере комедия будет добавляться дважды). Затем в коде сохраняется список жанров в `ViewBag` объекте.

В следующем коде показано, как проверить `movieGenre` параметр. Если он не пуст, код дополнительно ограничивает запрос фильмов, чтобы ограничить выбранные фильмы указанным жанром.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Добавление разметки в представление Сеарчиндекс для поддержки поиска по жанру

Добавьте `Html.DropDownList` вспомогательную функцию в файл *виевс\мовиес\сеарчиндекс.кштмл* непосредственно перед `TextBox` вспомогательным модулем. Готовая разметка показана ниже:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

Запустите приложение и перейдите по */мовиес/сеарчиндекс*. Попробуйте поиск по жанру, по имени фильма и по обоим критериям.

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

В этом разделе вы проверили методы действия CRUD и представления, созданные платформой. Вы создали метод и представление действия поиска, которые позволяют пользователям выполнять поиск по названию и жанру фильма. В следующем разделе вы узнаете, как добавить свойство в `Movie` модель и как добавить инициализатор, который будет автоматически создавать тестовую базу данных.

> [!div class="step-by-step"]
> [Назад](accessing-your-models-data-from-a-controller.md)
> [Вперед](adding-a-new-field-to-the-movie-model-and-table.md)
