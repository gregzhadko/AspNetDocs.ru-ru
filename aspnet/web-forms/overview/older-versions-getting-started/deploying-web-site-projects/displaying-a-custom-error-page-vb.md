---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
title: Отображение настраиваемой страницы ошибок (VB) | Документация Майкрософт
author: rick-anderson
description: Что видят пользователи при возникновении ошибки времени выполнения в веб-приложении ASP.NET? Ответ зависит от того, как &lt;веб-сайта&gt; конфигурацию customErrors...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 14873c5d-81a9-455b-bd71-30fb555583e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 33367d5e3c4b5c8fa039ee20704054ba508e717a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522774"
---
# <a name="displaying-a-custom-error-page-vb"></a>Отображение страницы пользовательской ошибки (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_VB.zip) или [скачать PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_vb.pdf)

> Что видят пользователи при возникновении ошибки времени выполнения в веб-приложении ASP.NET? Ответ зависит от того, как конфигурация&gt; &lt;customErrors веб-сайта. По умолчанию пользователи показывают невидимый желтый экран о том, что произошла ошибка времени выполнения. В этом учебнике показано, как настроить эти параметры для отображения страницы настраиваемой ошибки визуально, которая соответствует внешнему интерфейсу веб-узла.

## <a name="introduction"></a>Введение

В идеальном мире ошибки времени выполнения не возникают. Программисты могут написать код, Нари ошибку и устойчивую проверку вводимых пользователем данных, а внешние ресурсы, такие как серверы баз данных и серверы электронной почты, никогда не переходят в автономный режим. Разумеется, на практике ошибки неизбежны. Классы в .NET Framework сообщают об ошибке, вызывая исключение. Например, вызов метода Open объекта SqlConnection устанавливает соединение с базой данных, указанной в строке подключения. Однако если база данных не работает или в строке подключения указаны недопустимые учетные данные, метод Open вызывает исключение `SqlException`. Исключения могут обрабатываться с помощью блоков `Try/Catch/Finally`. Если код в блоке `Try` вызывает исключение, управление передается соответствующему блоку catch, где разработчик может попытаться устранить ошибку. Если соответствующий блок catch отсутствует или код, вызвавший исключение, находится не в блоке try, то исключение перколатес стек вызовов в поиске блоков `Try/Catch/Finally`.

Если исключение восстановится до среды выполнения ASP.NET без обработки, вызывается [событие`Error`](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) [класса`HttpApplication`](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)и отображается страница настроенной *ошибки* . По умолчанию ASP.NET отображает страницу ошибки, ласковоую [желтым экраном смерти](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) (исод). Существует две версии ИСОД: одна показывает сведения об исключении, трассировку стека и другие сведения, полезные для разработчиков при отладке приложения (см. **рис. 1**); в другом просто говорится об ошибке времени выполнения (см. рис. **2**).

Сведения об исключении ИСОД весьма полезны для разработчиков, которые выполняют отладку приложения, но показывают ИСОД для конечных пользователей. Вместо этого конечные пользователи должны быть переведены на страницу ошибки, которая обеспечивает внешний вид и удобство работы узла с более понятными для пользователя prose, описывающими ситуацию. Хорошая новость состоит в том, что создание такой настраиваемой страницы ошибки довольно просто. В этом учебнике начинается знакомство с ASP. Различные страницы ошибок NET. Затем показано, как настроить веб-приложение таким способом, чтобы пользователи отображали настраиваемую страницу ошибки на лицевой стороне ошибки.

### <a name="examining-the-three-types-of-error-pages"></a>Изучение трех типов страниц ошибок

При возникновении необработанного исключения в приложении ASP.NET появляется один из трех типов страниц ошибок:

- Желтый экран сведений об исключении на странице ошибки смерти
- Желтый экран ошибки времени выполнения на странице ошибки смерти или
- Настраиваемая страница ошибки

Наиболее знакомыми разработчиками страниц ошибок являются сведения об исключении ИСОД. По умолчанию эта страница отображается для пользователей, посещаемых локально, поэтому это страница, отображаемая при возникновении ошибки при тестировании сайта в среде разработки. Как следует из названия, сведения об исключении ИСОД предоставляют подробные сведения об исключении: тип, сообщение и трассировку стека. Более того, если исключение было вызвано кодом в классе кода программной части страницы ASP.NET и если приложение настроено для отладки, то сведения об исключении ИСОД также будут показывать эту строку кода (и несколько строк кода выше и ниже).

