---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Проверка методов Edit и режима правки | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 1894971430c4febee19f095373411ed319edc015
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045212"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Изучение методов Edit и представления Edit

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

В этом разделе вы изучите созданные `Edit` методы действий и представления для контроллера фильмов. Но сначала мы будем использовать сокращенную версию, чтобы сделать дату выпуска более эффективной. Откройте файл *моделс\мовие.КС* и добавьте выделенные строки, показанные ниже:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

Кроме того, можно сделать так, чтобы культура даты была такой:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

Пространство имен [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) будет рассмотрено в следующем учебнике. Атрибут [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) определяет отображаемое имя поля (в этом случае "Release Date" вместо "ReleaseDate"). Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) указывает тип данных, в данном случае это дата, поэтому сведения о времени, хранящиеся в поле, не отображаются. Атрибут [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) необходим для ошибки в браузере Chrome, которая неправильно отображает форматы даты.

Запустите приложение и перейдите к `Movies` контроллеру. Наведите указатель мыши на ссылку **Edit (изменить** ), чтобы просмотреть URL-адрес, на который он ссылается.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Ссылка для **редактирования** была создана `Html.ActionLink` методом в представлении *виевс\мовиес\индекс.кштмл* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`Объект является вспомогательным объектом, который предоставляется с помощью свойства в базовом классе [System. Web. MVC. вебвиевпаже](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) . `ActionLink`Метод вспомогательного метода упрощает динамическое создание ГИПЕРССЫЛОК HTML, которые связываются с методами действий на контроллерах. Первым аргументом `ActionLink` метода является текст ссылки для отрисовки (например, `<a>Edit Me</a>` ). Вторым аргументом является имя вызываемого метода действия (в данном случае это `Edit` действие). Последний аргумент — это [Анонимный объект](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , создающий данные маршрута (в данном случае — идентификатор 4).

Созданная ссылка показана на предыдущем рисунке `http://localhost:1234/Movies/Edit/4` . Маршрут по умолчанию (установленный в *app \_ старт\раутеконфиг.КС*) принимает шаблон URL-адреса `{controller}/{action}/{id}` . Таким образом, ASP.NET преобразует `http://localhost:1234/Movies/Edit/4` запрос к `Edit` методу действия `Movies` контроллера с параметром, `ID` равным 4. Изучите следующий код из *файла \_ старт\раутеконфиг.КС приложения* . Метод [файл MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) используется для маршрутизации HTTP-запросов к правильному контроллеру и методу действия и указания необязательного параметра ID. Метод [файл MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) также используется [хтмлхелперс](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) , например `ActionLink` для создания URL-адресов с учетом контроллера, метода действия и всех данных маршрута.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

Можно также передать параметры метода действия с помощью строки запроса. Например, URL-адрес `http://localhost:1234/Movies/Edit?ID=3` также передает параметру `ID` 3 значение `Edit` метода действия `Movies` контроллера.

![едиткуеристринг](examining-the-edit-methods-and-edit-view/_static/image3.png)

Откройте `Movies` контроллер. `Edit`Ниже показаны два метода действия.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

