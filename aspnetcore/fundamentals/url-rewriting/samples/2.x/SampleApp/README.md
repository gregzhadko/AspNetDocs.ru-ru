---
ms.openlocfilehash: 4a4ad30846d1993b3e561c96c00fbf9a0c7f3929
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040811"
---
# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="4cc16-101">Пример переопределения URL-адресов ASP.NET Core (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="4cc16-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="4cc16-102">Этот пример иллюстрирует использование ПО промежуточного слоя для переопределения URL-адресов ASP.NET Core 2.x.</span><span class="sxs-lookup"><span data-stu-id="4cc16-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="4cc16-103">Это приложение демонстрирует варианты перенаправления и переопределения URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="4cc16-103">The app demonstrates URL redirect and URL rewriting options.</span></span>

<span data-ttu-id="4cc16-104">При запуске этого примера нефайловые отклики возвращают переопределенный или перенаправленный URL-адрес, если к URL-адресу запроса применяется одно из правил.</span><span class="sxs-lookup"><span data-stu-id="4cc16-104">When running the sample, non-file responses return the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span> <span data-ttu-id="4cc16-105">Для примеров текстовых или XML-файлов ПО промежуточного слоя статических файлов обслуживает файл после того, как ПО промежуточного слоя переопределяет URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="4cc16-105">For the XML and text file examples, Static File Middleware serves the file after the request URL is rewritten by the middleware.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="4cc16-106">Включенные примеры</span><span class="sxs-lookup"><span data-stu-id="4cc16-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="4cc16-107">Код состояния успеха: 302 (найдено)</span><span class="sxs-lookup"><span data-stu-id="4cc16-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="4cc16-108">Пример (перенаправление): **/redirect-rule/{группа_записи}** в **/redirected/{группа_записи}**</span><span class="sxs-lookup"><span data-stu-id="4cc16-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="4cc16-109">Код состояния успеха: 200 (ОК)</span><span class="sxs-lookup"><span data-stu-id="4cc16-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="4cc16-110">Пример (переопределение): **/rewrite-rule/{группа_записи_1}/{группа_записи_2}** в **/rewritten?var1={группа_записи_1}&var2={группа_записи_2}**</span><span class="sxs-lookup"><span data-stu-id="4cc16-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="4cc16-111">Код состояния успеха: 302 (найдено)</span><span class="sxs-lookup"><span data-stu-id="4cc16-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="4cc16-112">Пример (перенаправление): **/apache-mod-rules-redirect/{группа_записи}** в **/redirected?id={группа_записи}**</span><span class="sxs-lookup"><span data-stu-id="4cc16-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="4cc16-113">Код состояния успеха: 200 (ОК)</span><span class="sxs-lookup"><span data-stu-id="4cc16-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="4cc16-114">Пример (переопределение): **/iis-rules-rewrite/{группа_записи}** в **/rewritten?id={группа_записи}**</span><span class="sxs-lookup"><span data-stu-id="4cc16-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXmlFileRequests)`
  - <span data-ttu-id="4cc16-115">Код состояния успеха: 301 (перемещен окончательно)</span><span class="sxs-lookup"><span data-stu-id="4cc16-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="4cc16-116">Пример (перенаправление): **/file.xml** в **/xmlfiles/file.xml**</span><span class="sxs-lookup"><span data-stu-id="4cc16-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(RewriteTextFileRequests)`
  - <span data-ttu-id="4cc16-117">Код состояния успеха: 200 (ОК)</span><span class="sxs-lookup"><span data-stu-id="4cc16-117">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="4cc16-118">Пример (переопределение): **/some_file.txt** в **/file.txt**</span><span class="sxs-lookup"><span data-stu-id="4cc16-118">Example (rewrite): **/some_file.txt** to **/file.txt**</span></span>
* `Add(new RedirectImageRequests(".png", "/png-images")))`<br>`Add(new RedirectImageRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="4cc16-119">Код состояния успеха: 301 (перемещен окончательно)</span><span class="sxs-lookup"><span data-stu-id="4cc16-119">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="4cc16-120">Пример (перенаправление): **/image.png** в **/png-images/image.png**</span><span class="sxs-lookup"><span data-stu-id="4cc16-120">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="4cc16-121">Пример (перенаправление): **/image.jpg** в **/jpg-images/image.jpg**</span><span class="sxs-lookup"><span data-stu-id="4cc16-121">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="use-a-physicalfileprovider"></a><span data-ttu-id="4cc16-122">Использование PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="4cc16-122">Use a PhysicalFileProvider</span></span>

<span data-ttu-id="4cc16-123">Вы также можете получить `IFileProvider`, создав `PhysicalFileProvider` для передачи в методы `AddApacheModRewrite()` и `AddIISUrlRewrite()`:</span><span class="sxs-lookup"><span data-stu-id="4cc16-123">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>

```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```

## <a name="secure-redirection-extensions"></a><span data-ttu-id="4cc16-124">Расширения безопасного перенаправления</span><span class="sxs-lookup"><span data-stu-id="4cc16-124">Secure redirection extensions</span></span>

<span data-ttu-id="4cc16-125">Этот пример включает в себя конфигурацию `WebHostBuilder`, чтобы приложение использовало URL-адреса (`https://localhost:5001`, `https://localhost`), и тестовый сертификат (*testCert.pfx*) с целью помочь вам в изучении этих методов безопасного перенаправления.</span><span class="sxs-lookup"><span data-stu-id="4cc16-125">This sample includes `WebHostBuilder` configuration for the app to use URLs (`https://localhost:5001`, `https://localhost`) and a test certificate (*testCert.pfx*) to assist in exploring the secure redirect methods.</span></span> <span data-ttu-id="4cc16-126">Если порт 443 на сервере уже назначен или используется, пример `https://localhost` не работает &mdash; нужно удалить `ListenOptions` для порта 443 в методе `CreateWebHostBuilder` файла *Program.cs* или отменить привязку порта 443 на сервере, чтобы Kestrel мог использовать этот порт.</span><span class="sxs-lookup"><span data-stu-id="4cc16-126">If the server already has port 443 assigned or in use, the `https://localhost` example doesn't work&mdash;remove the `ListenOptions` for port 443 in the `CreateWebHostBuilder` method of the *Program.cs* file or unbind port 443 on the server so that Kestrel can use the port.</span></span>

| <span data-ttu-id="4cc16-127">Метод</span><span class="sxs-lookup"><span data-stu-id="4cc16-127">Method</span></span>                           | <span data-ttu-id="4cc16-128">Код состояния</span><span class="sxs-lookup"><span data-stu-id="4cc16-128">Status Code</span></span> |    <span data-ttu-id="4cc16-129">Порт</span><span class="sxs-lookup"><span data-stu-id="4cc16-129">Port</span></span>    |
| -------------------------------- | :---------: | :--------: |
| `.AddRedirectToHttpsPermanent()` |     <span data-ttu-id="4cc16-130">301</span><span class="sxs-lookup"><span data-stu-id="4cc16-130">301</span></span>     | <span data-ttu-id="4cc16-131">null (465)</span><span class="sxs-lookup"><span data-stu-id="4cc16-131">null (465)</span></span> |
| `.AddRedirectToHttps()`          |     <span data-ttu-id="4cc16-132">302</span><span class="sxs-lookup"><span data-stu-id="4cc16-132">302</span></span>     | <span data-ttu-id="4cc16-133">null (465)</span><span class="sxs-lookup"><span data-stu-id="4cc16-133">null (465)</span></span> |
| `.AddRedirectToHttps(301)`       |     <span data-ttu-id="4cc16-134">301</span><span class="sxs-lookup"><span data-stu-id="4cc16-134">301</span></span>     | <span data-ttu-id="4cc16-135">null (465)</span><span class="sxs-lookup"><span data-stu-id="4cc16-135">null (465)</span></span> |
| `.AddRedirectToHttps(301, 5001)` |     <span data-ttu-id="4cc16-136">301</span><span class="sxs-lookup"><span data-stu-id="4cc16-136">301</span></span>     |    <span data-ttu-id="4cc16-137">5001</span><span class="sxs-lookup"><span data-stu-id="4cc16-137">5001</span></span>    |
