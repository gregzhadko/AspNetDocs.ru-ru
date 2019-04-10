---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: С помощью расширитель элемента управления ColorPicker (VB) | Документация Майкрософт
author: microsoft
description: ColorPicker является расширитель ASP.NET AJAX, который предоставляет функции выбора цвета на стороне клиента с помощью пользовательского интерфейса в элементе управления всплывающего окна. Его можно подключить к любой ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 311cd61ae971dd6b902411eca87f75f87f5868ae
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384063"
---
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="af689-104">С помощью расширитель элемента управления ColorPicker (VB)</span><span class="sxs-lookup"><span data-stu-id="af689-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="af689-105">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="af689-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="af689-106">ColorPicker является расширитель ASP.NET AJAX, который предоставляет функции выбора цвета на стороне клиента с помощью пользовательского интерфейса в элементе управления всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="af689-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="af689-107">Его можно подключить к любому элементу управления ASP.NET TextBox.</span><span class="sxs-lookup"><span data-stu-id="af689-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="af689-108">Его.</span><span class="sxs-lookup"><span data-stu-id="af689-108">It.</span></span>


<span data-ttu-id="af689-109">Чтобы объяснить, как используется расширитель элемента управления ColorPicker набор средств управления AJAX является целью данного учебника.</span><span class="sxs-lookup"><span data-stu-id="af689-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="af689-110">Расширитель элемента управления ColorPicker отображается всплывающее диалоговое окно, которое позволяет выбрать цвет.</span><span class="sxs-lookup"><span data-stu-id="af689-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="af689-111">ColorPicker параметр полезен, если вы хотите предоставить интуитивный пользовательский интерфейс пользователя для выбора цвета.</span><span class="sxs-lookup"><span data-stu-id="af689-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="af689-112">Расширение управления TextBox с расширитель элемента управления ColorPicker</span><span class="sxs-lookup"><span data-stu-id="af689-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="af689-113">Представьте, например, что вы хотите создать веб-сайт, позволяющий посетителям Создание настроенного визитные карточки.</span><span class="sxs-lookup"><span data-stu-id="af689-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="af689-114">Посетители могут введите текст для бизнес-Карточка и выбрать цвет.</span><span class="sxs-lookup"><span data-stu-id="af689-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="af689-115">Страницы ASP.NET в листинге 1 содержит два элемента управления TextBox с именем txtCardText и txtCardColor.</span><span class="sxs-lookup"><span data-stu-id="af689-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="af689-116">При отправке формы отображаются выбранные значения (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="af689-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>