На **рис. 1** показана страница сведений об исключении исод. Запишите URL-адрес в окне адреса браузера: `http://localhost:62275/Genre.aspx?ID=foo`. Помните, что на `Genre.aspx` странице перечислены обзоры книг в определенном жанре. Для этого требуется, чтобы значение `GenreId` (`uniqueidentifier`) передавалось через строку запроса. Например, правильный URL-адрес для просмотра вымышленных проверок `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`. Если значение, отличное от`uniqueidentifier`, передается через строку запроса (например, "foo"), возникает исключение.

> [!NOTE]
> Чтобы воспроизвести эту ошибку в демонстрационном веб-приложении, доступном для загрузки, можно либо посетить `Genre.aspx?ID=foo` напрямую, либо щелкнуть ссылку "создать ошибку времени выполнения" в `Default.aspx`.

Обратите внимание на сведения об исключении, представленные на **рис. 1**. Сообщение об исключении "не удалось преобразовать строку символов в uniqueidentifier" в верхней части страницы. Тип исключения, `System.Data.SqlClient.SqlException`, также присутствует в списке. Также имеется трассировка стека.

[![](displaying-a-custom-error-page-vb/_static/image2.png)](displaying-a-custom-error-page-vb/_static/image1.png)

**Рис. 1**. сведения об исключении Исод содержат сведения о исключении  
 ([Щелкните, чтобы просмотреть изображение с полным размером](displaying-a-custom-error-page-vb/_static/image3.png))

Другой тип ИСОД — это ошибка времени выполнения ИСОД и показана на рис. **2**. Ошибка времени выполнения ИСОД информирует посетителя о том, что произошла ошибка времени выполнения, но не содержит сведений о возникшем исключении. (Однако он предоставляет инструкции о том, как сделать сведения об ошибке видимыми, изменив файл `Web.config`, который является частью того, что делает такую ИСОД непрофессиональной.)

