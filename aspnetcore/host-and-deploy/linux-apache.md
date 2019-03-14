---
title: Размещение ASP.NET Core в операционной системе Linux с Apache
description: Процедура настройки Apache в качестве обратного прокси-сервера в CentOS для перенаправления трафика HTTP в веб-приложение ASP.NET Core, выполняемое в Kestrel.
author: spboyer
ms.author: spboyer
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 0dec9c657134bba3224a1fbb69aaefaaba753404
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026491"
---
# <a name="host-aspnet-core-on-linux-with-apache"></a><span data-ttu-id="629e4-103">Размещение ASP.NET Core в операционной системе Linux с Apache</span><span class="sxs-lookup"><span data-stu-id="629e4-103">Host ASP.NET Core on Linux with Apache</span></span>

<span data-ttu-id="629e4-104">Автор: [Шейн Бойер (Shayne Boyer)](https://github.com/spboyer)</span><span class="sxs-lookup"><span data-stu-id="629e4-104">By [Shayne Boyer](https://github.com/spboyer)</span></span>

<span data-ttu-id="629e4-105">Из этого руководства вы узнаете, как настроить [Apache](https://httpd.apache.org/) в качестве обратного прокси-сервера в [CentOS 7](https://www.centos.org/) для перенаправления трафика HTTP в веб-приложение ASP.NET Core, выполняемое на сервере [Kestrel](xref:fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="629e4-105">Using this guide, learn how to set up [Apache](https://httpd.apache.org/) as a reverse proxy server on [CentOS 7](https://www.centos.org/) to redirect HTTP traffic to an ASP.NET Core web app running on [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span> <span data-ttu-id="629e4-106">[Расширение mod_proxy](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) и связанные с ним модули создают обратный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="629e4-106">The [mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) and related modules create the server's reverse proxy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="629e4-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="629e4-107">Prerequisites</span></span>

* <span data-ttu-id="629e4-108">Сервер под управлением CentOS 7 и учетная запись обычного пользователя с правами sudo.</span><span class="sxs-lookup"><span data-stu-id="629e4-108">Server running CentOS 7 with a standard user account with sudo privilege.</span></span>
* <span data-ttu-id="629e4-109">Установите среду выполнения .NET Core на сервере.</span><span class="sxs-lookup"><span data-stu-id="629e4-109">Install the .NET Core runtime on the server.</span></span>
   1. <span data-ttu-id="629e4-110">Перейдите на [страницу всех загрузок .NET Core](https://www.microsoft.com/net/download/all).</span><span class="sxs-lookup"><span data-stu-id="629e4-110">Visit the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>
   1. <span data-ttu-id="629e4-111">Выберите последнюю не предварительную версию среды выполнения из списка под заголовком **Среда выполнения**.</span><span class="sxs-lookup"><span data-stu-id="629e4-111">Select the latest non-preview runtime from the list under **Runtime**.</span></span>
   1. <span data-ttu-id="629e4-112">Сделайте выбор и следуйте инструкциям для CentOS/Oracle.</span><span class="sxs-lookup"><span data-stu-id="629e4-112">Select and follow the instructions for CentOS/Oracle.</span></span>
* <span data-ttu-id="629e4-113">Существующее приложение ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="629e4-113">An existing ASP.NET Core app.</span></span>

## <a name="publish-and-copy-over-the-app"></a><span data-ttu-id="629e4-114">Публикация и копирование приложения</span><span class="sxs-lookup"><span data-stu-id="629e4-114">Publish and copy over the app</span></span>

<span data-ttu-id="629e4-115">Настройте приложение, чтобы [его развертывание зависело от платформы](/dotnet/core/deploying/#framework-dependent-deployments-fdd).</span><span class="sxs-lookup"><span data-stu-id="629e4-115">Configure the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd).</span></span>

<span data-ttu-id="629e4-116">Запустите [dotnet publish](/dotnet/core/tools/dotnet-publish) в среде разработки, чтобы упаковать приложение в каталог (например, *bin/Release/&lt;target_framework_moniker&gt;/publish*), который может выполняться на сервере:</span><span class="sxs-lookup"><span data-stu-id="629e4-116">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the development environment to package an app into a directory (for example, *bin/Release/&lt;target_framework_moniker&gt;/publish*) that can run on the server:</span></span>

```console
dotnet publish --configuration Release
```

<span data-ttu-id="629e4-117">Приложение может быть опубликовано как [автономное развертывание](/dotnet/core/deploying/#self-contained-deployments-scd), если вы предпочитаете не сохранять среду выполнения .NET Core на сервере.</span><span class="sxs-lookup"><span data-stu-id="629e4-117">The app can also be published as a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) if you prefer not to maintain the .NET Core runtime on the server.</span></span>

<span data-ttu-id="629e4-118">Скопируйте приложение ASP.NET Core на сервер с помощью инструмента, интегрированного в ваш рабочий процесс (например, SCP или SFTP).</span><span class="sxs-lookup"><span data-stu-id="629e4-118">Copy the ASP.NET Core app to the server using a tool that integrates into the organization's workflow (for example, SCP, SFTP).</span></span> <span data-ttu-id="629e4-119">Обычно веб-приложения находятся в каталоге *var* (например, *var/www/helloapp*).</span><span class="sxs-lookup"><span data-stu-id="629e4-119">It's common to locate web apps under the *var* directory (for example, *var/www/helloapp*).</span></span>

> [!NOTE]
> <span data-ttu-id="629e4-120">Если развертывание выполняется в рабочей среде, рабочий процесс непрерывной интеграции автоматически опубликует приложение и скопирует его ресурсы на сервер.</span><span class="sxs-lookup"><span data-stu-id="629e4-120">Under a production deployment scenario, a continuous integration workflow does the work of publishing the app and copying the assets to the server.</span></span>

## <a name="configure-a-proxy-server"></a><span data-ttu-id="629e4-121">Настройка прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="629e4-121">Configure a proxy server</span></span>

<span data-ttu-id="629e4-122">Обратный прокси-сервер — это стандартный вариант настройки для обслуживания динамических веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="629e4-122">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="629e4-123">Обратный прокси-сервер завершает HTTP-запрос и перенаправляет его в приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="629e4-123">The reverse proxy terminates the HTTP request and forwards it to the ASP.NET app.</span></span>

<span data-ttu-id="629e4-124">Прокси-сервер перенаправляет запросы клиента на другой сервер, а не обрабатывает их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="629e4-124">A proxy server is one which forwards client requests to another server instead of fulfilling requests itself.</span></span> <span data-ttu-id="629e4-125">Обратный прокси-сервер перенаправляет запросы в фиксированное назначение обычно от имени клиентов.</span><span class="sxs-lookup"><span data-stu-id="629e4-125">A reverse proxy forwards to a fixed destination, typically on behalf of arbitrary clients.</span></span> <span data-ttu-id="629e4-126">При работе с этим руководством мы настроим Apache в качестве обратного прокси-сервера, который работает на том же сервере, где Kestrel предоставляет приложение ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="629e4-126">In this guide, Apache is configured as the reverse proxy running on the same server that Kestrel is serving the ASP.NET Core app.</span></span>

<span data-ttu-id="629e4-127">Так как запросы перенаправляются обратным прокси-сервером, используйте [ПО промежуточного слоя перенаправления заголовков](xref:host-and-deploy/proxy-load-balancer), которое входит в пакет [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/).</span><span class="sxs-lookup"><span data-stu-id="629e4-127">Because requests are forwarded by reverse proxy, use the [Forwarded Headers Middleware](xref:host-and-deploy/proxy-load-balancer) from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="629e4-128">Это ПО обновляет `Request.Scheme`, используя заголовок `X-Forwarded-Proto`, что обеспечивает правильную работу URI перенаправления и других политик безопасности.</span><span class="sxs-lookup"><span data-stu-id="629e4-128">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="629e4-129">Любой компонент, который зависит от схемы, например проверка подлинности, генерация ссылок, перенаправление и геолокация, должен находиться после вызова ПО промежуточного слоя перенаправления заголовков.</span><span class="sxs-lookup"><span data-stu-id="629e4-129">Any component that depends on the scheme, such as authentication, link generation, redirects, and geolocation, must be placed after invoking the Forwarded Headers Middleware.</span></span> <span data-ttu-id="629e4-130">Как правило, ПО промежуточного слоя перенаправления заголовков должно выполняться до остального ПО промежуточного слоя, за исключением ПО промежуточного слоя для диагностики и обработки ошибок.</span><span class="sxs-lookup"><span data-stu-id="629e4-130">As a general rule, Forwarded Headers Middleware should run before other middleware except diagnostics and error handling middleware.</span></span> <span data-ttu-id="629e4-131">Такой порядок гарантирует, что ПО промежуточного слоя, полагающееся на сведения о перенаправленных заголовках, может использовать значения заголовков для обработки.</span><span class="sxs-lookup"><span data-stu-id="629e4-131">This ordering ensures that the middleware relying on forwarded headers information can consume the header values for processing.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="629e4-132">Вызовите метод <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> в методе `Startup.Configure` перед вызовом <xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*> или другого ПО промежуточного слоя, предназначенного для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="629e4-132">Invoke the <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> method in `Startup.Configure` before calling <xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*> or similar authentication scheme middleware.</span></span> <span data-ttu-id="629e4-133">В ПО промежуточного слоя настройте перенаправление заголовков `X-Forwarded-For` и `X-Forwarded-Proto`:</span><span class="sxs-lookup"><span data-stu-id="629e4-133">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="629e4-134">Вызовите метод <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> в методе `Startup.Configure` перед вызовом <xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*> и <xref:Microsoft.AspNetCore.Builder.FacebookAppBuilderExtensions.UseFacebookAuthentication*> или другого ПО промежуточного слоя, предназначенного для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="629e4-134">Invoke the <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> method in `Startup.Configure` before calling <xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*> and <xref:Microsoft.AspNetCore.Builder.FacebookAppBuilderExtensions.UseFacebookAuthentication*> or similar authentication scheme middleware.</span></span> <span data-ttu-id="629e4-135">В ПО промежуточного слоя настройте перенаправление заголовков `X-Forwarded-For` и `X-Forwarded-Proto`:</span><span class="sxs-lookup"><span data-stu-id="629e4-135">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

::: moniker-end

<span data-ttu-id="629e4-136">Если параметр <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions> не задан для ПО промежуточного слоя, по умолчанию перенаправляются заголовки `None`.</span><span class="sxs-lookup"><span data-stu-id="629e4-136">If no <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions> are specified to the middleware, the default headers to forward are `None`.</span></span>

<span data-ttu-id="629e4-137">По умолчанию доверенными считаются только прокси-серверы, работающие на localhost (127.0.0.1, [:: 1]).</span><span class="sxs-lookup"><span data-stu-id="629e4-137">Only proxies running on localhost (127.0.0.1, [::1]) are trusted by default.</span></span> <span data-ttu-id="629e4-138">Если запросы между Интернетом и веб-сервером обрабатывают другие прокси-серверы или сети организации, добавьте их в список <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> или <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> с помощью <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions>.</span><span class="sxs-lookup"><span data-stu-id="629e4-138">If other trusted proxies or networks within the organization handle requests between the Internet and the web server, add them to the list of <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> or <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> with <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions>.</span></span> <span data-ttu-id="629e4-139">Следующий пример добавляет доверенный прокси-сервер с IP-адресом 10.0.0.100 в ПО промежуточного слоя для перенаправления заголовков `KnownProxies` в `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="629e4-139">The following example adds a trusted proxy server at IP address 10.0.0.100 to the Forwarded Headers Middleware `KnownProxies` in `Startup.ConfigureServices`:</span></span>

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.KnownProxies.Add(IPAddress.Parse("10.0.0.100"));
});
```

<span data-ttu-id="629e4-140">Дополнительные сведения см. в разделе <xref:host-and-deploy/proxy-load-balancer>.</span><span class="sxs-lookup"><span data-stu-id="629e4-140">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

### <a name="install-apache"></a><span data-ttu-id="629e4-141">Установка Apache</span><span class="sxs-lookup"><span data-stu-id="629e4-141">Install Apache</span></span>

<span data-ttu-id="629e4-142">Обновите пакеты CentOS до последних стабильных версий:</span><span class="sxs-lookup"><span data-stu-id="629e4-142">Update CentOS packages to their latest stable versions:</span></span>

```bash
sudo yum update -y
```

<span data-ttu-id="629e4-143">Установите веб-сервер Apache на CentOS, выполнив одну команду `yum`:</span><span class="sxs-lookup"><span data-stu-id="629e4-143">Install the Apache web server on CentOS with a single `yum` command:</span></span>

```bash
sudo yum -y install httpd mod_ssl
```

<span data-ttu-id="629e4-144">Пример выходных данных этой команды:</span><span class="sxs-lookup"><span data-stu-id="629e4-144">Sample output after running the command:</span></span>

```bash
Downloading packages:
httpd-2.4.6-40.el7.centos.4.x86_64.rpm               | 2.7 MB  00:00:01
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Installing : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 
Verifying  : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 

Installed:
httpd.x86_64 0:2.4.6-40.el7.centos.4

Complete!
```

> [!NOTE]
> <span data-ttu-id="629e4-145">В нашем примере выходные данные содержат строку httpd.86_64, так как используется 64-разрядная версия CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="629e4-145">In this example, the output reflects httpd.86_64 since the CentOS 7 version is 64 bit.</span></span> <span data-ttu-id="629e4-146">Чтобы проверить, где установлен Apache, выполните `whereis httpd` из командной строки.</span><span class="sxs-lookup"><span data-stu-id="629e4-146">To verify where Apache is installed, run `whereis httpd` from a command prompt.</span></span>

### <a name="configure-apache"></a><span data-ttu-id="629e4-147">Настройка Apache</span><span class="sxs-lookup"><span data-stu-id="629e4-147">Configure Apache</span></span>

<span data-ttu-id="629e4-148">Файлы конфигурации для Apache находятся в каталоге `/etc/httpd/conf.d/`.</span><span class="sxs-lookup"><span data-stu-id="629e4-148">Configuration files for Apache are located within the `/etc/httpd/conf.d/` directory.</span></span> <span data-ttu-id="629e4-149">В алфавитном порядке обрабатываются все файлы с расширением *.conf*, а также файлы конфигурации модуля из папки `/etc/httpd/conf.modules.d/`, где содержатся файлы конфигурации, необходимые для загрузки модулей.</span><span class="sxs-lookup"><span data-stu-id="629e4-149">Any file with the *.conf* extension is processed in alphabetical order in addition to the module configuration files in `/etc/httpd/conf.modules.d/`, which contains any configuration files necessary to load modules.</span></span>

<span data-ttu-id="629e4-150">Создайте для приложения файл конфигурации с именем *helloapp.conf*:</span><span class="sxs-lookup"><span data-stu-id="629e4-150">Create a configuration file, named *helloapp.conf*, for the app:</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ServerName www.example.com
    ServerAlias *.example.com
    ErrorLog ${APACHE_LOG_DIR}helloapp-error.log
    CustomLog ${APACHE_LOG_DIR}helloapp-access.log common
</VirtualHost>
```

<span data-ttu-id="629e4-151">Блок `VirtualHost` может встречаться несколько раз в одном или нескольких файлах на сервере.</span><span class="sxs-lookup"><span data-stu-id="629e4-151">The `VirtualHost` block can appear multiple times, in one or more files on a server.</span></span> <span data-ttu-id="629e4-152">С представленным выше файлом конфигурации Apache принимает трафик от любого источника через порт 80.</span><span class="sxs-lookup"><span data-stu-id="629e4-152">In the preceding configuration file, Apache accepts public traffic on port 80.</span></span> <span data-ttu-id="629e4-153">Он обслуживает домен `www.example.com`, а псевдоним `*.example.com` указывает на тот же веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="629e4-153">The domain `www.example.com` is being served, and the `*.example.com` alias resolves to the same website.</span></span> <span data-ttu-id="629e4-154">Дополнительные сведения см. в статье [о поддержке виртуальных узлов на основе имен](https://httpd.apache.org/docs/current/vhosts/name-based.html).</span><span class="sxs-lookup"><span data-stu-id="629e4-154">See [Name-based virtual host support](https://httpd.apache.org/docs/current/vhosts/name-based.html) for more information.</span></span> <span data-ttu-id="629e4-155">Запросы к корневому каталогу перенаправляются на порт 5000 того же сервера по адресу 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="629e4-155">Requests are proxied at the root to port 5000 of the server at 127.0.0.1.</span></span> <span data-ttu-id="629e4-156">Для двусторонней связи требуются `ProxyPass` и `ProxyPassReverse`.</span><span class="sxs-lookup"><span data-stu-id="629e4-156">For bi-directional communication, `ProxyPass` and `ProxyPassReverse` are required.</span></span> <span data-ttu-id="629e4-157">Сведения о том, как изменить IP-адрес/порт Kestrel, см. в разделе [Kestrel: конфигурация конечной точки](xref:fundamentals/servers/kestrel#endpoint-configuration).</span><span class="sxs-lookup"><span data-stu-id="629e4-157">To change Kestrel's IP/port, see [Kestrel: Endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>

> [!WARNING]
> <span data-ttu-id="629e4-158">Если не удастся указать правильную [директиву ServerName](https://httpd.apache.org/docs/current/mod/core.html#servername) в блоке **VirtualHost**, приложение будет иметь значительные уязвимости.</span><span class="sxs-lookup"><span data-stu-id="629e4-158">Failure to specify a proper [ServerName directive](https://httpd.apache.org/docs/current/mod/core.html#servername) in the **VirtualHost** block exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="629e4-159">Привязки с подстановочными знаками на уровне дочерних доменов (например, `*.example.com`) не создают таких угроз безопасности, если вы полностью контролируете родительский домен (в отличие от варианта `*.com`, создающего уязвимость).</span><span class="sxs-lookup"><span data-stu-id="629e4-159">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="629e4-160">Дополнительные сведения см. в документе [rfc7230, раздел 5.4](https://tools.ietf.org/html/rfc7230#section-5.4).</span><span class="sxs-lookup"><span data-stu-id="629e4-160">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="629e4-161">Ведение журнала можно настроить отдельно для каждого `VirtualHost` с помощью директив `ErrorLog` и `CustomLog`.</span><span class="sxs-lookup"><span data-stu-id="629e4-161">Logging can be configured per `VirtualHost` using `ErrorLog` and `CustomLog` directives.</span></span> <span data-ttu-id="629e4-162">Журналы ошибок сохраняются в расположение `ErrorLog`, а параметр `CustomLog` задает имя и формат для файла журнала.</span><span class="sxs-lookup"><span data-stu-id="629e4-162">`ErrorLog` is the location where the server logs errors, and `CustomLog` sets the filename and format of log file.</span></span> <span data-ttu-id="629e4-163">В нашем примере здесь фиксируются сведения о запросах.</span><span class="sxs-lookup"><span data-stu-id="629e4-163">In this case, this is where request information is logged.</span></span> <span data-ttu-id="629e4-164">Для каждого запроса создается одна строка.</span><span class="sxs-lookup"><span data-stu-id="629e4-164">There's one line for each request.</span></span>

<span data-ttu-id="629e4-165">Сохраните файл и протестируйте конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="629e4-165">Save the file and test the configuration.</span></span> <span data-ttu-id="629e4-166">Если проверка выполнена успешно, ответ должен быть `Syntax [OK]`.</span><span class="sxs-lookup"><span data-stu-id="629e4-166">If everything passes, the response should be `Syntax [OK]`.</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="629e4-167">Перезапустите Apache.</span><span class="sxs-lookup"><span data-stu-id="629e4-167">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitor-the-app"></a><span data-ttu-id="629e4-168">Мониторинг приложения</span><span class="sxs-lookup"><span data-stu-id="629e4-168">Monitor the app</span></span>

<span data-ttu-id="629e4-169">Теперь Apache настроен на перенаправление запросов к `http://localhost:80` в приложение ASP.NET Core, выполняемое в Kestrel по адресу `http://127.0.0.1:5000`.</span><span class="sxs-lookup"><span data-stu-id="629e4-169">Apache is now setup to forward requests made to `http://localhost:80` to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span> <span data-ttu-id="629e4-170">Но Apache не настроен для управления процессом Kestrel.</span><span class="sxs-lookup"><span data-stu-id="629e4-170">However, Apache isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="629e4-171">Для запуска и мониторинга базового веб-приложения используйте *systemd* и создайте файл службы.</span><span class="sxs-lookup"><span data-stu-id="629e4-171">Use *systemd* and create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="629e4-172">*systemd* — это система инициализации, предоставляющая различные функции для запуска и остановки процессов, а также управления ими.</span><span class="sxs-lookup"><span data-stu-id="629e4-172">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span>

### <a name="create-the-service-file"></a><span data-ttu-id="629e4-173">Создание файла службы</span><span class="sxs-lookup"><span data-stu-id="629e4-173">Create the service file</span></span>

<span data-ttu-id="629e4-174">Создайте файл определения службы.</span><span class="sxs-lookup"><span data-stu-id="629e4-174">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-helloapp.service
```

<span data-ttu-id="629e4-175">Пример файла службы для приложения:</span><span class="sxs-lookup"><span data-stu-id="629e4-175">An example service file for the app:</span></span>

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/www/helloapp
ExecStart=/usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

<span data-ttu-id="629e4-176">Если пользователь *apache* в вашей конфигурации еще не используется, его необходимо создать и правильно предоставить ему права владения для соответствующих файлов.</span><span class="sxs-lookup"><span data-stu-id="629e4-176">If the user *apache* isn't used by the configuration, the user must be created first and given proper ownership of files.</span></span>

<span data-ttu-id="629e4-177">Используйте `TimeoutStopSec`, чтобы настроить время ожидания до завершения работы приложения после начального сигнала прерывания.</span><span class="sxs-lookup"><span data-stu-id="629e4-177">Use `TimeoutStopSec` to configure the duration of time to wait for the app to shut down after it receives the initial interrupt signal.</span></span> <span data-ttu-id="629e4-178">Если приложение не завершит работу в течение этого периода, оно прерывается сигналом SIGKILL.</span><span class="sxs-lookup"><span data-stu-id="629e4-178">If the app doesn't shut down in this period, SIGKILL is issued to terminate the app.</span></span> <span data-ttu-id="629e4-179">Укажите значение в секундах без единиц измерения (например, `150`), значение интервала (например, `2min 30s`) или значение `infinity`, которое отключает время ожидания.</span><span class="sxs-lookup"><span data-stu-id="629e4-179">Provide the value as unitless seconds (for example, `150`), a time span value (for example, `2min 30s`), or `infinity` to disable the timeout.</span></span> <span data-ttu-id="629e4-180">По умолчанию `TimeoutStopSec` принимает значение `DefaultTimeoutStopSec` в файле конфигурации диспетчера (*systemd-system.conf*, *system.conf.d*, *systemd-user.conf*, *user.conf.d*).</span><span class="sxs-lookup"><span data-stu-id="629e4-180">`TimeoutStopSec` defaults to the value of `DefaultTimeoutStopSec` in the manager configuration file (*systemd-system.conf*, *system.conf.d*, *systemd-user.conf*, *user.conf.d*).</span></span> <span data-ttu-id="629e4-181">В большинстве дистрибутивов по умолчанию устанавливается время ожидания 90 секунд.</span><span class="sxs-lookup"><span data-stu-id="629e4-181">The default timeout for most distributions is 90 seconds.</span></span>

```
# The default value is 90 seconds for most distributions.
TimeoutStopSec=90
```

<span data-ttu-id="629e4-182">Некоторые значения (например, строки подключения SQL) необходимо экранировать, чтобы поставщики конфигурации могли считать переменные среды.</span><span class="sxs-lookup"><span data-stu-id="629e4-182">Some values (for example, SQL connection strings) must be escaped for the configuration providers to read the environment variables.</span></span> <span data-ttu-id="629e4-183">Используйте следующую команду, чтобы создать правильно экранированное значение для файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="629e4-183">Use the following command to generate a properly escaped value for use in the configuration file:</span></span>

```console
systemd-escape "<value-to-escape>"
```

<span data-ttu-id="629e4-184">Сохраните файл и включите службу.</span><span class="sxs-lookup"><span data-stu-id="629e4-184">Save the file and enable the service:</span></span>

```bash
sudo systemctl enable kestrel-helloapp.service
```

<span data-ttu-id="629e4-185">Запустите службу и убедитесь, что она работает.</span><span class="sxs-lookup"><span data-stu-id="629e4-185">Start the service and verify that it's running:</span></span>

```bash
sudo systemctl start kestrel-helloapp.service
sudo systemctl status kestrel-helloapp.service

● kestrel-helloapp.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-helloapp.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-helloapp.service
            └─9021 /usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
```

<span data-ttu-id="629e4-186">Теперь, когда обратный прокси-сервер настроен и *systemd* управляет процессом Kestrel, веб-приложение можно считать полностью настроенным и вы можете обратиться к нему по адресу `http://localhost` из браузера на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="629e4-186">With the reverse proxy configured and Kestrel managed through *systemd*, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="629e4-187">Заголовок **Server** в ответе подтверждает, что приложение ASP.NET Core обслуживается Kestrel.</span><span class="sxs-lookup"><span data-stu-id="629e4-187">Inspecting the response headers, the **Server** header indicates that the ASP.NET Core app is served by Kestrel:</span></span>

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="view-logs"></a><span data-ttu-id="629e4-188">Просмотр журналов</span><span class="sxs-lookup"><span data-stu-id="629e4-188">View logs</span></span>

<span data-ttu-id="629e4-189">Так как веб-приложением, использующим Kestrel, управляет *systemd*, все события и процессы регистрируются в централизованном журнале.</span><span class="sxs-lookup"><span data-stu-id="629e4-189">Since the web app using Kestrel is managed using *systemd*, events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="629e4-190">Но этот журнал содержит все записи обо всех службах и процессах, управляемых *systemd*.</span><span class="sxs-lookup"><span data-stu-id="629e4-190">However, this journal includes entries for all of the services and processes managed by *systemd*.</span></span> <span data-ttu-id="629e4-191">Чтобы просмотреть элементы, связанные с `kestrel-helloapp.service`, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="629e4-191">To view the `kestrel-helloapp.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-helloapp.service
```

<span data-ttu-id="629e4-192">Чтобы отфильтровать элементы по времени, укажите в команде параметры времени.</span><span class="sxs-lookup"><span data-stu-id="629e4-192">For time filtering, specify time options with the command.</span></span> <span data-ttu-id="629e4-193">Например, `--since today` позволяет отфильтровать данные за текущий день, а `--until 1 hour ago` — просмотреть записи за предыдущий час.</span><span class="sxs-lookup"><span data-stu-id="629e4-193">For example, use `--since today` to filter for the current day or `--until 1 hour ago` to see the previous hour's entries.</span></span> <span data-ttu-id="629e4-194">Дополнительные сведения см. на странице руководства о команде [journalctl](https://www.unix.com/man-page/centos/1/journalctl/).</span><span class="sxs-lookup"><span data-stu-id="629e4-194">For more information, see the [man page for journalctl](https://www.unix.com/man-page/centos/1/journalctl/).</span></span>

```bash
sudo journalctl -fu kestrel-helloapp.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="data-protection"></a><span data-ttu-id="629e4-195">Защита данных</span><span class="sxs-lookup"><span data-stu-id="629e4-195">Data protection</span></span>

<span data-ttu-id="629e4-196">[Стек защиты данных в ASP.NET Core](xref:security/data-protection/introduction) используется определенным [ПО промежуточного слоя](xref:fundamentals/middleware/index) ASP.NET Core, включая промежуточное ПО для проверки подлинности (например, промежуточное ПО файлов cookie) и средствами защиты от подделки межсайтовых запросов.</span><span class="sxs-lookup"><span data-stu-id="629e4-196">The [ASP.NET Core Data Protection stack](xref:security/data-protection/introduction) is used by several ASP.NET Core [middlewares](xref:fundamentals/middleware/index), including authentication middleware (for example, cookie middleware) and cross-site request forgery (CSRF) protections.</span></span> <span data-ttu-id="629e4-197">Даже если API-интерфейсы защиты данных не вызываются из пользовательского кода, необходимо настроить защиту данных для создания постоянного [хранилища криптографических ключей](xref:security/data-protection/implementation/key-management).</span><span class="sxs-lookup"><span data-stu-id="629e4-197">Even if Data Protection APIs aren't called by user code, data protection should be configured to create a persistent cryptographic [key store](xref:security/data-protection/implementation/key-management).</span></span> <span data-ttu-id="629e4-198">Если защита данных не настроена, ключи хранятся в памяти и удаляются при перезапуске приложения.</span><span class="sxs-lookup"><span data-stu-id="629e4-198">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="629e4-199">Если набор ключей хранится в памяти, при перезапуске приложения происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="629e4-199">If the key ring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="629e4-200">Все токены аутентификации, использующие файлы cookie, становятся недействительными.</span><span class="sxs-lookup"><span data-stu-id="629e4-200">All cookie-based authentication tokens are invalidated.</span></span>
* <span data-ttu-id="629e4-201">При выполнении следующего запроса пользователю требуется выполнить вход снова.</span><span class="sxs-lookup"><span data-stu-id="629e4-201">Users are required to sign in again on their next request.</span></span>
* <span data-ttu-id="629e4-202">Все данные, защищенные с помощью набора ключей, больше не могут быть расшифрованы.</span><span class="sxs-lookup"><span data-stu-id="629e4-202">Any data protected with the key ring can no longer be decrypted.</span></span> <span data-ttu-id="629e4-203">Это могут быть [токены CSRF](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) и [файлы cookie временных данных ASP.NET Core MVC](xref:fundamentals/app-state#tempdata).</span><span class="sxs-lookup"><span data-stu-id="629e4-203">This may include [CSRF tokens](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) and [ASP.NET Core MVC TempData cookies](xref:fundamentals/app-state#tempdata).</span></span>

<span data-ttu-id="629e4-204">Сведения о настройке защиты данных для хранения и шифрования набора ключей см. в приведенных ниже статьях.</span><span class="sxs-lookup"><span data-stu-id="629e4-204">To configure data protection to persist and encrypt the key ring, see:</span></span>

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>

## <a name="secure-the-app"></a><span data-ttu-id="629e4-205">Защита приложения</span><span class="sxs-lookup"><span data-stu-id="629e4-205">Secure the app</span></span>

### <a name="configure-firewall"></a><span data-ttu-id="629e4-206">Настройка брандмауэра</span><span class="sxs-lookup"><span data-stu-id="629e4-206">Configure firewall</span></span>

<span data-ttu-id="629e4-207">*Firewalld* — это динамическая управляющая программа брандмауэра, которая поддерживает зоны сети.</span><span class="sxs-lookup"><span data-stu-id="629e4-207">*Firewalld* is a dynamic daemon to manage the firewall with support for network zones.</span></span> <span data-ttu-id="629e4-208">Фильтрацию портов и пакетов можно по-прежнему осуществлять через iptables.</span><span class="sxs-lookup"><span data-stu-id="629e4-208">Ports and packet filtering can still be managed by iptables.</span></span> <span data-ttu-id="629e4-209">*Firewalld* обычно устанавливается в системе по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="629e4-209">*Firewalld* should be installed by default.</span></span> <span data-ttu-id="629e4-210">`yum` позволяет установить этот пакет или убедиться, что он установлен.</span><span class="sxs-lookup"><span data-stu-id="629e4-210">`yum` can be used to install the package or verify it's installed.</span></span>

```bash
sudo yum install firewalld -y
```

<span data-ttu-id="629e4-211">С помощью `firewalld` вы можете открыть только те порты, которые необходимые для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="629e4-211">Use `firewalld` to open only the ports needed for the app.</span></span> <span data-ttu-id="629e4-212">В этом случае используются порты 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="629e4-212">In this case, port 80 and 443 are used.</span></span> <span data-ttu-id="629e4-213">Следующие команды назначают порты 80 и 443 постоянно открытыми.</span><span class="sxs-lookup"><span data-stu-id="629e4-213">The following commands permanently set ports 80 and 443 to open:</span></span>

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

<span data-ttu-id="629e4-214">Обновите параметры брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="629e4-214">Reload the firewall settings.</span></span> <span data-ttu-id="629e4-215">Проверьте, что доступные службы и порты находятся в зоне по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="629e4-215">Check the available services and ports in the default zone.</span></span> <span data-ttu-id="629e4-216">Эти параметры можно просмотреть с помощью `firewall-cmd -h`.</span><span class="sxs-lookup"><span data-stu-id="629e4-216">Options are available by inspecting `firewall-cmd -h`.</span></span>

```bash
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

```bash
public (default, active)
interfaces: eth0
sources: 
services: dhcpv6-client
ports: 443/tcp 80/tcp
masquerade: no
forward-ports: 
icmp-blocks: 
rich rules: 
```

### <a name="https-configuration"></a><span data-ttu-id="629e4-217">Конфигурация HTTPS</span><span class="sxs-lookup"><span data-stu-id="629e4-217">HTTPS configuration</span></span>

<span data-ttu-id="629e4-218">Apache для HTTPS настраивается с помощью модуля *mod_ssl*.</span><span class="sxs-lookup"><span data-stu-id="629e4-218">To configure Apache for HTTPS, the *mod_ssl* module is used.</span></span> <span data-ttu-id="629e4-219">При установке модуля *httpd* автоматически добавляется и модуль *mod_ssl*.</span><span class="sxs-lookup"><span data-stu-id="629e4-219">When the *httpd* module was installed, the *mod_ssl* module was also installed.</span></span> <span data-ttu-id="629e4-220">Если он по каким-то причинам отсутствует, добавьте его в систему с помощью `yum`.</span><span class="sxs-lookup"><span data-stu-id="629e4-220">If it wasn't installed, use `yum` to add it to the configuration.</span></span>

```bash
sudo yum install mod_ssl
```

<span data-ttu-id="629e4-221">Чтобы принудительно использовать HTTPS, установите модуль `mod_rewrite` для перезаписи URL-адресов:</span><span class="sxs-lookup"><span data-stu-id="629e4-221">To enforce HTTPS, install the `mod_rewrite` module to enable URL rewriting:</span></span>

```bash
sudo yum install mod_rewrite
```

<span data-ttu-id="629e4-222">Измените файл *helloapp.conf*, чтобы разрешить перезапись URL-адресов и безопасный обмен данными через порт 443:</span><span class="sxs-lookup"><span data-stu-id="629e4-222">Modify the *helloapp.conf* file to enable URL rewriting and secure communication on port 443:</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/helloapp-error.log
    CustomLog /var/log/httpd/helloapp-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

> [!NOTE]
> <span data-ttu-id="629e4-223">В этом примере используется локально созданный сертификат.</span><span class="sxs-lookup"><span data-stu-id="629e4-223">This example is using a locally-generated certificate.</span></span> <span data-ttu-id="629e4-224">В **SSLCertificateFile** должен быть указан основной файл сертификата для доменного имени.</span><span class="sxs-lookup"><span data-stu-id="629e4-224">**SSLCertificateFile** should be the primary certificate file for the domain name.</span></span> <span data-ttu-id="629e4-225">В **SSLCertificateKeyFile** должен быть указан файл ключа, сформированный при создании CSR.</span><span class="sxs-lookup"><span data-stu-id="629e4-225">**SSLCertificateKeyFile** should be the key file generated when CSR is created.</span></span> <span data-ttu-id="629e4-226">В **SSLCertificateChainFile** должен быть указан файл промежуточного сертификата (если он существует), предоставленный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="629e4-226">**SSLCertificateChainFile** should be the intermediate certificate file (if any) that was supplied by the certificate authority.</span></span>

<span data-ttu-id="629e4-227">Сохраните файл и протестируйте конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="629e4-227">Save the file and test the configuration:</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="629e4-228">Перезапустите Apache.</span><span class="sxs-lookup"><span data-stu-id="629e4-228">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a><span data-ttu-id="629e4-229">Дополнительные предложения Apache</span><span class="sxs-lookup"><span data-stu-id="629e4-229">Additional Apache suggestions</span></span>

### <a name="additional-headers"></a><span data-ttu-id="629e4-230">Дополнительные заголовки</span><span class="sxs-lookup"><span data-stu-id="629e4-230">Additional headers</span></span>

<span data-ttu-id="629e4-231">Для защиты от вредоносных атак следует изменить или добавить несколько заголовков.</span><span class="sxs-lookup"><span data-stu-id="629e4-231">In order to secure against malicious attacks, there are a few headers that should either be modified or added.</span></span> <span data-ttu-id="629e4-232">Убедитесь, что модуль `mod_headers` установлен.</span><span class="sxs-lookup"><span data-stu-id="629e4-232">Ensure that the `mod_headers` module is installed:</span></span>

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a><span data-ttu-id="629e4-233">Защита Apache от атак кликджекинга</span><span class="sxs-lookup"><span data-stu-id="629e4-233">Secure Apache from clickjacking attacks</span></span>

<span data-ttu-id="629e4-234">[Кликджекинг](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger) (или *атака с подменой пользовательского интерфейса*) является вредоносной атакой, при которой посетителя сайта обманным путем вынуждают щелкнуть ссылку или нажать кнопку не той страницы, на которой он находится.</span><span class="sxs-lookup"><span data-stu-id="629e4-234">[Clickjacking](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger), also known as a *UI redress attack*, is a malicious attack where a website visitor is tricked into clicking a link or button on a different page than they're currently visiting.</span></span> <span data-ttu-id="629e4-235">Используйте `X-FRAME-OPTIONS` для защиты сайта.</span><span class="sxs-lookup"><span data-stu-id="629e4-235">Use `X-FRAME-OPTIONS` to secure the site.</span></span>

<span data-ttu-id="629e4-236">Чтобы уменьшить риск атак кликджекинга, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="629e4-236">To mitigate clickjacking attacks:</span></span>

1. <span data-ttu-id="629e4-237">Измените файл *httpd.conf*.</span><span class="sxs-lookup"><span data-stu-id="629e4-237">Edit the *httpd.conf* file:</span></span>

   ```bash
   sudo nano /etc/httpd/conf/httpd.conf
   ```

   <span data-ttu-id="629e4-238">Добавьте строку `Header append X-FRAME-OPTIONS "SAMEORIGIN"`.</span><span class="sxs-lookup"><span data-stu-id="629e4-238">Add the line `Header append X-FRAME-OPTIONS "SAMEORIGIN"`.</span></span>
1. <span data-ttu-id="629e4-239">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="629e4-239">Save the file.</span></span>
1. <span data-ttu-id="629e4-240">Перезапустите Apache.</span><span class="sxs-lookup"><span data-stu-id="629e4-240">Restart Apache.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="629e4-241">Сканирование типа MIME</span><span class="sxs-lookup"><span data-stu-id="629e4-241">MIME-type sniffing</span></span>

<span data-ttu-id="629e4-242">Заголовок `X-Content-Type-Options` защищает Internet Explorer от *сканирования MIME* (определения `Content-Type` для файла по его содержимому).</span><span class="sxs-lookup"><span data-stu-id="629e4-242">The `X-Content-Type-Options` header prevents Internet Explorer from *MIME-sniffing* (determining a file's `Content-Type` from the file's content).</span></span> <span data-ttu-id="629e4-243">Если сервер задает заголовок `Content-Type` со значением `text/html`, и при этом установлен параметр `nosniff`, Internet Explorer отображает содержимое как `text/html` независимо от содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="629e4-243">If the server sets the `Content-Type` header to `text/html` with the `nosniff` option set, Internet Explorer renders the content as `text/html` regardless of the file's content.</span></span>

<span data-ttu-id="629e4-244">Измените файл *httpd.conf*.</span><span class="sxs-lookup"><span data-stu-id="629e4-244">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="629e4-245">Добавьте строку `Header set X-Content-Type-Options "nosniff"`.</span><span class="sxs-lookup"><span data-stu-id="629e4-245">Add the line `Header set X-Content-Type-Options "nosniff"`.</span></span> <span data-ttu-id="629e4-246">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="629e4-246">Save the file.</span></span> <span data-ttu-id="629e4-247">Перезапустите Apache.</span><span class="sxs-lookup"><span data-stu-id="629e4-247">Restart Apache.</span></span>

### <a name="load-balancing"></a><span data-ttu-id="629e4-248">Балансировка нагрузки</span><span class="sxs-lookup"><span data-stu-id="629e4-248">Load Balancing</span></span>

<span data-ttu-id="629e4-249">В этом примере показано, как установить и настроить Apache в CentOS 7 и Kestrel на том же компьютере.</span><span class="sxs-lookup"><span data-stu-id="629e4-249">This example shows how to setup and configure Apache on CentOS 7 and Kestrel on the same instance machine.</span></span> <span data-ttu-id="629e4-250">Чтобы устранить единую точку отказа, воспользуйтесь *mod_proxy_balancer* и измените значение **VirtualHost** для управления несколькими экземплярами веб-приложений за прокси-сервером Apache.</span><span class="sxs-lookup"><span data-stu-id="629e4-250">In order to not have a single point of failure; using *mod_proxy_balancer* and modifying the **VirtualHost** would allow for managing multiple instances of the web apps behind the Apache proxy server.</span></span>

```bash
sudo yum install mod_proxy_balancer
```

<span data-ttu-id="629e4-251">В представленном ниже файле конфигурации настроен дополнительный экземпляр `helloapp`, работающий на порте 5001.</span><span class="sxs-lookup"><span data-stu-id="629e4-251">In the configuration file shown below, an additional instance of the `helloapp` is set up to run on port 5001.</span></span> <span data-ttu-id="629e4-252">В разделе *Proxy* настраивается конфигурация подсистемы балансировки нагрузки с двумя членами для распределения нагрузки методом *byrequests*.</span><span class="sxs-lookup"><span data-stu-id="629e4-252">The *Proxy* section is set with a balancer configuration with two members to load balance *byrequests*.</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPass / balancer://mycluster/ 

    ProxyPassReverse / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5001/

    <Proxy balancer://mycluster>
        BalancerMember http://127.0.0.1:5000
        BalancerMember http://127.0.0.1:5001 
        ProxySet lbmethod=byrequests
    </Proxy>

    <Location />
        SetHandler balancer
    </Location>
    ErrorLog /var/log/httpd/helloapp-error.log
    CustomLog /var/log/httpd/helloapp-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

### <a name="rate-limits"></a><span data-ttu-id="629e4-253">Ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="629e4-253">Rate Limits</span></span>

<span data-ttu-id="629e4-254">С помощью элемента *mod_ratelimit*, который входит в модуль *httpd*, можно ограничить пропускную способность для клиентов:</span><span class="sxs-lookup"><span data-stu-id="629e4-254">Using *mod_ratelimit*, which is included in the *httpd* module, the bandwidth of clients can be limited:</span></span>

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```

<span data-ttu-id="629e4-255">В примере файла пропускная способность составляет 600 Кбит/с в корневой папке.</span><span class="sxs-lookup"><span data-stu-id="629e4-255">The example file limits bandwidth as 600 KB/sec under the root location:</span></span>

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```

### <a name="long-request-header-fields"></a><span data-ttu-id="629e4-256">Длинные поля заголовка запроса</span><span class="sxs-lookup"><span data-stu-id="629e4-256">Long request header fields</span></span>

<span data-ttu-id="629e4-257">Если приложение требует поля заголовка запроса длиннее, чем разрешено параметром по умолчанию прокси-сервера (обычно 8190 байт). измените значение директивы [LimitRequestFieldSize](https://httpd.apache.org/docs/2.4/mod/core.html#LimitRequestFieldSize).</span><span class="sxs-lookup"><span data-stu-id="629e4-257">If the app requires request header fields longer than permitted by the proxy server's default setting (typically 8,190 bytes), adjust the value of the [LimitRequestFieldSize](https://httpd.apache.org/docs/2.4/mod/core.html#LimitRequestFieldSize) directive.</span></span> <span data-ttu-id="629e4-258">Применяемое значение зависит от условий.</span><span class="sxs-lookup"><span data-stu-id="629e4-258">The value to apply is scenario-dependent.</span></span> <span data-ttu-id="629e4-259">Дополнительные сведения см. в документации сервера.</span><span class="sxs-lookup"><span data-stu-id="629e4-259">For more information, see your server's documentation.</span></span>

> [!WARNING]
> <span data-ttu-id="629e4-260">Не увеличивайте значение `LimitRequestFieldSize` по умолчанию, если это не требуется.</span><span class="sxs-lookup"><span data-stu-id="629e4-260">Don't increase the default value of `LimitRequestFieldSize` unless necessary.</span></span> <span data-ttu-id="629e4-261">Увеличение значения повышает риск переполнения буфера и атак типа "отказ в обслуживании" (DoS) со стороны злоумышленников.</span><span class="sxs-lookup"><span data-stu-id="629e4-261">Increasing the value increases the risk of buffer overrun (overflow) and Denial of Service (DoS) attacks by malicious users.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="629e4-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="629e4-262">Additional resources</span></span>

* [<span data-ttu-id="629e4-263">Необходимые компоненты для .NET Core в Linux</span><span class="sxs-lookup"><span data-stu-id="629e4-263">Prerequisites for .NET Core on Linux</span></span>](/dotnet/core/linux-prerequisites)
* <xref:test/troubleshoot>
* <xref:host-and-deploy/proxy-load-balancer>