[![S<span data-ttu-id="af689-117">простые формы для создания бизнес-карточка]</span><span class="sxs-lookup"><span data-stu-id="af689-117">imple form for creating a business card]</span></span>(using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

<span data-ttu-id="af689-118">**Рис 01**: Простая форма для создания бизнес-карточка ([Просмотр полноразмерного изображения](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="af689-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>


**<span data-ttu-id="af689-119">В листинге 1 - CreateCard.aspx</span><span class="sxs-lookup"><span data-stu-id="af689-119">Listing 1 - CreateCard.aspx</span></span>**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="af689-120">Формы в листинге 1 работает, но он не обеспечивает удобную работу пользователя.</span><span class="sxs-lookup"><span data-stu-id="af689-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="af689-121">Пользователь должен ввести цвет в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="af689-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="af689-122">Если пользователь хочет специализированные color – например, просто правой оттенок green рабочее время —, а затем пользователь должны понять, код цвета HTML без любое Справка.</span><span class="sxs-lookup"><span data-stu-id="af689-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="af689-123">Расширитель элемента управления ColorPicker можно использовать для создания удобства работы пользователя.</span><span class="sxs-lookup"><span data-stu-id="af689-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="af689-124">ColorPicker отображает диалоговое окно цвет при перемещении фокуса в элементе управления TextBox (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="af689-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>


[![T<span data-ttu-id="af689-125">он расширитель элемента управления ColorPicker]</span><span class="sxs-lookup"><span data-stu-id="af689-125">he ColorPicker Control Extender]</span></span>(using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

<span data-ttu-id="af689-126">**Рис. 02**: Расширитель элемента управления ColorPicker ([Просмотр полноразмерного изображения](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="af689-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>


<span data-ttu-id="af689-127">Необходимо выполнить два шага, чтобы использовать расширитель элемента управления ColorPicker с формой в листинге 1:</span><span class="sxs-lookup"><span data-stu-id="af689-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="af689-128">Добавление элемента управления ScriptManager к странице</span><span class="sxs-lookup"><span data-stu-id="af689-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="af689-129">Добавьте на страницу расширитель элемента управления ColorPicker</span><span class="sxs-lookup"><span data-stu-id="af689-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="af689-130">Перед использованием ColorPicker, ScriptManager необходимо добавить на страницу.</span><span class="sxs-lookup"><span data-stu-id="af689-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="af689-131">— Хорошее место для добавления ScriptManager сразу под открывающей серверных &lt;формы&gt; тега.</span><span class="sxs-lookup"><span data-stu-id="af689-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="af689-132">ScriptManager можно перетащить на страницу из области элементов (ScriptManager находится на вкладке расширений AJAX).</span><span class="sxs-lookup"><span data-stu-id="af689-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="af689-133">Кроме того можно ввести следующий тег в представление источника под открывающего тега формы на стороне сервера:</span><span class="sxs-lookup"><span data-stu-id="af689-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="af689-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span><span class="sxs-lookup"><span data-stu-id="af689-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="af689-135">Самый простой способ добавить расширитель элемента управления ColorPicker страницы находится в режиме конструктора.</span><span class="sxs-lookup"><span data-stu-id="af689-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="af689-136">Если навести указатель мыши txtCardColor TextBox одноименное появилась позволяет добавить расширитель (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="af689-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="af689-137">Если вы выберете этот параметр, откроется мастер расширения (см. рис. 4).</span><span class="sxs-lookup"><span data-stu-id="af689-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>


[![A<span data-ttu-id="af689-138">dding расширитель]</span><span class="sxs-lookup"><span data-stu-id="af689-138">dding an extender]</span></span>(using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

<span data-ttu-id="af689-139">**Рис 03**: Добавление расширитель ([Просмотр полноразмерного изображения](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="af689-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>


[![S<span data-ttu-id="af689-140">Отказ от расширитель элемента управления с помощью мастера расширитель]</span><span class="sxs-lookup"><span data-stu-id="af689-140">electing a control extender with the Extender Wizard]</span></span>(using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

<span data-ttu-id="af689-141">**Рис. 04**: Выбрав расширитель элемента управления с помощью мастера расширений ([Просмотр полноразмерного изображения](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="af689-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>


<span data-ttu-id="af689-142">Вы можете выбрать ColorPicker расширителя для расширения txtCardColor TextBox с ColorPicker расширителя.</span><span class="sxs-lookup"><span data-stu-id="af689-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="af689-143">Нажмите кнопку ОК, чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="af689-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="af689-144">После внесения этих изменений, исходный код страницы выглядит как листинг 2.</span><span class="sxs-lookup"><span data-stu-id="af689-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

**<span data-ttu-id="af689-145">В листинге 2 - CreateCard.aspx (с ColorPicker)</span><span class="sxs-lookup"><span data-stu-id="af689-145">Listing 2 - CreateCard.aspx (with ColorPicker)</span></span>**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="af689-146">Обратите внимание на то, что страница теперь содержит элемент управления ColorPickerExtender прямо под txtCardColor элемент управления TextBox.</span><span class="sxs-lookup"><span data-stu-id="af689-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="af689-147">ColorPickerExtender расширяет txtCardColor управления таким образом, чтобы он отображает диалоговое окно выбора цвета.</span><span class="sxs-lookup"><span data-stu-id="af689-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="af689-148">С помощью кнопки, чтобы открыть диалоговое окно выбора цвета</span><span class="sxs-lookup"><span data-stu-id="af689-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="af689-149">Расширитель ColorPicker поддерживает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="af689-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="af689-150">PopupButtonId - идентификатор кнопки на страницу, которая вызывает диалоговое окно выбора цвета для отображения.</span><span class="sxs-lookup"><span data-stu-id="af689-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="af689-151">PopupPosition - положение, относительно конечный элемент управления, диалоговое окно выбора цвета.</span><span class="sxs-lookup"><span data-stu-id="af689-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="af689-152">Возможными значениями являются абсолютное, Center, слева снизу, BottomRight, TopLeft, справа сверху, справа и слева (по умолчанию — слева снизу).</span><span class="sxs-lookup"><span data-stu-id="af689-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="af689-153">SampleControlId - идентификатор элемента управления, который отображает выбранный цвет.</span><span class="sxs-lookup"><span data-stu-id="af689-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="af689-154">SelectedColor - банке ColorPicker цвет.</span><span class="sxs-lookup"><span data-stu-id="af689-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="af689-155">Эти свойства можно использовать для настройки отображения диалоговое окно выбора цвета и способ отображения выбранного цвета.</span><span class="sxs-lookup"><span data-stu-id="af689-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="af689-156">На странице в листинге 3 показано, как можно использовать несколько из этих свойств.</span><span class="sxs-lookup"><span data-stu-id="af689-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

**<span data-ttu-id="af689-157">Листинг 3 - CreateCardButton.aspx</span><span class="sxs-lookup"><span data-stu-id="af689-157">Listing 3 - CreateCardButton.aspx</span></span>**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="af689-158">На странице в листинге 3 включает в себя Выбор цвета кнопки (см. рис. 5).</span><span class="sxs-lookup"><span data-stu-id="af689-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="af689-159">После нажатия этой кнопки, диалоговое окно выбора цвета появляется над текстового поля.</span><span class="sxs-lookup"><span data-stu-id="af689-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="af689-160">Если вы выбираете цвет в диалоговом окне выбранного цвета отображается как цвет фона lblSample элемент управления Label.</span><span class="sxs-lookup"><span data-stu-id="af689-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="af689-161">Свойство ColorPicker PopupButtonID используется должен быть сопоставлен расширителя ColorPicker кнопку выбора цвета.</span><span class="sxs-lookup"><span data-stu-id="af689-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="af689-162">При указании значения для свойства PopupButtonID диалоговое окно выбора цвета больше не отображается, когда целевой элемент управления имеет фокус.</span><span class="sxs-lookup"><span data-stu-id="af689-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="af689-163">Необходимо нажать кнопку для отображения диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="af689-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="af689-164">Свойство SampleControlID позволяет связать элемент управления, который отображает выбранный цвет с ColorPicker.</span><span class="sxs-lookup"><span data-stu-id="af689-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="af689-165">Цвет фона этого элемента управления ColorPicker примет выбранный цвет.</span><span class="sxs-lookup"><span data-stu-id="af689-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>


[![D<span data-ttu-id="af689-166">isplaying диалоговое окно выбора цвета с кнопкой]</span><span class="sxs-lookup"><span data-stu-id="af689-166">isplaying the color picker dialog with a button]</span></span>(using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

<span data-ttu-id="af689-167">**05 рис**: Отображение диалоговое окно выбора цвета с кнопкой ([Просмотр полноразмерного изображения](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="af689-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>


## <a name="summary"></a><span data-ttu-id="af689-168">Сводка</span><span class="sxs-lookup"><span data-stu-id="af689-168">Summary</span></span>

<span data-ttu-id="af689-169">В этом руководстве вы узнали, как использовать расширитель элемента управления ColorPicker, чтобы отобразить всплывающее диалоговое окно выбора цвета.</span><span class="sxs-lookup"><span data-stu-id="af689-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="af689-170">Во-первых мы рассмотрели, как можно отобразить диалоговое окно, при перемещении фокуса на элементе управления TextBox.</span><span class="sxs-lookup"><span data-stu-id="af689-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="af689-171">Далее вы узнали, как создать кнопку, которая отображает диалоговое окно выбора цвета, при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="af689-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="af689-172">Назад</span><span class="sxs-lookup"><span data-stu-id="af689-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
