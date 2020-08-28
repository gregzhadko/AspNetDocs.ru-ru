---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: Часть 6. Использование заметок к данным для проверки модели | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 6 охватывает использование заметок к данным для модели V...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 24d3f028a9a720e5b526518624c9c1c2ce2c37d4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044952"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="5d362-104">Часть 6. Использование заметок к данным для проверки модели</span><span class="sxs-lookup"><span data-stu-id="5d362-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="5d362-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="5d362-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="5d362-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="5d362-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="5d362-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="5d362-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="5d362-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5d362-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="5d362-109">Часть 6 охватывает использование заметок к данным для проверки модели.</span><span class="sxs-lookup"><span data-stu-id="5d362-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="5d362-110">У нас возникли серьезные проблемы с формами создания и редактирования: они не выполняют проверку.</span><span class="sxs-lookup"><span data-stu-id="5d362-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="5d362-111">Мы можем выполнить такие действия, как оставить обязательные поля пустыми или ввести буквы в поле Price, и первая ошибка, которую мы будем видеть, — из базы данных.</span><span class="sxs-lookup"><span data-stu-id="5d362-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="5d362-112">Можно легко добавить проверку в наше приложение, добавив заметки к данным в наши классы модели.</span><span class="sxs-lookup"><span data-stu-id="5d362-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="5d362-113">Заметки к данным позволяют описать правила, которые мы хотим применить к нашим свойствам модели, и ASP.NET MVC обеспечит их применение и отображение соответствующих сообщений для наших пользователей.</span><span class="sxs-lookup"><span data-stu-id="5d362-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="5d362-114">Добавление проверки в формы альбома</span><span class="sxs-lookup"><span data-stu-id="5d362-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="5d362-115">Мы будем использовать следующие атрибуты аннотации данных:</span><span class="sxs-lookup"><span data-stu-id="5d362-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="5d362-116">**Обязательное** — указывает, что свойство является обязательным полем.</span><span class="sxs-lookup"><span data-stu-id="5d362-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="5d362-117">**DisplayName** — определяет текст, используемый в полях формы и сообщениях проверки.</span><span class="sxs-lookup"><span data-stu-id="5d362-117">**DisplayName** – Defines the text to use on form fields and validation messages</span></span>
- <span data-ttu-id="5d362-118">**StringLength** — определяет максимальную длину для строкового поля</span><span class="sxs-lookup"><span data-stu-id="5d362-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="5d362-119">**Range** — задает максимальное и минимальное значение для числового поля.</span><span class="sxs-lookup"><span data-stu-id="5d362-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="5d362-120">**BIND** — перечисляет поля, которые следует исключить или включить при привязке значений параметров или форм к свойствам модели.</span><span class="sxs-lookup"><span data-stu-id="5d362-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="5d362-121">**Скаффолдколумн** — позволяет скрывать поля из форм редактора</span><span class="sxs-lookup"><span data-stu-id="5d362-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="5d362-122">*Примечание. Дополнительные сведения о проверке модели с помощью атрибутов заметок к данным см. в документации MSDN по адресу*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="5d362-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="5d362-123">Откройте класс альбома и добавьте в начало следующие операторы *using* .</span><span class="sxs-lookup"><span data-stu-id="5d362-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="5d362-124">Затем обновите свойства, чтобы добавить атрибуты отображения и проверки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5d362-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="5d362-125">Мы также изменили жанр и исполнитель на виртуальные свойства.</span><span class="sxs-lookup"><span data-stu-id="5d362-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="5d362-126">Это позволяет Entity Framework с отложенной загрузкой при необходимости.</span><span class="sxs-lookup"><span data-stu-id="5d362-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="5d362-127">После добавления этих атрибутов в модель альбома на экране создания и редактирования сразу же начинается проверка полей и использование отображаемых имен (например, URL-адрес обложки альбома вместо Албумартурл).</span><span class="sxs-lookup"><span data-stu-id="5d362-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="5d362-128">Запустите приложение и перейдите по/Стореманажер/креате..</span><span class="sxs-lookup"><span data-stu-id="5d362-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="5d362-129">Далее мы будем разбивать некоторые правила проверки.</span><span class="sxs-lookup"><span data-stu-id="5d362-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="5d362-130">Введите цену 0 и оставьте поле заголовок пустым.</span><span class="sxs-lookup"><span data-stu-id="5d362-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="5d362-131">При нажатии кнопки "создать" отобразится форма с сообщениями об ошибках проверки, показывающими, какие поля не соответствуют определенным Вами правилам проверки.</span><span class="sxs-lookup"><span data-stu-id="5d362-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="5d362-132">Тестирование проверки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="5d362-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="5d362-133">Проверка на стороне сервера очень важна с точки зрения приложения, так как пользователи могут обойти проверку на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="5d362-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="5d362-134">Однако формы веб-страниц, реализующие проверку на стороне сервера, представляют три существенных проблемы.</span><span class="sxs-lookup"><span data-stu-id="5d362-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="5d362-135">Пользователь должен подождать, пока форма будет отправлена, проверена на сервере и отправить ответ в браузер.</span><span class="sxs-lookup"><span data-stu-id="5d362-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="5d362-136">Пользователь не получает мгновенной отзыв об исправлении поля, чтобы оно передавало правила проверки.</span><span class="sxs-lookup"><span data-stu-id="5d362-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="5d362-137">Мы тратим ресурсы сервера на выполнение логики проверки вместо использования браузера пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d362-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="5d362-138">К счастью, шаблоны шаблонов ASP.NET MVC 3 имеют встроенную проверку на стороне клиента, что не требует дополнительной работы.</span><span class="sxs-lookup"><span data-stu-id="5d362-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="5d362-139">Ввод одной буквы в поле Title удовлетворяет требованиям проверки, поэтому сообщение проверки немедленно удаляется.</span><span class="sxs-lookup"><span data-stu-id="5d362-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="5d362-140">[Назад](mvc-music-store-part-5.md)
> [Вперед](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="5d362-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