По умолчанию ошибка времени выполнения ИСОД отображается для пользователей, посещенных удаленно (через http://www.yoursite.com), как указано URL-адресом в адресной строке браузера на **рис. 2**: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo`. Существуют два различных экрана ИСОД, так как разработчики заинтересованы в определении сведений об ошибках, но такие сведения не должны отображаться на активном сайте, так как они могут раскрыть потенциальные уязвимости или другие конфиденциальные сведения для всех, кто посещает ваш места.

> [!NOTE]
> Если вы выполняете следующие функции и используете DiscountASP.NET в качестве веб-узла, вы можете заметить, что ошибка времени выполнения ИСОД не отображается при посещении активного сайта. Это обусловлено тем, что DiscountASP.NET содержит серверы, настроенные на отображение сведений об исключении ИСОД по умолчанию. Хорошая новость заключается в том, что вы можете переопределить это поведение по умолчанию, добавив раздел `<customErrors>` в файл `Web.config`. Раздел "сведения о настройке отображаемой страницы ошибки" подробно рассматривает раздел `<customErrors>`.

[![](displaying-a-custom-error-page-vb/_static/image5.png)](displaying-a-custom-error-page-vb/_static/image4.png)

**Рис. 2**. ошибка времени выполнения Исод не содержит сведений об ошибке  
 ([Щелкните, чтобы просмотреть изображение с полным размером](displaying-a-custom-error-page-vb/_static/image6.png))

Третий тип страницы ошибки — настраиваемая страница ошибки, которая представляет собой создаваемую веб-страницу. Преимущество пользовательской страницы ошибок состоит в том, что вы имеете полный контроль над информацией, отображаемой пользователю вместе с ее внешним видом и поведением. страница настраиваемой ошибки может использовать ту же главную страницу и стили, что и другие страницы. Раздел "Использование настраиваемой страницы ошибки" содержит инструкции по созданию настраиваемой страницы ошибок и ее настройке для вывода в случае необработанного исключения. **На рис. 3** приведен краткий пик этой настраиваемой страницы ошибок. Как видите, страница ошибки выглядит гораздо более профессионально, чем один из желтых экранов смерти, показанных на рис. 1 и 2.

[![](displaying-a-custom-error-page-vb/_static/image8.png)](displaying-a-custom-error-page-vb/_static/image7.png)

**Рис. 3**. настраиваемая страница ошибки предлагает более специализированный внешний вид и оформление  
 ([Щелкните, чтобы просмотреть изображение с полным размером](displaying-a-custom-error-page-vb/_static/image9.png))

Уделите время изучению адресной строки браузера на рис. **3**. Обратите внимание, что в адресной строке отображается URL-адрес страницы настраиваемой ошибки (`/ErrorPages/Oops.aspx`). На рис. 1 и 2 желтые экраны смерти отображаются на той же странице, на которой возникла ошибка (`Genre.aspx`). На странице настраиваемой ошибки передается URL-адрес страницы, на которой произошла ошибка, с помощью параметра `aspxerrorpath` QueryString.

## <a name="configuring-which-error-page-is-displayed"></a>Настройка отображаемой страницы ошибок

Какая из трех возможных страниц ошибок отображается на основе двух переменных:

- Сведения о конфигурации в разделе `<customErrors>` и
- Будет ли пользователь посещать сайт локально или удаленно.

[Раздел`<customErrors>`](https://msdn.microsoft.com/library/h0hfz6fc.aspx) в `Web.config` имеет два атрибута, которые влияют на отображаемую страницу ошибки: `defaultRedirect` и `mode`. Атрибут `defaultRedirect` является необязательным. Если он указан, он указывает URL-адрес страницы настраиваемой ошибки и указывает, что вместо ошибки времени выполнения ИСОД должна отображаться пользовательская страница ошибки. Атрибут `mode` является обязательным и принимает одно из трех значений: `On`, `Off`или `RemoteOnly`. Эти значения имеют следующие особенности.

- `On` — указывает, что пользовательская страница ошибок или ошибка времени выполнения ИСОД отображаться для всех посетителей независимо от того, являются они локальными или удаленными.
- `Off` — указывает, что сведения об исключении отображаются для всех посетителей, независимо от того, являются они локальными или удаленными.
- `RemoteOnly` — указывает, что пользовательская страница ошибок или ошибка времени выполнения ИСОД отображается удаленным посетителям, а сведения об исключении ИСОД — локальным посетителям.

Если не указано иное, ASP.NET действует так, как если бы вы установили атрибут mode в `RemoteOnly` и не указали `defaultRedirect` значение. Иными словами, поведение по умолчанию заключается в том, что сведения об исключении ИСОД отображаются локальным посетителям, а ошибка времени выполнения ИСОД отображается для удаленных посетителей. Это поведение по умолчанию можно переопределить, добавив `<customErrors>` раздел в `Web.config file.` веб-приложения.

## <a name="using-a-custom-error-page"></a>Использование настраиваемой страницы ошибок

У каждого веб-приложения должна быть настраиваемая страница ошибки. Она предоставляет более профессионально выглядящий альтернативу ошибке времени выполнения ИСОД, легко создавать и настраивать приложение для использования настраиваемой страницы ошибок занимает всего несколько секунд. Первым шагом является создание настраиваемой страницы ошибок. Я добавил новую папку в приложение для рецензирования книги с именем `ErrorPages` и добавил к этой новой странице ASP.NET с именем `Oops.aspx`. Убедитесь, что страница использует ту же главную страницу, что и остальные страницы на сайте, чтобы он автоматически наследовал тот же внешний вид и поведение.

[![](displaying-a-custom-error-page-vb/_static/image11.png)](displaying-a-custom-error-page-vb/_static/image10.png)

**Рис. 4**. Создание настраиваемой страницы ошибок

Затем натратьте несколько минут на создание содержимого для страницы ошибки. Я создал простую настраиваемую страницу ошибки с сообщением, указывающим, что произошла непредвиденная ошибка, и обратная ссылка на домашнюю страницу сайта.

[![](displaying-a-custom-error-page-vb/_static/image13.png)](displaying-a-custom-error-page-vb/_static/image12.png)

**Рис. 5**. Проектирование пользовательской страницы ошибок  
 ([Щелкните, чтобы просмотреть изображение с полным размером](displaying-a-custom-error-page-vb/_static/image14.png))

После завершения страницы ошибки настройте веб-приложение на использование настраиваемой страницы ошибок вместо ошибки времени выполнения ИСОД. Это достигается путем указания URL-адреса страницы ошибки в атрибуте `defaultRedirect` раздела `<customErrors>`. Добавьте следующую разметку в файл `Web.config` приложения:

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample1.xml)]

