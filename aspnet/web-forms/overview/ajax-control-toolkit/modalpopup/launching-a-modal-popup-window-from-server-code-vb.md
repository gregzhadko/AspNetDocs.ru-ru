---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: Запуск модального всплывающего окна из серверного кода (Visual Basic) | Документация Майкрософт
author: wenz
description: Элемент управления ModalPopup в AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью средств на стороне клиента. Тем не менее в некоторых сценариях требуется, t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 55ee67150d1567a0334988a06ff0fcca8a89bbd4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404056"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a><span data-ttu-id="4d092-104">Запуск модального всплывающего окна из серверного кода (VB)</span><span class="sxs-lookup"><span data-stu-id="4d092-104">Launching a Modal Popup Window from Server Code (VB)</span></span>

<span data-ttu-id="4d092-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4d092-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4d092-106">[Скачать код](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4d092-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span></span>

> <span data-ttu-id="4d092-107">Элемент управления ModalPopup в AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью средств на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="4d092-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="4d092-108">Тем не менее в некоторых сценариях требуется запуск Открытие модального всплывающего окна на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="4d092-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>


## <a name="overview"></a><span data-ttu-id="4d092-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="4d092-109">Overview</span></span>

<span data-ttu-id="4d092-110">Элемент управления ModalPopup в AJAX Control Toolkit предоставляет простой способ создания модального всплывающего окна с помощью средств на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="4d092-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="4d092-111">Тем не менее в некоторых сценариях требуется запуск Открытие модального всплывающего окна на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="4d092-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="4d092-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="4d092-112">Steps</span></span>

<span data-ttu-id="4d092-113">Во-первых веб-элемента управления кнопки ASP.NET должен продемонстрировать, как работает элемент управления ModalPopup.</span><span class="sxs-lookup"><span data-stu-id="4d092-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="4d092-114">Добавьте кнопку в &lt;формы&gt; элемент на новой странице:</span><span class="sxs-lookup"><span data-stu-id="4d092-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

<span data-ttu-id="4d092-115">Затем необходимо разметку для контекстного меню, которые вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="4d092-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="4d092-116">Определяют его как `<asp:Panel>` управления и убедитесь, что он включает элемент управления Button.</span><span class="sxs-lookup"><span data-stu-id="4d092-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="4d092-117">Элемент управления ModalPopup предоставляет функциональные возможности для создания такой кнопки закрытия контекстного меню. в противном случае нет простого способа перейдите к нему упразднены.</span><span class="sxs-lookup"><span data-stu-id="4d092-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

<span data-ttu-id="4d092-118">Добавьте элемент управления ModalPopup из набора средств AJAX ASP.NET на страницу.</span><span class="sxs-lookup"><span data-stu-id="4d092-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="4d092-119">Задать свойства для кнопки, который загружает элемент управления, кнопки, что делает его исчезают и идентификатор фактическое всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="4d092-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

<span data-ttu-id="4d092-120">Как и все веб-страницы, на базе ASP.NET AJAX; Диспетчера скриптов, необходимый для загрузки библиотеки JavaScript, необходимые для различных браузеры:</span><span class="sxs-lookup"><span data-stu-id="4d092-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

<span data-ttu-id="4d092-121">Запустите пример в браузере.</span><span class="sxs-lookup"><span data-stu-id="4d092-121">Run the example in the browser.</span></span> <span data-ttu-id="4d092-122">При нажатии кнопки на кнопке, откроется модальное всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="4d092-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="4d092-123">Чтобы получить тот же эффект, с помощью кода на стороне сервера, необходима новая кнопка:</span><span class="sxs-lookup"><span data-stu-id="4d092-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

<span data-ttu-id="4d092-124">Как вы видите, нажмите кнопку создает обратную передачу и выполняет `ServerButton_Click()` метод на сервере.</span><span class="sxs-lookup"><span data-stu-id="4d092-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="4d092-125">В этом методе вызывается функция JavaScript `launchModal()` выполняется должна быть точной, функция JavaScript, которая выполняется после загрузки страницы:</span><span class="sxs-lookup"><span data-stu-id="4d092-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

<span data-ttu-id="4d092-126">Задача `launchModal()` является отображение ModalPopup.</span><span class="sxs-lookup"><span data-stu-id="4d092-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="4d092-127">`launchModal()` Функция выполняется после загрузки страницы HTML.</span><span class="sxs-lookup"><span data-stu-id="4d092-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="4d092-128">В этот момент Однако платформа AJAX для ASP.NET не был полностью загружен еще.</span><span class="sxs-lookup"><span data-stu-id="4d092-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="4d092-129">Таким образом `launchModal()` функция просто задает переменную, которая впоследствии необходимо отображать элемент управления ModalPopup:</span><span class="sxs-lookup"><span data-stu-id="4d092-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

<span data-ttu-id="4d092-130">`pageLoad()` Функция JavaScript — это специальная функция, которая выполняется после полной загрузки ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="4d092-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="4d092-131">Поэтому добавим код этой функции для отображения элемента управления ModalPopup, но только если `launchModal()` был вызван до:</span><span class="sxs-lookup"><span data-stu-id="4d092-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

<span data-ttu-id="4d092-132">`$find()` Функция ищет именованный элемент на странице и ожидает, что в качестве параметра идентификатор на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="4d092-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="4d092-133">Таким образом `$find("mpe")` возвращает представление клиентского элемента управления ModalPopup; его `show()` метод позволяет отображается всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="4d092-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>


[![T<span data-ttu-id="4d092-134">он модальное всплывающее окно появляется при нажатии одной из кнопок]</span><span class="sxs-lookup"><span data-stu-id="4d092-134">he modal popup appears when either of the buttons is clicked]</span></span>(launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)

<span data-ttu-id="4d092-135">Модальное всплывающее окно появляется при нажатии одной из кнопок ([Просмотр полноразмерного изображения](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4d092-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4d092-136">[Назад](positioning-a-modalpopup-cs.md)
> [Вперед](using-modalpopup-with-a-repeater-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4d092-136">[Previous](positioning-a-modalpopup-cs.md)
[Next](using-modalpopup-with-a-repeater-control-vb.md)</span></span>
