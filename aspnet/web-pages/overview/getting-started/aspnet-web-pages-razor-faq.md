---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET веб-страниц (Razor) часто задаваемые вопросы Документы Майкрософт
author: Rick-Anderson
description: В этой статье перечислены некоторые часто задаваемые вопросы о ASP.NET веб-страниц (Razor) и WebMatrix. Версии программного обеспечения, используемые в учебнике ASP.NET веб-страниц (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543708"
---
# <a name="aspnet-web-pages-razor-faq"></a>Вопросы и ответы по веб-страницам ASP.NET (Razor)

; автор — [Том ФитцМакен (Tom FitzMacken)](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix больше не рекомендуется в качестве интегрированной среды разработки для ASP.NET web-страниц. Используйте [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) или [визуальный код студии](https://code.visualstudio.com/).
>
> В этой статье перечислены некоторые часто задаваемые вопросы о ASP.NET веб-страниц (Razor) и WebMatrix.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в учебнике
> 
> 
> - ASP.NET веб-страниц (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Этот учебник также работает с ASP.NET web Pages 2, WebMatrix 2 и Visual Studio 2012.

- [В чем разница между веб-страницами ASP.NET, ASP.NET веб-формами и ASP.NET MVC?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Нужен ли мне WebMatrix для работы с веб-страницами?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Могу ли я использовать элементы управления веб-ASP.NET веб-формами на странице Веб-страницы?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [Могу ли я развернуть веб-сайт ASP.NET без использования WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Должен ли я использовать помощника WebSecurity для поддержки логинов?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [Поддерживает ли ASP.NET веб-страниц HTML5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Могу ли я использовать JavaScript и j'еry с веб-страницами?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Дополнительные ресурсы](#AdditionalResources)

Для вопросов об ошибках и других проблемах, см [ASP.NET веб-страниц (Razor) Устранение неполадок Руководство](https://go.microsoft.com/fwlink/?LinkId=253001).

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>В чем разница между веб-страницами ASP.NET, ASP.NET веб-формами и ASP.NET MVC?

Все три ASP.NET технологии для создания динамических веб-приложений:

- ASP.NET Web Pages фокусируется на добавлении динамического (серверного) кода и доступа к базе данных к HTML-страницам, а также имеет простой и легкий синтаксис.
- ASP.NET Web Forms основан на модели объекта страницы и традиционных элементах управления типом окна (кнопки, списки и т.д.). Web Forms использует модель, основанную на событиях, знакомую тем, кто работал с разработкой на основе клиентов (Windows forms).
- ASP.NET MVC реализует шаблон модели-вид-контроллер для ASP.NET. Акцент делается на "разделение проблем" (обработка, данные и слои uI).

Все три структуры полностью поддерживаются и продолжают разрабатываться ASP.NET группой. В общем, выбор, какие рамки использовать зависит от вашего фона и опыта работы с ASP.NET.

ASP.NET веб-страниц, в частности, был разработан, чтобы сделать его легким для людей, которые уже знают HTML, чтобы добавить обработку сервера на свои страницы. Это хороший выбор для студентов, любителей, людей в целом, которые являются новыми для программирования. Он также может быть хорошим выбором для разработчиков, которые имеют опыт работы с non-ASP.NET веб-технологий.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Нужен ли мне WebMatrix для работы с веб-страницами?

Нет. WebMatrix больше не рекомендуется в качестве интегрированной среды разработки для ASP.NET web-страниц. Используйте [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) или [визуальный код студии](https://code.visualstudio.com/).

Если вы не хотите использовать visual Studio или Visual Studio Code, вы можете установить компоненты индивидуально с помощью [установки веб-платформы Майкрософт.](https://www.microsoft.com/web/downloads/platform.aspx) Вам нужны следующие продукты:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (который также устанавливает ASP.NET веб-страницы)
- IIS Express (веб-сервер)
- Компакт серверный сервер Microsoft S'L 4.0 (база данных)

Вы можете использовать текстовый редактор для редактирования *страниц .cshtml* (или *.vbhtml).*

Управление базами данных S'L Server Compact (*файлы .sdf)* без инструмента немного сложнее. Visual Studio содержит инструменты для управления базами данных *.sdf.* Вы также можете запустить команды в коде для выполнения многих задач управления сервером S'L.

Для тестирования страниц *.cshtml* без использования интегрированной среды разработки (IDE) можно развернуть их на живой сервер. (См. [Могу ли я развернуть веб-сайт ASP.NET без использования WebMatrix?)](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)

### <a name="running-iis-express-without-using-an-ide"></a>Запуск IIS Express без использования IDE

Если вы установите IIS Express на свой компьютер в качестве веб-сервера, вы можете использовать его для тестирования страниц. Вы можете запустить IIS Express из командной строки и связать его с определенным номером порта. Затем вы указываете этот порт при запросе файлов *.cshtml* в вашем браузере.

В Windows откройте запрос команды с привилегиями администратора и измените его на *C:'Program Files.IIS Express.* (Для 64-разрядных систем используйте папку *C: «Файлы программы »(x86)»IIS Express.)* Затем введите следующую команду, используя фактический путь к вашему сайту:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Вы можете использовать любой номер порта, который еще не зарезервирован каким-либо другим процессом. (Номера порта выше 1024, как правило, бесплатны.) Для `path` значения используйте путь папки веб-сайта, где находятся файлы *.cshtml.*

После запуска этой команды для настройки IIS Express для обслуживания ваших страниц можно открыть браузер и просмотреть файл *.cshtml.* Используйте URL,как следующее:

`http://localhost:35896/default.cshtml`

Для получения помощи с вариантами `iisexpress.exe /?` командной строки IIS Express введите на командной строке.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Могу ли я использовать элементы управления веб-ASP.NET веб-формами на странице Веб-страницы?

Нет. Элементы управления web Forms, такие как контроль [CheckBox,](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) [элементы управления проверки](https://msdn.microsoft.com/library/bwd43d0x)и управление [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) работают только на страницах Web Forms *(файлы .aspx).* Эти элементы управления требуют платформы страницы Web Forms.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>Могу ли я развернуть веб-сайт ASP.NET без использования WebMatrix?

Да. Вы можете вручную копировать файлы веб-сайта на сервер (обычно с помощью FTP). Если вы выполняете ручную копию, вы также должны скопировать файлы, которые поддерживают S'L Server Compact (база данных). Для получения подробной информации смотрите запись в блоге [Развертывание веб-страниц приложений без инструмента](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Должен ли я использовать помощника WebSecurity для поддержки логинов?

Нет. Одним `SimpleMembership` из вариантов является поставщик, врамкахный ASP.NET web-страниц. Поставщики безопасности, которые являются частью ASP.NET (с которыми вы могли бы работать в веб-формах), также доступны. Например, вы можете использовать проверку подлинности форм в ASP.NET веб-страниц так же, как в Web-формах. В качестве примера использования аутентификации форм можно ознакомиться в статье поддержки Майкрософт [«Как реализовать проверку подлинности на основе форм в вашем ASP.NET приложении с помощью C'.NET](https://support.microsoft.com/kb/301240). Чтобы загрузить простой пример, [см. &amp; ASP.NET версию "Логин пароль](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Для получения информации о том, как использовать проверку подлинности Windows, смотрите запись в блоге [с помощью проверки подлинности Windows в ASP.NET веб-страниц.](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>Поддерживает ли ASP.NET веб-страниц HTML5?

Да. Страницы, создаваемые с помощью веб-страниц ASP.NET *(страницы .cshtml* или *.vbhtml),* по существу являются HTML-страницами, которые также содержат код, который работает на сервере, до того, как страница будет отрисована. Пока браузер пользователя поддерживает HTML5, вы можете использовать элементы HTML5 на странице *.cshtml* или *.vbhtml.*

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Могу ли я использовать JavaScript и j'еry с веб-страницами?

Конечно. Страницы, которые вы создаете с помощью веб-страниц ASP.NET *(страницы .cshtml* или *.vbhtml)* являются просто HTML-страницами с кодом сервера. Таким образом, все, что вы можете сделать в обычной странице HTML, используя JavaScript или j'sry вы также можете сделать в *.cshtml* или *.vbhtml* странице.

Шаблон **стартового сайта** в WebMatrix содержит ряд библиотек j'ery. Если вы создаете сайт, используя этот шаблон, папка *Скриптов* содержит основную библиотеку j'ery *(jquery-1.6.2.js)* и библиотеки для проверки j'ery *(jquery.validate.js*и т.д.).

Вот некоторые сообщения в блоге, которые иллюстрируют способы использования j'ery с ASP.NET веб-страниц:

- [Добавление J'S'ry Добра к ASP.NET веб-страниц с помощью WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Рейчел Аппель
- [5 мин. Веб-Матрика и J'Ui j'ury - Json и j'ury шаблоны](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) Джонаса Эрикссона
- [WebMatrix и J'Ury формы](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) Майк Бринд

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

[Руководство по устранению неполадок веб-страниц ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253001)

[WebMatrix и форум веб-страниц ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix) на веб-сайте ASP.NET
