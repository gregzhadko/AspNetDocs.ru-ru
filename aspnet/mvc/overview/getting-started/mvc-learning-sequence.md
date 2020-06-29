---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: Рекомендуемые учебники и статьи по MVC | Документация Майкрософт
author: Rick-Anderson
description: На этой странице содержатся ссылки на учебники по ASP.NET MVC и предлагаемую последовательность действий.
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 7dc81cf09309194df4471fedfc74d4051f0fdb78
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484221"
---
# <a name="mvc-recommended-tutorials-and-articles"></a>Рекомендуемые учебники и статьи по MVC

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

<a id="pwd"></a>
## <a name="getting-started"></a>Приступая к работе

- [Начало работы с ASP.NET MVC 5](introduction/getting-started.md) Мы рекомендуем начать с этой серии статей из 11.
- [Основы Pluralsight ASP.NET MVC 5](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals) (Видеокурс)
- [Введение в ASP.NET MVC](https://channel9.msdn.com/Series/Introduction-to-ASP-NET-MVC) с Jon Гэллоуэй и Кристофер Харрисон
- [Жизненный цикл приложения ASP.NET MVC 5](lifecycle-of-an-aspnet-mvc-5-application.md) Документ в формате PDF, который составляет диаграмму жизненного цикла приложения ASP.NET MVC 5.

<a id="con"></a>
## <a name="working-with-data"></a>Работа с данными

- [Начало работы с EF 6 Code First с использованием MVC 5](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Dykstra)ный ряд, подробноный в EF.

<a id="wj"></a>
## <a name="security"></a>Безопасность

- [Создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) Этот популярный учебник поможет вам создать простое приложение и добавить членство и роли.
- [Создание приложения ASP.NET MVC 5 с помощью единого входа Facebook, Twitter, LinkedIn и Google OAuth2](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5, которое позволяет пользователям входить в систему с помощью OAuth 2,0 с учетными данными от внешнего поставщика проверки подлинности, например Facebook, Twitter, LinkedIn, Microsoft или Google.
- [Создание безопасного веб-приложения ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) Первая серия удостоверений содержит код для [повторной отправки ссылки для подтверждения](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend).
- [Приложение ASP.NET MVC 5 с использованием SMS и двухфакторной проверки подлинности по электронной почте](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) Секунду в ряде удостоверений.
- [Рекомендации по развертыванию паролей и других конфиденциальных данных в ASP.NET и службу приложений Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- [Двухфакторная проверка подлинности с помощью SMS и электронной почты с ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) `isPersistent` и файл cookie безопасности, код, требующий от пользователя иметь проверенную учетную запись электронной почты, прежде чем они смогут войти в систему, как SignInManager проверяет требования 2FA и многое другое.
- [Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Сведения об удостоверениях, не найденных в [создании безопасного веб-приложения ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля,](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) например о том, как разрешить пользователям сбрасывать забытый пароль.

<a id="da"></a>
## <a name="azure"></a>Azure

- [Создание веб-приложения ASP.NET в Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/) Краткое и простое руководство по развертыванию в Azure.
- [Создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>Производительность и отладка

- [Профилирование и отладка приложения ASP.NET MVC с помощью Glimpse](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)

## <a name="aspnet-mvc-dropdownlistfor-with-selectlistitem"></a>ASP.NET MVC Дропдовнлистфор with Селектлиститем

При использовании <xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A> вспомогательного метода и передаче ему коллекции `SelectListItem` , из которой он заполняется, объект `DropdownListFor` изменяет переданную коллекцию после ее вызова. `DropdownListFor`изменяет `SelectListItems` Выбранные свойства на все, что было выбрано в раскрывающемся списке. Это приводит к непредвиденному поведению.

<xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A>,, <xref:System.Web.Mvc.Html.SelectExtensions.DropDownList%2A> , <xref:System.Web.Mvc.Html.SelectExtensions.EnumDropDownListFor%2A> <xref:System.Web.Mvc.Html.SelectExtensions.ListBox%2A> И <xref:System.Web.Mvc.Html.SelectExtensions.ListBoxFor%2A> обновляют выбранное свойство любого объекта, `IEnumerable<SelectListItem>` переданного или найденного в ViewData.

Чтобы решить эту проблему, создайте отдельные перечислимые объекты, содержащие отдельные `SelectListItem` экземпляры, для каждого свойства в модели.

Дополнительные сведения см. в разделе

* [Дропдовнлистфор изменяет переданный ей набор Селектлиститем.](http://web.archive.org/web/20140902031437/http://aspnetwebstack.codeplex.com/workitem/1913)
* [Жетселектлиствисдефаултвалуе изменяет IEnumerable <SelectListItem> selectList](https://github.com/aspnet/AspNetWebStack/issues/271)