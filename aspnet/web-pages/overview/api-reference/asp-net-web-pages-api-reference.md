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
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="51cb8-103">ASP.NET веб-страниц (Razor) API Быстрая справка</span><span class="sxs-lookup"><span data-stu-id="51cb8-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="51cb8-104">; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="51cb8-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="51cb8-105">Эта страница содержит список с краткими примерами наиболее часто используемых объектов, свойств и методов программирования ASP.NET веб-страниц с помощью синтаксиса Razor.</span><span class="sxs-lookup"><span data-stu-id="51cb8-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="51cb8-106">Описания с пометкой "(v2)" были представлены в версии ASP.NET веб-страниц 2.</span><span class="sxs-lookup"><span data-stu-id="51cb8-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="51cb8-107">Для справочной документации API с [ASP.NETм.](https://go.microsoft.com/fwlink/?LinkId=208659)</span><span class="sxs-lookup"><span data-stu-id="51cb8-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="51cb8-108">Версии программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="51cb8-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="51cb8-109">ASP.NET веб-страниц (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="51cb8-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="51cb8-110">Этот учебник также работает с ASP.NET web Pages 2 и ASP.NET Web Pages 1.0 (за исключением функций, отмеченных v2).</span><span class="sxs-lookup"><span data-stu-id="51cb8-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="51cb8-111">Эта страница содержит справочную информацию для следующих:</span><span class="sxs-lookup"><span data-stu-id="51cb8-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="51cb8-112">Классы</span><span class="sxs-lookup"><span data-stu-id="51cb8-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="51cb8-113">Data</span><span class="sxs-lookup"><span data-stu-id="51cb8-113">Data</span></span>](#Data)
- [<span data-ttu-id="51cb8-114">Вспомогательные методы</span><span class="sxs-lookup"><span data-stu-id="51cb8-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="51cb8-115">Проверка</span><span class="sxs-lookup"><span data-stu-id="51cb8-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="51cb8-116">Классы</span><span class="sxs-lookup"><span data-stu-id="51cb8-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="51cb8-117">Содержит данные, которыми могут поделиться любые страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="51cb8-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="51cb8-118">Динамическое `App` свойство можно использовать для доступа к тем же данным, что и в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="51cb8-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="51cb8-119">Преобразует значение строки в значение Boolean (истинное/ложное).</span><span class="sxs-lookup"><span data-stu-id="51cb8-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="51cb8-120">Возвращает ложное или указанное значение, если строка не представляет истинное/ложное значение.</span><span class="sxs-lookup"><span data-stu-id="51cb8-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="51cb8-121">Преобразует значение строки на дату/время.</span><span class="sxs-lookup"><span data-stu-id="51cb8-121">Converts a string value to date/time.</span></span> <span data-ttu-id="51cb8-122">Возвраты `DateTime.MinValue` или указанное значение, если строка не представляет дату/время.</span><span class="sxs-lookup"><span data-stu-id="51cb8-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="51cb8-123">Преобразует значение строки в десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="51cb8-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="51cb8-124">Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="51cb8-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="51cb8-125">Преобразует значение строки в поплавок.</span><span class="sxs-lookup"><span data-stu-id="51cb8-125">Converts a string value to a float.</span></span> <span data-ttu-id="51cb8-126">Возвращает 0,0 или указанное значение, если строка не представляет десятичное значение.</span><span class="sxs-lookup"><span data-stu-id="51cb8-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="51cb8-127">Преобразует значение строки в ряд.</span><span class="sxs-lookup"><span data-stu-id="51cb8-127">Converts a string value to an integer.</span></span> <span data-ttu-id="51cb8-128">Возвращает 0 или указанное значение, если строка не представляет собой ряд.</span><span class="sxs-lookup"><span data-stu-id="51cb8-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="51cb8-129">Создает совместимый с браузером URL-адрес из локального пути файла с дополнительными дополнительными частями пути.</span><span class="sxs-lookup"><span data-stu-id="51cb8-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="51cb8-130">Рендеризм *значение* как HTML разметка вместо того, чтобы отобразить его как HTML-закодированный выход.</span><span class="sxs-lookup"><span data-stu-id="51cb8-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="51cb8-131">Возвращает верно, если значение может быть преобразовано из строки в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="51cb8-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="51cb8-132">Возвращает верно, если объект или переменная не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="51cb8-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="51cb8-133">Возвращает верно, если запрос POST.</span><span class="sxs-lookup"><span data-stu-id="51cb8-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="51cb8-134">(Первоначальные запросы, как правило, GET.)</span><span class="sxs-lookup"><span data-stu-id="51cb8-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="51cb8-135">Онажаем путь страницы макета для применения к этой странице.</span><span class="sxs-lookup"><span data-stu-id="51cb8-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="51cb8-136">Содержит данные, общие между страницей, страницами макета и частичными страницами в текущем запросе.</span><span class="sxs-lookup"><span data-stu-id="51cb8-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="51cb8-137">Динамическое `Page` свойство можно использовать для доступа к тем же данным, что и в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="51cb8-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="51cb8-138">(Страницы для выкладки) Рендеринг содержимого страницы содержимого, не в которых не указаны разделы.</span><span class="sxs-lookup"><span data-stu-id="51cb8-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="51cb8-139">Рендеринг страницы содержимого с использованием заданного пути и дополнительных дополнительных данных.</span><span class="sxs-lookup"><span data-stu-id="51cb8-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="51cb8-140">Значения дополнительных параметров можно получить `PageData` из позиции (пример 1) или ключа (пример 2).</span><span class="sxs-lookup"><span data-stu-id="51cb8-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="51cb8-141">(Страницы для выкладки) Рендерс раздела содержимого с именем.</span><span class="sxs-lookup"><span data-stu-id="51cb8-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="51cb8-142">Набор *требуется* для ложного, чтобы сделать раздел необязательным.</span><span class="sxs-lookup"><span data-stu-id="51cb8-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="51cb8-143">Получает или устанавливает значение cookie HTTP.</span><span class="sxs-lookup"><span data-stu-id="51cb8-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="51cb8-144">Получает файлы, загруженные в текущем запросе.</span><span class="sxs-lookup"><span data-stu-id="51cb8-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="51cb8-145">Получает данные, которые были размещены в форме (в виде строк).</span><span class="sxs-lookup"><span data-stu-id="51cb8-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="51cb8-146">`Request[key]`проверяет как `Request.Form` коллекции, так и коллекции. `Request.QueryString`</span><span class="sxs-lookup"><span data-stu-id="51cb8-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="51cb8-147">Получает данные, указанные в строке запроса URL.</span><span class="sxs-lookup"><span data-stu-id="51cb8-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="51cb8-148">`Request[key]`проверяет как `Request.Form` коллекции, так и коллекции. `Request.QueryString`</span><span class="sxs-lookup"><span data-stu-id="51cb8-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="51cb8-149">Выборочно отстраняет проверку запроса на элемент формы, значение строки запроса, файлы cookie или значение заголовка.</span><span class="sxs-lookup"><span data-stu-id="51cb8-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="51cb8-150">Проверка запроса включена по умолчанию и не позволяет пользователям размещать разметку или другой потенциально опасный контент.</span><span class="sxs-lookup"><span data-stu-id="51cb8-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="51cb8-151">Добавляет заголовок сервера HTTP в ответ.</span><span class="sxs-lookup"><span data-stu-id="51cb8-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="51cb8-152">Кэшивывод вывода страницы в течение определенного времени.</span><span class="sxs-lookup"><span data-stu-id="51cb8-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="51cb8-153">Дополнительно установите *раздвижные,* чтобы сбросить тайм-аут на каждой странице доступа и *варьироватьByParams* кэшировать различные версии страницы для каждой строки запроса в запросе страницы.</span><span class="sxs-lookup"><span data-stu-id="51cb8-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="51cb8-154">Перенаправляет запрос браузера на новое место.</span><span class="sxs-lookup"><span data-stu-id="51cb8-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="51cb8-155">Устанавливает код состояния HTTP, отправленный в браузер.</span><span class="sxs-lookup"><span data-stu-id="51cb8-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="51cb8-156">Записывает содержимое *данных* в ответ с дополнительным типом MIME.</span><span class="sxs-lookup"><span data-stu-id="51cb8-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="51cb8-157">Записывает содержимое файла в ответ.</span><span class="sxs-lookup"><span data-stu-id="51cb8-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="51cb8-158">(Страницы для выкладки) Определяет раздел содержимого с именем.</span><span class="sxs-lookup"><span data-stu-id="51cb8-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="51cb8-159">Декодирует строку, которая закодирована HTML.</span><span class="sxs-lookup"><span data-stu-id="51cb8-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="51cb8-160">Кодирует строку для визуализации в HTML разметке.</span><span class="sxs-lookup"><span data-stu-id="51cb8-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="51cb8-161">Возвращает физический путь сервера для указанного виртуального пути.</span><span class="sxs-lookup"><span data-stu-id="51cb8-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="51cb8-162">Декодирует текст с URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="51cb8-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="51cb8-163">Закодирует текст для ввода URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="51cb8-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="51cb8-164">Получает или устанавливает значение, которое существует до тех пор, пока пользователь не закроет браузер.</span><span class="sxs-lookup"><span data-stu-id="51cb8-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="51cb8-165">Отображает строку, представленную значение объекта.</span><span class="sxs-lookup"><span data-stu-id="51cb8-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="51cb8-166">Получает дополнительные данные из URL (например, */MyPage/ExtraData).*</span><span class="sxs-lookup"><span data-stu-id="51cb8-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="51cb8-167">Изменяет пароль заданного пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="51cb8-168">Подтверждает учетную запись, используя токен подтверждения учетной записи.</span><span class="sxs-lookup"><span data-stu-id="51cb8-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="51cb8-169">Создает новую учетную запись пользователя с указанным именем пользователя и паролем.</span><span class="sxs-lookup"><span data-stu-id="51cb8-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="51cb8-170">Чтобы потребовать подтверждения токена, пройти верно для *requireConfirmationToken.*</span><span class="sxs-lookup"><span data-stu-id="51cb8-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="51cb8-171">Получает идентификатор integer для пользователя, зарегистрированного в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="51cb8-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="51cb8-172">Получает имя пользователя, зарегистрированного в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="51cb8-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="51cb8-173">Создает маркер сготовона паролей, который может быть отправлен по электронной почте пользователю, чтобы пользователь мог сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="51cb8-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="51cb8-174">Возвращает идентификатор пользователя с имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="51cb8-175">Возвращаетверно, если текущий пользователь входит в систему.</span><span class="sxs-lookup"><span data-stu-id="51cb8-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="51cb8-176">Возвращает верно, если пользователь был подтвержден (например, через подтверждение электронной почты).</span><span class="sxs-lookup"><span data-stu-id="51cb8-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="51cb8-177">Возвращается верно, если имя текущего пользователя совпадает с указанным именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="51cb8-178">Записи пользователя, установив маркер проверки подлинности в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="51cb8-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="51cb8-179">Записи пользователя, удалив маркер маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="51cb8-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="51cb8-180">Если пользователь не прошел проверку подлинности, задает состояние HTTP 401 (Не санкционировано).</span><span class="sxs-lookup"><span data-stu-id="51cb8-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="51cb8-181">Если текущий пользователь не является участником одной из указанных ролей, статус HTTP устанавливается до 401 (несанкционированно).</span><span class="sxs-lookup"><span data-stu-id="51cb8-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="51cb8-182">Если текущий пользователь не является пользователем, указанным *именем пользователя,* статус HTTP устанавливается до 401 (несанкционированно).</span><span class="sxs-lookup"><span data-stu-id="51cb8-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="51cb8-183">Если токен сготовона пароля действителен, изменяем пароль пользователя к новому паролю.</span><span class="sxs-lookup"><span data-stu-id="51cb8-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="51cb8-184">Данные</span><span class="sxs-lookup"><span data-stu-id="51cb8-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="51cb8-185">Выполняет *S'Lstatement* (с дополнительными параметрами), такими как INSERT, DELETE или UPDATE и возвращает количество затронутых записей.</span><span class="sxs-lookup"><span data-stu-id="51cb8-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="51cb8-186">Возвращает столбец идентификаторов из последней вставленной строки.</span><span class="sxs-lookup"><span data-stu-id="51cb8-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="51cb8-187">Открывает либо указанный файл базы данных, либо базу данных, указанную с помощью названной строки подключения из файла *Web.config.*</span><span class="sxs-lookup"><span data-stu-id="51cb8-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="51cb8-188">Открывает базу данных с помощью строки соединения.</span><span class="sxs-lookup"><span data-stu-id="51cb8-188">Opens a database using the connection string.</span></span> <span data-ttu-id="51cb8-189">(Это контрастирует `Database.Open`с , который использует имя строки соединения.)</span><span class="sxs-lookup"><span data-stu-id="51cb8-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="51cb8-190">Запрашивает базу данных с помощью *S'Lstatement* (по желанию проходящие параметры) и возвращает результаты в виде коллекции.</span><span class="sxs-lookup"><span data-stu-id="51cb8-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="51cb8-191">Выполняет *S'Lstatement* (с дополнительными параметрами) и возвращает одну запись.</span><span class="sxs-lookup"><span data-stu-id="51cb8-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="51cb8-192">Выполняет *S'Lstatement* (с дополнительными параметрами) и возвращает одно значение.</span><span class="sxs-lookup"><span data-stu-id="51cb8-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="51cb8-193">Вспомогательные методы</span><span class="sxs-lookup"><span data-stu-id="51cb8-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="51cb8-194">Рендеринг кода JavaScript Google Analytics для указанного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="51cb8-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="51cb8-195">Рендерс код JavaScript StatCounter Analytics для указанного проекта.</span><span class="sxs-lookup"><span data-stu-id="51cb8-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="51cb8-196">Рендерс Yahoo Analytics JavaScript код для указанной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="51cb8-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="51cb8-197">Проходит поиск в Bing.</span><span class="sxs-lookup"><span data-stu-id="51cb8-197">Passes a search to Bing.</span></span> <span data-ttu-id="51cb8-198">Чтобы указать сайт для поиска и название для окна `Bing.SiteUrl` `Bing.SiteTitle` поиска, можно установить и свойства.</span><span class="sxs-lookup"><span data-stu-id="51cb8-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="51cb8-199">Обычно эти свойства устанавливаются \* \_\* на странице AppStart.</span><span class="sxs-lookup"><span data-stu-id="51cb8-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="51cb8-200">Инициализирует диаграмму.</span><span class="sxs-lookup"><span data-stu-id="51cb8-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="51cb8-201">Добавляет легенду в диаграмму.</span><span class="sxs-lookup"><span data-stu-id="51cb8-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="51cb8-202">Добавляет ряд значений в диаграмму.</span><span class="sxs-lookup"><span data-stu-id="51cb8-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="51cb8-203">Возвращает хэш для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="51cb8-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="51cb8-204">Алгоритм по `sha256`умолчанию .</span><span class="sxs-lookup"><span data-stu-id="51cb8-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="51cb8-205">Позволяет пользователям Facebook установить подключение к страницам.</span><span class="sxs-lookup"><span data-stu-id="51cb8-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="51cb8-206">Рендерс ui для загрузки файлов.</span><span class="sxs-lookup"><span data-stu-id="51cb8-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="51cb8-207">Рендерс указанного тега геймера Xbox.</span><span class="sxs-lookup"><span data-stu-id="51cb8-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="51cb8-208">Рендеринг изображения Gravatar для указанного адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="51cb8-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="51cb8-209">Преобразует объект данных в строку в формате JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="51cb8-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="51cb8-210">Преобразует строку ввода, закодированную JSON, в объект данных, который можно итерировать или вставить в базу данных.</span><span class="sxs-lookup"><span data-stu-id="51cb8-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="51cb8-211">Renders социальных сетей ссылки, используя указанное название и дополнительный URL.</span><span class="sxs-lookup"><span data-stu-id="51cb8-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="51cb8-212">Связывает сообщение об ошибке с полем формы.</span><span class="sxs-lookup"><span data-stu-id="51cb8-212">Associates an error message with a form field.</span></span> <span data-ttu-id="51cb8-213">Используйте `ModelState` помощника, чтобы получить доступ к этому члену.</span><span class="sxs-lookup"><span data-stu-id="51cb8-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="51cb8-214">Связывает сообщение об ошибке с формой.</span><span class="sxs-lookup"><span data-stu-id="51cb8-214">Associates an error message with a form.</span></span> <span data-ttu-id="51cb8-215">Используйте `ModelState` помощника, чтобы получить доступ к этому члену.</span><span class="sxs-lookup"><span data-stu-id="51cb8-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="51cb8-216">Возвращает верно, если нет ошибок проверки.</span><span class="sxs-lookup"><span data-stu-id="51cb8-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="51cb8-217">Используйте `ModelState` помощника, чтобы получить доступ к этому члену.</span><span class="sxs-lookup"><span data-stu-id="51cb8-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="51cb8-218">Рендеринг свойств и значений объекта и любых детских объектов.</span><span class="sxs-lookup"><span data-stu-id="51cb8-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="51cb8-219">Рендеринг тест проверки reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="51cb8-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="51cb8-220">Устанавливает государственные и частные ключи для обслуживания reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="51cb8-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="51cb8-221">Обычно эти свойства устанавливаются \* \_\* на странице AppStart.</span><span class="sxs-lookup"><span data-stu-id="51cb8-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="51cb8-222">Возвращает результат ы теста reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="51cb8-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="51cb8-223">Рендеринг информации о состоянии ASP.NET веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="51cb8-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="51cb8-224">Рендерс поток Twitter для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="51cb8-225">Рендерс поток Twitter для указанного текста поиска.</span><span class="sxs-lookup"><span data-stu-id="51cb8-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="51cb8-226">Renders Flash видеоплеер для указанного файла с дополнительной шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="51cb8-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="51cb8-227">Renders проигрыватель Windows Media для указанного файла с дополнительной шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="51cb8-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="51cb8-228">Renders Silverlight для указанного файла *.xap* с необходимой шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="51cb8-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="51cb8-229">Возвращает объект, указанный *ключом,* или обнуляется, если объект не найден.</span><span class="sxs-lookup"><span data-stu-id="51cb8-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="51cb8-230">Удаляет объект, указанный *ключом,* из кэша.</span><span class="sxs-lookup"><span data-stu-id="51cb8-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="51cb8-231">Вкладывает *значение* в кэш под именем, указанным *ключом.*</span><span class="sxs-lookup"><span data-stu-id="51cb8-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="51cb8-232">Создает новый `WebGrid` объект, используя данные из запроса.</span><span class="sxs-lookup"><span data-stu-id="51cb8-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="51cb8-233">Рендеринг разметки для отображения данных в таблице HTML.</span><span class="sxs-lookup"><span data-stu-id="51cb8-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="51cb8-234">Рендерс пейджер `WebGrid` для объекта.</span><span class="sxs-lookup"><span data-stu-id="51cb8-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="51cb8-235">Загружает изображение с заданного пути.</span><span class="sxs-lookup"><span data-stu-id="51cb8-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="51cb8-236">Добавляет указанное изображение в качестве водяного знака.</span><span class="sxs-lookup"><span data-stu-id="51cb8-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="51cb8-237">Добавляет указанный текст к изображению.</span><span class="sxs-lookup"><span data-stu-id="51cb8-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="51cb8-238">Переворачивает изображение горизонтально или вертикально.</span><span class="sxs-lookup"><span data-stu-id="51cb8-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="51cb8-239">Загружает изображение при размещении изображения на странице во время загрузки файла.</span><span class="sxs-lookup"><span data-stu-id="51cb8-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="51cb8-240">Изображки изображения.</span><span class="sxs-lookup"><span data-stu-id="51cb8-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="51cb8-241">Вращает изображение влево или вправо.</span><span class="sxs-lookup"><span data-stu-id="51cb8-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="51cb8-242">Сохраняет изображение в указанном пути.</span><span class="sxs-lookup"><span data-stu-id="51cb8-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="51cb8-243">Устанавливает пароль для сервера SMTP.</span><span class="sxs-lookup"><span data-stu-id="51cb8-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="51cb8-244">Обычно это свойство устанавливается на \* \_странице AppStart.\*</span><span class="sxs-lookup"><span data-stu-id="51cb8-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="51cb8-245">Отправляет электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="51cb8-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="51cb8-246">Устанавливает имя сервера SMTP.</span><span class="sxs-lookup"><span data-stu-id="51cb8-246">Sets the SMTP server name.</span></span> <span data-ttu-id="51cb8-247">Обычно это свойство устанавливается на \* \_странице AppStart.\*</span><span class="sxs-lookup"><span data-stu-id="51cb8-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="51cb8-248">Устанавливает имя пользователя для сервера SMTP.</span><span class="sxs-lookup"><span data-stu-id="51cb8-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="51cb8-249">Обычно это свойство следует \* \_\* установить на странице AppStart.</span><span class="sxs-lookup"><span data-stu-id="51cb8-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="51cb8-250">Проверка</span><span class="sxs-lookup"><span data-stu-id="51cb8-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="51cb8-251">(v2) Рендеринг сообщения об ошибке проверки для указанного поля.</span><span class="sxs-lookup"><span data-stu-id="51cb8-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="51cb8-252">(v2) Отображает список всех ошибок проверки.</span><span class="sxs-lookup"><span data-stu-id="51cb8-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="51cb8-253">(v2) Регистрирует элемент ввода пользователя для заданного типа проверки.</span><span class="sxs-lookup"><span data-stu-id="51cb8-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="51cb8-254">(v2) Динамически отображает атрибуты класса CSS для проверки на стороне клиента, чтобы можно было форматировать сообщения об ошибке проверки.</span><span class="sxs-lookup"><span data-stu-id="51cb8-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="51cb8-255">(Требуется, чтобы вы ссылали соответствующие библиотеки клиент-скриптов и определить классы CSS.)</span><span class="sxs-lookup"><span data-stu-id="51cb8-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="51cb8-256">(v2) Позволяет проверить клиентскую проверку для поля ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="51cb8-257">(Требуется ссылка на соответствующие библиотеки клиент-скриптов.)</span><span class="sxs-lookup"><span data-stu-id="51cb8-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="51cb8-258">(v2) Возвращает верно, если все пользовательские элементы ввода, которые регистрируются для проверки содержат действительные значения.</span><span class="sxs-lookup"><span data-stu-id="51cb8-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="51cb8-259">(v2) Уточняется, что пользователи должны предоставить значение для элемента ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="51cb8-260">(v2) Уточняется, что пользователи должны предоставлять значения для каждого из элементов ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="51cb8-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="51cb8-261">Этот метод не позволяет указать пользовательское сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="51cb8-261">This method does not let you specify a custom error message.</span></span>

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

<span data-ttu-id="51cb8-262">(v2) При использовании `Validation.Add` метода упоняется тест проверки.</span><span class="sxs-lookup"><span data-stu-id="51cb8-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
