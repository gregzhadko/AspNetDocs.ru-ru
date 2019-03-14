---
ms.openlocfilehash: 939231583679d469d01724cc1a405bd45e46d2c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57175901"
---
```console
npm run release
```

<span data-ttu-id="41aa2-101">Эта команда создает ресурсы на стороне клиента, которые будут обслуживаться при выполнении приложения.</span><span class="sxs-lookup"><span data-stu-id="41aa2-101">This command yields the client-side assets to be served when running the app.</span></span> <span data-ttu-id="41aa2-102">Эти ресурсы помещаются в папку *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="41aa2-102">The assets are placed in the *wwwroot* folder.</span></span>

<span data-ttu-id="41aa2-103">Веб-пакет выполнил следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="41aa2-103">Webpack completed the following tasks:</span></span>

* <span data-ttu-id="41aa2-104">Очистка содержимого каталога *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="41aa2-104">Purged the contents of the *wwwroot* directory.</span></span>
* <span data-ttu-id="41aa2-105">Преобразование TypeScript в JavaScript (&mdash;этот процесс называется *транспилированием*).</span><span class="sxs-lookup"><span data-stu-id="41aa2-105">Converted the TypeScript to JavaScript&mdash;a process known as *transpilation*.</span></span>
* <span data-ttu-id="41aa2-106">Корректировка созданного кода JavaScript в целях уменьшения размера файла (&mdash;этот процесс называется *минификацией*).</span><span class="sxs-lookup"><span data-stu-id="41aa2-106">Mangled the generated JavaScript to reduce file size&mdash;a process known as *minification*.</span></span>
* <span data-ttu-id="41aa2-107">Копирование обработанных файлов JavaScript, CSS и HTML из каталога *src* в *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="41aa2-107">Copied the processed JavaScript, CSS, and HTML files from *src* to the *wwwroot* directory.</span></span>
* <span data-ttu-id="41aa2-108">Внедрение следующих элементов в файл *wwwroot/index.html*:</span><span class="sxs-lookup"><span data-stu-id="41aa2-108">Injected the following elements into the *wwwroot/index.html* file:</span></span>
    * <span data-ttu-id="41aa2-109">Тег `<link>`, ссылающийся на файл *wwwroot/main.\<hash\>.css*.</span><span class="sxs-lookup"><span data-stu-id="41aa2-109">A `<link>` tag, referencing the *wwwroot/main.\<hash\>.css* file.</span></span> <span data-ttu-id="41aa2-110">Этот тег размещается непосредственно после закрывающего тега `</head>`.</span><span class="sxs-lookup"><span data-stu-id="41aa2-110">This tag is placed immediately before the closing `</head>` tag.</span></span>
    * <span data-ttu-id="41aa2-111">Тег `<script>`, ссылающийся на минифицированный файл *wwwroot/main.\<hash\>.js*.</span><span class="sxs-lookup"><span data-stu-id="41aa2-111">A `<script>` tag, referencing the minified *wwwroot/main.\<hash\>.js* file.</span></span> <span data-ttu-id="41aa2-112">Этот тег размещается непосредственно после закрывающего тега `</body>`.</span><span class="sxs-lookup"><span data-stu-id="41aa2-112">This tag is placed immediately before the closing `</body>` tag.</span></span>
