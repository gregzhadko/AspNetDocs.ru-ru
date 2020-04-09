---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET веб-страниц (Razor) API Быстрая справка (ru) Документы Майкрософт
author: Rick-Anderson
description: Эта страница содержит список с краткими примерами наиболее часто используемых объектов, свойств и методов программирования ASP.NET веб-страниц с помощью синтаксиса Razor.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675853"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET веб-страниц (Razor) API Быстрая справка

; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)

> Эта страница содержит список с краткими примерами наиболее часто используемых объектов, свойств и методов программирования ASP.NET веб-страниц с помощью синтаксиса Razor.
> 
> Описания с пометкой "(v2)" были представлены в версии ASP.NET веб-страниц 2.
> 
> Для справочной документации API с [ASP.NETм.](https://go.microsoft.com/fwlink/?LinkId=208659)
> 
> ## <a name="software-versions"></a>Версии программного обеспечения
> 
> 
> - ASP.NET веб-страниц (Razor) 3
>   
> 
> Этот учебник также работает с ASP.NET web Pages 2 и ASP.NET Web Pages 1.0 (за исключением функций, отмеченных v2).

Эта страница содержит справочную информацию для следующих:

- [Классы](#Classes)
- [Data](#Data)
- [Вспомогательные методы](#Helpers)
- [Проверка](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Классы

### `AppState[key], AppState[index],App`

Содержит данные, которыми могут поделиться любые страницы приложения. Динамическое `App` свойство можно использовать для доступа к тем же данным, что и в следующем примере:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Преобразует значение строки в значение Boolean (истинное/ложное). Возвращает ложное или указанное значение, если строка не представляет истинное/ложное значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Преобразует значение строки на дату/время. Возвраты `DateTime.MinValue` или указанное значение, если строка не представляет дату/время.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Преобразует значение строки в десятичное значение. Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Преобразует значение строки в поплавок. Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Преобразует значение строки в ряд. Возвращает 0 или указанное значение, если строка не представляет собой ряд.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

Создает совместимый с браузером URL-адрес из локального пути файла с дополнительными дополнительными частями пути.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

Рендеризм *значение* как HTML разметка вместо того, чтобы отобразить его как HTML-закодированный выход.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Возвращает верно, если значение может быть преобразовано из строки в указанный тип.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Возвращает верно, если объект или переменная не имеет значения.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

Возвращает верно, если запрос POST. (Первоначальные запросы, как правило, GET.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Онажаем путь страницы макета для применения к этой странице.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Содержит данные, общие между страницей, страницами макета и частичными страницами в текущем запросе. Динамическое `Page` свойство можно использовать для доступа к тем же данным, что и в следующем примере:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Страницы для выкладки) Рендеринг содержимого страницы содержимого, не в которых не указаны разделы.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Рендеринг страницы содержимого с использованием заданного пути и дополнительных дополнительных данных. Значения дополнительных параметров можно получить `PageData` из позиции (пример 1) или ключа (пример 2).

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Страницы для выкладки) Рендерс раздела содержимого с именем. Набор *требуется* для ложного, чтобы сделать раздел необязательным.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Получает или устанавливает значение cookie HTTP.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Получает файлы, загруженные в текущем запросе.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Получает данные, которые были размещены в форме (в виде строк). `Request[key]`проверяет как `Request.Form` коллекции, так и коллекции. `Request.QueryString`

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

Получает данные, указанные в строке запроса URL. `Request[key]`проверяет как `Request.Form` коллекции, так и коллекции. `Request.QueryString`

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Выборочно отстраняет проверку запроса на элемент формы, значение строки запроса, файлы cookie или значение заголовка. Проверка запроса включена по умолчанию и не позволяет пользователям размещать разметку или другой потенциально опасный контент.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Добавляет заголовок сервера HTTP в ответ.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Кэшивывод вывода страницы в течение определенного времени. Дополнительно установите *раздвижные,* чтобы сбросить тайм-аут на каждой странице доступа и *варьироватьByParams* кэшировать различные версии страницы для каждой строки запроса в запросе страницы.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Перенаправляет запрос браузера на новое место.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Устанавливает код состояния HTTP, отправленный в браузер.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

Записывает содержимое *данных* в ответ с дополнительным типом MIME.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Записывает содержимое файла в ответ.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Страницы для выкладки) Определяет раздел содержимого с именем.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

Декодирует строку, которая закодирована HTML.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

Кодирует строку для визуализации в HTML разметке.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Возвращает физический путь сервера для указанного виртуального пути.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

Декодирует текст с URL-адреса.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Закодирует текст для ввода URL-адреса.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Получает или устанавливает значение, которое существует до тех пор, пока пользователь не закроет браузер.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Отображает строку, представленную значение объекта.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

Получает дополнительные данные из URL (например, */MyPage/ExtraData).*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Изменяет пароль заданного пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Подтверждает учетную запись, используя токен подтверждения учетной записи.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Создает новую учетную запись пользователя с указанным именем пользователя и паролем. Чтобы потребовать подтверждения токена, пройти верно для *requireConfirmationToken.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Получает идентификатор integer для пользователя, зарегистрированного в настоящее время.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Получает имя пользователя, зарегистрированного в настоящее время.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Создает маркер сготовона паролей, который может быть отправлен по электронной почте пользователю, чтобы пользователь мог сбросить пароль.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Возвращает идентификатор пользователя с имени пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Возвращаетверно, если текущий пользователь входит в систему.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Возвращает верно, если пользователь был подтвержден (например, через подтверждение электронной почты).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Возвращается верно, если имя текущего пользователя совпадает с указанным именем пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Записи пользователя, установив маркер проверки подлинности в файле cookie.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Записи пользователя, удалив маркер маркера проверки подлинности.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Если пользователь не прошел проверку подлинности, задает состояние HTTP 401 (Не санкционировано).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Если текущий пользователь не является участником одной из указанных ролей, статус HTTP устанавливается до 401 (несанкционированно).

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Если текущий пользователь не является пользователем, указанным *именем пользователя,* статус HTTP устанавливается до 401 (несанкционированно).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Если токен сготовона пароля действителен, изменяем пароль пользователя к новому паролю.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Данные

### `Database.Execute(SQLstatement [,parameters]`

Выполняет *S'Lstatement* (с дополнительными параметрами), такими как INSERT, DELETE или UPDATE и возвращает количество затронутых записей.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

Возвращает столбец идентификаторов из последней вставленной строки.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Открывает либо указанный файл базы данных, либо базу данных, указанную с помощью названной строки подключения из файла *Web.config.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Открывает базу данных с помощью строки соединения. (Это контрастирует `Database.Open`с , который использует имя строки соединения.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

Запрашивает базу данных с помощью *S'Lstatement* (по желанию проходящие параметры) и возвращает результаты в виде коллекции.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

Выполняет *S'Lstatement* (с дополнительными параметрами) и возвращает одну запись.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

Выполняет *S'Lstatement* (с дополнительными параметрами) и возвращает одно значение.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Вспомогательные методы

### `Analytics.GetGoogleHtml(webPropertyId)`

Рендеринг кода JavaScript Google Analytics для указанного идентификатора.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Рендерс код JavaScript StatCounter Analytics для указанного проекта.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Рендерс Yahoo Analytics JavaScript код для указанной учетной записи.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Проходит поиск в Bing. Чтобы указать сайт для поиска и название для окна `Bing.SiteUrl` `Bing.SiteTitle` поиска, можно установить и свойства. Обычно эти свойства устанавливаются * \_* на странице AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Инициализирует диаграмму.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Добавляет легенду в диаграмму.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Добавляет ряд значений в диаграмму.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Возвращает хэш для указанных данных. Алгоритм по `sha256`умолчанию .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Позволяет пользователям Facebook установить подключение к страницам.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Рендерс ui для загрузки файлов.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Рендерс указанного тега геймера Xbox.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Рендеринг изображения Gravatar для указанного адреса электронной почты.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Преобразует объект данных в строку в формате JavaScript Object Notation (JSON).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

Преобразует строку ввода, закодированную JSON, в объект данных, который можно итерировать или вставить в базу данных.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Renders социальных сетей ссылки, используя указанное название и дополнительный URL.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Связывает сообщение об ошибке с полем формы. Используйте `ModelState` помощника, чтобы получить доступ к этому члену.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Связывает сообщение об ошибке с формой. Используйте `ModelState` помощника, чтобы получить доступ к этому члену.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Возвращает верно, если нет ошибок проверки. Используйте `ModelState` помощника, чтобы получить доступ к этому члену.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Рендеринг свойств и значений объекта и любых детских объектов.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

Рендеринг тест проверки reCAPTCHA.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

Устанавливает государственные и частные ключи для обслуживания reCAPTCHA. Обычно эти свойства устанавливаются * \_* на странице AppStart.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

Возвращает результат ы теста reCAPTCHA.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Рендеринг информации о состоянии ASP.NET веб-страниц.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Рендерс поток Twitter для указанного пользователя.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Рендерс поток Twitter для указанного текста поиска.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Renders Flash видеоплеер для указанного файла с дополнительной шириной и высотой.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Renders проигрыватель Windows Media для указанного файла с дополнительной шириной и высотой.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Renders Silverlight для указанного файла *.xap* с необходимой шириной и высотой.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

Возвращает объект, указанный *ключом,* или обнуляется, если объект не найден.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

Удаляет объект, указанный *ключом,* из кэша.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

Вкладывает *значение* в кэш под именем, указанным *ключом.*

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Создает новый `WebGrid` объект, используя данные из запроса.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Рендеринг разметки для отображения данных в таблице HTML.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Рендерс пейджер `WebGrid` для объекта.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Загружает изображение с заданного пути.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Добавляет указанное изображение в качестве водяного знака.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Добавляет указанный текст к изображению.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Переворачивает изображение горизонтально или вертикально.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Загружает изображение при размещении изображения на странице во время загрузки файла.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Изображки изображения.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Вращает изображение влево или вправо.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Сохраняет изображение в указанном пути.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

Устанавливает пароль для сервера SMTP. Обычно это свойство устанавливается на * \_странице AppStart.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Отправляет электронное сообщение.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

Устанавливает имя сервера SMTP. Обычно это свойство устанавливается на * \_странице AppStart.*

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

Устанавливает имя пользователя для сервера SMTP. Обычно это свойство следует * \_* установить на странице AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Проверка

### `Html.ValidationMessage(field)`

(v2) Рендеринг сообщения об ошибке проверки для указанного поля.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2) Отображает список всех ошибок проверки.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2) Регистрирует элемент ввода пользователя для заданного типа проверки.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2) Динамически отображает атрибуты класса CSS для проверки на стороне клиента, чтобы можно было форматировать сообщения об ошибке проверки. (Требуется, чтобы вы ссылали соответствующие библиотеки клиент-скриптов и определить классы CSS.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2) Позволяет проверить клиентскую проверку для поля ввода пользователя. (Требуется ссылка на соответствующие библиотеки клиент-скриптов.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2) Возвращает верно, если все пользовательские элементы ввода, которые регистрируются для проверки содержат действительные значения.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2) Уточняется, что пользователи должны предоставить значение для элемента ввода пользователя.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2) Уточняется, что пользователи должны предоставлять значения для каждого из элементов ввода пользователя. Этот метод не позволяет указать пользовательское сообщение об ошибке.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

(v2) При использовании `Validation.Add` метода упоняется тест проверки.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
