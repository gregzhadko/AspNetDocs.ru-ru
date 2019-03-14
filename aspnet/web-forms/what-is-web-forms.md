---
uid: web-forms/what-is-web-forms
title: Что такое веб-форм | Документация Майкрософт
author: rick-anderson
description: ''
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 5fa1daf9-1161-4cfa-bd4c-658f48b2c229
msc.legacyurl: /web-forms/what-is-web-forms
msc.type: content
ms.openlocfilehash: e135cfa2945b9e7e5269eb436ff0c1dff20aacdf
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039071"
---
<a name="what-is-web-forms"></a>Что такое веб-форм
====================
Веб-форм ASP.NET является частью платформа веб-приложений ASP.NET и входит в состав [Visual Studio](https://www.asp.net/downloads). Он является одним из четырех моделей программирования, которые можно использовать для создания веб-приложений ASP.NET, другие — ASP.NET MVC, веб-страниц ASP.NET и приложений ASP.NET.

Веб-формы, страницы, которые пользователям запрашивать с помощью обозревателя. Эти страницы могут быть написаны с использованием сочетания HTML, клиентских сценариев серверными элементами управления и серверного кода. При запросе пользователем страницы, он компилируется и выполняется на сервере платформой, и платформа создает HTML-разметка, которая может отобразить браузер. На странице веб-форм ASP.NET представлены сведения для пользователей в любой браузер или клиентское устройство.

С помощью Visual Studio, можно создать веб-форм ASP.NET. Интегрированная среда разработки (IDE) Visual Studio позволяет перетаскивать элементы управления сервера для макета страницы веб-форм. Можно затем легко задать свойства, методы и события для элементов управления на странице, или для самой страницы. Эти свойства, методы и события используются для определения поведения веб-страницы, внешнего вида и поведения и т. д. Чтобы написать код сервера для обработки логики для страницы, можно использовать .NET-языке вроде C# или Visual Basic.

> [!NOTE] 
> 
> Документация по ASP.NET и Visual Studio распространяется на несколько версий. Разделы, в которых рассматриваются функции предыдущих версий, может быть полезно для текущих задач и сценарии с использованием последних версий.


**Ниже приведены веб-форм ASP.NET.** 

- Основаны на технологии Microsoft ASP.NET, в котором код, выполняемый на сервере, динамически создает выходные данные веб-страницы для браузера или клиентского устройства.
- Совместимо с любого браузера или мобильного устройства. Веб-страницу ASP.NET автоматически отображает правильные обозревателю код HTML для функции, такие как стили, расположение и т. д.
- Совместим с любой язык, поддерживаемый .NET среда CLR, такие как Microsoft Visual Basic и Microsoft Visual C#.
- На платформе Microsoft .NET Framework. Это позволяет использовать все преимущества платформы, включая управляемую среду, строгая типизация и наследование.
- Гибкая, так как вы можете добавить созданные пользователем и сторонним производителем, элементы управления к ним.

**Предложение веб-форм ASP.NET:** 

- Разделение HTML и другим кодом пользовательского интерфейса от логики приложения.
- Большой набор серверных элементов управления для общих задач, включая доступ к данным.
- Мощные привязки данных, с поддержкой прекрасно.
- Поддержка сценариев на стороне клиента, выполняемый в браузере.
- Поддержка различных других возможностей, включая маршрутизацию, безопасности, производительности, интернационализации, тестирование, отладку, обработку ошибок и управление состоянием.

## <a name="aspnet-web-forms-helps-you-overcome-challenges"></a>Веб-форм ASP.NET помогает преодолеть трудности

Программирования веб-приложений связаны задачи, которые обычно не встают при программировании традиционных клиентских приложений. Перечислены некоторые из них:

- **Реализация сложного веб-интерфейса пользователя** — могут возникнуть трудности и сложен в проектировании и реализации пользователя с помощью базовых возможностей HTML, особенно в том случае, если страница имеет сложную структуру, большой объем динамического содержимого и полнофункциональный объекты, взаимодействующих с пользователем.
- **Разделение клиента и сервера** -в веб-приложение, клиент (браузер) и сервер находятся в разных программ, часто работающих на разных компьютерах (и даже в различных операционных системах). Следовательно эти две части приложения совместно использовать очень небольшой объем информации. они могут взаимодействовать, но обычно обмениваются только небольшими фрагментами основных сведений.
- **Без отслеживания состояния выполнения** — Если веб-сервер получает запрос на страницу, он находит эту страницу, обрабатывает его, отправляет его в браузер и затем удаляет все сведения о. Если пользователь запрашивает ту же страницу еще раз, сервер повторяется последовательность целиком, обрабатывая страницу с нуля. Другими словами, сервер не пользуется памятью страниц, обработанных — страницы не имеют состояния. Таким образом Если приложению требуется хранить информацию о странице, состояний может стать проблемой.
- **Неизвестные возможности клиента** -во многих случаях веб-приложения доступны для многих пользователей, использующих самые разнообразные браузеры. Обозреватели имеют различные возможности, что затрудняет создание приложения, которое будет выполняться одинаково хорошо на каждом из них.
- **Сложности с доступом к данным** -считывание и запись в источник данных в традиционных веб-приложениях может быть сложной и ресурсоемкой.
- **Сложности с масштабируемостью** — во многих случаях веб-приложения, разработанные с помощью существующих методов, не являются масштабируемыми из-за недостатка совместимости между различными компонентами приложения. Это часто является недостатком приложений при значительных колебаниях обрабатываемого.

Для решения этих проблем для веб-приложений может потребоваться значительное время и усилия. Веб-форм ASP.NET и платформы ASP.NET решают эти задачи одним из следующих способов:

- **Интуитивно понятный и согласованный объектная модель** -страниц ASP.NET предоставляет объектную модель, дающий возможность работать с формами как единое целое, а не как отдельные клиентские и серверные части. В этой модели можно программировать страницы более интуитивно понятным способом, чем в традиционных веб-приложений, включая возможность задать свойства для элементов страницы и реагировать на события. Кроме того серверные элементы управления ASP.NET являются абстракцией физического содержимого HTML-страницы и прямого взаимодействия между браузером и сервером. Как правило можно использовать серверные элементы управления, как это может работать с элементами управления в клиентском приложении не придется думать о том, как создавать HTML для представления и обрабатывать элементы управления и их содержимое.
- **Модель программирования на основе событий** -веб-форм ASP.NET предоставляют веб-приложениям привычную модель написания обработчиков событий для событий, происходящих на стороне клиента или сервера. Платформа ASP.NET абстрагирует эту модель таким образом, что базовый механизм захвата события на клиенте, передачи его на сервер и вызов соответствующего метода является полностью автоматическим и невидимым для вас. Результатом является код простая структура, поддерживающая разработку на основе событий.
- **Управление состоянием интуитивно понятный** - страниц ASP.NET автоматически решает задачу поддержания состояния страницы и ее элементов управления и предоставляет явные способы сохранения состояния сведений о приложении. Это достигается без использования значительных ресурсов сервера и может быть реализована с или без отправки файлов cookie в браузере.
- **Приложения, независимые от браузера** -страниц ASP.NET позволяет вам создавать вся логика приложения на сервере, что устраняет необходимость явно создавать код для различных обозревателей. Тем не менее он по-прежнему позволяет воспользоваться преимуществами функций конкретного браузера путем написания кода на стороне клиента для обеспечения лучшей производительности и более широкие возможности клиента.
- **Поддержка .NET framework common language runtime** -страниц ASP.NET основана на .NET Framework, поэтому все возможности платформы доступны для любого приложения ASP.NET. Приложения могут быть написаны на любом языке, совместимом со средой выполнения. Кроме того упрощается доступ к данным с помощью инфраструктуры доступа к данным, предоставляемые платформой .NET Framework, включая ADO.NET.
- **Производительность масштабируемого сервера .NET framework** -страниц ASP.NET позволяет масштабировать веб-приложение с одного компьютера с одним процессором для веб-фермы несколькими компьютерами, четко и без сложных изменений в приложение логика.

## <a name="features-of-aspnet-web-forms"></a>Функции веб-форм ASP.NET

- **Серверные элементы управления**-серверные элементы управления ASP.NET — это объекты, на веб-страниц ASP.NET, которые выполняются при запросе страницы и визуализации разметки в браузере. Многие веб-сервера управления аналогичны знакомые HTML-элементы, такие как кнопки и текстовые поля. Другие элементы управления реализуют более сложное поведение, например календарь и элементы управления, которые можно использовать для подключения к источникам данных и отображения данных.
- **Главные страницы**-главные страницы ASP.NET позволяют создавать устойчивый макет страниц в приложении. Одна главная страница определяет внешний вид и стандартное поведение, которое требуется для всех страниц (или группы страниц) в приложении. Затем можно создать отдельных страниц контента с содержимым, которое будет отображаться. Когда пользователи запрашивают страницы содержимого, они выполняют слияние с главной страницей для получения выходных данных, который соединяет макет главной страницы с содержимым на странице содержимого.
- **Работа с данными**-ASP.NET предоставляет множество вариантов для хранения, извлечения и отображения данных. В приложении веб-форм ASP.NET используйте элементы управления с привязкой к данным для автоматизации презентации или ввода данных в элементах пользовательского интерфейса веб-страницы, таких как таблицы и текстовые поля и раскрывающиеся списки.
- **Членство**-ASP.NET Identity хранит учетные данные пользователей в базе данных, созданных приложением. При входе пользователей, приложение проверяет свои учетные данные путем чтения базы данных. Проекта *учетной записи* папка содержит файлы, которые реализуют различные части членства: регистрация, вход, изменения пароля и авторизации доступа. Кроме того веб-форм ASP.NET поддерживает OAuth и OpenID. Эти улучшения проверки подлинности позволяют пользователям входить на сайт, с помощью существующих учетных данных, из таких как Facebook, Twitter, Windows Live и Google. По умолчанию этот шаблон создает базы данных членства, используя имя базы данных по умолчанию для экземпляра SQL Server Express LocalDB, сервер базы данных разработки, входящий в состав Visual Studio Express 2013 для Web.
- **Клиентский скрипт и клиентские платформы**-серверных функций ASP.NET можно улучшить, включая функциональность сценария клиента на страницах веб-форм ASP.NET. Клиентский скрипт можно использовать для предоставления пользователям многофункциональных, более быстрых пользовательский интерфейс. Клиентский скрипт может использоваться для выполнения асинхронных вызовов веб-серверу, пока страница выполняется в браузере.
- **Маршрутизация**-маршрутизация URL-адресов можно настроить приложение для принятия URL-адреса, которые не сопоставлены с физическими файлами запросов. URL-адрес запроса — это просто URL-адрес, пользователь вводит в браузер, чтобы найти страницу на веб-сайт. Маршрутизация используется для определения URL-адреса, которые семантически значимые для пользователей и, которые могут помочь в оптимизации поисковой системы (SEO).
- **Управление состоянием**-веб-форм ASP.NET содержит несколько параметров, которые помогут вам сохранить данные на уровне страниц и уровне приложения.
- **Безопасность**— важная часть Разработка более безопасных приложений — понять возможных угроз. Корпорация Майкрософт разработала способ категоризации угроз: Спуфинг, незаконное изменение, отказ, раскрытие информации, отказ в обслуживании и несанкционированное получение прав (STRIDE). В веб-форм ASP.NET можно добавить точек расширения и параметры конфигурации, которые позволяют настраивать различные возможности безопасности в веб-форм ASP.NET.
- **Производительность**-производительность может быть ключевым фактором успеха веб-узла или проекта. Веб-формы ASP.NET позволяет изменять производительности, относящиеся к странице и обработки сервером управления, управление состоянием, доступ к данным, конфигурации приложения и загрузка и эффективных методов программирования.
- **Интернационализация**— веб-форм ASP.NET позволяет создавать веб-страниц, которые можно получить, содержимого и других данных на языке, выбранном для браузера на основе или явного выбора пользователем языка. Содержимое и другие данные, называется ресурсы и такие данные могут храниться в файлах ресурсов или других источников. На странице веб-форм ASP.NET настроить элементы управления для получения значений свойств из ресурсов. Во время выполнения выражения ресурсов заменяются ресурсы из соответствующего локализованного файла ресурсов.
- **Отладка и обработка ошибок**-ASP.NET включает в себя функции, которые помогут вам диагностировать проблемы, которые могут возникнуть в приложении Web Forms. Отладка и обработка ошибок также поддерживаются в веб-форм ASP.NET, чтобы ваши приложения, компиляции и ее выполнение.
- **Развертывания и размещения**-Visual Studio, ASP.NET, Azure и службы IIS предоставляют средства, помогающие в процессе развертывания и размещения приложения веб-форм.

## <a name="deciding-when-to-create-a-web-forms-application"></a>Когда необходимо создавать в приложениях Web Forms

Необходимо внимательно рассмотреть ли для реализации веб-приложения с помощью ASP.NET Web Forms модели или другой модели, такие как платформа ASP.NET MVC. Платформа MVC не заменяет модели веб-форм; Обе модели можно использовать для веб-приложений. Прежде чем использовать модель веб-форм или MVC framework для определенного веб-сайта, взвесить все преимущества каждого подхода.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Преимущества веб-приложения на веб-форм

Платформа на основе веб-форм имеет следующие преимущества:

- Она поддерживает модель событий, которая сохраняет состояние по протоколу HTTP, что выгодно для разработки бизнес-веб-приложений. Приложения на основе веб-форм предоставляет множество событий, которые поддерживаются в сотни серверных элементов управления.
- Она использует шаблон контроллера страницы, добавляющий функции к отдельным страницам. Дополнительные сведения см. в разделе [контроллера страницы](https://go.microsoft.com/fwlink/?LinkId=106359 "контроллера страницы") на веб-сайте MSDN.
- Она использует состояние представления или формы на основе сервера, которые может облегчить управление информацией о состоянии.
- Он хорошо подходит для небольших коллективов веб-разработчиков, желающих воспользоваться преимуществами большое число компонентов, доступных для быстрой разработки приложений.
- Как правило, менее сложна для разработки приложений, так как компоненты ( **страницы** класса элементов управления и т. д.) тесно интегрированы и требуют меньшего объема кода, чем в модели MVC.

### <a name="advantages-of-an-mvc-based-web-application"></a>Преимущества MVC веб-приложения

Платформа ASP.NET MVC предоставляет следующие преимущества:

- Он облегчает управление сложными структурами путем разделения приложения на модель, представление и контроллер.
- Он не использует состояние просмотра или серверные формы. Это делает платформу MVC идеальной для разработчиков, которым необходим полный контроль над поведением приложения.
- Она использует схему основного контроллера, который обрабатывает запросы веб-приложений через один контроллер. Это позволяет создать приложение, которое поддерживает расширенную инфраструктуру маршрутизации. Дополнительные сведения см. в разделе [интерфейсного контроллера](https://go.microsoft.com/fwlink/?LinkId=106357 "интерфейсного контроллера") на сайте MSDN.
- Он обеспечивает лучшую поддержку для разработки приложений на основе тестирования (TDD).
- Он хорошо подходит для веб-приложений, поддерживаемых крупными коллективами разработчиков и дизайнеров, которым требуется высокая степень контроля над поведением приложения.