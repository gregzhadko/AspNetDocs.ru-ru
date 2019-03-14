---
title: Введение в компоненты Razor
author: guardrex
description: 'Узнайте больше о компонентах Razor в ASP.NET Core, которые позволяют создать интерактивный клиентский веб-интерфейс с использованием .NET в приложении ASP.NET Core.'
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/12/2019
uid: razor-components/index
---
# <a name="introduction-to-razor-components"></a><span data-ttu-id="a31be-103">Введение в компоненты Razor</span><span class="sxs-lookup"><span data-stu-id="a31be-103">Introduction to Razor Components</span></span>

<span data-ttu-id="a31be-104">Авторы: [Дэниэл Рот (Daniel Roth)](https://github.com/danroth27) и [Люк Лэтем (Luke Latham)](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="a31be-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="a31be-105">*Компоненты Razor* — это средства для создания интерактивного клиентского веб-интерфейса с использованием .NET, которые предоставляют такие возможности:</span><span class="sxs-lookup"><span data-stu-id="a31be-105">*Razor Components* is a way to build interactive client-side web UI with .NET:</span></span>

* <span data-ttu-id="a31be-106">создание многофункциональных интерактивных пользовательских интерфейсов с помощью C# (а не JavaScript);</span><span class="sxs-lookup"><span data-stu-id="a31be-106">Build rich interactive UIs using C# instead of JavaScript.</span></span>
* <span data-ttu-id="a31be-107">совместное использование серверной и клиентской логик приложений, написанных с помощью .NET;</span><span class="sxs-lookup"><span data-stu-id="a31be-107">Share server-side and client-side app logic all written with .NET.</span></span>
* <span data-ttu-id="a31be-108">отображение пользовательского интерфейса в виде HTML-страницы с CSS для широкой поддержки браузеров, в том числе для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="a31be-108">Render the UI as HTML and CSS for wide browser support, including mobile browsers.</span></span>

<span data-ttu-id="a31be-109">Компоненты Razor поддерживают базовые функции, которые требуются большинству приложений, в том числе такие:</span><span class="sxs-lookup"><span data-stu-id="a31be-109">Razor Components supports core facilities required by most apps, including:</span></span>

* <span data-ttu-id="a31be-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="a31be-110">Parameters</span></span>
* <span data-ttu-id="a31be-111">Обработка событий</span><span class="sxs-lookup"><span data-stu-id="a31be-111">Event handling</span></span>
* <span data-ttu-id="a31be-112">привязка данных,</span><span class="sxs-lookup"><span data-stu-id="a31be-112">Data binding</span></span>
* <span data-ttu-id="a31be-113">Маршрутизация</span><span class="sxs-lookup"><span data-stu-id="a31be-113">Routing</span></span>
* <span data-ttu-id="a31be-114">Внедрение зависимостей</span><span class="sxs-lookup"><span data-stu-id="a31be-114">Dependency injection</span></span>
* <span data-ttu-id="a31be-115">Макеты</span><span class="sxs-lookup"><span data-stu-id="a31be-115">Layouts</span></span>
* <span data-ttu-id="a31be-116">Использование шаблонов</span><span class="sxs-lookup"><span data-stu-id="a31be-116">Templating</span></span>
* <span data-ttu-id="a31be-117">Каскадные значения</span><span class="sxs-lookup"><span data-stu-id="a31be-117">Cascading values</span></span>

<span data-ttu-id="a31be-118">Компоненты Razor отделяют логику отображения компонентов от способов применения обновлений пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a31be-118">Razor Components decouples component rendering logic from how UI updates are applied.</span></span> <span data-ttu-id="a31be-119">Компоненты Razor в ASP.NET Core в .NET Core 3.0 реализуют поддержку размещения компонентов Razor на сервере в приложении ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a31be-119">ASP.NET Core Razor Components in .NET Core 3.0 adds support for hosting Razor Components on the server in an ASP.NET Core app.</span></span> <span data-ttu-id="a31be-120">Обновления пользовательского интерфейса обрабатываются через подключение SignalR.</span><span class="sxs-lookup"><span data-stu-id="a31be-120">UI updates are handled over a SignalR connection.</span></span>

<span data-ttu-id="a31be-121">Среда выполнения:</span><span class="sxs-lookup"><span data-stu-id="a31be-121">The runtime:</span></span>

* <span data-ttu-id="a31be-122">обрабатывает отправку событий пользовательского интерфейса из браузера на сервер;</span><span class="sxs-lookup"><span data-stu-id="a31be-122">Handles sending UI events from the browser to the server.</span></span>
* <span data-ttu-id="a31be-123">применяет обновления пользовательского интерфейса, отправленные сервером браузеру после выполнения компонентов.</span><span class="sxs-lookup"><span data-stu-id="a31be-123">Applies UI updates sent by the server back to the browser after running the components.</span></span>

<span data-ttu-id="a31be-124">Подключение, используемое компонентами Razor для обмена данными с браузером, также применяется для обработки вызовов взаимодействия JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a31be-124">The connection used by Razor Components to communicate with the browser is also used to handle JavaScript interop calls.</span></span>

![Компоненты Razor выполняют код .NET на сервере и взаимодействуют с моделью DOM на стороне клиента через подключение SignalR](index/_static/aspnet-core-razor-components.png)

<span data-ttu-id="a31be-126">Дополнительные сведения см. в разделе <xref:razor-components/hosting-models#server-side-hosting-model>.</span><span class="sxs-lookup"><span data-stu-id="a31be-126">For more information, see <xref:razor-components/hosting-models#server-side-hosting-model>.</span></span>

<span data-ttu-id="a31be-127">*Blazor* — это экспериментальная модель размещения на стороне клиента для компонентов Razor.</span><span class="sxs-lookup"><span data-stu-id="a31be-127">*Blazor* is the experimental client-side hosting model of Razor Components.</span></span> <span data-ttu-id="a31be-128">Blazor работает в среде .NET в браузере, используя открытые веб-стандарты без подключаемых модулей или транспиляции кода.</span><span class="sxs-lookup"><span data-stu-id="a31be-128">Blazor runs on .NET in the browser using open web standards without plugins or code transpilation.</span></span> <span data-ttu-id="a31be-129">Дополнительные сведения см. в разделе <xref:razor-components/hosting-models#client-side-hosting-model>.</span><span class="sxs-lookup"><span data-stu-id="a31be-129">For more information, see <xref:razor-components/hosting-models#client-side-hosting-model>.</span></span>

## <a name="components"></a><span data-ttu-id="a31be-130">Компоненты</span><span class="sxs-lookup"><span data-stu-id="a31be-130">Components</span></span>

<span data-ttu-id="a31be-131">*Компонент Razor* — это часть пользовательского интерфейса, например страница, диалоговое окно или форма ввода данных.</span><span class="sxs-lookup"><span data-stu-id="a31be-131">A *Razor Component* is a piece of UI, such as a page, dialog, or data entry form.</span></span> <span data-ttu-id="a31be-132">Компоненты обрабатывают для пользователей события и определяют гибкую логику отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a31be-132">Components handle user events and define flexible UI rendering logic.</span></span> <span data-ttu-id="a31be-133">Их можно вкладывать друг в друга и использовать повторно.</span><span class="sxs-lookup"><span data-stu-id="a31be-133">Components can be nested and reused.</span></span>

<span data-ttu-id="a31be-134">Компоненты — это классы .NET, встроенные в сборки .NET, которые можно совместно использовать и распространять в виде пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="a31be-134">Components are .NET classes built into .NET assemblies that can be shared and distributed as NuGet packages.</span></span> <span data-ttu-id="a31be-135">Этот класс может записываться в виде страницы разметки Razor (*.cshtml*) или в виде класса C# (*.cs*).</span><span class="sxs-lookup"><span data-stu-id="a31be-135">The class can either be written in the form of a Razor markup page (*.cshtml*) or as a C# class (*.cs*).</span></span>

<span data-ttu-id="a31be-136">[Razor](xref:mvc/views/razor) — это синтаксис для объединения разметки HTML с кодом C#.</span><span class="sxs-lookup"><span data-stu-id="a31be-136">[Razor](xref:mvc/views/razor) is a syntax for combining HTML markup with C# code.</span></span> <span data-ttu-id="a31be-137">Razor предназначен для повышения производительности разработчика и позволяет разработчику переключаться между разметкой и C# в одном файле с поддержкой [IntelliSense](/visualstudio/ide/using-intellisense).</span><span class="sxs-lookup"><span data-stu-id="a31be-137">Razor is designed for developer productivity, allowing the developer to switch between markup and C# in the same file with [IntelliSense](/visualstudio/ide/using-intellisense) support.</span></span> <span data-ttu-id="a31be-138">Razor Pages и представления MVC также используют Razor.</span><span class="sxs-lookup"><span data-stu-id="a31be-138">Razor Pages and MVC views also use Razor.</span></span> <span data-ttu-id="a31be-139">В отличие от Razor Pages и представлений MVC, которые созданы на базе модели "запрос — ответ", компоненты используются исключительно для обработки композиции пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a31be-139">Unlike Razor Pages and MVC views, which are built around a request/response model, components are used specifically for handling UI composition.</span></span> <span data-ttu-id="a31be-140">Компоненты Razor можно использовать исключительно для клиентской логики и композиции пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a31be-140">Razor Components can be used specifically for client-side UI logic and composition.</span></span>

<span data-ttu-id="a31be-141">Следующая разметка является примером настраиваемого диалогового компонента в файле Razor (*DialogComponent.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="a31be-141">The following markup is an example of a custom dialog component in a Razor file (*DialogComponent.cshtml*):</span></span>

```cshtml
<div>
    <h2>@Title</h2>
    @BodyContent
    <button onclick=@OnOK>OK</button>
</div>

@functions {
    public string Title { get; set; }
    public RenderFragment BodyContent { get; set; }
    public Action OnOK { get; set; }
}
```

<span data-ttu-id="a31be-142">Когда этот компонент используется в другом месте в приложении, IntelliSense ускоряет разработку с помощью выполнения синтаксиса и параметров.</span><span class="sxs-lookup"><span data-stu-id="a31be-142">When this component is used elsewhere in the app, IntelliSense speeds development with syntax and parameter completion.</span></span>

<span data-ttu-id="a31be-143">Компоненты преобразуются в представление DOM браузера в памяти, которое называется *деревом визуализации*. Его затем можно использовать для гибкого и эффективного обновления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a31be-143">Components render into an in-memory representation of the browser DOM called a *render tree* that can then be used to update the UI in a flexible and efficient way.</span></span>

## <a name="javascript-interop"></a><span data-ttu-id="a31be-144">Взаимодействие с JavaScript</span><span class="sxs-lookup"><span data-stu-id="a31be-144">JavaScript interop</span></span>

<span data-ttu-id="a31be-145">Для приложений, требующих сторонние библиотеки JavaScript и API браузера, компоненты взаимодействуют с JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a31be-145">For apps that require third-party JavaScript libraries and browser APIs, components interoperate with JavaScript.</span></span> <span data-ttu-id="a31be-146">Компоненты могут использовать любую библиотеку или API, которые может использовать JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a31be-146">Components are capable of using any library or API that JavaScript is able to use.</span></span> <span data-ttu-id="a31be-147">Код C# может вызывать код JavaScript, а код JavaScript — код C#.</span><span class="sxs-lookup"><span data-stu-id="a31be-147">C# code can call into JavaScript code, and JavaScript code can call into C# code.</span></span> <span data-ttu-id="a31be-148">Дополнительные сведения см. в разделе [Взаимодействие с JavaScript](xref:razor-components/javascript-interop).</span><span class="sxs-lookup"><span data-stu-id="a31be-148">For more information, see [JavaScript interop](xref:razor-components/javascript-interop).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a31be-149">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a31be-149">Additional resources</span></span>

* <xref:spa/blazor/index>
* [<span data-ttu-id="a31be-150">WebAssembly</span><span class="sxs-lookup"><span data-stu-id="a31be-150">WebAssembly</span></span>](http://webassembly.org/)
* [<span data-ttu-id="a31be-151">Руководство по языку C#</span><span class="sxs-lookup"><span data-stu-id="a31be-151">C# Guide</span></span>](/dotnet/csharp/)
* <xref:mvc/views/razor>
* [<span data-ttu-id="a31be-152">HTML</span><span class="sxs-lookup"><span data-stu-id="a31be-152">HTML</span></span>](https://www.w3.org/html/)