Обратите внимание на второй метод действия `Edit`, которому предшествует атрибут `HttpPost`. Этот атрибут указывает, что перегрузка `Edit` метода может быть вызвана только для запросов POST. Атрибут можно применить `HttpGet` к первому методу Edit, но это не обязательно, так как это значение по умолчанию. (Мы будем называть методы действий, которым неявно назначается `HttpGet` атрибут в качестве `HttpGet` методов.) Атрибут [BIND](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) является еще одним важным механизмом безопасности, который позволяет злоумышленникам переключать данные в вашу модель. В атрибут BIND, который требуется изменить, должны быть включены только свойства. Вы можете ознакомиться с перезаписью и атрибутом BIND в [примечании безопасности при перезаписи](https://go.microsoft.com/fwlink/?LinkId=317598). В простой модели, используемой в этом учебнике, мы будем привязать все данные в модели. Атрибут [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) используется для предотвращения подделки запроса и связывания с `@Html.AntiForgeryToken()` в файле представления редактирования (*виевс\мовиес\едит.кштмл*), а часть показана ниже:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` создает маркер скрытой подделки формы, который должен соответствовать `Edit` методу `Movies` контроллера. Дополнительные сведения о подделке межсайтовых запросов (также известном как XSRF или CSRF) см. в статье мой учебник [XSRF/CSRF предотвращение в MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).

`HttpGet` `Edit` Метод принимает параметр идентификатора фильма, находит фильм с помощью `Find` метода Entity Framework и возвращает выбранный фильм в представление редактирования. Если фильм не удается найти, возвращается [хттпнотфаунд](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) . Если в представлении редактирования создана система формирования шаблонов, она проверяет класс `Movie` и создает код для отображения элементов `<label>` и `<input>` для каждого свойства класса. В следующем примере показано представление редактирования, созданное системой формирования шаблонов Visual Studio:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Обратите внимание, что в шаблоне представления есть `@model MvcMovie.Models.Movie` оператор в верхней части файла — это указывает, что представление ожидает, что модель шаблона представления будет иметь тип `Movie` .

Сформированный код использует несколько *вспомогательных методов* для упрощения разметки HTML. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Вспомогательное приложение отображает имя поля ( &quot; title &quot; , &quot; ReleaseDate &quot; , &quot; Жанр &quot; или &quot; Price &quot; ). [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Вспомогательный объект визуализирует элемент HTML `<input>` . В [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) вспомогательном модуле отображаются все сообщения проверки, связанные с этим свойством.

Запустите приложение и перейдите по URL-адресу */Movies* . Щелкните ссылку **Edit** (Изменить). Просмотрите исходный код страницы в окне браузера. Ниже показан HTML-код для элемента Form.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>`Элементы находятся в ЭЛЕМЕНТЕ HTML, `<form>` атрибут которого `action` имеет значение POST для URL-адреса */мовиес/едит* . Данные формы будут отправлены на сервер при нажатии кнопки **сохранить** . Во второй строке показан скрытый токен [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) , созданный `@Html.AntiForgeryToken()` вызовом.

## <a name="processing-the-post-request"></a>Обработка запроса POST

В следующем листинге демонстрируется версия `HttpPost` метода действия `Edit`.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Атрибут [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) проверяет токен [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) , сформированный `@Html.AntiForgeryToken()` вызовом в представлении.

[Связыватель модели MVC ASP.NET](https://msdn.microsoft.com/library/dd410405.aspx) принимает значения отправленной формы и создает `Movie` объект, который передается в качестве `movie` параметра. `ModelState.IsValid`Проверяет, можно ли использовать данные, отправленные в форме, для изменения (изменения или обновления) `Movie` объекта. Если данные являются допустимыми, данные фильмов сохраняются в `Movies` коллекцию `db` ( `MovieDBContext` экземпляр). Новые данные фильмов сохраняются в базе данных путем вызова `SaveChanges` метода `MovieDBContext` . После сохранения данных код перенаправляет пользователя в метод действия `Index` класса `MoviesController`, который отображает коллекцию фильмов с учетом только что внесенных изменений.

Как только проверка на стороне клиента определит, что значение поля недопустимо, выводится сообщение об ошибке. Если JavaScript отключен, проверка на стороне клиента отключена. Однако сервер обнаруживает, что отправленные значения недопустимы, а значения формы повторно отображаются с сообщениями об ошибках.

Проверка рассматривается более подробно далее в этом руководстве.

`Html.ValidationMessageFor`Вспомогательные методы в шаблоне представления *Edit. cshtml* отвечают за отображение соответствующих сообщений об ошибках.

![абкнотвалид](examining-the-edit-methods-and-edit-view/_static/image4.png)

Все `HttpGet` методы соответствуют аналогичному шаблону. Они получают объект Movie (или список объектов, в случае использования `Index` ) и передают модель в представление. `Create`Метод передает пустой объект Movie в представление создания. Все методы, которые создают, редактируют, удаляют или иным образом изменяют данные, делают это в перегрузке метода `HttpPost`. Изменение данных в методе HTTP GET является угрозой безопасности, как описано в записи блога [совет ASP.NET #46 — не использовать ссылки DELETE, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Изменение данных в методе GET также нарушает рекомендации по протоколу HTTP и шаблон архитектуры [RESTful](http://en.wikipedia.org/wiki/Representational_State_Transfer) , указывающий, что запросы GET не должны изменять состояние приложения. Другими словами, операция GET должна выполняться безопасным способом, то есть не иметь побочных эффектов и не изменять существующие данные.

## <a name="jquery-validation-for-non-english-locales"></a>проверка jQuery для национальных стандартов, отличных от английского

Если используется компьютер с английским языком США, можно пропустить этот раздел и перейти к следующему руководству. Версию этого учебника для глобализации можно скачать [здесь](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475). Отличные два этапа учебника по интернационализации см. в разделе [надим ASP.NET MVC 5 International интернационализации](http://afana.me/post/aspnet-mvc-internationalization.aspx).

> [!NOTE]
> для поддержки проверки jQuery для национальных стандартов, отличных от английского, которые используют запятую ( &quot; , &quot; ) для десятичной запятой и форматы даты, отличные от US-English, необходимо включить *globalize.js* и определенные *языки и региональные параметры и globalize.cultures.js* файла (из [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) и JavaScript для использования `Globalize.parseFloat` . Вы можете получить неанглоязычные проверки jQuery в NuGet. (Не устанавливайте глобализацию, если используется английский язык).

1. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **Управление пакетами NuGet для решения**.

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. На левой панели нажмите кнопку <strong>Обзор *.</strong> * (См. изображение ниже.)
3. В поле ввода введите * глобализация * *.

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) Выберите `jQuery.Validation.Globalize` , выберите `MvcMovie` и нажмите кнопку **установить**. Файл *Scripts\jquery.globalize\globalize.js* будет добавлен в проект. Папка * Скриптс\жкуери.глобализе\културес \* будет содержать множество файлов JavaScript языка и региональных параметров. Обратите внимание, что установка этого пакета может занять пять минут.

   В следующем коде показаны изменения в файле Виевс\мовиес\едит.кштмл:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Чтобы избежать повторения этого кода в каждом представлении редактирования, его можно переместить в файл макета. Сведения о том, как оптимизировать загрузку скрипта, см. в разделе мой учебник [объединение и минификации](../../performance/bundling-and-minification.md).

Дополнительные сведения см. в статье [ASP.NET MVC 3 International](http://afana.me/post/aspnet-mvc-internationalization.aspx) и [ASP.NET MVC 3 internationaling-Part 2 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).

Как временное исправление, если вы не можете выполнить проверку в Вашем языковом стандарте, можно принудительно настроить компьютер на использование английского языка (США) или отключить JavaScript в браузере. Чтобы заставить компьютер использовать английский язык (США), можно добавить элемент Globalization в корневой файл *web.config* проектов. В следующем коде показан элемент globalization с культурой, заданной США английским.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a> В следующем руководстве мы реализуем функции поиска.

> [!div class="step-by-step"]
> [Назад](accessing-your-models-data-from-a-controller.md)
> [Вперед](adding-search.md)
