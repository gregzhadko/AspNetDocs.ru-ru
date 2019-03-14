---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: Перенос данных универсального поставщика членства и профилей пользователей в ASP.NET Identity (C#) | Документация Майкрософт
author: rustd
description: Этот учебник описывает шаги, необходимые для миграции пользователей и роли данных и данные профиля пользователя, созданных с помощью универсальные поставщики существующего приложения...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: a91bb6ac51819d7dbb8eb3c63bd36a9d830eecce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058461"
---
<a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a><span data-ttu-id="529ce-103">Перенос данных универсального поставщика членства и профилей пользователей в ASP.NET Identity (C#)</span><span class="sxs-lookup"><span data-stu-id="529ce-103">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity (C#)</span></span>
====================
<span data-ttu-id="529ce-104">по [Пранавом Растоги](https://github.com/rustd), [Рик Андерсон]((https://twitter.com/RickAndMSFT)), [(Robert McMurray)](https://github.com/rmcmurray), [Suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="529ce-104">by [Pranav Rastogi](https://github.com/rustd), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Robert McMurray](https://github.com/rmcmurray), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="529ce-105">Этом руководстве описаны шаги, необходимые для переноса пользователей и роли данных и данные профиля пользователя, созданных с помощью универсальные поставщики существующего приложения модель удостоверений ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="529ce-105">This tutorial describes the steps that are necessary to migrate user and role data and user profile data created using Universal Providers of an existing application to the ASP.NET Identity model.</span></span> <span data-ttu-id="529ce-106">Этот подход упомянутые здесь, можно использовать для переноса данных профиля пользователя в приложение с помощью членства SQL также.</span><span class="sxs-lookup"><span data-stu-id="529ce-106">The approach mentioned here to migrate user profile data can be used in an application with SQL membership as well.</span></span>


<span data-ttu-id="529ce-107">С выпуском Visual Studio 2013, группа разработчиков ASP.NET представлены новую систему ASP.NET Identity и Дополнительные сведения об этом выпуске [здесь](../../index.md).</span><span class="sxs-lookup"><span data-stu-id="529ce-107">With the release of Visual Studio 2013, the ASP.NET team introduced a new ASP.NET Identity system, and you can read more about that release [here](../../index.md).</span></span> <span data-ttu-id="529ce-108">Вслед за статью, чтобы перенести веб-приложений от [членства SQL в новую систему удостоверений](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md), в этой статье показана последовательность действий для миграции существующих приложений, которые следуют модели поставщиков для Управление пользователями и ролями в новую модель удостоверений.</span><span class="sxs-lookup"><span data-stu-id="529ce-108">Following up on the article to migrate web applications from [SQL Membership to the new Identity system](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md), this article illustrates the steps to migrate existing applications that follow the Providers model for user and role management to the new Identity model.</span></span> <span data-ttu-id="529ce-109">Цель этого учебника будет главным образом на переноса данных профиля пользователя в легко подключить его в новой системе.</span><span class="sxs-lookup"><span data-stu-id="529ce-109">The focus of this tutorial will be primarily on migrating the user profile data to seamlessly hook it into the new system.</span></span> <span data-ttu-id="529ce-110">Миграция сведений о пользователях и роли аналогичен и для членства SQL.</span><span class="sxs-lookup"><span data-stu-id="529ce-110">Migrating user and role information is similar for SQL membership.</span></span> <span data-ttu-id="529ce-111">В приложение с помощью членства SQL также можно использовать подход, выполнить при переносе данных профиля.</span><span class="sxs-lookup"><span data-stu-id="529ce-111">The approach followed to migrate profile data can be used in an application with SQL membership as well.</span></span>

<span data-ttu-id="529ce-112">Например мы начнем с веб-приложения, созданные с помощью Visual Studio 2012, которая использует модель поставщиков.</span><span class="sxs-lookup"><span data-stu-id="529ce-112">As an example, we will start with a web app created using Visual Studio 2012 which uses the Providers model.</span></span> <span data-ttu-id="529ce-113">Мы будем затем добавьте код для управления профилями, регистрации пользователя, добавить данные профиля для пользователей, перенос схемы базы данных и затем изменить приложение, чтобы использовать систему удостоверений Управление пользователями и ролями.</span><span class="sxs-lookup"><span data-stu-id="529ce-113">We'll then add code for profile management, register a user, add profile data for the users, migrate the database schema, and then change the application to use the Identity system for user and role management.</span></span> <span data-ttu-id="529ce-114">Для проверки переноса пользователи, созданных с помощью универсальные поставщики должны иметь возможность входа в систему, и новые пользователи должны иметь возможность регистрации.</span><span class="sxs-lookup"><span data-stu-id="529ce-114">As a test of migration, users created using Universal Providers should be able to log in and new users should be able to register.</span></span>

> [!NOTE]
> <span data-ttu-id="529ce-115">Вы найдете полный пример в [ https://github.com/suhasj/UniversalProviders-Identity-Migrations ](https://github.com/suhasj/UniversalProviders-Identity-Migrations).</span><span class="sxs-lookup"><span data-stu-id="529ce-115">You can find the complete sample at [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations).</span></span>


## <a name="profile-data-migration-summary"></a><span data-ttu-id="529ce-116">Сводка по миграции данных профиля</span><span class="sxs-lookup"><span data-stu-id="529ce-116">Profile data migration summary</span></span>

<span data-ttu-id="529ce-117">Прежде чем начать с миграцией, давайте рассмотрим возможности хранения данных профиля в модели поставщиков.</span><span class="sxs-lookup"><span data-stu-id="529ce-117">Before starting with the migrations, let us look at the experience of storing profile data in the Providers model.</span></span> <span data-ttu-id="529ce-118">Данные профилирования для приложения, которые пользователи могут храниться несколькими способами, наиболее распространенные из них с помощью поставщиков встроенных профилей, поставляемых вместе с универсальные поставщики.</span><span class="sxs-lookup"><span data-stu-id="529ce-118">Profile data for application users can be stored in multiple ways, the most common among them being using the inbuilt profile providers shipped along with the Universal Providers.</span></span> <span data-ttu-id="529ce-119">Включает действия</span><span class="sxs-lookup"><span data-stu-id="529ce-119">The steps would include</span></span>

1. <span data-ttu-id="529ce-120">Добавьте класс, который имеет свойства, используемого для хранения данных профилирования.</span><span class="sxs-lookup"><span data-stu-id="529ce-120">Add a class that has properties used to store Profile data.</span></span>
2. <span data-ttu-id="529ce-121">Добавьте класс, который расширяет «ProfileBase» и реализует методы, чтобы получить указанные выше данные профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="529ce-121">Add a class that extends 'ProfileBase' and implements methods to get the above profile data for the user.</span></span>
3. <span data-ttu-id="529ce-122">Включить с помощью поставщиков профилей по умолчанию в *web.config* файл и определить класс, объявленный на шаге 2 # для использования в доступ к сведениям профиля.</span><span class="sxs-lookup"><span data-stu-id="529ce-122">Enable using default profile providers in the *web.config* file and define the class declared in step #2 to be used in accessing profile information.</span></span>

<span data-ttu-id="529ce-123">Сведения о профиле хранится в виде сериализованного xml и двоичные данные в таблице «Профили» в базе данных.</span><span class="sxs-lookup"><span data-stu-id="529ce-123">The profile information is stored as serialized xml and binary data in the 'Profiles' table in the database.</span></span>

<span data-ttu-id="529ce-124">После миграции приложения, чтобы использовать новую систему ASP.NET Identity, сведения о профиле десериализуется и хранятся в виде свойства класса пользователя.</span><span class="sxs-lookup"><span data-stu-id="529ce-124">After migrating the application to use the new ASP.NET Identity system, the profile information is deserialized and stored as properties on the user class.</span></span> <span data-ttu-id="529ce-125">Затем можно сопоставить каждое свойство на столбцы в таблице пользователя.</span><span class="sxs-lookup"><span data-stu-id="529ce-125">Each property can then be mapped onto columns in the user table.</span></span> <span data-ttu-id="529ce-126">Преимущество в том, что свойств можно было работать непосредственно с помощью класса пользователя в дополнение к отсутствию для сериализации или десериализации данных каждый раз при доступе к его.</span><span class="sxs-lookup"><span data-stu-id="529ce-126">The advantage here is that the properties can be worked on directly using the user class in addition to not having to serialize/deserialize data information each time when accessing it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="529ce-127">Начало работы</span><span class="sxs-lookup"><span data-stu-id="529ce-127">Getting Started</span></span>

1. <span data-ttu-id="529ce-128">Создайте новое приложение веб-форм ASP.NET 4.5 в Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="529ce-128">Create a new ASP.NET 4.5 Web Forms application in Visual Studio 2012.</span></span> <span data-ttu-id="529ce-129">Текущий образец использует шаблон веб-форм, но можно также использовать приложения MVC.</span><span class="sxs-lookup"><span data-stu-id="529ce-129">The current sample uses the Web Forms template, but you could use MVC Application as well.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. <span data-ttu-id="529ce-130">Создайте новую папку «Модели» для хранения сведений профиля</span><span class="sxs-lookup"><span data-stu-id="529ce-130">Create a new folder 'Models' to store profile information</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. <span data-ttu-id="529ce-131">Например сообщите нам храните даты рождения "," Город "," Высота "и" вес пользователя в профиле.</span><span class="sxs-lookup"><span data-stu-id="529ce-131">As an example, let us store the date of birth, city, height and weight of the user in profile.</span></span> <span data-ttu-id="529ce-132">Высоты и ширины, хранятся как пользовательский класс с именем «PersonalStats».</span><span class="sxs-lookup"><span data-stu-id="529ce-132">The height and weight are stored as a custom class called 'PersonalStats'.</span></span> <span data-ttu-id="529ce-133">Для хранения и извлечения профиля, нам нужен класс, который расширяет «ProfileBase».</span><span class="sxs-lookup"><span data-stu-id="529ce-133">To store and retrieve the profile, we need a class that extends 'ProfileBase'.</span></span> <span data-ttu-id="529ce-134">Давайте создадим новый класс «AppProfile» для получения и хранения сведений профиля.</span><span class="sxs-lookup"><span data-stu-id="529ce-134">Let's create a new class 'AppProfile' to get and store profile information.</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. <span data-ttu-id="529ce-135">Включить профиль в *web.config* файл.</span><span class="sxs-lookup"><span data-stu-id="529ce-135">Enable profile in the *web.config* file.</span></span> <span data-ttu-id="529ce-136">Введите имя класса, который будет использоваться для хранения или извлечения сведения о пользователе, созданный на шаге #3.</span><span class="sxs-lookup"><span data-stu-id="529ce-136">Enter the class name to be used to store/retrieve user information created in step #3.</span></span>

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. <span data-ttu-id="529ce-137">Добавьте страницу web forms, в папке «Учетная запись», чтобы получить данные профиля пользователя и сохранить их.</span><span class="sxs-lookup"><span data-stu-id="529ce-137">Add a web forms page in 'Account' folder to get the profile data from the user and store it.</span></span> <span data-ttu-id="529ce-138">Щелкните правой кнопкой проект и выберите «Добавить новый элемент».</span><span class="sxs-lookup"><span data-stu-id="529ce-138">Right click on project and select 'Add new Item'.</span></span> <span data-ttu-id="529ce-139">Добавьте новую страницу веб-форм с главной страницей «AddProfileData.aspx».</span><span class="sxs-lookup"><span data-stu-id="529ce-139">Add a new webforms page with master page 'AddProfileData.aspx'.</span></span> <span data-ttu-id="529ce-140">Скопируйте следующий код в разделе «MainContent»:</span><span class="sxs-lookup"><span data-stu-id="529ce-140">Copy the following in the 'MainContent' section:</span></span>

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   <span data-ttu-id="529ce-141">Добавьте следующий код в коде программной части:</span><span class="sxs-lookup"><span data-stu-id="529ce-141">Add the following code in the code behind:</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   <span data-ttu-id="529ce-142">Добавьте пространство имен, в какие AppProfile определен класс, чтобы удалить ошибки компиляции.</span><span class="sxs-lookup"><span data-stu-id="529ce-142">Add the namespace under which AppProfile class is defined to remove the compilation errors.</span></span>
6. <span data-ttu-id="529ce-143">Запустите приложение и создать нового пользователя с именем пользователя "**olduser".**</span><span class="sxs-lookup"><span data-stu-id="529ce-143">Run the app and create a new user with username '**olduser'.**</span></span> <span data-ttu-id="529ce-144">Перейдите на страницу «AddProfileData» и добавьте сведения о профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="529ce-144">Navigate to the 'AddProfileData' page and add profile information for the user.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

<span data-ttu-id="529ce-145">Вы можете проверить, что данные хранятся в качестве сериализованный xml в таблице «Профили» в окне обозревателя серверов.</span><span class="sxs-lookup"><span data-stu-id="529ce-145">You can verify that the data is stored as serialized xml in the 'Profiles' table using the Server Explorer window.</span></span> <span data-ttu-id="529ce-146">В Visual Studio в меню «Вид» выберите «Обозреватель серверов».</span><span class="sxs-lookup"><span data-stu-id="529ce-146">In Visual Studio, from 'View' menu, choose 'Server Explorer'.</span></span> <span data-ttu-id="529ce-147">Должно быть подключение данных для базы данных, определенных в *web.config* файл.</span><span class="sxs-lookup"><span data-stu-id="529ce-147">There should be a data connection for the database defined in the *web.config* file.</span></span> <span data-ttu-id="529ce-148">Если щелкнуть соединение с данными отобразится другой подкатегории.</span><span class="sxs-lookup"><span data-stu-id="529ce-148">Clicking on the data connection shows different sub categories.</span></span> <span data-ttu-id="529ce-149">Разверните узел «Таблицы» для отображения разных таблиц в базе данных, а затем щелкнуть правой кнопкой мыши «Профили» и выберите «Показать таблицу данных» для просмотра профиля данных, хранящихся в таблице профилей.</span><span class="sxs-lookup"><span data-stu-id="529ce-149">Expand 'Tables' to show the different tables in your database, then right click on 'Profiles' and choose 'Show Table Data' to view the profile data stored in the Profiles table.</span></span>

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a><span data-ttu-id="529ce-150">Перенос схемы базы данных</span><span class="sxs-lookup"><span data-stu-id="529ce-150">Migrating database schema</span></span>

<span data-ttu-id="529ce-151">Чтобы работать с системой идентификации существующей базы данных, необходимо обновить схему базы данных удостоверений для поддержки поля, которые мы добавили в исходной базе данных.</span><span class="sxs-lookup"><span data-stu-id="529ce-151">To make the existing database work with the Identity system, we need to update the schema in the Identity database to support the fields we added to the original database.</span></span> <span data-ttu-id="529ce-152">Это можно сделать с помощью скриптов SQL для создания новых таблиц и Копировать сведения о существующем.</span><span class="sxs-lookup"><span data-stu-id="529ce-152">This can be done using SQL scripts to create new tables and copy the existing information.</span></span> <span data-ttu-id="529ce-153">В окне «Обозреватель серверов» разверните узел «DefaultConnection» для отображения таблиц.</span><span class="sxs-lookup"><span data-stu-id="529ce-153">In the 'Server Explorer' window, expand the 'DefaultConnection' to display the tables.</span></span> <span data-ttu-id="529ce-154">Таблицы щелкните правой кнопкой мыши и выберите «Создать запрос»</span><span class="sxs-lookup"><span data-stu-id="529ce-154">Right click Tables and select 'New Query'</span></span>

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

<span data-ttu-id="529ce-155">Вставьте скрипт SQL из [ https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt ](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) и запустите его.</span><span class="sxs-lookup"><span data-stu-id="529ce-155">Paste the SQL script from [https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) and run it.</span></span> <span data-ttu-id="529ce-156">Если обновляется «DefaultConnection», мы видим, что добавляются новые таблицы.</span><span class="sxs-lookup"><span data-stu-id="529ce-156">If the 'DefaultConnection' is refreshed, we can see that the new tables are added.</span></span> <span data-ttu-id="529ce-157">Вы можете проверить данные внутри таблицы, чтобы увидеть, что данные были перенесены.</span><span class="sxs-lookup"><span data-stu-id="529ce-157">You can check the data inside the tables to see that the information has been migrated.</span></span>

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a><span data-ttu-id="529ce-158">Миграция приложения для использования ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="529ce-158">Migrating the application to use ASP.NET Identity</span></span>

1. <span data-ttu-id="529ce-159">Установите пакеты Nuget, необходимые для ASP.NET Identity:</span><span class="sxs-lookup"><span data-stu-id="529ce-159">Install the Nuget packages needed for ASP.NET Identity:</span></span>

    - <span data-ttu-id="529ce-160">Microsoft.AspNet.Identity.EntityFramework</span><span class="sxs-lookup"><span data-stu-id="529ce-160">Microsoft.AspNet.Identity.EntityFramework</span></span>
    - <span data-ttu-id="529ce-161">Microsoft.AspNet.Identity.Owin</span><span class="sxs-lookup"><span data-stu-id="529ce-161">Microsoft.AspNet.Identity.Owin</span></span>
    - <span data-ttu-id="529ce-162">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="529ce-162">Microsoft.Owin.Host.SystemWeb</span></span>
    - <span data-ttu-id="529ce-163">Microsoft.Owin.Security.Facebook</span><span class="sxs-lookup"><span data-stu-id="529ce-163">Microsoft.Owin.Security.Facebook</span></span>
    - <span data-ttu-id="529ce-164">Microsoft.Owin.Security.Google</span><span class="sxs-lookup"><span data-stu-id="529ce-164">Microsoft.Owin.Security.Google</span></span>
    - <span data-ttu-id="529ce-165">Microsoft.Owin.Security.MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="529ce-165">Microsoft.Owin.Security.MicrosoftAccount</span></span>
    - <span data-ttu-id="529ce-166">Microsoft.Owin.Security.Twitter</span><span class="sxs-lookup"><span data-stu-id="529ce-166">Microsoft.Owin.Security.Twitter</span></span>

   <span data-ttu-id="529ce-167">Дополнительные сведения об управлении пакетами Nuget можно найти [здесь](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)</span><span class="sxs-lookup"><span data-stu-id="529ce-167">More information on managing Nuget packages can be found [here](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)</span></span>
2. <span data-ttu-id="529ce-168">Для работы с существующими данными в таблице, необходимо создать классы моделей, которые сопоставляются с таблицами и подключить их в системы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="529ce-168">To work with existing data in the table, we need to create model classes which map back to the tables and hook them up in the Identity system.</span></span> <span data-ttu-id="529ce-169">Как часть контракта удостоверений классы модели должен реализовывать интерфейсы, определенные в библиотеке dll Identity.Core или можно расширить существующую реализацию этих интерфейсов, доступных в Microsoft.AspNet.Identity.EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="529ce-169">As part of the Identity contract, the model classes should either implement the interfaces defined in the Identity.Core dll or can extend the existing implementation of these interfaces available in Microsoft.AspNet.Identity.EntityFramework.</span></span> <span data-ttu-id="529ce-170">Мы будем использовать существующие классы для роли, имена входа и утверждения пользователей.</span><span class="sxs-lookup"><span data-stu-id="529ce-170">We will be using the existing classes for role, user logins and user claims.</span></span> <span data-ttu-id="529ce-171">Нам нужно использовать настраиваемого пользователя для нашего примера.</span><span class="sxs-lookup"><span data-stu-id="529ce-171">We need to use a custom user for our sample.</span></span> <span data-ttu-id="529ce-172">Щелкните правой кнопкой проект и создать новую папку «IdentityModels».</span><span class="sxs-lookup"><span data-stu-id="529ce-172">Right click on the project and create new folder 'IdentityModels'.</span></span> <span data-ttu-id="529ce-173">Добавьте новый класс «User», как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="529ce-173">Add a new 'User' class as shown below:</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   <span data-ttu-id="529ce-174">Обратите внимание на то, что «ProfileInfo» теперь является свойством класса пользователя.</span><span class="sxs-lookup"><span data-stu-id="529ce-174">Notice that the 'ProfileInfo' is now a property on the user class.</span></span> <span data-ttu-id="529ce-175">Поэтому мы используем класс пользователя напрямую работать с данными профиля.</span><span class="sxs-lookup"><span data-stu-id="529ce-175">Hence we can use the user class to directly work with profile data.</span></span>

<span data-ttu-id="529ce-176">Скопируйте файлы в **IdentityModels** и **IdentityAccount** папок из источника загрузки ( [ https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations ](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ).</span><span class="sxs-lookup"><span data-stu-id="529ce-176">Copy the files in the **IdentityModels** and **IdentityAccount** folders from the download source ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ).</span></span> <span data-ttu-id="529ce-177">Они имеют, в остальных классах модели и новые страницы, необходимые для пользователей и управление ролями с помощью API-интерфейсов ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="529ce-177">These have the remaining model classes and the new pages needed for user and role management using the ASP.NET Identity APIs.</span></span> <span data-ttu-id="529ce-178">Этот подход используется аналогичен членства SQL и подробное описание можно найти [здесь](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md).</span><span class="sxs-lookup"><span data-stu-id="529ce-178">The approach used is similar to the SQL Membership and the detailed explanation can be found [here](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md).</span></span>

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a><span data-ttu-id="529ce-179">Копирование данных профиля в новые таблицы</span><span class="sxs-lookup"><span data-stu-id="529ce-179">Copying Profile data to the new tables</span></span>

<span data-ttu-id="529ce-180">Как упоминалось ранее, необходимо десериализовать XML-данные в таблицах профили и сохранять их в столбцы в таблице AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="529ce-180">As mentioned earlier, we need to deserialize the xml data in the Profiles tables and store it in the columns of the AspNetUsers table.</span></span> <span data-ttu-id="529ce-181">Новые столбцы были созданы в таблице users на предыдущем шаге, остается лишь для заполнения этих столбцов с данными, необходимыми.</span><span class="sxs-lookup"><span data-stu-id="529ce-181">The new columns were created in the users table in the previous step so all that is left is to populate those columns with the necessary data.</span></span> <span data-ttu-id="529ce-182">Чтобы сделать это, мы будем использовать консольное приложение, которое запускается один раз для заполнения только что созданные столбцы в таблице users.</span><span class="sxs-lookup"><span data-stu-id="529ce-182">To do this, we will use a console application which is run once to populate the newly created columns in the users table.</span></span>

1. <span data-ttu-id="529ce-183">Создайте новое консольное приложение в существующие решения.</span><span class="sxs-lookup"><span data-stu-id="529ce-183">Create a new console application in the exiting solution.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. <span data-ttu-id="529ce-184">Установите последнюю версию пакета Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="529ce-184">Install the latest version of the Entity Framework package.</span></span>
3. <span data-ttu-id="529ce-185">Добавьте веб-приложения, созданный ранее, как ссылка на консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="529ce-185">Add the web application created above as a reference to the console application.</span></span> <span data-ttu-id="529ce-186">Для выполнения щелкните правой кнопкой мыши проект, а затем «Добавление ссылок», выберите решение, затем щелкните кнопкой мыши проект и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="529ce-186">To do this right click on Project, then 'Add References', then Solution, then click on the project and click OK.</span></span>
4. <span data-ttu-id="529ce-187">Скопируйте код ниже в класс Program.cs.</span><span class="sxs-lookup"><span data-stu-id="529ce-187">Copy the below code in the Program.cs class.</span></span> <span data-ttu-id="529ce-188">Эта логика считывает данные профиля для каждого пользователя, сериализует его как объект «ProfileInfo» и сохраняет его в базе данных.</span><span class="sxs-lookup"><span data-stu-id="529ce-188">This logic reads profile data for each user, serializes it as 'ProfileInfo' object and stores it back to the database.</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   <span data-ttu-id="529ce-189">Некоторые используемые модели определяются в папке «IdentityModels» проекта веб-приложения, поэтому необходимо включить соответствующие пространства имен.</span><span class="sxs-lookup"><span data-stu-id="529ce-189">Some of the models used are defined in the 'IdentityModels' folder of the web application project, so you must include the corresponding namespaces.</span></span>
5. <span data-ttu-id="529ce-190">Приведенный выше код работает с файлом базы данных в приложении\_папке данных проекта веб-приложения, созданные на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="529ce-190">The above code works on the database file in the App\_Data folder of the web application project created in the previous steps.</span></span> <span data-ttu-id="529ce-191">Для ссылки, обновите строку подключения в файле app.config консольного приложения, в строке подключения в файле web.config веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="529ce-191">To reference that, update the connection string in the app.config file of the console application with the connection string in the web.config of the web application.</span></span> <span data-ttu-id="529ce-192">Также предоставляют полный физический путь в свойстве «AttachDbFilename».</span><span class="sxs-lookup"><span data-stu-id="529ce-192">Also provide the complete physical path in the 'AttachDbFilename' property.</span></span>
6. <span data-ttu-id="529ce-193">Откройте командную строку и перейдите к папке bin выше консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="529ce-193">Open a command prompt and navigate to the bin folder of the above console application.</span></span> <span data-ttu-id="529ce-194">Запустите исполняемый файл и просмотрите выходные данные журнала, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="529ce-194">Run the executable and review the log output as shown in the following image.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. <span data-ttu-id="529ce-195">Откройте таблицу «AspNetUsers» в обозревателе серверов и проверки правильности данных в новые столбцы, которые содержат свойства.</span><span class="sxs-lookup"><span data-stu-id="529ce-195">Open the 'AspNetUsers' table in the Server Explorer and verify the data in the new columns that hold the properties.</span></span> <span data-ttu-id="529ce-196">Их следует обновить с помощью соответствующих значений свойств.</span><span class="sxs-lookup"><span data-stu-id="529ce-196">They should be updated with the corresponding property values.</span></span>

## <a name="verify-functionality"></a><span data-ttu-id="529ce-197">Проверка работоспособности</span><span class="sxs-lookup"><span data-stu-id="529ce-197">Verify functionality</span></span>

<span data-ttu-id="529ce-198">Используйте страницы вновь добавленный членства, которые реализуются с помощью ASP.NET Identity для входа в систему пользователя из старой базы данных.</span><span class="sxs-lookup"><span data-stu-id="529ce-198">Use the newly added membership pages that are implemented using ASP.NET Identity to login a user from the old database.</span></span> <span data-ttu-id="529ce-199">Он должен иметь возможности использовать те же учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="529ce-199">The user should be able to log in using the same credentials.</span></span> <span data-ttu-id="529ce-200">Попробуйте другие функциональные возможности, как добавление OAuth, создание нового пользователя, изменения пароля, Добавление ролей, добавьте пользователей в роли и т. д.</span><span class="sxs-lookup"><span data-stu-id="529ce-200">Try the other functionalities like adding OAuth, creating a new user, changing a password, adding roles, add users to roles, etc.</span></span>

<span data-ttu-id="529ce-201">Данные профиля пользователя старых и новых пользователей должны быть получены и хранятся в таблице users.</span><span class="sxs-lookup"><span data-stu-id="529ce-201">The Profile data for the old user and the new users should be retrieved and stored in the users table.</span></span> <span data-ttu-id="529ce-202">Старой таблицы больше не должна быть ссылка.</span><span class="sxs-lookup"><span data-stu-id="529ce-202">The old table should no longer be referenced.</span></span>

## <a name="conclusion"></a><span data-ttu-id="529ce-203">Заключение</span><span class="sxs-lookup"><span data-stu-id="529ce-203">Conclusion</span></span>

<span data-ttu-id="529ce-204">Статьи описывается процесс переноса веб-приложений, которые используются модели поставщика для членства в ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="529ce-204">The article described the process of migrating web applications that used the provider model for membership to ASP.NET Identity.</span></span> <span data-ttu-id="529ce-205">Кроме того, статьи описанные перенос данных профиля для пользователей связать системы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="529ce-205">The article additionally outlined migrating profile data for users to be hooked into the Identity system.</span></span> <span data-ttu-id="529ce-206">Оставьте комментарии ниже для вопросов и проблем, возникающих при миграции приложения.</span><span class="sxs-lookup"><span data-stu-id="529ce-206">Please leave comments below for questions and issues encountered when you migrate your app.</span></span>

<span data-ttu-id="529ce-207">*Благодаря Рик Андерсон и (Robert McMurray) за рецензирование статьи.*</span><span class="sxs-lookup"><span data-stu-id="529ce-207">*Thanks to Rick Anderson and Robert McMurray for reviewing the article.*</span></span>