Приведенная выше разметка настраивает приложение для отображения сведений об исключении ИСОД пользователям, посещенным локально, при использовании пользовательской страницы ошибки ой. aspx для пользователей, посещенных удаленно. Чтобы увидеть это в действии, разверните веб-сайт в рабочей среде, а затем посетите страницу жанр. aspx на активном сайте с недопустимым значением строки запроса. Вы увидите страницу настраиваемой ошибки (см. рис. **3**).

Чтобы убедиться, что пользовательская страница ошибки отображается только для удаленных пользователей, перейдите на страницу `Genre.aspx` с неверной строкой запроса из среды разработки. Вы по-прежнему увидите сведения об исключении ИСОД (см. **рис. 1**). Параметр `RemoteOnly` гарантирует, что пользователи, посещающие сайт в рабочей среде, видят страницу настраиваемой ошибки, а разработчики, работающие локально, продолжают видеть сведения об исключении.

## <a name="notifying-developers-and-logging-error-details"></a>Уведомление разработчиков и запись сведений об ошибках

Ошибки, возникающие в среде разработки, были вызваны разработчиком на компьютере. Она показывает сведения об исключении в сведениях об исключении ИСОД и знает, какие шаги она выполняла в момент возникновения ошибки. Но при возникновении ошибки в рабочей среде разработчик не имеет сведений о том, что произошла ошибка, если пользователь, посещающий сайт, не потратит время на сообщение об ошибке. Даже если пользователь выходит из строя, чтобы предупредить команду разработчиков о том, что произошла ошибка, не зная тип исключения, сообщение и трассировку стека, это может быть трудно диагностировать причину ошибки, разрешить отдельно исправить ее.

По этим причинам важно, чтобы любая ошибка в рабочей среде записалась в какое-либо постоянное хранилище (например, в базу данных) и что разработчики предупреждают об этой ошибке. Страница настраиваемой ошибки может показаться хорошим местом для ведения журнала и уведомления. К сожалению, настраиваемая страница ошибки не имеет доступа к сведениям об ошибке и поэтому не может использоваться для записи этих сведений в журнал. Хорошая новость состоит в том, что существует несколько способов перехвата сведений об ошибке и их записи в журнал, а в следующих трех руководствах подробно рассматривается этот раздел.

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>Использование различных настраиваемых страниц ошибок для различных состояний ошибок HTTP

Если исключение вызывается страницей ASP.NET и не обрабатывается, исключение перколатес до среды выполнения ASP.NET, которая отображает настроенную страницу ошибки. Если запрос поступает в подсистему ASP.NET Engine, но не может быть обработан по какой-либо причине, возможно, запрошенный файл не найден или для него отключены разрешения на чтение. Затем обработчик ASP.NET создает `HttpException`. Это исключение, например исключения, возникающие на страницах ASP.NET, передается в среду выполнения, что приводит к отображению соответствующей страницы ошибки.

Это означает, что для веб-приложения в рабочей среде, если пользователь запрашивает страницу, которая не найдена, он увидит страницу настраиваемой ошибки. **На рис. 6** показан пример. Поскольку запрос предназначен для несуществующей страницы (`NoSuchPage.aspx`), создается `HttpException` и отображается страница настраиваемой ошибки (Обратите внимание на ссылку на `NoSuchPage.aspx` в параметре строки запроса `aspxerrorpath`).

[![](displaying-a-custom-error-page-vb/_static/image16.png)](displaying-a-custom-error-page-vb/_static/image15.png) **рис. 6**. Среда выполнения ASP.NET отображает настроенную страницу ошибки в ответ на недопустимый запрос.  
 ([Щелкните, чтобы просмотреть изображение с полным размером](displaying-a-custom-error-page-vb/_static/image17.png)) 

