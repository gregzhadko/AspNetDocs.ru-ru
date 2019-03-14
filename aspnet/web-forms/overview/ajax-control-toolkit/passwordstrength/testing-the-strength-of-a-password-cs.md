---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: Тестирование надежности пароля (C#) | Документация Майкрософт
author: wenz
description: Таким образом, чтобы отложенной Пользователи склонны выберите простые пароли, которые легко взломать пароли в любом месте, являются обязательными. Элемент управления PasswordStrength в ASP. Н...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: b71744df46f8b8d20efafa333a10370397c37d2f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048411"
---
<a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="f4dd7-104">Тестирование надежности пароля (C#)</span><span class="sxs-lookup"><span data-stu-id="f4dd7-104">Testing the Strength of a Password (C#)</span></span>
====================
<span data-ttu-id="f4dd7-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f4dd7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f4dd7-106">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f4dd7-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="f4dd7-107">Таким образом, чтобы отложенной Пользователи склонны выберите простые пароли, которые легко взломать пароли в любом месте, являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="f4dd7-108">PasswordStrength управления в ASP.NET AJAX Control Toolkit можно проверить, насколько хорошо работает пароль.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="f4dd7-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="f4dd7-109">Overview</span></span>

<span data-ttu-id="f4dd7-110">Таким образом, чтобы отложенной Пользователи склонны выберите простые пароли, которые легко взломать пароли в любом месте, являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="f4dd7-111">`PasswordStrength` Элемента управления в ASP.NET AJAX Control Toolkit можно проверить, насколько хорошо работает пароль.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="f4dd7-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="f4dd7-112">Steps</span></span>

<span data-ttu-id="f4dd7-113">`PasswordStrength` Управления расширяет текстовое поле и проверяет, является ли пароль в нем достаточно хорошо.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="f4dd7-114">Он предлагает множество возможностей с помощью атрибутов; Ниже приведены лишь некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="f4dd7-115">`MinimumNumericCharacters` Минимальное число цифр в пароле</span><span class="sxs-lookup"><span data-stu-id="f4dd7-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="f4dd7-116">`MinimumSymbolCharacters` Минимальное число специальных символов (не буквы и цифры) в пароле</span><span class="sxs-lookup"><span data-stu-id="f4dd7-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="f4dd7-117">`PreferredPasswordLength` Минимальная длина пароля</span><span class="sxs-lookup"><span data-stu-id="f4dd7-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="f4dd7-118">`RequiresUpperAndLowerCaseCharacters` нужно ли использовать прописные и строчные буквы пароль</span><span class="sxs-lookup"><span data-stu-id="f4dd7-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="f4dd7-119">`StrengthIndicatorType` Предоставляет информацию, как представлять стойкость пароля, как текст (значение `"Text"`) или в качестве своего рода индикатор хода выполнения (значение `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="f4dd7-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="f4dd7-120">В `DisplayPosition` атрибут, настройкой где отображаются сведения.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="f4dd7-121">Ниже приведен полный пример, включая ASP.NET AJAX `ScriptManager` управления `PasswordStrength` управления и, конечно, текстовое поле, где пользователь может ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="f4dd7-122">Для целей демонстрации поле последняя форма является регулярное текстовое поле, а не поле пароля, чтобы вы могли видеть во время разработки, при вводе.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="f4dd7-123">Откройте страницу и введите сейчас: Только после ввода строчные буквы, прописные буквы, цифры и символы, считается как неразрывный пароль.</span><span class="sxs-lookup"><span data-stu-id="f4dd7-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="f4dd7-124">[![Теперь пароль (), неплохо](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f4dd7-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="f4dd7-125">Теперь пароль (), неплохо ([Просмотр полноразмерного изображения](testing-the-strength-of-a-password-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f4dd7-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f4dd7-126">Вперед</span><span class="sxs-lookup"><span data-stu-id="f4dd7-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
