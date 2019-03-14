---
title: Настройка локализации переносных объектов в ASP.NET Core
author: sebastienros
description: Эта статья содержит вводные сведения о файлах переносимых объектов и описывает действия по их использованию в приложении ASP.NET Core с помощью платформы Orchard Core.
ms.author: scaddie
ms.date: 09/26/2017
uid: fundamentals/portable-object-localization
ms.openlocfilehash: c9f892f5a886d7167b4705595ed2277279495201
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053221"
---
# <a name="configure-portable-object-localization-in-aspnet-core"></a><span data-ttu-id="37e43-103">Настройка локализации переносных объектов в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="37e43-103">Configure portable object localization in ASP.NET Core</span></span>

<span data-ttu-id="37e43-104">Авторы: [Себастьен Рос](https://github.com/sebastienros) (Sébastien Ros) и [Скотт Эдди](https://twitter.com/Scott_Addie) (Scott Addie)</span><span class="sxs-lookup"><span data-stu-id="37e43-104">By [Sébastien Ros](https://github.com/sebastienros) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="37e43-105">Эта статья описывает действия по использованию файлов переносимых объектов в приложении ASP.NET Core с помощью платформы [Orchard Core](https://github.com/OrchardCMS/OrchardCore).</span><span class="sxs-lookup"><span data-stu-id="37e43-105">This article walks through the steps for using Portable Object (PO) files in an ASP.NET Core application with the [Orchard Core](https://github.com/OrchardCMS/OrchardCore) framework.</span></span>

<span data-ttu-id="37e43-106">**Примечание.** Orchard Core не продукт Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="37e43-106">**Note:** Orchard Core isn't a Microsoft product.</span></span> <span data-ttu-id="37e43-107">Поэтому корпорация Майкрософт не предоставляет поддержку для этого компонента.</span><span class="sxs-lookup"><span data-stu-id="37e43-107">Consequently, Microsoft provides no support for this feature.</span></span>

<span data-ttu-id="37e43-108">[Просмотреть или скачать образец кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/localization/sample/POLocalization) ([как скачивать](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="37e43-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/localization/sample/POLocalization) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="what-is-a-po-file"></a><span data-ttu-id="37e43-109">Что такое файл переносимых объектов?</span><span class="sxs-lookup"><span data-stu-id="37e43-109">What is a PO file?</span></span>

<span data-ttu-id="37e43-110">Файлы переносимых объектов (PO) распространяются как текстовые файлы со строками, переведенными на заданный язык.</span><span class="sxs-lookup"><span data-stu-id="37e43-110">PO files are distributed as text files containing the translated strings for a given language.</span></span> <span data-ttu-id="37e43-111">Файлы PO дают определенные преимущества по сравнению с файлами *RESX*, например:</span><span class="sxs-lookup"><span data-stu-id="37e43-111">Some advantages of using PO files instead *.resx* files include:</span></span>
- <span data-ttu-id="37e43-112">Файлы PO поддерживают преобразование во множественную форму, файлы *RESX* — нет.</span><span class="sxs-lookup"><span data-stu-id="37e43-112">PO files support pluralization; *.resx* files don't support pluralization.</span></span>
- <span data-ttu-id="37e43-113">Файлы PO не компилируются подобно файлам *RESX*.</span><span class="sxs-lookup"><span data-stu-id="37e43-113">PO files aren't compiled like *.resx* files.</span></span> <span data-ttu-id="37e43-114">Поэтому потребность в специальных инструментах и действиях сборки отпадает.</span><span class="sxs-lookup"><span data-stu-id="37e43-114">As such, specialized tooling and build steps aren't required.</span></span>
- <span data-ttu-id="37e43-115">Файлы PO хорошо работают со средствами редактирования, предназначенными для совместной работы по сети.</span><span class="sxs-lookup"><span data-stu-id="37e43-115">PO files work well with collaborative online editing tools.</span></span>

### <a name="example"></a><span data-ttu-id="37e43-116">Пример</span><span class="sxs-lookup"><span data-stu-id="37e43-116">Example</span></span>

<span data-ttu-id="37e43-117">Ниже приведен пример файла PO, содержащего перевод двух строк на французский язык, для одной из которых приведена форма во множественном числе:</span><span class="sxs-lookup"><span data-stu-id="37e43-117">Here is a sample PO file containing the translation for two strings in French, including one with its plural form:</span></span>

<span data-ttu-id="37e43-118">*fr.po*</span><span class="sxs-lookup"><span data-stu-id="37e43-118">*fr.po*</span></span>

```text
#: Services/EmailService.cs:29
msgid "Enter a comma separated list of email addresses."
msgstr "Entrez une liste d'emails séparés par une virgule."

#: Views/Email.cshtml:112
msgid "The email address is \"{0}\"."
msgid_plural "The email addresses are \"{0}\"."
msgstr[0] "L'adresse email est \"{0}\"."
msgstr[1] "Les adresses email sont \"{0}\""
```

<span data-ttu-id="37e43-119">В этом примере используется следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="37e43-119">This example uses the following syntax:</span></span>

- <span data-ttu-id="37e43-120">`#:`: Комментарий, указывающий контекст переводимой строки.</span><span class="sxs-lookup"><span data-stu-id="37e43-120">`#:`: A comment indicating the context of the string to be translated.</span></span> <span data-ttu-id="37e43-121">Одну и ту же строку можно перевести по-разному в зависимости от характера ее использования.</span><span class="sxs-lookup"><span data-stu-id="37e43-121">The same string might be translated differently depending on where it's being used.</span></span>
- <span data-ttu-id="37e43-122">`msgid`: Непереведенная строка.</span><span class="sxs-lookup"><span data-stu-id="37e43-122">`msgid`: The untranslated string.</span></span>
- <span data-ttu-id="37e43-123">`msgstr`: Переведенная строка.</span><span class="sxs-lookup"><span data-stu-id="37e43-123">`msgstr`: The translated string.</span></span>

<span data-ttu-id="37e43-124">При поддержке преобразования во множественную форму можно определить дополнительные записи.</span><span class="sxs-lookup"><span data-stu-id="37e43-124">In the case of pluralization support, more entries can be defined.</span></span>

- <span data-ttu-id="37e43-125">`msgid_plural`: Непереведенная строка во множественном числе.</span><span class="sxs-lookup"><span data-stu-id="37e43-125">`msgid_plural`: The untranslated plural string.</span></span>
- <span data-ttu-id="37e43-126">`msgstr[0]`: Переведенная строка для случая 0.</span><span class="sxs-lookup"><span data-stu-id="37e43-126">`msgstr[0]`: The translated string for the case 0.</span></span>
- <span data-ttu-id="37e43-127">`msgstr[N]`: Переведенная строка для случая N.</span><span class="sxs-lookup"><span data-stu-id="37e43-127">`msgstr[N]`: The translated string for the case N.</span></span>

<span data-ttu-id="37e43-128">Спецификацию файла PO см. [здесь](https://www.gnu.org/savannah-checkouts/gnu/gettext/manual/html_node/PO-Files.html).</span><span class="sxs-lookup"><span data-stu-id="37e43-128">The PO file specification can be found [here](https://www.gnu.org/savannah-checkouts/gnu/gettext/manual/html_node/PO-Files.html).</span></span>

## <a name="configuring-po-file-support-in-aspnet-core"></a><span data-ttu-id="37e43-129">Настройка поддержки файлов PO в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="37e43-129">Configuring PO file support in ASP.NET Core</span></span>

<span data-ttu-id="37e43-130">Этот пример основан на приложении ASP.NET Core MVC, созданном из шаблона проекта Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="37e43-130">This example is based on an ASP.NET Core MVC application generated from a Visual Studio 2017 project template.</span></span>

### <a name="referencing-the-package"></a><span data-ttu-id="37e43-131">Указание ссылок на пакет</span><span class="sxs-lookup"><span data-stu-id="37e43-131">Referencing the package</span></span>

<span data-ttu-id="37e43-132">Добавьте ссылку на пакет NuGet `OrchardCore.Localization.Core`.</span><span class="sxs-lookup"><span data-stu-id="37e43-132">Add a reference to the `OrchardCore.Localization.Core` NuGet package.</span></span> <span data-ttu-id="37e43-133">Его можно найти на [MyGet](https://www.myget.org/) в следующем источнике пакетов: https://www.myget.org/F/orchardcore-preview/api/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="37e43-133">It's available on [MyGet](https://www.myget.org/) at the following package source: https://www.myget.org/F/orchardcore-preview/api/v3/index.json</span></span>

<span data-ttu-id="37e43-134">Файл *CSPROJ* теперь содержит строку следующего вида (номер версии может отличаться):</span><span class="sxs-lookup"><span data-stu-id="37e43-134">The *.csproj* file now contains a line similar to the following (version number may vary):</span></span>

[!code-xml[](localization/sample/POLocalization/POLocalization.csproj?range=9)]

### <a name="registering-the-service"></a><span data-ttu-id="37e43-135">Регистрация службы</span><span class="sxs-lookup"><span data-stu-id="37e43-135">Registering the service</span></span>

<span data-ttu-id="37e43-136">Добавьте необходимые службы в метод `ConfigureServices` файла *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="37e43-136">Add the required services to the `ConfigureServices` method of *Startup.cs*:</span></span>

[!code-csharp[](localization/sample/POLocalization/Startup.cs?name=snippet_ConfigureServices&highlight=4-21)]

<span data-ttu-id="37e43-137">Добавьте необходимое ПО промежуточного слоя в метод `Configure` файла *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="37e43-137">Add the required middleware to the `Configure` method of *Startup.cs*:</span></span>

[!code-csharp[](localization/sample/POLocalization/Startup.cs?name=snippet_Configure&highlight=15)]

<span data-ttu-id="37e43-138">Добавьте следующий код в нужное представление Razor.</span><span class="sxs-lookup"><span data-stu-id="37e43-138">Add the following code to your Razor view of choice.</span></span> <span data-ttu-id="37e43-139">В этом примере используется *About.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="37e43-139">*About.cshtml* is used in this example.</span></span>

[!code-cshtml[](localization/sample/POLocalization/Views/Home/About.cshtml)]

<span data-ttu-id="37e43-140">Экземпляр `IViewLocalizer` внедряется и используется для перевода текста "Hello world!".</span><span class="sxs-lookup"><span data-stu-id="37e43-140">An `IViewLocalizer` instance is injected and used to translate the text "Hello world!".</span></span>

### <a name="creating-a-po-file"></a><span data-ttu-id="37e43-141">Создание файла PO</span><span class="sxs-lookup"><span data-stu-id="37e43-141">Creating a PO file</span></span>

<span data-ttu-id="37e43-142">Создайте файл с именем *<culture code>.po* в корневой папке приложения.</span><span class="sxs-lookup"><span data-stu-id="37e43-142">Create a file named *<culture code>.po* in your application root folder.</span></span> <span data-ttu-id="37e43-143">В этом примере файл имеет имя *fr.po*, так как используется французский язык:</span><span class="sxs-lookup"><span data-stu-id="37e43-143">In this example, the file name is *fr.po* because the French language is used:</span></span>

[!code-text[](localization/sample/POLocalization/fr.po)]

<span data-ttu-id="37e43-144">Данный файл содержит как строку на перевод, так и строку, переведенную на французский язык.</span><span class="sxs-lookup"><span data-stu-id="37e43-144">This file stores both the string to translate and the French-translated string.</span></span> <span data-ttu-id="37e43-145">При необходимости переводы возвращаются к своим родительским языку и региональным параметрам.</span><span class="sxs-lookup"><span data-stu-id="37e43-145">Translations revert to their parent culture, if necessary.</span></span> <span data-ttu-id="37e43-146">В этом примере файл *fr.po* используется, если запрошены язык и региональные параметры `fr-FR` или `fr-CA`.</span><span class="sxs-lookup"><span data-stu-id="37e43-146">In this example, the *fr.po* file is used if the requested culture is `fr-FR` or `fr-CA`.</span></span>

### <a name="testing-the-application"></a><span data-ttu-id="37e43-147">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="37e43-147">Testing the application</span></span>

<span data-ttu-id="37e43-148">Запустите приложение и перейдите по URL-адресу `/Home/About`.</span><span class="sxs-lookup"><span data-stu-id="37e43-148">Run your application, and navigate to the URL `/Home/About`.</span></span> <span data-ttu-id="37e43-149">Отображается текст **Hello world!**</span><span class="sxs-lookup"><span data-stu-id="37e43-149">The text **Hello world!**</span></span> <span data-ttu-id="37e43-150">.</span><span class="sxs-lookup"><span data-stu-id="37e43-150">is displayed.</span></span>

<span data-ttu-id="37e43-151">Перейдите по URL-адресу `/Home/About?culture=fr-FR`.</span><span class="sxs-lookup"><span data-stu-id="37e43-151">Navigate to the URL `/Home/About?culture=fr-FR`.</span></span> <span data-ttu-id="37e43-152">Отображается текст **Bonjour le monde!**</span><span class="sxs-lookup"><span data-stu-id="37e43-152">The text **Bonjour le monde!**</span></span> <span data-ttu-id="37e43-153">.</span><span class="sxs-lookup"><span data-stu-id="37e43-153">is displayed.</span></span>

## <a name="pluralization"></a><span data-ttu-id="37e43-154">Преобразование во множественную форму</span><span class="sxs-lookup"><span data-stu-id="37e43-154">Pluralization</span></span>

<span data-ttu-id="37e43-155">Файлы PO поддерживают преобразование во множественную форму, что удобно, когда одну и ту же строку нужно переводить по-разному в зависимости от кратности.</span><span class="sxs-lookup"><span data-stu-id="37e43-155">PO files support pluralization forms, which is useful when the same string needs to be translated differently based on a cardinality.</span></span> <span data-ttu-id="37e43-156">Эта задача осложняется тем, что каждый язык имеет собственные правила для выбора строк в зависимости от кратности.</span><span class="sxs-lookup"><span data-stu-id="37e43-156">This task is made complicated by the fact that each language defines custom rules to select which string to use based on the cardinality.</span></span>

<span data-ttu-id="37e43-157">Пакет локализации Orchard предоставляет API для автоматического вызова этих различных форм множественного числа.</span><span class="sxs-lookup"><span data-stu-id="37e43-157">The Orchard Localization package provides an API to invoke these different plural forms automatically.</span></span>

### <a name="creating-pluralization-po-files"></a><span data-ttu-id="37e43-158">Создание файлов PO с множественными формами</span><span class="sxs-lookup"><span data-stu-id="37e43-158">Creating pluralization PO files</span></span>

<span data-ttu-id="37e43-159">Добавьте в указанный ранее файл *fr.po* следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="37e43-159">Add the following content to the previously mentioned *fr.po* file:</span></span>

```text
msgid "There is one item."
msgid_plural "There are {0} items."
msgstr[0] "Il y a un élément."
msgstr[1] "Il y a {0} éléments."
```

<span data-ttu-id="37e43-160">Сведения о том, что означает каждая запись в этом примере, см. в разделе [Что такое файл переносимых объектов?](#what-is-a-po-file).</span><span class="sxs-lookup"><span data-stu-id="37e43-160">See [What is a PO file?](#what-is-a-po-file) for an explanation of what each entry in this example represents.</span></span>

### <a name="adding-a-language-using-different-pluralization-forms"></a><span data-ttu-id="37e43-161">Добавление языка с использованием различных форм множественного числа</span><span class="sxs-lookup"><span data-stu-id="37e43-161">Adding a language using different pluralization forms</span></span>

<span data-ttu-id="37e43-162">В предыдущем примере использовались строки на английском и французском языках.</span><span class="sxs-lookup"><span data-stu-id="37e43-162">English and French strings were used in the previous example.</span></span> <span data-ttu-id="37e43-163">Эти языки имеют всего две формы множественного числа и используют схожие правила. Кратность, равная единице, соответствует первой форме множественного числа.</span><span class="sxs-lookup"><span data-stu-id="37e43-163">English and French have only two pluralization forms and share the same form rules, which is that a cardinality of one is mapped to the first plural form.</span></span> <span data-ttu-id="37e43-164">Любая другая кратность соответствует второй форме множественного числа.</span><span class="sxs-lookup"><span data-stu-id="37e43-164">Any other cardinality is mapped to the second plural form.</span></span>

<span data-ttu-id="37e43-165">Подобные правила действуют не во всех языках.</span><span class="sxs-lookup"><span data-stu-id="37e43-165">Not all languages share the same rules.</span></span> <span data-ttu-id="37e43-166">Это показано на примере чешского языка, где форм множественного числа три.</span><span class="sxs-lookup"><span data-stu-id="37e43-166">This is illustrated with the Czech language, which has three plural forms.</span></span>

<span data-ttu-id="37e43-167">Создайте файл `cs.po`, как показано ниже, и обратите внимание, что для преобразования во множественную форму нужно три разных перевода:</span><span class="sxs-lookup"><span data-stu-id="37e43-167">Create the `cs.po` file as follows, and note how the pluralization needs three different translations:</span></span>

[!code-text[](localization/sample/POLocalization/cs.po)]

<span data-ttu-id="37e43-168">Чтобы принять локализации на чешский язык, добавьте `"cs"` в список поддерживаемых языков и региональных параметров в методе `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="37e43-168">To accept Czech localizations, add `"cs"` to the list of supported cultures in the `ConfigureServices` method:</span></span>

```csharp
var supportedCultures = new List<CultureInfo>
{
    new CultureInfo("en-US"),
    new CultureInfo("en"),
    new CultureInfo("fr-FR"),
    new CultureInfo("fr"),
    new CultureInfo("cs")
};
```

<span data-ttu-id="37e43-169">Измените файл *Views/Home/About.cshtml*, чтобы отобразить локализованные строки во множественном числе для разных кратностей:</span><span class="sxs-lookup"><span data-stu-id="37e43-169">Edit the *Views/Home/About.cshtml* file to render localized, plural strings for several cardinalities:</span></span>

```cshtml
<p>@Localizer.Plural(1, "There is one item.", "There are {0} items.")</p>
<p>@Localizer.Plural(2, "There is one item.", "There are {0} items.")</p>
<p>@Localizer.Plural(5, "There is one item.", "There are {0} items.")</p>
```

<span data-ttu-id="37e43-170">**Примечание.** В реальной ситуации переменная будет использоваться для представления этого числа.</span><span class="sxs-lookup"><span data-stu-id="37e43-170">**Note:** In a real world scenario, a variable would be used to represent the count.</span></span> <span data-ttu-id="37e43-171">Здесь мы повторяем один и тот же код с тремя различными значениями, чтобы описать частный случай.</span><span class="sxs-lookup"><span data-stu-id="37e43-171">Here, we repeat the same code with three different values to expose a very specific case.</span></span>

<span data-ttu-id="37e43-172">После переключения языка и региональных параметров вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="37e43-172">Upon switching cultures, you see the following:</span></span>

<span data-ttu-id="37e43-173">Для `/Home/About`:</span><span class="sxs-lookup"><span data-stu-id="37e43-173">For `/Home/About`:</span></span>

```html
There is one item.
There are 2 items.
There are 5 items.
```

<span data-ttu-id="37e43-174">Для `/Home/About?culture=fr`:</span><span class="sxs-lookup"><span data-stu-id="37e43-174">For `/Home/About?culture=fr`:</span></span>

```html
Il y a un élément.
Il y a 2 éléments.
Il y a 5 éléments.
```

<span data-ttu-id="37e43-175">Для `/Home/About?culture=cs`:</span><span class="sxs-lookup"><span data-stu-id="37e43-175">For `/Home/About?culture=cs`:</span></span>

```html
Existuje jedna položka.
Existují 2 položky.
Existuje 5 položek.
```

<span data-ttu-id="37e43-176">Обратите внимание, что для чешского языка все три перевода различаются.</span><span class="sxs-lookup"><span data-stu-id="37e43-176">Note that for the Czech culture, the three translations are different.</span></span> <span data-ttu-id="37e43-177">На французском и английском языках для двух последних переведенных строк используется одинаковая конструкция.</span><span class="sxs-lookup"><span data-stu-id="37e43-177">The French and English cultures share the same construction for the two last translated strings.</span></span>

## <a name="advanced-tasks"></a><span data-ttu-id="37e43-178">Расширенные задачи</span><span class="sxs-lookup"><span data-stu-id="37e43-178">Advanced tasks</span></span>

### <a name="contextualizing-strings"></a><span data-ttu-id="37e43-179">Учет контекста строк</span><span class="sxs-lookup"><span data-stu-id="37e43-179">Contextualizing strings</span></span>

<span data-ttu-id="37e43-180">Приложения часто содержат переводимые строки в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="37e43-180">Applications often contain the strings to be translated in several places.</span></span> <span data-ttu-id="37e43-181">Одна и та же строка, находящаяся в разных местах приложения (представления Razor или файлы классов), может переводиться по-разному.</span><span class="sxs-lookup"><span data-stu-id="37e43-181">The same string may have a different translation in certain locations within an app (Razor views or class files).</span></span> <span data-ttu-id="37e43-182">Файл PO поддерживает понятие контекста файла, которое можно использовать для классификации представляемых строк.</span><span class="sxs-lookup"><span data-stu-id="37e43-182">A PO file supports the notion of a file context, which can be used to categorize the string being represented.</span></span> <span data-ttu-id="37e43-183">В зависимости от контекста файла (или его отсутствия) строку можно перевести по-разному.</span><span class="sxs-lookup"><span data-stu-id="37e43-183">Using a file context, a string can be translated differently, depending on the file context (or lack of a file context).</span></span>

<span data-ttu-id="37e43-184">Службы локализации PO используют имя полного класса или представление, используемые при переводе строки.</span><span class="sxs-lookup"><span data-stu-id="37e43-184">The PO localization services use the name of the full class or the view that's used when translating a string.</span></span> <span data-ttu-id="37e43-185">Это достигается путем установки значения для записи `msgctxt`.</span><span class="sxs-lookup"><span data-stu-id="37e43-185">This is accomplished by setting the value on the `msgctxt` entry.</span></span>

<span data-ttu-id="37e43-186">Рассмотрим небольшое дополнение к предыдущему примеру *fr.po*.</span><span class="sxs-lookup"><span data-stu-id="37e43-186">Consider a minor addition to the previous *fr.po* example.</span></span> <span data-ttu-id="37e43-187">Представление Razor, расположенное в *Views/Home/About.cshtml*, можно определить в качестве контекста файла, задав зарезервированное значение записи `msgctxt`:</span><span class="sxs-lookup"><span data-stu-id="37e43-187">A Razor view located at *Views/Home/About.cshtml* can be defined as the file context by setting the reserved `msgctxt` entry's value:</span></span>

```text
msgctxt "Views.Home.About"
msgid "Hello world!"
msgstr "Bonjour le monde!"
```

<span data-ttu-id="37e43-188">При такой настройке `msgctxt` перевод текста отображается при переходе по адресу `/Home/About?culture=fr-FR`.</span><span class="sxs-lookup"><span data-stu-id="37e43-188">With the `msgctxt` set as such, text translation occurs when navigating to `/Home/About?culture=fr-FR`.</span></span> <span data-ttu-id="37e43-189">При переходе по адресу `/Home/Contact?culture=fr-FR` перевод не отображается.</span><span class="sxs-lookup"><span data-stu-id="37e43-189">The translation won't occur when navigating to `/Home/Contact?culture=fr-FR`.</span></span>

<span data-ttu-id="37e43-190">Если с заданным контекстом файла не совпадает ни одна из конкретных записей, резервный механизм Orchard Core ищет соответствующий файл PO без контекста.</span><span class="sxs-lookup"><span data-stu-id="37e43-190">When no specific entry is matched with a given file context, Orchard Core's fallback mechanism looks for an appropriate PO file without a context.</span></span> <span data-ttu-id="37e43-191">Если предположить, что для *Views/Home/Contact.cshtml* не задан никакой контекст, при переходе по адресу `/Home/Contact?culture=fr-FR` загружается файл PO, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="37e43-191">Assuming there's no specific file context defined for *Views/Home/Contact.cshtml*, navigating to `/Home/Contact?culture=fr-FR` loads a PO file such as:</span></span>

[!code-text[](localization/sample/POLocalization/fr.po)]

### <a name="changing-the-location-of-po-files"></a><span data-ttu-id="37e43-192">Изменение расположения для файлов PO</span><span class="sxs-lookup"><span data-stu-id="37e43-192">Changing the location of PO files</span></span>

<span data-ttu-id="37e43-193">Расположение по умолчанию для файлов PO можно изменить в `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="37e43-193">The default location of PO files can be changed in `ConfigureServices`:</span></span>

```csharp
services.AddPortableObjectLocalization(options => options.ResourcesPath = "Localization");
```

<span data-ttu-id="37e43-194">В этом примере файлы PO загружаются из папки *Localization*.</span><span class="sxs-lookup"><span data-stu-id="37e43-194">In this example, the PO files are loaded from the *Localization* folder.</span></span>

### <a name="implementing-a-custom-logic-for-finding-localization-files"></a><span data-ttu-id="37e43-195">Реализация настраиваемой логики для поиска файлов локализации</span><span class="sxs-lookup"><span data-stu-id="37e43-195">Implementing a custom logic for finding localization files</span></span>

<span data-ttu-id="37e43-196">Когда для поиска файлов PO требуется более сложная логика, можно реализовать интерфейс `OrchardCore.Localization.PortableObject.ILocalizationFileLocationProvider` и зарегистрировать его как службу.</span><span class="sxs-lookup"><span data-stu-id="37e43-196">When more complex logic is needed to locate PO files, the `OrchardCore.Localization.PortableObject.ILocalizationFileLocationProvider` interface can be implemented and registered as a service.</span></span> <span data-ttu-id="37e43-197">Это удобно, когда файлы PO могут храниться в различных расположениях или должны находиться в иерархии папок.</span><span class="sxs-lookup"><span data-stu-id="37e43-197">This is useful when PO files can be stored in varying locations or when the files have to be found within a hierarchy of folders.</span></span>

### <a name="using-a-different-default-pluralized-language"></a><span data-ttu-id="37e43-198">Использование языка с другими формами множественного числа по умолчанию</span><span class="sxs-lookup"><span data-stu-id="37e43-198">Using a different default pluralized language</span></span>

<span data-ttu-id="37e43-199">Этот пакет содержит метод расширения `Plural`, характерный для двух форм множественного числа.</span><span class="sxs-lookup"><span data-stu-id="37e43-199">The package includes a `Plural` extension method that's specific to two plural forms.</span></span> <span data-ttu-id="37e43-200">Для языков с большим числом форм множественного числа нужно создать отдельный метод расширения.</span><span class="sxs-lookup"><span data-stu-id="37e43-200">For languages requiring more plural forms, create an extension method.</span></span> <span data-ttu-id="37e43-201">При наличии метода расширения вам не потребуется предоставлять файл локализации для языка по умолчанию &mdash;, исходные строки уже доступны непосредственно в коде.</span><span class="sxs-lookup"><span data-stu-id="37e43-201">With an extension method, you won't need to provide any localization file for the default language &mdash; the original strings are already available directly in the code.</span></span>

<span data-ttu-id="37e43-202">Можно использовать более универсальную перегрузку `Plural(int count, string[] pluralForms, params object[] arguments)`, которая принимает строковый массив переводов.</span><span class="sxs-lookup"><span data-stu-id="37e43-202">You can use the more generic `Plural(int count, string[] pluralForms, params object[] arguments)` overload which accepts a string array of translations.</span></span>