По умолчанию все типы ошибок приводят к отображению одной и той же настраиваемой страницы ошибок. Однако можно указать другую настраиваемую страницу ошибки для конкретного кода состояния HTTP с помощью `<error>` дочерних элементов в разделе `<customErrors>`. Например, чтобы страница ошибки отображалась в случае ошибки «страница не найдена» с кодом состояния HTTP 404, обновите раздел `<customErrors>`, включив в него следующую разметку:

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample2.xml)]

После этого изменения, когда пользователь посещает удаленно запрашивает несуществующий ресурс ASP.NET, он будет перенаправлен на `404.aspx` настраиваемую страницу ошибок вместо `Oops.aspx`. Как показано на **рис. 7** , страница `404.aspx` может содержать более конкретное сообщение, чем общая пользовательская страница ошибки.

> [!NOTE]
> Дополнительные сведения о создании эффективных 404 страниц ошибок см. на [страницах ошибок 404](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/) .

[![](displaying-a-custom-error-page-vb/_static/image19.png)](displaying-a-custom-error-page-vb/_static/image18.png) **рис. 7**. на странице настраиваемой ошибки 404 отображается более целевое сообщение, чем `Oops.aspx`  
 ([Щелкните, чтобы просмотреть изображение с полным размером](displaying-a-custom-error-page-vb/_static/image20.png)) 

Так как известно, что страница `404.aspx` достижима только тогда, когда пользователь выполняет запрос к странице, которая не была найдена, можно улучшить эту настраиваемую страницу ошибки, включив в нее функции, помогающие пользователю устранить эту ошибку конкретного типа. Например, можно создать таблицу базы данных, которая сопоставляет известные неправильные URL-адреса с хорошими URL-адресами, а затем попросит `404.aspx` настраиваемой страницы ошибок выполнить запрос к этой таблице и предложить страницы, к которым пользователь может обратиться.

> [!NOTE]
> Страница настраиваемой ошибки отображается только при выполнении запроса к ресурсу, обрабатываемому ядром ASP.NET. Как обсуждалось в [основных различиях между IIS и ASP.NET Development Serverным](core-differences-between-iis-and-the-asp-net-development-server-vb.md) руководством, веб-сервер может выполнять определенные запросы. По умолчанию веб-сервер IIS обрабатывает запросы на статическое содержимое, например изображения и HTML-файлы, без вызова подсистемы ASP.NET. Следовательно, если пользователь запрашивает несуществующий файл изображения, он получит сообщение об ошибке по умолчанию 404 IIS, а не ASP. NET — настроенная страница ошибки.

## <a name="summary"></a>Сводка

Когда в приложении ASP.NET возникает необработанное исключение, пользователь показывает одну из трех страниц ошибок: желтой экран сведений об исключении. Желтый экран ошибки времени выполнения. или настраиваемую страницу ошибки. Отображаемая страница ошибки зависит от конфигурации `<customErrors>` приложения и от того, посещает пользователь локально или удаленно. Поведение по умолчанию — показывать сведения об исключении ИСОД локальным посетителям, а ошибка времени выполнения ИСОД удаленным посетителям.

Несмотря на то, что ошибка времени выполнения ИСОД скрывает потенциально конфиденциальную информацию об ошибках от пользователя, который посещает сайт, она нарушает внешний вид веб-узла и делает приложение ошибками. Лучшим подходом является использование настраиваемой страницы ошибок, которая включает создание и проектирование пользовательской страницы ошибок и указание ее URL-адреса в атрибуте `defaultRedirect` раздела `<customErrors>`. Можно даже иметь несколько настраиваемых страниц ошибок для различных состояний ошибок HTTP.

Страница настраиваемой ошибки является первым шагом в комплексной стратегии обработки ошибок для веб-сайта в рабочей среде. Также важны важные шаги для разработчика ошибки и ведения журнала. В следующих трех руководствах рассматриваются методы уведомления об ошибках и ведения журнала.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Страницы ошибок, еще один раз](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [Правила разработки исключений](https://msdn.microsoft.com/library/ms229014.aspx)
- [Понятные пользователю страницы ошибок](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Обработка и создание исключений](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [Правильное использование настраиваемых страниц ошибок в ASP.NET](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [Назад](strategies-for-database-development-and-deployment-vb.md)
> [Вперед](processing-unhandled-exceptions-vb.md)
