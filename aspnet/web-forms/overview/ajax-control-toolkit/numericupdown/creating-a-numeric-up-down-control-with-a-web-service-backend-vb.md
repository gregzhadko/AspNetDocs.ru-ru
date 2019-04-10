---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: Создание числового вверх/вниз элемента управления с помощью серверной веб-службы (Visual Basic) | Документация Майкрософт
author: wenz
description: Вместо позволить пользователю ввести значение в типа "флажок", числовой вверх/вниз элемента управления (который существует в Windows и других операционных системах) может оказаться как дополнительные c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 0442b5e22e44e0767825026b26ad3da55777b962
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384270"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="84a18-103">Создание числового поля со стрелками "вверх/вниз" с помощью серверной веб-службы (VB)</span><span class="sxs-lookup"><span data-stu-id="84a18-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>

<span data-ttu-id="84a18-104">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="84a18-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="84a18-105">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="84a18-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="84a18-106">Вместо позволить пользователю ввести значение в типа "флажок", числовой вверх/вниз элемента управления (который существует в Windows и других операционных системах) может оказаться как более уверенно.</span><span class="sxs-lookup"><span data-stu-id="84a18-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="84a18-107">По умолчанию элемент управления NumericUpDown всегда увеличивает или уменьшает значение на 1, но веб-службы подтверждает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="84a18-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="84a18-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="84a18-108">Overview</span></span>

<span data-ttu-id="84a18-109">Вместо позволить пользователю ввести значение в типа "флажок", числовой вверх/вниз элемента управления (который существует в Windows и других операционных системах) может оказаться как более уверенно.</span><span class="sxs-lookup"><span data-stu-id="84a18-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="84a18-110">По умолчанию `NumericUpDown` управления всегда увеличивает или уменьшает значение на 1, но веб-службы подтверждает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="84a18-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="84a18-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="84a18-111">Steps</span></span>

<span data-ttu-id="84a18-112">ASP.NET AJAX Control Toolkit содержит `NumericUpDown` расширителя, который автоматически добавляет две кнопки в текстовое поле: Одно для увеличения его значения, один для его уменьшения.</span><span class="sxs-lookup"><span data-stu-id="84a18-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="84a18-113">Однако элемент управления также поддерживает вызов веб-службы (или вызов метода страницы).</span><span class="sxs-lookup"><span data-stu-id="84a18-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="84a18-114">При каждом щелчке вверх или вниз, JavaScript, код подключается к веб-сервер и выполняет метод существует.</span><span class="sxs-lookup"><span data-stu-id="84a18-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="84a18-115">Подпись метода — приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="84a18-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="84a18-116">`current` Аргумент является текущее значение в текстовом поле; `tag` атрибут является дополнительный контекст данных, которое можно задать в качестве свойства `NumericUpDown` расширитель (но не является обязательным).</span><span class="sxs-lookup"><span data-stu-id="84a18-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="84a18-117">В данном примере числовые вверх/вниз элемента управления должны разрешены только значения, являющиеся степенями двух: 1, 2, 4, 8, 16, 32, 64 и т. д.</span><span class="sxs-lookup"><span data-stu-id="84a18-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="84a18-118">Следовательно метод, выполняемый, когда пользователь хочет увеличить значение должен double старое значение; другой метод необходимо разделить значение два.</span><span class="sxs-lookup"><span data-stu-id="84a18-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="84a18-119">Итак, вот полный веб-службы:</span><span class="sxs-lookup"><span data-stu-id="84a18-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="84a18-120">Наконец создайте новую страницу ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="84a18-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="84a18-121">Как правило, требуется `ScriptManager` элемента управления, `TextBox` управления и `NumericUpDownExtender` элемента управления.</span><span class="sxs-lookup"><span data-stu-id="84a18-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="84a18-122">Для последнего необходимо предоставить данные веб-службы:</span><span class="sxs-lookup"><span data-stu-id="84a18-122">For the latter, you have to provide the web service information:</span></span>

- `ServiceDownMethod` <span data-ttu-id="84a18-123">Имя от списка веб-метода или странице метод</span><span class="sxs-lookup"><span data-stu-id="84a18-123">name of the down web method or page method</span></span>
- `ServiceDownPath` <span data-ttu-id="84a18-124">путь к веб-службы с помощью метода вниз службы; пропустить, если вы используете метод страницы</span><span class="sxs-lookup"><span data-stu-id="84a18-124">path to the web service with the down service method; omit if you are using a page method</span></span>
- `ServiceUpMethod` <span data-ttu-id="84a18-125">Имя вверх веб-метода или странице метод</span><span class="sxs-lookup"><span data-stu-id="84a18-125">name of the up web method or page method</span></span>
- `ServiceUpPath` <span data-ttu-id="84a18-126">путь к веб-службы с помощью метода вверх службы; пропустить, если вы используете метод страницы</span><span class="sxs-lookup"><span data-stu-id="84a18-126">path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="84a18-127">Вот полная разметка для страницы:</span><span class="sxs-lookup"><span data-stu-id="84a18-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="84a18-128">При запуске страницы, обратите внимание на то, как значение в текстовое поле всегда удваивается при нажмите кнопку "верхний" и уменьшается вдвое при нажатии на кнопку ниже.</span><span class="sxs-lookup"><span data-stu-id="84a18-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


[![O<span data-ttu-id="84a18-129">чтение чисел, которые являются степенью двойки отображаются]</span><span class="sxs-lookup"><span data-stu-id="84a18-129">nly numbers that are a power of 2 appear]</span></span>(creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

<span data-ttu-id="84a18-130">Отображаются только те числа, которые являются степенью двойки ([Просмотр полноразмерного изображения](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="84a18-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="84a18-131">Назад</span><span class="sxs-lookup"><span data-stu-id="84a18-131">Previous</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
