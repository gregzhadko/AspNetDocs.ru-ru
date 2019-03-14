---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Создание числового вверх/вниз элемента управления с помощью серверной веб-службы (C#) | Документация Майкрософт
author: wenz
description: Вместо позволить пользователю ввести значение в типа "флажок", числовой вверх/вниз элемента управления (который существует в Windows и других операционных системах) может оказаться как дополнительные c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: ffefed61e259994990315d17a545ef74074092a6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050731"
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="7f4fd-103">Создание числового поля со стрелками "вверх/вниз" с помощью серверной веб-службы (C#)</span><span class="sxs-lookup"><span data-stu-id="7f4fd-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>
====================
<span data-ttu-id="7f4fd-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7f4fd-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7f4fd-105">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7f4fd-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="7f4fd-106">Вместо позволить пользователю ввести значение в типа "флажок", числовой вверх/вниз элемента управления (который существует в Windows и других операционных системах) может оказаться как более уверенно.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="7f4fd-107">По умолчанию элемент управления NumericUpDown всегда увеличивает или уменьшает значение на 1, но веб-службы подтверждает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="7f4fd-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="7f4fd-108">Overview</span></span>

<span data-ttu-id="7f4fd-109">Вместо позволить пользователю ввести значение в типа "флажок", числовой вверх/вниз элемента управления (который существует в Windows и других операционных системах) может оказаться как более уверенно.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="7f4fd-110">По умолчанию `NumericUpDown` управления всегда увеличивает или уменьшает значение на 1, но веб-службы подтверждает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="7f4fd-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="7f4fd-111">Steps</span></span>

<span data-ttu-id="7f4fd-112">ASP.NET AJAX Control Toolkit содержит `NumericUpDown` расширителя, который автоматически добавляет две кнопки в текстовое поле: Одно для увеличения его значения, один для его уменьшения.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="7f4fd-113">Однако элемент управления также поддерживает вызов веб-службы (или вызов метода страницы).</span><span class="sxs-lookup"><span data-stu-id="7f4fd-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="7f4fd-114">При каждом щелчке вверх или вниз, JavaScript, код подключается к веб-сервер и выполняет метод существует.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="7f4fd-115">Подпись метода — приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="7f4fd-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="7f4fd-116">`current` Аргумент является текущее значение в текстовом поле; `tag` атрибут является дополнительный контекст данных, которое можно задать в качестве свойства `NumericUpDown` расширитель (но не является обязательным).</span><span class="sxs-lookup"><span data-stu-id="7f4fd-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="7f4fd-117">В данном примере числовые вверх/вниз элемента управления должны разрешены только значения, являющиеся степенями двух: 1, 2, 4, 8, 16, 32, 64 и т. д.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="7f4fd-118">Следовательно метод, выполняемый, когда пользователь хочет увеличить значение должен double старое значение; другой метод необходимо разделить значение два.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="7f4fd-119">Итак, вот полный веб-службы:</span><span class="sxs-lookup"><span data-stu-id="7f4fd-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="7f4fd-120">Наконец создайте новую страницу ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="7f4fd-121">Как правило, требуется `ScriptManager` элемента управления, `TextBox` управления и `NumericUpDownExtender` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="7f4fd-122">Для последнего необходимо предоставить данные веб-службы:</span><span class="sxs-lookup"><span data-stu-id="7f4fd-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="7f4fd-123">`ServiceDownMethod` Имя от списка веб-метода или странице метод</span><span class="sxs-lookup"><span data-stu-id="7f4fd-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="7f4fd-124">`ServiceDownPath` путь к веб-службы с помощью метода вниз службы; пропустить, если вы используете метод страницы</span><span class="sxs-lookup"><span data-stu-id="7f4fd-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="7f4fd-125">`ServiceUpMethod` Имя вверх веб-метода или странице метод</span><span class="sxs-lookup"><span data-stu-id="7f4fd-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="7f4fd-126">`ServiceUpPath` путь к веб-службы с помощью метода вверх службы; пропустить, если вы используете метод страницы</span><span class="sxs-lookup"><span data-stu-id="7f4fd-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="7f4fd-127">Вот полная разметка для страницы:</span><span class="sxs-lookup"><span data-stu-id="7f4fd-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="7f4fd-128">При запуске страницы, обратите внимание на то, как значение в текстовое поле всегда удваивается при нажмите кнопку "верхний" и уменьшается вдвое при нажатии на кнопку ниже.</span><span class="sxs-lookup"><span data-stu-id="7f4fd-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="7f4fd-129">[![Отображаются только те числа, которые являются степенью числа 2](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7f4fd-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="7f4fd-130">Отображаются только те числа, которые являются степенью двойки ([Просмотр полноразмерного изображения](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7f4fd-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7f4fd-131">Вперед</span><span class="sxs-lookup"><span data-stu-id="7f4fd-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
